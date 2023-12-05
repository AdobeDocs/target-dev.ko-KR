---
title: Adobe Target 벌크 프로필 업데이트 API
description: 사용 방법 알아보기 [!DNL Adobe Target] [!UICONTROL 벌크 프로필 업데이트 API] 여러 방문자의 프로필 데이터를 다음으로 보내기 [!DNL Target].
feature: APIs/SDKs
contributors: https://github.com/icaraps
source-git-commit: b263fef6017dc6f840037cab9045c36b9e354cee
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 9%

---

# [!DNL Adobe Target Bulk Profile Update API]

다음 [!DNL Adobe Target] [!UICONTROL 벌크 프로필 업데이트 API] 배치 파일을 사용하여 웹 사이트에 대한 여러 방문자의 사용자 프로필을 일괄적으로 업데이트할 수 있습니다.

사용 [!UICONTROL 벌크 프로필 업데이트 API], 많은 사용자에 대해 프로필 매개 변수 형식으로 자세한 방문자 프로필 데이터를 편리하게 보낼 수 있습니다. [!DNL Target] 모든 외부 소스에서 외부 소스에는 일반적으로 웹 페이지에서 사용할 수 없는 CRM(고객 관계 관리) 또는 POS(판매 지점) 시스템이 포함될 수 있습니다.

| 버전 | URL 예 | 기능 |
| --- | --- | --- |
| v1 | `http://CLIENTCODE.tt.omtrdc.net/m2/ CLIENTCODE/profile/batchUpdate` | 벌크 프로필 업데이트만 지원합니다. |
| v2 | `http://CLIENTCODE.tt.omtrdc.net/m2/ CLIENTCODE/v2/profile/batchUpdate` | <ul><li>프로필을 찾을 수 없는 경우 만듭니다.</li><li>행별 상태 업데이트.</li></ul> |

>[!NOTE]
>
>버전 2(v2) [!UICONTROL 벌크 프로필 업데이트 API] 는 현재 버전입니다. 그러나 [!DNL Target] 는 여전히 버전 1(v1)을 지원합니다.

## 벌크 프로필 업데이트 API의 이점

* 프로필 속성의 개수에 대한 제한은 없습니다.
* 사이트를 통해 전송된 프로필 속성은 API를 통해 또는 그 반대로 업데이트할 수 있습니다.

## 주의 사항

* 묶음 파일의 크기는 50MB 미만이어야 합니다. 또한 총 행 수는 업로드당 500,000개 행을 초과하지 않아야 합니다.
* 후속 배치에서 24시간 동안 업로드할 수 있는 행 수에는 제한이 없습니다. 그러나 영업 시간 동안 처리 프로세스를 조절하여 다른 프로세스가 효율적으로 실행되도록 할 수도 있습니다.
* 동일한 thirdPartyIds 간에 mbox를 호출하지 않고 연속적인 v2 배치 업데이트를 호출하면 첫 번째 배치 업데이트 호출에서 업데이트된 속성을 재정의합니다.

## 배치 파일

프로필 데이터를 대량으로 업데이트하려면 배치 파일을 만듭니다. 배치 파일은 다음 샘플 파일과 유사한 쉼표로 구분된 값이 있는 텍스트 파일입니다.

``````
batch=pcId, param1, param2, param3, param4 123, value1 124, value1,,, value4 125,, value2 126, value1, value2, value3, value4
``````

에 대한 POST 호출에서 이 파일을 참조합니다. [!DNL Target] 파일을 처리할 서버. 배치 파일을 생성할 때 다음 사항을 고려하십시오.

