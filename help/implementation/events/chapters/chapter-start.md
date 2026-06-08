---
title: 章節開始
description: 代表內容中章節區段的開始。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 7%

---


# 章節開始

章節開始事件代表內容中章節的開始。 章節追蹤為選用，且不是核心媒體追蹤的必要專案。 章節不能重疊；傳送[章節完成](chapter-complete.md)或[章節略過](chapter-skip.md)以關閉目前的章節，然後再開始新章節。

* **必要條件**： [工作階段開始](../session/session-start.md)
* **關聯的量度**： [[!UICONTROL 章節開始]](/help/reporting/metrics/chapter-starts.md)

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

使用`eventType: "media.chapterStart"`和必要的`chapterDetails`來呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterStart",
    mediaCollection: {
      chapterDetails: {
        friendlyName: "Pilot Episode - Opening",
        index: 1,
        offset: 0,
        length: 240
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

將章節名稱、位置、長度和開始時間傳遞至`createChapterObject`，然後呼叫`trackEvent`。

```swift
let chapterObject = Media.createChapterObjectWith(name: "Pilot Episode - Opening",
                                              position: 1,
                                                length: 240,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

>[!TAB Android]

將章節名稱、位置、長度和開始時間傳遞至`createChapterObject`，然後呼叫`trackEvent`。

```kotlin
val chapterObject = Media.createChapterObject("Pilot Episode - Opening",
                                              1,
                                              240,
                                              0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

>[!TAB Roku Edge]

使用`eventType: "media.chapterStart"`和必要的`chapterDetails`來呼叫`sendMediaEvent`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterStart",
        "mediaCollection": {
            "chapterDetails": {
                "friendlyName": "Pilot Episode - Opening",
                "index": 1,
                "offset": 0,
                "length": 240
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

使用必要的`chapterDetails`呼叫[chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart)端點：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.chapterStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0,
        "chapterDetails": {
          "index": 1,
          "length": 240,
          "offset": 0
        }
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## 舊版實作型別（僅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

將章節名稱、位置、長度和開始時間傳遞至`ADB.Media.createChapterObject`：

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length (seconds)
  0                           // start time (seconds)
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, null);
```

>[!TAB Chromecast]

將章節名稱、位置、長度和開始時間傳遞至`ADBMobile.media.createChapterObject`：

```javascript
var chapterInfo = ADBMobile.media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length (seconds)
  0                           // start time (seconds)
);

ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterStart, chapterInfo, null);
```

>[!TAB Roku 2.x]

使用`adb_media_init_chapterinfo`建立章節物件，然後追蹤事件：

```brightscript
adb = ADBMobile()
chapterInfo = adb_media_init_chapterinfo("Pilot Episode - Opening", 1, 240.0, 0.0)  ' name, position, length, startTime

adb.mediaTrackEvent(adb.MEDIA_CHAPTER_START, chapterInfo)
```

>[!TAB 媒體收集API]

傳送`chapterStart`張貼至[事件端點](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.friendlyName": "Pilot Episode - Opening",
    "media.chapter.index": 1,
    "media.chapter.offset": 0,
    "media.chapter.length": 240
  }
}
```

>[!ENDTABS]
