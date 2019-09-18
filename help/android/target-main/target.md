---
description: 您可以在 Android 應用程式中提供目標式內容。
keywords: Android；資料庫；行動；sdk
seo-description: 您可以在 Android 應用程式中提供目標式內容。
seo-title: 目標設定
solution: Marketing Cloud、Analytics
title: 目標設定
topic: 開發人員和實施
uuid: 09fe2c9c-7b60-49c3-bb9 d-36a30 ce7 c350
translation-type: tm+mt
source-git-commit: 3cc97443fabcb9ae9e09b998801bbb57785960e0

---


# Target configuration {#target-configuration}

您可以在 Android 應用程式中提供目標式內容。

## Set the application context {#section_37CAE496FF894FCA821F7760605574CA}

**(必要)**`setContext()` 在主要活動的 `onCreate()` 方法中，一次必須呼叫方法。

例如:

```java
@Override 
public void onCreate(Bundle savedInstanceState) { 
  super.onCreate(savedInstanceState); 
  setContentView(R.layout.main); 
  Config.setContext(this.getApplicationContext()); 
}
```

如果您在實施 Analytics 或 Audience Management 時已新增此方法呼叫，便不需要再次新增。