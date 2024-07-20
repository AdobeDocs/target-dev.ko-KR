---
title: ' [!DNL Adobe Target] Python SDK에서 이벤트 구독'
description: '[!UICONTROL OnDeviceDecisioningHandler] 개체를 사용하여 Python SDK 내에서 발생하는 다양한 이벤트를 구독하는 방법에 대해 알아봅니다.'
feature: APIs/SDKs
exl-id: 4e32e3b5-6072-4703-b09d-abb467aa1304
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 3%

---

# SDK 이벤트(Python)

## 설명

[SDK를 초기화](initialize-sdk.md)할 때 `options["events"]` dict는 이벤트 이름 키와 콜백 함수 값이 있는 선택적 개체입니다. SDK 내에서 발생하는 다양한 이벤트를 구독하는 데 사용할 수 있습니다. 예를 들어 `client_ready` 이벤트는 SDK에서 메서드 호출을 수행할 준비가 되었을 때 호출되는 콜백 함수와 함께 사용할 수 있습니다.

`callback` 함수가 호출되면 이벤트 개체가 전달됩니다. 각 이벤트에는 이벤트 이름에 해당하는 `type`이(가) 있으며, 일부 이벤트에는 관련 정보가 있는 추가 속성이 포함되어 있습니다.

## 이벤트

| 이벤트 이름(유형) | 설명 | 추가 이벤트 속성 |
| --- | --- | --- |
| client_ready | 아티팩트가 다운로드되고 SDK가 get_offers 호출을 위해 준비되면 내보내집니다. 사용 시 권장 | 온디바이스 의사 결정 방법. | 없음 |
| artifact_download_succeeded | 새 아티팩트가 다운로드될 때마다 내보내집니다. | artifact_payload, artifact_location |
| artifact_download_failed | 아티팩트가 다운로드되지 않을 때마다 내보내집니다. | artifact_location, 오류 |

## 예

### Python

```python {line-numbers="true"}
def client_ready_callback():
    # make get_offers requests

def artifact_download_succeeded(event):
    print("The artifact was successfully downloaded from {}".format(event.artifact_location))
    # optionally do something with event.artifact_payload, like persist it

def artifact_download_failed(event):
    print("The artifact failed to download from {} with the following error: {}"
          .format(event.artifact_location, str(event.error)))

client_options = {
    "client": "acmeclient",
    "organization_id": "1234567890@AdobeOrg",
    "events": {
        "client_ready": client_ready_callback,
        "artifact_download_succeeded": artifact_download_succeeded,
        "artifact_download_failed": artifact_download_failed
    }
}
target_client = target_client.create(client_options)
```