* 파일의 첫 행은 열 머리글을 지정해야 합니다.
* 첫 번째 헤더는 다음 중 하나여야 합니다. `pcId` 또는 `thirdPartyId`. 다음 [!UICONTROL Marketing Cloud 방문자 ID] 은(는) 지원되지 않습니다. [!UICONTROL pcId] 다음 값: [!DNL Target]-생성된 visitorID입니다. `thirdPartyId` 는 클라이언트 응용 프로그램에서 지정한 ID이며, 로 전달됩니다. [!DNL Target] mbox 호출을 통해 `mbox3rdPartyId`. 이는 여기에서 다음과 같이 참조되어야 합니다. `thirdPartyId`.
* 보안상의 이유로 배치 파일에서 지정하는 매개변수와 값은 UTF-8을 사용하여 URL로 인코딩되어야 합니다. HTTP 요청을 통해 처리하기 위해 매개 변수와 값을 다른 에지 노드로 전달할 수 있습니다.
* 매개 변수는 형식이어야 합니다. `paramName` 만 해당. 매개변수는에 표시됩니다. [!DNL Target] 다음으로: `profile.paramName`.
* 을 사용하는 경우 [!UICONTROL 벌크 프로필 업데이트 API] v2, 각각에 대해 모든 매개 변수 값을 지정할 필요는 없습니다 `pcId`. 프로필은 다음에 대해 만들어집니다. `pcId` 또는 `mbox3rdPartyId` 에서 찾을 수 없음 [!DNL Target]. v1을 사용하는 경우 누락된 pcIds 또는 mbox3rdPartyIds에 대해 프로필이 만들어지지 않습니다.
* 묶음 파일의 크기는 50MB 미만이어야 합니다. 또한 총 행 수는 50만 개를 초과할 수 없습니다. 이 제한은 서버가 너무 많은 요청으로 침수되지 않도록 합니다.
* 여러 파일을 보낼 수 있습니다. 단, 하루에 보내는 모든 파일의 행 합계 합계는 각 클라이언트에 대해 100만 개를 초과할 수 없습니다.
* 업로드하는 속성의 수에는 제한이 없습니다. 그러나 시스템 데이터를 포함한 프로필의 전체 크기는 2000KB를 초과할 수 없습니다. [!DNL Adobe] 프로필 속성에 대해 1000KB 미만의 스토리지를 사용하는 것이 좋습니다.
* 매개 변수와 값은 대/소문자를 구분합니다.

## HTTP POST 요청

에 대한 HTTP POST 요청 만들기 [!DNL Target] 파일을 처리할 에지 서버입니다. 다음은 curl 명령을 사용한 batch.txt 파일에 대한 샘플 HTTP POST 요청입니다.

``````
curl -X POST --data-binary @BATCH.TXT http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/v2/profile/batchUpdate
``````

여기서

BATCH.TXT는 파일 이름입니다. CLIENTCODE는 [!DNL Target] 클라이언트 코드입니다.

클라이언트 코드를 모르는 경우 [!DNL Target] 사용자 인터페이스 클릭 **[!UICONTROL 관리]** > **[!UICONTROL 구현]**. 클라이언트 코드는에 표시됩니다. [!UICONTROL 계정 세부 정보] 섹션.

### Inspect 응답

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

오류가 있는 경우 응답에는 다음이 포함됩니다. `success=false` 오류에 대한 자세한 메시지를 표시합니다.

### 기본 일괄 처리 상태 응답

위의 경우 성공한 기본 응답 `batchStatus` 클릭한 URL 링크는 다음과 같습니다.

```
<response><batchId>demo4-1701473848678-13029383</batchId><status>complete</status><batchSize>1</batchSize></response>
```

상태 필드에 필요한 값은 다음과 같습니다.

| 상태 | 세부 사항 |
| --- | --- |
| [!UICONTROL complete] | 프로필 배치 업데이트 요청이 완료되었습니다. |
| [!UICONTROL 미완료] | 프로필 배치 업데이트 요청이 아직 처리 중이며 완료되지 않았습니다. |
| [!UICONTROL 중단] | 프로필 배치 업데이트 요청이 중단되어 완료할 수 없습니다. |

### 자세한 배치 상태 URL 응답

매개 변수를 전달하여 보다 자세한 응답을 가져올 수 있습니다 `showDetails=true` (으)로 `batchStatus` 위의 url입니다.

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
