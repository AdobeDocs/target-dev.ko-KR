---
title: 개인화에  [!DNL Adobe Target] with [!DNL Web SDK] 을(를) 사용합니다.
description: ' [!DNL Experience Platform Web SDK] 사용 [!DNL Adobe Target]을 통해 개인화된 콘텐츠를 렌더링하는 방법을 알아봅니다.'
feature: AEP Web SDK
source-git-commit: 1fe6adc25604612ed9fa090f1f68c18b9c0bdf63
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 5%

---

# 개인화에 [!DNL Adobe Target] 및 [!DNL Web SDK] 사용

[!DNL Adobe Experience Platform] [!DNL Web SDK]은(는) [!DNL Adobe Target]에서 관리되는 개인화된 경험을 웹 채널에 전달하고 렌더링할 수 있습니다. VEC([시각적 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html))라고 하는 WYSIWYG 편집기 또는 [양식 기반 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html))를 사용하여 활동 및 개인화 경험을 만들고, 활성화하고, 전달할 수 있습니다.

>[!IMPORTANT]
>
>[!DNL Target]Target을 at.js 2.x에서 Experience Platform Web SDK으로 마이그레이션[!DNL Experience Platform Web SDK] 자습서를 사용하여 [ 구현을 ](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html)&#x200B;(으)로 마이그레이션하는 방법을 알아봅니다.
>
>[!DNL Target]Web SDK에서 Adobe Experience Cloud 구현[ 자습서를 사용하여 처음으로 ](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html)을(를) 구현하는 방법을 알아봅니다. [!DNL Target]에 대한 자세한 내용은 [Experience Platform Web SDK으로 Target 설정](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html)이라는 자습서 섹션을 참조하십시오.

다음 기능이 테스트되었으며 현재 [!DNL Target]에서 지원됩니다.

