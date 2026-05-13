---
title: 心率參數說明
description: 探索 Adobe 會收集並於 Media Analytics (心率) 伺服器上處理的心率參數。
uuid: e9ddda32-0952-43d0-a702-49f5b1bfd8cf
exl-id: ffa67b5e-ee54-4a5b-8064-decd108f944b
feature: Streaming Media, Variables
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/kBThvgKw7QOwvcWzdGwwipkudTGhhbLB0BRq-z3PPWQ
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: b3f03848-ae12-48b2-8aab-cad18567eb32id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: e7d92df1-c5ba-4e93-85df-f83171b889beid: e992d880-33bc-4949-a648-aa7d410276cdid: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 672
ht-degree: 99%

---

# Media Analytics (心率) 參數說明{#heartbeat-parameter-descriptions}

Adobe 收集並於 Media Analytics (心率) 伺服器上處理的 Media Analytics 參數清單：

## 所有事件

| 名稱 | 資料來源 |  說明  |
| ---  | --- | --- |
| `s:event:type` | Media SDK | (必要)<br/><br/>要追蹤的事件類型。 事件類型： <ul> <li> s:event:type=start </li> <li> `s:event:type=complete` </li> <li> `s:event:type=chapter_start` </li> <li> `s:event:type=chapter_complete` </li> <li> `s:event:type=buffer` </li> <li> `s:event:type=pause` </li> <li> `s:event:type=resume` </li> <li> `s:event:type=bitrate_change` </li> <li> `s:event:type=aa_start` </li> <li> `s:event:type=stall` </li> <li> `s:event:type=end` </li> </ul> |
| `l:event:prev_ts` | Media SDK | (必要)<br/><br/>此工作階段中相同類型的上次事件時間戳記。 值為 -1。 |
| `l:event:ts` | Media SDK | (必要)<br/><br/>事件的時間戳記。 |
| `l:event:duration` | Media SDK | (必要)<br/><br/>此值是由 Media SDK 從內部 (而非由播放器) 設定 (以毫秒為單位)。 它是用於運算後端量度所花時間。 例如，a.media.totalTimePlayed 是以產生所有 Play (type=play) 心率持續時間的總和來計算。 <br/>*注意：*&#x200B;某些事件的這個參數會設為 0，因為這些事件是「狀態變更事件」(例如 type=complete, type=chapter_complete, or type=bitrate_change)。 |
| `l:event:playhead` | VideoInfo | (必要)<br/><br/>事件記錄時，播放點位於目前作用中的資產內 (主要內容或廣告)。 |
| `s:event:sid` | Media SDK | (必要)<br/><br/>工作階段 ID (隨機產生的字串)。 某個工作階段 (視訊 + 廣告) 中的所有事件應該是相同的。 |
| `l:asset:duration` / `l:asset:length` <br/>（已將長度重新命名為持續時間） | VideoInfo | (必要)<br/><br/>主要資產的影片資產長度。 |
| `s:asset:publisher` | MediaHeartbeatConfig | (必要)<br/><br/>資產的發佈者。 |
| `s:asset:video_id` | VideoInfo | (必要)<br/><br/>此 ID 會唯一識別發佈者編目中的影片。 |
| `s:asset:type` | Media SDK | (必要)<br/><br/>資產類型 (主要或廣告)。 |
| `s:stream:type` | VideoInfo | (必要)<br/><br/>資料流類型。 可以是下列其中一項： <ul> <li> live </li> <li> VOD </li> <li> 線性 </li> </ul> |
| `s:user:id` | 行動應用程式測量 VisitorID 的設定物件 | (選用)<br/><br/>使用者明確設定的訪客 ID。 |
| `s:user:aid` | Experience Cloud 組織 | (選用)<br/><br/>使用者的 Analytics 訪客 ID 值。 |
| `s:user:mid` | Experience Cloud 組織 | (必要)<br/><br/>使用者的 Experience cloud 訪客 ID 值。 |
| `s:cuser:customer_user_ids_x` | MediaHeartbeatConfig | (選用)<br/><br/>在 Audience Manager 上設定的所有使用者 ID。 |
| `l:aam:loc_hint` | MediaHeartbeatConfig | (必要)<br/><br/>aa_start 之後每個裝載時傳送的 AAM 資料 |
| `s:aam:blob` | MediaHeartbeatConfig | (必要)<br/><br/>aa_start 之後每個裝載時傳送的 AAM 資料 |
| `s:sc:rsid` | 報表套裝 ID。 | (必要)<br/><br/>應該傳送報表的 Adobe Analytics RSID。 |
| `s:sc:tracking_server` | MediaHeartbeatConfig | (必要)<br/><br/>Adobe Analytics 追蹤伺服器。 |
| `h:sc:ssl` | MediaHeartbeatConfig | (必要)<br/><br/>流量是透過 HTTPS (若設為 1) 或透過 HTTP (設為 0)。 |
| `s:sp:ovp` | MediaHeartbeatConfig | (選用)<br/><br/>設為黃金時段播放器的「黃金時段」，或其他播放器的實際 OVP。 |
| `s:sp:sdk` | MediaHeartbeatConfig | (必要)<br/><br/>OVP 版本字串。 |
| `s:sp:player_name` | VideoInfo | (必要)<br/><br/>視訊播放器名稱 (實際播放器軟體，用來識別播放器)。 |
| `s:sp:channel` | MediaHeartbeatConfig | (選用)<br/><br/>使用者觀看內容的頻道。 若為行動應用程式，則為應用程式名稱。 若為網站，則為網域名稱。 |
| `s:sp:hb_version` | Media SDK | (必要)<br/><br/>發出呼叫的 Media SDK 程式庫的版本號碼。 |
| `l:stream:bitrate` | QoSInfo | (必要)<br/><br/>資料流位元速率的目前值 (以每秒位元組數為單位)。 |

