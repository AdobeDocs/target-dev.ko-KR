---
keywords: at.js, 브라우저 사용자 에이전트, 사용자 에이전트, 클라이언트 힌트, 사용자 에이전트
description: Adobe Target이 사용자 에이전트 및 클라이언트 힌트를 사용하여 방문자를 세그먼테이션 및 개인 맞춤화에 적합하게 만드는 방법에 대해 알아보십시오.
title: 사용자 에이전트 및 클라이언트 힌트
feature: at.js
exl-id: e0d87d95-ee95-4ca9-8632-222ae1fb9a91
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1208'
ht-degree: 74%

---

# 사용자 에이전트 및 클라이언트 힌트

Adobe Target은 사용자 에이전트를 사용하여 방문자를 세그먼테이션 및 개인 맞춤화할 수 있도록 합니다.

>[!NOTE]
>
>이 문서의 정보는 [at.js 버전 2.9.0](target-atjs-versions.md) 이상의 버전에 적용됩니다.

웹 브라우저가 서버에 요청할 때마다 브라우저 및 브라우저가 실행되는 환경에 대한 정보가 요청 헤더에 포함됩니다. 인터넷 초기부터 이 데이터는 사용자 에이전트라는 단일 문자열로 집계되었습니다.

다음 텍스트는 Safari 브라우저를 사용하는 Mac OS X 기반 컴퓨터의 샘플 사용자 에이전트입니다.

```
Mozilla/5.0 (Linux; Android 12; SM-S908E) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.41 Mobile Safari/537.36 
```

이 사용자 에이전트에서 요청을 수신하는 서버는 브라우저 및 운영 체제에 대한 다음 정보를 식별할 수 있습니다.

| 정보 | 세부 사항 |
| --- | --- |
| 소프트웨어 이름 | Chrome |
| 소프트웨어 버전 | 101 |
| 전체 소프트웨어 버전 | 101.0.4951.41 |
| 레이아웃 엔진 이름 | AppleWebKit |
| 레이아웃 엔진 버전 | 537.36 |
| 운영 체제 | Android |
| 운영 체제 버전 | Android 12 (Snow Cone) |
| 디바이스 | SM-S908E (Samsung Galaxy S22 Ultra) |

수년에 걸쳐 사용자 에이전트 문자열에 포함된 브라우저 및 디바이스 정보의 양이 증가했습니다.

## 사용자 에이전트 사용 사례

사용자 에이전트는 오랫동안 마케팅 및 개발자 팀에 브라우저, 운영 체제 및 장치가 사이트 콘텐츠를 표시하는 방법과 더불어 사용자가 웹 사이트와 상호 작용하는 방법에 대한 중요한 통찰력을 제공하는 데 사용되었습니다. 사용자 에이전트는 스팸을 차단하고 다양한 추가 목적을 위해 사이트를 크롤링하는 봇을 필터링하는 데에도 사용됩니다.

그러나 최근 몇 년 동안 일부 사이트 소유자와 마케팅 공급업체는 사용자 에이전트를 요청 헤더에 포함된 다른 정보와 함께 사용하여 사용자 모르게 사용자를 식별하는 수단으로 사용할 수 있는 전자 개인정보 기능을 생성했습니다. 사용자 에이전트가 사이트 소유자에게 제공하는 중요한 목적에도 불구하고 브라우저 개발진은 사이트 방문자의 잠재적인 개인정보 보호 문제를 제한하기 위해 사용자 에이전트 작동 방식을 변경하기로 결정했습니다.

브라우저 개발자는 이 문제를 해결하기 위한 솔루션으로 사용자 에이전트 클라이언트 힌트를 만들었습니다. 클라이언트 힌트를 사용하면 사이트에서 필요한 브라우저, 운영 체제 및 디바이스 정보를 수집하는 동시에 지문 작업과 같은 은밀한 추적 방법에 대한 보호를 강화할 수 있습니다.

## 클라이언트 힌트

사용자 에이전트 클라이언트 힌트는 웹 사이트 소유자에게 사용자 에이전트에서 사용 가능한 동일한 정보의 대부분에 액세스할 수 있는 기능을 제공하지만 보다 개인정보 보호에 특화되었습니다. 최신 브라우저가 사용자 에이전트를 웹 서버에 보낼 때 전체 사용자 에이전트는 필요 여부에 관계없이 모든 요청에 대해 전송됩니다. 반면에 클라이언트 힌트는 서버가 클라이언트에 대해 알고자 하는 추가 정보를 브라우저에 요청해야 하는 모델을 시행합니다. 이 요청을 수신하면 브라우저는 자체 정책 또는 사용자 구성을 적용하여 반환되는 데이터를 결정할 수 있습니다. 이제 모든 요청에 대해 기본적으로 전체 사용자 에이전트를 노출하는 대신 액세스가 명시적이고 감사 가능한 방식으로 관리됩니다.

