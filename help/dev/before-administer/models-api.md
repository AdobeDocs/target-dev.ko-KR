---
title: Adobe 모델 API 개요
description: 사용자가 기능을 기계 학습 모델에 포함하지 않도록 차단하는 데 사용할 수 있는 모델 API의 개요입니다.
exl-id: e34b9b03-670b-4f7c-a94e-0c3cb711d8e4
feature: APIs/SDKs, Recommendations, Administration & Configuration
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '1289'
ht-degree: 2%

---

# 모델 API 개요

차단 목록에 추가하다 API라고도 하는 모델 API를 통해 사용자는 머신 러닝 모델에 사용되는 기능 목록을 조회하고 관리할 수 있습니다. [!UICONTROL Automated Personalization] (AP) 및 [!DNL Auto-Target] (AT) 활동. AP 또는 AT 활동용 모델에서 기능을 사용하지 않으려면 모델 API를 사용하여 해당 기능을 &quot;사용자 차단 목록&quot;에 추가할 수 있습니다.

A **[!UICONTROL 차단 목록]** 제외할 기능 세트를 정의합니다. [!DNL Adobe Target] 을 참조하십시오. 기능에 대한 자세한 내용은 [다음에 의해 사용된 데이터 [!DNL Target] 머신 러닝 알고리즘](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/ap-data.html).

차단 목록은 활동(활동 수준)별로 정의되거나 [!DNL Target] 계정(글로벌 수준).

