---
title: Adobe Target 단일 프로필 업데이트 API
description: 사용 방법 알아보기 [!DNL Adobe Target] [!UICONTROL 단일 프로필 업데이트 API] 단일 방문자의 프로필 데이터를 (으)로 보내기 [!DNL Target].
feature: APIs/SDKs
contributors: https://github.com/icaraps
source-git-commit: 81bff85a9d1fe28ca267c471a470da95568fd06d
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 4%

---

# [!DNL Adobe Target Single Profile Update API]

다음 [!DNL Adobe Target] [!UICONTROL 단일 프로필 업데이트 API] 단일 사용자에 대한 프로필 업데이트를 보낼 수 있습니다. 다음 [!UICONTROL 단일 프로필 업데이트 API] 는 과 거의 동일합니다. [!UICONTROL 벌크 프로필 업데이트 API], 그러나 방문자 프로필은 .cvs 파일 대신 API 호출에 인라인으로 한 번에 하나씩 업데이트됩니다.

다음 [!UICONTROL 단일 프로필 업데이트 API] 및 는 일반적으로 구현되지 않은 채널에서 발생하는 트랜잭션과 관련하여 업데이트가 발생해야 하는 경우에 사용됩니다 [!DNL Target]. 예를 들어 일부 오프라인 작업을 수행하는 단일 방문자의 프로필을 업데이트하려고 합니다. 콜 센터 문의, 대출 지원, 매장 내 로열티 카드 사용, 키오스크 액세스 등의 작업을 수행할 수 있습니다.

의 이점 [!UICONTROL 단일 프로필 업데이트 API] 포함:

* 프로필 속성의 개수에 대한 제한은 없습니다.
* 사이트를 통해 전송된 프로필 속성은 API를 통해 또는 그 반대로 업데이트할 수 있습니다.

## 주의 사항

* 다음 [!UICONTROL 단일 프로필 업데이트 API] 는 롤링 24시간 동안 100만 개의 업데이트를 수행하도록 제한됩니다.
* 업데이트는 일반적으로 1시간 이내에 발생하지만 반영하는 데 24시간 정도 소요될 수 있습니다.

  업데이트를 더 많이 보내야 하거나 더 짧은 기간에 업데이트를 처리해야 하는 경우 클라이언트측 업데이트(기본 설정) 또는 를 통해 트랜잭션 프로필 업데이트를 보내는 것이 좋습니다. [!DNL Adobe Target] 서버측 [배달 API](/help/dev/implement/delivery-api/overview.md).

## 형식

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