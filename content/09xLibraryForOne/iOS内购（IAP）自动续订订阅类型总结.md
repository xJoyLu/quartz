## 一、介绍

> -   **iOS** 的 **App** 内购类型有四种：
> -   1.  **消耗型商品：**只可使用一次的产品，使用之后即失效，必须再次购买。  
>         **示例：**钓鱼 **App** 中的鱼食。
> -   2.  **非消耗型商品：**只需购买一次，不会过期或随着使用而减少的产品。  
>         **示例：**游戏 **App** 的赛道。
> -   3.  **自动续期订阅：**允许用户在固定时间段内购买动态内容的产品。除非用户选择取消，否则此类订阅会自动续期。  
>         **示例：**每月订阅提供流媒体服务的 **App**。
> -   4.  **非续期订阅：**允许用户购买有时限性服务的产品。此 **App** 内购买项目的内容可以是静态的。此类订阅不会自动续期。  
>         **示例：**为期一年的已归档文章目录订阅。

经过完成这次的项目，我觉得其中最麻烦的就是 **自动续期订阅** 类型。因为其他几类都是一次性的内购类型，而只有自定续期订阅类是有连续性的，其中还有**免费试用期**、**促销期**的概念，用户还可以**取消续订**，**恢复续订**等。后台也需要有很多相应的逻辑操作。在这里总结一下完成自动续订订阅类型过程中遇到的问题和一些坑，希望帮助到大家。

## 二、创建自动续订类型时需要注意的地方

#### 1、App 专用共享密钥：

需要创建一个 **“App 专用共享密钥”**，它是用于接收此 **App** 自动续订订阅收据的唯一代码。这个秘钥用来想苹果服务器进行校验票据 **receipt**，不仅需要传 **receipt**，还需要传这个秘钥。  
如果您需要将此 **App** 转让给其他开发人员，或者需要将主共享密钥设置为专用，可能需要使用 **App 专用共享密钥**。  

