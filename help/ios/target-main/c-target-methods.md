---
description: 以下為 iOS 資料庫所提供的 Adobe Target 方法清單。
seo-description: 以下為 iOS 資料庫所提供的 Adobe Target 方法清單。
seo-title: Adobe Mobile Services的iOS Target方法
solution: Marketing Cloud、Analytics
title: iOS適用的Target方法
topic: 開發人員和實施
uuid: 692bcda1-02ba-4902-bd65-15888adf1952
translation-type: tm+mt
source-git-commit: df4ea2c4002611c72009cf69598cbbb74b5c15c4

---


# iOS的Target方法 {#target-methods}

以下為 iOS 資料庫所提供的 Adobe Target 方法清單。

SDK目前支援多個Adobe Experience Cloud解決方案，包括Analytics、Target、Audience Manager和Adobe Experience Platform Identity Service。各方法會根據解決方案加上前置詞。例如， 方法會加上前置詞 `target`target。

>[!TIP]
>
>生命週期量度會以參數形式傳送至各 mbox 負載。如需詳細資訊，請參閱[生命週期量度](/help/ios/metrics.md)。

## 類別參考：ADBTargetLocationRequest

### 屬性

```objective-c
NSString *name; 
NSString *defaultContent; 
NSMutableDictionary *parameters;
```

### 字串常數

>[!TIP]
>
>下列常數用於自訂參數的設定時，易於使用。

```iOS
NSString *const ADBTargetParameterOrderId; 
NSString *const ADBTargetParameterOrderTotal; 
NSString *const ADBTargetParameterProductPurchasedId; 
NSString *const ADBTargetParameterCategoryId; 
NSString *const ADBTargetParameterMbox3rdPartyId; 
NSString *const ADBTargetParameterMboxPageValue; 
NSString *const ADBTargetParameterMboxPc; 
NSString *const ADBTargetParameterMboxSessionId; 
NSString *const ADBTargetParameterMboxHost;
```

