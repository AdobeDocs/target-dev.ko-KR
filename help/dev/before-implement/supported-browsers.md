---
keywords: 브라우저, 사전 요구 사항, 요구 사항, internet explorer, chrome, firefox, safari, android, surface, Browsers0
description: ' [!DNL Adobe Target] 이(가) 인터페이스 및 콘텐츠 전달을 위해 지원하는 인터넷 브라우저를 알아봅니다.'
title: ' [!DNL Target] 이(가) 지원하는 브라우저는 무엇입니까?'
feature: Implementation
exl-id: 1d778e14-26b0-477b-ac28-d304db70a133
source-git-commit: f194c6de43070443b78c9a69b4233c27d70b8858
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 23%

---

# 지원되는 브라우저

[!DNL Adobe Target] 애플리케이션 및 콘텐츠 전달은 광범위한 브라우저 및 장치에서 테스트되었습니다.

TLS에 대한 자세한 내용은 [TLS(전송 계층 보안) 암호화 변경 사항](tls-transport-layer-security-encryption.md)을 참조하십시오.

## [!DNL Target] Standard/Premium 인터페이스

[!DNL Target] 인터페이스는 다음 브라우저 및 장치를 지원합니다.

| 장치 유형 | 브라우저 버전 |
|--- |--- |
| Windows | <ul><li>Microsoft Edge</li><li>Google Chrome (최신, 최신 마이너스 1)</li><li>Mozilla Firefox (최신, 최신 마이너스 1)</li></ul> |
| Mac | <ul><li>Firefox(최신, 최신 마이너스 1)</li><li>Chrome (최신, 최신 마이너스 1)</li></ul> |

## 콘텐츠 전달

콘텐츠 전달은 다음 브라우저 및 장치에서 테스트되었습니다.

| 장치 유형 | 브라우저 버전 |
|--- |--- |
| Windows | <ul><li>Microsoft Internet Explorer 9 및 10. 에뮬레이션 모드에서 테스트되었습니다. **참고**: IE 9의 콘텐츠 전달은 더 이상 at.js 1.3.0 이상에서 지원되지 않습니다. IE 10, 11 및 모든 이전 버전의 콘텐츠 전달은 더 이상 at.js 2.5.0 이상에서 지원되지 않습니다.</li><li>Internet Explorer 11. **참고**: IE 10, 11 및 모든 이전 버전의 콘텐츠 전달은 더 이상 at.js 2.5.0 이상에서 지원되지 않습니다.</li><li>Microsoft Edge</li><li>Chrome (최신, 최신 마이너스 1)</li><li>Firefox(최신, 최신 마이너스 1)</li></ul> |
| Mac | <ul><li>Apple Safari(최신) **참고**: Safari가 퍼스트 파티 및 타사 쿠키를 처리하는 방법에 대한 자세한 내용은 [Target 쿠키](../implement/client-side/atjs/atjs-cookies.md)를 참조하십시오.</li><li>Firefox(최신, 최신 마이너스 1)</li><li>Chrome (최신, 최신 마이너스 1)</li></ul> |
| 모바일/태블릿 | <ul><li>Apple iOS(최신)</li><li>Android 장치 및 태블릿(Android 4 이상)</li><li>Microsoft Surface(Windows 8.1)</li></ul> |

다음을 참고하십시오.

* [!DNL Adobe Experience Platform Web SDK]은(는) [!DNL Google Chrome], [!DNL Safari], [!DNL Firefox] 및 [!DNL Microsoft Edge Chromium]의 최신 버전에서 최적으로 작동하도록 디자인되었습니다. 이러한 브라우저의 이전 버전 또는 사용되지 않는 브라우저(예: [!DNL Internet Explorer])에서 특정 기능을 사용하는 데 문제가 있을 수 있습니다.
* at.js 구현의 경우 [!DNL Target]은(는) Internet Explorer 이전 버전 및 위에 나열된 브라우저의 이전 버전에서 기본 콘텐츠를 표시합니다.
* Internet Explorer에서는 알 수 없는 모든 요소(예: 사용자 지정 요소)를 동일한 요소 유형으로 처리합니다. 따라서 게재는 사용자 지정 요소에서 작동하지 않습니다.
* [!DNL Target]은(는) 위 목록에 없는 브라우저와 [quirks 모드](https://en.wikipedia.org/wiki/Quirks_mode)를 사용하는 브라우저에는 기본 콘텐츠를 표시합니다. at.js에는 표준 모드에서 렌더링되는 문서 형식(예: `<!DOCTYPE html>`)이 필요합니다.
* [!DNL Adobe] 배달 인프라가 2018년 9월 12일 이후에 TLS 1.0 장치 및 브라우저를 지원하지 않도록 보호됩니다. 이러한 변경의 전반적 영향에 대해 이해하려면 [TLS(전송 계층 보안) 암호화 변경 사항](../before-implement/tls-transport-layer-security-encryption.md)을 참조하십시오.
