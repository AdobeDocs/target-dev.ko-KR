---
title: Adobe 모델 API 개요
description: 사용자가 기능을 기계 학습 모델에 포함하지 않도록 차단하는 데 사용할 수 있는 모델 API의 개요입니다.
exl-id: e34b9b03-670b-4f7c-a94e-0c3cb711d8e4
feature: APIs/SDKs, Recommendations, Administration & Configuration
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '1288'
ht-degree: 2%

---

# 모델 API 개요

차단 목록에 추가하다 API라고도 하는 모델 API를 사용하면 사용자가 [!UICONTROL Automated Personalization]&#x200B;(AP) 및 [!DNL Auto-Target]&#x200B;(AT) 활동에 대한 머신 러닝 모델에 사용되는 기능 목록을 보고 관리할 수 있습니다. AP 또는 AT 활동용 모델에서 기능을 사용하지 않으려면 모델 API를 사용하여 해당 기능을 &quot;사용자 차단 목록&quot;에 추가할 수 있습니다.

**[!UICONTROL blocklist]**&#x200B;은(는) [!DNL Adobe Target]이(가) 해당 기계 학습 모델에서 제외할 기능 집합을 정의합니다. 기능에 대한 자세한 내용은 [사용한 데이터 [!DNL Target] 머신 러닝 알고리즘](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/ap-data.html)을 참조하십시오.

차단 목록은 활동(활동 수준)별로 정의되거나 [!DNL Target] 계정(전역 수준) 내의 모든 활동에 대해 정의될 수 있습니다.

