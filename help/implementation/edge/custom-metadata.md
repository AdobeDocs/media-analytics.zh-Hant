---
title: 自訂中繼資料支援 — XDM格式
description: 瞭解如何使用Experience Edge XDM格式傳送包含媒體追蹤事件的自訂中繼資料。
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 5%

---


# 自訂中繼資料支援 — XDM格式

Experience Edge API可讓您在`sessionStart`、`adStart`和`chapterStart` API事件中，連同標準XDM欄位一起傳送媒體自訂中繼資料。 透過XDM格式傳送的媒體自訂中繼資料可轉送至&#x200B;**Adobe Analytics**&#x200B;和&#x200B;**Adobe Experience Platform**。

如需媒體收集API實作，請參閱[自訂中繼資料支援](/help/implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md)。

## 概觀

媒體自訂中繼資料可在Experience Edge請求中的兩個位置傳送，每個位置都具有不同的路由行為：

| 位置 | 已傳送至Adobe Analytics | 已傳送至Adobe Experience Platform | 使用案例 |
|----------|------------------------|-----------------------------------|----------|
| `xdm.mediaCollection.customMetadata` | ✅是 | ✅是 | 兩種系統所需的業務資料 |
| `_data` | ✅是 | ❌否 | Analytics專屬標幟或處理提示 |

自訂中繼資料適用於三種事件型別：

| 事件 | 中繼資料套用至 |
|-------|-------------------|
| `sessionStart` | 主要內容（整個工作階段） |
| `adStart` | 個人廣告 |
| `chapterStart` | 內容章節或區段 |

## 結構

### `xdm.mediaCollection.customMetadata` (Analytics + AEP)

自訂中繼資料是`mediaCollection`物件內的&#x200B;**名稱值物件陣列**：

```json
{
  "xdm": {
    "mediaCollection": {
      "customMetadata": [
        {
          "name": "_tenant.fieldName",
          "value": "fieldValue"
        }
      ]
    }
  }
}
```

&lt;InlineAlert variant="warning" slots="text" />

`customMetadata`必須是`mediaCollection`內的&#x200B;**陣列**，而不是在`xdm`根層級。

**不正確：**

```json
{
  "xdm": {
    "eventType": "media.sessionStart",
    "customMetadata": [...]  // ❌ Wrong location
  }
}
```

**正確：**

```json
{
  "xdm": {
    "eventType": "media.sessionStart",
    "mediaCollection": {
      "customMetadata": [...]  // ✅ Inside mediaCollection
    }
  }
}
```

### `_data` （僅限Analytics）

`_data`物件是一種特殊的Experience Edge建構，它會繞過資料集將資料專門傳送到Adobe Analytics。 自訂中繼資料必須放在`__adobe.analytics.contextData`下。

不像`xdm.mediaCollection.customMetadata`使用&#x200B;**名稱值物件陣列**，`_data`對應直接在`contextData`下使用一般&#x200B;**索引鍵值物件**：

| 方法 | 結構 | 目標 |
|----------|-----------|-------------|
| `xdm.mediaCollection.customMetadata` | `{"name": "...", "value": "..."}`物件的陣列 | Analytics + AEP |
| `_data.__adobe.analytics.contextData` | 一般索引鍵值物件`{"key": "value"}` | 僅限Analytics |

```json
{
  "xdm": { ... },
  "_data": {
    "__adobe": {
      "analytics": {
        "contextData": {
          "debugMode": "true",
          "internalTestFlag": "QA-Session"
        }
      }
    }
  }
}
```

### 命名慣例

* **XDM格式：**&#x200B;具有使用底線的租使用者名稱空間的前置詞。 您也可以在租使用者自訂欄位群組（例如`_<tenant>.<struct_name>.<field_name>`）中建立結構。
* **`_data`格式：**&#x200B;欄位放在`_data.__adobe.analytics.contextData`下 — 欄位名稱不需要底線首碼（例如`debugFlag`）

## 主要內容自訂中繼資料

與`sessionStart`一同傳送。 套用至要追蹤的主要媒體，並在整個廣告和章節呼叫中保持可用。 此處定義的任何自訂中繼資料都會由媒體後端在相應的關閉呼叫上自動合併。 它將與為廣告和章節定義的任何特定自訂中繼資料一起包含。

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### 請求

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
          "sessionDetails": {
            "name": "Sample Video",
            "playerName": "HTML5 Player",
            "contentType": "VOD",
            "length": 3600,
            "channel": "Sports"
          },
          "playhead": 0,
          "customMetadata": [
            {
              "name": "_mycompany.contentCategory",
              "value": "Live Sports"
            },
            {
              "name": "_mycompany.leagueType",
              "value": "Professional"
            }
          ]
        },
        "timestamp": "2026-03-10T18:00:00Z"
      }
    }
  ]
}'
```

## 廣告自訂中繼資料

與`adStart`一同傳送。 特定於每個個別廣告。 來自`sessionStart`的自訂中繼資料也會由廣告關閉呼叫上的媒體後端自動合併，連同此處定義的任何廣告特定自訂中繼資料。

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### 請求

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
          "sessionID": "your-session-id",
          "playhead": 30,
          "advertisingDetails": {
            "name": "Summer Sale Ad",
            "playerName": "HTML5 Player",
            "length": 30,
            "podPosition": 1
          },
          "customMetadata": [
            {
              "name": "_mycompany.campaignId",
              "value": "SUMMER2026"
            },
            {
              "name": "_mycompany.targetAudience",
              "value": "18-34"
            },
            {
              "name": "_mycompany.adFormat",
              "value": "skippable"
            }
          ]
        },
        "timestamp": "2026-03-10T18:05:30Z"
      }
    }
  ]
}'
```

## 章節自訂中繼資料

與`chapterStart`一同傳送。 特定於每個內容章節或區段。 來自`sessionStart`的自訂中繼資料也會由章節關閉呼叫上的媒體後端自動合併，連同此處定義的任何章節特定自訂中繼資料。

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### 請求

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.chapterStart",
        "mediaCollection": {
          "sessionID": "your-session-id",
          "playhead": 600,
          "chapterDetails": {
            "friendlyName": "Introduction",
            "length": 300,
            "index": 1,
            "offset": 600
          },
          "customMetadata": [
            {
              "name": "_mycompany.chapterType",
              "value": "tutorial"
            },
            {
              "name": "_mycompany.difficulty",
              "value": "beginner"
            }
          ]
        },
        "timestamp": "2026-03-10T18:10:00Z"
      }
    }
  ]
}'
```

## 使用`_data`物件（僅限Analytics的中繼資料）

當您在Adobe Analytics中需要&#x200B;**不應**&#x200B;儲存在AEP資料集中的中繼資料時，請使用`_data`物件 — 例如，暫時旗標、偵錯變數或Analytics專屬的處理提示。

&lt;InlineAlert variant="warning" slots="text" />

透過`_data`傳送的資料未儲存在Adobe Experience Platform中，因此無法用於Real-Time CDP、Journey Orchestration或其他AEP服務。

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### 請求

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
          "sessionDetails": {
            "name": "Sample Video",
            "playerName": "HTML5 Player",
            "contentType": "VOD",
            "length": 3600
          },
          "playhead": 0,
          "customMetadata": [
            {
              "name": "_mycompany.league",
              "value": "Action"
            }
          ]
        },
        "timestamp": "2026-03-10T18:00:00Z"
      },
      "_data": {
        "__adobe": {
          "analytics": {
            "contextData": {
              "debugMode": "true",
              "testFlag": "QA-Session"
            }
          }
        }
      }
    }
  ]
}'
```

在此範例中，

* `_mycompany.league`→傳送至Analytics和AEP
* `debugMode`和`testFlag` （在`_data.__adobe.analytics.contextData`下）只→傳送到Analytics


## 下游資料位置

&lt;InlineAlert variant="info" slots="text" />

`xdm.mediaCollection.customMetadata`是用來傳送包含事件的自訂中繼資料的&#x200B;**傳入API路徑**。 處理之後，資料會以內容資料變數的形式轉送至Adobe Analytics，並儲存在`xdm.mediaReporting.customMetadata`下的Adobe Experience Platform中，以最上層平面化的欄位形式儲存。

**Adobe Analytics:**

* 處理之後，自訂中繼資料會以內容資料變數的形式轉送至Adobe Analytics。 `_tenant`首碼會自動移除，所以處理規則只會參考`_tenant`之後的欄位路徑（例如，`_mycompany.contentCategory`變成`contentCategory`）
* 透過`_data`傳送的資料也會轉送至Adobe Analytics，並可透過處理規則取得
* 使用處理規則將內容資料變數對應至eVar、prop或其他Analytics變數。 如需詳細資訊，請參閱Adobe Experience Platform Edge Network的[資料變數對應](https://experienceleague.adobe.com/zh-hant/docs/analytics/implementation/aep-edge/data-var-mapping)。

**Adobe Experience Platform：**

* 自訂中繼資料欄位必須定義為XDM結構描述中的自訂欄位（例如`_mycompany`），並且可以在AEP中以平面化的欄位形式儲存和查詢

  ![XDM結構描述中的自訂欄位定義](assets/custom_metadata.png)
* 對於報表和查詢，自訂中繼資料可在`xdm.mediaReporting.customMetadata`下取得，也可作為頂層平面化欄位。 使用最適合您使用案例的專案。
* 區段、Journey Orchestration和Real-Time CDP啟用都可存取

## 行為

* 所有自訂中繼資料值都必須是&#x200B;**字串**。 在傳送之前轉換數字和布林值。
* `sessionStart`中繼資料會在整個工作階段中持續存在；更新需要新的工作階段
* 每個`adStart`和`chapterStart`事件都可以包含不同的自訂中繼資料
* 標準欄位存在時，偏好使用標準XDM欄位(`sessionDetails`、`advertisingDetails`、`chapterDetails`)而非自訂中繼資料

>[!MORELIKETHIS]
>
>* [自訂中繼資料支援](/help/implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md)。 — MC API （JSON格式）
>* [媒體收集詳細資料資料型別](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) — XDM結構描述參考
>* [Adobe Experience Platform Edge Network的資料變數對應](https://experienceleague.adobe.com/zh-hant/docs/analytics/implementation/aep-edge/data-var-mapping) — XDM欄位的Analytics內容資料對應

<!--
* [Session endpoints](sessions.md) — Session lifecycle management
* [Ad endpoints](ads.md) — Track advertising impressions
* [Chapter endpoints](chapters.md) — Segment content into chapters
-->
