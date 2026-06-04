---
title: 應用程式版本
description: 報告用於每個串流工作階段的媒體播放器應用程式版本。
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 4%

---


# 應用程式版本

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**應用程式版本**&#x200B;報告維度。 如需如何收集此變數，請參閱[應用程式版本](/help/implementation/variables/core/app-version.md)。*

>[!ENDSHADEBOX]

**應用程式版本**&#x200B;維度會報告在SDK初始化時設定的媒體播放器應用程式版本字串。 使用它來識別哪些播放器版本正在使用中、將品質或行為變更與特定發行版本建立關聯，並優先支援廣泛使用的版本。

>[!NOTE]
>
>此維度會擷取&#x200B;**媒體播放器應用程式**&#x200B;的版本，而非Adobe的SDK資料庫。 Adobe自己的SDK程式庫版本會作為個別的內部欄位自動收集。

## 如何填入此維度

應用程式版本在SDK初始化時設定一次，並自動納入每個工作階段開始請求中。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 使用Edge實作時透過XDM欄位對應自動收集。 若為僅限Analytics的實作，請使用[處理規則](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/processing-rules.md)將內容資料`media.sdkVersion`對應至自訂eVar。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.appVersion`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料摘要 | 沒有專用的資料摘要欄。 對於僅限Analytics的實作，請使用透過處理規則設定的自訂eVar的資料摘要欄。 |
| Audience Manager | `c_contextdata.media.sdkVersion` （僅限Analytics實施） |

## 維度項目

每個專案都是在SDK初始化時設定的常值版本字串。 在您的實施中使用一致的版本化Scheme，讓版本字串可以預測地在報表中累計。
