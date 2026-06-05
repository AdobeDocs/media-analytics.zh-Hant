---
title: 串流媒體服務發行說明
description: 檢視串流媒體服務的發行說明。
feature: Release Notes
role: User, Admin, Developer
exl-id: ef068aa6-fdf4-4a5c-b5d0-b93ad31894e8
TQID: https://experienceleague.adobe.com/yNfosiewndKE7c-VjoVM6D3ifYlgX3eJGgYQWcBC9no
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: f73667dc-d296-4875-8975-ac3fdc3adc42
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: ac8a38fa-dec3-4581-8f64-178fde9f64e8
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7b5232f25f3aa26e8566783557163f316af3fe57
workflow-type: tm+mt
source-wordcount: 720
ht-degree: 35%

---

# 串流媒體服務發行說明

**上次更新日期**：2026年6月4日

## 2026

| 功能 | 說明 | 日期 |
| --- | --- | --- |
| **支援排程資料** | 上傳過去直播內容的排程資料，以按方案或區段追蹤收視率。 支援的內容型別包括：<ul><li>FAST (免費廣告支援的電視) 平台</li><li>本地串流</li><li>現場體育賽事</li></ul>如需詳細資訊，請參閱[上傳排程資料以追蹤即時內容](/help/use-cases/track-schedule-data.md)使用案例。 | 開始推出： 2025年10月29日<p>全面發佈：2026年10月</p> |

## 2025

| 功能 | 說明 | 日期 |
| --- | --- | --- |
| **`mediaTimed`XDM欄位淘汰** | `mediaTimed` XDM物件已過時，改用`mediaReporting`欄位路徑。 在2025年5月9日之前實施Analytics來源聯結器的客戶必須移轉其設定。 如需詳細資訊，請參閱下列移轉指南：<ul><li>[將對象移轉至新的串流媒體欄位](/help/implementation/edge/migrate/migrate-audiences.md)</li><li>[移轉Customer Journey Analytics以使用新的串流媒體欄位](/help/implementation/edge/migrate/migrate-cja-setup.md)</li><li>[將自訂欄位的資料準備移轉至新的串流媒體欄位](/help/implementation/edge/migrate/migrate-dataprep.md)</li><li>[將設定檔移轉至新的串流媒體欄位](/help/implementation/edge/migrate/migrate-profiles.md)</li></ul> | 2025 年 10 月 |

## 2024

| 功能 | 說明 | 日期 |
| --- | --- | --- |
| **網頁SDK支援** | 使用Web SDK或Web SDK標籤擴充功能，將串流媒體網頁資料傳送至Adobe Experience Platform Edge Network，實現跨平台解決方案（例如Customer Journey Analytics、Real-time CDP、Journey Optimizer和事件轉送）的統一收集方法。 如需詳細資訊，請參閱[設定適用於串流媒體的Web SDK](/help/implementation/edge/web-sdk.md)或[設定適用於串流媒體的Web SDK標籤擴充功能](/help/implementation/edge/web-sdk-tags.md)。 | 2024 年 5 月 29 日 |
| **Roku支援** | 使用Roku SDK將串流媒體資料傳送到Adobe Experience Platform。 如需詳細資訊，請參閱[設定適用於串流媒體的Roku](/help/implementation/edge/roku.md)。 | 2024 年 4 月 12 日 |

## 2023

| 功能 | 說明 | 日期 |
| --- | --- | --- |
| **Experience Edge支援** | 使用iOS和Android適用的Media Edge API或Mobile SDK實作串流媒體收集。<ul><li>[設定適用於串流媒體的Media Edge API](/help/implementation/edge/media-edge-api.md)</li><li>[設定適用於串流媒體的iOS](/help/implementation/edge/ios.md)或[設定適用於具標籤的串流媒體的iOS](/help/implementation/edge/ios-tags.md)</li><li>[設定適用於串流媒體的Android](/help/implementation/edge/android.md)或[設定適用於具標籤的串流媒體的Android](/help/implementation/edge/android-tags.md)</li></ul> | 2023年5月12日 |

## 2022

| 功能 | 說明 | 日期 |
| --- | --- | --- |
| **多重播放器狀態追蹤** | 使用Media Collection API實作多個[播放器狀態追蹤](/help/implementation/events/player-state/overview.md)。 | 2022 年 9 月 |
| 已重新命名 XDM 欄位 | 已重新命名XDM欄位名稱以保持一致性：<ul><li>音訊和視訊引數</li><li>廣告參數</li><li>章節參數</li><li>播放器狀態參數</li><li>品質參數</li></ul> | 2022 年 9 月 |
| **個面板已新增至Customer Journey Analytics** | 已將[媒體同時檢閱者面板](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers)和[媒體播放時間面板](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/cja-workspace/panels/media-playback-time-spent)新增至Customer Journey Analytics。 | 2022 年 8 月 9 日 |
| **平均分鐘觀眾數** | 您可以使用[平均每分鐘觀眾數面板](https://experienceleague.adobe.com/zh-hant/docs/analytics/analyze/analysis-workspace/panels/average-minute-audience-panel)來更瞭解平均內容使用量。 <br>「平均分鐘觀眾數」可比較任何長度或類型的節目。 此外，您也可以比較數位平均分鐘觀眾數和線性電視的平均分鐘量度，或是將前者附加到後者。 此面板提供較大的彈性來測量自訂時段的平均觀眾數，以及持續時間分類的更新時間。 | 2022 年 3 月 16 日 |

## 2021

| 功能 | 說明 | 日期 |
| --- | --- | --- |
| **媒體播放時間** | 「[播放時間](https://experienceleague.adobe.com/zh-hant/docs/analytics/analyze/analysis-workspace/panels/media-playback-time-spent)」面板提供寶貴的觀眾參與度insight，並可讓媒體組織透過進階花費時間分析及時段功能，以每分鐘的使用者參與度取得更深入、更細微的分析。 您可以觀察使用者在特定時間點觀看您的媒體串流所花的時間多寡。 您可以依不同的資料粒度 (包括新的 5 分鐘、15 分鐘和 30 分鐘資料粒度) 分割播放持續時間。 | 2021 年 9 月 |

## 2020

| 功能 | 說明 | 日期 |
| --- | --- | --- |
| **媒體同時檢閱者面板** | [同時檢閱者面板](https://experienceleague.adobe.com/zh-hant/docs/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers)可協助您瞭解人數高峰或趨勢反轉的時間。 取得內容品質和檢閱者參與的寶貴洞察，並取得疑難排解或規劃數量和規模的協助。<br><br>[媒體同時檢閱者面板（教學課程）](https://experienceleague.adobe.com/zh-hant/docs/analytics-learn/tutorials/analysis-workspace/using-panels/media-concurrent-viewers-panel-in-analysis-workspace) | 2020年9月；2021年1月 |
| **支援的裝置和平台** | 含 AEP SDK 的 Media Launch 擴充功能現在支援下列 OTT 裝置： <div><ul><li>Apple TV (tvOS)</li><li>Fire TV (Fire OS)</li><li>Android TV</li></ul></div> | 2020 年 6 月 |
