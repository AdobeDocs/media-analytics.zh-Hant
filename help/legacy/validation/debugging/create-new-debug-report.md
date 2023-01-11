---
title: 建立新的 Debug 報表
description: 了解如何建立新的 Debug 報表。
uuid: 438fde3d-98f9-46d1-9672-75d204361568
exl-id: 047acf35-8c1c-4493-9ee7-e2bad47c351e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '203'
ht-degree: 100%

---

# 建立新的 Debug 報表{#create-a-new-debug-report}

若要建立新的 Debug 報表：

1. 在[!UICONTROL 「建立新的 Debug 報表」]中選取以下項目：

   ![](assets/create-new-debug-report.png)

1. 將以下資訊填入欄位：

   * **為報表命名** - 輸入播放器名稱和日期，以便在認證期間輕鬆追蹤播放器，同時持續區隔品牌和平台。
   * **Adobe Analytics**

      * [!UICONTROL 使用者名稱]和[!UICONTROL 共用機密] - 這些是選用欄位，不過您可以將網站服務 API 認證新增到 Adobe Debug，顯示不同的報表套裝名稱和設定。

         您可以利用以下任一方式存取：

         * [!UICONTROL 「Analytics > 管理員 > 公司設定 > 網站服務」]
         * [!UICONTROL 「Analytics > 管理員 > 使用者管理 > 使用者 > 個別使用者設定」]若要為新使用者建立網站服務 API 認證，請在[!UICONTROL 「使用者管理」]中將使用者新增到&#x200B;**「網站服務存取」**&#x200B;使用者群組。
      * [!UICONTROL 「預設端點」]- 此欄位中的資料由 Adobe 提供，因此無法變更。
      * [!UICONTROL 「額外端點」]- 您可新增 `CNAMES`（如果有使用的話），來追蹤 `metrics.companyname.com` 之類的伺服器
   * **視訊心率 (Media Analytics)**

      * [!UICONTROL 「預設端點」]- 此欄位中的資料由 Adobe 提供，因此無法變更。
      * [!UICONTROL 「額外端點」]- 您可新增 `CNAMES`，（如果有使用的話），來追蹤 `metrics.companyname.com` 之類的伺服器。
