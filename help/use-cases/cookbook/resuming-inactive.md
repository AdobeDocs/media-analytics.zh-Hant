---
title: 繼續非作用中工作階段
description: 了解如何處理繼續非作用中工作階段。
uuid: 3ff1205d-7bbe-4016-9bd7-6e34b7862c4c
exl-id: ee4cf7f5-5788-4d35-a04d-4ed714ccd663
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/KT7NfrYlagrMwAjsrbSNR8YUbj5d-ihU8AfJ6wcbgOA
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: 398
ht-degree: 37%

---

# 繼續非作用中工作階段{#resuming-inactive-sessions}

## 長暫停

Media SDK 會自動追蹤媒體播放處於以下非作用中狀態之一的時間：

* 已暫停
* 搜尋
* 已擱置
* 緩衝

如果媒體追蹤工作階段保持在非作用中狀態超過 30 分鐘，將自動關閉工作階段。 如果使用者在先前的非作用中視訊追蹤工作階段之後繼續 (`trackPlay`)，媒體心率會使用先前使用的視訊資訊和中繼資料自動建立新視訊工作階段，並傳送繼續心率事件。

## 使用恢復旗標的跨裝置切換

處理單一應用程式工作階段繼續的恢復機制也適用於檢視器在裝置之間傳輸播放時，例如從手機將視訊播放至電視或Chromecast接收器。 由於每個裝置都會執行其自己的Media SDK例項，因此切換預設會建立多個工作階段。 使用恢復旗標將它們拼接成邏輯延續，以便Analytics將合併檢視報告為單一參與片段，而不是單獨的媒體開始。

**如何實作：**

1. 在檢視者起始轉換時，在&#x200B;**來源裝置** （例如電話）上呼叫`trackSessionEnd`。 請勿呼叫`trackComplete` — 內容尚未完成，正在移至其他裝置。
2. 在&#x200B;**目的地裝置** （例如Chromecast）上，呼叫`trackSessionStart`並將恢復旗標設為`true`且在來源裝置上使用相同的內容中繼資料（名稱、識別碼、長度）。 傳遞檢視器在來源裝置上離開的播放點位置。
3. 如果檢視器稍後將播放傳回來源裝置，請在目的地重複相同的模式： `trackSessionEnd`，並在來源使用繼續旗標重複`trackSessionStart`。

設定繼續旗標會使Adobe Analytics遞增[內容繼續](/help/reporting/metrics/content-resumes.md)，而非[媒體開始](/help/reporting/metrics/media-starts.md)，做為第二個和後續的移交階段。 由於沒有內建機制可讓您在SDK執行個體之間共用工作階段ID，因此恢復標幟是使用者端宣告 — 當您知道檢視器正在繼續前一個工作階段時，可以根據您的應用程式邏輯來傳遞它。

## 手動繼續先前關閉的工作階段

只有在應用程式未關閉時，Media SDK 才會自動繼續工作階段。 如果應用程式儲存使用者資料並有能力繼續先前關閉的媒體，您便可以手動觸發繼續事件。 開始視訊追蹤工作階段時，請設定選用的 Video Resumed 屬性。

### Android

```java
// Set MediaHeartbeat.MediaObjectKey.mediaResumed to true
public void onmediaLoad(Observable observable, Object data) {

  // Replace <MEDIA_NAME> with the media name.
  // Replace <MEDIA_ID> with a media unique identifier.
  // Replace <MEDIA_LENGTH> with the media length.  
  MediaObject mediaInfo = MediaHeartbeat.createMediaObject(  
      <MEDIA_NAME>,  
      <MEDIA_ID>,  
      <MEDIA_LENGTH>,  
      MediaHeartbeat.StreamType.VOD
  );

  // Set to true if this is a resume playback scenario
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.mediaResumed, true);

  _heartbeat.trackSessionStart(mediaInfo, mediaMetadata);
}
```

### iOS

```
- (void)onMainmediaLoaded:(NSNotification *)notification {
  //Replace <MEDIA_NAME> with the media name.
  //Replace <MEDIA_ID> with a media unique identifier.
  //Replace <MEDIA_LENGTH> with the media length.     
  ADBMediaObject *mediaObject =  
    [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME>
                       mediaId:<MEDIA_ID>
                       length:<MEDIA_LENGTH>
                       streamType:ADBMediaHeartbeatStreamTypeVOD];

  //Set to YES if this user is resuming a previously closed media session
  [mediaObject setValue:@(YES) forKey:ADBMediaObjectKeymediaResumed];

  [_mediaHeartbeat trackSessionStart:mediaObject data:mediaMetadata];
}
```

### JavaScript

```js
_onmediaLoad = function () {
  // Replace <MEDIA_NAME> with the media name.
  // Replace <MEDIA_ID> with a media unique identifier.
  // Replace <MEDIA_LENGTH> with the media length.  
  var mediaObject =  
    MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>,  
                                     MediaHeartbeat.StreamType.VOD);

  // Set to true if this user is resuming a previously closed media session
  mediaObject.setValue(MediaObjectKey.mediaResumed, true);
  this._mediaHeartbeat.trackSessionStart(mediaObject, contextData);
};
```
