---
description: 建立新應用程式或編輯現有應用程式時，您可以在「管理應用程式設定」頁面上配置「SDK 分析」選項。
keywords: 行動
seo-description: 建立新應用程式或編輯現有應用程式時，您可以在「管理應用程式設定」頁面上配置「SDK 分析」選項。
seo-title: 配置 SDK 分析選項
solution: Marketing Cloud、Analytics
title: 配置 SDK 分析選項
topic: 量度
uuid: fd3a21d2-6560-4e96-92Fe-b99 caac5 e834
translation-type: tm+mt
source-git-commit: d028fe0f9477bc011aa8fda21a0a389808df0fce

---


# Configure SDK Analytics options {#configure-sdk-analytics-options}

建立新應用程式或編輯現有應用程式時，您可以在「管理應用程式設定」頁面上配置「SDK 分析」選項。

Type information in the following fields under **[!UICONTROL SDK Analytics Options]**:

* **[!UICONTROL 使用 HTTPS]**

   啟用 HTTPS 以提高安全性。

* **[!UICONTROL 日期回溯工作階段點擊]**

   啓用或停用Adobe SDK回溯作業資訊點擊的能力。工作階段資訊點擊目前包含當機和工作階段長度。啟用時，Adobe SDK 會日期回溯工作階段點擊至前一個工作階段之最後點擊的 1 秒後。這表示當機和工作階段資料會關連至事件發生的正確日期。應用程式的每個新啟動都會日期回溯一個點擊。停用時，Adobe SDK 會將工作階段資訊附加至目前的生命週期。

* **[!UICONTROL 隱私]**

   選擇隱私權選項:

   * **[!UICONTROL 傳送資料，直到選擇退出為止]**
   * **[!UICONTROL 保留資料，直到選擇加入為止]**

* **[!UICONTROL 工作階段逾時 (秒)]**

   指定工作階段逾時值。

   預設值為 300 秒。指定在兩次應用程式啟動之間需經過的時間長度 (單位為秒)，超過該秒數後，該次啟動即視同新的作業階段。這個逾時值也套用至將應用程式傳送至背景並重新啟動時。應用程式在背景花的時間，不算在作業階段長度中。

* **[!UICONTROL 批次限制]**

   指定在傳送資料前要佇列多少點擊。

   設為 0 表示立即傳送點擊。批次限制代表在連續呼叫中傳送之點擊數目的臨界值。例如，如果此選項設為 10，在第 10 個點擊前的每個點擊都會先儲存在佇列中。直到第 10 個點擊傳入，才會連續傳送全部 10 個點擊。

* **[!UICONTROL 更多詳情]**

   按一下&#x200B;**[!UICONTROL 「更多詳情」]連結即可檢視報表套裝 ID 和追蹤伺服器、啟用或停用離線追蹤，以及檢視所使用的字元編碼模式 (例如 UTF-8)。**

   啟用離線追蹤時，裝置離線時產生的資料會加上時間戳記並在稍後傳送。若停用此選項，則會捨棄離線資料。