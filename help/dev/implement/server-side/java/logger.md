---
title: 초기화 [!DNL Adobe Target] 요청을 기록할 Java SDK
description: 에 요청을 기록하는 방법 알아보기 [!DNL Adobe Target] Java SDK.
feature: APIs/SDKs
exl-id: 85d1a6ef-0b08-4948-8133-740b7d6141dd
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 4%

---

# 로거(Java)

## 설명

날짜 [sdk 초기화](initialize-sdk.md), 다음과 같은 몇 가지 옵션이 있습니다. `ClientConfig` 개체를 설정합니다.

| 옵션 | 설명 |
| --- | --- |
| `logRequests` | 전체 요청 본문과 응답 본문을 기록합니다. |
| `logRequestStatus` | 응답 시간과 함께 요청의 URL, 상태를 기록합니다. |

[!DNL Target] Java SDK는 `slf4j` 로깅 중. 다음과 같은 로거의 구현을 제공해야 합니다. `java.util.logging`, `logback`, 및 `log4j`. 을(를) 참조하십시오 [http://www.slf4j.org/manual.html](http://www.slf4j.org/manual.html) 추가 정보. 모든 로그가 인쇄됩니다. `debug`.

## 예

추가 `slf4j` 종속성.

>[!BEGINTABS]

>[!TAB Gradle]

### Gradle

```javascript {line-numbers="true"}
compile 'org.slf4j:slf4j-simple:2.0.0-alpha0'
```

>[!TAB Maven]

```javascript {line-numbers="true"}
<dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-simple</artifactId>
    <version>2.0.0-alpha0</version>
</dependency>
```

>[!ENDTABS]

활성화 `DEBUG` 구현을 기반으로 로그를 만들고 요청 로깅 플래그를 표시합니다.

### 디버그

```javascript {line-numbers="true"}
System.setProperty(SimpleLogger.DEFAULT_LOG_LEVEL_KEY, "DEBUG");
ClientConfig config = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .logRequests(true)
        .logRequestStatus(true)
        .build();

TargetClient targetClient = TargetClient.create(config);
```

요청, 응답 및 응답 시간이 콘솔에 인쇄되는 것을 볼 수 있습니다.
