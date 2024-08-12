---
title: C# - 6.0 Null Conditional Operator
description: C# 6.0 Null Conditional Operator
date: 2015-06-15 22:10:59.602+08:00
slug: "csharp-6-null-conditional-operator"
tags:  [ c# ]
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

---

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