---
title: 標準和自訂狀態簡介
description: 了解播放器狀態追蹤功能，包括實作和報告標準和自訂播放器狀態的需求和准則。
exl-id: 3c492055-d471-4147-aa78-b058d6b931f4
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 92%

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

* 一個視訊工作階段 最多能有 10 個播放器狀態。
* 可使用任意的狀態組合。
* 如果傳入了多個播放器狀態，只有前 10 個會保留，並轉送給下游的 VA 處理元件。
* 10 個狀態的上限適用於所有狀態，無論關閉與否皆然。
* 狀態可以多次開始和結束，均計為單一狀態。例如，`closedCapationing` 可以開始和停止五次，但只會計為單一狀態。
* 超過 10 個允許狀態數上限的狀態會被捨棄。

## 自訂狀態

您可以建立自訂狀態，在播放工作階段期間擷取自訂動作並更新自訂中繼資料。

如需建立自訂狀態的相關資訊，請參閱[媒體 API 參考指南：`createStateObject`](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
