---
title: 대상 타기팅
description: 대상을 사용하여 실험 및 개인화 활동을 타깃팅할 수 있습니다. [!DNL Adobe Target] 는 기본적으로 무수히 강력한 대상 타깃팅 기능을 지원합니다.
exl-id: df1bd856-e848-452c-90a0-abf29e7a2313
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 17%

---

# 대상 타기팅

## 개요

대상을 사용하여 실험 및 개인화 활동을 타깃팅할 수 있습니다. [!DNL Adobe Target] 는 기본적으로 무수히 강력한 대상 타깃팅 기능을 지원합니다. 다음 속성은에 사용할 수 있습니다. [대상 타기팅](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/create-audience.html):

### [!DNL Target] 라이브러리

자세한 내용은 [[!DNL Target] 라이브러리](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-library.html). &#x200B;
* Bing에서 참조됨
* Chrome 브라우저
* Firefox 브라우저
* Google에서 참조됨
* Internet Explorer
* Linux 운영 체제
* Mac 운영 체제
* 새 방문자
* 재방문자
* Safari 브라우저
* 태블릿 장치
* Windows 운영 체제
* Yahoo에서 참조됨

### 지역

자세한 내용은 [지역](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html). &#x200B; &#x200B;
* 국가/지역
* 주/도
* 구/군/시
* 우편번호
* 위도
* 경도
* DMA
* 모바일 통신사

### 네트워크

자세한 내용은 [네트워크](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html).

* ISP
* 도메인 이름
* 연결 속도

### 모바일

자세한 내용은 [ 모바일 ](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html)을 참조하십시오. 

* 장치 마케팅 이름
* 장치 모델
* 장치 공급업체
* 모바일 장치입니다.
* 휴대 전화입니다.
* 태블릿입니다.
* OS
* 화면 높이(픽셀)
* 화면 너비(픽셀)

### 사용자 지정

자세한 내용은 [사용자 지정 매개 변수](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html).

* 모든 키/값 쌍

### 운영 체제

자세한 내용은 [운영 체제](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html).

* Linux
* Macintosh
* Windows

### 사이트 페이지

자세한 내용은 [사이트 페이지](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html).

* 현재 페이지
* 이전 페이지
* 랜딩 페이지
* HTTP 헤더

### 브라우저

자세한 내용은 [브라우저](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html).

* 유형
* 언어
* 버전

### 방문자 프로필

자세한 내용은 [방문자 프로필](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html).

* 지속되는 모든 키/값 쌍

### 트래픽 소스

자세한 내용은 [트래픽 소스](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html).

* Baidu에서
* Bing에서
* Google에서
* Yahoo에서
* 참조 랜딩 페이지: URL
* 참조 랜딩 페이지: 도메인
* 참조 랜딩 페이지: 쿼리

### 시간대

자세한 내용은 [ 시간대 ](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html)를 참조하십시오.

* 시작 날짜/종료 날짜

## 클라이언트 힌트

[!DNL Adobe Target] 브라우저, 운영 체제 및 모바일 대상 속성과 프로필 스크립트의 특정 인스턴스를 올바르게 세분하려면 클라이언트 힌트가 필요합니다. 자세한 배경 정보는 [사용자 에이전트 및 클라이언트 힌트](../../../client-side/atjs/user-agent-and-client-hints.md).

### 클라이언트 힌트를 전달하는 방법 [!DNL Adobe Target]

Node.js SDK v2.4.0 및 Java SDK v2.3.0부터 클라이언트 힌트를으로 보낼 수 있습니다. [!DNL Target] 경유 `getOffers()` 호출. 클라이언트 힌트는 `request.context` 개체와 사용자 에이전트.

>[!BEGINTABS]

>[!TAB Node.js SDK]

```js {line-numbers="true"}
targetClient.getOffers({ 
    request: { 
        context: { 
            channel: "mobile" 
            userAgent: "Mozilla/5.0 (Linux; Android 12; Pixel 4a) AppleWebKit/537.36 (KHTML, like Gecko) Mobile Safari/537.36", 
            clientHints: { 
                mobile: "true", 
                platform: "Linux", 
                platformVersion: "12.1", 
                model: "Pixel 4a", 
                browserUAWithMajorVersion: "\"Not A;Brand\";v=\"98\", \"Chromium\";v=\"98\", \"Google Chrome\";v=\"98\"", 
                browserUAWithFullVersion: "\" Not A;Brand\";v=\"98.0.0.0\", \"Chromium\";v=\"98.0.4844.83\", \"Google Chrome\";v=\"98.0.4758.101\"", 
                bitness: "64", 
                architecture: "x86" 
            } 
        }, 
        execute: { 
            mboxes: [{ 
                name: "home", 
                index: 1 
            }] 
        } 
    } 
});
```

>[!TAB Java SDK]

```javascript {line-numbers="true"}
import com.adobe.target.delivery.v1.model.ClientHints; 
import com.adobe.target.delivery.v1.model.Context; 
import com.adobe.target.delivery.v1.model.ExecuteRequest; 
import com.adobe.target.edge.client.model.TargetDeliveryRequest; 

 
ClientHints clientHints = new ClientHints(); 
clientHints.setMobile(true); 
clientHints.setPlatform("macOS"); 
clientHints.setArchitecture("x86"); 
clientHints.setPlatformVersion("11.3.1"); 
clientHints.setBrowserUAWithMajorVersion( 
  "\" Not A;Brand\";v=\"99\", \"Chromium\";v=\"99\", \"Google Chrome\";v=\"99\""); 
String userAgent = 
  "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Safari/537.36"; 

 
TargetDeliveryRequest request = TargetDeliveryRequest.builder() 
        .execute(new ExecuteRequest().pageLoad(pageLoad)) 
        .context(new Context().clientHints(clientHints).userAgent(userAgent)) 
        .build(); 
```

>[!ENDTABS]

## 온디바이스 의사 결정

다음 표는 디바이스에서 의사 결정에 대해 지원되거나 지원되지 않는 대상 규칙을 나타냅니다.

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

### 온디바이스 의사 결정을 위한 지역 타기팅

Adobe 지역 기반 대상을 사용하는 온디바이스 의사 결정 활동에 대해 지연 시간이 거의 0에 가깝도록 유지하려면 호출에 지역 값을 직접 제공하는 것이 좋습니다. `getOffers`. 다음을 설정하여 이 작업을 수행합니다. `Geo` 의 오브젝트 `Context` 요청. 즉, 서버에서 각 최종 사용자의 위치를 확인하는 방법이 필요합니다. 예를 들어 서버는 사용자가 구성하는 서비스를 사용하여 IP-to-Geo 조회를 수행할 수 있습니다. Google Cloud와 같은 일부 호스팅 공급자는 각 의 사용자 지정 헤더를 통해 이 기능을 제공합니다 `HttpServletRequest`.

>[!BEGINTABS]

>[!TAB Node.js SDK]

```js {line-numbers="true"}
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

>[!TAB Java SDK]

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

그러나 서버에 대해 IP-to-Geo 조회를 수행할 수 없지만 `getOffers` 지역 기반 대상자를 포함하는 요청도 지원됩니다. 이 접근 방식의 단점은 원격 IP-to-Geo 조회를 사용하여 각 항목에 지연을 추가한다는 것입니다 `getOffers` 호출합니다. 이 지연 시간은 원격보다 짧아야 합니다. `getOffers` 서버 근처에 있는 CDN에 도달하므로 를 호출합니다. 다음을 수행해야 합니다. **전용** 다음을 제공합니다. `ipAddress` 의 필드 `Geo` 의 오브젝트 `Context` SDK가 사용자 IP 주소의 지리적 위치를 검색하도록 요청하십시오. 기타 다른 필드가 있는 경우 `ipAddress` 이(가) 제공됩니다. [!DNL Target] SDK는 확인을 위해 지리적 위치 메타데이터를 가져오지 않습니다.

>[!BEGINTABS]

>[!TAB Node.js SDK]

```js {line-numbers="true"}
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

>[!TAB Java SDK]

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

## 서버측 의사 결정

다음 표는 서버측 의사 결정에 대해 지원되거나 지원되지 않는 대상 규칙을 나타냅니다.

| 대상 규칙 | 서버측 의사 결정 |
| --- | --- |
| [지역](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | 예 |
| [네트워크](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | 예 |
| [모바일](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | 예 |
| [사용자 지정 매개 변수](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | 예 |
| [운영 체제](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | 예 |
| [사이트 페이지](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | 예 |
| [브라우저](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | 예 |
| [방문자 프로필](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | 예 |
| [트래픽 소스](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | 예 |
| [시간대](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | 예 |
| [Experience Cloud 대상](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html) (Adobe Audience Manager, Adobe Analytics 및 Adobe Experience Manager의 대상 | 예 |
