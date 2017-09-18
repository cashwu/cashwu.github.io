---
title: 'C# 6 Null Conditional Operator'
tags:
  - 'c#'
categories: []
date: 2015-06-15 08:00:00
---

## Before C# 6

```csharp
static void Main( string[ ] args )  
{ 
    Employee emp = null; 
    if(emp != null)
    {
        Console.WriteLine( emp.EmpName );   
    }
}

class Employee  
{ 
    public string EmpName; 
} 
```

## C# 6

```csharp
static void Main( string[ ] args )  
{ 
    Employee emp = null; 
    Console.WriteLine( emp?.EmpName );  
}

class Employee  
{ 
    public string EmpName; 
} 
```

## Before C# 6

```csharp
static void Main( string[ ] args )  
{ 
    Employee emp = null; 
    var name = emp != null ? emp.EmpName : "NoName";
    Console.WriteLine( name );   
}

class Employee  
{ 
    public string EmpName; 
} 
```

## C# 6

```csharp
static void Main( string[ ] args )  
{ 
    Employee emp = null; 
    var name = emp?.EmpName ?? "NoName";
    Console.WriteLine( name );   
}

class Employee  
{ 
    public string EmpName; 
} 
```