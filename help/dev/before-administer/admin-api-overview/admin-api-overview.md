---
title: Adobe Target 관리 API 개요
description: ' [!DNL Adobe Target Admin API] 개요'
exl-id: 1168d376-c95b-4c5a-b7a2-c7815799a787
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1312'
ht-degree: 2%

---

# Target 관리 API 개요

이 문서에서는 [!DNL Adobe Target Admin API]을(를) 이해하고 성공적으로 사용하는 데 필요한 배경 정보에 대한 개요를 제공합니다. 다음 내용은 사용자가 [!DNL Adobe Target Admin API]에 대해 [인증을 구성](../configure-authentication.md)하는 방법을 이해하고 있다고 가정합니다.

>[!NOTE]
>
>UI를 통해 [!DNL Target]을(를) 관리하려면 *Adobe Target 비즈니스 실무자 안내서*](https://experienceleague.adobe.com/docs/target/using/administer/administrating-target.html?lang=en)의 [관리 섹션을 참조하십시오.
>
>관리 API 및 프로필 API는 종종 총괄적으로(&quot;관리 및 프로필 API&quot;) 참조되지만, 별도로(&quot;관리 API&quot; 및 &quot;프로필 API&quot;) 참조할 수도 있습니다. Recommendations API는 [!DNL Target] 관리 API의 특정 구현입니다.

## 시작하기 전에

[관리 API](../../administer/admin-api/admin-api-overview-new.md)에 대해 제공된 모든 코드 예제에서 {tenant}을(를) 테넌트 값으로, `your-bearer-token`을(를) JWT로 생성한 액세스 토큰으로, `your-api-key`을(를) [Adobe Developer Console](https://developer.adobe.com/console/home)의 API 키로 바꿉니다. 테넌트 및 JWT에 대한 자세한 내용은 Adobe [!DNL Target] 관리 API에 대해 [인증을 구성](../configure-authentication.md)하는 방법에 대한 문서를 참조하십시오.

## 버전 매기기

모든 API에는 연결된 버전이 있습니다. 사용하려는 API의 올바른 버전을 제공하는 것이 중요합니다.

요청에 페이로드(POST 또는 PUT)가 포함된 경우 요청의 `Content-Type` 헤더를 사용하여 버전을 지정합니다.

요청에 페이로드(GET, DELETE 또는 OPTIONS)가 포함되어 있지 않으면 `Accept` 헤더를 사용하여 버전을 지정합니다.

버전을 제공하지 않으면 호출이 기본적으로 V1(application/vnd.adobe.target.v1+json)로 설정됩니다.

>[!NOTE]
>
>올바른 버전을 지정하지 않은 경우(예: V2 페이로드를 사용하지만 Content-Type 헤더를 지정하지 않은 경우) API가 역으로 호환되지 않는 경우 API는 지원되지 않는 오류로 응답합니다.

지원되지 않는 기능에 대한 오류 메시지

```
{
    "httpStatus": 406,
    "requestId": "8752b736-cf71-4d81-86c3-94be2b5ae648",
    "requestTime": "2018-02-02T21:39:06.405Z",
    "errors": [
        {
            "errorCode": "Unsupported.Feature",
            "message": "Unsupported features detected"
        }
    ]
}
```

관리 Postman 컬렉션

Postman은 API 호출을 쉽게 실행할 수 있는 애플리케이션입니다. 이 [Target 관리 API Postman 컬렉션](https://developers.adobetarget.com/api/#admin-postman-collection)에는 활동, 대상, 오퍼, 보고서, Mbox 및 환경을 사용하여 인증이 필요한 모든 Target 관리 API 호출이 포함되어 있습니다

## 응답 코드

다음은 Target 관리 API에 대한 일반적인 응답 코드입니다.

| 상태 | 의미 | 설명 |
| --- | --- | --- |
| 200 | [확인](https://www.rfc-editor.org/rfc/rfc7231#section-6.3.1) | 확인 |  |
| 400 | [잘못된 요청](https://www.rfc-editor.org/rfc/rfc7231#section-6.5.1) | 잘못된 요청. 요청에 제공된 데이터가 잘못되었을 가능성이 큽니다. |  |
| 401 | [권한 없음](https://www.rfc-editor.org/rfc/rfc7235#section-3.1) | 사용자는 이 작업을 수행할 수 없습니다. |  |
| 403 | [사용할 수 없음](https://www.rfc-editor.org/rfc/rfc7231#section-6.5.3) | 이 리소스에 대한 액세스가 금지되어 있습니다. |  |
| 404 | [찾을 수 없음](https://www.rfc-editor.org/rfc/rfc7231#section-6.5.4) | 참조된 리소스를 찾을 수 없습니다. |  |

## 활동

활동을 통해 사용자에 대한 콘텐츠를 테스트하거나 개인화할 수 있습니다. 활동은 다음 유형 중 하나일 수 있습니다.

* [A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [경험 타겟팅(XT)](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html)
* [Recommendations](https://experienceleague.adobe.com/docs/target/using/activities/recommendations-activity.html)
* [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [MVT(다변량 테스트)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)

## 일괄 업데이트

여러 관리 API를 단일 배치 요청으로 실행할 수 있습니다.

### 일괄 처리 호출 실행

`POST /{tenant}/target/batch`

여러 API 호출을 함께 스택하고 단일 배치로 실행합니다.

일괄 처리를 사용하면 단일 HTTP 요청에서 여러 작업에 대한 명령을 전달할 수 있습니다. 아래 섹션에 설명된 관련 작업 간의 종속성을 지정할 수도 있습니다. TNT는 각 독립 작업을(병렬로 가능) 처리하고 종속 작업을 순차적으로 처리합니다. 모든 작업이 완료되면 통합 응답이 다시 전달되고 HTTP 연결이 닫힙니다.

배치 API는 JSON 배열로 표현되는 논리적 HTTP 요청 배열에서 가져옵니다. 각 요청에는 메서드(HTTP 메서드 GET/PUT/POST/DELETE 등에 해당), relativeUrl(admin/rest/ 뒤 URL 부분), 선택적 헤더 배열(HTTP 헤더에 해당) 및 선택적 본문(POST 및 PUT 요청용)이 있습니다. 배치 API는 JSON 배열로 표현되는 논리적 HTTP 응답 배열을 반환합니다. 각 응답에는 상태 코드, 선택적 헤더 배열 및 선택적 본문(JSON 인코딩 문자열)이 있습니다. 일괄 처리된 요청을 수행하려면 수행할 각 개별 작업을 설명하는 JSON 개체를 작성합니다. 허용되는 최대 작업 수는 256개입니다(0개에서 255개까지).

요청에서 작업 간 종속성 지정 기본적으로 배치 API 요청에 지정된 작업은 독립적입니다. 즉, 서버에서 임의의 순서로 실행할 수 있으며 한 작업의 오류가 다른 작업의 실행에 영향을 주지 않습니다.

요청의 작업은 종종 종속됩니다. 예를 들어 한 작업의 출력이 다음 작업의 입력에 사용될 수 있습니다. 예를 들어 operationId=0에서 만든 오퍼는 campaign 만들기 operationId=1에서 사용해야 합니다.

두 배치 작업을 함께 연결하려면 종속 작업에 필요한 작업의 ID를 지정하십시오(예: &quot;dependsOnOperationId&quot; : 5). 또한 일괄 처리 작업의 POST 요청을 통해 생성된 리소스의 ID를 &quot;relativeUrl&quot; 및 &quot;body&quot;의 종속 작업에 모두 사용할 수 있습니다.

#### 권한 및 제한

일괄 처리 API 작업을 실행하려면 기본 사용자에게 최소 &quot;편집기&quot; 권한이 있어야 합니다(사용자가 보유한 권한보다 추가 권한이 필요한 경우 각 개별 작업에 대해). 일반적인 조절 전략은 모든 작업을 개별적으로 수행한 것처럼 일괄 API 작업에 적용됩니다.

모든 작업이 완료되면 일괄 처리가 완료되며 종속성 작업이 실패했거나 건너뛴 것이므로 작업이 성공(2xx statusCode), 실패(4xx, 5xx status code) 또는 건너뛸 수 있습니다.

#### 요청 개체 매개 변수

| 특성 | 설명 | 제한 | 기본값 |
| --- | --- | --- | --- |
| 본문 | http 일괄 처리 작업의 본문입니다. 은 POST 및 PUT을 제외한 모든 작업에 대해 무시됩니다. 은(는) 이전 일괄 처리 작업의 ID를 참조할 수 있습니다. 예: &quot;offerId&quot;: &quot;{operationIdResponse:0}&quot;, &quot;segmentId&quot;: &quot;{operationIdResponse:1}&quot; | 은(는) 유효한 JSON이어야 합니다. operationIdResponse를 참조하는 경우 참조된 operationId 응답은 유효한 ID여야 하며 해당 작업에 대한 메서드는 POST 상태여야 합니다. | 빈 개체 {} |  |
| dependsOnOperationIds | 지정된 작업이 성공적으로 완료된 경우에만 현재 작업이 실행되도록 하는 제한 ID 목록입니다. 을 사용하여 작업을 연결할 수 있습니다. | 최대 255개의 작업이 허용됩니다. 고유 값만 허용됩니다. 배열에서 유효한 operationId를 가리켜야 합니다. 순환 의존성은 허용되지 않습니다. |  |  |
| 헤더 | 특정 작업과 함께 보낼 키-값 헤더의 배열입니다. Authorization 헤더를 통해 배치 API에 대한 인증을 수행한 경우 개별 작업에도 복사됩니다. | 허용된 배열의 최대 헤더 수는 50개입니다. | Content-Type: application/json |  |
| headers->name | 헤더 이름 | 다른 헤더 이름 간에 고유해야 합니다. 헤더는 rfc에서 대소문자를 구분하지 않습니다. 그렇지 않으면 값이 서로 무시됩니다. |  |  |
| headers->value | 헤더 값 | 해당 사항 없음 | 빈 문자열 |  |
| 방법 | 사용할 HTTP 메서드. 사용 가능한 옵션: GET, POST, PUT, PATCH, DELETE | GET, POST, PUT, PATCH, DELETE 메서드만 허용됩니다. |  |  |
| operationId | 응답 및 참조 결과를 위한 다른 작업 중에서 작업을 식별하는 데 사용되는 작업 ID입니다. | 다른 작업들에서 고유함, 0-255 값 |  |  |
| 작업 | 일괄 처리에서 수행할 작업 목록입니다. 주문은 관련이 없습니다. | 최대 256개의 작업이 허용됩니다. |  |  |
| relativeUrl | &quot;/admin/rest/&quot; 뒤에 있는 관리자 rest API의 상대 URL입니다. 다음과 같은 쿼리 문자열 매개 변수를 포함할 수 있습니다. &quot;/v2/campaigns?limit=10&amp;offset=10&quot;. 은(는) 이전 일괄 처리 작업의 ID를 포함하는 URL을 참조할 수 있습니다(예: &quot;/v1/offers/{operationIdResponse:0}&quot;). 쿼리 매개 변수가 전송되는 경우 URL로 인코딩해야 합니다. | /로 시작해야 합니다(상대적). 유효한 새 JSON API만 지원됩니다. relativeURL이 잘못된 경우 특정 작업에 대한 404 응답이 반환됩니다. operationIdResponse를 참조하는 경우 참조된 operationId 응답이 유효한 ID여야 하며 해당 작업에 대한 메서드는 POST 상태여야 합니다. |  |  |

#### 샘플 요청 개체

```
{
  "operations": [
    {
      "operationId": 1,
      "dependsOnOperationIds~": [0],
      "method": "POST",
      "relativeUrl": "/v1/offers",
      "headers~": [
        {
          "name": "Content-Type",
          "value": "application/json"
        }
      ],
      "body~": {
        "key": "value"
      }
    }
  ]
}
```

#### 응답 개체 매개 변수

| 매개 변수 | 설명 |
| --- | --- |
| operationId | 다른 작업에서 작업을 식별하는 데 사용되는 작업 ID입니다. POST 요청에서 전송된 ID와 동일합니다. |  |
| 건너뜀 | 작업이 실행되었거나 건너뛴 경우 표시할 부울 플래그. 현재 작업이 실패한 작업에 따라 달라지는 경우 true가 됩니다(2xx와 다른 statusCode 값이 반환됨). |  |
| statusCode | 반환된 후 종속된 모든 작업을 건너뜁니다(실행되지 않음). |  |
| 헤더 | 특정 작업에 대한 응답으로 전송할 키-값 헤더 배열. |  |
| headers->name | 헤더 이름 |  |
| headers->value | 헤더 값 |  |
| 본문 | http 일괄 처리 응답 작업의 본문 |  |

#### 샘플 응답 개체

```
{
  "results": [
    {
      "operationId": 1,
      "skipped~": false,
      "statusCode~": 200,
      "headers~": [
        {
          "name": "Content-Type",
          "value": "application/json; charset=UTF-8"
        }
      ],
      "body~": {
        "id": 5
      }
    }
  ]
}
```
