---
title: React - JSX Set Property
description: React JSX Set Property
date: 2015-12-24 20:14:28.398+08:00
slug: "react-jsx-set-property"
tags:  [ js,react ]
---

如果 JSX 的屬性需要使用條件判斷來設值的話，用下面的寫法會 render 出無效的 javascript

```js
<div className={ if(isComplete){ "is-complete" } } >...</div>  
```

解決的方式可以使用下面其中一個方法：

- 使用三元運算式
- 設置一個變數，並在屬性中使用
- 將邏輯寫到函數中
- 使用 &&

### 使用三元運算式

```js
render : function(){  
    return <div className = {
        this.state.isComplete ? "is-complete" : ""
    } >...</div>;
}
```

### 使用變數

```js
getIsComplete : function() {  
    return this.state.isComplete ? "is-complete" : "";
}

render : function(){  
    var isComplete = this.getIsComplete();
    return <div className = {isComplete} >...</div>;
}
```

### 使用函數

```js
getIsComplete : function() {  
    return this.state.isComplete ? "is-complete" : "";
}

render : function(){  
    return <div className = { this.getIsComplete() } >...</div>;
}
```

### 使用 &&

```js
render : function(){  
    return <div className = { this.state.isComplete && "is-complete" } >...</div>;
}
```