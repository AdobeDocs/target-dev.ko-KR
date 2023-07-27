---
title: create 메서드를 사용하여 Java SDK 초기화
description: create 메서드를 사용하여 Java SDK를 초기화하고 [!UICONTROL TargetClient] 을(를) 호출하려면 [!DNL Adobe Target] (실험 및 개인화된 경험)
feature: APIs/SDKs
exl-id: 0e0ddead-7de8-4549-b81c-e72598558e4b
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 18%

---

# Java SDK 초기화

## 설명

사용 `create` 메서드를 사용하여 Java SDK를 초기화하고 [!UICONTROL Target 클라이언트] 을(를) 호출하려면 [!DNL Adobe Target] (실험 및 개인화된 경험)

## 방법

[!UICONTROL TargetClient] 다음을 사용하여 생성됨 `TargetClient.create`.

### 만들기

```javascript {line-numbers="true"}
TargetClient TargetClient.create(ClientConfig clientConfig)
```

ClientConfig는 다음을 사용하여 만들어집니다. `ClientConfig.builder`.

```javascript {line-numbers="true"}
ClientConfigBuilder ClientConfig.builder()
```

## 매개 변수

`ClientConfigBuilder` 에는 다음 구조가 있습니다.

| 이름 | 유형 | 필수 | 기본값 | 설명 |
| --- | --- | --- | --- | --- |
| 클라이언트 | 문자열 | 예 | 없음 | [!UICONTROL Target 클라이언트 Id] |
| organizationId | 문자열 | 예 | 없음 | [!UICONTROL Experience Cloud 조직 ID] |
| connectTime | 숫자 | 아니오 | 10000 | 모든 요청에 대한 연결 시간 제한(밀리초) |
| socketTime | 숫자 | 아니오 | 10000 | 모든 요청에 대한 소켓 시간 제한(밀리초) |
| maxConnectionPerHost | 숫자 | 아니오 | 100 | 최대 연결 수 [!DNL Target] 호스트 |
| maxConnectionTotal | 숫자 | 아니오 | 200 | 모든 연결을 포함한 최대 연결 수 [!DNL Target] 호스트 |
| enableRetries | 부울 | 아니오 | true | 소켓 시간 초과에 대한 자동 재시도(최대 4회) |
| logRequest | 부울 | 아니오 | false | 로그 [!DNL Target] 디버그의 요청 및 응답 |
| logRequestStatus | 부울 | 아니오 | false | 로그 [!DNL Target] 응답 시간, 상태 및 URL |
| serverDomain | 문자열 | 아니오 | `*client*.tt.omtrdc.net` | 기본 호스트 이름 무시 |
| secure | 부울 | 아니오 | true | HTTP 체계를 적용하도록 설정 해제 |
| requestInterceptor | HttpRequestInterceptor | 아니요 | Null | 사용자 지정 요청 인터셉터 추가 |
| defaultPropertyToken | 문자열 | 아니오 | 없음 | 다음에 대한 기본 속성 토큰을 설정합니다. `getOffers` 호출합니다. **온디바이스 의사 결정**, SDK는에 설정된 속성 토큰에 대한 적격 활동이 포함된 아티팩트만 다운로드합니다. `defaultPropertyToken` |
| defaultDecisioningMethod | DecisioningMethod enum | 아니요 | SERVER_SIDE | 온디바이스 의사 결정을 사용하려면 ON_DEVICE 또는 HYBRID로 설정해야 합니다. |
| 원격 분석 사용 | 부울 | 아니오 | true | 에 대한 요청 중에 고객이 추가 데이터 수집을 옵트아웃할 수 있음 [!DNL Target] 서버 |
| proxyConfig | 클라이언트 프록시 구성 | 아니요 | 없음 | 클라이언트가 자체 프록시 세부 정보를 제공할 수 있음 |
| exceptionHandler | TargetExceptionHandler | 아니요 | 없음 | 규칙 처리 중 사용자 지정 예외 처리를 구현하는 데 사용할 수 있습니다. |
| httpClient | HttpClient | 아니요 | 없음 | 사용자가 다음을 바꿀 수 있도록 허용 [!DNL Target] 사용자 지정 HTTP 클라이언트가 있는 HTTP 클라이언트 |
| onDeviceEnvironment | 문자열 | 아니오 | production | 스테이징과 같은 다른 온디바이스 환경을 지정하는 데 사용할 수 있습니다. |
| onDeviceConfigHost | 문자열 | 아니오 | `assets.adobetarget.com` | 온디바이스 의사 결정 아티팩트 파일을 다운로드하는 데 사용할 다른 호스트를 지정하는 데 사용할 수 있습니다. |
| onDeviceDecisioningPollingIntSecs | int | 아니요 | 300(5분) | 온디바이스 의사 결정 아티팩트 파일 가져오기 사이의 시간(초) |
| ondeviceArtifactPayload | 바이트[] | 아니요 | 없음 | 즉각적인 실행이 가능하도록 이전 아티팩트 페이로드와 함께 디바이스에서 의사 결정 제공 |
| onDeviceDecisioningHandler | OnDeviceDecisioningHandler | 아니요 | 없음 | 온디바이스 의사 결정 이벤트에 대한 콜백을 등록합니다. |
| onDeviceAllMatchingRulesMboxes | 목록\&lt;string> | 아니요 | 없음 | 사용자가 온디바이스 의사 결정 중에 일치하는 모든 규칙 콘텐츠가 반환되는 mbox를 지정할 수 있습니다. |

## 예

### Java

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .build();

TargetClient.create(clientConfig);

// make calls to Adobe Target
```
