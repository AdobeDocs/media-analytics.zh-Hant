---
title: 關於標準和自訂狀態
description: 本主題說明播放器狀態追蹤功能，包括實作和報告標準與自訂播放器狀態的需求與准則。
translation-type: tm+mt
source-git-commit: 1cf11a6b8971f5be490998bbd855a27bfe366e48
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 1%

---


# 關於標準和自訂狀態

有5種標準播放器狀態可供使用，您可以新增自訂狀態。

| 標準狀態名稱 | Media SDK常數 | Media Collection API名稱 |
|-----------------------|------------------------------------------|-----------------------------|
| 全螢幕 | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| 隱藏字幕 | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| 靜音 | `ADB.Media.PlayerState.Mute` | `mute` |
| 畫中畫 | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| 焦點 | `ADB.Media.PlayerState.InFocus` | `inFocus` |

資料的計算方式與標準和自訂狀態相同，但Analytics報表的資料儲存方式不同。

**針對標準狀態**-當您從Analytics報表（管理員端）的「媒體管理」控制台啟用播放器狀態追蹤時，有15個解決方案變數可用於報告和資料匯出。

**針對自訂狀態**-您可以建立自己的處理規則，將計算值儲存至自訂事件，然後使用這些規則來報告和匯出資料。

## 準則

* 一個視訊作業限制為10個獨特的自訂播放器狀態。
* 如果多個播放器狀態通過，則僅保留前10個並轉發到下游的VA(?video analytics)處理元件。
* 所有狀態最多應用10個狀態，無論它們是否關閉。
* 同一狀態可以啟動和結束任意次數，並計為單一狀態。
* 超過自訂上限的每個狀態？ 狀態(10)被丟棄。

## 自訂狀態

您可以建立自訂狀態，在播放作業階段期間擷取自訂動作並更新自訂中繼資料。

需要有關自訂狀態的更多資訊
