---
seo-title: 計算量度
title: 計算量度
uuid: 9d35155-58aa-4f05-896e-c5 cbc4 b13 d59
translation-type: tm+mt
source-git-commit: 5582243074a712e53dd23071d319a9ad1f89e10e

---


# 計算量度{#calculated-metrics}

>[!NOTE]
>
>這些計算量度於9/13/18推出。

| 量度 | 說明 | Formula |
|---|---|---|
| 平均每一媒體資料流的廣告數 | 每個媒體開始的廣告開始次數 | `Ad Starts / Media Starts` |
| 平均每個媒體資料流的章節數 | 每個媒體啓動章節開始 | `Chapter Start / Media Starts` |
| 平均媒體逗留時間 | 每個媒體啓動總逗留時間(HH：MM：SS) | `Media Time Spent / Media Starts` |
| 平均內容逗留時間 | 每次內容開始的內容逗留時間 (HH:MM:SS) | `Content Time Spent / Content Start` |
| 平均廣告逗留時間 | 每次廣告開始的廣告逗留時間 (HH:MM:SS) | `Ad Time Spent / Ad Start` |
| 平均章節逗留時間 | 每次章節開始的章節逗留時間 (HH:MM:SS) | `Chapter Time Spent / Chapter Start` |
| 媒體結束率 | 內容完成數與媒體起始數的比率 (%) | `Content Completes/ Media Starts` |
| 內容結束率 | 內容結束與內容開始的比率 (%) | `Content Completes / Content Starts` |
| 廣告結束率 | 廣告結束與廣告開始的比率 (%) | `Ad Completes / Ad Starts` |
| 章節結束率 | 章節結束與章節開始的比率 (%) | `Chapter Completes / Chapter Starts` |
| 開始前中斷率 | 開始前掉格與媒體開始的比率 (%) | `Drops before Starts / Media Starts` |
| 內容暫停期間率 | 總暫停期間與內容逗留時間的比率 (%) | `Total Pause Duration / Content Time Spent` |
| 內容緩衝期間率 | 總緩衝期間與內容逗留時間的比率 (%) | `Total Buffer Duration / Content Time Spent` |
| 內容開始時間率 | 開始時間與內容逗留時間的比率 (%) | `Time to Start / Content Time Spent` |
| 廣告逗留時間率 | 廣告逗留時間與內容逗留時間的比率 (%) | `Ad Time Spent / Content Time Spent` |