사용자 에이전트 클라이언트 힌트는 버전 89부터 Chrome에서 사용할 수 있습니다. Microsoft Edge, Opera, Brave, Chrome Android, Opera Android 및 Samsung Internet과 같은 최신 버전의 Chromium 기반 브라우저도 Client Hints API를 지원합니다.

브라우저가 웹 서버에 보낸 첫 번째 요청의 헤더에 포함된 클라이언트 힌트에는 브라우저 브랜드, 브라우저의 주요 버전 및 클라이언트가 모바일 디바이스인지 여부에 대한 표시기가 포함됩니다. 각 데이터 조각에는 단일 사용자 에이전트 문자열로 그룹화되지 않고 고유한 헤더 값이 있습니다.

예를 들어 몇 가지 클라이언트 힌트는 다음과 같습니다.

```
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99" 
Sec-CH-UA-Mobile: ?0 
Sec-CH-UA-Platform: "macOS"
```

...이지만 동일한 브라우저의 사용자 에이전트입니다.

```
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36 
```

정보는 비슷하지만 서버에 대한 첫 번째 요청에는 사용자 에이전트 문자열에서 사용할 수 있는 항목의 하위 집합만 포함하는 클라이언트 힌트가 포함되어 있습니다. 요청에서 누락된 사항은 OS 아키텍처, 전체 OS 버전, 레이아웃 엔진 이름, 레이아웃 엔진 버전 및 전체 브라우저 버전입니다. 그러나 후속 요청에서 Client Hint API는 웹 서버 디바이스에 대한 높은 엔트로피 수준의 세부 정보를 추가로 요청할 수 있도록 합니다. 이러한 높은 엔트로피 값이 요청되면 브라우저 정책 또는 사용자 설정에 따라 브라우저 응답에 해당 정보가 포함될 수 있습니다.

다음 예제는 높은 엔트로피 값이 요청될 때 Client Hints API에서 반환되는 JSON 오브젝트입니다.

```
{ 

    "architecture":"x86", 
    "bitness":"64", 
    "brands":[ 
        { 
            "brand":" Not A;Brand", 
            "version":"99" 
        }, 
        { 
            "brand":"Chromium", 
            "version":"100" 
        }, 
        { 
            "brand":"Google Chrome", 
            "version":"100" 
        } 
    ], 
    "fullVersionList":[ 
        { 
            "brand":" Not A;Brand", 
            "version":"99.0.0.0" 
        }, 
        { 
            "brand":"Chromium", 
            "version":"100.0.4896.127" 
        }, 
        { 
            "brand":"Google Chrome", 
            "version":"100.0.4896.127" 
        } 
    ], 
    "mobile":false, 
    "model":"", 
    "platformVersion":"12.2.1" 
} 
```

높은 엔트로피 값에는 기본 클라이언트 힌트 정보에서 사용할 수 없는 몇 가지 추가 정보가 포함됩니다. 다음 표에는 기본 요청과 높은 엔트로피 사용자 에이전트 클라이언트 힌트 정보에서 사용할 수 있는 데이터에 대한 세부 정보가 포함되어 있습니다.

| HTTP 헤더 | JavaScript | 사용자 에이전트 | 클라이언트 힌트 | 높은 엔트로피 클라이언트 힌트 |
| --- | --- | --- | --- | --- |
| Sec-CH-UA | 브랜드 | 예 | 예 | 아니요 |
| Sec-CH-UA-Platform | 플랫폼 | 예 | 예 | 아니요 |
| Sec-CH-UA-Mobile | 모바일 | 예 | 예 | 아니요 |
| Sec-CH-UA-Platform-Version | platformVersion | 예 | 아니요 | 예 |
| Sec-CH-UA-Arch | 아키텍처 | 예 | 아니요 | 예 |
| Sec-CH-UA-Model | 모델 | 예 | 아니요 | 예 |
| Sec-CH-UA-Bitness | 비트니스 | 예 | 아니요 | 예 |
| Sec-CH-UA-Full-Version-List | fullVersionList | 예 | 아니요 | 예 |

## 클라이언트 힌트로 마이그레이션

