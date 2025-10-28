---
title: Adobe Target 벌크 프로필 업데이트 API
description: ' [!DNL Adobe Target] [!UICONTROL Bulk Profile Update API]을(를) 사용하여 타깃팅에 사용할 여러 방문자의 프로필 데이터를  [!DNL Target] 에 보내는 방법을 알아봅니다.'
feature: APIs/SDKs
contributors: https://github.com/icaraps
exl-id: 0f38d109-5273-4f73-9488-80eca115d44d
source-git-commit: 38ed32560170e5a8f472aa191bb5a24d4e13cde7
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 6%

---

# [!DNL Adobe Target Bulk Profile Update API]

[!DNL Adobe Target] [!UICONTROL Bulk Profile Update API]을(를) 사용하면 배치 파일을 사용하여 웹 사이트에 대한 여러 방문자의 사용자 프로필을 일괄적으로 업데이트할 수 있습니다.

[!UICONTROL Bulk Profile Update API]을(를) 사용하면 많은 사용자에 대한 프로필 매개 변수 형식의 자세한 방문자 프로필 데이터를 외부 소스에서 [!DNL Target]&#x200B;(으)로 편리하게 보낼 수 있습니다. 외부 소스에는 일반적으로 웹 페이지에서 사용할 수 없는 CRM(고객 관계 관리) 또는 POS(판매 지점) 시스템이 포함될 수 있습니다.

| 버전 | URL 예 | 기능 |
| --- | --- | --- |
| v1 | `http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/profile/batchUpdate` | 벌크 프로필 업데이트만 지원합니다. |
| v2 | `http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/v2/profile/batchUpdate` | <ul><li>프로필을 찾을 수 없는 경우 만듭니다.</li><li>행별 상태 업데이트.</li></ul> |

>[!NOTE]
>
>[!DNL Bulk Profile Update API]의 버전 2(v2)가 현재 버전입니다. 그러나 [!DNL Target]은(는) 버전 1(v1)을 계속 지원합니다.
>
>* [!DNL Target] 구현에서 익명 방문자에 대한 프로필 식별자 중 하나로 [!DNL Experience Cloud ID]&#x200B;(ECID)을 사용하는 경우 버전 2(v2) 배치 파일에서 키로 `pcId`을(를) 사용하지 마십시오. `pcId`의 v2와 함께 [!DNL Bulk Profile Update API]을(를) 사용하는 것은 ECID에 의존하지 않는 독립 실행형 [!DNL Target] 구현에만 사용됩니다.
>
>* 구현에서 프로필 식별에 ECID를 사용하고 일괄 처리 파일의 키로 `pcId`을(를) 사용하려면 API 버전 1(v1)을 사용하십시오.
>
>* 구현에서 프로필 식별에 `thirdPartyId`을(를) 사용하는 경우 키로 `thirdPartyId`을(를) 사용하여 API의 버전 2(v2)를 사용하십시오.

## [!UICONTROL Bulk Profile Update API]의 이점

* 프로필 속성의 개수에 대한 제한은 없습니다.
* 사이트를 통해 전송된 프로필 속성은 API를 통해 또는 그 반대로 업데이트할 수 있습니다.

## 주의 사항

* 묶음 파일의 크기는 50MB 미만이어야 합니다. 또한 총 행 수는 업로드당 500,000개 행을 초과하지 않아야 합니다.
* 업데이트는 일반적으로 1시간 이내에 발생하지만 반영하는 데 24시간 정도 소요될 수 있습니다.
* 후속 배치에서 24시간 동안 업로드할 수 있는 행 수에는 제한이 없습니다. 그러나 영업 시간 동안 처리 프로세스를 조절하여 다른 프로세스가 효율적으로 실행되도록 할 수도 있습니다.
* 동일한 thirdPartyIds 간에 mbox를 호출하지 않고 연속적인 v2 배치 업데이트를 호출하면 첫 번째 배치 업데이트 호출에서 업데이트된 속성을 재정의합니다.
* [!DNL Adobe]은(는) 일괄 처리 프로필 데이터의 100%가 Target에 온보딩되고 유지되므로 타깃팅에서 사용할 수 있다고 보장하지 않습니다. 현재 설계에서는 적은 비율의 데이터(대규모 프로덕션 배치의 최대 0.1%)가 온보딩되거나 보존되지 않을 수 있습니다.