<!-- To get started with the Models API in order to create and manage your blocklist, download the Postman Collection [here](https://git.corp.adobe.com/target/ml-configuration-management-service/tree/nextRelease/rest_api_library). Note this is an Adobe internal link. Need to publish this publicly if want to share with customers. -->

## 모델 API 사양

모델 API 사양 보기 [여기](../administer/models-api/models-api-overview.md).

## 전제 조건

모델 API를 사용하려면 다음을 사용하여 인증을 구성해야 합니다. [Adobe Developer 콘솔](https://developer.adobe.com/console/home), 다음과 같은 작업을 수행하는 것처럼 [Target 관리 API](../administer/admin-api/admin-api-overview-new.md). 자세한 내용은 [인증 구성 방법](../before-administer/configure-authentication.md).

## 모델 API 사용 지침

차단 목록 관리 방법

[**1단계:**](#step1) 활동에 대한 기능 목록 보기

[**2단계:**](#step2) 활동 차단 목록 확인

[**3단계:**](#step3) 활동 차단 목록에 기능 추가

[**4단계:**](#step4) (선택 사항) 차단 해제

[**5단계:**](#step5) (선택 사항) 글로벌 차단 목록 관리


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
>활동의 활동 ID를 찾으려면 [!DNL Target] UI. 관심 있는 활동을 클릭합니다. 활동 ID는 결과 활동 개요 페이지의 본문과 해당 페이지의 URL 끝에 표시됩니다.

다음 **[!UICONTROL externalName]** 은 기능의 사용자에게 친숙한 이름입니다. 작성자: [!DNL Target], 그리고 이 값은 시간이 지남에 따라 변경될 수 있습니다. 사용자는에서 사용자에게 친숙한 이러한 이름을 볼 수 있습니다. [개인화 통찰력 보고서](https://experienceleague.adobe.com/docs/target/using/reports/insights/personalization-insights-reports.html).

다음 **[!UICONTROL internalName]** 는 기능의 실제 식별자입니다. 또한 다음을 통해 생성됩니다. [!DNL Target], 그러나 변경할 수 없습니다. 이 값은 차단 목록에 추가하다와 같은 기능을 식별하기 위해 참조해야 하는 값입니다.

기능 목록을 값으로 채우려면(즉, null이 아니도록 하려면) 활동은 다음을 수행합니다.

1. Status = Live이거나 이전에 활성화했어야 합니다.
1. 모델이 실행할 데이터가 있도록 캠페인 활동이 있을 만큼 충분히 오래 실행되고 있었어야 합니다.

## 단계 2: 활동의 차단 목록 확인 {#step2}

다음은 차단 목록 보기. 즉, 현재 이 활동의 모델에 포함되지 못하고 있는 기능(있는 경우)을 확인합니다.

>[!ERROR]
>
>참고: `/blockList/` 은 요청에서 대/소문자를 구분합니다.

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
>기능을 추가하기 전에 전체 차단 목록을 처음 확인하면 이와 같은 빈 결과가 나타날 수 있습니다. 그러나 차단 목록에 추가하다 결과에서 기능을 추가(및 제거)하면 빈 차단 목록에 추가된 기능 배열이 반환되는 약간 다른 결과가 표시될 수 있습니다. 에서 이 예제를 보려면 계속 읽으십시오. [4단계](#step4).

## 단계 3: 활동의 차단 목록에 추가하다에 기능 추가 {#step3}

차단 목록에 추가하다에 기능을 추가하려면 요청을 PUT에서 GET으로 변경하고 요청 본문을 수정하여 `blockedFeatureSources` 또는 `blockedFeatures` 원하는 대로.

* 요청 본문에는 다음 중 하나가 필요합니다. `blockedFeatures` 또는 `blockedFeatureSources`. 둘 다 포함될 수 있습니다.
* 채우기 `blockedFeatures` 다음 위치에서 식별된 값 포함 `internalName`. 다음을 참조하십시오 [1단계](#step1).
* 채우기 `blockedFeatureSources` (아래 표의 값 포함)

참고: `blockedFeatureSources` 피쳐의 출처를 나타냅니다. 차단 목록에 추가 목적으로 기능은 사용자가 전체 기능 세트를 한 번에 차단할 수 있는 기능 그룹 또는 카테고리 역할을 합니다. 값: `blockedFeatureSources` 기능 식별자의 첫 번째 문자와 일치(`blockedFeatures` 또는 `internalName` 값). 따라서 &quot;기능 접두사&quot;로 간주할 수도 있습니다.

### 테이블 `blockedFeatureSources` 값 {#table}

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
| MOB | 모바일 |
| CRS | 사용자 지정 - 고객 속성 |
| UPA | 사용자 지정 - RT-CDP 프로필 속성 |
| IAC | 방문자 관심 영역 |  |

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

여기에 표시된 예에서는 사용자가 두 개의 기능을 차단하고 있습니다. `SES_PREVIOUS_VISIT_COUNT` 및 `SES_TOTAL_SESSIONS`에 설명된 대로 활동 ID가 260480 활동에 대한 전체 기능 목록을 쿼리하여 식별됩니다. [1단계](#step1). 또한 Experience Cloud 세그먼트에서 오는 모든 기능을 차단합니다. 이는 다음에 설명된 대로 &quot;AAM&quot;라는 접두사가 있는 기능을 차단함으로써 수행됩니다. [표](#table) 위.

![3단계](assets/models-api-step-3.png)

차단 목록에 추가 후 을 수행하여 업데이트된 차단 목록에 추가하다를 확인하는 것이 좋습니다 [2단계](#step2) 다시 GET 차단 목록에 추가하다. 결과가 예상대로 나타나는지 확인합니다(결과에 최신 PUT 요청에서 추가된 기능이 포함되어 있는지 확인).

## 4단계: (선택 사항) 차단 해제 {#step4}

모든 차단 목록에 추가된 기능을 차단 해제하려면 다음 값에서 값을 지웁니다. `blockedFeatureSources` 또는 `blockedFeatures`.

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

여기에 표시된 예에서 사용자는 활동 ID가 260840 활동에 대한 차단 목록에 추가하다를 지웁니다. 차단된 기능과 해당 소스에 대한 빈 배열이 응답에서 확인됩니다.`blockedFeatureSources` 및 `blockedFeatures`, 각각

![4단계](assets/models-api-step-4.png)

항상 그렇듯이 차단 목록에 추가하다를 수정한 후에는 다음을 수행하는 것이 좋습니다 [2단계](#step2) 다시 한 번(GET차단 목록에 추가하다 에 예상대로 기능이 포함되는지 확인). 여기에 표시된 예에서 사용자는 이제 차단 목록에 추가하다가 비어 있는지 확인하고 있습니다.

![4b단계](assets/models-api-step-4b.png)

질문: 어떻게 모든 것이 아니라 일부 차단 목록에 추가하다를 삭제할 수 있습니까?

답변: 다중 차단 목록에서 차단 목록에 추가된 기능의 개별 하위 집합을 제거하려면 사용자가 차단하려는 기능의 업데이트된 목록을 보내면 됩니다. [차단 목록에 추가하다 요청](#step3)를 설정하는 대신 전체 차단 목록에 추가하다를 지우고 원하는 기능을 다시 추가합니다. 즉, 와 같이 업데이트된 기능 목록을 보냅니다. [3단계](#step3))를 클릭하여 차단 목록에 추가하다에서 &quot;삭제&quot;할 기능을 제외합니다.

## 단계 5: (선택 사항) 글로벌 차단 목록 관리 {#step5}

위의 예는 모두 단일 활동의 맥락에 있었습니다. 각 활동에 대해 개별적으로 차단 목록에 추가하다를 지정하지 않고 주어진 클라이언트(테넌트)에서 모든 활동에 대한 기능을 차단할 수도 있습니다. 전역 차단 목록을 수행하려면 `/blockList/global` 대신 를 호출하십시오. `blockList/<campaignId>`.

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

위에 표시된 샘플 요청에서 사용자는 의 모든 활동에 대해 &quot;AAM_FEATURE_1&quot;과 &quot;AAM_FEATURE_2&quot;라는 두 개의 기능을 차단합니다 [!DNL Target] 계정입니다. 즉, 활동에 관계없이 &quot;AAM_FEATURE_1&quot; 및 &quot;AAM_FEATURE_2&quot;는 이 계정의 머신 러닝 모델에 포함되지 않습니다. 또한 접두사가 &quot;AAM&quot;, &quot;PRO&quot; 또는 &quot;ENV&quot;인 모든 기능을 전역적으로 차단합니다.

질문: 위의 코드 샘플은 중복되지 않습니까?

답변: 예. 값이 &quot;AAM&quot;로 시작하는 기능을 차단하는 동시에 소스가 &quot;AAM&quot;인 모든 기능을 차단하는 것은 이중화됩니다. 결과적으로 AAM(Experience Cloud 세그먼트)에서 가져온 모든 기능이 차단됩니다. 따라서 Experience Cloud 세그먼트에서 모든 기능을 차단하는 것이 목표라면 위의 예에서 &quot;AAM&quot;로 시작하는 특정 기능을 개별적으로 지정할 필요가 없습니다.

마지막 단계: 활동 수준이든 글로벌 수준이든, 활동 수준을 수정한 후 차단 목록에 추가하다를 확인하는 것이 좋습니다. 이렇게 하면 예상한 값이 포함됩니다. 다음을 변경하여 이 작업을 수행합니다. `PUT` (으)로 `GET`.

아래 표시된 샘플 응답은 다음을 나타냅니다. [!DNL Target] 는 두 개의 개별 기능과 &quot;AAM&quot;, &quot;PRO&quot; 및 &quot;ENV&quot;에서 제공되는 모든 기능을 차단합니다.

![5단계](assets/models-api-step-5.png)
