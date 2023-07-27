---
title: 에서 getAttributes 사용 [!DNL Adobe Target] Java SDK 사용
description: getAttributes()를 사용하여 실험과 개인화된 경험을 가져오는 방법을 알아봅니다. [!DNL Target] 속성 값을 추출할 수 있습니다.
feature: APIs/SDKs
exl-id: e493e1b9-7180-4a7c-b98d-be84cc3a57c3
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 13%

---

# 속성 가져오기(Java)

## 설명

`getAttributes()` 에서 실험 및 개인화된 경험을 가져오는 데 사용됩니다. [!DNL Target] 속성 값을 추출할 수 있습니다.

## 방법

### getAttributes

```javascript {line-numbers="true"}
Attributes TargetClient.getAttributes(TargetDeliveryRequest targetRequest, String ...mboxes)
```

## 매개 변수

| 이름 | 유형 | 필수 | 기본값 | 설명 |
| --- | --- | --- | --- | --- |
| targetRequest | TargetDeliveryRequest | 예 | 없음 | 에 사용된 것과 동일한 target 요청 [오퍼 &#x200B; 가져오기](get-offers.md) |
| mboxNames | var-args 배열 | 아니요 | 없음 | mbox 이름의 var-args 배열 |


## 결과

An `Attributes` 다음에서 개체가 반환됩니다. `TargetClient.getAttributes()` 에는 다음과 같은 메서드가 있습니다.

| 이름 | 유형 | 설명 |
| --- | --- | --- |
| getBoolean(mboxName, key) | 부울 | 지정된 mbox 이름 및 속성 키에 대한 값을 반환합니다. |
| getString(mboxName, key) | 문자열 | 지정된 mbox 이름 및 속성 키에 대한 값을 반환합니다. |
| getInteger(mboxName, key) | 정수 | 지정된 mbox 이름 및 속성 키에 대한 값을 반환합니다. |
| getDouble(mboxName, key) | 이중 | 지정된 mbox 이름 및 속성 키에 대한 값을 반환합니다. |
| toMboxMap(mboxName) | 맵 | 키 값 쌍이 있는 단순 맵을 반환합니다. |
| getResponse() | TargetDeliveryResponse | getOffers에서 일반적으로 반환되는 응답 개체를 반환합니다. |

## 예

### Java

```javascript {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .build();

TargetClient targetJavaClient = TargetClient.create(clientConfig);

TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
        .context(new Context().channel(ChannelType.WEB))
        .build();

Attributes offerAttributes = targetJavaClient.getAttributes(targetDeliveryRequest, "demo-engineering-flags");

//returns just the value of searchProviderId from the mbox offer
String searchProviderId = offerAttributes.getString("demo-engineering-flags", "searchProviderId");

//returns a simple Map representing the mbox offer
Map<String, Object> engineeringFlags = offerAttributes.toMboxMap("demo-engineering-flags");

//  the value of engineeringFlags looks like this
//  {
//      "cdnHostname": "cdn.cloud.corp.net",
//      "searchProviderId": 143,
//      "hasLegacyAccess": false
//  }

String assetUrl = "http://" + engineeringFlags.cdnHostname + "/path/to/asset";
```
