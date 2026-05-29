---
title: 同盟資料
description: 計算透過同盟資料共用而非客戶自己的實作接收的工作階段。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 6%

---


# 同盟資料

>[!AVAILABILITY]
>
>Federated Analytics服務僅在搭配Adobe Analytics使用串流媒體功能時可用。 Customer Journey Analytics中不提供Federated Analytics。

**同盟資料**&#x200B;量度會計算透過同盟資料共用（而非您自己的實作）接收的工作階段。 用它來測量合作夥伴共用工作階段的數量，並將參與度、完成度或品質與第一方工作階段進行比較。

如需詳細資訊，請參閱[同盟媒體](/help/use-cases/federated-media.md)使用案例。

>[!TIP]
>
>如果您想要使用同盟資料做為維度，請建立將`a.media.federated`內容資料變數對應至eVar的[處理規則](https://experienceleague.adobe.com/zh-hant/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。

## 此量度的計算方式

當工作階段經過同盟通道時，媒體後端會設定此旗標。 該量度會在每個合格工作階段增加一次，並在結束通話時回報。

| 報告系統 | 來源 |
| --- | --- |
| Adobe Analytics | 啟用[[!UICONTROL 視訊中繼資料]](/help/reporting/media-reports-enable.md)時，自動從內容資料`a.media.federated`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isFederated`](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 資料饋送 | `event_list`， `post_event_list` （請參閱[`event.tsv`](https://experienceleague.adobe.com/zh-hant/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查閱） |
| Audience Manager | `c_contextdata.a.media.federated` |
