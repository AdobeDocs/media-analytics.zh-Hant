---
title: 建立新的 Debug 報表
description: 了解如何建立新的 Debug 報表。
uuid: 438fde3d-98f9-46d1-9672-75d204361568
exl-id: 047acf35-8c1c-4493-9ee7-e2bad47c351e
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 52%

---

# 建立新的 Debug 報表{#create-a-new-debug-report}

若要建立新的 Debug 報表：

1. 在[!UICONTROL 「建立新的 Debug 報表」]中選取以下項目：

   ![](assets/create-new-debug-report.png)

1. 將以下資訊填入欄位：

   * **為報告命名** — 輸入播放器名稱和日期，以便在認證期間輕鬆追蹤播放器，並將品牌和平台分開。
   * **Adobe Analytics**

      * [!UICONTROL 使用者名稱]和[!UICONTROL 共用機密] — 這些欄位是選擇性的，但您可以將網站服務API認證新增至Adobe Debug，以顯示報表套裝的變數名稱和變數設定。

        您可以利用以下任一方式存取：

         * [!UICONTROL Analytics >管理員>公司設定>網站服務]
         * [!UICONTROL Analytics >管理員>使用者管理>使用者>個別使用者設定]若要為新使用者建立網站服務API認證，請在[!UICONTROL 使用者管理]中將使用者新增至&#x200B;**網站服務存取**&#x200B;使用者群組。

      * [!UICONTROL 「預設端點」]- 此欄位中的資料由 Adobe 提供，因此無法變更。
      * [!UICONTROL 「額外端點」]- 您可新增 `CNAMES`（如果有使用的話），來追蹤 `metrics.companyname.com` 之類的伺服器

   * **視訊心率 (Media Analytics)**

      * [!UICONTROL 「預設端點」]- 此欄位中的資料由 Adobe 提供，因此無法變更。
      * [!UICONTROL 「額外端點」]- 您可新增 `CNAMES`，（如果有使用的話），來追蹤 `metrics.companyname.com` 之類的伺服器。
