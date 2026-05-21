---
title: ' [!DNL Adobe Target] Python SDK에서 비동기 요청을 사용하는 방법'
description: ' [!DNL Target] Python SDK이 효과적인 대상 시간을 0으로 줄일 수 있는 비동기 요청을 지원하는 방법에 대해 알아봅니다.'
feature: APIs/SDKs
exl-id: fafb9e28-5ac5-41c1-8e7f-f40550b6749f
TQID: https://experienceleague.adobe.com/CFfT7Amoca2yqYkkt9AviTmWi-RCjGdABYYuWHxvqC8
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bcc5edb5-84c3-4940-9f84-ed88b6c16274
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 130
ht-degree: 15%

---

# 속성 가져오기(Python)

## 설명

`get_attributes()`은(는) [!DNL Target]에서 실험과 개인화된 경험을 가져오고 특성 값을 추출하는 데 사용됩니다.


## 방법

### getAttributes

```python {line-numbers="true"}
target_client_instance.get_attributes(mbox_names, options)
```

## 매개변수

| 이름 | 유형 | 필수 | 기본값 | 설명 |
| --- | --- | --- | --- | --- |
| mbox_names | list[str] | 예 | 없음 | mbox 이름 목록 |
| options | dict | 아니오 | 없음 | [오퍼 가져오기](get-offers.md)에 사용된 것과 동일한 옵션 |

## Attributeprovider

`target_client.get_attributes()`이(가) 반환한 `AttributesProvider`에는 다음 메서드가 있습니다.

| 방법 | 반환 유형 | 설명 |
| --- | --- | --- |
| get_value(mbox_name, key) | any | 지정된 mbox 이름 및 속성 키에 대한 값을 반환합니다. |
| as_object(mbox_name) | dict | 키 값 쌍이 있는 단순 json 개체 반환 |
| get_response() | [TargetDeliveryResponse](https://github.com/adobe/target-python-sdk/blob/main/target_python_sdk/types/target_delivery_response.py) | `get_offers`이(가) 정상적으로 반환한 응답 개체를 반환합니다. |

## 예

### Python

```python {line-numbers="true"}
def client_ready_callback():
    context = Context(channel=ChannelType.WEB)
    mboxes = [MboxRequest(name="a1-serverside-ab", index=1)]
    execute = ExecuteRequest(mboxes=mboxes)
    delivery_request = DeliveryRequest(context=context, execute=execute)

    get_attributes_options = {
      "request": delivery_request
    }

    attributes_provider = target_client.get_attributes(["demo-engineering-flags"], get_attributes_options)
    # returns just the value of searchProviderId from the demo-engineering-flags mbox offer
    search_provider_id = attributes_provider.get_value("demo-engineering-flags", "searchProviderId")

    # returns a simple dict object representing the demo-engineering-flags mbox offer
    engineering_flags = attributes_provider.as_object("demo-engineering-flags")
    """  the value of engineeringFlags looks like this
        {
            "cdnHostname": "cdn.cloud.corp.net",
            "searchProviderId": 143,
            "hasLegacyAccess": false
        }
    """

    asset_url = "http://{}/path/to/asset".format(engineering_flags.get("cdnHostname"))


client_options = {
    "client": "acmeclient",
    "organization_id": "1234567890@AdobeOrg",
    "events": {
        "client_ready": client_ready_callback
    }
}
target_client = TargetClient.create(client_options)
```
