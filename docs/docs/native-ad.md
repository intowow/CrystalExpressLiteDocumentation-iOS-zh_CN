您可以透過以下步驟為 iOS App 添加原生廣告。
## 1. 要求原生廣告
```objc
- (void)loadNativeAd {
    CENativeAd *nativeAd = [[CENativeAd alloc] initWithPlacement:@"廣告版位名稱"];

    // set delegate to self
    nativeAd.delegate = self;

    [nativeAd loadAd];
}
```

## 2. 利用回傳的廣告素材創建原生廣告 view
- SDK 完成讀取原生廣告素材之後會呼叫 `nativeAdDidLoad:(CENativeAd *)nativeAd` 這個代理人方法, App 可以透過 `nativeAd` 取得下列廣告元件
    - 文字
        - 廣告標題: `nativeAd.title`
        - 廣告文字描述: `nativeAd.body`
        - 廣告動作文字: `nativeAd.callToAction`
    - 圖像
        - 廣告 icon: `nativeAd.icon`, 可以透過 `loadImageAsyncWithBlock` 讀取得到 `UIImage`
    - 主要廣告內容
        - 需搭配 `CEMediaView` 來讀取, App 可以控制 `CEMediaView` 的大小做最佳的廣告展示
            - ex. `[self.adMediaCoverView setNativeAd:nativeAd]`
- App 可以自行組合以上廣告元件並展示最適合 App 的原生廣告
```objc
#pragma mark - CENativeAdDelegate

//
// In demo code, we have layout demo native Ad in storyboard.
// Please see the source code at: https://github.com/intowow/CrystalExpressCNSample/tree/master/CrystalExpressLite
// After nativeAd did load, we setup each app component by access nativeAd
// ex. nativeAd.title, nativeAd.body ...etc
//
- (void)nativeAdDidLoad:(CENativeAd *)nativeAd
{
    _nativeAd = nativeAd;

    __weak typeof(self) weakSelf = self;
    [self.nativeAd.icon loadImageAsyncWithBlock:^(UIImage *image) {
        __strong typeof(self) strongSelf = weakSelf;
        strongSelf.adIconImageView.image = image;
    }];

    // self.adMediaCoverView is a CEMediaView instance
    [self.adMediaCoverView setNativeAd:nativeAd];
    self.adTitle.text = nativeAd.title;
    self.adBody.text = nativeAd.body;
    [self.callToActionBtn setTitle:nativeAd.callToAction forState:UIControlStateNormal];

    // layout your own native ad components....
    //

    // register the ad view with nativeAd
    [nativeAd registerViewForInteraction:self.adUIView
                      withViewController:self];

//    You can replace to use the following method to specify the clicable area
//
//    NSArray *clickableViews = @[
//                                self.callToActionBtn,
//                                self.adBody,
//                                ];
//
//    [nativeAd registerViewForInteraction:self.adUIView
//                      withViewController:self
//                      withClickableViews:clickableViews];

}

```

## 3. 註冊原生廣告
- 最後我們要跟 `nativeAd` 註冊用戶可互動的範圍, 標示哪些廣告元件可以點擊
```objc
    ....

    // register the ad view with nativeAd
    [nativeAd registerViewForInteraction:self.adUIView
                      withViewController:self];

//    You can replace to use the following method to specify the clicable area
//
//    NSArray *clickableViews = @[
//                                self.callToActionBtn,
//                                self.adBody,
//                                ];
//
//    [nativeAd registerViewForInteraction:self.adUIView
//                      withViewController:self
//                      withClickableViews:clickableViews];

    ....
```

## 4. 控制原生廣告播放
- 當呼叫 `CEMediaView` 的 `setNavieAd` 之後，會組成廣告主要的 View (可能是 image/animation/video)

```objc
    [self.adMediaCoverView setNativeAd:nativeAd];
```

- 可以透過 `CEMediaView` 的 instance 來控制廣告行為
    - 視頻播放/停止
    - 視頻開啟聲音/關閉聲音

```objc
// play AD while view controller appear
- (void)viewDidAppear:(BOOL)animated
{
    [super viewDidAppear:animated];
    if (_adMediaCoverView) {
        [_adMediaCoverView play];
    }
}

// stop AD while view controller disappear
- (void)viewDidDisappear:(BOOL)animated
{
    [super viewDidDisappear:animated];
    if (_adMediaCoverView) {
        [_adMediaCoverView stop];
    }
}

// use the following method to control mute/unmute
[_adMediaCoverView mute];
[_adMediaCoverView unmute];
```

## 5. 清除暫存廣告
```objc
- (void)destroyAD
{
    if (_adMediaCoverView) {
        [_adMediaCoverView destroy];
        _adMediaCoverView = nil;
    }
}
```

### 注意事項
1. 若是重複利用 AdView 來顯示原生廣告，請呼叫 `[nativeAd unregisterView]` 清除前一次註冊的原生廣告內容

## Reference
- [API reference](http://intowow.github.io/CrystalExpressLiteDocumentation-iOS-zh_CN/)
- [範例程式](https://github.com/intowow/CrystalExpressSample-Lite-iOS)
