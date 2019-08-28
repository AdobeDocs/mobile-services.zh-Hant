---
description: 此資訊可協助您進行應用程式內傳訊疑難排解。
keywords: 行動
seo-description: 此資訊可協助您進行應用程式內傳訊疑難排解。
seo-title: 疑難排解應用程式內訊息
solution: Marketing Cloud、Analytics
title: 疑難排解應用程式內訊息
topic: 量度
uuid: 39c3a21d-92c2-4004-b00 f-99b6 f91 d3696
translation-type: tm+mt
source-git-commit: 12e01e112debffd877dd62f1fd2505724b2aae7d

---


# 疑難排解應用程式內傳訊{#troubleshooting-in-app-messaging}

此資訊可協助您進行應用程式內傳訊疑難排解。

如果您已完成應用程式內傳訊的所有要求，但訊息仍無法顯示，請檢查下列項目:

## 應用程式中是使用最新設定和最新 SDK 嗎?

Ensure that you have an [In-App Messaging](/help/android/messaging-main/messaging/messaging.md) section in your configuration (downloaded JSON file) or have a Messages remote endpoint, so that it can be retrieved from dynamic tag management.

## 我的 Android 全螢幕訊息無法顯示。我已使用正確的 SDK 和配置，也符合觸發器條件。

您有更新資訊清單檔案、定義全螢幕活動嗎?

## 我的 Android 本機通知訊息沒有作用。

請務必在資訊清單中宣告本機通知廣播接收器。For more information, see step 2 in *Enabling In-App Messaging* in [In-App Messaging](/help/android/messaging-main/messaging/messaging.md).

## 這是現時訊息嗎?

若要確認您的訊息是否為現時，請在「管理應用程式內訊息」頁面的&#x200B;**「狀態」**&#x200B;欄中，檢查訊息清單。

## 檢視 *顯示一次*， *一律顯示*， *顯示「對象」索引標籤上的離線* 設定。

確定這些設定是依照您想要的方式。在&#x200B;**[!UICONTROL 「對象」]**&#x200B;標籤中，檢閱您的&#x200B;**「觸發器」]選項，該選項可讓您指定顯示訊息的頻率。[!UICONTROL **

## 如果使用啓動事件做為觸發器…

啟動只會發生在新的工作階段。如需工作階段開始時間的詳細資訊，請參閱 `lifecycleTimeout`JSON 設定[中的 ](/help/android/configuration/json-config/json-config.md) 列。

## 我已從遠端更新訊息，但應用程式仍顯示舊訊息。

請記住以下資訊:

* 動態標籤管理需要數分鐘時間，才能以您的新定義更新端點。等候一段時間，然後再試一次。
* 新啟動時才會更新設定。如果應用程式在生命週期工作階段逾時期間重新啟動，則您的新設定可能尚未下載。

如需詳細資訊，請參閱[生命週期量度](/help/android/metrics.md)。

## 我的影像無法完全符合範本所提供的空間。

應用程式內訊息全螢幕範本支援顯示來自遠端伺服器 (影像 URL) 或應用程式套件 (套件影像) 的影像。該影像應為標準影像格式，例如 JPG、GIF 或 PNG。由於裝置螢幕有許多不同的尺寸，因此影像很有可能無法完全符合範本所提供的空間。該範本著重於顯示影像的中央，因此如果影像不符合空間，請裁切 (縱向) 或淡化 (橫向) 邊緣。

以下為各方向的正確放置與大小調整規則:

* **縱向**
   * 手機的高度為 195px.
   * 平板電腦的高度為 529px.
   * 如果影像寬度小於裝置寬度，則將影像置於中央。
   * 如果影像寬度大於裝置寬度，則裁切影像。

* **橫向**
   * 將影像高度縮放為裝置高度的 100%。
   * 寬度為裝置的 75%，右側須淡出。
   如果您無法順利使用全螢幕範本，可以下載並使用自訂 HTML 範本。此範本可提供更大的影像靈活性，並能讓您完全控制範本。
