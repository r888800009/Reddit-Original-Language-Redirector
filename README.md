# Reddit Original Language Redirector

Reddit Original Language Redirector 是一個小型 Chrome 擴充功能，用來自動將 Reddit 的 zh-Hant 翻譯網址重新導向到原始語言頁面。它會移除 Reddit URL 中的 `tl=zh-hant` 參數，並加入 `show=original`，避免 Reddit 自動顯示繁體中文、粵語或其他不想要的翻譯內容。

適合想關閉 Reddit 自動翻譯、固定查看 Reddit 原文、避免 Reddit 中文翻譯頁面的使用者。

## 功能特色

- 自動將 Reddit 翻譯頁面導向原始語言頁面。
- 移除 `tl=zh-hant`，並加入或替換為 `show=original`。
- 支援 `reddit.com` 與 `www.reddit.com` 等 Reddit 網域。
- 使用 Chrome Manifest V3 與 Declarative Net Request。
- 不讀取頁面內容，不收集瀏覽資料。

當 Reddit 頁面網址包含 `tl=zh-hant` 時，這個擴充功能會在頂層頁面導覽時重新導向，方式如下：

1. 移除 `tl` query 參數。
2. 加上或替換為 `show=original`。

範例：

```text
https://www.reddit.com/r/example/comments/abc123/title/?tl=zh-hant
```

會變成：

```text
https://www.reddit.com/r/example/comments/abc123/title/?show=original
```

## 用途

這個 Chrome 擴充功能的用途是避免 Reddit 將內容翻譯成粵語或其他不想要的 zh-Hant 翻譯輸出，改為顯示 Reddit 原始頁面。

它刻意保持簡單，只使用安全完成此功能所需的最低權限。

## 隱私與權限

這個擴充功能採用最小權限設計：

- 使用 Manifest V3。
- 使用 `declarativeNetRequestWithHostAccess`，不讀取頁面內容。
- 只要求 Reddit 網址的 host access：
  - `https://reddit.com/*`
  - `https://*.reddit.com/*`
- 只作用於頂層 Reddit 頁面導覽。
- 不使用 content scripts。
- 不使用 background service worker。
- 不使用 `tabs`、`storage`、`cookies` 或 `webRequest`。
- 不收集、儲存、傳送或檢查瀏覽資料。

這個擴充功能只在 `rules/reddit-original-language.json` 宣告一條靜態重新導向規則。

## 檔案

```text
manifest.json
rules/reddit-original-language.json
README.md
```

## 本機安裝

1. 解壓縮這個套件。
2. 開啟 Chrome 並前往 `chrome://extensions/`。
3. 啟用 **Developer mode**。
4. 點選 **Load unpacked**。
5. 選擇解壓縮後的擴充功能資料夾。

## 測試

開啟一個包含 `tl=zh-hant` 的 Reddit 網址，例如：

```text
https://www.reddit.com/r/example/comments/abc123/title/?tl=zh-hant
```

Chrome 應該會將它重新導向到同一個 Reddit 網址，並移除 `tl`、加上 `show=original`。

## 設計說明

這個擴充功能使用靜態 Declarative Net Request 規則，因為它比用 JavaScript 攔截請求更能保護隱私。瀏覽器會根據封裝在擴充功能內的規則執行重新導向，因此擴充功能不需要讀取頁面、存取 Reddit 內容，或在 Reddit 頁面上執行程式碼。
