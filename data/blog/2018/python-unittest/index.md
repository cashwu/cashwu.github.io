---
title: Python - 單元測試
summary: Python 單元測試
date: 2018-12-12 09:00:35.197+08:00
tags: [ python ]
draft: false
---

> PyCharm 2018.3.1

- 在專案上按右鍵，新增一個 python 檔案，選擇 unit test

![](/static/images/404.webp)

![](/static/images/404.webp)

- 新增出來的檔案會有一個預設的測試範本

![](/static/images/404.webp)

- 在測試裡面新增一個類別

```python
class Calculator:

    @staticmethod
    def plus(x, y):
        return x + y
```

- 修改測試去測它，需要注意的是，`def` 的測試方法名稱要是 `test` 開頭才會被視為測試

```python
class CalculatorTests(unittest.TestCase):
    def test_plus(self):
        result = Calculator.plus(1, 2)
        self.assertEqual(3, result)
```

- 所需要的測試方法都在 `self` 裡面

![](/static/images/404.webp)

> 比較不解的是，參數都是用 first 和 second 來當名稱，是不是用 expected 和 actual 會比較好一點，不過不意外的是前面的參數 (first) 是 expected