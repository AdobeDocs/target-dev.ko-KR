---
title: 사용자 지정 HTTP 클라이언트를 구성하는 방법 알아보기
description: ClientConfig.builder().httpClient()를 사용하여 TargetClient를 구성하는 방법을 알아봅니다.
feature: APIs/SDKs
exl-id: 7615029c-b62d-4ed1-aadb-32e364c4c654
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# 사용자 지정 HTTP 클라이언트 구성(Java)

SDK를 실행하는 애플리케이션에 사용자 정의 HTTP 클라이언트가 필요한 경우, SSL 구성 또는 요청에 기본 헤더 추가와 같은 기능을 활성화하려면 다음을 수행합니다. `TargetClient` 다음을 사용하여 구성해야 합니다. `ClientConfig.builder().httpClient()`:

## 기본 사용자 지정 HTTP 클라이언트 구성

SDK는 현재 를 구현하는 HTTP 클라이언트를 지원합니다. `org.apache.http.client.HttpClient` 인터페이스.

### 기본 구현

```java {line-numbers="true"}
CloseableHttpClient httpClient = HttpClients.custom().build();
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .httpClient(httpClient)
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```

## SSL 구성을 사용한 사용자 지정 HTTP 클라이언트 구성

다음은에서 SSL을 구성하는 방법의 예입니다. `TargetClient` 을(를) 사용자 지정하여 `HttpClient` 에 전달됨 `ClientConfig`. 다음 코드 조각은 `org.apache.http.conn.ssl` ssl 구성을 위한 패키지

### SSL 구현

```java {line-numbers="true"}
SSLContext context = SSLContextBuilder.create().build();
SSLConnectionSocketFactory sslSocketFactory = new SSLConnectionSocketFactory(context);
CloseableHttpClient httpClient = HttpClients.custom().setSSLSocketFactory(sslSocketFactory).build();
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .httpClient(httpClient)
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```
