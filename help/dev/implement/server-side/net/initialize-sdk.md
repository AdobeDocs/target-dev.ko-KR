---
title: create 메서드를 사용하여 .NET SDK 초기화
description: create 메서드를 사용하여 Java SDK를 초기화하고 [!UICONTROL TargetClient]을(를) 인스턴스화하여 실험 및 개인화된 경험을 위해  [!DNL Adobe Target] 을(를) 호출하는 방법에 대해 알아봅니다.
feature: APIs/SDKs
exl-id: 501010c3-22f4-49a8-b2ac-c7307232d180
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 16%

---

# .NET SDK 초기화

## 설명

`Create` 메서드를 사용하여 .NET SDK를 초기화하고 [!UICONTROL Target Client]을(를) 인스턴스화하여 실험 및 개인화된 경험을 위해 [!DNL Adobe Target]을(를) 호출합니다.

.NET 종속성 삽입을 사용하는 경우 서비스 구성 단계에서 `services.AddTargetLibrary()`을(를) 호출하여 SDK를 추가한 다음 앱의 생성자에 `ITargetClient targetClient`을(를) 삽입하면 됩니다.

그런 다음 SDK의 `Initialize` 메서드를 사용하여 SDK를 구성하면 초기화 단계가 완료됩니다.

## 방법

`TargetClient.Create`을(를) 사용하여 `TargetClient`을(를) 만듭니다.

## C\#

```csharp {line-numbers="true"}
TargetClient TargetClient.Create(TargetClientConfig clientConfig)
```

`ClientConfig`이(가) ClientConfig.Builder를 사용하여 만들어집니다.

## C\#

```csharp {line-numbers="true"}
TargetClientConfig.Builder TargetClientConfig.Builder()
```

## 매개 변수

`TargetClientConfig.Builder`의 구조는 다음과 같습니다.

| 이름 | 유형 | 필수 | 기본값 | 설명 |
| --- | --- | --- | --- | --- |
| 클라이언트 | string | 예 | 없음 | [!UICONTROL Target Client Id] |
| 조직 ID | string | 예 | 없음 | [!UICONTROL Experience Cloud Organization ID] |
| 시간 초과 | int | 아니요 | 10000 | 모든 요청에 대한 시간 제한(밀리초) |
| 프록시 |  | WebProxy | 아니요 | null | 모든 [!DNL Target]개 요청에 대한 프록시 |
| 재시도 정책 | 정책 | 아니요 | null | 모든 [!DNL Target]개 요청에 대한 정책 다시 시도 |
| AsyncRetryPolicy | AsyncPolicy | 아니요 | null | 모든 [!DNL Target] 요청에 대한 비동기 다시 시도 정책 |
| Logger | ILogger | 아니요 | null | [!DNL Target]개 요청 및 응답의 디버그 로깅에 사용됩니다. |
| 서버 도메인 | string | 아니요 | `client.tt.omtrdc.net` | 기본 호스트 이름 무시 |
| 보안 | 부울 | 아니요 | true | HTTP 체계를 적용하도록 설정 해제 |
| DefaultPropertyToken | string | 아니요 | null | `getOffers` 호출마다 기본 속성 토큰을 설정합니다. |
| 원격 분석 사용 | 부울 | 아니요 | true | SDK 사용 환경을 개선하기 위해 원격 분석 데이터 보내기 |
| DecisioningMethod | DecisioningMethod enum | 아니요 | 서버측 | 온디바이스 의사 결정을 활성화하려면 OnDevice 또는 Hybrid로 설정해야 합니다. |
| OnDeviceDecisionReady | 작업 | 아니요 | null | 온디바이스 의사 결정 준비 이벤트에 대한 위임(온디바이스 의사 결정이 준비되면 한 번 호출됨) |
| ArtifactDownloadSucceeded | 작업 | 아니요 | null | 온디바이스 의사 결정 아티팩트 다운로드 성공(성공한 각 아티팩트 다운로드에서 호출됨)에 대한 위임 |
| ArtifactDownloadFailed | 작업 | 아니요 | null | 온디바이스 의사 결정 아티팩트 다운로드 실패(실패한 각 아티팩트 다운로드에 대해 호출됨)에 대한 위임 |
| OnDeviceEnvironment | string | 아니요 | production | 스테이징과 같은 다른 온디바이스 환경을 지정하는 데 사용할 수 있습니다. |
| OnDeviceConfigHost | string | 아니요 | `assets.adobetarget.com` | 온디바이스 의사 결정 아티팩트 파일을 다운로드하는 데 사용할 다른 호스트를 지정하는 데 사용할 수 있습니다. |
| OnDeviceDecisioningPollingIntSecs | int | 아니요 | 300(5분) | 온디바이스 의사 결정 아티팩트 파일 가져오기 사이의 시간(초) |
| OnDeviceArtifactLoad | string | 아니요 | null | 즉각적인 실행이 가능하도록 로컬 아티팩트 페이로드를 사용하여 디바이스에서 의사 결정 제공 |

## 예

## C\#

```csharp {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("acmeclient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
    .Build();

targetClient = TargetClient.Create(targetClientConfig);

// make calls to Adobe Target
```
