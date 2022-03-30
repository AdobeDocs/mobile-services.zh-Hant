---
description: 具有促銷電子標籤和產品特定活動的產品變數示例。
solution: Experience Cloud Services,Analytics
title: 產品變數及其包含的銷售 eVar 與產品專屬事件
topic-fix: Developer and implementation
uuid: 94e882e4-b19d-4c48-9dfb-331465490347
exl-id: 3a90f624-da13-4c26-9e4c-3a4af33bc5ee
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '66'
ht-degree: 24%

---

# Products 變數及其包含的銷售 eVar 與產品專屬事件{#products-variable-with-merchandising-evars-and-product-specific-events}

具有促銷電子標籤和產品特定活動的產品變數示例。

```
//create a context data dictionary 
var cdata = new Windows.Foundation.Collections.PropertySet(); 
  
// add products, a purchase id, a purchase context data key, and any other data you want to collect. 
// Note the special syntax for products 
cdata["&&events"] = "event1 "; 
cdata["&&products"] = ";Running Shoes;1;69.95;event1=5.5;eVar1=Merchandising,;Running Socks;10;29.99"; 
cdata["m.purchaseid"] = "1234567890"; 
cdata["m.purchase"] = "1"; 
  
var ADB = ADBMobile; 
// send the tracking call - use either a trackAction or TrackState call. 
// trackAction example: 
ADB.Analytics.trackAction("purchase", cdata); 
// trackState example: 
ADB.Analytics.trackState("Order Confirmation", cdata);
```

>[!TIP]
>
>如果使用 *`&&products`* 變數，還必須在 *`&&events`* 變數，否則在處理期間過濾出事件。
