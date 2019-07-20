---
seo-title: 取得同時檢閱者 JSON 報表資料
title: 取得同時檢閱者 JSON 報表資料
uuid: 9168f114-2459-4951-a06 c-57b735 d09 dc0
translation-type: tm+mt
source-git-commit: 82317dfd0e6eaef20890d03c32fe088a7574ead2

---


# 取得同時檢閱者 JSON 報表資料{#get-concurrent-viewers-json-report-data}

You can obtain concurrent viewers report data using the _* 1.4 version *_ of the Analytics APIs:
* [Analytics API](https://github.com/AdobeDocs/analytics-1.4-apis)
* [Swagger](https://adobedocs.github.io/analytics-1.4-apis/swagger-docs.html#/Report/Report.Get)

1. 使用UI上建立的任何區段來篩選資料。若要依特定的內容ID進行篩選，請建立新區段。
1. Set the `elements` -&gt; `id` in the request body to `videoconcurrentviewers`.
1. 請求足夠數量的資料。Adobe建議使用3200個資料點，以確保資料中沒有空隙。

   * The data range you specify in the report gathers all concurrent viewer data _at the time the video session ended._&#x200B;因此，您必須考慮在一天內開始並在午夜後結束(亦即隔天)的工作階段。

   * Request more than one day of data, but in your analysis _* use only the first day of the data.*_

此案例的請求裝載範例如下：

```
{
  "reportDescription":{
    "reportSuiteID":"[YOUR_RSID]",
    "dateFrom":"2018-07-01",
    "dateTo":"2018-07-02",
    "metrics":[
      {
        "id":"instances"
      }
    ],
    "elements":[
      {
        "id":"videoconcurrentviewers",
        "top":"3200"
      }
    ],
    "segments":[
      {
        "id":"s1234_58ca4fc7e4b0abc238707bb9"                                         
      }
    ],
    "sortBy":"instances",
    "locale":"en_US"
  }
}
```

<!--
You can extract the concurrent viewers report data using the Experience Cloud API Explorer as follows. 

1. Navigate to: [https://marketing.adobe.com/developer/api-explorer.](https://marketing.adobe.com/developer/api-explorer)
1. Select and enter the following information in the API Explorer form:

    * **API -** Select "Report".
    * **Method -** Select "Queue".
    * **Environment -** Select your data center.
    * Request JSON - Specify the following:

        * `reportSuiteID` - For info on reports suites: [Report Suites](https://marketing.adobe.com/resources/help/en_US/sc/implement/ref-reports-report-suites.html)
        
        * `dateTo` - End date of the report.         
        
          >[!NOTE]
          >
          >The maximum time period supported is two days.

        * `dateFrom` - Start date of the report.
        * `elements : id` - Set to `"videoconcurrentviewers"`
        
        * `elements : top` - Specify the number of entries to be returned.

      Sample request body:

      ```    
      {
          "reportDescription": {
              "reportSuiteID": "[Your Report Suite ID]",
              "dateTo": "2017-09-07",
              "dateFrom": "2017-09-07"
              "metrics": [
                  {
                      "id": "instances"
                  }
              ],
              "elements": [
                  {
                      "id": "videoconcurrentviewers",
                      "top": 2880
                  }
              ]
              "locale": "en_US"
          }
      }
      
      ```

      >[!TIP]
      >
      >Some sessions are ended on the next day, and at that point the data will be available for reporting. In that case the best approach is to select 2 days (2880 minutes) of data, and use only the data for the first day (1440 minutes).

1. Click **Get Response**.

   In the Response field, you should get a `reportID`.
1. In the form, change **Method** to "Get".
1. Enter the value of the `reportID` you received in Step 3, and click **Get Response**.

   The concurrent viewers report data, in JSON format, is presented in the Response field.
   
   For example:
   
   ![](assets/api_helper_2.png) 

   ![](assets/api_helper_1.png)

-->
