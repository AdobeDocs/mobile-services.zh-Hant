---
description: 可以在 Adobe Mobile Services 中產生具備獨特追蹤代碼的贏取連結。當使用者按一下產生的連結後，使用者從App Store下載並執行應用程式時，SDK會自動收集並傳送贏取資料至Adobe Mobile Services。
keywords: Android；資料庫；行動；sdk
seo-description: 可以在 Adobe Mobile Services 中產生具備獨特追蹤代碼的贏取連結。當使用者按一下產生的連結後，使用者從App Store下載並執行應用程式時，SDK會自動收集並傳送贏取資料至Adobe Mobile Services。
seo-title: 行動應用程式贏取
solution: Marketing Cloud、Analytics
title: 行動應用程式贏取
topic: 開發人員和實施
uuid: 4d32ee9-e856-4e 40-a29-2b5 bcc106 e0
translation-type: tm+mt
source-git-commit: 54150c39325070f37f8e1612204a745d81551ea7

---


# Mobile app acquisition {#mobile-app-acquisition}

可以在 Adobe Mobile Services 中產生具備獨特追蹤代碼的贏取連結。當使用者按一下產生的連結後，使用者從App Store下載並執行應用程式時，SDK會自動收集並傳送贏取資料至Adobe Mobile Services。

## 新版 Adobe Experience Cloud SDK

正在尋找 Adobe Experience Platform Mobile SDK 的相關資訊和文件嗎? 按一下[這裡](https://aep-sdks.gitbook.io/docs/)以取得最新文件。

我們在 2018 年 9 月時發行了全新的 SDK 主要版本。這些新的 Adobe Experience Platform Mobile SDK 可透過 [Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) 設定。

* 若要開始使用，請前往 [Launch](https://launch.adobe.com/)。
* 若要查看 Experience Platform SDK 的儲存庫內容，請前往[ Github: Adobe Experience Platform SDK](https://github.com/Adobe-Marketing-Cloud/acp-sdks)。

>[!IMPORTANT]
>
> If you are using the Adobe Experience Platform Mobile SDKs with Adobe Launch, you **must** also install the Adobe Analytics Mobile Services extension to use Adobe Mobile Services features such as Acquisition links. 如需詳細資訊，請參閱 [Adobe Analytics - Mobile Services](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services)。For more information about using Acquisition and Marketing Links with the Experience Cloud SDKs, see [Acquisition and Marketing Links](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services#acquisition-and-marketing-links).

>[!IMPORTANT]
>
>若要使用 Acquisition，您&#x200B;**必須**&#x200B;有 SDK 4.1 版或更新版本。

贏取連結必須在 Adobe Mobile Services 中建立。For more information, see [Acquisition](/help/using/acquisition-main/acquisition-main.md).

**在 SDK 4.13.1 版及更新版本中**:

如果您無法使用在 Adobe Mobile Services 中建立的贏取連結，仍可透過 Google Play Acquisition 由 SDK 收集和傳送贏取資料。

收集來自標準 Google Play Acquisition 促銷活動的贏取資料:

* 使用標準 Google Play 商店贏取方法。

   自訂贏取資料可與標準 Google Play Acquisition 鍵值值組搭配使用。

* 當使用者因 Google Play 商店贏取而下載和執行應用程式時，系統將會收集反向連結的資料，並傳送至 Adobe Mobile Services。

   * The data is stored and available in the `AdobeDataCallback` instance that was registered earlier with the SDK.

      如需詳細資訊，請參閱 [設定方法](/help/android/configuration/methods.md)。

   * 會使用 `MobileDataEvent.MOBILE_EVENT_ACQUISITION_INSTALL` 或 `MobileDataEvent.MOBILE_EVENT_ACQUISITION_LAUNCH` 使用事件類型。

   * 屬於 Google Play 贏取資料一部分的自訂鍵值將會使用`a.acquisition.custom.`「」建立命名空間。

如果您有使用在 Adobe Mobile Services 中建立的贏取連結，請完成下列作業以新增自訂資料至贏取連結:

1. 為贏取變數加上前置詞`adb`「。

   When the SDK receives the acquisition data from Adobe Mobile Services (on first launch), that data will be stored and also available in the `AdobeDataCallback` instance registered earlier with the SDK, as mentioned in [Configuration Methods](/help/android/configuration/methods.md).

1. `MobileDataEvent.MOBILE_EVENT_ACQUISITION_INSTALL` 將會使用或 `MobileDataEvent.MOBILE_EVENT_ACQUISITION_LAUNCH` 使用事件類型。

1. 自訂資料索引鍵會加上前置詞`a.acquisition.custom.`

>[!TIP]
>
>如果您要將資料傳送至多個報表套裝，請從報表套裝ID清單中的第一個報表套裝使用應用程式的贏取資料。

本節中的更新可讓 SDK 透過贏取連結傳送贏取資料。

## Tracking mobile acquisition {#section_CEA30C652AC8470784B8054E299B80FA}

1. 新增程式庫[至您的專案並實施生命週期。

   如需詳細資訊，請參閱 *核心實作與生命週期* 中 [的新增SDK和設定檔案至IntelliJ IDEA或Eclipse專案](/help/android/getting-started/dev-qs.md)。

1. 匯入資料庫:

   ```java
   import com.adobe.mobile.*;
   ```

1. 針對反向連結實施 `BroadcastReceiver`:

   ```java
   package com.your.package.name;  // replace with your app package name 
   
   import android.content.BroadcastReceiver; 
   import android.content.Context; 
   import android.content.Intent; 
   
   public class GPBroadcastReceiver extends BroadcastReceiver { 
     @Override 
     public void onReceive(Context c, Intent i) { 
      com.adobe.mobile.Analytics.processReferrer(c, i); 
     } 
   }
   ```

1. 更新 `AndroidManifest.xml` 以啟用於先前步驟建立的 `BroadcastReceiver`:

   ```xml
   <receiver android:name="com.your.package.name.GPBroadcastReceiver" android:exported="true"> 
    <intent-filter> 
     <action android:name="com.android.vending.INSTALL_REFERRER" /> 
    </intent-filter> 
   </receiver>
   ```

1. Verify that the `ADBMobileConfig.json` file contains the required acquisition settings:

   ```xml
   "acquisition": { 
      "server": "c00.adobe.com", 
      "appid": "0652024f-adcd-49f9-9bd7-2552a4565d2f" 
   }, 
   "analytics": { 
     "referrerTimeout": 5, 
     ...
   ```

   >[!IMPORTANT]
   >
   >如果您要將資料傳送至多個報表套裝，請從報表套裝ID清單中，使用與第一個報表套裝關聯的應用程式取得設定(贏取伺服器和appid)。

   `acquisition` 這些設定由Adobe Mobile服務產生，不應變更。For more information about how to download a customized `ADBMobileConfig.json` file with the `acquisition` settings pre-configured, see [Before You Start](/help/android/getting-started/requirements.md).

啟用這些設定後，贏取資料會在應用程式初次啟動後，自動透過初始生命週期呼叫傳送。

>[!CAUTION]
>
>`referrerTimeout` 必須設為高於0的值，才能啓用應用程式贏取。