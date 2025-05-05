---
title: Adobe Target 단일 프로필 업데이트 API
description: ' [!DNL Adobe Target] [!UICONTROL Single Profile Update API]을(를) 사용하여 단일 방문자의 프로필 데이터를  [!DNL Target] (으)로 보내는 방법을 알아봅니다.'
feature: APIs/SDKs
contributors: https://github.com/icaraps
exl-id: 4e022db3-215f-461b-9222-38ce2f2dbc28
source-git-commit: e2462d12cf58ab5a588c13a96df5e6abafb9d675
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 3%

---

# [!DNL Adobe Target Single Profile Update API]

[!DNL Adobe Target] [!UICONTROL Single Profile Update API]을(를) 사용하면 한 사용자에 대한 프로필 업데이트를 보낼 수 있습니다. [!UICONTROL Single Profile Update API]은(는) [!UICONTROL Bulk Profile Update API]과(와) 거의 동일하지만 한 번에 한 방문자 프로필이 .cvs 파일 대신 API 호출로 업데이트됩니다.

[!UICONTROL Single Profile Update API] 및 은 일반적으로 [!DNL Target]을(를) 구현하지 않은 채널에서 발생하는 트랜잭션과 관련하여 업데이트가 발생해야 하는 경우에 사용됩니다. 예를 들어 일부 오프라인 작업을 수행하는 단일 방문자의 프로필을 업데이트하려고 합니다. 콜 센터 문의, 대출 지원, 매장 내 로열티 카드 사용, 키오스크 액세스 등의 작업을 수행할 수 있습니다.

[!UICONTROL Single Profile Update API]의 이점은 다음과 같습니다.

* 프로필 속성의 개수에 대한 제한은 없습니다.
* 사이트를 통해 전송된 프로필 속성은 API를 통해 또는 그 반대로 업데이트할 수 있습니다.

## 주의 사항

* [!UICONTROL Single Profile Update API]은(는) 롤링 24시간 동안 100만 개의 업데이트를 수행하도록 제한됩니다.
* 업데이트는 일반적으로 1시간 이내에 발생하지만 반영하는 데 24시간 정도 소요될 수 있습니다.

  더 많은 업데이트를 보내야 하거나 더 짧은 기간에 업데이트를 처리해야 하는 경우 클라이언트측 업데이트(기본 설정) 또는 [!DNL Adobe Target] 서버측 [배달 API](/help/dev/implement/delivery-api/overview.md)를 통해 트랜잭션 프로필 업데이트를 보내는 것이 좋습니다.

* [!UICONTROL Single Profile Update API]은(는) 서버 간 API이며 웹 페이지에서 작동하도록 디자인되지 않았습니다. 웹 페이지 내에서 방문자 프로필을 업데이트하려면 [trackEvent()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) 함수 또는 [배달 API](/help/dev/implement/delivery-api/overview.md)를 사용할 수 있습니다.

## 형식

프로필 매개 변수를 `profile.paramName=value` 형식으로 지정하십시오.

`pcId`에 대한 프로필을 업데이트하려면 다음을 사용합니다.

``` ```
https://&lt;your-client-code>.tt.omtrdc.net/m2/client/profile/update?mboxPC=1368007744041-575948.01_00&profile.attr=0&profile.attr2=1...
``` ```

`mbox3rdPartyId`에 대한 프로필을 업데이트하려면 다음을 사용합니다.

``` ```
shell http://&lt;your-client-code>.tt.omtrdc.net/m2/client/profile/update?mbox3rdPartyId=123456&profile.attr=0&profile.attr2=1...
``` ```

[!UICONTROL Single Profile Update API]은(는) 업데이트 전용입니다. 아무 것도 발견되지 않으면 프로필이 만들어지지 않습니다.

## 참고

* 매개 변수와 값은 UTF-8을 사용하여 URL로 인코딩되어야 합니다.
* 매개 변수 형식은 `profile.paramName`입니다.
* 모든 pcIds 및 mbox3rdPartyIds에 대해 일부 매개 변수 값이 있어야 하는 것은 아닙니다.
* 매개 변수와 값은 대/소문자를 구분합니다.
* GET과 POST이 모두 지원됩니다.
* 제한의 현재 크기 제한은 GET의 경우 8KB, POST의 경우 60KB입니다.

## 응답

위의 요청에 대한 샘플 응답은 다음과 같습니다.

`trueRequest successfully submitted`

이 응답은 응답이 제출되었으며 곧 처리됨을 나타냅니다.
