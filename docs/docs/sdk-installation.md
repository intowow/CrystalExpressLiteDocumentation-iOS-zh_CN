### 需求與限制
- CrystalExpress&trade; SDK Lite 需要 iOS 7.0 或是以上版本

### 下載 CrystalExpress&trade; SDK Lite

[下載連結](https://s3.cn-north-1.amazonaws.com.cn/intowow-sdk/ios/Manual/crystalexpress-lite-cn-1.0.1.zip)

### 安裝
1. 打開 xcode 中的 project 設定頁面，Build Phases > Link Binary With Libraries，加入 crystalexpress-lite-cn-1.0.1.a
2. 將 zip 檔中的 header 檔加入 project 中
3. 確認以下的 frameworks 都已加入 Build Phases
<ul>
  - MobileCoreServices.framework
  - SystemConfiguration.framework
  - AdSupport.framework
  - libz.tbd
  - CoreTelephony.framework
  - libsqlite3.tbd
  - AVFoundation.framework
  - libicucore.tbd</ul>
4. 在 TARGETS -> Build Settings -> Linking -> Other Linker Flags 加入 -ObjC
5. 安裝完成, 您可以開始使用 CrystalExpress SDK Lite library

### 允許 HTTP 連線
- 在 xcode 7 (iOS9) 之後，會阻擋 http 連線，需要在 Info.plist 中加入忽略的網址清單
- 目前許多廣告的點擊連結都還是 http 連線, 我們無法事先預知需要排除的網域名稱，因此需要允許任意的 http 連線

``` xml
<key>NSAppTransportSecurity</key>
<dict>
     <key>NSAllowsArbitraryLoads</key>
     <true/>
</dict>
```

### 範例程式

[網頁連結](https://github.com/intowow/CrystalExpressSample-Lite-iOS)
