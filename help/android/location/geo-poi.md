---
description: 地理位置可協助您透過經緯度和 Android 應用程式中預先定義的地標來測量位置資料。
seo-description: 地理位置可協助您透過經緯度和 Android 應用程式中預先定義的地標來測量位置資料。
seo-title: 地理位置和興趣點
solution: Marketing Cloud、Analytics
title: 地理位置和興趣點
topic: 開發人員和實施
uuid: b8209370-cbc4-40f9-97d8-017e2 d74 a377
translation-type: tm+mt
source-git-commit: 3cc97443fabcb9ae9e09b998801bbb57785960e0

---


# Geo-location and points of interest {#geo-location-and-points-of-interest}

地理位置可協助您透過經緯度和 Android 應用程式中預先定義的地標來測量位置資料。

各 `trackLocation` 呼叫均會傳送以下資訊:

* 在 Adobe Mobile Services 使用者介面中定義之地標 (POI) 的經緯度和位置。

   此資訊會傳遞至行動解決方案變數以進行自動報告。

* 以內容資料傳遞之與中心的距離和精確度。

   系統不會自動擷取上述變數。You must map these context data variables by using the instructions in the *Sending Additional Data* section below.

## 動態 POI 更新 {#section_3747B310DD5147E2AAE915E762997712}

自 4.2 版開始，POI 皆會在 Adobe Mobile 使用者介面中定義，並會動態同步至應用程式設定檔案。此同步需要ADBMobile `analytics.poi`[JSON設定](/help/android/configuration/json-config/json-config.md)中的設定：

```js
“analytics.poi”: “https://assets.adobedtm.com/…/yourfile.json”,
```

如果尚未設定此項目，您必須下載更新版本的 `ADBMobile.json` 檔案，並將其新增至您的應用程式。如需詳細資訊，請參閱 [「下載SDK和測試工具](/help/android/getting-started/requirements.md)」。

## Tracking geo-location and POIs {#section_B1616E400A7548F9A672F97FEC75AE27}

1. 新增資料庫至您的專案與實施生命週期。

   如需詳細資訊，請參閱 *核心實作與生命週期* 中 [的新增SDK和設定檔案至IntelliJ IDEA或Eclipse專案](/help/android/getting-started/dev-qs.md)。

1. 匯入資料庫:

   ```java
   import com.adobe.mobile.*;
   ```

1. 呼叫 `trackLocation` 以追蹤目前位置:

   ```java
   Location currentLocation = new Location("my location here"); 
   Analytics.trackLocation(currentLocation, null);
   ```

   >[!TIP]
   >
   >您可以隨時呼叫 `trackLocation` 。

   You can use location strategies to determine the location that is passed to the `trackLocation` call. 如需詳細資訊，請參閱 [Android位置策略](https://developer.android.com/guide/topics/location/strategies.html)。

此外，如果該位置經判斷位於定義的 POI 半徑範圍內，則 `a.loc.poi` 內容資料變數將會與 `trackLocation` 點擊一併傳入，並會在&#x200B;**「位置劃分」**&#x200B;報表中報告為 POI。`a.loc.dist` 內容變數也會以公尺為單位傳送來自定義座標的距離。

## Sending additional data {#section_3EBE813E54A24F6FB669B2478B5661F9}

除了位置資料之外，您還可以隨著每次追蹤位置呼叫傳送其他內容資料:

```java
HashMap<String, Object> locationContextData = new HashMap<String, Object>(); 
locationContextData.put("myapp.location.LocationSource", "GPS"); 
 
Location currentLocation = new Location("my location here"); 
Analytics.trackLocation(currentLocation, locationContextData);
```

內容資料值必須對應至 Adobe Mobile Services 使用者介面中的自訂變數:

![](assets/map-location-context-data.png)

## Location context data {#section_FFB71E6653F9410A89CC6ACC0C9164A9}

經緯度會透過三種不同內容資料參數傳送，且各參數代表不同程度的精準度，其中共有六個內容資料參數。

例如，座標 lat = 40.93231, long = -111.93152 代表位置精準度為 1 公尺。此位置會根據下列變數的精準度來分割。

`a.loc.lat.a`= 040.9

`a.loc.lat.b` = 32

`a.loc.lat.c` = 31

`a.loc.lon.a` = -111.9

`a.loc.lon.b` = 31

`a.loc.lon.c` = 52

視目前位置準確度而定，部分精準度可能會顯示為 `00`。例如，如果該位置目前準確程度至 100 公尺，則 `a.loc.lat.c` 和 `a.loc.lon.c` 將會填入 `00`。

請記住以下資訊:

* `trackLocation` 請求會以等同 `trackAction` 於呼叫的方式傳送。

* 系統不會在一般 `trackAction` 和 `trackState` 呼叫過程中傳遞 POI，因此您必須使用 `trackLocation` 呼叫來追蹤 POI。

* 必要時，您應經常呼叫 `trackLocation` 以追蹤位置和 POI。

   建議您視應用程式需求，在應用程式啟動時呼叫 `trackLocation`，並在隨後視需要再次進行。

* POI 只有在已於應用程式設定檔案中完成定義後，才會填入。

   POI 不會套用至先前已傳送的歷史 `trackLocation` 呼叫。
* `trackLocation` 呼叫支援傳送與 `trackAction` 呼叫類似的其他內容資料。

* 當兩個 POI 的直徑範圍重疊時，會使用包含目前位置的第一個 POI。

   當您的 POI 重疊時，您應依最高至最低精細度的順序列出 POI，以確保報告最精細的 POI。
