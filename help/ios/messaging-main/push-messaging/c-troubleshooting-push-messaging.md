---
description: 此資訊可協助您進行推送訊息疑難排解。
keywords: 行動
seo-description: 此資訊可協助您進行推送訊息疑難排解。
seo-title: 疑難排解推送訊息
solution: Marketing Cloud、Analytics
title: 疑難排解推送訊息
topic: 量度
uuid: 87d7dcb6-82a8-46e3-a6 ed-7f895 a22 f2 af
translation-type: tm+mt
source-git-commit: 3cc97443fabcb9ae9e09b998801bbb57785960e0

---


# Troubleshooting push messaging {#troubleshooting-push-messaging}

此資訊可協助您進行推送訊息疑難排解。

## 為什麼有時候推送訊息的傳送會延遲?

下列延遲類型可能與 Mobile Services 的推送訊息有關:

* **等候 Analytics 點擊**

   每個報表套裝都可設定處理傳入 Analytics 點擊的時機。預設為 1 小時。實際處理 Analytics 點擊最多可能需要 30 分鐘，但通常為 15 至 20 分鐘。

   例如，某個報表套裝每小時處理一次點擊。如果您將最大處理時間計為 30 分鐘，則某個傳入的點擊可能需要 90 分鐘才可供推送訊息使用。如果使用者在早上 9:01 啟動應用程式，則點擊會在早上 10:15 到 10:30 之間，於 Mobile Services 使用者介面中顯示為新的唯一使用者。

* **等候推送服務**

   推送服務 (APNS 或 GCM) 可能不會立即送出訊息。雖然此情形不常見，但曾發生過 5 至 10 分鐘延遲的現象。在「訊息」頁面中，您可按一下訊息的「檢視」連結，以確認推送訊息已傳送至推送服務。在報表中，成功傳送至推送服務的數量會列在「已發佈」欄。

   >[!TIP]
   >
   >推送服務不保證傳送訊息。如需服務的可靠性詳細資訊，請參閱適當文件。
   >
   >* **APNS**: [服務品質](https://developer.apple.com/documentation/usernotifications)
      >
      >
   * **GCM**: [訊息的生命週期](https://developers.google.com/cloud-messaging/concept-options)


## 我該如何更新 Apple 推送服務憑證?

傳送推送訊息須使用有效的推送服務憑證。Mobile Services 會在憑證接近到期或到期時通知您。如果您收到此通知，請完成下列步驟以更新憑證:

1. Click **[!UICONTROL Manage App Settings]**.
2. To delete the current certificate, scroll to **[!UICONTROL Push Services]** and click **[!UICONTROL Delete]**.
3. 設定並測試新的憑證。

   如需詳細資訊，請參閱[啟用推送訊息的必備條件](/help/using/c-manage-app-settings/c-mob-confg-app/configure-push-messaging/prerequisites-push-messaging.md)

4. 按一下&#x200B;**[!UICONTROL 儲存]**。

## 我為何在 iOS 模擬器中看不到推送訊息?

iOS 模擬器不支援推送訊息。