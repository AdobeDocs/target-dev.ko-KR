---
title: 온디바이스 의사 결정에서 지원되는 기능은 무엇입니까?
description: 라이브 서버 호출을 사용하여 머신 러닝을 통해 가장 관련성이 높고 매력적인 개인화된 콘텐츠를 전달하는 방법을 알아봅니다.
feature: APIs/SDKs
exl-id: 15d9870f-6c58-4da0-bfe5-ef23daf7d273
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 10%

---

# 지원되는 기능 개요

[!DNL Adobe Target]의 서버측 SDK는 개발자가 의사 결정을 위해 데이터의 성능과 최신 상태 중에서 선택할 수 있는 유연성을 제공합니다. 즉, 머신 러닝을 통해 가장 관련성이 높고 매력적인 개인화된 콘텐츠를 전달하는 것이 가장 중요한 경우 라이브 서버 호출을 수행해야 합니다. 그러나 성능이 더 중요한 경우에는 디바이스에서 결정을 내려야 합니다. 대상 [!UICONTROL 온디바이스 의사 결정] 작동하는 데 필요한 기능은 다음 목록을 참조하십시오.

* 활동 유형
* 대상 타기팅
* 할당 방법

## 활동 유형

다음 표는 다음 항목을 나타냅니다. [활동 유형](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) 을(를) 사용하여 생성됨 [양식 기반 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?) 다음에 대해 지원되거나 지원되지 않음: [!UICONTROL 온디바이스 의사 결정].

| 활동 유형 | 지원됨 |
| --- | --- |
| [A/B 테스트](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html) | 예 |
| [자동 할당](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | 아니오 |
| [자동 타깃팅](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) | 아니오 |
| [Analytics for Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) (A4T) | 예 |
| [다변량 테스트](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html) (MVT) | 아니요 |
| [경험 타겟팅](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html) (XT) | 예 |
| [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) (AP) | 아니오 |
| [권장 사항](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html) | 아니오 |


## 대상 타기팅

다음 표는 지원되거나 지원되지 않는 대상 규칙을 나타냅니다. [!UICONTROL 온디바이스 의사 결정].

| 대상 규칙 | 온디바이스 의사 결정 |
| --- | --- |
| [지역](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | 예 |
| [네트워크](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | 아니요 |
| [모바일](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | 아니요 |
| [사용자 지정 매개 변수](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | 예 |
| [운영 체제](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | 예 |
| [사이트 페이지](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | 예 |
| [브라우저](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | 예 |
| [방문자 프로필](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | 아니요 |
| [트래픽 소스](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | 아니요 |
| [시간대](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | 예 |
| [Experience Cloud 대상](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html) (Adobe Audience Manager, Adobe Analytics 및 Adobe Experience Manager의 대상 | 아니요 |

### 에 대한 지역 타깃팅 [!UICONTROL 온디바이스 의사 결정]

에 대해 지연 시간이 거의 0에 가깝게 유지 [!UICONTROL 온디바이스 의사 결정] Adobe 지리 기반 대상이 있는 활동에서는 호출에 지리 값을 직접 제공할 것을 권장합니다. `getOffers`. 다음을 설정하여 이 작업을 수행합니다. `Geo` 의 오브젝트 `Context` 요청. 즉, 서버에서 각 최종 사용자의 위치를 확인하는 방법이 필요합니다. 예를 들어 서버는 사용자가 구성하는 서비스를 사용하여 IP-to-Geo 조회를 수행할 수 있습니다. Google Cloud와 같은 일부 호스팅 공급자는 각 의 사용자 지정 헤더를 통해 이 기능을 제공합니다 `HttpServletRequest`.

>[!BEGINTABS]

>[!TAB Node.js]

```csharp {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    decisioningMethod: "on-device"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
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

>[!TAB Java]

```javascript {line-numbers="true"}
public class TargetRequestUtils {

    public static Context getContext(HttpServletRequest request) {
        Context context = new Context()
            .geo(ipToGeoLookup(request.getRemoteAddr()))
            .channel(ChannelType.WEB)
            .timeOffsetInMinutes(330.0)
            .address(getAddress(request));
        return context;
    }

    public static Geo ipToGeoLookup(String ip) {
        GeoResult geoResult = geoLookupService.lookup(ip);
        return new Geo()
            .city(geoResult.getCity())
            .stateCode(geoResult.getStateCode())
            .countryCode(geoResult.getCountryCode());
    }

}
```

>[!ENDTABS]

그러나 서버에 IP-to-Geo 조회를 수행할 수 없지만 계속 수행하려는 경우 [!UICONTROL 온디바이스 의사 결정] 대상 `getOffers` 지역 기반 대상자를 포함하는 요청도 지원됩니다. 이 접근 방식의 단점은 원격 IP-to-Geo 조회를 사용하여 각 항목에 지연을 추가한다는 것입니다 `getOffers` 호출합니다. 이 지연 시간은 원격보다 짧아야 합니다. `getOffers` 서버 근처에 있는 CDN에 도달하므로 를 호출합니다. 다음을 제공해야 합니다. `ipAddress` 의 필드 `Geo` 의 오브젝트 `Context` SDK가 사용자 IP 주소의 지리적 위치를 검색하도록 요청하십시오. 기타 다른 필드가 있는 경우 `ipAddress` 이(가) 제공됩니다. [!DNL Target] SDK는 확인을 위해 지리적 위치 메타데이터를 가져오지 않습니다.


>[!BEGINTABS]

>[!TAB Node.js]

```csharp {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    decisioningMethod: "on-device"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
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

>[!TAB Java]

```javascript {line-numbers="true"}
public class TargetRequestUtils {

    public static Context getContext(HttpServletRequest request) {
        Context context = new Context()
            .geo(new Geo().ipAddress(request.getRemoteAddr()))
            .channel(ChannelType.WEB)
            .timeOffsetInMinutes(330.0)
            .address(getAddress(request));
        return context;
    }

}
```

>[!ENDTABS]

## 할당 방법

다음 표는 지원되는 할당 방법과 지원되지 않는 할당 방법을 보여 줍니다 [!UICONTROL 온디바이스 의사 결정].

| 할당 방법 | 지원됨 |
| --- | --- |
| 수동 | 예 |
| [최고 경험에 자동 할당](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | 아니요 |
| [개인화된 경험에 대한 자동 타겟](https://experienceleague.adobe.com/docs/target/using/activities/auto-target-to-optimize.html) | 아니요 |
