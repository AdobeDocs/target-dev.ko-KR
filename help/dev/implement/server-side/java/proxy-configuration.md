---
title: 에서 프록시 구성 구현 [!DNL Adobe Target] Java SDK
description: 에서 TargetClient 프록시 구성을 구성하는 방법을 알아봅니다. [!DNL Adobe Target] Java SDK.
feature: APIs/SDKs
exl-id: 32e8277d-3bba-4621-b9c7-3a49ac48a466
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 1%

---

# 프록시 구성(Java)

## 기본 프록시

SDK를 실행하는 응용 프로그램에서 인터넷에 액세스하기 위해 프록시가 필요한 경우 `TargetClient` 다음과 같이 프록시 구성을 사용해야 합니다.

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

프록시 인증이 필요한 경우 자격 증명을 매개 변수로서 `ClientProxyConfig` 아래 예제에 따라 생성자입니다. 이 기능은 간단한 사용자 이름/암호 프록시 인증에만 작동합니다.

### 기본 프록시 인증

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .proxyConfig(new ClientProxyConfig(host,port,username,password))
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```
