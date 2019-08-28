---
description: 以下為 Android 資料庫所提供的 Adobe Analytics 方法清單。
keywords: Android；資料庫；行動；sdk
seo-description: 以下為 Android 資料庫所提供的 Adobe Analytics 方法清單。
seo-title: Analytics 方法
solution: Marketing Cloud、Analytics
title: Analytics 方法
topic: 開發人員和實施
uuid: ac7c640e-9dcc-4724-b561-019cc025 d5 a7
translation-type: tm+mt
source-git-commit: 46a0b8e0087c65880f46545a78f74d5985e36cdc

---


# Analytics methods {#analytics-methods}

以下為 Android 資料庫所提供的 Adobe Analytics 方法清單。

SDK目前支援多個Adobe Experience Cloud解決方案]，包括Analytics]、Target]、Audience Manager]和Adobe Experience Platform Identity Service。各方法會根據解決方案加上前置詞，例如 Experience Cloud ID 方法會加上前置詞 `analytics`。

下列各方法將用來傳送資料至您的 Adobe Analytics 報表套裝:

* **trackState**

   使用可選內容資料來追蹤應用程式。States are the views that are available in your app, such as `home dashboard`, `app settings`, `cart`, and so on. 這些狀態類似於網站上的頁面，且 `trackState` 呼叫會遞增頁面檢視。

   If `state` is empty, `app name app version (build)` is displayed in reports. 如果在報表中看到這個值，請務必在每個 `state` 呼叫中設定 `trackState`。

   >[!TIP]
   >
   >這是唯一遞增頁面檢視的追蹤呼叫。

   * 以下是此方法的語法:

      ```java
      public staticvoidtrackState(Stringstate, Map<String,Object> contextData);
      ```

   * 以下是此方法的範例程式碼:

      ```java
      Analytics.trackState("loginScreen",null);
      ```

* **trackAction**&#x200B;追蹤應用程式中的動作。

   Actions that you want to measure, such as `logons`, `banner taps`, `feed subscriptions`, and other metrics, that occur in your app.

   * 以下是此方法的語法:

      ```java
      publicstaticvoidtrackAction(Stringstate,Map<String,Object> contextData);
      ```

   * 以下是此方法的範例程式碼:

      ```java
      Analytics.trackAction("heroBannerTouched",null);
      ```

* **getTrackingIdentifier**&#x200B;傳回自動產生的訪客識別碼給Analytics。

   這是應用程式專屬的唯一訪客 ID，會在初次啟動時產生，並會儲存以供後續使用。ID 會在應用程式升級時保留，並於應用程式解除安裝時移除。

   * 以下是此方法的語法:

      ```java
      public static String getTrackingIdentifier(); 
      ```

   * 以下是此方法的範例程式碼:

      ```java
      String trackingId = Analytics.getTrackingIdentifier(); 
      ```

* **trackLocation**

   在定義的興趣點中傳送目前經緯度和位置。如需詳細資訊，請參閱 [地理位置和興趣點](/help/android/location/geo-poi.md)。

   * 以下是此方法的語法:

      ```java
      public static void trackLocation(Location location, Map<String,Object> contextData); 
      ```

   * 以下是此方法的範例程式碼:

      ```java
      Analytics.trackLocation(userLocation, null);
      ```

* **trackLifetime&#x200B;ValueIncrease**

   Adds `amount` to the user's lifetime value.

   * 以下是此方法的語法:

      ```java
      publicstaticvoidtrackLifetimeValueIncrease(BigDecimalamount,Map<String,Object>contextData);
      ```

   * 以下是此方法的範例程式碼:

      ```java
      Analytics.trackLifetimeValueIncrease(new BigDecimal(30), null);
      ```

* **trackTimed&#x200B;ActionStart**

   以名稱 `action` 啟動計時動作。

   如果您對已啟動的動作呼叫此方法，則會覆寫先前的計時動作。

   >[!TIP]
   >
   >此呼叫不會傳送點擊。

   * 以下是此方法的語法:
   ```java
   publicstaticvoidtrackTimedActionStart(Stringaction,Map<String,Object>contextData);
   ```

   * 以下是此方法的範例程式碼:

      ```java
      Analytics.trackTimedActionStart("cartToCheckout",null)
      ```


* **trackTimed&#x200B;ActionUpdate**

   傳遞 `contextData` 以更新與 `action` 關聯的內容資料。傳遞的 `data` 會附加至該動作的現有資料，如果已為 `action` 定義了相同鍵值，則會覆寫資料。

   >[!TIP]
   >
   >此呼叫不會傳送點擊。

   * 以下是此方法的語法:

      ```java
      public static void trackTimedActionUpdate(Stringaction,Map <String,Object> contextData); 
      ```

   * 以下是此方法的程式碼範例：

      ```java
      HashMap cdata = new HashMap<String Object> (); 
      cdata.put("quantity",3); 
      Analytics.trackTimedActionUpdate("cartToCheckout", cdata);
      ```

* **trackTimed&#x200B;ActionEnd**

   結束計時動作。If you provide `block`, you can access the final time values and can manipulate `data` before sending the final hit.

   >[!TIP]
   >
   >If you provide `block`, you must return `true` to send a hit. Passing `null` for `block` sends the final hit.

   * 以下是此方法的語法:

      ```java
      public static void trackTimedActionEnd(Stringaction,TimedActionBlock<Boolean> logic); 
      ```

   * 以下是此方法的範例程式碼:

      ```java
      Analytics.trackTimedActionEnd("cartToCheckout",new
      Analytics.TimedActionBlock<Boolean>(){
        @Override
        public Booleancall(long inAppDuration,long totalDuration, Map<String,
      Object> contextData) {
              contextData.put("price", 49.95);
              return true;
         }
      });
      ```

* **sendQueuedHits**

   **須使用 SDK 4.1 版.**

   無論排入佇列的點擊數量多寡，此方法會強制資料庫傳送離線佇列中的所有點擊。

   * 以下是此方法的語法:

      ```java
      voidsendQueuedHits()
      ```

   * 以下是此方法的範例程式碼:

      ```java
      Analytics.sendQueuedHits();
      ```

* **getQueueSize**

   傳回在離線佇列中儲存的追蹤呼叫數目。

   * 以下是此方法的語法:

      ```java
      long getQueueSize()
      ```

   * 以下是此方法的範例程式碼:

      ```java
      long queueSize = Analytics.getQueueSize(); 
      ```

* **clearQueue**

   清除離線佇列中的所有點擊。

   * 以下是此方法的語法:

      ```java
      voidclearQueue()
      ```

   * 以下是此方法的範例程式碼:

      ```java
      Analytics.clearQueue();
      ```

      >[!WARNING]
      >
      > 手動清除佇列時請小心。此程序無法回復。