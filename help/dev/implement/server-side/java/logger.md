---
title: 요청을 기록하려면  [!DNL Adobe Target] Java SDK 초기화
description: ' [!DNL Adobe Target] Java SDK에 요청을 기록하는 방법을 알아봅니다.'
feature: APIs/SDKs
exl-id: 85d1a6ef-0b08-4948-8133-740b7d6141dd
source-git-commit: 526445fccee9b778b7ac0d7245338f235f11d333
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 4%

---

# 로거(Java)

## 설명

[SDK을 초기화](initialize-sdk.md)할 때 `ClientConfig` 개체에 로그 요청으로 설정할 수 있는 몇 가지 옵션이 있습니다.

| 옵션 | 설명 |
| --- | --- |
| `logRequests` | 전체 요청 본문과 응답 본문을 기록합니다. |
| `logRequestStatus` | 응답 시간과 함께 요청의 URL, 상태를 기록합니다. |

[!DNL Target] Java SDK에서 `slf4j` 로깅을 사용합니다. `java.util.logging`, `logback` 및 `log4j` 같은 로거의 구현을 제공해야 합니다. 자세한 내용은 [https://www.slf4j.org/manual.html](https://www.slf4j.org/manual.html)을(를) 참조하십시오. 모든 로그가 `debug`에 인쇄됩니다.

## 예

`slf4j` 종속성을 추가합니다.

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

구현에 따라 `DEBUG` 로그를 사용하도록 설정하고 요청 로깅 플래그를 표시합니다.

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
