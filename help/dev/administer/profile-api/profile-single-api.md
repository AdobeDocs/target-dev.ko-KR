---
title: Adobe Target 단일 프로필 업데이트 API
description: 사용 방법 알아보기 [!DNL Adobe Target] [!UICONTROL 단일 프로필 업데이트 API] 단일 방문자의 프로필 데이터를 (으)로 보내기 [!DNL Target].
feature: APIs/SDKs
contributors: https://github.com/icaraps
source-git-commit: 6f7d9875e3b73352ead3a55e40a4b2f81f3d4400
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 2%

---

# [!DNL Adobe Target Single Profile Update API]

다음 [!DNL Adobe Target] [!UICONTROL 단일 프로필 업데이트 API] 단일 사용자에 대한 프로필 업데이트를 보낼 수 있습니다. 다음 [!UICONTROL 단일 프로필 업데이트 API] 및 는 일반적으로 구현되지 않은 채널에서 발생하는 트랜잭션과 관련하여 업데이트가 발생해야 하는 경우에 사용됩니다 [!DNL Target].

다음 [!UICONTROL 단일 프로필 업데이트 API] 는 롤링 24시간 동안 100만 개의 업데이트를 수행하도록 제한됩니다. 업데이트는 일반적으로 1시간 이내에 발생하지만 반영하는 데 24시간 정도 소요될 수 있습니다. 업데이트를 더 많이 보내야 하거나 더 짧은 기간에 업데이트를 처리해야 하는 경우 클라이언트측 업데이트(기본 설정) 또는 를 통해 트랜잭션 프로필 업데이트를 보내는 것이 좋습니다. [!DNL Adobe Target] 서버측 [배달 API](/help/dev/implement/delivery-api/overview.md).

프로필 매개 변수를 형식으로 지정합니다. `profile.paramName=value`.

에 대한 프로필을 업데이트하려면 `pcId`, 사용:

``````
https://<your-client-code>.tt.omtrdc.net/m2/client/profile/update?mboxPC=1368007744041-575948.01_00&profile.attr=0&profile.attr2=1...
``````

에 대한 프로필을 업데이트하려면 `mbox3rdPartyId`, 사용:

``````
shell http://<your-client-code>.tt.omtrdc.net/m2/client/profile/update?mbox3rdPartyId=123456&profile.attr=0&profile.attr2=1...
``````

다음 [!UICONTROL 단일 프로필 업데이트 API] 업데이트 전용입니다. 아무 것도 발견되지 않으면 프로필이 만들어지지 않습니다.

## 참고

* 매개 변수와 값은 UTF-8을 사용하여 URL로 인코딩되어야 합니다.
* 매개변수 포맷: `profile.paramName`.
* 모든 pcIds 및 mbox3rdPartyIds에 대해 일부 매개 변수 값이 있어야 하는 것은 아닙니다.
* 매개변수 및 값은 대/소문자를 구분합니다.
* GET과 POST이 모두 지원됩니다.
* 제한의 현재 크기 제한은 GET의 경우 8KB, POST의 경우 60KB입니다.

## 응답

위의 요청에 대한 샘플 응답은 다음과 같습니다.

`trueRequest successfully submitted`

이 응답은 응답이 제출되었으며 곧 처리됨을 나타냅니다.