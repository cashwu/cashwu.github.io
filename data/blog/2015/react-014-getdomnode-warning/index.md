---
title: React - 0.14 getDOMNode Warning
description: React Warning - ReactDOMComponent - Do not access .getDOMNode() of a DOM node; instead, use the node directly. This DOM node was rendered by MyForm.
date: 2015-12-26 20:08:42.794+08:00
slug: "react-014-getdomnode-warning"
tags: [ js , react ]
---

## 問題

跟著 React 書上的範例操作時，發現出現下面的 Warning

> Warning: ReactDOMComponent: Do not access .getDOMNode() of a DOM node; instead, use the node directly. This DOM node was rendered by MyForm.

```js
/*input 輸入資料後，按下 Button，Alert 輸入的資料*/
var MyForm = React.createClass({  
    submitHandler: function(event){
        event.preventDefault();

        var hellotTo = this.refs.hellotTo.getDOMNode().value;
        alert(hellotTo);
    },
    render: function(){
        return(
            <form onSubmit={this.submitHandler}>
                <input ref="hellotTo" type="text" defaultValue="Hello World!" />
                <br/ >
                <button type="submit">Speak</button>
            </form>
        );
    }
});
```

## 原因

React v0.14 把 getDOMNode() deprecated 了

## 解法

不用 getDOMNode() 就好，所以上面的程式修改成：

```js
var hellotTo = this.refs.hellotTo.value;  
```

### 參考網站

- [New deprecations, introduced with a warning](http://facebook.github.io/react/blog/2015/10/07/react-v0.14.html#new-deprecations-introduced-with-a-warning)
- [ERROR-3:React](http://my.oschina.net/wuguzi/?disp=2&p=1&catalog=3407299)