현재 Chromium 기반 브라우저는 웹 서버에 대한 요청 헤더에 클라이언트 힌트와 함께 사용자 에이전트를 계속 전송합니다. 그러나 2022년 4월부터 2023년 2월까지 계속해서 사용자 에이전트 문자열에 포함된 데이터의 양이 줄어듭니다. Safari 및 Firefox와 같은 다른 브라우저는 계속 사용자 에이전트 문자열을 활용합니다. 그러나 해당 브라우저 역시 문자열에 포함된 정보의 양을 줄일 것입니다.

## 클라이언트 힌트가 필요한 Target 사용 사례

Target의 다음 사용 사례에는 클라이언트 힌트가 필요합니다.

### 대상 속성

Target 대상을 사용하며 다음 대상 속성 중 하나를 사용하는 경우, Target에서 올바른 세분화를 수행하려면 클라이언트 힌트가 필요합니다.

* 브라우저
* 운영 체제
* 모바일

### 프로필 스크립트

프로필 스크립트를 사용하고 `user.browser` 속성(사용자 에이전트 참조)을 참조하는 경우 하나 이상의 클라이언트 힌트도 확인하도록 프로필 스크립트를 업데이트해야 할 수 있습니다. 함수 `user.clientHint('sec-ch-ua-xxxxx')`를 사용하여 클라이언트 힌트에 액세스할 수 있습니다. 클라이언트 힌트 헤더 이름은 모두 소문자여야 합니다.

다음 예제는 프로필 스크립트에서 Windows OS를 올바르게 감지하는 방법을 보여 줍니다.

```
"return (((user.browser != null) && (user.browser.indexOf(\"Windows\") > -1)) || " + 
      "((user.clientHint('sec-ch-ua-platform') != null) && 
(user.clientHint('sec-ch-ua-platform') === 'Windows')));" 
```

다음은 클라이언트 힌트 및 해당 프로필 스크립트 사용 의미 체계의 표입니다.

| 클라이언트 힌트 헤더 | 엔트로피 | 대상 속성 | 프로필 스크립트 사용 |
| --- | --- | --- | --- |
| [Sec-CH-UA](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA) | 낮음 | 브라우저 | `user.clientHint('sec-ch-ua')` |
| [Sec-CH-UA-Arch](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Arch) | 높음 | 프로필 스크립트를 통해 사용자에게 노출됨 | `user.clientHint('sec-ch-ua-arch')` |
| [Sec-CH-UA-Bitness](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Bitness) | 높음 | 프로필 스크립트를 통해 사용자에게 노출됨 | `user.clientHint('sec-ch-ua-bitness')` |
| [Sec-CH-UA-Full-Version-List](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Full-Version-List) | 높음 | 브라우저 | `user.clientHint('sec-ch-ua-full-version-list')` |
| [Sec-CH-UA-Mobile](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Mobile) | 낮음 | 모바일 | `user.clientHint('sec-ch-ua-mobile')` |
| [Sec-CH-UA-Model](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Model) | 높음 | 모바일 | `user.clientHint('sec-ch-ua-model')` |
| [Sec-CH-UA-Platform](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Platform) | 낮음 | 운영 체제 | `user.clientHint('sec-ch-ua-platform')` |
| [Sec-CH-UA-Platform-Version](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Platform-Version) | 높음 | 프로필 스크립트를 통해 사용자에게 노출됨 | `user.clientHint('sec-ch-ua-platform-version')` |

## Adobe Target에 클라이언트 힌트를 전달하는 방법

다음 섹션에는 Target 구현에 따라 클라이언트 힌트를 전달하는 방법에 대한 자세한 정보가 포함되어 있습니다.

### at.js 버전 2.9.0 이상

at.js 2.9.0부터 사용자 에이전트 클라이언트 힌트는 브라우저에서 자동으로 수집되어 다음과 같은 경우 Target으로 전송됩니다 `getOffer/getOffers()` 이(가) 호출되었습니다. 기본적으로 at.js는 “낮은 엔트로피” 클라이언트 힌트만 수집합니다. 이전 섹션에서 “높은 엔트로피”로 분류된 데이터를 기반으로 잠재고객 세분화를 수행하거나 프로필 스크립트를 사용하는 경우 at.js를 구성하여 `targetGlobalSettings`를 통해 브라우저에서 “높은 엔트로피” 클라이언트 힌트를 수집해야 합니다.

```
window.targetGlobalSettings = { allowHighEntropyClientHints: true };
```

### 서버측 SDK

서버측 SDK를 통해 클라이언트 힌트를 전달하는 방법에 대한 자세한 내용은 다음을 참조하십시오. [클라이언트 힌트](../../server-side/sdk-guides/core-principles/audience-targeting.md#client-hints) 을 참조하십시오.
