---
title: 串流媒體收集API — 快速入門
description: 開始使用 Streaming Media API。了解如何快速確認您的要求資料。
uuid: ca20bad4-2c8f-406b-833e-b4883a9aa534
exl-id: 08bb5873-f69a-4fdd-8f27-69649b4acb17
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 97%

---

# 快速入門{#quick-start}

>[!TIP]
>
>收集向 Media Analytics (MA) Collection API 後端伺服器發出成功[工作階段要求](../mc-api-ref/mc-api-sessions-req.md)所需的要求資料。您可以手動傳送要求 (利用 `curl` 或 Postman 等)，進而迅速驗證要求資料。如此一來，您將能立即獲知要求中是否有因為資料類型錯誤或資訊錯誤而引起的問題。請使用 [JSON 驗證結構](../mc-api-ref/mc-api-json-validation.md)來確認您提供的要求資料是否適當。

1. 收集必要的標準 Adobe Analytics 和訪客資料；您必須提供這些資料才能執行任何 Experience Cloud 應用程式：

   * 訪客 Experience Cloud 組織 ID
   * 訪客 Experience Cloud 使用者 ID
   * Analytics 報表套裝 ID
   * Analytics 追蹤伺服器 URL

1. 為 `sessions` 要求內文建立 JSON 物件，其中包含發出成功呼叫所需的最少資料。例如：

   ```json
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
   >您必須在 JSON 要求內文中使用正確的資料類型。例如，`analytics.enableSSL` 須有布林值、`media.length` 是數值等。您可以參閱 [JSON 驗證結構](mc-api-validate-reqs.md)，查閱參數類型和強制與選用需求。

1. 將工作階段要求傳送到 MA Collection API 端點。如果您的要求裝載無效，請找出問題並再次嘗試，直到獲得 `201 Created` 回應為止。在以下 `curl` 範例中，JSON 要求內文位於名為 `sample_data_session` 的檔案中：

   ```sh
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

如果[工作階段要求](../mc-api-ref/mc-api-sessions-req.md)成功，您會獲得與前述內容相似的 `201 Created` 回應。回應的 Location 標題含有工作階段 ID。工作階段 ID 是回應中的重要資訊，因為它是所有後續追蹤呼叫的必要元件。成功傳回[工作階段要求](../mc-api-ref/mc-api-sessions-req.md)後，您就可以放心地在視訊播放器中使用 MA API 實作視訊追蹤。
