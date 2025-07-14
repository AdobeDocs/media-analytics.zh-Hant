---
title: 串流媒體事件類型和說明
description: '什麼是媒體收集事件型別和說明？ '
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
exl-id: f2919e69-8b03-45b4-b9cd-365222a061e0
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 79%

---

# 事件類型和說明{#event-types-and-descriptions}

## sessionStart

連同 `sessions` 呼叫一起傳送。當回應傳回時，您可以從 Location 標題擷取工作階段 ID，並使用於後續發送給收集伺服器的事件呼叫。

## play

當播放器從其他狀態變更為「正在播放」狀態時傳送 (即播放器觸發 `on('Playing')` 回呼)。在播放器改變為「正在播放」之前，其他可能的狀態包括「正在緩衝」、使用者從「已暫停」狀態繼續播放、播放器從錯誤中恢復、自動播放等。

## ping

* **主要內容 -** 在主要內容播放期間，必須每隔 10 秒傳送一次，不論其他已傳送的 API 事件為何。第一個 Ping 事件應該要在主要內容開始播放後 10 秒引發。
* **廣告內容 -** 在廣告追蹤期間，必須每 1 秒傳送一次。

Ping 事件的要求內文&#x200B;*不*&#x200B;應該包含 `params` 對應。

## bitrateChange

位元速率變更時傳送。

## bufferStart

緩衝開始時傳送。`bufferResume` 事件類型並不存在。在 `bufferStart` 後傳送 `play` 事件即代表 `bufferResume`。

## pauseStart

使用者按下「暫停」時傳送。`resume` 事件類型並不存在。在 `pauseStart` 後傳送 `play` 事件即代表 `resume`。

## adBreakStart

代表廣告插播開始

## adStart

代表廣告開始

## adComplete

代表廣告插播結束

## adSkip

代表廣告略過

## adBreakComplete

代表廣告插播結束

## chapterStart

代表章節區段開始

## chapterSkip

代表章節略過

## chapterComplete

代表章節結束

## error

代表已發生錯誤。

## sessionEnd

當使用者放棄檢視內容，而且不太可能返回工作階段時，用來通知 Media Analytics 後端立即關閉工作階段.

如果未傳送`sessionEnd`，放棄的工作階段通常會逾時[2&rbrace; （在10分鐘內未接收到任何事件，或播放點在30分鐘內未移動）。 ](../mc-api-impl/mc-api-timeout.md)此外，使用該工作階段ID進行的所有後續媒體呼叫都將被捨棄。

## sessionComplete

到達主要內容的結尾時傳送

>[!IMPORTANT]
>
>若要驗證事件參數類型和需求是否正確，請參考 [JSON 驗證結構](mc-api-json-validation.md)以瞭解每種事件類型。

## stateStart

代表播放器狀態追蹤已開始。

如需詳細資訊，請參閱[實作與報告](/help/use-cases/player-state-tracking/implementation-and-reporting.md)。

## stateEnd

代表播放器狀態追蹤的結尾。

如需詳細資訊，請參閱[實作與報告](/help/use-cases/player-state-tracking/implementation-and-reporting.md)。