## 배치 파일

프로필 데이터를 대량으로 업데이트하려면 배치 파일을 만듭니다. 배치 파일은 다음 샘플 파일과 유사한 쉼표로 구분된 값이 있는 텍스트 파일입니다.

``````
batch=pcId,param1,param2,param3,param4
123,value1
124,value1,,,value4
125,,value2
126,value1,value2,value3,value4
``````

>[!NOTE]
>
>`batch=` 매개 변수는 필수이며 파일의 시작 부분에 지정해야 합니다.

파일을 처리하기 위해 [!DNL Target] 서버에 대한 POST 호출에서 이 파일을 참조합니다. 배치 파일을 생성할 때 다음 사항을 고려하십시오.

* 파일의 첫 행은 열 머리글을 지정해야 합니다.
* 첫 번째 헤더는 `pcId` 또는 `thirdPartyId`이어야 합니다. [!UICONTROL Marketing Cloud visitor ID]은(는) 지원되지 않습니다. [!UICONTROL pcId]은(는) [!DNL Target]에서 생성한 visitorID입니다. `thirdPartyId`은(는) 클라이언트 응용 프로그램에서 지정한 ID이며, mbox 호출을 통해 [!DNL Target]&#x200B;(으)로 `mbox3rdPartyId`에 전달됩니다. 여기에서 `thirdPartyId`(으)로 참조되어야 합니다.
* 보안상의 이유로 배치 파일에서 지정하는 매개변수와 값은 UTF-8을 사용하여 URL로 인코딩되어야 합니다. HTTP 요청을 통해 처리하기 위해 매개 변수와 값을 다른 에지 노드로 전달할 수 있습니다.
* 매개 변수는 `paramName` 형식이어야 합니다. 매개 변수가 [!DNL Target]에 `profile.paramName`(으)로 표시됩니다.
* [!UICONTROL Bulk Profile Update API] v2를 사용하는 경우 각 `pcId`에 대해 모든 매개 변수 값을 지정할 필요는 없습니다. `pcId`에서 찾을 수 없는 `mbox3rdPartyId` 또는 [!DNL Target]에 대해 프로필이 만들어집니다. v1을 사용하는 경우 누락된 pcIds 또는 mbox3rdPartyIds에 대해 프로필이 만들어지지 않습니다.
* 묶음 파일의 크기는 50MB 미만이어야 합니다. 또한 총 행 수는 50만 개를 초과할 수 없습니다. 이 제한은 서버가 너무 많은 요청으로 침수되지 않도록 합니다.
* 여러 파일을 보낼 수 있습니다. 단, 하루에 보내는 모든 파일의 행 합계 합계는 각 클라이언트에 대해 100만 개를 초과할 수 없습니다.
* 업로드할 수 있는 속성 수에는 제한이 없습니다. 하지만 고객 속성, 프로필 API, Mbox 내 프로필 매개 변수 및 프로필 스크립트 출력을 포함하는 외부 프로필 데이터의 총 크기는 64KB를 초과할 수 없습니다.
* 매개 변수와 값은 대/소문자를 구분합니다.

## HTTP POST 요청

파일을 처리할 [!DNL Target] Edge Server에 대한 HTTP POST 요청을 만듭니다. 다음은 curl 명령을 사용한 batch.txt 파일에 대한 샘플 HTTP POST 요청입니다.

``````
curl -X POST --data-binary @BATCH.TXT http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/v2/profile/batchUpdate
``````

여기서

BATCH.TXT는 파일 이름입니다. CLIENTCODE는 [!DNL Target] 클라이언트 코드입니다.

