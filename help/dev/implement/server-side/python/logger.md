---
title: 요청을 기록하려면  [!DNL Adobe Target] Python SDK을 초기화하십시오.
description: ' [!DNL Adobe Target] Python SDK에 요청을 기록하는 방법을 알아봅니다.'
feature: APIs/SDKs
exl-id: 0b3792a5-a9a7-4768-a429-598b49f1fd93
TQID: https://experienceleague.adobe.com/9LSln8V3QIG9GTok2yTTnKvhlpQhaed3a-qJyA4jErg
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: a94ced60-8199-4549-b453-ede2acb4101e
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 97
ht-degree: 3%

---

# 로거(Python)

## 설명

[SDK을 초기화](initialize-sdk.md)할 때 `options["logger"]` 개체는 선택 개체입니다. 기본적으로 `adobe.target` 네임스페이스 아래에 INFO 수준 로거가 만들어집니다. 그러나 문제가 발생할 때 로그 수준을 사용자 지정하거나 효과적으로 디버깅하기 위해 SDK을 초기화할 때 `logger` 개체를 제공할 수 있습니다.

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
