---
title: 播放器狀態追蹤簡介
description: 了解播放器狀態追蹤功能，包括實作和報告播放器狀態的要求與準則。
exl-id: c678e182-74e4-4f46-8596-7be57e645c66
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/R4ByVgEI65JyN-LFdMX1CCBs4zVyppVgebN9OJxJNMM
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: c153fd90-23e1-4614-81d3-3cc7571227f7id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: c2be0313-b3ae-45e0-b454-d20bf54b23f2id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 409
ht-degree: 100%

---

# 播放器狀態追蹤簡介

為了讓您的產品提供最佳體驗，並提升企業價值，了解客戶的視訊觀看行為至關重要。 這包括客戶在不同播放器狀態所花的時間。  因應需求靈活地建立、測量新的播放器狀態和事件也很重要。

「播放器狀態追蹤」功能可讓您使用標準解決方案變數集，針對全螢幕、隱藏式字幕、靜音、子母畫面和觀看中等播放工作階段，擷取觀看者互動行為。  「播放器狀態追蹤」也能讓您選擇建立自訂播放器狀態。 在 Analysis Workspace 中製作報表時，您可以使用「播放器狀態追蹤」變數。

為了擷取播放器狀態變更，「播放器狀態追蹤」會更新視訊測量中繼資料。 舉例來說，為了判斷觀看者是否「確實」觀看視訊，「播放器狀態追蹤」會測量視訊播放期間的聲音開啟時間和聲音關閉時間 (代表觀看者可能沒有在認真觀看視訊)，以及視訊處於一般模式和全螢幕模式的時間。

「播放器狀態追蹤」的優點如下：

* 提供可測量常見狀態 (如全螢幕或隱藏式字幕) 的標準變數
* 提供可自訂的變數，以利測量播放工作階段期間的自訂狀態
* 測量自訂播放器狀態發生的時間長度
* 測量可能同時發生的多個狀態

![播放器狀態追蹤](assets/player_state_tracking.png)

## 需求

「播放器狀態追蹤」需要下列其中一項，才能進行資料收集：
* Media JS SDK 3.0 以上版本
* Adobe Marketing Cloud 解決方案適用的 Chromecast 3.0 SDK
* Media Analytics 擴充功能 (以便與 Adobe Experience Platform (AEP) SDK 搭配使用)
   * 網頁版：Adobe Media Analytics (3.x SDK) for Audio and Video v1.0 以上版本
   * 行動版：Adobe Media Analytics for Audio and Video v2.0 以上版本
* 媒體收集 API

## 準則

在實作播放器狀態追蹤之前，請先將下列準則納入考量。

* 所有播放器狀態都會列入計算 (不分割)
* 您可以同時測量多個播放器狀態。
* 播放期間最多可追蹤 10 個播放器狀態。
* 播放器狀態量度只會在媒體關閉呼叫時傳送至 Analytics 以供產生報表。
* 狀態停止後，便不會維護應用程式狀態的相關知識。 狀態結束後，狀態必須重新開始才能繼續追蹤。 每次進入新的播放狀態時，播放器狀態都必須重新開始。
* 系統會分別擷取每個播放工作階段的播放器狀態，而不會合併計算多個播放工作階段的播放器狀態。
