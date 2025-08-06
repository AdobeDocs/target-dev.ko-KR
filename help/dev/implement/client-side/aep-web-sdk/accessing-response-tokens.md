---
title: Adobe Experience Platform Web SDK을 사용하여 응답 토큰 액세스
description: ' [!DNL Adobe Experience Platform Web SDK]을(를) 사용하여 응답 토큰에 액세스하는 방법을 알아봅니다.'
keywords: 개인화;target;adobe target;renderDecisions;sendEvent;decisionScopes;result.decisions,응답 토큰;
feature: AEP Web SDK
source-git-commit: f010ca54aac3c2a644a77fb2f88aff1996f6ddfe
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# 응답 토큰 액세스

[!DNL Adobe Target]에서 반환된 Personalization 콘텐츠에는 활동, 오퍼, 경험, 사용자 프로필, 지역 정보 등에 대한 세부 정보인 [응답 토큰](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)이(가) 포함되어 있습니다. 이러한 세부 정보는 서드파티 도구와 공유하거나 디버깅에 사용할 수 있습니다. [!DNL Target] 사용자 인터페이스에서 응답 토큰을 구성할 수 있습니다.

개인화 콘텐츠에 액세스하려면 이벤트를 전송할 때 콜백 함수를 제공하십시오. 이 콜백은 SDK이 서버로부터 성공적인 응답을 받은 후에 호출됩니다. 콜백에는 반환된 개인화 콘텐츠가 포함된 `result` 속성이 포함될 수 있는 `propositions` 개체가 제공됩니다. 다음은 콜백 함수를 제공하는 예입니다.

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

이 예에서 `result.propositions`은(는) 존재하는 경우 이벤트와 관련된 개인화 제안이 포함된 배열입니다. [의 콘텐츠에 대한 자세한 내용은 ](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content)개인화 콘텐츠 렌더링`result.propositions.`을 참조하십시오

웹 SDK에서 자동으로 렌더링된 모든 명제에서 모든 활동 이름을 수집하여 단일 배열로 푸시하려는 경우 그런 다음 단일 스토리지를 서드파티로 전송할 수 있습니다. 이 경우:

1. `result` 개체에서 제안을 추출합니다.
1. 각 제안을 반복합니다.
1. SDK이 제안을 제공했는지 확인합니다.
1. 그렇다면, 명제의 각 항목을 반복해라.
1. 응답 토큰이 포함된 개체인 `meta` 속성에서 활동 이름을 검색합니다.
1. 활동 이름을 배열에 푸시합니다.
1. 활동 이름을 서드파티에 보냅니다.

코드는 다음과 같습니다.

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    var activityNames = [];
    propositions.forEach(function(proposition) {
      if (proposition.renderAttempted) {
        proposition.items.forEach(function(item) {
          if (item.meta) {
            // item.meta contains the response tokens.
            var activityName = item.meta["activity.name"];
            // Ignore duplicates
            if (activityNames.indexOf(activityName) === -1) {
              activityNames.push(activityName);
            }
          }
        });
      }
    });
    // Now that activity names are in an array,
    // you can send them to a third party or use
    // them in some other way.
  });
```
