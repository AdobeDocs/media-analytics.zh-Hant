---
title: 章節位置
description: 在內容內設定章節索引。 章節ID需要章節位置才能正確自動產生。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 6%

---


# 章節位置

>[!BEGINSHADEBOX]

*本頁涵蓋&#x200B;**章節位置**&#x200B;變數的資料集合。 如需對應的報表維度，請參閱[章節位置](/help/reporting/dimensions/chapter-position.md)。*

>[!ENDSHADEBOX]

章節位置變數是內容內章節的索引，從`1` （典型）或`0` （視您的慣例而定）開始。 在每個章節使用穩定索引，讓相同的章節跨工作階段累計。

| 屬性 | 價值 |
| --- | --- |
| **內容資料變數** | `a.media.chapter.position` |
| **XDM集合欄位** | [`xdm.mediaCollection.chapterDetails.index`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **Audience Manager特徵** | `c_contextdata.a.media.chapter.position` |
| **必要** | 否（行動SDK）；是（Edge、媒體收集API） |
| **與**&#x200B;一起傳送 | [章節開始](/help/implementation/events/chapters/chapter-start.md)，章節關閉 |

## 建議的實作型別

>[!BEGINTABS]

>[!TAB Web SDK]

呼叫[`sendEvent`](https://experienceleague.adobe.com/tw/en/docs/experience-platform/collection/js/commands/sendevent/overview)時，在`xdm.mediaCollection.chapterDetails`內設定`index`：

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

將章節位置作為第二個引數傳給`createChapterObject`。

```swift
let chapterObject = Media.createChapterObjectWith(name: "Pilot Episode - Opening",
                                              position: 1,
                                                length: 240,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

>[!TAB Android]

將章節位置作為第二個引數傳給`createChapterObject`。

```kotlin
val chapterObject = Media.createChapterObject("Pilot Episode - Opening",
                                              1L,
                                              240.0,
                                              0.0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

>[!TAB Roku Edge]

呼叫`media.chapterStart`的`sendMediaEvent`時，在`xdm.mediaCollection.chapterDetails`中設定`index`：

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

呼叫`xdm.mediaCollection.chapterDetails`內有`index`的[chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart)端點：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.chapterStart",
      "mediaCollection": {
        "chapterDetails": {
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

將章節位置作為第二個引數傳遞給`ADB.Media.createChapterObject`：

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Pilot Episode - Opening",
  1,
  240,
  0
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, contextData);
```

>[!TAB Chromecast]

將章節位置作為第二個引數傳遞給`ADBMobile.media.createChapterObject`：

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

將章節位置作為第二個引數(`position`)傳遞給`adb_media_init_chapterinfo`：

```brightscript
adb = ADBMobile()
chapterInfo = adb_media_init_chapterinfo("Pilot Episode - Opening", 1, 240.0, 0.0)  ' name, position, length, startTime

adb.mediaTrackEvent(adb.MEDIA_CHAPTER_START, chapterInfo)
```

>[!TAB 媒體收集API]

在`chapterStart` POST要求的`params`物件中包含`media.chapter.index`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.index": 1
  }
}
```

如需完整的要求結構，請參閱[媒體收集API事件參考](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。

>[!ENDTABS]
