---
title: Shell - 把 zip 替換成 7z
description: 因為之前存檔 (備份) 的檔案有蠻多都是 zip 的，想說可不可以一次把它換成 7z 的檔案
date: 2024-03-09
slug: "shell-covert-zip-to-7z"
tags: [ shell ]
draft: false
---

![](./cover.webp)

因為之前存檔 (備份) 的檔案有蠻多都是 `zip` 的，想說可不可以一次把它換成 `7z` 的檔案，於是就有這篇文章

我記得好像也是問 `GPT` 的，只是我找不到對話記錄

```shell
#!/bin/bash

# 檢查是否安裝了 7z
if ! command -v 7zz &> /dev/null; then
    echo "錯誤：未安裝 7z。請先安裝 7z 後再運行此腳本。"
    exit 1
fi

# 定位到包含 ZIP 檔案的資料夾
#cd /path/to/directory

# 尋找所有的 ZIP 檔案並進行處理
for file in *.zip; do
    # 確保檔案存在
    if [[ -f "$file" ]]; then
        # 解壓縮 ZIP 檔案
        unzip "$file"

        # 移除副檔名，獲得檔案名稱
        filename=$(basename "$file" .zip)

        # 使用 7z 壓縮，壓縮率設為最高
        7zz a -t7z -mx=9 "$filename.7z" "$filename"

        # 測試壓縮檔案的完整性
        if 7zz t "$filename.7z"; then
            echo "7z 檔案測試通過：$filename.7z"

            # 刪除原始 ZIP 檔案和解壓縮後的檔案/資料夾
            rm -r "$file" "$filename"
        else
            echo "警告：7z 檔案測試失敗：$filename.7z，保留原始 ZIP 檔案。"
        fi
    fi
done
```

> Photo by [Michal Balog](https://unsplash.com/@mikbutcher?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash) on [Unsplash](https://unsplash.com/photos/brown-cardboard-boxes-on-brown-wooden-table-66NaCdBrkCs?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash)