---
title: ' [!DNL Adobe Target] Java SDK에서 프록시 구성 구현'
description: ' [!DNL Adobe Target] Java SDK에서 TargetClient 프록시 구성을 구성하는 방법에 대해 알아봅니다.'
feature: APIs/SDKs
exl-id: 32e8277d-3bba-4621-b9c7-3a49ac48a466
source-git-commit: 59ab3f53e2efcbb9f7b1b2073060bbd6a173e380
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---

# 프록시 구성(Java)

## 기본 프록시

SDK를 실행하는 응용 프로그램에서 인터넷에 액세스하기 위해 프록시가 필요한 경우 다음과 같이 프록시 구성을 사용하여 `TargetClient`을(를) 구성해야 합니다.

### 기본 프록시 구성

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .proxyConfig(new ClientProxyConfig(host,port))
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```

## 인증

프록시 인증이 필요한 경우 아래 예제에 따라 자격 증명을 매개 변수로 `ClientProxyConfig` 생성자에 전달할 수 있습니다. 이 기능은 간단한 사용자 이름/암호 프록시 인증에만 작동합니다.

### 기본 프록시 인증

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .proxyConfig(new ClientProxyConfig(host,port,username,password))
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```

## 온디바이스 의사 결정

규칙 아티팩트를 가져오는 요청의 경우 응답을 캐시하지 않도록 프록시를 구성해야 합니다. 그러나 해당 요청에 대해 프록시의 캐싱 메커니즘을 구성할 수 없는 경우 프록시 수준 캐시를 무시하는 해결 방법으로 구성 옵션을 사용하십시오. 이 해결 방법은 빈 문자열 값이 있는 `Authorization` 헤더를 규칙 요청에 추가하며, 이 요청은 응답을 캐시하지 않아야 함을 프록시에 표시해야 합니다.

이 해결 방법을 사용하려면 다음을 설정하십시오.

```java {line-numbers="true"}
ClientConfig.builder()
    .shouldArtifactRequestBypassProxyCache(true)
    .build();
```


