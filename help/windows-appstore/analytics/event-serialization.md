---
description: 處理規則不支援事件序列化。在移動SDK中，必須在上下文資料參數中使用特殊語法來直接在伺服器調用上設定序列化事件。
solution: Experience Cloud Services,Analytics
title: 事件序列化
topic-fix: Developer and implementation
uuid: a5966d05-e218-446f-9f19-8664a84b74cd
exl-id: 42ea5e0f-a69e-44ab-aa4e-bbec27815cc8
source-git-commit: 5434d8809aac11b4ad6dd1a3c74dae7dd98f095a
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 31%

---

# 事件序列化{#event-serialization}

處理規則不支援事件序列化。在移動SDK中，必須在上下文資料參數中使用特殊語法來直接在伺服器調用上設定序列化事件。

```js
cdata["&&events"] = "event1:12341234";
```

例如：

```js
//create a context data dictionary 
var cdata = new Windows.Foundation.Collections.PropertySet(); 
 
// add events 
cdata["&&events"] = "event1:12341234"; 
 
var ADB = ADBMobile; 
// send the tracking call - use either a trackAction or TrackState call. 
// trackAction example: 
ADB.Analytics.trackAction("action", cdata); 
// trackState example: 
ADB.Analytics.trackState("State Name", cdata);
```
