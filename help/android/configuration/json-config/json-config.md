---
description: 此資訊可協助您使用 ADBMobile.json 設定檔案。
seo-description: 此資訊可協助您使用 ADBMobile.json 設定檔案。
seo-title: ADBMobile JSON 設定
solution: Marketing Cloud、Analytics
title: ADBMobile JSON 設定
topic: 開發人員和實施
uuid: 1decf605-7bc3-4e73-ad52-1dex5821599 e
translation-type: tm+mt
source-git-commit: 19264af3f4a675add6f61c27f4cdaf20033b9bb7

---


# ADBMobile JSON config file {#adbmobile-json-config}

此資訊可協助您瞭解ADBMobile. json組態檔中的變數。

## `ADBMobileConfig.json` config檔案參考 {#section_5AD4EDF87E304980B4AC4A5657FDA8B9}

您的應用程式可以跨多平台使用此相同的設定檔案:

>[!TIP]
>
>**在Android**&#x200B;中 `ADBMobileConfig.json` ，檔案必須放置在 `assets` 檔案夾中。

以下是JSON檔案中的變數清單，以及每個變數所需的最低SDK版本：

* **acquisition**
   * 最低 SDK 版本: 4.1
   * 啟用行動應用程式贏取。
      * `server`這是贏取伺服器在首次啓動時被檢查的贏取伺服器。
      * `appid` – 即產生的 ID，可在贏取伺服器上唯一識別此應用程式。
   如果缺少此區段，請啟用行動應用程式贏取並重新下載 SDK 設定檔案。如需詳細資訊，請參閱 *此變數清單中的referrerTimeout* 。

* **analyticsForwardingEnabled**
   * 最低SDK版本為4.8.0。
   * 預設值為 `false`。

      `audienceManager` 物件中的屬性。如果已設定 Audience Manager 且 `analyticsForwardingEnabled` 已設為 `true`，所有的 Analytics 流量也會轉送至 Audience Manager。

* **backdateSessionInfo**
   * 最低 SDK 版本: 4.6.
   * 啟用/停用 Adobe SDK 日期回溯工作階段資訊點擊的能力。

      工作階段資訊點擊目前包括當機和工作階段長度，可予以啟用或停用。

      **啟用或停用點擊**

      * 若將值設為 `false`，表示&#x200B;**停用**&#x200B;點擊。SDK 會回復到 4.1 版之前的行為，將先前工作階段的工作階段資訊與後續工作階段的首次點擊混為一談。Adobe SDK 也會將工作階段資訊附加至目前的生命週期，以免導致誇大不實的造訪計數。由於造訪數據不再有誇大失真的問題，因此可發現造訪計數立即下降。

      * 若您未提供值，系統的預設值會是 `true`，亦即&#x200B;**啟用**&#x200B;點擊。啟用這些點撃後，Adobe SDK 會日期回溯工作階段點擊至前一個工作階段之最後點擊的 1 秒後。這表示當機和工作階段資料會關聯至事件發生的正確日期。副作用是 SDK 可能會為該日期回溯點撃建立一次造訪。應用程式每次重新啟動，日期都會回溯一個點擊。

         >[!IMPORTANT]
         >
         >回溯日期作業點擊資訊會在作業資訊伺服器呼叫中傳送，並可能套用其他伺服器呼叫。

* **batchLimit**
   * 最低 SDK 版本: 4.1
   * 連續呼叫中可傳送的點撃數臨界值。

      例如，如果 `batchLimit` 設為 10，則在第 10 個點擊前的每個點擊都會先儲存在佇列中。第 10 個點擊傳入後，便會連續傳送全部 10 個點擊。

      請記住以下資訊:

      * 預設值為 `0`，即表示未啟用批次處理程序。
      * 需要 `offlineEnabled = true`。

* **charset**
   * 最低 SDK 版本: 4.0
   * 定義您用於傳送至 Analytics 之資料的字元集。

      字元集可用來將傳入的資料轉換成 UTF-8 以供儲存和報告。

* **clientCode**
   * 最低 SDK 版本: 4.0
   * 您獲派的用戶端代碼。

      >[!IMPORTANT]
      >
      >Target需要此變數。

* **coopUnsafe**
   * 最低 SDK 版本: 4.16.1
   * `marketingCloud` 物件的布林屬性，在設定為 `true`時，會使裝置選擇退出Experience Cloud的Device Co-Op。
   * 預設值為 `false`.
   * **唯有**&#x200B;以 Device Co-op 佈建的客戶，才會使用此設定。
   若 Device Co-op 成員要求將此值設為 `true`，您需要與 Co-op 團隊合作，為您的 Device Co-op 帳戶向其申請黑名單標記。沒有啟用可這些標幟的自助式路徑。

   請記住以下資訊:

   * When `coopUnsafe` is set to `true`, `coop_unsafe=1` will always be appended to Audience Manager and Visitor ID hits.
   * If you enable Analytics server-side forwarding to Audience Manager, you will also see `coop_unsafe=1` Analytics hits.


* **environmentId**
   * 最低 SDK 版本: 4.14
   * 您想使用之環境的 ID。

      您可以指定有效的 ID (`environmentId=8`)，要是沒有 `environmentId`，系統會使用預設的生產環境。

* **lifecycleTimeout**
   * 最低 SDK 版本: 4.0
   * 預設值為 300 秒。

      指定在兩次應用程式啟動之間須經過的時間長度 (以秒為單位)，但在啟動前視同新的工作階段。這個逾時值也套用至將應用程式傳送至背景並重新啟動時。

      應用程式在背景花的時間，不算在作業階段長度中。

* **messages**

   * 最低 SDK 版本: 4.2
   * 由 Adobe Mobile Services 自動產生，可定義應用程式內傳訊的設定。如需詳細資訊，請參閱下方的&#x200B;*訊息說明*&#x200B;一節。

* **offlineEnabled**

   * 最低 SDK 版本: 4.0
   * 啟用後，點擊會在裝置離線時排入佇列，並在稍後裝置上線時傳送。

      您的報表套裝必須啟用時間戳記才能使用離線追蹤功能。

      預設值為 `false`。

      >[!IMPORTANT]
      >
      >如果報表套裝已啟用時間戳記，您的 `offlineEnabled` 組態屬性&#x200B;**必須**&#x200B;為 true。如果報表套裝未啟用時間戳記，您的 `offlineEnabled` 設定屬性&#x200B;**必須**&#x200B;為 false。
      >
      >如果此項目未正確設定，將會遺失資料。如果您不確定報表套裝是否啟用時間戳記，請連絡客戶服務或從 Adobe Mobile Services 下載設定檔案。

      如果您目前回報 AppMeasurement 資料的報表套裝也可從 JavaScript 收集資料，則必須為行動資料設定個別的報表套裝，或在使用 `s.timestamp` 變數的所有 JavaScript 點擊上加上自訂時間戳記。

* **org**

   * 最低 SDK 版本: 4.3
   * 指定 ID 服務的 Experience Cloud 組織 ID。

* **poi**
   * 最低 SDK 版本: 4.0
   * 每個地標 (POI) 陣列內含 POI 名稱、該地標區域的經緯度以及半徑 (以公尺為單位)。

      POI 名稱可以是任何字串。送出 `trackLocation` 呼叫後，如果目前座標位在定義的 POI 中，則會填入內容資料變數並與 `trackLocation` 呼叫一併傳送。

      ```javascript
      "poi": [
                 ["san francisco",37.757144,-122.44812,7000]
                 ["santa cruz",36.972935,-122.01725,600]
             ]
      ```

      自 4.2 版開始，POI 皆會在 Adobe Mobile 介面中定義，並會動態同步至應用程式設定檔案。此同步需要使用 `analytics.poi` 設定:

      ```javascript
      “analytics.poi“: `https://assets.adobedtm.com/`
      …/yourfile.json”`,
      ```

      若尚未設定此設定，則必須更新 `ADBMobile.json` 檔案以包含此行。若要下載更新的設定檔案，請參閱 [「開始之前](/help/android/getting-started/requirements.md)」。

* **postback**
   * 最低 SDK 版本: 4.6
   * 以下是「回撥」訊息範本的定義:

      ```javascript
      "payload":{
        "templateurl":"", //required will be token-expanded prior to being sent
        "templatebody":"", //optional - if this length > 0 POST will be used as transport method. This is a base64 encoded blob, which will be decoded and token-expanded prior to being sent.
        "contenttype": "", // optional - if this is length > 0 and POST type is selected this will be set as the Content-Type header.  if this is not supplied for a POST request, the default will be "application/x-www-form-urlencoded"
        "timeout": 0 // optional - number of seconds to wait before timing out.  Default is 2.}
      ```

      The `payload` object in the code is a sample payload for a message definition that goes in the `ADBMobileConfig.json` file. For more information, see [Postbacks](/help/android/analytics-main/postbacks/postbacks.md).

* **privacyDefault**
   * 最低 SDK 版本: 4.0
   * 預設值為 `optedin`。
      * 若為 `optedin`，點擊會立即傳送。
      * 若為 `optedout`，點擊會被捨棄。
      * 若為 `optunknown`，如果您的報表套裝已啟用時間戳記，會儲存點擊直到隱私權狀態變更為選擇加入 (屆時會傳送點擊) 或選擇退出 (屆時會捨棄點擊) 為止。
      If your report suite is not timestamp-enabled, hits are discarded until the privacy status changes to `optedin`.  這僅會設定初始值。如果已在程式碼中設定或變更此值，即會使用新的值直到再次變更，或應用程式解除安裝並重新安裝為止。


* **referrerTimeout**
   * 最低 SDK 版本: 4.1
   * 在逾時前，於初次啟動時，SDK 等待贏取反向連結資料的秒數。如果您正在使用贏取，我們建議您設定 5 秒逾時。

      >[!IMPORTANT]
      >
      >「贏取」需要此變數。如果變數設為 `0` 或不包含變數，SDK 不會等待贏取資料，且不會追蹤贏取量度。

* **remotes**
   * 最低 SDK 版本: 4.2
   * 自動設定並為動態設定檔案定義 Adobe 已裝載端點。

      每個設定檔案的最後一次更新時間將對每次啟動時的當前版本進行檢查，且會下載並儲存更新。
      * `analytics.poi` 是裝載 POI 設定的端點。
      * `messages` 是裝載應用程式內訊息設定的端點。

* **rsids**
   * 最低 SDK 版本: 4.0
   * 用來接收 Analytics 資料的一或多個報表套裝。多個報表套裝的 ID 應以逗號分隔，中間沒有空格。

      ```javascript
        "rsids" "rsid"
      ```

      ```javascript
        "rsids" "rsid1,rsid2"
      ```

      >[!IMPORTANT]
      >
      >Analytics需要此變數。

* **server**
   * 最低 SDK 版本: 4.0
   * Analytics 或 Audience Management 伺服器，依父節點而定。This variable should be populated with the server domain, without an `https://` or `https://` protocol prefix. 此前置詞會由資料庫自動處理且是以 `ssl` 變數為基礎。如果 `ssl` 為 `true`，會對此伺服器進行安全連線。如果 `ssl` 為 `false`，會對此伺服器進行非安全連線。

* **ssl**
   * 最低 SDK 版本: 4.0
   * 預設值為 `false`。

      啟用 (`true`) 或停用 (`false`) 透過 SSL (HTTPS) 傳送測量資料的能力。

      以下顯示「回撥」訊息範本的定義:

      ```javascript
      "payload": {
          "templateurl":"",//required-will be token-expanded prior to being sent 
          "templatebody": "", //optional - if this length >  0 POST will be used& as transport method. This is a base64 encoded blob, which will be  decoded and token-expanded prior to being sent.
          "contenttype": "" // optional - if this is length > 0 POST type is selected this will be set as the Content-Type header. if this is not supplied for a POST request, the default will be "application/x-www-form-urlencoded"
          "timeout": 0 // optional - number of seconds to wait before timing& out. Default is 2.}
      ```

* **timeout**
   * 最低 SDK 版本: 4.0
   * 決定 Target 等待回應的時間長度。


## Sample `ADBMobileConfig.json` file {#section_4655EF79744649E5A5AE19E3224C472C}

以下是範例 `ADBMobileConfig.json` 檔案:

```js
 { 
    "version": "2014-08-05T19:18:28.169Z", 
    "marketingCloud" : { 
        "org": "016D5C175213CCA80A490D05@AdobeOrg", 
        "coopUnsafe": false 
    }, 
    "target": { 
        "clientCode": "", 
        "timeout": 5, 
        "environmentId": 8 
    }, 
    "audienceManager": { 
        "server": "", 
        "analyticsForwardingEnabled": false 
    }, 
    "acquisition": { 
        "server": "c00.adobe.com", 
        "appid": "10a77a60192fbb628376e1b1daeeb65debf934e2c807e067ceb2963a41b165ee" 
    }, 
    "analytics": { 
        "rsids": "coolApp", 
        "server": "my.CoolApp.com", 
        "ssl": true, 
        "offlineEnabled": true, 
        "charset": "UTF-8", 
        "lifecycleTimeout": 300, 
        "privacyDefault": "optedin", 
        "batchLimit": 0, 
        "referrerTimeout": 5, 
        "poi": [ 
            ["san francisco",37.757144,-122.44812,7000],  
            ["santa cruz",36.972935,-122.01725,600] 
        ] 
    }, 
    "messages": [ 
        { 
            "messageId": "cb426565-a563-497a-a889-9dbeb451f8ae", 
            "template": "fullscreen", 
            "payload": { 
                 "html": "<!DOCTYPE html><html><head><meta charset=\"utf-8\" /><title></title><style></style></head><body><iframe src=\"https://www.adobe.com/\" frameborder=\"0\"></iframe></body></html>" 
            }, 
            "showOffline": false, 
            "showRule": "always", 
            "endDate": 2524730400, 
            "startDate": 0, 
            "audiences": [], 
            "triggers": [ 
                { 
                    "key": "pev2", 
                    "matches": "eq", 
                    "values": [ 
                        "AMACTION:custom" 
                    ] 
                } 
            ] 
        } 
    ], 
    "remotes": { 
        "analytics.poi": "https://assets.adobedtm.com/staging/42a6fc9b77cd9f29082cf19b787bae75b7d1f9ca/scripts/satellite-53e0faadc2f9ed92bc00003b.json", 
        "messages": "https://assets.adobedtm.com/staging/42a6fc9b77cd9f29082cf19b787bae75b7d1f9ca/scripts/satellite-53e0f9e2c2f9ed92bc000032.json" 
    } 
}
```

## 訊息說明 {#section_B97D654BA92149CE91F525268D7AD71F}

訊息節點是由 Adobe Mobile Services 自動產生，通常無須手動變更。以下說明可供疑難排解之用:

* "messageId"
* 產生的 ID，必要
* "template"
   * "alert"、"fullscreen" 或 "local"
   * 要求

* "showOffline"
   * true 或 false
   * 預設為 false

* "showRule"
   * "always"、"once" 或 "untilClick"
   * 要求

* "endDate"
   * 自 1970 年 1 月 1 日起的秒數
   * 預設為 2524730400

* "startDate"
   * 自 1970 年 1 月 1 日起的秒數
   * 預設為 0

* "payload"
   * "html"
      * 僅限全螢幕範本，必要
      * html 定義訊息
   * "image"
      * 僅限全螢幕，選用
      * 用於全螢幕影像的 url 至影像
   * "altImage"
      * 僅限全螢幕，選用
      * 要使用的套件影像名稱 (如果
         * 影像
         * 中指定的 URL 無法連線)
   * "title"
      * 全螢幕及提示，必要
      * 全螢幕或提示訊息的標題文字
   * "content"
      * 提示及本機通知，必要
      * 提示訊息的子文字，或本機通知訊息的通知文字
   * "confirm"
      * 提示，選用
      * 用於確認按鈕的文字
   * "cancel"
      * 提示，必要
      * 用於取消按鈕的文字
   * "url"
      * 提示，選用
      * 按下確認按鈕後要載入的 url 動作
   * "wait"
      * 本機通知，必要
      * 符合條件後，發佈本機通知的等待時間 (以秒為單位)



* "audiences"
   * 定義訊息顯示方式的物件陣列
   * "key"
      * 在點撃中尋找的變數名稱，必要
* "matches"
   * 進行比較時使用的符合項目類型
   * eq = 相等
   * ne = 不相等
   * co = 包含
   * ne = 不包含
   * sw = 以此開頭
   * ew = 以此結尾
   * ex = 存在
   * ne = 不存在
   * lt = 小於
   * le = 小於或等於
   * gt = 大於
   * ge = 大於或等於
* "values"
   * 一連串的值，用來比對
      * key
      * 與符合項目中的
      * matches
* "triggers"
   * 與對象相同，但這是動作而不是對象
   * "key"
   * "matches"
   * "values"