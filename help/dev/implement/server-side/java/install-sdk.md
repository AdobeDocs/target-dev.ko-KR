---
title: Java SDK 설치
description: 설치 방법 알아보기 [!DNL Adobe Target] Java SDK.
feature: APIs/SDKs
exl-id: 5828d5b3-c487-49bf-9458-7ef94374e32d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---

# Java SDK 설치

Java SDK는에서 배포합니다. [Maven Central](https://search.maven.org/artifact/com.adobe.target/target-java-sdk). 시작하려면 를 설치하여 종속으로 추가합니다. `gradle` 또는 `maven`:

>[!BEGINTABS]

>[!TAB Gradle]

```javascript {line-numbers="true"}
compile 'com.adobe.target:java-sdk:1.0'
```

>[!TAB Maven]

```javascript {line-numbers="true"}
<dependency>
    <groupId>com.adobe.target</groupId>
    <artifactId>java-sdk</artifactId>
    <version>2.0</version>
</dependency>
```

>[!ENDTABS]

오픈 소스 코드는에서 찾을 수 있습니다. <https://github.com/adobe/target-java-sdk>.
