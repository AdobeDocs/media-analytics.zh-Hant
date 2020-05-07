---
title: 計算量度
description: null
uuid: 9dd35155-58aa-4f05-896e-c5cbc4b13d59
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 計算量度{#calculated-metrics}

>[!NOTE]
>
>以下計算量度已於 2018 年 9 月 13 日導入。

| 量度 | 說明 | 公式 |
|---|---|---|
| 每媒體資料流的平均廣告數 | 每次媒體開始的廣告開始數 | `Ad Starts / Media Starts` |
| 每媒體資料流的平均章節數 | 每次媒體開始的章節開始數 | `Chapter Start / Media Starts` |
| 平均媒體逗留時間 | 每次資料流開始的總逗留時間 (HH:MM:SS) | `Media Time Spent / Media Starts` |
| 平均內容逗留時間 | 每次內容開始的內容逗留時間 (HH:MM:SS) | `Content Time Spent / Content Start` |
| 平均廣告逗留時間 | 每次廣告開始的廣告逗留時間 (HH:MM:SS) | `Ad Time Spent / Ad Start` |
| 平均章節逗留時間 | 每次章節開始的章節逗留時間 (HH:MM:SS) | `Chapter Time Spent / Chapter Start` |
| 媒體結束率 | 內容完成數與媒體起始數的比率 (%) | `Content Completes/ Media Starts` |
| 內容結束率 | 內容結束與內容開始的比率 (%) | `Content Completes / Content Starts` |
| 廣告結束率 | 廣告結束與廣告開始的比率 (%) | `Ad Completes / Ad Starts` |
| 章節結束率 | 章節結束與章節開始的比率 (%) | `Chapter Completes / Chapter Starts` |
| 開始前中斷率 | 開始前掉格與媒體開始的比率 (%) | `Drops before Starts / Media Starts` |
| 內容暫停期間率 | 總暫停期間與內容逗留時間的比率 (%) | `Total Pause Duration / Content Time Spent` |
| 內容緩衝期間率 | 總緩衝期間與內容逗留時間的比率 (% ) | `Total Buffer Duration / Content Time Spent` |
| 內容開始時間率 | 開始時間與內容逗留時間的比率 (%) | `Time to Start / Content Time Spent` |
| 廣告逗留時間率 | 廣告逗留時間與內容逗留時間的比率 (%) | `Ad Time Spent / Content Time Spent` |
