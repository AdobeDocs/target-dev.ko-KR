---
keywords: 구현, javascript 라이브러리, js, atjs, 온디바이스 의사 결정, 온디바이스 의사 결정, 지원되는 기능, $8
description: 지원되는 기능 알아보기 [!UICONTROL 온디바이스 의사 결정].
title: 온디바이스 의사 결정에서 지원되는 기능
feature: at.js
exl-id: bdd65658-6c4a-41ae-a222-59c00a11bdac
source-git-commit: 79ffa3f58d780f587fe1202b82d3860395504dfe
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 10%

---

# 에 대해 지원되는 기능 [!UICONTROL 온디바이스 의사 결정]

다음 [!DNL Adobe Target] JS SDK는 고객이 의사 결정을 위해 데이터의 성능과 신선도 중에서 선택할 수 있는 유연성을 제공합니다. 즉, 머신 러닝을 통해 가장 관련성이 높고 매력적인 개인화된 콘텐츠를 전달하는 것이 가장 중요한 경우 라이브 서버 호출을 수행해야 합니다. 그러나 성능이 더 중요한 경우에는 온디바이스 및 인메모리 결정을 내려야 합니다. 대상 [!UICONTROL 온디바이스 의사 결정] 작동하려면 지원되는 기능을 나열하는 다음 섹션을 참조하십시오.

## 지원되는 활동 유형

다음 표는 다음 항목을 나타냅니다. [활동 유형](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) 작성자: [양식 기반 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) 또는 [시각적 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC)는에 대해 지원되거나 지원되지 않습니다. [!UICONTROL 온디바이스 의사 결정].

| 활동 유형 | 지원됨? |
| --- | --- |
| [A/B 테스트](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html) | 예 |
| [자동 할당](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | 아니오 |
| [자동 타깃팅](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) ![프리미엄](../../../assets/premium.png) | 아니요 |
| [다변량 테스트](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html) (MVT) | 아니요 |
| [경험 타겟팅](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html) (XT) | 예 |
| [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) ![Premium](../../../assets/premium.png) | 아니오 |
| [권장 사항](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html) ![프리미엄](../../../assets/premium.png) | 아니요 |
| [Analytics for Target을 사용하는 활동](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?) (A4T) | 예 |

## 대상 타기팅

다음 표는 지원되거나 지원되지 않는 대상 규칙을 나타냅니다. [!UICONTROL 온디바이스 의사 결정].

| 대상 규칙 | 지원됨? |
| --- | --- |
| [지역](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | 예<P>온디바이스 의사 결정을 사용할 때 지원되는 지역 속성은 다음과 같습니다.<ul><li>국가/지역</li><li>구/군/시</li><li>위도</li><li>경도</li></ul> |
| [네트워크](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | 아니요 |
| [모바일](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | 아니요 |
| [사용자 정의 매개변수](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | 예 |
| [운영 체제](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | 예 |
| [사이트 페이지](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | 예 |
| [브라우저](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | 예 |
| [방문자 프로필](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | 아니요 |
| [트래픽 소스](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | 아니요 |
| [시간대](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | 예 |
| Adobe Experience Cloud 대상<P>([!DNL Audiences from Adobe Analytics], [!DNL Adobe Audience Manager], 및 [!DNL Adobe Experience Manager]) | 아니요 |

### 에 대한 지역 타깃팅 [!UICONTROL 온디바이스 의사 결정]

에 대한 최소 지연 유지 [!UICONTROL 온디바이스 의사 결정] Adobe 지리 기반 대상이 있는 활동에서는 호출에 지리 값을 직접 제공할 것을 권장합니다. [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md). 요청의 컨텍스트에서 지역 개체를 설정합니다. 즉, 브라우저에서 각 방문자의 위치를 결정하는 방법입니다. 예를 들어 구성한 서비스를 사용하여 IP-to-Geo 조회를 수행할 수 있습니다. Google Cloud와 같은 일부 호스팅 공급자는 각 의 사용자 지정 헤더를 통해 이 기능을 제공합니다 `HttpServletRequest`.

```javascript {line-numbers="true"}
window.adobe.target.getOffers({ 
    decisioningMethod: "on-device", 
    request: { 
        context: { 
            geo: { 
                city: "SAN FRANCISCO", 
                countryCode: "US", 
                stateCode: "CA", 
                latitude: 37.75, 
                longitude: -122.4 
            } 
        }, 
        execute: { 
            pageLoad: {} 
        } 
    } 
})
```

그러나 서버에서 IP-to-Geo 조회를 수행할 수 없지만 계속 수행하려는 경우 [!UICONTROL 온디바이스 의사 결정] 대상 [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md) 지역 기반 대상자를 포함하는 요청도 지원됩니다. 이 접근 방식의 단점은 원격 IP-to-Geo 조회를 사용한다는 것입니다. 이 조회는 각 IP에 지연 시간을 추가합니다 `getOffers` 호출합니다. 이 지연은 1보다 작아야 합니다. `getOffers` 서버 근처에 있는 CDN에 도달하므로 서버측 의사 결정을 사용하여 를 호출합니다. SDK에 대한 요청의 컨텍스트에서 지역 개체에 &quot;ipAddress&quot; 필드만 제공하여 방문자 IP 주소의 지역 위치를 검색합니다. &quot;ipAddress&quot; 이외의 다른 필드가 제공된 경우 [!DNL Target] SDK는 확인을 위해 지리적 위치 메타데이터를 가져오지 않습니다.

```javascript {line-numbers="true"}
window.adobe.target.getOffers({ 
    decisioningMethod: "on-device", 
    request: { 
        context: { 
            geo: { 
                ipAddress: "127.0.0.1" 
            } 
        }, 
        execute: { 
            pageLoad: {} 
        } 
    } 
})
```

### 할당 방법

다음 표는 지원되는 할당 방법과 지원되지 않는 할당 방법을 보여 줍니다 [!UICONTROL 온디바이스 의사 결정].

| 할당 방법 | 지원됨? |
| --- | --- |
| 수동 | 예 |
| [최고 경험에 자동 할당](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | 아니요 |
| [개인화된 경험에 대한 자동 타겟](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) | 아니요 |
