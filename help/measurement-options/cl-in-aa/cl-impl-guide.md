---
title: 自訂連結實施指南
description: null
uuid: 83315e73-20ca-4db5-9d43-33daade45a13
translation-type: tm+mt
source-git-commit: 72cdf2d03ebae6998514c9092ab462c29345c9f9
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 86%

---


# 自訂連結實施指南{#custom-link-implementation-guide}

自訂視訊追蹤採用 Analytics `appMeasurement` 中的[使用自訂連結程式碼手動追蹤連結](https://docs.adobe.com/content/help/en/media-analytics/using/measurement-options/cl-in-aa/cl-impl-guide.html)。自訂視訊連結視訊追蹤經常用於不太需要視訊測量的平台與裝置上。

* 在 JavaScript 中: `s.tl()` 函數
* 在行動應用程式中: [trackAction() Android](https://docs.adobe.com/content/help/en/mobile-services/android/analytics-android/actions.html)、[trackAction() iOS](https://docs.adobe.com/content/help/en/mobile-services/ios/analytics-ios/actions.html)、[trackAction() OTT](/help/sdk-implement/analytics-with-ott/track-app-actions.md)
* 在 Data Insertion API 中: [linktype 標記](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/reference/r_supported_tags.md)

## 需求

* 視訊播放器 API 事件與資料的存取權
* 使用 Analytics SDK 時可新增指令碼
* 使用 Data Insertion API 時可新增追蹤信標 (自訂指令碼或硬式編碼)

## 中繼資料

* 您可以將中繼資料視為連結資料的一部分，新增到任何追蹤呼叫中
* 請記得更新 `linkTrackVars` 與 `linkTrackEvents`

```javascript
/* Call on video complete */ 
 
if (e.type == "ended") {  
    s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15'; 
    s.linkTrackEvents = 'event3'; 
    s.prop10 = mediaName; 
    s.eVar10 = mediaName; 
    s.eVar12 = "video"; 
    s.eVar13 = document.title; 
    s.eVar15 = mediaPlayerName; 
    s.events = 'event3'; 
    s.tl(this,'o','Video Complete'); 
};
```

## 為什麼要使用自訂連結

* 需滿足最低必要條件
* 適用於任何平台，包括 NoScript 平台
* 所有計算 (如逗留時間或四分位數) 都必須在自訂指令碼中進行
* 簡單明瞭，沒有隱藏的資料庫或指令碼
* 全面掌握視訊資料的各個層面

## HTML5 播放器適用的範例 JavaScript

```javascript
<script type="text/javascript"> 
  myvideo = document.getElementById('movie'); 
  myvideo.addEventListener('play',myHandler,false); 
  myvideo.addEventListener('seeked',myHandler,false); 
  myvideo.addEventListener('seeking',myHandler,false); 
  myvideo.addEventListener('pause',myHandler,false); 
  myvideo.addEventListener('ended',myHandler,false); 
   
  function myHandler(e) { 
      var video = document.getElementsByTagName('video')[0]; 
      var mediaName="13502979:Sailing"; 
      var mediaLength = video.duration; 
      var mediaPlayerName = "HTML5 Player"; 
      /*Define video offset*/ 
      if (video.currentTime > 0) { 
          mediaOffset = Math.floor(video.currentTime); 
      } else { 
          mediaOffset = 0; 
      }; 
      /*Call on video start*/ 
      if (e.type == "play") { 
          if (mediaOffset == 0) { 
              console.log(mediaPlayerName + 
                ' -> start -> playhead: ' +  
                Math.floor(video.currentTime)); 
              s.linkTrackVars='events,prop10,eVar10,eVar12,eVar13,eVar15'; 
              s.linkTrackEvents='event2'; 
              s.prop10=mediaName; 
              s.eVar10=mediaName; 
              s.eVar12="video"; 
              s.eVar13=document.title; 
              s.eVar15=mediaPlayerName; 
              s.events='event2'; 
              s.tl(this,'o','Video Start'); 
          } 
      }; 
   
      /*Call on video pause*/ 
      if (e.type == "pause") { 
          console.log(mediaPlayerName +' -> pause -> playhead: ' + Math.floor(video.currentTime)); 
          if (video.currentTime != video.duration) { 
              s.linkTrackVars='events,prop10,eVar10,eVar12,eVar13,eVar15'; 
              s.linkTrackEvents='event7'; 
              s.prop10=mediaName; 
              s.eVar10=mediaName; 
              s.eVar12="video"; 
              s.eVar13=document.title; 
              s.eVar15=mediaPlayerName; 
              s.events='event7'; 
              s.tl(this,'o','Video Pause'); 
          } 
      }; 
   
      /*Call on video complete*/ 
      if (e.type == "ended") { 
          console.log(mediaPlayerName + 
            ' -> ended -> playhead: ' + 
            Math.floor(video.currentTime)); 
          s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15'; 
          s.linkTrackEvents = 'event3'; 
          s.prop10= m ediaName; 
          s.eVar10=mediaName; 
          s.eVar12="video"; 
          s.eVar13=document.title; 
          s.eVar15=mediaPlayerName; 
          s.events='event3'; 
          s.tl(this,'o','Video Complete'); 
      }; 
  }; 
</script>
```
