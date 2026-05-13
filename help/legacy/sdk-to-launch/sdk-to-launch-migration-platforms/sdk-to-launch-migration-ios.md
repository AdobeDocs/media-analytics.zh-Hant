---
title: 從獨立Media SDK移轉至Adobe Launch - iOS
description: 了解如何從 Media SDK 移轉至 iOS 版的 Launch。
exl-id: f70b8e1b-cb9f-4230-86b2-171bdaed4615
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/drdnQd83UXJkMKj-isUKPeIHe9xGetwY31HzHf37IEo
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 429
ht-degree: 60%

---

# 從獨立 Media SDK 移轉至 Adobe Launch - iOS

>[!NOTE]
>Adobe Experience Platform Launch 已經過品牌重塑，現在是 Experience Platform 中的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=zh-TW)。

## 設定

### 獨立 Media SDK

在獨立Media SDK中，您可在應用程式中設定追蹤設定，
並在建立追蹤器時將其傳遞至SDK。

```objective-c
ADBMediaHeartbeatConfig *config =
  [[ADBMediaHeartbeatConfig alloc] init];

config.trackingServer = @"namespace.hb.omtrdc.net";
config.channel = @"sample-channel";
config.appVersion = @"v2.0.0";
config.ovp = @"video-provider";
config.playerName = @"native-player";
config.ssl = YES;
config.debugLogging = YES;

ADBMediaHeartbeat* tracker =
  [[ADBMediaHeartbeat alloc] initWithDelegate:self config:config];
```

### Launch 擴充功能

1. 在 Experience Platform Launch 中，按一下您行動屬性的[!UICONTROL 「擴充功能」]標籤
1. 在[!UICONTROL 「編目」]標籤上，找到 Adobe Media Analytics for Audio and Video 擴充功能，然後按一下[!UICONTROL 「安裝」]。
1. 在擴充功能設定頁面中，設定追蹤參數。
Media 擴充功能會使用已設定的參數進行追蹤。

   ![](assets/launch_config_mobile.png)

[設定Media Analytics擴充功能](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)

## 建立追蹤器

### 獨立 Media SDK

在獨立Media SDK中，您可以手動建立`ADBMediaHeartbeatConfig`物件
和設定追蹤引數。 實作委派介面公開
`getQoSObject()` 與 `getCurrentPlaybackTime()functions.`

建立 MediaHeartbeat 例項以供追蹤：

```objective-c
@interface PlayerDelegate : NSObject<ADBMediaHeartbeatDelegate>
@end

@implementation PlayerDelegate {
}

- (NSTimeInterval) getCurrentPlaybackTime {
    // When called should return the current player time in seconds.
    return playhead_;
}

- (nonnull ADBMediaObject*) getQoSObject {
    // When called should return the latest qos values.
    return qosObject_;
}
@end

ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init];

config.trackingServer = @"namespace.hb.omtrdc.net";
config.channel = @"sample-channel";
config.appVersion = @"app-version";
config.ovp = @"video-provider";
config.playerName = @"native-player";
config.ssl = YES;
config.debugLogging = YES;
ADBMediaHeartbeatDelegate* delegate = [[PlayerDelegate alloc] init];

ADBMediaHeartbeat* tracker =
  [[ADBMediaHeartbeat alloc] initWithDelegate:delegate config:config];
```

### Launch 擴充功能

