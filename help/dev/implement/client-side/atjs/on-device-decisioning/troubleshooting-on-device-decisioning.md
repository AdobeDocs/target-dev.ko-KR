---
keywords: 구현, javascript 라이브러리, js, atjs, 온디바이스 의사 결정, 온디바이스 의사 결정, at.js, 온디바이스, 온디바이스, 문제 해결, 문제 해결, 구현2
description: at.js 라이브러리를 사용하여 [!UICONTROL on-device decisioning] 문제를 해결하는 방법을 알아봅니다.
title: at.js JavaScript 라이브러리를 사용하여 온디바이스 의사 결정 문제를 해결하려면 어떻게 합니까?
feature: at.js
exl-id: b9530cc7-5e83-4fdf-bde9-b2492e0861ff
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# at.js에 대한 [!UICONTROL on-device decisioning] 문제 해결

at.js JavaScript 라이브러리를 사용하여 [!UICONTROL Adobe Target]의 [!UICONTROL on-device decisioning] 문제를 해결하려면 다음 단계를 완료하십시오.

## 1단계: at.js에 대한 콘솔 로그 활성화

URL 매개 변수 `mboxDebug=1`을(를) 추가하면 at.js가 브라우저의 콘솔에서 메시지를 인쇄할 수 있습니다.

모든 메시지에는 편리한 개요를 위해 접두사 &quot;AT:&quot;가 들어 있습니다. 아티팩트가 성공적으로 로드되었는지 확인하려면 콘솔 로그에 다음과 유사한 메시지가 포함되어야 합니다.

```
AT: LD.ArtifactProvider fetching artifact - https://assets.adobetarget.com/your-client-cide/production/v1/rules.json
AT: LD.ArtifactProvider artifact received - status=200
```

다음 그림은 콘솔 로그에 이러한 메시지를 보여줍니다.

이미지 를 클릭하여 전체 너비로 확장합니다.

![아티팩트 메시지가 포함된 콘솔 로그](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/browser-console.png "아티팩트 메시지가 포함된 콘솔 로그"){zoomable="yes"}

## 2단계: 브라우저의 네트워크 탭에서 규칙 아티팩트 다운로드 확인

브라우저의 네트워크 탭을 엽니다.

예를 들어 Google Chrome에서 DevTools를 열려면 다음을 수행합니다.

1. Ctrl+Shift+J(Windows) 또는 Command+Option+J(Mac)를 누릅니다.
1. 네트워크 탭으로 이동합니다.
1. 키워드 &quot;rules.json&quot;으로 호출을 필터링하여 아티팩트 규칙 파일만 표시되도록 합니다.

   또한 &quot;/delivery|rules.json/&quot;별로 필터링하여 모든 Target 호출 및 아티팩트 rules.json을 표시할 수 있습니다.

   Google Chrome의 ![네트워크 탭](assets/rule-json.png)

## 3단계: at.js 사용자 지정 이벤트를 사용하여 규칙 아티팩트 다운로드 확인

at.js 라이브러리는 [!UICONTROL on-device decisioning]을(를) 지원하도록 두 개의 새로운 사용자 지정 이벤트를 전달합니다.

* `adobe.target.event.ARTIFACT_DOWNLOAD_SUCCEEDED`
* `adobe.target.event.ARTIFACT_DOWNLOAD_FAILED`

가입하면 애플리케이션에서 이러한 사용자 지정 이벤트를 수신하여 아티팩트 규칙 파일 다운로드의 성공 또는 실패 시 작업을 수행할 수 있습니다.

다음 예제는 아티팩트 다운로드 성공 및 실패 이벤트를 수신하는 코드 샘플을 보여 줍니다.

```javascript {line-numbers="true"}
document.addEventListener(adobe.target.event.ARTIFACT_DOWNLOAD_SUCCEEDED, function(e) { 
  console.log("Artifact successfully downloaded", e.detail);
}, false);

document.addEventListener(adobe.target.event.ARTIFACT_DOWNLOAD_FAILED, function(e) { 
  console.log("Artifact failed to download", e.detail);
}, false);
```
