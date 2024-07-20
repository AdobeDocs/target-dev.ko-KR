---
keywords: 허용 목록에 추가하다 콘텐츠 보안 정책, csp.js, 허용 목록, 플리커, 사전 숨기기, 사전 숨기기, 콘텐츠 보안 정책, iFrame, iframe
description: ' [!DNL Adobe Target]을(를) 사용할 때 추가해야 하는 콘텐츠 보안 정책(CSP) 지침에 대해 알아봅니다.'
title: ' [!DNL Target] 은 콘텐츠 보안 정책(CSP)을 어떻게 처리합니까?'
feature: Privacy & Security
exl-id: ec6942e5-36d8-4f88-b3d6-47f9eaca03a8
source-git-commit: c43c79b29768694eac534e22047b5ee6a3d0ccd5
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 28%

---

# 콘텐츠 보안 정책(CSP) 지침

[!DNL Adobe Target] 구현에 [콘텐츠 보안 정책](https://ko.wikipedia.org/wiki/Content_Security_Policy)(CSP)을 사용하는 경우 [at.js 2.1 이상 버전](../../implement/client-side/atjs/target-atjs-versions.md)을 사용할 때 다음과 같은 CSP 지침을 추가해야 합니다.

* `*.tt.omtrdc.net` 허용 목록이 포함된 `connect-src` [!DNL Target] 에지로의 네트워크 요청을 수락하기 위해 필요합니다.
* `style-src unsafe-inline` 사전 숨기기 및 플리커 제어에 필요합니다.
* `script-src unsafe-inline`. HTML 오퍼의 일부일 수 있는 JavaScript 실행을 허용하기 위해 필요합니다.

## 자주 묻는 질문 (FAQ)

보안 정책에 대한 다음 FAQ를 참조하십시오.

### CORS(원본 간 리소스 공유) 및 Flash 도메인 간 정책에 보안 문제가 있습니까?

CORS 정책을 구현하는 권장 방법은 신뢰할 수 있는 도메인의 허용 목록을 통해 필요한 신뢰할 수 있는 출처에만 액세스할 수 있도록 허용하는 것입니다. Flash 도메인 간 정책에 대해서도 마찬가지입니다. 일부 [!DNL Target] 고객은 Target의 도메인에 와일드카드 문자를 사용하는 것에 대해 우려하고 있습니다. 우려되는 점은 사용자가 애플리케이션에 로그인하여 정책이 허용하는 도메인을 방문하는 경우 해당 도메인에서 실행 중인 모든 악성 콘텐츠가 애플리케이션에서 민감한 콘텐츠를 검색하고 로그인한 사용자의 보안 컨텍스트에서 작업을 수행할 가능성이 있다는 것입니다. 이러한 상황을 일반적으로 CSRF(크로스 사이트 요청 위조)라고 합니다.

그러나 [!DNL Target] 구현에서는 이러한 정책이 보안 문제를 나타내서는 안 됩니다.

“adobe.tt.omtrdc.net”은 Adobe 소유 도메인입니다. [!DNL Adobe Target]은 테스트 및 개인화 도구이며 [!DNL Target]은 인증 없이 어디에서나 요청을 수신하고 처리할 수 있습니다. 이러한 요청에는 A/B 테스트, 권장 사항 또는 콘텐츠 개인화에 사용되는 키/값 쌍이 포함되어 있습니다.

Adobe은 &quot;adobe.tt.omtrdc.net&quot;이 가리키는 [!DNL Adobe Target] 에지 서버에 PII(개인 식별 정보) 또는 기타 민감한 정보를 저장하지 않습니다.

JavaScript 호출을 통해 모든 도메인에서 [!DNL Target]에 액세스할 수 있습니다. 이 액세스를 허용하는 유일한 방법은 와일드 카드로 &quot;Access-Control-Allow-Origin&quot;을 적용하는 것입니다.

### 내 사이트가 외부 도메인에 iFrame으로 임베드되는 것을 허용하거나 방지하려면 어떻게 해야 합니까?

[시각적 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html){target=_blank}(VEC)가 웹 사이트를 iFrame에 포함할 수 있도록 하려면 웹 서버 설정에서 CSP(설정된 경우)를 변경해야 합니다. [!DNL Adobe] 도메인은 화이트리스트에 추가하고 구성해야 합니다.

보안상의 이유로 사이트가 외부 도메인 아래에 iFrame으로 포함되지 않도록 하려는 경우

다음 섹션에서는 VEC가 iFrame에 사이트를 포함하도록 허용하거나 금지하는 방법에 대해 설명합니다.

#### VEC가 사이트를 iFrame에 포함할 수 있도록 허용

VEC가 웹 사이트를 iFrame에 포함할 수 있도록 하는 가장 쉬운 방법은 가장 광범위한 와일드카드인 `*.adobe.com`을(를) 허용하는 것입니다.

예:

`Content-Security-Policy: frame-ancestors 'self' *.adobe.com`

다음 그림에서와 같이(확대하려면 클릭):


가장 넓은 와일드카드가 있는 ![CSP](/help/dev/before-implement/privacy/assets/csp-adobe.png){width="600" zoomable="yes"}

실제 [!DNL Adobe] 서비스만 허용할 수 있습니다. 이 시나리오는 `*.experiencecloud.adobe.com + https://experiencecloud.adobe.com`을(를) 사용하여 달성할 수 있습니다.

예:

`Content-Security-Policy: frame-ancestors 'self' https://*.experiencecloud.adobe.com https://experiencecloud.adobe.com https://experience.adobe.com`

다음 그림에서와 같이(확대하려면 클릭):

![ExperienceCloud의 CSP 범위](/help/dev/before-implement/privacy/assets/csp-experiencecloud.png){width="600" zoomable="yes"}

`https://<Client Code>.experiencecloud.adobe.com https://experience.adobe.com`을(를) 사용하여 회사 계정에 가장 제한적인 액세스를 수행할 수 있습니다. 여기서 `<Client Code>`은(는) 특정 클라이언트 코드를 나타냅니다.

예:

`Content-Security-Policy: frame-ancestors 'self'  https://ags118.experiencecloud.adobe.com https://experience.adobe.com`

다음 그림에서와 같이(확대하려면 클릭):

![클라이언트 코드 범위가 지정된 CSP](/help/dev/before-implement/privacy/assets/csp-clientcode.png){width="600" zoomable="yes"}

>[!NOTE]
>
>[Launch/Tag](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md)을(를) 구현한 경우 잠금 해제해야 합니다.
>
>예:
>
> `Content-Security-Policy: frame-ancestors 'self' *.adobe.com *.assets.adobedtm.com;`

#### VEC가 사이트를 iFrame에 포함하지 못하도록 합니다.

VEC가 사이트를 iFrame에 포함할 수 없도록 &quot;자체&quot;로만 제한할 수 있습니다.

예:

`Content-Security-Policy: frame-ancestors 'self'`

다음 그림에 표시된 대로(확대하려면 클릭):

![CSP 오류](/help/dev/before-implement/privacy/assets/csp-error.png){width="600" zoomable="yes"}

다음과 같은 오류 메시지가 표시됩니다.

`Refused to frame 'https://kuehl.local/' because an ancestor violates the following Content Security Policy directive: "frame-ancestors 'self'".`