![](//upload-images.jianshu.io/upload_images/1802326-5892de248ac8bc78.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

#### 2、订阅群组：

-   订阅群组相关的详细建议看下这个 [**订阅群组的官方文档**](https://links.jianshu.com/go?to=https%3A%2F%2Fhelp.apple.com%2Fapp-store-connect%2F%23%2Fdev7f2d6b652)。

创建自动续订类型的时候，如果还不存在订阅群组，就需要创建一个，以向用户提供一系列内容供应、服务等级或时限。名字可以自己随便起，就是给自己看的，有代表意义就行，一个群组下可以有多个自动续订订阅。如果你要搞促销优惠，那么每个顾客可以享受每个订阅群组的一个推介促销优惠一次。

一个订阅群组中的订阅是 **互斥** 的，这意味着用户只能一次订阅一个群组中的一个选项。如果你希望用户能够一次购买多个订阅，你可以将这些 **App** 内购买项目放在不同的订阅群组中。  

![](//upload-images.jianshu.io/upload_images/1802326-f9c8e755ec9ea6d8.png?imageMogr2/auto-orient/strip|imageView2/2/w/818/format/webp)

#### 3、订阅状态 URL：

自动续订订阅还需要填写订阅状态 **URL**。在 **App 信息** 里配置，这个 **URL** 配置以后，我们后台就能收到 **server to server** 的通知了。文章最后后详细讲后台的相关操作。  

![](//upload-images.jianshu.io/upload_images/1802326-ef0e80333e00611c.png?imageMogr2/auto-orient/strip|imageView2/2/w/968/format/webp)

#### 4、推介促销优惠：

-   促销优惠相关的详细建议看下这个 [**价格与销售范围的官方文档**](https://links.jianshu.com/go?to=https%3A%2F%2Fhelp.apple.com%2Fapp-store-connect%2F%23%2Fdev2acb77fcc)。

**推介促销优惠** 可以设置各种优惠，比如像我们公司的项目采取的就是前七天免费试用，当然你也可以设置前两个月半价等等。  

![](//upload-images.jianshu.io/upload_images/1802326-b0674b80aec6377c.png?imageMogr2/auto-orient/strip|imageView2/2/w/1170/format/webp)

这个推介促销优惠的三种类型：  

![](//upload-images.jianshu.io/upload_images/1802326-87dcd053f61ce80f.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

属性

描述

随用随付

如果您选择“随用随付”，则顾客将按选定时限的每个结算周期支付折扣价格（例如，订阅的标准价格为 9.99 美元，折扣价为前 3 个月每月 1.99 美元）。

提前支付

如果您选择“提前支付”，顾客将一次性支付选定时限的折扣价格（例如，订阅的标准价格为 9.99 美元，折扣价为前 2 个月 1.99 美元）。

免费

如果您选择“免费”，则顾客在选定的时限内免费访问订阅。时限可以是 3 天、1 周、2 周、1 个月、2 个月、3 个月、6 个月或 1 年。一个月的免费试用在 28 到 31 天不等。

**⚠️ 注意：**此价格面向新顾客。推介促销优惠可用于吸引 **新顾客**。就是说这个用户享受过七天免费试用了，那么下次就享受不了了，这个是由苹果去判断的。  
**下面是苹果让谨记的原话：**

> -   顾客可以享受每个订阅群组的一个推介促销优惠
> -   您可以针对每个地区设置一个当前推介促销优惠和一个未来推介促销优惠
> -   您可以在 **App Store Connect** 中管理地区销售范围、开始和结束日期
> -   如果您已[推广您的 App 内购买项目](https://links.jianshu.com/go?to=https%3A%2F%2Fhelp.apple.com%2Fapp-store-connect%2F%23%2Fdeve3105860f)，推介促销优惠将显示在您的 **App Store** 产品页上
> -   推介促销优惠适用于运行 **iOS 10、Apple TVOS 10** 和 **macOS 10.12.6** 及更高版本的顾客

## 二、内购流程

#### 1. 流程简述

**先来看一下iOS内购的通用流程：**  

![](//upload-images.jianshu.io/upload_images/1802326-88de93744d51cd9d.png?imageMogr2/auto-orient/strip|imageView2/2/w/388/format/webp)

支付流程.png

> -   1.  用户向苹果服务器发起购买请求，收到购买完成的回调（购买完成后会把钱打给申请内购的银行卡内）
> -   2.  购买成功流程结束后, 向服务器发起验证凭证（app端自己也可以不依靠服务器自行验证）
> -   3.  自己的服务器工作分 **4** 步：  
>         **3.1** 接收 **iOS** 端发过来的购买凭证。  
>         **3.2** 判断凭证是否已经存在或验证过，然后存储该凭证。  
>         **3.3** 将该凭证发送到苹果的服务器（区分沙盒环境还是正式环境）验证，并将验证结果返回给客户端。  
>         **sandbox** 开发环境：  
>         **[https://sandbox.itunes.apple.com/verifyReceipt](https://links.jianshu.com/go?to=https%3A%2F%2Fsandbox.itunes.apple.com%2FverifyReceipt)**  
>         **prod** 生产环境：  
>         **[https://buy.itunes.apple.com/verifyReceipt](https://links.jianshu.com/go?to=https%3A%2F%2Fbuy.itunes.apple.com%2FverifyReceipt)**  
>         具体操作可以看这个 [**通过App Store验证收据。**](https://links.jianshu.com/go?to=https%3A%2F%2Fdeveloper.apple.com%2Flibrary%2Farchive%2Freleasenotes%2FGeneral%2FValidateAppStoreReceipt%2FChapters%2FValidateRemotely.html%23%2F%2Fapple_ref%2Fdoc%2Fuid%2FTP40010573-CH104-SW3)  
>         **3.4** 修改用户相应的会员权限或发放虚拟物品。

简单来说就是将该购买凭证用 **Base64** 编码，然后 **POST** 给苹果的验证服务器，苹果将验证结果以 **JSON** 形式返回。  

![](//upload-images.jianshu.io/upload_images/1802326-cf1d74c53c6aedf5.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

#### 2. 具体实现

**自动订阅类型需要注意：**  
**app开始运行时，一定要添加监听**

```objc
[[SKPaymentQueue defaultQueue] addTransactionObserver:self];
```

因为自动订阅类型，除了第一次购买行为是用户主动触发的。后续续费都是 **Apple** 自动完成的，一般在要过期的前 **24** 小时开始，苹果会尝试扣费，扣费成功的话会在 **APP** 下次启动的时候主动推送给 **APP**。所以，**APP** 启动的时候一定要添加上面的那句话。

⚠️ **订单结束后一定要执行 finishTransaction 操作**

```objc
[[SKPaymentQueue defaultQueue] finishTransaction:transaction];
```

下面看一下重要的几个代理方法的实现：  
首先要引入苹果内购必须要的一个库 **StoreKit**

```objc
#import <StoreKit/StoreKit.h>
```

###### （1） 开始调起支付流程，请求商品信息，这里需要用到SKProductsRequestDelegate，它是商品请求回调，可告诉你有没有这个商品

```objc
/**
 调起支付，请求商品信息
 @param productId 商品Id（在苹果connect上配置的内购地址）
 */
- (void)payWithAppleProductID:(NSString *)productId {
    
    if ([SKPaymentQueue canMakePayments]) {
        // 如果允许应用内付费购买
        // 把商品ID信息放入一个集合中
        NSArray *productIdentifiers = [[NSArray alloc] initWithObjects: productId, nil];
        NSSet * set = [NSSet setWithArray:productIdentifiers];
        // 请求内购商品信息，只返回你请求的产品（主要用于验证商品的有效性）
        SKProductsRequest * request = [[SKProductsRequest alloc] initWithProductIdentifiers:set];
        request.delegate = self;
        [request start];
        
    } else {
        // 如果用户手机禁止应用内付费购买.
        // 则弹出开启购买权限开关的提示等...
    }
}

#pragma mark - SKProductRequestDelegate 
/**
 收到产品返回信息
 SKProductsRequest是苹果封装好的一个对象，该对象有两个属性。
 products是一个数组，代表的是你获取到的所有商品信息，每个商品  都是一个数组元素。
 invalidProductIdentifiers是无效的商品id的数组，此id对应的是你在苹果后台构建的商品id。
 */
- (void)productsRequest:(SKProductsRequest *)request didReceiveResponse:(SKProductsResponse *)response{

    NSLog(@"--------------收到产品反馈消息---------------------");
    NSArray *product = response.products;
    if([product count] == 0){
        [SVProgressHUD dismiss];
        NSLog(@"--------------没有商品------------------");
        return;
    }

    NSLog(@"productID:%@", response.invalidProductIdentifiers);
    NSLog(@"产品付费数量:%lu",(unsigned long)[product count]);

    SKProduct *requestProduct = nil;
    for (SKProduct *pro in product) {
        NSLog(@"%@", [pro description]);
        NSLog(@"%@", [pro localizedTitle]);
        NSLog(@"%@", [pro localizedDescription]);
        NSLog(@"%@", [pro price]);
        NSLog(@"%@", [pro productIdentifier]);
        // 如果后台消费条目的ID与我这里需要请求的一样（用于确保订单的正确性）
        if([pro.productIdentifier isEqualToString:_currentProId]){
            requestProduct = pro;
        }
    }

    // 发送购买请求
    //SKPayment *payment = [SKPayment paymentWithProduct:requestProduct];// 不可变的
    SKMutablePayment *payment = [SKMutablePayment paymentWithProduct:requestProduct];// 可变的
    payment.applicationUsername = @"123456";// 发起支付时候指定用户的userId
    [[SKPaymentQueue defaultQueue] addPayment:payment];
}

// 请求失败
- (void)request:(SKRequest *)request didFailWithError:(NSError *)error{
    NSLog(@"------------------错误-----------------:%@", error);
}

- (void)requestDidFinish:(SKRequest *)request{
    NSLog(@"------------反馈信息结束-----------------");
}
```

在发送购买请求的时候，我绑定了当前登录用户的 **id**

```objc
payment.applicationUsername = [Global sharedGlobal].loginInfo.userId;
```

这样在之后收到交易回调的时候，我可以根据携带的**applicationUsername** 来判断当前用户是否是同一个用户，如果是同一个用户再去验证票据。但不要完全依赖这个参数，因为在网上也看到有人说这个参数有时候会为空，所以我们在验证的时候要首先判断是否为空，如果不为空，再去和当前用户 **id** 比对。如果为空，就照常接着走验证票据流程就行了。

> -   **SKProductsRequest** 是苹果封装好的一个对象，该对象有两个属性。
> -   属性 **products** 是一个数组，代表的是你获取到的所有商品信息，每个商品都是一个数组元素。
> -   属性 **invalidProductIdentifiers** 是无效的商品id的数组，此id对应的是你在苹果后台构建的商品id。

```objc
// Array of SKProduct instances.
@property(nonatomic, readonly) NSArray<SKProduct *> *products NS_AVAILABLE(10_7, 3_0);

// Array of invalid product identifiers.
@property(nonatomic, readonly) NSArray<NSString *> *invalidProductIdentifiers NS_AVAILABLE(10_7, 3_0);
```

###### （2）判断购买结果，这里需要用到 **SKPaymentTransactionObserver**，**SKPaymentTransactionObserver** 是交易观察者，用来告诉你交易进行到哪个步骤了。

```objc
// 13.监听购买结果
- (void)paymentQueue:(SKPaymentQueue *)queue updatedTransactions:(NSArray *)transaction {
    
    for (SKPaymentTransaction *tran in transaction){
        
        switch (tran.transactionState) {
            case SKPaymentTransactionStatePurchased:
                NSLog(@"交易完成");
                // 订阅特殊处理
                if (tran.originalTransaction) {
                    // 如果是自动续费的订单,originalTransaction会有内容
                    NSLog(@"自动续费的订单,originalTransaction = %@",tran.originalTransaction);
                } else {
                    // 普通购买，以及第一次购买自动订阅
                    NSLog(@"普通购买，以及第一次购买自动订阅");
                }
                 if ([Global sharedGlobal].loginInfo.logined) {
                    // 只有登录了才去处理票据 和 执行finish操作
                    NSString *orderUserId = [[tran payment] applicationUsername];// 得到该订单的用户Id
                    if ((orderUserId && orderUserId.length > 0 && [[Global sharedGlobal].loginInfo.userId isEqualToString:orderUserId]) || (nil == orderUserId || orderUserId.length == 0)) {
                        // 当订单的userId和当前userId一致 或者 订单userId为空时才处理票据、执行finish操作
                        [self completeTransaction:tran];
                        [[SKPaymentQueue defaultQueue] finishTransaction:tran];// 销毁本次操作，由本地数据库进行记录和恢复
                    }
                }
                break;
            case SKPaymentTransactionStatePurchasing:
                NSLog(@"商品添加进列表");
                break;
            case SKPaymentTransactionStateRestored:
                NSLog(@"已经购买过商品");
                [[SKPaymentQueue defaultQueue] finishTransaction:tran];
                break;
            case SKPaymentTransactionStateFailed:
                NSLog(@"交易失败");
                [[SKPaymentQueue defaultQueue] finishTransaction:tran];
                break;
            default:
                break;
        }
    }
}

// 交易结束,当交易结束后还要去appstore上验证支付信息是否都正确,只有所有都正确后,我们就可以给用户方法我们的虚拟物品了。
- (void)completeTransaction:(SKPaymentTransaction *)transaction {
    
    NSString * str = [[NSString alloc] initWithData:transaction.transactionReceipt encoding:NSUTF8StringEncoding];
    NSString *environment = [self environmentForReceipt:str];
    NSLog(@"----- 完成交易调用的方法completeTransaction 1--------%@",environment);
    // 验证凭据，获取到苹果返回的交易凭据
    NSURL *receiptURL = [[NSBundle mainBundle] appStoreReceiptURL];// appStoreReceiptURL iOS7.0增加的，购买交易完成后，会将凭据存放在该地址
    NSData *receiptData = [NSData dataWithContentsOfURL:receiptURL];// 从沙盒中获取到购买凭据
    NSString *encodeStr = [receiptData base64EncodedStringWithOptions:NSDataBase64EncodingEndLineWithLineFeed];// BASE64 常用的编码方案，通常用于数据传输，以及加密算法的基础算法，传输过程中能够保证数据传输的稳定性，BASE64是可以编码和解码的
    
    if (![UserOrderInfo isHasReceiptDate:encodeStr]) {
        // 如果本地数据库没有此条票据记录
        NSString *environmentStr;
        if ([environment isEqualToString:@"environment=Sandbox"]) {
            environmentStr = @"sandbox";
        } else {
            environmentStr = @"product";
        }
        // 将票据POST给自己的服务器去校验...        
    }
}
```

要发给后台同事的交易凭据长度会很大，一开始是 **7000** 多位，所以后台限制了 **10000** 位长度，结果随着订阅增多，交易凭据也越来越大，最后都达到了 **3** 万多位，后台只好把长度改为了 **30** 万位限制。

-   > 我在以上的基础上，添加了本地数据的订单记录，以防止掉单，在验证票据之前先把所有数据包括票据都插入到了本地数据库，并且执行了**`Objc [[SKPaymentQueue defaultQueue] finishTransaction:transaction];`**  
    > 也就是告知苹果我的支付流程已经结束了。这样如果中途程序闪退或者其他情况出现，在下次启动 **app** 的时候会率先查询本地数据库有无未完成的订单操作并继续内购流程。就不依赖苹果自动的通知来继续完成内购了，因为苹果内购绑定的是 **appleId**，而大部分公司需求都是绑定自己 **app** 的用户 **id**。自己进行本地记录回复能更好的处理这种情况，当然如果用户换了设备当然就没办法了。
    

## 三、各种情况

#### 1. Upgrades and Plan Changes升级和计划变更

用户可以在 **App Store** 或您应用的界面中的帐户设置中管理他们的订阅。对于每个订阅，**App Store** 会显示订阅组提供的所有续订选项。用户可以轻松更改其服务级别，并根据需要随时选择升级，降级或交叉评级。任何持续时间的降级或具有不同持续时间的交叉等级将在下一个续订日期生效。

您可以查看收据的 **“订阅自动续订首选项”** 字段，以了解用户选择的任何计划更改，这些更改将在下一个续订日期生效。

#### 2. Expiration and Renewal到期和续订

订阅续订过程在到期日期前十天开始。在这十天内，App Store会检查可能会延迟或阻止订阅自动续订的任何结算问题，例如：

> -   客户的付款方式不再有效，
> -   自用户购买订阅以来，产品价格上涨，
> -   该产品已不再可用。

**App Store** 可以通知用户任何问题，以便他们可以在订阅到期之前解决它，并避免其订阅服务中断。  
在订阅到期之前的 **24** 小时内，**App Store** 开始尝试自动续订。**App Store** 会多次尝试在一段时间内自动续订订阅，但如果尝试失败次数过多，最终会停止。

> -   **注意：** 对于与帐单相关的问题，**App Store** 可能会尝试续订最多 **60** 天的订阅。您可以在收据中检查订阅重试标记，以确定 **App Store** 是否仍在尝试续订订阅。

#### 3. Cancellation消除

订阅在购买时全额支付。用户只能通过联系 **Apple** 客户服务获得退款。例如，如果用户意外购买了错误的产品，客户支持可以取消订阅并发出全部或部分退款。客户可以在订阅期间取消订阅，但订阅仍在同一时期结束时支付。

要检查 **Apple** 客户支持是否已取消购买，请在收据中查找 **“取消日期”** 字段。如果该字段包含日期，则无论订阅的到期日期如何，购买都已取消。关于提供内容或服务，将取消的交易视为没有进行过购买。

根据您的应用提供的产品类型，您可能需要检查当前有效的订阅期，或者您可能需要检查所有过去的订阅期。例如，杂志应用程序需要检查所有过去的订阅期，以确定用户应该访问哪些问题。具有流服务的应用程序仅需要检查当前活动的订阅以确定用户是否应该有权访问其服务。

## 三、服务端验证

其实内购也可以完全靠客户端自己去验证，但是为了安全起见，大部分公司都会选择让服务器端去验证订单的有效性。当然我们项目也不例外。  
首先要在 **itunes connection** 上配置自动续期订阅下，可以参考下面的苹果官方文档，[《启用针对自动续期订阅的服务器通知》](https://links.jianshu.com/go?to=https%3A%2F%2Fhelp.apple.com%2Fapp-store-connect%2F%23%2Fdev0067a330b)。  
自动续订订阅和其他类型的区别还有必须在 **App Store Connect** 中生成一个 **共享密钥**，把这个秘钥发给后台同事，并且我们填写好 **订阅状态 URL**。

如果这样配置了 **server to server** 的通知，后台就会收到下面的几种状态更新通知类型：

NOTIFICATION_TYPE

描述

**INITIAL_BUY**

初次购买订阅。latest_receipt通过在App Store中验证，可以随时将您的服务器存储在服务器上以验证用户的订阅状态。

**CANCEL**

Apple客户支持取消了订阅。检查Cancellation Date以了解订阅取消的日期和时间。

**RENEWAL**

已过期订阅的自动续订成功。检查Subscription Expiration Date以确定下一个续订日期和时间。

**INTERACTIVE_RENEWAL**

客户通过使用应用程序界面或在App Store中的App Store中以交互方式续订订阅。服务立即可用。

**DID_CHANGE_RENEWAL_PREF**

客户更改了在下次续订时生效的计划。当前的有效计划不受影响。

由此可以看出并没有用户正常续订的通知，这块就和安卓不一样了，安卓是会有续订的通知的。苹果是默认就续订上了，取消才会有通知。

一开始后台这边也是遇到了很多不懂的问题，最后发现同一个订单凭据是可以一直使用的，不管你后面续订了多少次，随便这些中的一个凭据发给苹果验证，就能得到所有的订单信息和订阅状态，这样每个周期结束的时候（试用期最后一天或者月底），就可以根据票据信息去得到用户是否仍然续订的信息，这样就可以决定是否继续给下个月的 **VIP** 了。

## 四、沙盒测试

因为我们的项目要求第一次购买自动续订的享受七天免费试用期，而一个苹果沙盒账号只能享受一次免费试用期，所以导致我每自测一次都要申请一个新的沙盒账号，提交给测试部门测试的时候又要申请一堆账号，最后申请了 **47** 个沙盒账号……  
在我们测试自动续期订阅时，时限会缩短。此外，测试订阅最多仅能自动续期 **6** 次。

实际时限

测试时限

1 周

3 分钟

1个月

5 分钟

2 个月

10 分钟

3 个月

15 分钟

6 个月

30 分钟

1 年

1 小时

和安卓相比，苹果测试起来没那么友好，尤其是没办法模拟用户手动取消订阅的场景，因为沙盒账号没有办法管理订阅。而安卓是可以测试这一场景的。

另外需要注意，沙盒账号的续订，如果一直打开着 **app**，可能过了 **5** 分钟续订周期也不会收到通知，最好是杀死 **app**，**5** 分钟后重新启动，这样就会收到续订的通知了。

> -   **使用户能够管理订阅**

在非沙盒账号的情况下，项目中可以设置为打开此 **URL** 启动**iTunes** 或 **iTunes Store** 并显示“管理订阅”页面。  
[https://buy.itunes.apple.com/WebObjects/MZFinance.woa/wa/manageSubscriptions](https://links.jianshu.com/go?to=https%3A%2F%2Fbuy.itunes.apple.com%2FWebObjects%2FMZFinance.woa%2Fwa%2FmanageSubscriptions)

⚠️**注意：** 如果你是通过 **TestFlight** 安装的，那么就不用使用**沙盒账号**进行购买了，需要使用**真实的账号**进行购买，当然也不会扣除你的钱的，只不过弹窗的说明变了，如下图：  

![](//upload-images.jianshu.io/upload_images/1802326-37b9061b6cd66240.jpeg?imageMogr2/auto-orient/strip|imageView2/2/w/616/format/webp)

## 五、关于审核

##### 1. 自动续订订阅的说明一定要有。

自动续订订阅，一定要在 **app** 中有详细的说明，类似下图这种：

![](//upload-images.jianshu.io/upload_images/1802326-100a8095ee4b9b69.jpeg?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

  
上面只是个例子，我们的 **app** 只做了会员服务协议，没有右边那个自动续费条款也没事儿。  
除了在 **app** 里要写，在 **iTunes Connect** 的应用描述里也要写，以喜马拉雅为例，如下图：

![](//upload-images.jianshu.io/upload_images/1802326-4303540a0c86bc92.jpeg?imageMogr2/auto-orient/strip|imageView2/2/w/1080/format/webp)

  
如果没有这些说明苹果基本是会拒你的。

##### 2. 不允许强制用户必须登录才能购买

因为苹果规定所有内购绑定的账号都应该是 **apple** 账号，所以不登陆你 **app** 自己的账号也应该可以购买，也就是游客状态下也要能购买，不然就耽误苹果赚钱了。  
关于这个问题有两个解决办法：  
（1）做游客模式可购买（未登录是绑定设备，下一个账号登录以后绑定账号）  
（2）必须登录才可以使用 **app**。  
当然也可以做一个审核接口来应对。

**以上总结参考了并部分摘抄了以下文章，非常感谢以下作者的分享！：  
[1、作者光彩影的《iOS内购：自动续期订阅总结》](https://www.jianshu.com/p/abd2ba4deb54)  
[2、苹果官方的帮助文档](https://links.jianshu.com/go?to=https%3A%2F%2Fhelp.apple.com%2Fapp-store-connect%2F%23%2Fdev636f037c8)  
[3、作者qiyer的《iOS 自动订阅开发》](https://www.jianshu.com/p/687c34c11002)**

  
  
作者：凡几多  
链接：https://www.jianshu.com/p/9531a85ba165  
来源：简书  
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。