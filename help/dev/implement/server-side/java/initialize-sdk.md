---
title: create 메서드를 사용하여 Java SDK 초기화
description: create 메서드를 사용하여 Java SDK를 초기화하고 [!UICONTROL TargetClient]을(를) 인스턴스화하여 실험 및 개인화된 경험을 위해  [!DNL Adobe Target] 을(를) 호출하는 방법에 대해 알아봅니다.
feature: APIs/SDKs
exl-id: 0e0ddead-7de8-4549-b81c-e72598558e4b
source-git-commit: 1d080b5e402e5d55039bf06611b44678cc6c36de
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 17%

---

# Java SDK 초기화

## 설명

Java SDK를 초기화하고 [!UICONTROL Target Client]을(를) 인스턴스화하여 실험 및 개인화된 경험을 위해 [!DNL Adobe Target]을(를) 호출하려면 `create` 메서드를 사용하십시오.

## 방법

`TargetClient.create`을(를) 사용하여 [!UICONTROL TargetClient]을(를) 만듭니다.

### 만들기

```javascript {line-numbers="true"}
TargetClient TargetClient.create(ClientConfig clientConfig)
```

`ClientConfig.builder`을(를) 사용하여 ClientConfig를 만들었습니다.

```javascript {line-numbers="true"}
ClientConfigBuilder ClientConfig.builder()
```

## 매개 변수

`ClientConfigBuilder`의 구조는 다음과 같습니다.

| 이름 | 유형 | 필수 | 기본값 | 설명 |
| --- | --- | --- | --- | --- |
| 클라이언트 | 문자열 | 예 | 없음 | [!UICONTROL Target Client Id] |
| organizationId | 문자열 | 예 | 없음 | [!UICONTROL Experience Cloud Organization ID] |
| connectTime | 숫자 | 아니오 | 10000 | 모든 요청에 대한 연결 시간 제한(밀리초) |
| socketTime | 숫자 | 아니오 | 10000 | 모든 요청에 대한 소켓 시간 제한(밀리초) |
| maxConnectionPerHost | 숫자 | 아니오 | 100 | [!DNL Target] 호스트당 최대 연결 수 |
| maxConnectionTotal | 숫자 | 아니오 | 200 | 모든 [!DNL Target]개의 호스트를 포함한 최대 연결 |
| connectionTtlMs | 숫자 | 아니오 | -1 | 총 TTL(Time to Live)은 영구 연결의 최대 수명(밀리초)을 정의합니다. 기본적으로 연결은 무기한 유지됩니다. |
| 유휴 연결 유효성 검사 | 숫자 | 아니오 | 1000 | 재사용 전에 영구 연결이 재확인되는 비활성 기간(밀리초) |
| evictIdleConnectionsAfterSecs | 숫자 | 아니오 | 20 | 연결 풀에서 유휴 연결을 제거하는 시간(초) |
| enableRetries | 부울 | 아니오 | true | 소켓 시간 초과에 대한 자동 재시도(최대 4회) |
| logRequest | 부울 | 아니오 | false | 디버그에서 [!DNL Target]개의 요청 및 응답 기록 |
| logRequestStatus | 부울 | 아니오 | false | [!DNL Target] 응답 시간, 상태 및 URL 기록 |
| serverDomain | 문자열 | 아니오 | `*client*.tt.omtrdc.net` | 기본 호스트 이름 무시 |
| secure | 부울 | 아니오 | true | HTTP 체계를 적용하도록 설정 해제 |
| requestInterceptor | HttpRequestInterceptor | 아니요 | Null | 사용자 지정 요청 인터셉터 추가 |
| defaultPropertyToken | 문자열 | 아니오 | 없음 | 모든 `getOffers` 호출에 대해 기본 속성 토큰을 설정합니다. **온디바이스 의사 결정**&#x200B;의 경우 SDK는 `defaultPropertyToken`에 설정된 속성 토큰에 대해 정규화된 활동이 포함된 아티팩트만 다운로드합니다. |
| defaultDecisioningMethod | DecisioningMethod enum | 아니요 | SERVER_SIDE | 온디바이스 의사 결정을 사용하려면 ON_DEVICE 또는 HYBRID로 설정해야 합니다. |
| 원격 분석 사용 | 부울 | 아니오 | true | 고객이 [!DNL Target] 서버에 요청하는 동안 추가 데이터 수집을 옵트아웃할 수 있도록 허용합니다. |
| proxyConfig | 클라이언트 프록시 구성 | 아니요 | 없음 | 클라이언트가 자체 프록시 세부 정보를 제공할 수 있음 |
| exceptionHandler | TargetExceptionHandler | 아니요 | 없음 | 규칙 처리 중 사용자 지정 예외 처리를 구현하는 데 사용할 수 있습니다. |
| httpClient | HttpClient | 아니요 | 없음 | 사용자가 [!DNL Target] HTTP 클라이언트를 사용자 지정 HTTP 클라이언트로 바꿀 수 있습니다. |
| onDeviceEnvironment | 문자열 | 아니오 | production | 스테이징과 같은 다른 온디바이스 환경을 지정하는 데 사용할 수 있습니다. |
| onDeviceConfigHost | 문자열 | 아니오 | `assets.adobetarget.com` | 온디바이스 의사 결정 아티팩트 파일을 다운로드하는 데 사용할 다른 호스트를 지정하는 데 사용할 수 있습니다. |
| onDeviceDecisioningPollingIntSecs | int | 아니요 | 300(5분) | 온디바이스 의사 결정 아티팩트 파일 가져오기 사이의 시간(초) |
| ondeviceArtifactPayload | 바이트[] | 아니요 | 없음 | 즉각적인 실행이 가능하도록 이전 아티팩트 페이로드와 함께 디바이스에서 의사 결정 제공 |
| onDeviceDecisioningHandler | OnDeviceDecisioningHandler | 아니요 | 없음 | 온디바이스 의사 결정 이벤트에 대한 콜백을 등록합니다. |
| onDeviceAllMatchingRulesMboxes | List\&lt;String\> | 아니요 | 없음 | 사용자가 온디바이스 의사 결정 중에 일치하는 모든 규칙 콘텐츠가 반환되는 mbox를 지정할 수 있습니다. |

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
