---
title: 文件更新
description: null
uuid: 1f3e48df-83b6-418c-8cf7-d79466481f79
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 資源{#resources}

## 發行說明{#release-notes}

* [發行說明](https://docs.adobe.com/content/help/zh-Hant/release-notes/experience-cloud/current.html)

## 文件更新{#documentation-updates}

### 上次更新: 2019 年 10 月 {#October-2019-update}

多項編輯和格式修正。
擴展到 Media SDK 以外的逐步指南主題，包括有關「媒體追蹤以外的媒體維度」的全新一般逐步指南主題。


### 上次更新日期: 2019 年 3 月 7 日 {#March-2019-update}

* 本次更新主要是為了在 JavaScript 和 OTT 平台上發行的 2.2 版 Media SDK。
* JavaScript 和 OTT 平台上發行的 2.2 版 Media SDK 提供與下述 iOS 和 Android 平台相同的支援 (2018 年 11 月 1 日更新)。

### 上次更新: 2018 年 11 月 1 日 {#November-2018-update}

* 本次更新主要是為了在 Android 與 iOS 平台上發行的 2.2 版 Media SDK。
* Android 與 iOS 平台上的 2.2 版 Media SDK 支援在前述平台上追蹤音訊，另改善了一些內部功能。
* 加入音訊追蹤功能後，Media SDK 與媒體收集 API 均提供音訊與視訊追蹤功能，因此我們需要相對廣義的命名更新:

   * 整套解決方案的名稱為 Adobe Analytics for Audio and Video
   * 先前各式文件中所用的簡稱「Video Analytics」現改為「Media Analytics」
   * SDK 中參照「視訊心率程式庫」(VHL) 的文句現改為「Media SDK」
   * 先前提及「視訊」或「vhl」的檔案名稱與 URL (如 API 參考的連結) 現於原處改用「媒體」
   * 在程式碼中，中繼資料索引鍵的名稱現以「MEDIA」取代「VIDEO」
   * 依此類推...

* 除了前述改變之外，我們另重新建構了 Media SDK 區段，包括標準中繼資料實作與返回各自主題的參照 (它們在前一次文件更新時收錄在&#x200B;*追蹤核心*&#x200B;主題)。這些主題與&#x200B;*追蹤核心*、*追蹤搜尋*&#x200B;及&#x200B;*追蹤緩衝*&#x200B;等主題現歸納在同一個組別，收錄在&#x200B;*追蹤音訊與視訊播放*&#x200B;之下。

* Federated Analytics 表單已更新為 3.2 版，藉此反應與追蹤音訊有關的新參數。

### 更新: 2018 年 10 月 10 日 {#October-2018-update}

* 「SDK 實作」區域的文件結構已經過「重組」，將個別 (但大致相同) 的平台實施指南合併成一個 SDK 實作區段，並將平台專用的追蹤範例呈現在通用追蹤主題下方的子區段。
* 為了因應移轉到新文件系統的需求，檔案已全數重新命名。所有 DITA 字首 ( c_、r_、t_ ) 分別代表概念、參照及工作等主題類型) 已刪除。所有底線 (’_’) 均已以連字號取代 ('-')。另外，檔案名稱與主題的標題也更相似。
* 更新一般驗證與認證主題。
* 加入測量選項解說等介紹性素材，另更新必備條件、實施路徑及 Audience Manager 啟用。
* 更新「量度和中繼資料」與「Reporting and Analysis」區段，藉此反應新增的 Audio Analytics 功能。