<!-- To get started with the Models API in order to create and manage your blocklist, download the Postman Collection [here](https://git.corp.adobe.com/target/ml-configuration-management-service/tree/nextRelease/rest_api_library). Note this is an Adobe internal link. Need to publish this publicly if want to share with customers. -->

## 모델 API 사양

모델 API 사양 [여기](../administer/models-api/models-api-overview.md)를 봅니다.

## 사전 요구 사항

모델 API를 사용하려면 [Target 관리 API](https://developer.adobe.com/console/home)에서와 마찬가지로 [Adobe Developer Console](../administer/admin-api/admin-api-overview-new.md)을(를) 사용하여 인증을 구성해야 합니다. 자세한 내용은 [인증을 구성하는 방법](../before-administer/configure-authentication.md)을 참조하세요.

## 모델 API 사용 지침

차단 목록 관리 방법

[**1단계:**](#step1) 활동에 대한 기능 목록 보기

[**2단계:**](#step2) 활동 차단 목록 확인

[**단계 3:**](#step3) 활동의 차단 목록에 추가하다에 기능 추가

[**4단계:**](#step4)(선택 사항) 차단 해제

[**단계 5:**](#step5)(선택 사항) 전역 차단 목록 관리


## 1단계: 활동에 대한 기능 목록 보기 {#step1}

기능을 차단 목록에 추가 하기 전에 해당 활동에 대한 모델에 현재 포함되어 있는 기능 목록을 확인하십시오.

>[!BEGINTABS]

>[!TAB 요청]

```json {line-numbers="true"}
GET https://mc.adobe.io/<tenant>/target/models/features/<campaignId>
```

>[!TAB 응답]

```json {line-numbers="true"}
{
    "features": [
        {
            "externalName": "Visitor Profile - Total Visits to Activity",
            "internalName": "SES_PREVIOUS_VISIT_COUNT",
            "type": "CONTINUOUS"
        },
        {
            "externalName": "Visitor Profile - Total Visits",
            "internalName": "SES_TOTAL_SESSIONS",
            "type": "CONTINUOUS"
        },
        {
            "externalName": "Visitor Profile - Pages Seen Before Activity",
            "internalName": "SES_PREVIOUS_VISIT_COUNT",
            "type": "CONTINUOUS"
        },
        {
            "externalName": "Visitor Profile - Activity Lifetime Time on Site",
            "internalName": "SES_TOTAL_TIME",
            "type": "CONTINUOUS"
        }
    ],
    "reportParameters": {
        "clientCode": <tenant>,
        "campaignId": <campaignId>
    }
}
```

>[!ENDTABS]

<!-- JUDY: Update codeblock above once you have the complete Response. -->

여기에 표시된 예에서 사용자는 활동 ID가 260840 활동에 대해 모델에서 사용 중인 기능 목록을 보기 위해 확인하고 있습니다.

![1단계](assets/models-api-step-1.png)

>[!NOTE]
>
>활동의 활동 ID를 찾으려면 [!DNL Target] UI에서 활동 목록으로 이동합니다. 관심 있는 활동을 클릭합니다. 활동 ID는 결과 활동 개요 페이지의 본문과 해당 페이지의 URL 끝에 표시됩니다.

**[!UICONTROL externalName]**&#x200B;은(는) 기능에 대한 알기 쉬운 이름입니다. 이 값은 [!DNL Target]에 의해 만들어지며 시간이 지남에 따라 변경될 수 있습니다. 사용자는 [Personalization 인사이트 보고서](https://experienceleague.adobe.com/docs/target/using/reports/insights/personalization-insights-reports.html)에서 사용자에게 친숙한 이러한 이름을 볼 수 있습니다.

**[!UICONTROL internalName]**&#x200B;은(는) 기능의 실제 식별자입니다. 또한 [!DNL Target]에 의해 만들어졌지만 변경할 수 없습니다. 이 값은 차단 목록에 추가하다와 같은 기능을 식별하기 위해 참조해야 하는 값입니다.

기능 목록을 값으로 채우려면(즉, null이 아니도록 하려면) 활동은 다음을 수행합니다.

1. Status = Live이거나 이전에 활성화했어야 합니다.
1. 모델이 실행할 데이터가 있도록 캠페인 활동이 있을 만큼 충분히 오래 실행되고 있었어야 합니다.

## 단계 2: 활동의 차단 목록 확인 {#step2}

다음은 차단 목록 보기. 즉, 현재 이 활동의 모델에 포함되지 못하고 있는 기능(있는 경우)을 확인합니다.

>[!ERROR]
>
>`/blockList/`은(는) 요청에서 대/소문자를 구분합니다.

>[!BEGINTABS]

>[!TAB 요청]

```json {line-numbers="true"}
GET https://mc.adobe.io/<tenant>/target/models/features/blockList/<campaignId>
```

>[!TAB 응답]

```json {line-numbers="true"}

```

>[!ENDTABS]

여기에 표시된 예에서 사용자는 활동 ID가 260840 활동에 대해 차단된 기능 목록을 확인하고 있습니다. 결과가 비어 있습니다. 즉, 이 활동에는 현재 차단 목록에 추가된 기능이 없습니다.

![2단계](assets/models-api-step-2.png)

>[!NOTE]
>
>기능을 추가하기 전에 전체 차단 목록을 처음 확인하면 이와 같은 빈 결과가 나타날 수 있습니다. 그러나 차단 목록에 추가하다 결과에서 기능을 추가(및 제거)하면 빈 차단 목록에 추가된 기능 배열이 반환되는 약간 다른 결과가 표시될 수 있습니다. [4단계](#step4)에서 이 예제를 보려면 계속 읽으십시오.

## 단계 3: 활동의 차단 목록에 추가하다에 기능 추가 {#step3}

차단 목록에 추가하다에 기능을 추가하려면 GET에서 PUT으로 요청을 변경하고 요청 본문을 수정하여 `blockedFeatureSources` 또는 `blockedFeatures`을(를) 원하는 대로 지정하십시오.

* 요청 본문에는 `blockedFeatures` 또는 `blockedFeatureSources`이(가) 필요합니다. 둘 다 포함될 수 있습니다.
* `blockedFeatures`에서 식별된 값으로 `internalName`을(를) 채웁니다. [단계 1](#step1)을 참조하세요.
* 아래 표의 값으로 `blockedFeatureSources`을(를) 채웁니다.

`blockedFeatureSources`은(는) 기능의 출처를 나타냅니다. 차단 목록에 추가 목적으로 기능은 사용자가 전체 기능 세트를 한 번에 차단할 수 있는 기능 그룹 또는 카테고리 역할을 합니다. `blockedFeatureSources`의 값은 기능 식별자의 첫 번째 문자(`blockedFeatures` 또는 `internalName` 값)와 일치하므로 &quot;기능 접두사&quot;로 간주할 수도 있습니다.

### `blockedFeatureSources` 값 테이블 {#table}

| 접두사 | 설명 |
| --- | --- |
| 상자 | mbox 매개 변수 |
| URL | 사용자 지정 - URL 매개 변수 |
| 환경 | 환경 |
| SES | 방문자 프로필 |
| 지역 | 지리적 위치 |
| PRO | 사용자 지정 - 프로필 |
| SEG | 사용자 지정 - 보고 세그먼트 |
| AAM | 사용자 지정 - Experience Cloud 세그먼트 |
| 군중 | 모바일 |
| CRS | 사용자 지정 - 고객 속성 |
| UPA | 사용자 지정 - RT-CDP 프로필 속성 |
| IAC | 방문자 관심 영역 |

>[!BEGINTABS]

>[!TAB 요청]

```json {line-numbers="true"}
PUT https://mc.adobe.io/<tenant>/target/models/features/blockList/<campaignId>

{
    "blockedFeatureSources": ["AAM"],
    "blockedFeatures": ["SES_PREVIOUS_VISIT_COUNT", "SES_TOTAL_SESSIONS"]
}
```

>[!TAB 응답]

```json {line-numbers="true"}
{
    "blockedFeatures": [
            "SES_PREVIOUS_VISIT_COUNT",
            "SES_TOTAL_SESSIONS"
        ],
    "blockedFeatureSources": [
            "AAM"
        ]
}
```

>[!ENDTABS]

여기에 표시된 예에서 사용자는 `SES_PREVIOUS_VISIT_COUNT`단계 1`SES_TOTAL_SESSIONS`에 설명된 대로 활동 ID가 260480 활동에 대한 전체 기능 목록을 쿼리하여 이전에 식별한 두 개의 기능 [&#x200B; 및 &#x200B;](#step1)을(를) 차단하고 있습니다. 또한 위의 [표](#table)에 설명된 대로 &quot;AAM&quot;라는 접두사가 있는 기능을 차단하여 얻은 Experience Cloud 세그먼트에서 오는 모든 기능을 차단합니다.

![3단계](assets/models-api-step-3.png)

차단 목록에 추가 후 [2](#step2)을(를) 다시 수행하여 업데이트된 차단 목록 단계를 확인하는 것이 좋습니다(GET 차단 목록에 추가하다). 결과가 예상대로 표시되는지 확인합니다(결과에 최신 PUT 요청에서 추가된 기능이 포함되어 있는지 확인).

## 4단계: (선택 사항) 차단 해제 {#step4}

모든 차단 목록에 추가된 기능을 차단 해제하려면 `blockedFeatureSources` 또는 `blockedFeatures`에서 값을 지우십시오.

>[!BEGINTABS]

>[!TAB 요청]

```json {line-numbers="true"}
PUT https://mc.adobe.io/<tenant>/target/models/features/blockList/<campaignId>

{
    "blockedFeatureSources": [],
    "blockedFeatures": []
}
```

>[!TAB 응답]

```json {line-numbers="true"}
{
    "blockedFeatures": [],
    "blockedFeatureSources": []
}
```

>[!ENDTABS]

여기에 표시된 예에서 사용자는 활동 ID가 260840 활동에 대한 차단 목록에 추가하다를 지웁니다. 응답이 차단된 기능과 해당 소스 모두에 대해 빈 배열을 확인합니다. 각각—`blockedFeatureSources` 및 `blockedFeatures`.

![4단계](assets/models-api-step-4.png)

차단 목록에 추가하다 차단 목록에 추가하다를 수정하는 경우 항상 그렇듯이 [2단계](#step2)를 다시 수행하는 것이 좋습니다(예상대로 GET에 기능이 포함되어 있는지 확인). 여기에 표시된 예에서 사용자는 이제 차단 목록에 추가하다가 비어 있는지 확인하고 있습니다.

![4b단계](assets/models-api-step-4b.png)

질문: 어떻게 모든 것이 아니라 일부 차단 목록에 추가하다를 삭제할 수 있습니까?

답변: 다중 차단 목록에 추가된 기능의 개별 하위 집합을 제거하기 위해 사용자는 전체 차단 목록에 추가하다차단 목록에 추가하다 을 지우고 원하는 기능을 다시 추가하는 것에 반대하므로 [차단 목록에 추가하다 요청](#step3)에서 차단하고자 하는 기능의 업데이트된 목록을 보내면 됩니다. 즉, 업데이트된 기능 목록([3](#step3)단계)을 보내 차단 목록에서 &quot;삭제&quot;할 기능을 제외하도록 합니다.

## 단계 5: (선택 사항) 글로벌 차단 목록 관리 {#step5}

위의 예는 모두 단일 활동의 맥락에 있었습니다. 각 활동에 대해 개별적으로 차단 목록에 추가하다를 지정하지 않고 주어진 클라이언트(테넌트)에서 모든 활동에 대한 기능을 차단할 수도 있습니다. 전역 차단 목록을 수행하려면 `/blockList/global` 대신 `blockList/<campaignId>` 호출을 사용하십시오.

>[!BEGINTABS]

>[!TAB 요청]

```json {line-numbers="true"}
PUT https://mc.adobe.io/<tenant>/target/models/features/blockList/global

{
    "blockedFeatureSources": ["AAM", "PRO", "ENV"],
    "blockedFeatures": ["AAM_FEATURE_1", "AAM_FEATURE_2"]
}
```

>[!TAB 응답]

```json {line-numbers="true"}
{
    "blockedFeatures": [
        "AAM_FEATURE_1",
        "AAM_FEATURE_2"
    ],
    "blockedFeatureSources": [
        "AAM",
        "PRO",
        "ENV"
    ]
}
```

>[!ENDTABS]

위에 표시된 샘플 요청에서 사용자는 [!DNL Target] 계정의 모든 활동에 대해 두 개의 기능인 &quot;AAM_FEATURE_1&quot; 및 &quot;AAM_FEATURE_2&quot;를 차단하고 있습니다. 즉, 활동에 관계없이 &quot;AAM_FEATURE_1&quot; 및 &quot;AAM_FEATURE_2&quot;는 이 계정의 머신 러닝 모델에 포함되지 않습니다. 또한 사용자는 접두사가 &quot;AAM&quot;, &quot;PRO&quot; 또는 &quot;ENV&quot;인 모든 기능을 전역적으로 차단하고 있습니다.

질문: 위의 코드 샘플은 중복되지 않습니까?

답변: 예. 값이 &quot;AAM&quot;로 시작하는 기능을 차단하는 동시에 소스가 &quot;AAM&quot;인 모든 기능을 차단하는 것은 이중화됩니다. 그 결과, AAM(Experience Cloud 세그먼트)에서 가져온 모든 기능이 차단됩니다. 따라서, 목표가 Experience Cloud 세그먼트에서 모든 기능을 차단하는 것이면 위의 예에서 &quot;AAM&quot;로 시작하는 특정 기능을 개별적으로 지정할 필요가 없습니다.

마지막 단계: 활동 수준이든 글로벌 수준이든, 활동 수준을 수정한 후 차단 목록에 추가하다를 확인하는 것이 좋습니다. 이렇게 하면 예상한 값이 포함됩니다. `PUT`을(를) `GET`(으)로 변경하여 이 작업을 수행합니다.

아래 표시된 샘플 응답은 [!DNL Target]이(가) 두 개의 개별 기능과 &quot;AAM&quot;, &quot;PRO&quot; 및 &quot;ENV&quot;에서 가져온 모든 기능을 차단함을 나타냅니다.

![5단계](assets/models-api-step-5.png)
