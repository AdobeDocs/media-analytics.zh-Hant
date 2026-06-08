---
title: 章節名稱
description: 設定每個章節的易記名稱，讓章節層級報表可以依章節標題劃分。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 8%

---


# 章節名稱

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**章節名稱**變數的資料集合。 如需對應的報表維度，請參閱[章節名稱](/help/reporting/dimensions/chapter-name.md)。*

>[!ENDSHADEBOX]

章節名稱變數是章節的可讀取標題（例如，`"Pilot Episode - Opening"`）。 在內容分成章節的每個`media.chapterStart`事件上設定它。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.chapter.friendlyName` |
| **XDM集合欄位** | [`xdm.mediaCollection.chapterDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **Audience Manager特徵** | `c_contextdata.a.media.chapter.friendlyName` |
| **必要** | 否 |
| **與**&#x200B;一起傳送 | [章節開始](/help/implementation/events/chapters/chapter-start.md)，章節關閉 |

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`xdm.mediaCollection.chapterDetails`內設定`friendlyName`：

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

將章節名稱作為第一個(`name`)引數傳遞給`createChapterObject`。

```swift
let chapterObject = Media.createChapterObjectWith(name: "Pilot Episode - Opening",
                                              position: 1,
                                                length: 240,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

>[!TAB Android]

將章節名稱作為第一個(`name`)引數傳遞給`createChapterObject`。

```kotlin
val chapterObject = Media.createChapterObject("Pilot Episode - Opening",
                                              1L,
                                              240.0,
                                              0.0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

>[!TAB Roku Edge]

呼叫`media.chapterStart`的`sendMediaEvent`時，在`xdm.mediaCollection.chapterDetails`中設定`friendlyName`：

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

呼叫`xdm.mediaCollection.chapterDetails`內有`friendlyName`的[chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart)端點：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.chapterStart",
      "mediaCollection": {
        "chapterDetails": {
          "friendlyName": "Pilot Episode - Opening",
          "index": 1,
          "offset": 0,
          "length": 240
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

>[!ENDTABS]

## 舊版實作型別（僅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

將章節名稱作為第一個引數傳遞給`ADB.Media.createChapterObject`：

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length (seconds)
  0                           // start time (seconds)
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, contextData);
```

>[!TAB Chromecast]

將章節名稱作為第一個引數(`name`)傳遞給`ADBMobile.media.createChapterObject`：

```javascript
var chapterInfo = ADBMobile.media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length
  0                           // startTime
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterStart, chapterInfo, null);
```

>[!TAB Roku 2.x]

將章節名稱作為第一個引數(`name`)傳遞給`adb_media_init_chapterinfo`：

```brightscript
adb = ADBMobile()
chapterInfo = adb_media_init_chapterinfo("Pilot Episode - Opening", 1, 240.0, 0.0)  ' name, position, length, startTime

adb.mediaTrackEvent(adb.MEDIA_CHAPTER_START, chapterInfo)
```

>[!TAB 媒體收集API]

在`chapterStart` POST要求的`params`物件中包含`media.chapter.friendlyName`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.friendlyName": "Pilot Episode - Opening"
  }
}
```

如需完整的要求結構，請參閱[媒體收集API事件參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。

>[!ENDTABS]
