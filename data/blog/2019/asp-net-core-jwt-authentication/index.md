---
title: ASP.NET Core 使用 JWT 驗證 
summary: ASP.NET Core 使用 JWT 驗證
date: 2019-04-27 11:09:50.61+08:00
tags: [ asp.net core , jwt ]
draft: false
---

JWT 是前後端分離常使用的驗證方式，來看怎麼在 ASP.NET Core 裡面很簡單的加上這個驗證

> ASP.NET Core 2.2

## 安裝套件

- [System.IdentityModel.Tokens.Jwt](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt/)
- [Microsoft.AspNetCore.Authentication.JwtBearer](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.JwtBearer/)

## JWT 設定

- 在 `Startup` 的 `ConfigureServices` 加入 `AddAuthentication`，`DefaultAuthenticateScheme` 和 `DefaultChallengeScheme` 都設置成 `JwtBearerDefaults.AuthenticationScheme`

- 在 `AddAuthentication` 後面加入 `AddJwtBearer`，設置 JWT 的設定，下面三個個設定記得換成自己的設定值，基本上這個三設定值也都會驗證，所以相關的 Validate 設定都設成 true
	- SymmetricSecurityKey
	- ValidIssuer
	- ValidAudience
- 這裡的 `IssuerSigningKey` 是簽章用的 Key，一定不能外流，記得換成自己的

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddAuthentication(options =>
            {
                options.DefaultAuthenticateScheme = JwtBearerDefaults.AuthenticationScheme;
                options.DefaultChallengeScheme = JwtBearerDefaults.AuthenticationScheme;
            })
            .AddJwtBearer(options =>
            {
                options.TokenValidationParameters = new TokenValidationParameters
                {
                    ValidateIssuerSigningKey = true,
                    IssuerSigningKey =
                            new SymmetricSecurityKey(Encoding.UTF8.GetBytes("123730a1-1e99-428b-9f6d-9f3ed4021234")), // Key
                    ValidateIssuer = true,
                    ValidIssuer = "CashUser", // 簽發者
                    ValidateAudience = true,
                    ValidAudience = "CashAudience", // 接收者
                    ValidateLifetime = true, // 驗證時間
                    RequireExpirationTime = true, // 是不是有過期時間
                    ClockSkew = TimeSpan.Zero // 時間偏移
                };
            });
}

```

- 在 `Startup` 的 `Configure` 記得啟用驗證 `UseAuthentication`
	- 記得有順序性的問題，`UseAuthentication` 之後的 Middleware 就都要驗證也可以使用

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseAuthentication();

    app.UseMvc(routes =>
    {
        routes.MapRoute(name: "default",
                        template: "{controller=Home}/{action=Index}/{id?}");
    });
}
```

## Token Action

- 寫一個 Action 來取得 Token
- `Claim` 指的是你的資料或者說是你給出去的權限也行，如果沒有特殊的要求這個可以先不給，之前講群組的時候就會用到
- 下面三個設定值記得要跟在 `Startup` 裡面設定的一樣，不然就沒月辦法通過驗證的
	- securityKey
	- issuer
	- audience

- 過期時間一般是設定成 30 分鐘，建議不要設定的太大

```csharp
[HttpGet]
public IActionResult JwtToken()
{
    var claims = new List<Claim>
    {
        new Claim(ClaimTypes.Name, "cash")
    };

    var securityKey = "123730a1-1e99-428b-9f6d-9f3ed4021234";

    var token = new JwtSecurityToken(new JwtHeader(new SigningCredentials(new SymmetricSecurityKey(Encoding.UTF8.GetBytes(securityKey)),
                                                                          SecurityAlgorithms.HmacSha256)),
                                     new JwtPayload(issuer: "CashUser",
                                                    audience: "CashAudience",
                                                    claims: claims,
                                                    notBefore: DateTime.UtcNow,
                                                    expires: DateTime.UtcNow.AddMinutes(30)));

    var tokenStr = new JwtSecurityTokenHandler().WriteToken(token);

    return Json(new { Token = tokenStr });
}
```

## 測試 Token

- 實際執行 Action，就可以拿到 Token

![](/static/images/404.webp)

- 可以到 [jwt.io](https://jwt.io/) 這個網站，把自己的 Token 貼進去，在右邊就可以看到 Token 的內容

![](/static/images/404.webp)

- 如果滑鼠移到參考或是值上面的話，會有提示，而且日期也會轉成本地的時間

![](/static/images/404.webp)

## Authorize Action

- 寫一個需要被驗證的 Action，其實也是在 Action 上面加上 `Authorize` 的 attribute 而已

```csharp
[Authorize]
[HttpGet]
public IActionResult GetData()
{
    return Json(new { Data = 123 });
}
```

## 測試 Authorize Action

- 直接呼叫 `GetData` 的話就會回傳 `401`，然後會在 Header 裡面跟你說驗證的內容是使用 `Bearer`

![](/static/images/404.webp)

- 把產生出來的 Token 加到呼叫的 Header 裡面，這樣子就可以拿到資料了
	- Key 是 `Authorization`
	- Value 是 `Bearer Token內容`，記得中間有個空白

![](/static/images/404.webp)