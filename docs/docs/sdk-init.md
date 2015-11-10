## Import 標頭檔

添加下方的代碼到您的 `AppDelegate` 中來 import 標頭檔案 :
```objc
#import "I2WAPI.h"
```

## 初始化 SDK
在 application delegate 的 `application:didFinishLaunchingWithOptions:` 中初始化 CrystalExpress&trade; SDK Lite:
```objc
#import "I2WAPI.h"

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    // init SDK
    [I2WAPI initWithVerboseLog:NO isTestMode:NO crystalId:@"intowow提供的CRYSTAL_ID"];
    return YES;
}

```
- 設定 `initWithVerboseLog:(BOOL)` 將會 開啟/關閉 除錯訊息
- 設定 `isTestMode:(BOOL)` 將會控制是否初始化 SDK 成[測試模式](test-mode.md)
- `crystalId:(NSString *)` 請填入 intowow 配發給 App 的 Crystal ID 
