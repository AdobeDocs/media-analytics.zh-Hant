---
title: 追蹤廣告
description: 有關如何使用 Media SDK 實作廣告追蹤的概觀。
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
exl-id: c714d31f-3d08-4ded-a413-2762d53bec75
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/PguxKIzAL95WbMl5c0yJq9rYSqZgOGbbAYtxOI4eVOs
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 513
ht-degree: 3%

---


# 追蹤廣告

廣告播放追蹤涵蓋廣告插播、廣告開始、廣告完成，以及廣告略過。 使用媒體播放器的API來識別關鍵播放器事件，並填入必要的廣告變數。

## 播放器事件

| 播放器事件 | 動作 |
| --- | --- |
| 廣告插播開始 | 建立廣告插播物件；呼叫AdBreakStart |
| 廣告開始 | 建立廣告物件；呼叫AdStart |
| 廣告完成 | 呼叫Adcomplete |
| 廣告略過 | 呼叫AdSkip |
| 廣告插播完成 | 呼叫AdBreakComplete |

## 實作步驟

1. 識別廣告插播界限何時開始（包括前段），並建立廣告插播物件。 如需欄位定義，請參閱[廣告插播名稱](/help/implementation/variables/ads/ad-break-name.md)和[廣告插播開始時間](/help/implementation/variables/ads/ad-break-start-time.md)。
1. 呼叫[廣告插播開始](/help/implementation/events/ads/ad-break-start.md)以開始追蹤廣告插播。
1. 識別廣告何時開始並建立廣告物件。 如需欄位定義，請參閱[廣告名稱](/help/implementation/variables/ads/ad-name.md)、[廣告識別碼](/help/implementation/variables/ads/ad-id.md)、[廣告長度](/help/implementation/variables/ads/ad-length.md)、[Pod位置中的廣告](/help/implementation/variables/ads/ad-in-pod-position.md)以及[廣告播放器名稱](/help/implementation/variables/ads/ad-player-name.md)。
1. 可選擇附加標準廣告中繼資料。 如需可用的金鑰，請參閱[廣告商](/help/implementation/variables/ads/advertiser.md)、[促銷活動ID](/help/implementation/variables/ads/campaign-id.md)、[Creative ID](/help/implementation/variables/ads/creative-id.md)、[Creative URL](/help/implementation/variables/ads/creative-url.md)、[位置ID](/help/implementation/variables/ads/placement-id.md)以及[網站ID](/help/implementation/variables/ads/site-id.md)。
1. 呼叫[廣告開始](/help/implementation/events/ads/ad-start.md)以開始追蹤廣告。
1. 當廣告播放到完成時，請呼叫[廣告完成](/help/implementation/events/ads/ad-complete.md)。
1. 如果檢視器略過廣告，請呼叫[廣告略過](/help/implementation/events/ads/ad-skip.md)而非廣告完成。
1. 對於相同廣告插播中的其他廣告，請重複步驟3到7。
1. 當廣告插播完成時，請呼叫[廣告插播完成](/help/implementation/events/ads/ad-break-complete.md)。

>[!IMPORTANT]
>
>**前段廣告：請勿在`AdBreakStart`和`AdStart`之前呼叫`trackPlay`。** 主要內容增量[內容開始](/help/reporting/metrics/content-starts.md)上的前`play`個Ping。 如果在前段廣告事件引發之前呼叫`trackPlay`，且檢視者在廣告期間退出，則即使未播放任何主要內容，內容開始次數也會增加。 對於前段案例，延遲`trackPlay`直到傳送`AdBreakStart`和`AdStart`之後。

>[!NOTE]
>
>廣告播放期間報告的播放點值代表檢視者在&#x200B;**主要內容**&#x200B;中的位置，而非廣告中的位置。 對於10分鐘視訊之前的前段廣告，整個廣告的播放點都是`0`。 對於以5分鐘標籤開始的中段廣告，播放點在廣告期間維持在`300` （秒）。

## 常見問題

### 廣告之間非預期的main:play呼叫

如果您看到在連續廣告之間發生`main:play`個呼叫，則AdComplete呼叫與下一個AdStart呼叫之間會存在超過250毫秒的間隙。 發生此間隔時，Media SDK會退回傳送主要內容Ping，這樣可針對前段案例提早設定內容開始量度。

**原因：** Media SDK未設定廣告資訊，且播放器處於播放狀態，因此會將間隔期間計入主要內容。

**解決方法：**&#x200B;延遲每個廣告的AdComplete呼叫（最後一個除外），而不是在廣告結束時立即呼叫。 依下列方式批次處理呼叫：

* 在每個&#x200B;**廣告開始**&#x200B;時：如果先前的廣告存在且尚未標籤為完成，請呼叫新廣告的AdComplete *before*。
* 在每個&#x200B;**廣告資產結束**&#x200B;時：不要立即呼叫AdComplete；請將其延遲。
* 在&#x200B;**廣告插播完成**：呼叫最後一個廣告的AdComplete （如果尚未呼叫），然後呼叫AdBreakComplete。

此模式可確保AdComplete和下一個AdStart會連續引發，消除任何間隙。
