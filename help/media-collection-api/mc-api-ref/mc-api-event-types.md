---
seo-title: 事件類型和說明
title: 事件類型和說明
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 事件類型和說明{#event-types-and-descriptions}

## sessionStart

隨電話 `sessions` 傳送。 當回應傳回時，您可以從 Location 標題擷取工作階段 ID，並使用於後續發送給收集伺服器的事件呼叫。

## play

Sent when the player changes state to "playing" from another state (i.e., the `on('Playing')` callback is triggered by the player). 在播放器改變為「正在播放」之前，其他可能的狀態包括「正在緩衝」、使用者從「已暫停」狀態繼續播放、播放器從錯誤中恢復、自動播放等。

## ping

* **主要內容 -** 在主要內容播放期間，必須每隔 10 秒傳送一次，不論其他已傳送的 API 事件為何。第一個 Ping 事件應該要在主要內容開始播放後 10 秒引發。
* **廣告內容 -** 在廣告追蹤期間，必須每隔 1 秒傳送一次。

Ping 事件的要求內文&#x200B;*不*&#x200B;應該包含 `params` 對應。

## 位元速率變更

在位元變更時傳送。

## bufferStart

在緩衝開始時傳送。 `bufferResume` 事件類型並不存在。A `bufferResume` is inferred when you send a `play` event after `bufferStart`.

## pauseStart

當使用者按「暫停」時傳送。 `resume` 事件類型並不存在。A `resume` is inferred when you send a `play` event after a `pauseStart`.

## adBreakStart

代表廣告插播開始

## adStart

發出廣告開始的信號

## adComplete

代表廣告插播結束

## adSkip

發出廣告跳過的信號

## adBreakComplete

代表廣告插播結束

## chapterStart

代表章節區段開始

## chapterSkip

指示章節跳過

## chapterComplete

表示章節完成

## error

發出錯誤信號。

## sessionEnd

當使用者放棄檢視內容且不太可能返回時，這會用來通知Media Analytics後端以立即關閉作業。

If you don't send a `sessionEnd`, an abandoned session will time-out normally (after no events are received for 10 minutes, or when no playhead movement occurs for 30 minutes), and the session is deleted by the backend.

## sessionComplete

到達主要內容的結尾時傳送

>[!IMPORTANT]
>
>You should refer to the [JSON validation schemas](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) for each event type, to verify correct event parameter types and requirements.

