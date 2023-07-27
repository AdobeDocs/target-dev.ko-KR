---
title: 에서 getOffers() 사용 [!DNL Adobe Target] python SDK 사용 시
description: getOffers()를 사용하여 결정을 실행하고 경험을 검색하는 방법을 알아봅니다. [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 9539b806-e070-430e-80cf-cf632ce3f207
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 13%

---

# 오퍼 가져오기(Python)

## 설명

`get_offers()` 의사 결정을 실행하고 경험을 검색하는 데 사용됩니다. [!DNL Adobe Target].


## 방법

### getOffers

```python {line-numbers="true"}
target_client_instance.get_offers(options)
```

## 매개 변수

다음 `options` dict의 구조는 다음과 같습니다.

| 이름 | 유형 | 필수 | 기본값 | 설명 |
| --- | --- | --- | --- | --- |
| 요청 | DeliveryRequest | 예 | 없음 | 을 준수합니다. [[!DNL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) 요청 |
| target_cookie | str | no | 없음 | [!DNL Target] cookie |
| target_location_hint | str | no | 없음 | [!DNL Target] 지역 힌트 |
| consumer_id | str | no | 없음 | 여러 호출을 결합할 때 서로 다른 소비자 ID가 제공되어야 합니다 |
| customer_ids | 목록[고객 ID] | no | 없음 | VisitorId 호환 형식의 고객 ID 목록 |
| session_id | str | no | 없음 | 여러 요청을 연결하는 데 사용됨 |
| callback | 호출 가능 | no | 없음 | 요청을 비동기식으로 처리하는 경우 응답이 준비되면 콜백이 호출됩니다 |
| err_callback | 호출 가능 | no | 없음 | 요청을 비동기적으로 처리하는 경우 예외가 발생하면 오류 콜백이 호출됩니다 |

## 반환

를 반환합니다. `TargetDeliveryResponse` 를 동기식으로 호출하거나(기본값) `AsyncResult` 콜백과 함께 호출되는 경우입니다. `TargetDeliveryResponse` 에는 다음 구조가 있습니다.

| 이름 | 유형 | 설명 |
| --- | --- | --- |
| 응답 | DeliveryResponse | 을 준수합니다. [[!UICONTROL Target 배달 API]](/help/dev/implement/delivery-api/overview.md) 응답 |
| target_cookie | dict | [!DNL Target] cookie |
| target_location_hint_cookie | dict | [!DNL Target] 위치 힌트 쿠키 |
| analytics_details | 목록[Analytics 응답] | 클라이언트측 Analytics 사용의 경우 Analytics 페이로드 |
| 추적 | 목록[dict] | 모든 요청 mbox/보기에 대해 집계된 추적 데이터 |
| response_tokens | 목록[dict] | &#x200B; 목록[응답 토큰](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) |
| meta | dict | 온디바이스 의사 결정에 사용하기 위한 추가 의사 결정 메타데이터 |

`target_cookie` 및 `target_location_hint_cookie` 데이터를 다시 브라우저로 전달하는 데 사용되는 객체는 다음 구조를 갖습니다.

| 이름 | 유형 | 설명 |
| --- | --- | --- |
| 이름 | str | 쿠키 이름 |
| value | any | 쿠키 값, 값이 문자열로 변환됩니다. |
| max_age | int | 다음 `max_age option` 는 현재 시간(초)을 기준으로 하여 만료 설정을 편리하게 할 수 있습니다 |

다음 `meta` 대상 응답의 상태를 나타내는 데 사용되는 객체는 다음 구조를 가집니다.

| 이름 | 유형 | 설명 |
| --- | --- | --- |
| decisioning_method | str | 사용된 의사 결정 방법: 온디바이스 또는 서버측 |
| remote_mboxes | 목록에 있는 참조 페이지를 나타냅니다`[str]` | 의사 결정 방법이 다음과 같은 경우 `on-device`, 디바이스에서 완전히 결정되지 않은 mbox 이름 배열이 제공됩니다. 즉, [[!UICONTROL Target 배달 API]](/help/dev/implement/delivery-api/overview.md) 요청이 필요합니다. |
| 원격 보기 수 | 목록에 있는 참조 페이지를 나타냅니다`[str]` | 의사 결정 메서드가 온디바이스일 때 온디바이스에서 완전히 결정될 수 없는 보기 이름 배열이 제공됩니다. 즉, [[!UICONTROL Target 배달 API]](/help/dev/implement/delivery-api/overview.md) 요청이 필요합니다. |

## 예

### Python

```python {line-numbers="true"}
def client_ready_callback():
    context = Context(channel=ChannelType.WEB)
    mboxes = [MboxRequest(name="a1-serverside-ab", index=1)]
    execute = ExecuteRequest(mboxes=mboxes)
    delivery_request = DeliveryRequest(context=context, execute=execute)

    get_offers_options = {
      "request": delivery_request
    }

    target_delivery_response = target_client.get_offers(get_offers_options)


client_options = {
    "client": "acmeclient",
    "organization_id": "1234567890@AdobeOrg",
    "events": {
        "client_ready": client_ready_callback
    }
}
target_client = TargetClient.create(client_options)
```
