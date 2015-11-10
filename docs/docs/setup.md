## 基本要求
- CrystalExpressLite 需要 iOS 7.0 或是以上版本

## SDK 整合之前事項
- 如果您的 app 沒有申請過 `Crystal_Id`, 請跟 Intowow 申請

## 安裝 SDK
### 手動安裝 SDK
1. 下載 SDK
    - [crystalexpress-lite-cn-1.0.1](https://s3.cn-north-1.amazonaws.com.cn/intowow-sdk/ios/Manual/crystalexpress-lite-cn-1.0.1.zip)
2. 打開 xcode 中的 project 設定頁面, Build Phases > Link Binary With Libraries, 加入 CrystalExpressSDK-lite-CN-1.x.x.a
3. 將 zip 檔中的 header 檔加入 project 中
4. 確認以下的 frameworks 都已加入 Build Phases
    - MobileCoreServices.framework
    - SystemConfiguration.framework
    - AdSupport.framework
    - libz.tbd
    - CoreTelephony.framework
    - libsqlite3.tbd
    - AVFoundation.framework
    - libicucore.tbd
5. 在 TARGETS -> Build Settings -> Linking -> Other Linker Flags 加入 `-ObjC`
6. 安裝完成, 您可以開始使用 CrystalExpress SDK library

## 設定允許 Http 連線
- 在 xcode7 (iOS9) 之後, 會阻擋 http 連線, 需要在 Info.plist 中加入忽略的網址清單
- 目前許多廣告的點擊連結都還是 http 連線, 我們無法事先預知需要排除的 domain, 因此需要允許任意的 http 連線

```xml
<key>NSAppTransportSecurity</key>
<dict>
     <key>NSAllowsArbitraryLoads</key>
     <true/>
</dict>
```

## 建立廣告版位
- 請與 intowow 聯繫於後台建立廣告版位