>[!IMPORTANT]
>
>* If you are using SDKs **before** version 4.14.0, see [Input Parameters](https://developers.adobetarget.com/api/#input-parameters) for parameters limitations.
   >
   >
* If you are using SDKs version 4.14.0 **or after**, see [Batch Input Parameters](https://developers.adobetarget.com/api/#batch-input-parameters) for parameters limitations.


### 方法

* **targetLoadRequest:&#x200B;callback**

   Sends request to your configured Target server and returns the string value of the offer that is generated in a block `callback`.

   * 以下是此方法的語法:

      ```objective-c
      + (void) targetLoadRequest:(ADBTargetLocationRequest *)request
                        callback:(void (^)(NSString *content))callback;
      ```

   * 以下是此方法的範例程式碼:

      ```objective-c
      [ADBMobile targetLoadRequest:myRequest
                          callback:^(NSString *content) {
                            // do something with content
                          }];
      ```

* **targetLoadRequestWithName:defaultContent:profileParameters:orderParameters:mboxParameters:requestLocationParameters:callback:**

   傳送要求至您設定的 Target 伺服器並傳回區塊回撥中產生之選件的字串值。

   * 以下是此方法的語法:

      ```objective-c
      + (void) targetLoadRequestWithName:(nullable NSString *)name
                          defaultContent:(nullable NSString *)defaultContent
                      profileParameters:(nullable NSDictionary *)profileParameters
                        orderParameters:(nullable NSDictionary *)orderParameters
                         mboxParameters:(nullable NSDictionary *)mboxParameters
                requestLocationParameters:(nullable NSDictionary *)requestLocationParameters
                                 callback:(nullable void (^)(NSString
                                 * __nullable content))callback;
      ```

   * 傳回: N/A

   * 以下是此方法的參數：

      * **`name`**

         您要擷取的 Target mbox/位置名稱。

         * **類型**: NSString*
      * **`defaultContent`**

         如果 Target 伺服器無法連線或使用者不符合促銷活動資格，則將會在回撥中傳回值。

         * **類型**: NSString*
      * **`profileParameters`**

         此字典中的值會根據 Target 要求進入「profileParameters」物件。

         * **類型**: NSDictionary*
      * **`orderParameters`**

         此字典中的值會根據 Target 要求進入「order」物件。

         * **類型**: NSDictionary
      * **`mboxParameters`**

         此字典中的值會根據 Target 要求進入「mboxParameters」物件。

         * **類型**: NSDictionary*
      * **`requestLocationParameters`**

         此字典中的值會根據 Target 要求進入「requestLocation」物件。

         **類型**: NSDictionary*

      * **`callback`**

         此方法將會與 Target 伺服器中的選件內容一併接受呼叫。如果 Target 伺服器無法連線，或使用者不符合促銷活動資格，則將會傳回 defaultContent。
      **類型**: 函式

   * 以下是此方法的範例程式碼:

      ```objective-c
      [ADBMobile targetLoadRequestWithName:@"myHeroBanner"
                            defaultContent:@"defaultHeroBanner.png"
                        profileParameters:@{@"age":@"20-29"}
                          orderParameters:nil
                           mboxParameters:@{@"customParam":@"customValue"}
                requestLocationParameters:@{@"host":@"my.hostname.com"}
                                 callback:^(NSString *content){
                                   // do something with content
                                   myImageView.image = [UIImage imageNamed:content];
                                 }];
      ```

      如需基礎Target API的詳細資訊，請參閱 [Adobe Target開發人員](https://docs.adobe.com/dev/products/target/reference/delivery.html)。







* **targetLoadRequestWithName:defaultContent:profileParameters:orderParameters:mboxParameters:callback**

   傳送要求至您設定的 Target 伺服器，並傳回區塊回撥中產生之選件的字串值。

   * 以下是此方法的語法:

      ```objective-c
      + (void) targetLoadRequestWithName:(nullable NSString *)name
                          defaultContent:(nullable NSString *)defaultContent
                      profileParameters:(nullable NSDictionary *)profileParameters
                        orderParameters:(nullable NSDictionary *)orderParameters
                         mboxParameters:(nullable NSDictionary *)mboxParameters
                               callback:(nullable void (^)(NSString * __nullable content))callback;
      ```

   * 以下是此方法的範例程式碼:

      ```objective-c
      [ADBMobile targetLoadRequestWithName:@"mboxName"
                            defaultContent:@"defaultContent"
                         profileParameters:{@"profile-parameter-key": @"profile-parameter-value"}
                           orderParameters:@{@"order-parameter-key": @"order-parameter-value"}
                            mboxParameters:@{@"mbox-parameter-key": @"mbox-parameter-value"}
                                   callback:^(NSString * content) {
                                           //do something with content 
                                 }
                               }];
      ```

* **targetCreateOrder&#x200B;ConfirmRequestWithName:&#x200B;orderId:&#x200B;orderTotal:&#x200B;productPurchasedId:&#x200B;parameters**

   建立 `ADBTargetLocationRequest`一個。

   * 以下是此方法的語法:

      ```objective-c
      + (ADBTargetLocationRequest *)
      targetCreateOrderConfirmRequestWithName:(NSString *)name
                                      orderId:(NSString *)orderId
                                  orderTotal:(NSString *)orderTotal
                          productPurchasedId:(NSString *)productPurchasedId
                              parameters:(NSDictionary *)parameters;
      ```

* **targetCreateRequestWithName:&#x200B;&#x200B;defaultContent:&#x200B;parameters**

   方便讓建構函式使用指定的參數來建立 ADBTargetLocationRequest 物件。

   * 以下是此方法的語法:

      ```objective-c
      + (ADBTargetLocationRequest *)
      targetCreateRequestWithName:(NSString *)name
                           defaultContent:(NSString *)defaultContent
                               parameters:(NSDictionary *)parameters;
      ```

   * 以下是此方法的範例程式碼:

      ```objective-c
      ADBTargetLocationRequest *myRequest =  
      [ADBMobile targetCreateRequestWithName:@"heroBanner"
                              defaultContent:@"default.png"
                                  parameters:nil];
      ```

* **targetThirdPartyID**

   傳回第三方 ID。

   * 以下是此方法的語法:

      ```objective-c
      + (nullable NSString *) targetThirdPartyID;
      ```

   * 以下是此方法的範例程式碼:

      ```objective-c
      NSString *thirdPartyId = [ADBMobile targetThirdPartyID];
      ```

* **targetSetThirdPartyID**

   設定第三方 ID。

   * 以下是此方法的語法:

      ```objective-c
      + (void) targetSetThirdPartyID:(nullable NSString *)thirdPartyID;
      ```

   * 以下是此方法的範例程式碼:

      ```objective-c
      [ADBMobile targetSetThirdPartyID:@"thirdPartyID"];
      ```

* **targetClearCookies**

   清除應用程式中的目標 Cookie。

   >[!TIP]
   >
   >自SDK4.10.0版起，Target不再使用Cookie。此方法會重設 thirdPartyID 和 sessionID。

   * 以下是此方法的語法:

      ```objective-c
      + (void) targetClearCookies;
      ```

   * 以下是此方法的範例程式碼:

      ```objective-c
      [ADBMobile targetClearCookies];
      ```

* **targetPcID**

   傳回 PcID。

   * 以下是此方法的語法:

      ```objective-c
      + (nullable NSString *) targetPcID;
      ```

   * 以下是此方法的範例程式碼:

      ```objective-c
      NSString *myTargetPcID = [ADBMobile targetPcID];
      ```

* **targetSessionID**

   傳回 SessionID。

   * 以下是此方法的語法:

      ```objective-c
      + (nullable NSString *) targetPcID;
      ```

   * 以下是此方法的範例程式碼:

      ```objective-c
      NSString *myTargetSessionID = [ADBMobile targetSessionID];
      ```

### 範例

```objective-c
// make your request 
ADBTargetLocationRequest *myRequest =  
 [ADBMobile targetCreateRequestWithName:@"heroBanner"  
                         defaultContent:@"default.png"  
                          parameters:nil]; 
// load your request 
[ADBMobile targetLoadRequest:myRequest  
                    callback:^(NSString *content) { 
                        // do something with content 
                        heroImage.image = [UIImage imageNamed:content];
                    }];
```