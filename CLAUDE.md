# CLAUDE.md

此檔案為 Claude Code (claude.ai/code) 在此程式碼庫中工作時提供指導。

## 專案概述

這是一個使用 Next.js、TypeScript 和 Tailwind CSS 建置的個人部落格系統。它基於「Tailwind Next.js Starter Blog」模板，並使用 Contentlayer 進行內容管理。部落格以正體中文（zh-tw）撰寫，專注於程式設計和技術主題。

## 核心架構

### 內容管理

- **Contentlayer**：以類型安全的方式管理 MDX 內容
- **部落格文章**：位於 `data/blog/` 目錄，按年份組織
- **作者**：位於 `data/authors/` 目錄（default.mdx 是主要作者）
- **內容類型**：部落格文章和作者資料在 `contentlayer.config.ts` 中定義
- **Frontmatter**：支援標題、日期、標籤、草稿狀態、摘要、圖片、作者、版面配置等

### 路由和頁面

- **App Router**：使用 Next.js 13+ App Router 模式
- **動態路由**：部落格文章使用 `app/blog/[...slug]/page.tsx` 進行嵌套路由
- **靜態生成**：所有部落格文章在建置時進行靜態生成
- **版面配置**：提供三種文章版面配置（PostLayout、PostSimple、PostBanner）

### 內容處理

- **MDX 外掛**：配置 remark 和 rehype 外掛以增強 markdown 處理
- **語法高亮**：使用 rehype-prism-plus 提供行號
- **數學渲染**：KaTeX 支援數學表達式
- **圖片優化**：Next.js Image 元件支援 image.cashwu.com 遠端圖片
- **目錄**：自動從標題生成目錄

## 開發指令

```bash
# 安裝相依套件
yarn

# 開發伺服器
yarn dev

# 建置生產版本
yarn build

# 啟動生產伺服器
yarn serve

# 程式碼檢查
yarn lint

# 分析套件大小
yarn analyze
```

## 網站配置

### 主要配置檔案

- `data/siteMetadata.js`：網站元資料、分析、評論、搜尋配置
- `contentlayer.config.ts`：內容層配置和 MDX 外掛
- `next.config.js`：Next.js 配置（含安全標頭和 CSP）
- `tailwind.config.js`：Tailwind CSS 配置

### 關鍵設定

- **語言**：正體中文（zh-tw）
- **主題**：預設深色模式
- **分析**：已配置 Umami 分析
- **搜尋**：使用 Kbar 搜尋提供者
- **評論**：Giscus 配置可用但未啟用
- **圖片**：允許來自 image.cashwu.com 網域的遠端圖片

## 內容結構

### 部落格文章

- **位置**：`data/blog/` 以年份為基礎的組織
- **格式**：帶有 frontmatter 的 MDX 檔案
- **必填欄位**：title、date
- **選填欄位**：tags、lastmod、draft、summary、images、authors、layout、canonicalUrl
- **草稿**：帶有 `draft: true` 的文章會在生產建置中被排除

### 版面配置

- **PostLayout**：預設雙欄版面配置，包含元資料和導航
- **PostSimple**：簡化的單欄版面配置
- **PostBanner**：支援橫幅圖片的版面配置

## 重要檔案

### 核心元件

- `components/MDXComponents.tsx`：自訂 MDX 元件
- `layouts/`：文章版面配置模板
- `app/blog/[...slug]/page.tsx`：動態部落格文章渲染
- `app/layout.tsx`：根版面配置和主題提供者

### 生成檔案

- `app/tag-data.json`：自動生成的標籤計數
- `public/search.json`：Kbar 搜尋索引
- `contentlayer/generated/`：自動生成的內容類型

## 開發筆記

### 內容工作流程

1. 在 `data/blog/YYYY/` 目錄中建立新的 MDX 檔案
2. 添加必要的 frontmatter（title、date）
3. 內容由 Contentlayer 自動處理
4. 靜態頁面在建置時生成

### 圖片處理

- 圖片從外部 CDN（image.cashwu.com）提供
- 遠端圖片模式在 next.config.js 中配置
- 使用標準 markdown 圖片語法：`![alt](url)`

### SEO 和效能

- 自動生成結構化資料（JSON-LD）
- 包含 Open Graph 和 Twitter 元標籤
- 網站地圖和 RSS 摘要生成
- 配置安全標頭和 CSP

### 分析和搜尋

- 使用環境變數整合 Umami 分析
- Kbar 搜尋搭配自動生成索引
- 基於標籤的內容組織

## Git 提交規範

### 提交訊息限制

- **禁止使用 Claude Code 相關字樣**：提交訊息中不得包含任何與 Claude Code、Claude、AI 助手等相關的字詞
- **移除自動生成標籤**：不要使用包含「Generated with Claude Code」或類似的自動生成標籤
- **簡潔明確**：使用簡潔、描述性的提交訊息，專注於實際的程式碼變更內容
- **中文優先**：提交訊息建議使用正體中文，但也可以使用英文

## 部落格文章撰寫指南

### 文章格式規範

- 新增文章時，請參考 `data/blog/_Draft/index.mdx` 的相關格式和內容
- 使用 `PostSimple` 版面配置作為預設選項
- 必須包含 `lastmod` 欄位以追蹤文章更新時間
- 圖片使用 `image.cashwu.com` CDN 託管
- 每篇文章需有封面圖片，格式為 `https://image.cashwu.com/YYYY/article-slug/01.webp`

### Frontmatter 必填欄位

```yaml
---
layout: PostSimple
title: '文章標題'
summary: '文章摘要'
date: 'YYYY-MM-DD'
lastmod: 'YYYY-MM-DD'
tags: ['標籤1', '標籤2']
draft: false
images: ['https://image.cashwu.com/YYYY/article-slug/01.webp']
---
```

### 內容結構

1. **封面圖片**：文章開頭放置封面圖片

   ```markdown
   ![](https://image.cashwu.com/YYYY/article-slug/01.webp)
   ```

2. **圖片來源標註**：根據圖片來源選擇適當的標註

   - AI 生成：`> 圖片來源：AI 產生`
   - 網路來源：`> 圖片來源：網路。若分享內容有侵害您的圖片版權，請來信告知，我們會及時加上版權信息，若是您反對使用，本著對版權人尊重的原則，會儘速移除相關內容。`
   - Unsplash：`> Photo by [作者名](連結) on [Unsplash](連結)`

3. **內容區塊**：可選擇性包含以下結構
   - 問題描述
   - 原因分析
   - 解決方案
   - 參考連結

### 多媒體內容

- **YouTube 嵌入**：使用 iframe 元件，設定 16:9 比例
- **程式碼區塊**：支援語法高亮，使用三個反引號包圍
- **數學表達式**：支援 KaTeX 語法

### 贊助區塊

每篇文章結尾應包含統一的贊助支持區塊：

```markdown
## 支持創作

如果這篇文章對您有幫助，歡迎透過 [贊助連結](https://portaly.cc/cashwugeek) 支持我持續創作優質內容。您的支持是我前進的動力！
```

**位置**：放在文章內容結束後、分隔線和圖片來源標註之前