클라이언트 코드를 모르는 경우 [!DNL Target] 사용자 인터페이스에서 **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**&#x200B;을(를) 클릭합니다. 클라이언트 코드는 [!UICONTROL Account Details] 섹션에 표시됩니다.

### 응답 검사

프로필 API는 &quot;batchStatus&quot; 아래의 링크와 함께 처리할 배치의 제출 상태를 특정 배치 작업의 전체 상태를 보여 주는 다른 URL로 반환합니다.

### API 응답 예

잘린 다음 코드는 프로필 API 응답의 예입니다.

```
<response>
    <success>true</success>
    <batchStatus>http://mboxedge45.tt.omtrdc.net/m2/demo/profile/batchStatus?batchId=demo-1701473848678-13029383</batchStatus>
    <message>Batch submitted for processing</message>
</response>
```

오류가 있는 경우 응답에는 `success=false`과(와) 오류에 대한 자세한 메시지가 포함됩니다.

### 기본 일괄 처리 상태 응답

위의 `batchStatus` URL 링크를 클릭했을 때 성공한 기본 응답은 다음과 같습니다.

```
<response><batchId>demo4-1701473848678-13029383</batchId><status>complete</status><batchSize>1</batchSize></response>
```

상태 필드에 필요한 값은 다음과 같습니다.

| 상태 | 세부 사항 |
| --- | --- |
| [!UICONTROL complete] | 프로필 배치 업데이트 요청이 완료되었습니다. |
| [!UICONTROL incomplete] | 프로필 배치 업데이트 요청이 아직 처리 중이며 완료되지 않았습니다. |
| [!UICONTROL stuck] | 프로필 배치 업데이트 요청이 중단되어 완료할 수 없습니다. |

### 자세한 배치 상태 URL 응답

매개 변수 `showDetails=true`을(를) 위의 `batchStatus` URL로 전달하여 보다 자세한 응답을 가져올 수 있습니다.

예:

```
http://mboxedge45.tt.omtrdc.net/m2/demo/profile/batchStatus?batchId=demo-1701473848678-13029383&showDetails=true
```

#### 자세한 응답

```
<response>
    <batchId>demo4-1701473848678-13029383</batchId>
    <status>complete</status>
    <batchSize>1</batchSize>
    <consumedCount>1</consumedCount>
    <successfulUpdates>1</successfulUpdates>
    <profilesNotFound>0</profilesNotFound>
    <failedUpdates>0</failedUpdates>
</response>
```

## [!DNL Bulk Profile Update API]의 빈 값 처리에 대한 설명

[!DNL Target] [!DNL Bulk Profile Update API]&#x200B;(v1 또는 v2)을 사용할 때 시스템에서 빈 매개 변수 또는 특성 값을 처리하는 방법을 이해하는 것이 중요합니다.

### 예상 동작

기존 매개 변수 또는 속성에 대해 빈 값(&quot;&quot;, null 또는 누락 필드)을 전송해도 프로필 저장소에서 해당 값이 재설정되거나 삭제되지 않습니다. 이것은 계획적인 것이다.

빈 값은 무시됩니다. API는 불필요한 업데이트 또는 의미 없는 업데이트를 방지하기 위해 처리 중에 빈 값을 필터링합니다.

**기존 데이터를 지우지 않습니다**: 매개 변수에 이미 값이 있는 경우 빈 값을 보내면 값이 변경되지 않습니다.

**비어 있는 일괄 처리를 건너뜁니다**: 일괄 처리에 비어 있거나 null 값만 포함되어 있으면 일괄 처리가 완전히 무시되고 업데이트가 적용되지 않습니다.

### 추가 참고 사항

이 동작은 [!DNL Bulk Profile Update API]의 v1과 v2 모두에 적용됩니다.

빈 값을 전송하여 특성을 지우거나 제거하려고 시도해도 효과가 없습니다.

명시적 속성 제거에 대한 지원은 API의 향후 버전(v3)에 대해 계획되어 있지만 현재 사용할 수 없습니다.