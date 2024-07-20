---
keywords: 모바일 앱,aep sdk,기본 앱,웹 보기,기본;swift,adobe experience platform mobile sdk,모바일 sdk,기본 코드
description: 웹 보기가 있는 기본 앱에서  [!DNL AEP Mobile SDK] 을(를) 사용하여  [!DNL Adobe Target] 을(를) 구현하는 방법에 대해 알아봅니다.
title: 웹 보기에서 네이티브 코드를 사용하는 모바일 앱에서  [!DNL Adobe Target] 구현
feature: Implement Mobile
role: Developer
exl-id: 3dd2e1d7-c744-4ba8-aaa4-6c2fe64d01fa
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# 웹 보기를 사용하는 기본 앱에서 [!DNL AEP Mobile SDK]을(를) 사용하여 [!DNL Target] 구현

이 문서에서는 [!DNL Adobe Experience Platform Mobile SDK]을(를) 사용하여 웹 보기에서 네이티브 코드를 사용하는 모바일 앱에서 [!DNL Adobe Target]을(를) 구현하기 위한 모범 사례를 공유합니다.

이 문서에서는 [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/getting-started/){target=_blank} 및 GitHub 저장소의 [Swift](https://github.com/adobe/aep-sdk-app/){target=_blank}에 작성된 [!DNL Target] 통합을 사용하는 샘플 iOS 앱을 사용합니다.

실제 환경에서는 엔터프라이즈 앱이 모바일 앱에서 웹 보기를 사용할 수 있습니다. 웹 보기는 URL을 사용하여 웹 페이지를 로드하는 컨테이너입니다. 이 컨테이너는 컨트롤이 없는 브라우저 창과 유사합니다. iOS에서 웹 보기 컨테이너는 웹 페이지를 처리할 때 Safari 브라우저로 작동합니다.

## 전제 조건

[!DNL Adobe Experience Platform Mobile SDK]을(를) 시작하려면 몇 가지 전제 조건 작업을 수행해야 합니다.

자세한 내용은 [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/){target=_blank} 설명서의 [Adobe Target](https://developer.adobe.com/client-sdks/documentation/adobe-target/){target=_blank}을(를) 참조하십시오.

## 기본 코드와 웹 보기 동기화

웹 보기가 있는 기본 앱에서 [!DNL Target]을(를) 구현할 때 어려움은 [!DNL Adobe Experience Platform Mobile SDK]이(가) [!DNL Adobe] 솔루션이 원활하게 작동하는 데 필요한 모든 식별자를 이미 생성했다는 것입니다. 그러나 식별자는 기본 플랫폼 환경에 없으므로 웹 보기에 아직 표시되지 않습니다. 따라서 방문자 ID가 웹 환경에서 지속되도록 일부 SDK 식별자를 웹 보기에 전달하는 브리지를 만들어야 합니다. 이 작업을 제대로 수행하지 못하면 중복 방문이 발생하고, 이는 보고에 영향을 줍니다.

다행히 [!DNL Adobe Experience Platform Mobile SDK]에서는 다음 샘플 코드와 같이 웹 보기에서 동일한 방문자를 사용하고 유지하는 데 필요한 [!DNL Adobe] 매개 변수를 생성하는 편리한 방법을 제공합니다.

```swift
Identity.appendTo(url: URL(string: url), completion: {appendedURL, error in
  print("appendedURL \(String(describing: appendedURL))")
  // load the url with ECID on the main thread
  DispatchQueue.main.async {
    let request = NSMutableURLRequest(url: appendedURL!)
    self.webView.load(request as URLRequest)
  }
});
```

`Identity.appendTo` 메서드에 대한 자세한 내용 및 메서드 사용 방법의 예를 보려면 *Mobile SDK 설명서*&#x200B;에서 [Swift > 예제](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/tabs/api-reference/){target=_blank}을 참조하십시오.

`Identity.appendTo`을(를) 사용하는 URL:

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2
```

을 다음과 같이 변환합니다.

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2&adobe_mc=TS%3D1660667205%7CMCMID%3D69624092487065093697422606480535692677%7CMCORGID%3DEB9CAE8B56E003697F000101%40AdobeOrg
```

알 수 있듯이 URL에 `adobe_mc` 매개 변수가 추가되었습니다. 이 매개변수에는 다음에 대한 인코딩된 값이 포함되어 있습니다.

* TS=1660667205: 현재 타임스탬프입니다. 이 타임스탬프는 웹 보기가 만료된 값을 받지 않도록 합니다.
* MCMID=69624092487065093697422606480535692677: [!UICONTROL Experience Cloud ID](ECID). [!DNL Adobe] 솔루션 간 방문자 식별에 필요한 MID 또는 [!UICONTROL Marketing Cloud ID]이라고도 합니다.
* MCORGID=EB9CAE8B56E003697F000101@AdobeOrg: [!UICONTROL Adobe Organization ID].

`Identity.getUrlVariables`은(는) [!DNL Experience Cloud Identity Service] URL 변수를 포함하는 적절한 형식의 문자열을 반환하는 대체 [!DNL Adobe Experience Platform Mobile SDK] 메서드입니다. 자세한 내용은 *ID API 참조*&#x200B;에서 [getUrlVariables](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/api-reference/#geturlvariables){target=_blank}을(를) 참조하십시오.

## 동일 세션 환경을 위해 [!DNL Target] 세션 ID를 전달합니다.

[!DNL Target] 사용자 여정이 기본 보기와 웹 보기에서 원활하게 작동하도록 하려면 한 단계 더 필요합니다. 이 단계에는 [!DNL Adobe Experience Platform Mobile SDK]에서 [!DNL Target] 세션 ID를 추출하여 모바일 앱의 웹 보기로 전달하는 작업이 포함됩니다.

`Target.getSessionId`은(는) 웹 보기 URL에 전달할 수 있는 세션 ID를 `mboxSession` 매개 변수로 추출합니다.

```swift
Target.getSessionId { (id, err) in
    // read Target sessionId
}
```

## 웹 보기에서 테스트

웹 미리 보기 링크는 [!UICONTROL Activity detail] 페이지에서 [[!UICONTROL Adobe QA] 링크](/help/dev/implement/mobile/target-mobile-preview.md)를 클릭하여 다음과 같이 각 경험 미리 보기 링크를 복사하는 팝업을 표시합니다.

```
?at_preview_token=mhFIzJSF7JWb-RsnakpBqi_s83Sl64hZp928VWpkwvI&at_preview_index=1_1&at_preview_listed_activities_only=true
```

웹 미리 보기 링크에 추가 `at_preview_index` 및 `at_preview_listed_activities_only` 매개 변수가 포함되어 있습니다. 이러한 매개 변수를 복사하여 웹 링크 매개 변수를 사용하여 모바일 친화적인 미리 보기 링크를 구성합니다.

예:

```
com.adobe.targetmobile://?at_preview_token=mhFIzJSF7JWb-RsnakpBqhBwj-TiIlZsRTx_1QQuiXLIJFdpSLeEZwKGPUyy57O_&at_preview_index=1_1&at_preview_listed_activities_only=true
```

iOS Safari 브라우저에서 링크를 열면 앱은 다음 예제와 유사하게 `AppDelegate` 클래스의 URL을 캡처합니다.

```swift
func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {
  print("url= \(String(describing: url.absoluteString))")
  //...
```

앱에서 필요한 모든 매개 변수를 캡처했으므로 필요할 때 웹에 전달할 수 있습니다.

```swift
Identity.appendTo(url: URL(string: url), completion: {appendedURL, error in
  let urlWithWebPreviewLink = appendedURL + "&" + myPreviewLinkFromAppDelegate
```

웹 보기 링크에 대한 최종 출력은 다음과 같습니다.

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2&adobe_mc=TS%3D1660667205%7CMCMID%3D69624092487065093697422606480535692677%7CMCORGID%3DEB9CAE8B56E003697F000101%40AdobeOrg&at_preview_token=mhFIzJSF7JWb-RsnakpBqi_s83Sl64hZp928VWpkwvI&at_preview_index=1_1&at_preview_listed_activities_only=true
```
