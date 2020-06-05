---
title: 標準和自訂狀態簡介
description: 此主題說明播放器狀態追蹤功能，包括實作和報告標準與自訂播放器狀態的要求與準則。
translation-type: tm+mt
source-git-commit: f7a45dfbabe71fa9e1de7a4f4b2a7e64849e4ef4
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 66%

---


# 標準和自訂狀態簡介

我們提供 5 種標準播放器狀態，您也可以新增自訂狀態。

| 標準狀態名稱 | Media SDK 常數 | Media Collection API 名稱 |
|-----------------------|------------------------------------------|-----------------------------|
| 全螢幕 | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| 隱藏式字幕 | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| 靜音 | `ADB.Media.PlayerState.Mute` | `mute` |
| 子母畫面 | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| 觀看中 | `ADB.Media.PlayerState.InFocus` | `inFocus` |

標準和自訂狀態的資料計算方式相同，但兩者的資料儲存方式則因 Analytics 報告目的而有所不同。

**標準狀態** — 當您從 Analytics 報告 (管理員端) 的「媒體管理」控制台啟用播放器狀態追蹤時，有 15 個解決方案變數可用於報告和資料匯出。

**自訂狀態** — 您可以自行建立處理規則，將計算值儲存至自訂事件，然後使用這些規則來報告和匯出資料。

## 準則

* 一個視訊作業限制為10個播放器狀態。
* 允許任何狀態組合。
* 如果多個播放器狀態通過，則僅保留前10個並轉發到下游的VA處理元件。
* 10 個狀態的上限適用於所有狀態，無論關閉與否。
* 狀態可以多次啟動和結束，並計為單一狀態。 例如，可 `closedCapationing` 以啟動和停止5次，但會計為單一狀態。
* 每個超過10個允許狀態上限的狀態都會被捨棄。

## 自訂狀態

您可以建立自訂狀態，在播放工作階段期間擷取自訂動作並更新自訂中繼資料。

如需建立自訂狀態的詳細資訊，請參閱「媒 [體API參考指南」: `createStateObject`](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
