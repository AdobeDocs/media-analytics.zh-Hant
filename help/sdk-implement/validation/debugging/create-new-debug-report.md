---
title: 建立新的 Debug 報表
description: 本主題說明如何建立新的除錯報表。
uuid: 438fde3d-98f9-46d1-9672-75d204361568
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 建立新的 Debug 報表{#create-a-new-debug-report}

若要建立新的 Debug 報表:

1. In [!UICONTROL Create New Debug Report] select the following:

   ![](assets/create-new-debug-report.png)

1. 將以下資訊填入欄位:

   * **為報表命名** - 輸入播放器名稱和日期，以便在認證期間輕鬆追蹤播放器，同時持續區隔品牌和平台。
   * **Adobe Analytics**

      * [!UICONTROL 使用者名稱]和[!UICONTROL 共用機密] - 這些是選用欄位，不過您可以將網站服務 API 認證新增到 Adobe Debug，顯示不同的報表套裝名稱和設定。

         您可以利用以下任一方式存取:

         * [!UICONTROL 「Analytics &gt; 管理員 &gt; 公司設定 &gt; 網站服務」]
         * [!UICONTROL 「Analytics &gt; 管理員 &gt; 使用者管理 &gt; 使用者 &gt; 個別使用者設定」]若要為新使用者建立網站服務 API 認證，請在[!UICONTROL 「使用者管理」]中將使用者新增到&#x200B;**「網站服務存取」**&#x200B;使用者群組。
      * [!UICONTROL 預設端點] -此欄位中的資料由Adobe提供，無法變更。
      * [!UICONTROL 額外端點] -如果您 `CNAMES`使用，則新增用於追蹤伺服器(例如 `metrics.companyname.com`
   * **視訊心率（媒體分析）**

      * [!UICONTROL 預設端點] -此欄位中的資料由Adobe提供，無法變更。
      * [!UICONTROL 額外端點] -如 `CNAMES`果您使用端點，請為追蹤伺服器新增，例如 `metrics.companyname.com`:



