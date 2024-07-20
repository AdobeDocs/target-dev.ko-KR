---
title: 요청을 기록하려면  [!DNL Adobe Target] Python SDK를 초기화하십시오.
description: ' [!DNL Adobe Target] Python SDK에서 요청을 기록하는 방법에 대해 알아봅니다.'
feature: APIs/SDKs
exl-id: 0b3792a5-a9a7-4768-a429-598b49f1fd93
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 3%

---

# 로거(Python)

## 설명

[SDK를 초기화](initialize-sdk.md)할 때 `options["logger"]` 개체는 선택적 개체입니다. 기본적으로 `adobe.target` 네임스페이스 아래에 INFO 수준 로거가 만들어집니다. 그러나 문제가 발생할 때 로그 수준을 사용자 지정하거나 효과적으로 디버깅하기 위해 SDK를 초기화할 때 `logger` 개체를 제공할 수 있습니다.

`logger` 개체에는 `debug()` 및 `error()` 메서드가 있어야 합니다. 적절한 로거가 제공되면 [!DNL Target]개의 요청 및 응답이 기록됩니다.

## 예

### Python

```python {line-numbers="true"}
logger = logging.getLogger("org.logger")
logger.setLevel(logging.DEBUG)

client_options = {
  "client": "acmeclient",
  "organization_id": "1234567890@AdobeOrg",
  "logger": logger
}
target_client = TargetClient.create(client_options)
```

콘솔에 요청 및 응답이 인쇄되는 것을 볼 수 있습니다.
