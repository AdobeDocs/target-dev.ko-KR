---
keywords: 모바일 앱,aep sdk,기본 앱,웹 보기,기본;swift,adobe experience platform mobile sdk,모바일 sdk,기본 코드
description: 구현 방법 알아보기 [!DNL Adobe Target] (으)로 [!DNL AEP Mobile SDK] 웹 보기가 있는 기본 앱에서.
title: 구현 [!DNL Adobe Target] 웹 보기에서 네이티브 코드를 사용하는 모바일 앱에서
feature: Implement Mobile
role: Developer
source-git-commit: c0fda36cb5472d71438c47b8b484716003da4214
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---


# 구현 [!DNL Target] (으)로 [!DNL AEP Mobile SDK] 웹 보기가 있는 기본 앱에서

이 문서에서는 구현을 위한 모범 사례를 공유합니다. [!DNL Adobe Target] 를 사용하여 웹 보기에 네이티브 코드를 사용하는 모바일 앱에서 [!DNL Adobe Experience Platform Mobile SDK].

이 문서에서는 다음을 사용하여 샘플 iOS 앱을 사용합니다. [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/getting-started/){target=_blank} and a [!DNL Target] integration written in [Swift from the GitHub repository](https://github.com/adobe/aep-sdk-app/){target=_blank}.

실제 환경에서는 엔터프라이즈 앱이 모바일 앱에서 웹 보기를 사용할 수 있습니다. 웹 보기는 URL을 사용하여 웹 페이지를 로드하는 컨테이너입니다. 이 컨테이너는 컨트롤이 없는 브라우저 창과 유사합니다. iOS에서 웹 보기 컨테이너는 웹 페이지를 처리할 때 Safari 브라우저로 작동합니다.

## 전제 조건

을(를) 시작하려면 [!DNL Adobe Experience Platform Mobile SDK]몇 가지 전제 조건 작업을 수행해야 합니다.

자세한 내용은 [Adobe Target](https://developer.adobe.com/client-sdks/documentation/adobe-target/){target=_blank} in the [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/){target=_blank} 설명서를 참조하십시오.

## 기본 코드와 웹 보기 동기화

구현 시 문제 [!DNL Target] 웹 보기가 있는 기본 앱에서 [!DNL Adobe Experience Platform Mobile SDK] 에 필요한 모든 식별자가 이미 생성되었습니다. [!DNL Adobe] 원활하게 작동할 수 있는 솔루션 그러나 식별자는 기본 플랫폼 환경에 없으므로 웹 보기에 아직 표시되지 않습니다. 따라서 방문자 ID가 웹 환경에서 지속되도록 일부 SDK 식별자를 웹 보기에 전달하는 브리지를 만들어야 합니다. 이 작업을 제대로 수행하지 못하면 중복 방문이 발생하고, 이는 보고에 영향을 줍니다.

다행히도 [!DNL Adobe Experience Platform Mobile SDK] 편리한 생성 방법을 제공합니다. [!DNL Adobe] 다음 샘플 코드에 표시된 것처럼 웹 보기에서 동일한 방문자를 사용하고 유지하는 데 필요한 매개 변수입니다.

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

에 대한 자세한 내용은 `Identity.appendTo` 메서드 및 메서드 사용 방법의 예를 보려면 [Swift > 예](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/tabs/api-reference/){target=_blank} 다음에서 *모바일 SDK 설명서*.

사용 `Identity.appendTo`, 이 URL:

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2
```

을 다음과 같이 변환합니다.

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2&adobe_mc=TS%3D1660667205%7CMCMID%3D69624092487065093697422606480535692677%7CMCORGID%3DEB9CAE8B56E003697F000101%40AdobeOrg
```

보시다시피 `adobe_mc` URL에 추가된 매개 변수입니다. 이 매개변수에는 다음에 대한 인코딩된 값이 포함되어 있습니다.

* TS=1660667205: 현재 타임스탬프입니다. 이 타임스탬프는 웹 보기가 만료된 값을 받지 않도록 합니다.
* MCMID=69624092487065093697422606480535692677: [!UICONTROL EXPERIENCE CLOUD ID] (ECID). MID 또는 [!UICONTROL MARKETING CLOUD ID] 다음에 필요함: [!DNL Adobe] 솔루션 간 방문자 식별.
* MCORGID=EB9CAE8B56E003697F000101@AdobeOrg: [!UICONTROL Adobe 조직 ID].

다음 `Identity.getUrlVariables` 대체 항목 [!DNL Adobe Experience Platform Mobile SDK] 다음을 포함하는 적절한 형식의 문자열을 반환하는 메서드 [!DNL Experience Cloud Identity Service] URL 변수. 자세한 내용은 [getUrlVariables](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/api-reference/#geturlvariables){target=_blank} 다음에서 *ID API 참조*.

## 전달 [!DNL Target] 동일 세션 경험의 세션 ID

을(를) 만들려면 한 가지 추가 단계가 필요합니다. [!DNL Target] 사용자 여정은 기본 보기와 웹 보기에서 원활하게 작동합니다. 이 단계에는 를 추출하고 전달하는 작업이 포함됩니다. [!DNL Target] 의 세션 ID [!DNL Adobe Experience Platform Mobile SDK] 모바일 앱의 웹 보기를 표시합니다.

다음 `Target.getSessionId` 는 웹 보기 URL에 전달될 수 있는 세션 ID를 다음으로 추출합니다. `mboxSession` 매개 변수:

```swift
Target.getSessionId { (id, err) in
    // read Target sessionId
}
```

## 웹 보기에서 테스트

웹 미리 보기 링크는 [!UICONTROL 활동 세부 사항] 을 클릭하여 페이지 만들기 [[!UICONTROL ADOBE QA] 링크](/help/dev/implement/mobile/target-mobile-preview.md) 각 경험 미리 보기 링크를 복사하는 팝업을 표시하려면 다음과 같이 하십시오.

```
?at_preview_token=mhFIzJSF7JWb-RsnakpBqi_s83Sl64hZp928VWpkwvI&at_preview_index=1_1&at_preview_listed_activities_only=true
```

웹 미리 보기 링크에 추가 기능 포함 `at_preview_index` 및 `at_preview_listed_activities_only` 매개 변수. 이러한 매개 변수를 복사하여 웹 링크 매개 변수를 사용하여 모바일 친화적인 미리 보기 링크를 구성합니다.

예:

```
com.adobe.targetmobile://?at_preview_token=mhFIzJSF7JWb-RsnakpBqhBwj-TiIlZsRTx_1QQuiXLIJFdpSLeEZwKGPUyy57O_&at_preview_index=1_1&at_preview_listed_activities_only=true
```

iOS Safari 브라우저에서 링크를 열면 앱에서 URL을 캡처합니다 `AppDelegate` 다음 예제와 유사한 클래스:

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
