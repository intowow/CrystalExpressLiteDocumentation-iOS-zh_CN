## 1. 什麼是測試模式?
測試模式是針對整合測試時使用以避免混淆正式環境的廣告。測試模式下的廣告不會出現在正式模式中。

## 2. 如何上廣告到測試模式?
營運端可以在後台上廣告時，於委刊項設定打開測試模式的開關，此廣告即會投遞於測試模式中。

## 3. 測試模式與正式模式廣告服務有何不同?
測試模式不支援鎖定地理位置投遞廣告。

## 4. 程式整合時如何啟用測試模式?
初始化 SDK 時將測試模式開關設為 `YES` 即可
```objc
// init SDK with test mode
  [I2WAPI initWithVerboseLog:YES isTestMode:YES crystalId:@"yourcrystalidhere"];
```