* [A/B 테스트](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [A4T 노출 및 전환 보고](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)
* [Automated Personalization 활동](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [경험 타깃팅 활동](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [MVT(다변량 테스트)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [권장 사항 활동](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [기본 대상 노출 및 전환 보고](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [VEC 지원](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Web SDK] 시스템 다이어그램

다음 다이어그램은 [!DNL Target] 및 [!DNL Web SDK] Edge Decisioning의 워크플로를 이해하는 데 도움이 됩니다.

![Experience Platform Web SDK을 사용한 Adobe Target Edge Decisioning 다이어그램](/help/dev/implement/client-side/aep-web-sdk/assets/target-platform-web-sdk-new.png)

| 호출 | 세부 사항 |
| --- | --- |
| 1 | 장치가 [!DNL Web SDK]을(를) 로드합니다. [!DNL Web SDK]이(가) XDM 데이터, 데이터스트림 환경 ID, 전달된 매개 변수 및 고객 ID(선택 사항)를 사용하여 Edge Network에 요청을 보냅니다. 페이지(또는 컨테이너)가 미리 숨겨져 있습니다. |
| 2 | Edge Network은 Edge Services에 요청을 전송하여 방문자 ID, 동의 및 지리적 위치 및 장치에 친숙한 이름과 같은 기타 방문자 컨텍스트 정보로 이를 보강합니다. |
| 3 | Edge Network이 방문자 ID 및 전달된 매개 변수와 함께 보강된 개인화 요청을 [!DNL Target] 에지에 보냅니다. |
| 4 | 프로필 스크립트가 실행된 다음 [!DNL Target] 프로필 저장소에 공급됩니다. 프로필 저장소는 [!UICONTROL Audience Library]의 세그먼트(예: [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], [!DNL Adobe Experience Platform]에서 공유된 세그먼트)를 가져옵니다. |
| 5 | [!DNL Target]은(는) URL 요청 매개 변수 및 프로필 데이터를 기반으로 현재 페이지 보기 및 향후 프리페치된 보기에 대해 방문자에게 표시할 활동 및 경험을 결정합니다. [!DNL Target]이(가) Edge Network으로 다시 보냅니다. |
| 6 | a. Edge Network은 추가적인 개인화를 위한 프로필 값을 선택적으로 포함하여 개인화 응답을 다시 페이지로 전송합니다. 현재 페이지의 개인화된 콘텐츠는 기본 콘텐츠의 플리커 없이 가능한 한 빨리 나타납니다.<br>b. SPA(단일 페이지 애플리케이션)에서 사용자 작업의 결과로 표시되는 보기의 개인화된 콘텐츠는 캐시되므로 보기가 트리거될 때 추가적인 서버 호출 없이 즉시 적용될 수 있습니다. <br>c입니다. Edge Network은 방문자 ID와 동의, 세션 ID, ID, 쿠키 확인, 개인화와 같은 쿠키의 다른 값을 보냅니다. |
| 7 | 웹 SDK은 장치에서 Edge Network으로 알림을 보냅니다. |
| 8 | Edge Network은 [!UICONTROL Analytics for Target]&#x200B;(A4T) 세부 정보(활동, 경험 및 전환 메타데이터)를 [!DNL Analytics] 에지에 전달합니다. |

## [!DNL Adobe Target] 사용

[!DNL Target]을(를) 사용하려면 다음을 수행하십시오.

1. 적절한 클라이언트 코드를 사용하여 [!DNL Target]데이터스트림[에서 ](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview)을(를) 사용하도록 설정하십시오.
1. 이벤트에 `renderDecisions` 옵션을 추가합니다.

그런 다음 선택적으로 다음 옵션을 추가할 수도 있습니다.

* **`decisionScopes`**: 이 옵션을 이벤트에 추가하여 특정 활동(양식 기반 작성기로 만든 활동에 유용함)을 검색합니다.
* **[코드 조각 사전 숨김](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/manage-flicker)**: 페이지의 특정 부분만 숨깁니다.

## [!UICONTROL Adobe Target] VEC 사용

VEC를 [!DNL Web SDK] 구현과 함께 사용하려면 [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) 또는 [Chrome](https://experienceleague.adobe.com/en/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension) VEC Helper 확장 프로그램을 설치하고 활성화하십시오.

자세한 내용은 [Adobe Target 안내서](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html)에서 *시각적 경험 작성기 Helper 확장 기능*&#x200B;을 참조하십시오.

## 개인화된 콘텐츠 렌더링

자세한 내용은 [개인화 콘텐츠 렌더링](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content)을 참조하십시오.

## XDM의 대상

[!DNL Target]을(를) 통해 전달되는 [!DNL Web SDK] 활동에 대한 대상을 정의할 때 [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html)을(를) 정의하고 사용해야 합니다. XDM 스키마, 클래스 및 스키마 필드 그룹을 정의한 후에는 타깃팅을 위해 XDM 데이터로 정의된 [!DNL Target] 대상 규칙을 만들 수 있습니다. [!DNL Target] 내에서 XDM 데이터가 [!UICONTROL Audience Builder]에 사용자 지정 매개 변수로 표시됩니다. XDM은 점 표기법을 사용하여 serialize됩니다(예: `web.webPageDetails.name`).

사용자 지정 매개 변수 또는 사용자 프로필을 사용하는 사전 정의된 대상이 있는 [!DNL Target] 활동이 있는 경우 SDK을 통해 올바르게 전달되지 않습니다. 사용자 지정 매개 변수 또는 사용자 프로필을 사용하는 대신 XDM을 사용해야 합니다. 그러나 XDM이 필요하지 않은 [!DNL Web SDK]을(를) 통해 지원되는 기본 대상 타깃팅 필드가 있습니다. 이러한 필드는 XDM이 필요하지 않은 [!DNL Target] UI에서 사용할 수 있습니다.

* 타겟 라이브러리
* 지역
* 네트워크
* 운영 체제
* 사이트 페이지
* 브라우저
* 트래픽 소스
* 시간대

자세한 내용은 [Adobe Target 안내서](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html)의 *대상 범주*&#x200B;를 참조하십시오.

### 응답 토큰

응답 토큰은 Google 또는 Facebook과 같은 서드파티에 메타데이터를 전송하는 데 사용됩니다. 응답 토큰이 반환됩니다
`meta` > `propositions` 내의 `items` 필드에서 다음을 수행합니다.

다음은 샘플입니다.

```json
{
  "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI2NzM2IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
  "scope": "__view__",
  "scopeDetails": ...,
  "renderAttempted": true,
  "items": [
    {
      "id": "0",
      "schema": "https://ns.adobe.com/personalization/dom-action",
      "meta": {
        "experience.id": "0",
        "activity.id": "126736",
        "offer.name": "Default Content",
        "offer.id": "0"
      }
    }
  ]
}
```

응답 토큰을 수집하려면 `alloy.sendEvent` 약속을 구독하고 `propositions`을(를) 반복한 다음 `items` -> `meta`에서 세부 정보를 추출해야 합니다.

`proposition`마다 `renderAttempted`이(가) 렌더링되었는지 여부를 나타내는 `proposition` 부울 필드가 있습니다. 아래 샘플을 참조하십시오.

```js
alloy("sendEvent",
  {
    "renderDecisions": true,
    "decisionScopes": [
      "hero-container"
    ]
  }).then(result => {
    const { propositions } = result;

    // filter rendered propositions
    const renderedPropositions = propositions.filter(proposition => proposition.renderAttempted === true);

    // collect the item metadata that represents the response tokens
    const collectMetaData = (items) => {
      return items.filter(item => item.meta !== undefined).map(item => item.meta);
    }

    const pageLoadResponseTokens = renderedPropositions
      .map(proposition => collectMetaData(proposition.items))
      .filter(e => e.length > 0)
      .flatMap(e => e);
  });
  
```

자동 렌더링이 활성화된 경우 제안 배열에 다음이 포함됩니다.

#### 페이지 로드 시:

* `propositions` 플래그가 `renderAttempted`(으)로 설정된 양식 기반 작성기 기반 `false`
* `renderAttempted` 플래그가 `true`(으)로 설정된 시각적 경험 작성기 기반 제안
* `renderAttempted` 플래그가 `true`(으)로 설정된 단일 페이지 애플리케이션 보기에 대한 시각적 경험 작성기 기반 제안

#### 보기 - 변경(캐시된 보기):

* `renderAttempted` 플래그가 `true`(으)로 설정된 단일 페이지 애플리케이션 보기에 대한 시각적 경험 작성기 기반 제안

자동 렌더링이 비활성화되면 제안 배열에 다음이 포함됩니다.

#### 페이지 로드 시:

* [!DNL Form-based Composer] 플래그가 `propositions`(으)로 설정된 `renderAttempted` 기반 `false`
* [!DNL Visual Experience Composer] 플래그가 `renderAttempted`(으)로 설정된 `false` 기반 제안
* [!DNL Visual Experience Composer] 플래그가 `renderAttempted`(으)로 설정된 단일 페이지 응용 프로그램 보기에 대한 `false` 기반 제안

#### 보기 - 변경(캐시된 보기):

* `renderAttempted` 플래그가 `false`(으)로 설정된 단일 페이지 애플리케이션 보기에 대한 시각적 경험 작성기 기반 제안

### 단일 프로필 업데이트

[!DNL Web SDK]을(를) 사용하면 프로필을 [!DNL Target] 프로필로 업데이트하고 [!DNL Web SDK]을(를) 경험 이벤트로 업데이트할 수 있습니다.

[!DNL Target] 프로필을 업데이트하려면 프로필 데이터가 다음과 함께 전달되었는지 확인하십시오.

* `"data {"` 아래
* `"__adobe.target"` 아래
* 접두사 `"profile."`

| 키 | 유형 | 설명 |
| --- | --- | --- |
| `renderDecisions` | 부울 | DOM 작업을 해석해야 하는지 여부를 개인화 구성 요소에 지시합니다. |
| `decisionScopes` | 배열 `<String>` | 결정을 검색할 범위 목록 |
| `xdm` | 개체 | 웹 SDK에 경험 이벤트로 전송되는 XDM 형식의 데이터 |
| `data` | 개체 | 대상 클래스 아래의 [!DNL Target] 솔루션으로 전송된 임의의 키/값 쌍입니다. |

<!--Typical [!DNL Web SDK] code using this command looks like the following:-->

**콘텐츠가 최종 사용자에게 표시될 때까지 프로필 또는 엔터티 매개 변수 저장 지연**

콘텐츠가 표시될 때까지 프로필의 기록 특성을 지연하려면 요청에서 `data.adobe.target._save=false`을(를) 설정하십시오.

예를 들어 웹 사이트에는 웹 사이트의 세 범주 링크(남성, 여성 및 아동)에 해당하는 세 가지 결정 범위가 포함되어 있으며 사용자가 최종적으로 방문한 범주를 추적하려고 합니다. 콘텐츠가 요청될 때 범주가 지속되지 않도록 `__save` 플래그를 `false`(으)로 설정하여 이러한 요청을 보냅니다. 콘텐츠가 시각화되면 기록할 해당 특성에 대한 적절한 페이로드(`eventToken` 및 `stateToken` 포함)를 보냅니다.

아래 예제에서는 trackEvent 스타일 메시지를 보내고, 프로필 스크립트를 실행하고, 속성을 저장하고, 이벤트를 즉시 기록합니다.

```js
alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": { /* Experience Event XDM data */ },
    "data": {
        "__adobe": {
            "target": {
                " __save": true|false,
                //defaults to true if omitted
                "profile.gender": "female",
                "profile.age": 30,
                "entity.name": "T-shirt",
                "entity.id": "1234"
            }
        }
    }
})
```

>[!NOTE]
>
>`__save` 지시문이 생략되면 프로필 및 엔티티 속성이 즉시 저장됩니다. `__save` 지시문은 프로필 특성 및 엔터티 세부 사항에만 관련됩니다.

## 권장 사항 요청

다음 표에는 [!DNL Recommendations] 특성과 각 특성이 [!DNL Web SDK]을(를) 통해 지원되는지 여부가 나열되어 있습니다.

| 카테고리 | 속성 | 지원 상태 |
| --- | --- | --- |
| 권장 사항 - 기본 엔티티 속성 | entity.id | 지원됨 |
|  | entity.name | 지원됨 |
|  | entity.categoryId | 지원됨 |
|  | entity.pageUrl | 지원됨 |
|  | entity.thumbnailUrl | 지원됨 |
|  | entity.message | 지원됨 |
|  | entity.value | 지원됨 |
|  | entity.inventory | 지원됨 |
|  | entity.brand | 지원됨 |
|  | entity.margin | 지원됨 |
|  | entity.event.detailsOnly | 지원됨 |
| 권장 사항 - 사용자 지정 엔티티 속성 | entity.yourCustomAttributeName | 지원됨 |
| 권장 사항 - 예약된 mbox/페이지 매개 변수 | excludedIds | 지원됨 |
|  | cartIds | 지원됨 |
|  | productPurchasedId | 지원됨 |
| 카테고리 관심도에 대한 페이지 또는 항목 카테고리 | user.categoryId | 지원됨 |

**Recommendations 특성을 [!DNL Target]에 보내는 방법:**

```js
alloy("sendEvent", {
  "renderDecisions": true,
  "data": {
    "__adobe": {
      "target": {
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```

## mbox 전환 지표 표시 {#display-mbox-conversion-metrics}

아래 샘플은 콘텐츠나 활동에 대한 자격이 없어도 디스플레이 mbox 전환을 추적하고 프로필 매개 변수를 [!DNL Target]에 보내는 방법을 보여 줍니다.

```js
alloy("sendEvent", {
    "xdm": {
        "_experience": {
            "decisioning": {
                "propositions": [{
                    "scope": "conversion-step-1" //example scope name
                }],
                "propositionEventType": {
                    "display": 1
                }
            }
        },
        "eventType": "decisioning.propositionDisplay"
    }
});
```


| 속성 | 설명 |
|---------|----------|
| `xdm._experience.decisioning.propositions[x].scope` | 성공 지표를 와 연결할 범위입니다(Target 측의 특정 활동에 기여함). |
| `xdm._experience.decisioning.propositions[x].eventType` | 의도한 이벤트 유형을 설명하는 문자열입니다. 이 사용 사례에 대해 `"decisioning.propositionDisplay"`(으)로 설정하십시오. |

## 디버깅

mboxTrace 및 mboxDebug는 더 이상 사용되지 않습니다. 대신 [웹 SDK 디버깅](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/use-cases/debugging)의 메서드를 사용하십시오.

## Terminology

**제안**: [!DNL Target]에서 제안은 활동에서 선택한 경험과 상관 관계가 있습니다.

**스키마**: 결정의 스키마가 [!DNL Target]의 오퍼 유형입니다.

**범위**: 결정 범위입니다. [!DNL Target]에서 범위는 mbox입니다. 글로벌 mbox가 `__view__` 범위입니다.

**XDM**: XDM이 점 표기법으로 serialize된 다음 mbox 매개 변수로 [!DNL Target]에 삽입됩니다.
