---
title: Shell - 同步 Git remote 下面的所有分支到另外一個新的 remote
description: 這是一個很神奇的需求，要把一個遠端 remote 下面的所有分支，推到一個新的 remote 分支
date: 2024-03-16
slug: "git-sync-remote-all-branch-to-another-remote-using-shell"
tags: [ shell, git ]
# tldr: Making GitHub Actions with Js Code
draft: false
---

![](./cover.webp)

這是一個很神奇的需求，要把一個遠端 remote 下面的所有分支，推到一個新的 remote 分支，會這樣子做的原因主要有兩個

- 我本機上已經有舊的 remote 部份分支的改動 commit 
- 舊的 remote 分支太多

於是又跟 ChatGPT pair 寫 Shell 來完成這次的任務 😂

```shell
#!/bin/bash

#指定要列出的 remote 名稱
remote_name="old_origin"

# 指定要推送到的 remote 名稱
push_remote_name="origin"

# 用於存儲推送失敗的分支名稱
failed_branches=()

# 取得 repository 的指定 remote 的 branch
git branch -r | grep "$remote_name" | sed 's/^[[:space:]]*//' | while read branch; do

    # 檢查本地是否已經有這個分支，如果沒有就建立
    local_branch="${branch#*/}"

    echo "current branch: $local_branch"

    if ! git rev-parse --verify "$local_branch" >/dev/null 2>&1; then
        echo "Creating local branch: $local_branch"
        git checkout -b "$local_branch" "$branch"
    else
        echo "Checking out local branch: $local_branch"
        git checkout "$local_branch"
    fi

    # 推送到指定的 remote 上
    echo "Pushing branch: $local_branch to remote: $push_remote_name"

    if git push "$push_remote_name" "$local_branch"; then
        echo "Push successful"
    else
        echo "Push failed"
        failed_branches+=("$local_branch")
    fi
done

# 列出推送失敗的分支
if [ ${#failed_branches[@]} -gt 0 ]; then
    echo "The following branches failed to push:"
    for branch in "${failed_branches[@]}"; do
        echo "$branch"
    done
fi
```

> Photo by [Yancy Min](https://unsplash.com/@yancymin?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash) on [Unsplash](https://unsplash.com/photos/a-close-up-of-a-text-description-on-a-computer-screen-842ofHC6MaI?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash)