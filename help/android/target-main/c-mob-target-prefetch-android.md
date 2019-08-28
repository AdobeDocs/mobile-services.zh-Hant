---
description: Adobe Target 預先擷取功能使用 Android Mobile SDK，透過快取伺服器回應，盡量以最少次數擷取提供項目內容。
seo-description: Adobe Target 預先擷取功能使用 Android Mobile SDK，透過快取伺服器回應，盡量以最少次數擷取提供項目內容。
seo-title: Android 中的預先擷取選件內容
title: Android 中的預先擷取選件內容
uuid: 063451b8-e191-4d58-8d8-1723e310 ad1 a
translation-type: tm+mt
source-git-commit: fa7375ac8a1345d81748bcf635791c46d3943fed

---


# 預先擷取 Android 中的選件內容 {#prefetch-offer-content-in-android}

Adobe Target 預先擷取功能使用 Android Mobile SDK，透過快取伺服器回應，盡量以最少次數擷取提供項目內容。

>[!IMPORTANT]
>
>Adobe Target中的「自動目標」、「自動分配」和「自動個人化」活動類型不支援Android的Mobile SDK預先擷取功能。

此程序會減少載入時間，避免多個網路呼叫，並允許通知 Adobe Target 行動應用程式使用者造訪哪一個 mbox。預先擷取呼叫期間，會擷取並快取所有內容，而且將從快取中擷取此內容，以供包含指定 mbox 名稱之快取內容的所有未來呼叫使用。

預先擷取內容不會在跨啟動之間持續有效。The prefetch content is cached as long as the application lives or until the `clearPrefetchCache()` method is called.

>[!IMPORTANT]
>
>Target prefetch APIs have been available since SDK version 4.14.0. For more information about parameter limitations, see [Batch-input-parameters](https://developers.adobetarget.com/api/#batch-input-parameters).

在 SDK 4.14 或更新版本中，若要指定 ，啟動 v2 批次 mbox TnT 呼叫時，系統會從 檔案中挑選 `environmentId``ADBMobileConfig.json`environmentId。若未指定此檔案中的 `environmentId`，系統就不會以 TNT 批次 mbox 呼叫傳送任何環境參數，而是為預設環境傳送選件。

例如:

```java
if (MobileConfig.getInstance().mobileUsingTarget()){ 
            long environmentID = MobileConfig.getInstance().getEnvironmentID(); 
            if(environmentID != 0L){ 
                parametersJson.put(TargetJson.ENVIRONMENT_ID, environmentID); 
            } 
        }
```

## Pre-fetch methods {#section_05967F1F3A554B0FBC2C08A954554BDE}

以下是您可以在 Android 中用於預先擷取的方法:

* **prefetchContent**

   將含有一連串位置的預先擷取要求傳送至設定的 Target 伺服器，並在提供的回撥中傳回要求狀態。

   * 以下是此方法的語法:

      ```java
      public static void prefetchContent(
      final List<TargetPrefetchObject> targetPrefetchArray,
      final Map<String, Object> profileParameters,
      final TargetCallback<Boolean> callback)
      ```

   * 以下是此方法的參數：

      * **targetPrefetchArray**

         `TargetPrefetchObjects` 陣列，包含每個要預先擷取之 Target 位置的名稱與 mboxParameters。

      * **profileParameters**

         包含要與此要求中每個位置預先擷取搭配使用之設定檔參數的鍵值和值。

      * **callBack**

         完成預先擷取時叫用。Returns `true` if the prefetch was successful and `false` if the prefetch was unsuccesful.

* **loadRequests**

   針對在要求陣列中指定的多個 mbox 位置執行批次要求。 陣列中的每個物件包含回撥函式，當內容可用於其指定的 mbox 位置時，將會叫用該函式。

   >[!IMPORTANT]
   >
   >如果已請求位置的內容已快取，則會立即在提供的回呼中傳回。否則，SDK 將會傳送網路要求給 Target 伺服器以擷取內容。

   * 以下是此方法的語法:

      ```java
      public static void loadRequests( final List<TargetRequestObject> requestArray,  final Map<String, Object> profileParameters)
      ```

   * 以下是此方法的參數：

      * **requestArray**

         `TargetRequestObjects` 陣列，包含要擷取之每個位置的名稱、預設內容、參數，以及回撥函式。

      * **profileParameters**

         包含要與此要求中每個位置預先擷取搭配使用之設定檔參數的鍵值和值。

* **clearPrefetchCache**

   清除 Target 預先擷取快取的資料。

   * 以下是此方法的語法:

      ```java
      public static void clearPrefetchCache();
      ```

   * 此方法沒有參數。

* **createTargetRequestObject**

   使用提供的資料建立並傳回 `TargetRequestObject` 例項。

   * 以下是此方法的語法:

      ```java
      public static TargetPrefetchObject createTargetRequestObject( 
      final String mboxName,
      final String defaultContent, 
      final Map<String, Object> mboxParams, 
      final Map<String, Object> orderParams, 
      final Map<String, Object> productParams, 
      final Target.TargetCallback<String> callback)
      ```

* **createTargetPrefetchObject**

   使用提供的資料建立並傳回 TargetPrefetchObject 例項。

   * 以下是此方法的語法:

      ```java
      public static TargetPrefetchObject createTargetPrefetchObject( 
      final String mboxName, 
      final Map<String, Object> mboxParams) 
      final Map<String, Object> orderParams, 
      final Map<String, Object> productParams)
      ```

## Public classes {#section_A273E53F069E4327BBC8CE4910B37888}

以下是 Android 中支援預先擷取的公用類別:

### 類別參考：targetPrefetchObject

封裝用於 mbox 預先擷取的 mbox 名稱和參數。

* **`name`**

   將預先擷取的位置名稱。
   * **類型:** 字串

* `mboxParameters`

   將針對此 `mboxParameters` 要求附加作為 `TargetPrefetchObject` 的鍵值值組集合。
   * **類型**：地圖`<String, Object>`

* **`orderParameters`**

   將附加至 order 節點下目前 mbox 的鍵值值組集合。
   * **類型**：地圖 `<String, Object>`

* **`productParameters`**

   將附加至 product 節點下目前 mbox 的鍵值值組集合。

   * **類型**：地圖 `<String, Object>`


### 類別參考：TargetRequestObject

此類別封裝 mbox 名稱、預設內容、mbox 參數，以及用於 Target 位置要求的傳回回撥。

* **`mboxName`**

   要求位置的名稱。

   * **類型:** 字串

* **`mboxParameters`**

   將針對此 `mboxParameters` 附加作為 `TargetRequestObject` 的鍵值值組集合。

   * **類型：地圖`<String, Object>`**

* **`orderParameters`**

   將附加至 order 節點下目前 mbox 的鍵值值組集合。

   * **類型**：地圖 `<String, Object>`

* **`productParameters`**

   將附加至 product 節點下目前 mbox 的鍵值值組集合。

   * **類型**：地圖 `<String, Object>`

* **`defaultContent`**

   如果 SDK 無法從 Target 伺服器擷取內容，在回撥中傳回的字串值。

   * **類型:** 字串

* **`callback`**

   當指定的 `TargetRequestObject` 內容為可用狀態時，將呼叫函式指標。

   * **類型**：Target. targetCallback`<String>`


## Code sample {#section_BF7F49763D254371B4656E17953D520C}

以下是如何藉由使用 Android SDK 預先擷取內容的範例:

```java
// When your app launches, prefetch the content for a list of locations. 
// Define the list of mboxes that you want to prefetch. 
List<TargetPrefetchObject> prefetchMboxesList = new ArrayList<>(); 
  
Map<String, Object> mboxParameters1 = new HashMap<>(); 
mboxParameters1.put("status", "platinum"); 
prefetchMboxesList.add(Target.createTargetPrefetchObject("mboxName1", mboxParameters1));

Map<String, Object> mboxParameters2 = new HashMap<>(); 
mboxParameters2.put("userType", "paid"); 
 
List<String> purchasedIds = new ArrayList<String>(); 
purchasedIds.add("34"); 
purchasedIds.add("125");  
Map<String, Object> orderParameters2 = new HashMap<>(); 
orderParameters2.put("id", "ADCKKIM"); 
orderParameters2.put("total", "344.30"); 
orderParameters2.put("purchasedProductIds",  purchasedIds); 
  
Map<String, Object> productParameters2 = new HashMap<>(); 
productParameters2.put("id", "24D3412"); 
productParameters2.put("categoryId","Books"); 
  
prefetchMboxesList.add(Target.createTargetPrefetchObject("mboxName2", mboxParameters2, orderParameters2, productParameters2));

// Define the profile parameters map. 
Map<String, Object> profileParameters = new HashMap<>(); 
profileParameters.put("ageGroup", "20-32");

// Define the target callback for the prefetch call status. 
Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() { 
    @Override 
    public void call(final Boolean status) { 
        // check the returned status for the prefetch call 
    }};

// Call the prefetchContent API. 
Target.prefetchContent(prefetchMboxesList, profileParameters, prefetchStatusCallback);

// When the content is required, you can initiate the locations request. 
// Define the list of target request objects. 
List<TargetRequestObject> locationRequests = new ArrayList<>(); 
  
Target.TargetCallback<String> callback1 = new Target.TargetCallback<String>() { 
    @Override 
    public void call(final String content) { 
        // check the returned content for mboxName1. 
    }}; 
  
locationRequests.add(Target.createTargetRequestObject("mboxName1", "defaultContent1", mboxParameters1, callback1));

Target.TargetCallback<String> callback2 = new Target.TargetCallback<String>() { 
    @Override 
    public void call(final String content) { 
        // check the returned content for mboxName2. 
    }}; 
  
locationRequests.add(Target.createTargetRequestObject("mboxName2", "defaultContent2", mboxParameters2, orderParameters2, productParameters2, callback2)); 
  
// Call the loadRequests API. 
Target.loadRequests(locationRequests, profileParameters); 
```

## 其他資訊 {#section_A454BAD1CD49423E86C71BAEE06125FD}

以下是關於這些範例的部分其他資訊:

* `ProductParameters` 僅允許下列鍵值:

   * `id`
   * `categoryId`

* `OrderParameters` 僅允許下列鍵值:

   * `id`
   * `total`
   * `purchasedProductIds`

* `purchasedProducts` 接受字串的 ArrayList。