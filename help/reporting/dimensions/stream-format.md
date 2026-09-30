---
title: 串流格式
description: 報告每個工作階段的品質層級（通常是HD或SD）。
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 7%
---

# 串流格式

>[!BEGINSHADEBOX]

*此頁面涵蓋&#x200B;**資料流格式**&#x200B;報告維度。 如需如何收集此變數，請參閱[資料流格式](/help/implementation/variables/standard-metadata/stream-format.md)。*

>[!ENDSHADEBOX]

**串流格式**&#x200B;維度會報告每個工作階段的品質層級（通常是`"HD"`或`"SD"`，但任何字串皆可接受）。 用它來比較不同傳遞品質層級的參與度、完成度和品質。

## 如何填入此維度

串流格式由播放器在工作階段開始時設定。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 建立將`a.media.format`對應至eVar的[處理規則](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.streamFormat`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `evar1`-`evar250`、`post_evar1`-`post_evar250` （處理規則將`a.media.format`對應至的eVar） |
| Audience Manager | `c_contextdata.a.media.format` |

## 維度項目

每個專案都是工作階段開始時報告的常值格式值。 使用一組穩定的值(`HD`， `SD`， `4K`， `UHD`)，讓條列專案不會在拼字變異間分段。
