---
title: 초기화 [!DNL Adobe Target] 요청을 기록하는 Python SDK
description: 에 요청을 기록하는 방법 알아보기 [!DNL Adobe Target] Python SDK.
feature: APIs/SDKs
exl-id: 0b3792a5-a9a7-4768-a429-598b49f1fd93
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 3%

---

# 로거(Python)

## 설명

날짜 [sdk 초기화](initialize-sdk.md), `options["logger"]` 개체는 선택 사항입니다. 기본적으로 INFO 수준 로거는 `adobe.target` 네임스페이스입니다. 그러나 문제가 발생할 때 로그 수준을 사용자 정의하거나 효율적으로 디버깅하려면 `logger` sdk를 초기화할 때 개체를 제공할 수 있습니다.

다음 `logger` 개체에 다음이 있어야 합니다. `debug()` 및 `error()` 메서드를 사용합니다. 적절한 로거가 제공되면, [!DNL Target] 요청 및 응답이 기록됩니다.

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
