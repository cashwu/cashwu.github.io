---
title: Python - 傳遞 function 到另外一個 function 當成參數
description: 在 c# 裡面有很方便的 Func, Action 可以當成參數傳遞到另外一個方法裡面執行，就在找 python 裡面有沒有類似的寫法可以傳遞一個方法到另外一個方法執行
date: 2018-12-12 09:55:52.945+08:00
slug: "python-pass-function-as-argument-to-another-function"
tags: [ python ]
---

在 c# 裡面有很方便的 Func, Action 可以當成參數傳遞到另外一個方法裡面執行，就在找 python 裡面有沒有類似的寫法可以傳遞一個方法到另外一個方法執行

- 有一個 Calculator  類別，裡面有一個 operation 的 static 方法

```python
class Calculator:

    @staticmethod
    def operation(x, y, func):
        return func(x, y)
```

- 可以在方法裡面在寫一個方法，然後用這個 inner function 傳遞

```python
class CalculatorTest(unittest.TestCase):

    def test_operation(self):

        def plus(x, y):
            return x + y

        result = Calculator.operation(1, 2, plus)
        self.assertEqual(3, result)
```

- 可以使用 lambda 的方式傳遞

```python
class CalculatorTest(unittest.TestCase):

        result = Calculator.operation(2, 2, lambda x, y: x + y)
        self.assertEqual(4, result)
```

> 青菜蘿蔔各有所好，就視情況使用不同的方法吧 !!