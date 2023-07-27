---
title: 에서 비동기 요청을 사용하는 방법 [!DNL Adobe Target] Python SDK
description: 방법 알아보기 [!DNL Target] Python SDK는 비동기 요청을 지원하므로 유효 타겟 시간을 0으로 줄일 수 있습니다.
feature: APIs/SDKs
exl-id: 44ab74e5-3c1a-49cf-9fff-fe523b0c2592
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 4%

---

# 비동기 요청(Python)

## 설명

서버 측 통합의 한 가지 이점은 병렬 처리를 사용하여 서버 측에서 사용할 수 있는 엄청난 대역폭과 컴퓨팅 리소스를 활용할 수 있다는 것입니다. [!DNL Target] Python SDK는 비동기 요청을 지원하므로 유효 타겟 시간을 0으로 줄일 수 있습니다.

## 지원되는 메서드

### Python

```python {line-numbers="true"}
get_offers(options)
send_notifications(options)
get_attributes(mbox_names, options)
```

## 예

를 사용하는 샘플 응용 프로그램 `asyncio` python 3.9+에서 모듈의 비동기/대기는 다음과 같이 표시될 수 있습니다.

### Python

```python {line-numbers="true"}
async def execute_mboxes(self, mboxes):
    context = Context(channel=ChannelType.WEB)
    execute = ExecuteRequest(mboxes=mboxes)
    delivery_request = DeliveryRequest(context=context, execute=execute)

    get_offers_options = {
      "request": delivery_request
    }
    return await asyncio.to_thread(target_client.get_offers, get_offers_options)

async def get_target_delivery_response(mboxes):
    target_delivery_response = await execute_mboxes(mboxes)
    response = Response(target_delivery_response.get("response").to_str(), status=200, mimetype='application/json')
    return response

mboxes = [MboxRequest(name="a1-serverside-ab", index=1)]
return asyncio.run(get_target_delivery_response(mboxes)
```

이 예제에서는 사용자가 Python 3.9 이상을 사용하고 있다고 가정합니다. 이전 버전의 Python을 사용하는 경우에도 를 전달하여 비동기 요청을 보낼 수 있습니다 `options.callback` 끝 `get_offers`. 콜백 또는 비동기/대기를 사용한 비동기 실행에 대한 자세한 내용은 샘플 Flask 앱을 확인하십시오. [여기](https://github.com/adobe/target-python-sdk/blob/main/samples/app.py).
