---
title: 設定適用於串流媒體的Media Edge API
description: 使用Media Edge API直接將串流媒體資料傳送到Edge Network。
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# 設定適用於串流媒體的Media Edge API

如果您無法使用網頁SDK、Mobile SDK或Roku SDK （例如在自訂或不支援的執行階段上），可以使用Media Edge API直接將串流媒體資料傳送到Edge Network。 此API使用RESTful HTTP呼叫，且完全可自訂。

* **必要條件**：完成[Edge實作總覽](overview.md) （結構描述、資料集、資料流並啟用[!UICONTROL Media Analytics]）。

## 傳送媒體事件至Edge Network

媒體事件會傳送至`/ee/va/v1/`端點，並由`configId`查詢引數輸入您的資料流。 例如，工作階段以`sessionStart`的POST開始：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId=<datastreamID>" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": { "name": "video-123", "playerName": "player_name", "contentType": "vod", "length": 128, "channel": "sample_channel" },
        "playhead": 0
      }
    }
  }]
}'
```

回應會傳回所有後續事件都必須包含的工作階段ID。 如需完整的端點集、請求/回應格式及OpenAPI規格，請參閱[Media Edge API參考](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/)。

## 追蹤媒體事件

檢視每個[事件](/help/implementation/events/overview.md)和[變數](/help/implementation/variables/overview.md)頁面上的&#x200B;**Media Edge API**&#x200B;標籤，以取得確切的裝載。

## 下一步

實作完成後，您可以[為Edge實作](/help/reporting/setup/edge-reporting.md)設定報表。

>[!MORELIKETHIS]
>
>* [Media Edge API參考](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/)
>* [事件總覽](/help/implementation/events/overview.md)
>* [變數總覽](/help/implementation/variables/overview.md)