[媒體API參考 — 建立媒體追蹤器](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#createtracker)

建立追蹤器前，請先透過行動核心註冊媒體擴充功能和相依擴充功能。

```objective-c
// Register the extension once during app launch
#import <ACPCore.h>
#import <ACPAnalytics.h>
#import <ACPMedia.h>
#import <ACPIdentity.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [ACPCore setLogLevel:ACPMobileLogLevelDebug];
    [ACPCore configureWithAppId:@"your-launch-app-id"];
    [ACPMedia registerExtension];
    [ACPAnalytics registerExtension];
    [ACPIdentity registerExtension];
    [ACPCore start:nil];
    return YES;
}
```

註冊媒體擴充功能後，可使用以下 API 建立追蹤器。
追蹤器會自動從已設定的啟動屬性中挑選設定。

```objective-c
[ACPMedia createTracker:^(ACPMediaTracker * _Nullable mediaTracker) {
    // Use the instance for tracking media.
}];
```

## 更新播放點和體驗品質值。

### 獨立 Media SDK

在獨立Media SDK中，實作
`ADBMediaHeartbeartDelegate`通訊協定是在建立追蹤器時傳遞。
實施應於以下時間傳回最新的QoE和播放點：
追蹤器呼叫`getQoSObject()`和`getCurrentPlaybackTime()`介面
方法。

### Launch 擴充功能

實作應呼叫，更新目前播放器播放點。
追蹤器公開的`updateCurrentPlayhead`方法。 進行精確追蹤
您應每秒至少呼叫一次此方法。

[媒體API參考 — 更新目前的播放點](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#updatecurrentplayhead)

實作應呼叫「 」，以更新QoE資訊
追蹤器公開的`updateQoEObject`方法。 您應該呼叫此方法
當品品質度發生變更時。

[媒體API參考 — 更新QoE物件](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#createqoeobject)

## 傳遞標準媒體 / 廣告中繼資料

### 獨立 Media SDK

* 標準媒體中繼資料：

  ```objective-c
  ADBMediaObject *mediaObject =
    [ADBMediaHeartbeat createMediaObjectWithName:@"media-name"
                       mediaId:@"media-id"
                       length:60
                       streamType:ADBMediaHeartbeatStreamTypeVod
                       mediaType:ADBMediaTypeVideo];
  
  // Standard metadata keys provided by adobe.
  NSMutableDictionary *standardMetadata = [[NSMutableDictionary alloc] init];
  [standardMetadata setObject:@"Sample show" forKey:ADBVideoMetadataKeySHOW];
  [standardMetadata setObject:@"Sample season" forKey:ADBVideoMetadataKeySEASON];
  [mediaObject setValue:standardMetadata forKey:ADBMediaObjectKeyStandardMediaMetadata];
  
  //Attaching custom metadata
  NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init];
  [mediaMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
  [mediaMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
  
  [tracker trackSessionStart:mediaObject data:mediaMetadata];
  ```

* 標準廣告中繼資料：

  ```objective-c
  ADBMediaObject* adObject =
    [ADBMediaHeartbeat createAdObjectWithName:[adData objectForKey:@"name"]
                       adId:[adData objectForKey:@"id"]
                       position:[[adData objectForKey:@"position"] doubleValue]
                       length:[[adData objectForKey:@"length"] doubleValue]];
  
  // Standard metadata keys provided by adobe.
  NSMutableDictionary *standardMetadata =
    [[NSMutableDictionary alloc] init];
  [standardMetadata setObject:@"Sample Advertiser"
                    forKey:ADBAdMetadataKeyADVERTISER];
  [standardMetadata setObject:@"Sample Campaign"
                    forKey:ADBAdMetadataKeyCAMPAIGN_ID];
  [adObject setValue:standardMetadata
                    forKey:ADBMediaObjectKeyStandardAdMetadata];
  
  //Attaching custom metadata
  NSMutableDictionary *adDictionary = [[NSMutableDictionary alloc] init];
  [adDictionary setObject:@"Sample affiliate" forKey:@"affiliate"];
  
  [tracker trackEvent:ADBMediaHeartbeatEventAdStart
           mediaObject:adObject
           data:adDictionary];
  ```

### Launch 擴充功能

* 標準媒體中繼資料：

  ```objective-c
  NSDictionary *mediaObject =
    [ACPMedia createMediaObjectWithName:@"media-name"
              mediaId:@"media-id"
              length:60
              streamType:ACPMediaStreamTypeVod
              mediaType:ACPMediaTypeVideo];
  
  NSMutableDictionary *mediaMetadata =
    [[NSMutableDictionary alloc] init];
  
  // Standard metadata keys provided by adobe.
  [mediaMetadata setObject:@"Sample show" forKey:ACPVideoMetadataKeyShow];
  [mediaMetadata setObject:@"Sample season" forKey:ACPVideoMetadataKeySeason];
  
  // Custom metadata keys
  [mediaMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
  [mediaMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
  [_tracker trackSessionStart:mediaObject data:mediaMetadata];
  ```

* 標準廣告中繼資料：

  ```objective-c
  NSDictionary* adObject =
    [ACPMedia createAdObjectWithName:@"ad-name"
              adId:@"ad-id"
              position:1
              length:15];
  
  NSMutableDictionary* adMetadata =
    [[NSMutableDictionary alloc] init];
  
  // Standard metadata keys provided by adobe.
  [adMetadata setObject:@"Sample Advertiser" forKey:ACPAdMetadataKeyAdvertiser];
  [adMetadata setObject:@"Sample Campaign" forKey:ACPAdMetadataKeyCampaignId];
  
  // Custom metadata keys
  [adMetadata setObject:@"Sample affiliate" forKey:@"affiliate"];
  
  [tracker trackEvent:ACPMediaEventAdStart mediaObject:adObject data:adMetadata];
  ```
