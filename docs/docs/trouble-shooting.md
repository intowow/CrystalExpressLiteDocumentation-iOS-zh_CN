當您正在除錯時, 請初始化 I2WAPI debug message 開關設為 YES 來印出除錯訊息
```objc
[I2WAPI initWithVerboseLog:YES isTestMode:NO crystalId:@"yourcrystalidhere"];
```

## Crystal_id 不正確
- 您的訊息視窗出現此訊息:
    - `error:[Request failed: not found (404)], please reverify your crystal_id is set correct`
- 這表示您的填在 CrystalExpress.plist 裡的 Crystal_Id 不正確, 請重新檢查並校正

## [__NSArrayI enumFromString:]: unrecognized selector 閃退
- 您的 app 閃退時出現此訊息:
```
[__NSArrayI enumFromString:]: unrecognized selector sent to instance 0x78e37970
```
- 添加 -ObjC in TARGETS -> Build Settings -> Linking -> Other Linker Flags
