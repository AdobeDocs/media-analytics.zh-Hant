---
seo-title: 快速入門
title: 快速入門
uuid: ca20不差的4-2c8f-406b-833e-b4883 a
translation-type: tm+mt
source-git-commit: 654aaef5d816e75429975d04c4e81ad4d4b6f706

---


# 快速入門{#quick-start}

>[!TIP]
>
>Gather the request data necessary for completing a successful [Session request](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md) to the Media Analytics (MA) Collection API back-end server. 您可以手動傳送要求 (利用 `curl` 或 Postman 等)，進而迅速驗證要求資料。如此一來，您將能立即獲知要求中是否有因為資料類型錯誤或資訊錯誤而引起的問題。請使用 [JSON 驗證結構](../../media-collection-api/mc-api-ref/mc-api-json-validation.md)來確認您提供的要求資料是否適當。

1. 收集必要的標準 Adobe Analytics 和訪客資料；您必須提供這些資料才能執行任何 Experience Cloud 應用程式:

   * 訪客 Experience Cloud 組織 ID
   * 訪客Experience Cloud使用者ID
   * Analytics 報表套裝 ID
   * Analytics Tracking Server URL

1. 為 `sessions` 要求內文建立 JSON 物件，其中包含發出成功呼叫所需的最少資料。例如:

   ```
   { 
       "playerTime": { 
           "playhead": 0, 
           "ts": 1234560890123 
       }, 
       "eventType": "sessionStart", 
       "params": { 
           "media.playerName": "sample-html5-api-player", 
           "analytics.trackingServer": "[YOUR_TS]", 
           "analytics.reportSuite": "[YOUR_RSID]", 
           "media.contentType": "VOD", 
           "media.length": 60.39333333333333, 
           "media.id": "MA Collection API Sample Player", 
           "visitor.marketingCloudOrgId": "[YOUR_ORG_ID]", 
           "visitor.marketingCloudUserId": "[YOUR_ECID]",
           "media.name": "ClickMe", 
           "media.channel": "sample-channel", 
           "media.sdkVersion": "va-api-0.0.0", 
           "analytics.enableSSL": false 
       } 
   }
   ```

   >[!NOTE]
   >
   >您必須在JSON請求主體中使用正確的資料類型。E.g., `analytics.enableSSL` requires a boolean, `media.length` is numeric, etc. You can check parameter types and mandatory versus optional requirements by checking the [JSON validation schemas.](../../media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

1. 傳送階段作業要求至MA Collection API端點。如果您的要求裝載無效，請找出問題並再次嘗試，直到獲得 `201 Created` 回應為止。In this `curl` example, the JSON request body is in a file named `sample_data_session`:

   ```
   $ curl -i -d \ 
     @sample_data_session https://{uri}/api/v1/sessions \ 
     > curl.sessions.out 
   
   $ cat curl.sessions.out 
   HTTP/1.1 201 Created 
   Server: nginx/1.13.5 
   Date: Mon, 18 Dec 2017 22:34:12 GMT 
   Content-Type: application/octet-stream 
   Content-Length: 0 
   Connection: keep-alive 
   Location: /api/v1/sessions/a39c037641f[...]  # <== Session ID  
   Access-Control-Allow-Origin: * 
   Access-Control-Allow-Methods: OPTIONS,POST,PUT 
   Access-Control-Allow-Headers: Content-Type 
   Access-Control-Expose-Headers: Location
   ```

如果[工作階段要求](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md)成功，您會獲得與前述內容相似的 `201 Created` 回應。回應的 Location 標題含有工作階段 ID。工作階段 ID 是回應中的重要資訊，因為它是所有後續追蹤呼叫的必要元件。After a successful return of a [Sessions request](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md), you can confidently proceed with implementing video tracking using the MA API in your video player.
