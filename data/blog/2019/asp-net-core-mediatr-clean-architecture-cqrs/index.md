---
title: ASP.NET Core 使用 MediatR 簡單的實現 Clean Architecture、CQRS 和分層架構
summary: ASP.NET Core 使用 MediatR 簡單的實現 Clean Architecture、CQRS 和分層架構
date: 2019-04-21 10:14:23.425+08:00
tags: [ asp.net core , clean architecture , cqrs , mediatr ]
draft: false
---

在原本正在運行的專案已經導入 Clean Architecture 的架構和實作，不過在看到了 [Clean Architecture with ASP.NET Core 2.1](https://www.youtube.com/watch?v=_lwCVE_XgqI) 這個分享後，覺得這個架構的實作比自己寫的還要漂亮，所以慢慢的把這個分享的東西導入到自己的架構裡面

今天要分享的是使用 [`MediatR`](https://github.com/jbogard/MediatR) 這個套件，可以簡單的做到 CQRS 和架構上的分層

> 範例使用 ASP.NET Core 2.2 MVC 範本
> Repository 在 [Github](https://github.com/cashwublog/TestMediatR)

- 先建立一個 `ASP.NET Core 2.2 MVC` 的專案 (`TestMediatR`)，然後再同一個 solution 下面再建立二個 `.NETCoreApp v2.2` 的 Library (`BusinessLogic` 和 `DataAssert`)，相關的專案 reference 如下圖
	- TestMediatR -> BusinessLogic -> DataAssert

![](/static/images/404.webp)

## 建置 DataAssert

> 為了測試方便，在這裡使用的是 `InMemory` 的 Database，實務上請換成自己使用的 Database 和相關的套件

- DataAssert 加入 `EntityFrameworkCore` 的套件 (沒意外的話版號跟 .NET Core 的版號要一樣)
	- [Microsoft.EntityFrameworkCore](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore/)
	- [Microsoft.EntityFrameworkCore.InMemory](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.InMemory)

- 建立 `AppDbContext`

```csharp
public class AppDbContext : DbContext
{
    public AppDbContext(DbContextOptions<AppDbContext> options)
            : base(options)
    {
    }

    public DbSet<Person> Person { get; set; }
}
```

- 建立 `Person`

```csharp
public class Person
{
    public int Id { get; set; }

    public string Name { get; set; }
}
```

- 在 `TestMediatR` 專案加入 `AppDbContext`

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDbContext<AppDbContext>(options =>
    {
        options.UseInMemoryDatabase("TestMediatR");
    });

    services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
}
```

## 建置新增 Person 的 BusinessLogic

- DataAssert 專案加入 `MediatR` 的套件
	- [MediatR.Extensions.Microsoft.DependencyInjection](https://www.nuget.org/packages/MediatR.Extensions.Microsoft.DependencyInjection/)

- 建立 `AddPersonCommand`，實作 MediatR 的 `IRequest`，沒有回傳值的話可以不用寫泛型參數

```csharp
public class AddPersonCommand : IRequest
{
    public int Id { get; set; }

    public string Name { get; set; }
}
```

- 建立 `AddPersonCommandHandler`，來處理 `AddPersonCommand`，需要實作 MediatR 的 `IRequestHandler`，會需要實作一個 `Handle` 的方法，方法第一個參數就是實作 IRequest 的類別 (第一個泛型參數)
	- 第一個泛型參數是實作 IRequest 的 `AddPersonCommand`
	- 第二個泛型參數是回傳值，沒有的話就給 `Unit`
		- `Unit` 這是 MediatR 的內建型別，給無回傳值時使用

```csharp
public class AddPersonCommandHandler : IRequestHandler<AddPersonCommand, Unit>
{
    public Task<Unit> Handle(AddPersonCommand request, CancellationToken cancellationToken)
    {
        throw new System.NotImplementedException();
    }
}
```

- 實作 `AddPersonCommandHandler` 的內容，把傳入值轉成 Person，然後加到 DB 裡面，因為要回傳 `Unit`，可以使用`Unit.Value`當成回傳值

```csharp
public class AddPersonCommandHandler : IRequestHandler<AddPersonCommand, Unit>
{
    private readonly AppDbContext _dbContext;

    public AddPersonCommandHandler(AppDbContext dbContext)
    {
        _dbContext = dbContext;
    }

    public async Task<Unit> Handle(AddPersonCommand request, CancellationToken cancellationToken)
    {
        var person = new Person { Id = request.Id, Name = request.Name };
        await _dbContext.Person.AddAsync(person, cancellationToken);
        await _dbContext.SaveChangesAsync(cancellationToken);

        return Unit.Value;
    }
}
```

- 在 `TestMediatR` 專案註冊 `MediatR`
	- 如果是放在不同的專案，可以給那個專案的 `Assembly` name，同專案的話，基本上就不用加

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMediatR(typeof(AddPersonCommand).GetTypeInfo().Assembly);
}
```

## 建置 MVC

- 增加 `PersonController`，可以在 `constructor` 的時候注入 `IMediator` 使用

```csharp
[Route("api/[controller]/[action]")]
public class PersonController : Controller
{
    private readonly IMediator _mediator;

    public PersonController(IMediator mediator)
    {
        _mediator = mediator;
    }
}
```

- 增加 `Add` Action，傳入參數就是在 BusinessLogic 裡面新增的 `AddPersonCommand`，然後使用 Mediator 的 `Send` 方法，把需要處理的物件丟進去 (也就是實作 `IRequest` 的物件)，因為沒有回傳值，就直接 await 它就好

```csharp
[Route("api/[controller]/[action]")]
public class PersonController : Controller
{
    private readonly IMediator _mediator;

    public PersonController(IMediator mediator)
    {
        _mediator = mediator;
    }

    [HttpPost]
    public async Task<IActionResult> Add(AddPersonCommand command)
    {
        await _mediator.Send(command);
        return Ok();
    }
}
```

- 實際測試

![](/static/images/404.webp)

## 建置查詢 Person 的 BusinessLogic

- 建立查詢的回傳物件 `PersonQueryResponse`

```csharp
public class PersonQueryResponse
{
    public PersonQueryResponse(Person person)
    {
        Person = person;
    }

    public Person Person { get; private set; }
}
```

- 建立 `PersonQuery`，實作 MediatR 的 `IRequest`，泛型參數為回傳型別 `PersonQueryResponse`

```csharp
public class PersonQuery : IRequest<PersonQueryResponse>
{
    public int Id { get; set; }
}
```

- 建立 `PersonQueryHandler` 處理 `PersonQuery`
	- 第一個泛型參數是實作 IRequest 的 `PersonQuery`
	- 第二個泛型參數是回傳值 `PersonQueryResponse`

> 注意 : 如果 PersonQuery 的泛型參數和 PersonQueryHandler 第二個泛型參數不一致時會報錯

```csharp
public class PersonQueryHandler : IRequestHandler<PersonQuery, PersonQueryResponse>
{
    public Task<PersonQueryResponse> Handle(PersonQuery request, CancellationToken cancellationToken)
    {
        throw new System.NotImplementedException();
    }
}
```

- 實作 `PersonQueryHandler` 的內容，從 DB 查詢到資料然後回傳

```csharp
public class PersonQueryHandler : IRequestHandler<PersonQuery, PersonQueryResponse>
{
    private readonly AppDbContext _dbContext;

    public PersonQueryHandler(AppDbContext dbContext)
    {
        _dbContext = dbContext;
    }

    public async Task<PersonQueryResponse> Handle(PersonQuery request, CancellationToken cancellationToken)
    {
        var person = await _dbContext.Person.FirstOrDefaultAsync(a => a.Id == request.Id, cancellationToken);

        return new PersonQueryResponse(person);
    }
}
```

## 建置查詢 Person 的 Action

- 建立 `Query` Action

```csharp
[HttpPost]
public async Task<IActionResult> Query(PersonQuery query)
{
    return Ok(await _mediator.Send(query));
}
```

- 實際測試

![](/static/images/404.webp)

## 後記

原本我們都會寫在 Action 裡面的程式碼，利用 `MediatR` 這個套件，就可以簡單的作到把程式碼移到另外一個 Library 裡面，也可以從 Request 的 DTO 物件就實現了程式碼的 `CQRS`，不過如果還要作到影片中的 Clean Architecture 的話，以這個範例還有一段距離，有機會的話在來分享，有興趣的人也建議可以把影片看一次，應該會學到蠻多東西的。