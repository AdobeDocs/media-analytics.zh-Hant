---
seo-title: 概述
title: 概述
description: null
uuid: c14bdbef-5846-4d31-8a14-8e9e0e9c9861
exl-id: 58430636-7fab-433a-8ead-52ccaa45d920
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '331'
ht-degree: 100%

---

# 概述{#overview}

媒體收集 API 是 Adobe 用戶端 Media SDK 的 RESTful 替代方案。透過媒體收集 API，您的播放器可以使用 RESTful HTTP 呼叫追蹤音訊和視訊事件。

媒體收集 API 本質上是轉接程式，可做為伺服器端的 Media SDK。這表示 Media SDK 文件某些方面也與媒體收集 API 有關。例如，這兩個解決方案都使用相同的[串流媒體參數](/help/metrics-and-metadata/audio-video-parameters.md)，而且收集的串流媒體追蹤資料會產生相同的[報表和分析](/help/media-reports/media-reports-enable.md)。

## 媒體追蹤資料流程 {#media-tracking-data-flows}

實作媒體收集 API 的媒體播放器會直接向媒體追蹤後端伺服器發出 RESTful API 追蹤呼叫，而實作 Media SDK 的播放器則會向播放器應用程式內的 SDK API 發出追蹤呼叫。透過網路發出呼叫的其中一個效應，就是實作媒體收集 API 的播放器需要處置一些 Media SDK 自動處置的處理工作(詳情請參閱[媒體收集實施](mc-api-impl/mc-api-quick-start.md))。

媒體收集 API 擷取的追蹤資料，其傳送和初期處理方式與 Media SDK 播放器擷取的追蹤資料有所不同，不過這兩種解決方案使用的後端處理引擎是一樣的。

![](assets/col_api_overview_simple.png)

## API 概述 {#api-overview}

**URI：**&#x200B;請向 Adobe 代表索取。

**HTTP 方法：** POST，搭配 JSON 要求內文。

### API 呼叫 {#mc-api-calls}

* **`sessions`-** 與伺服器建立工作階段，並傳回後續 `events` 呼叫使用的工作階段 ID。應用程式會在追蹤工作階段開始時呼叫一次。

   ```
   {uri}/api/v1/sessions
   ```

* **`events`-** 傳送媒體追蹤資料。

   ```
   {uri}/api/v1/sessions/{session-id}/events
   ```

### 要求內文 {#mc-api-request-body}

```
{
    "playerTime": {
        "playhead": {playhead position in seconds},
        "ts": {timestamp in milliseconds}
    },
    "eventType": {event-type},
    "params": {
        {parameter-name}: {parameter-value},
        ...
        {parameter-name}: {parameter-value}
    },
    "qoeData" : {
        {parameter-name}: {parameter-value},
        ...
        {parameter-name}: {parameter-value}
    },
    "customMetadata": {
        {parameter-name}: {parameter-value},
        ...
        {parameter-name}: {parameter-value}
    }
}
```

* `playerTime` - 所有要求均強制使用。
* `eventType` - 所有要求均強制使用。
* `params` - 某些 `eventTypes` 強制使用。若要判斷哪些 eventTypes 屬於強制性質，哪些屬於選用性質，請參閱 [JSON 驗證結構](mc-api-ref/mc-api-json-validation.md)。

* `qoeData` - 所有要求均可選用。
* `customMetadata` - 所有要求均可選用，不過只能連同 `sessionStart`、`adStart` 和 `chapterStart` 事件類型一起傳送。

您可以利用開放使用的 `eventType`JSON 驗證結構[來驗證每種 ](mc-api-ref/mc-api-json-validation.md) 的參數類型，以及特定事件的參數屬於選用或必要性質。

### 事件類型 {#mc-api-event-types}

* `sessionStart`
* `play`
* `ping`
* `pauseStart`
* `bufferStart`
* `adStart`
* `adComplete`
* `adSkip`
* `adBreakStart`
* `adBreakComplete`
* `chapterStart`
* `chapterSkip`
* `chapterComplete`
* `sessionEnd`
* `sessionComplete`
