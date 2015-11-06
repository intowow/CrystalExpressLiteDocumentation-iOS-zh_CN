## 1. 要求原生廣告
```objc
- (void)loadNativeAd {
    CENativeAd *nativeAd = [[CENativeAd alloc] initWithPlacement:@"YOUR_PLACEMENT_NAME"];

    // set delegate to self
    nativeAd.delegate = self;

    [nativeAd loadAd];
}
```

## 2. 利用回傳的廣告素材創建原生廣告 view
## 3. 註冊原生廣告
```objc
#pragma mark - CENativeAdDelegate
- (void)nativeAdDidLoad:(CENativeAd *)nativeAd
{
    _nativeAd = nativeAd;

    __weak typeof(self) weakSelf = self;
    [self.nativeAd.icon loadImageAsyncWithBlock:^(UIImage *image) {
        __strong typeof(self) strongSelf = weakSelf;
        strongSelf.adIconImageView.image = image;
    }];

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

### 注意事項
1. 若是重複利用 AdView 來顯示原生廣告, 請呼叫 `[nativeAd unregisterView]` 清除前一次註冊的原生廣告內容

## Reference
- [API reference]()
- [Sample code project]()