## 錯誤事件

| 名稱 | 資料來源 | 說明   |
| ---  | --- | --- |
| `s:event:source` | Media SDK | (必要)<br/><br/>錯誤的來源，可能是播放器內部或應用程式層級。 |
| `s:event:id` | Media SDK | (必要)<br/><br/>錯誤 ID，可唯一識別錯誤。 |

## 廣告事件

| 名稱 | 資料來源 | 說明   |
| ---  | --- | --- |
| `s:asset:ad_id` | AdInfo | (必要)<br/><br/>廣告的名稱。 |
| `s:asset:ad_sid` | Media SDK | (必要)<br/><br/>Media SDK 產生的唯一識別碼會附加至所有與廣告相關的 Ping 上。 |
| `s:asset:pod_id` | Media SDK | (必要)<br/><br/>影片內的 Pod ID。 系統會依據下列公式自動運算此值：<br/>`MD5(video_id) + `<br/>`"_" + `<br/>`[pod index]` |
| `s:asset:pod_position` | AdBreakInfo | (必要)<br/><br/>Pod 內的廣告索引 (第一個廣告索引為 0，第二個廣告索引為 1，以此類推)。 |
| `s:asset:resolver` | AdBreakInfo | (必要)<br/><br/>廣告解析程式。 |
| `s:meta:custom_ad_metadata.x` | MediaHeartbeat | (選用)<br/><br/>自訂廣告中繼資料。 |

## 章節事件

| 名稱 | 資料來源 | 說明   |
| ---  | --- | --- |
| `s:stream:chapter_sid` | Media SDK | (必要)<br/><br/>與章節的播放例項相關聯的唯一識別碼。<br/> **注意：** 由於使用者執行的向後搜尋操作，章節可以播放許多次。 |
| `s:stream:chapter_name` | ChapterInfo | (選用)<br/><br/>章節的易記 (亦即人類看得懂的) 名稱。 |
| `s:stream:chapter_id` | Media SDK | (必要)<br/><br/>章節的唯一 ID。 系統會依據下列公式自動運算此值：<br/>`MD5(video_id) +`<br/>` "_" +`<br/>`chapter_pos` |
| `l:stream:chapter_pos` | ChapterInfo | (必要)<br/><br/>章節清單中章節的索引 (從 1 開始)。 |
| `l:stream:chapter_offset` | ChapterInfo | (必要)<br/><br/>章節在主要內容 (不包括廣告) 中的偏移量 (以秒為單位表示)。 |
| `l:stream:chapter_length` | ChapterInfo | (必要)<br/><br/>章節的期間 (以秒為單位表示)。 |
| `s:meta:custom_chapter_metadata.x` | ChapterInfo | (選用)<br/><br/>自訂章節中繼資料。 |

## 作業結束事件

| 名稱 | 資料來源 | 說明   |
| ---  | --- | --- |
| `s:event:type=end` | Media SDK | (必要)<br/><br/> `end` `close` |
