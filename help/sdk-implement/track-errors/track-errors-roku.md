---
seo-title: 在 Roku 上追蹤錯誤
title: 在 Roku 上追蹤錯誤
uuid: 4e0165f9-9169-47ed-9f11-ea8 a8778 f663
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# 在 Roku 上追蹤錯誤{#track-errors-on-roku}

>[!IMPORTANT]
>
>下列指示提供所有 2.x SDK 之間實作的指引。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](../../sdk-implement/download-sdks.md)

## 實施錯誤追蹤

1. 追蹤媒體播放器錯誤：

   ```
   ADBMobile().mediaTrackError(msg.GetMessage(), 
                               ADBMobile().ERROR_SOURCE_PLAYER)
   ```

>[!NOTE]
>
>追蹤媒體播放器錯誤不會停止媒體追蹤工作階段。If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

