---
seo-title: 心率參數說明
title: 心率參數說明
uuid: e9dda32-0952-43d-a702-49f5 b1 bfd8 cf
translation-type: tm+mt
source-git-commit: 6e13e9a6250949a3a7f059445da772b4db1fdb71

---


# 心率參數說明{#heartbeat-parameter-descriptions}

Adobe在心率伺服器上收集和處理的心率參數清單：

## 所有事件

| 名稱 | 必要/選用 | 資料來源 | 說明   |
| ---  | :---: | --- | --- |
| `s:event:type` | R | Media SDK | 要追蹤的事件類型。事件類型: <ul> <li> `s:event:type=start` </li> <li> `s:event:type=complete` </li> <li> `s:event:type=chapter_start` </li> <li> `s:event:type=chapter_complete` </li> <li> `s:event:type=buffer` </li> <li> `s:event:type=pause` </li> <li> `s:event:type=resume` </li> <li> `s:event:type=bitrate_change` </li> <li> `s:event:type=aa_start` </li> <li> `s:event:type=stall` </li> <li> `s:event:type=end` </li> </ul> |
| `l:event:prev_ts` | R | Media SDK | 此工作階段中相同類型的上次事件時間戳記。The value is `-1` |
| `l:event:ts` | R | Media SDK | 事件的時間戳記。 |
| `l:event:duration` | R | Media SDK | 此值是由 VHL 程式庫從內部 (而非由播放器) 設定 (單位: 毫秒)。它是用於運算後端量度所花時間。For example `a.media.totalTimePlayed` `type=play` Note:  For some of the HB that are sent This parameter is set to 0 for certain events because they are "state change events" (e.g., `type=complete` `type=chapter_complete` `type=bitrate_change` |
| `l:event:playhead` | R | `VideoInfo` | 事件記錄時，播放點位於目前作用中的資產內 (主要內容或廣告)。 |
| `s:event:sid` | R | Media SDK | 工作階段 ID (隨機產生的字串)。某個工作階段 (視訊 + 廣告) 中的所有事件應該是相同的。 |
| `l:asset:duration / l:asset:length` (重新命名自 `length``duration` | R | `VideoInfo` | 主要資產的影片資產長度。 |
| `s:asset:publisher` | R | `MediaHeartbeatConfig` | 資產的發佈者。 |
| `s:asset:video_id` | R | `VideoInfo` | 此 ID 會唯一識別發佈者目錄中的影片。 |
| `s:asset:type` | R | Media SDK | 資產類型 (主要或廣告)。 |
| `s:stream:type` | R | `VideoInfo` | 以下是可能會出現的資料流類型: <ul> <li> `live` </li> <li> `vod` </li> <li> `linear` </li> </ul>實施流量分類。 |
| `s:user:id` | O | 行動應用程式測量 VisitorID 的設定物件 | 使用者明確設定的訪客 ID。 |
| `s:user:aid` | O | Experience Cloud 組織 | 使用者的 Analytics 訪客 ID 值。 |
| `s:user:mid` | R | Experience Cloud 組織 | 使用者的 Experience cloud 訪客 ID 值。 |
| `s:cuser:customer_user_ids_x` | O | `MediaHeartbeatConfig` | 在 Audience Manager 上設定的所有使用者 ID |
| `l:aam:loc_hint` | R | `MediaHeartbeatConfig` | AAM data sent on each payload after `aa_start` |
| `s:aam:blob` | R | `MediaHeartbeatConfig` | AAM data sent on each payload after `aa_start` |
| `s:sc:rsid` | R | 報表套裝 ID。 | 應該傳送報表的 SiteCatalyst RSID。 |
| `s:sc:tracking_server` | R | `MediaHeartbeatConfig` | SiteCatalyst 追蹤伺服器。 |
| `h:sc:ssl` | R | `MediaHeartbeatConfig` | 流量是透過 HTTPS (若設為 1) 或透過 HTTP (設為 0)。 |
| `s:sp:ovp` | O | `MediaHeartbeatConfig` | 設定為黃金時段播放器的「黃金時段」，或其他播放器的實際 OVP。 |
| `s:sp:sdk` | R | `MediaHeartbeatConfig` | OVP 版本字串。 |
| `s:sp:player_name` | R | `VideoInfo` | 視訊播放器名稱 (實際播放器軟體，用來識別播放器)。 |
| `s:sp:channel` | O | `MediaHeartbeatConfig` | 使用者觀看內容的頻道。若為行動應用程式，則為應用程式名稱。若為網站，則為網域名稱。 |
| `s:sp:hb_version` | R | Media SDK | 發出呼叫的 VideoHeartbeat 程式庫的版本號碼。 |
| `l:stream:bitrate` | R | `QoSInfo` | 資料流位元速率的目前值 (以每秒位元組數為單位)。 |

## 錯誤事件

| 名稱 | 必要/選用 | 資料來源 | 說明   |
| ---  | :---: | --- | --- |
| `s:event:source` | R | Media SDK | 錯誤的來源，可能是播放器內部或應用程式層級。 |
| `s:event:id` | R | Media SDK | 錯誤 ID 可以不重複識別錯誤。 |

## 廣告事件

| 名稱 | 必要/選用 | 資料來源 | 說明   |
| ---  | :---: | --- | --- |
| `s:asset:ad_id` | R | `AdInfo` | 廣告名稱。 |
| `s:asset:ad_sid` | R | Media SDK | Media SDK 產生的唯一識別碼會附加至所有與廣告相關的 Ping 上。 |
| `s:asset:pod_id` | R | Media SDK | 影片內的 Pod ID。系統會依據下列公式自動運算此值: `MD5(video_id) + "_" + [pod index]` |
| `s:asset:pod_position` | R | `AdBreakInfo` | Pod 內的廣告索引 (第一個廣告索引為 0，第二個廣告索引為 1，以此類推)。 |
| `s:asset:resolver` | R | `AdBreakInfo` | 廣告解析程式。 |
| `s:meta:custom_ad_metadata.x` | O | `MediaHeartbeat` | 自訂廣告中繼資料。 |

## 章節事件

| 名稱 | 必要/選用 | 資料來源 | 說明   |
| ---  | :---: | --- | --- |
| `s:stream:chapter_sid` | R | Media SDK | 與章節的播放例項相關聯的唯一識別碼。注意: 由於使用者執行的向後搜尋操作，章節可以播放許多次。 |
| `s:stream:chapter_name` | O | `ChapterInfo` | 章節的易記 (亦即人類看得懂的) 名稱。 |
| `s:stream:chapter_id` | R | Media SDK | 章節的唯一 ID。系統會依據下列公式自動運算此值: `MD5(video_id) + "_" + chapter_pos` |
| `l:stream:chapter_pos` | R | `ChapterInfo` | 章節清單中章節的索引 (從 1 開始)。 |
| `l:stream:chapter_offset` | R | `ChapterInfo` | 章節在主內容 (不包括廣告) 中的偏移量 (以秒為單位表示)。 |
| `l:stream:chapter_length` | R | `ChapterInfo` | 章節的期間 (以秒表示)。 |
| `s:meta:custom_chapter_metadata.x` | O | `ChapterInfo` | 自訂章節中繼資料。 |

## 作業結束事件

| 名稱 | 必要/選用 | 資料來源 | 說明   |
| ---  | :---: | --- | --- |
| `s:event:type=end` | R | Media SDK | 該 `end` `close` |

