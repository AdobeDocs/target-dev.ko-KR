---
title: .NET SDK와 함께  [!DNL Adobe Target] 에서 getAttributes 사용
description: getAttributes()를 사용하여  [!DNL Target] 에서 실험과 개인화된 경험을 가져오고 특성 값을 추출하는 방법을 알아봅니다.
feature: APIs/SDKs
exl-id: 808da83d-3077-468b-a2ad-e35c25905f7d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 9%

---

# 속성 가져오기(.NET)

## 설명

`GetAttributes()`은(는) [!DNL Target]에서 실험과 개인화된 경험을 가져오고 특성 값을 추출하는 데 사용됩니다.

## 방법

### getAttributes

```dotnet {line-numbers="true"}
TargetAttributes TargetClient.GetAttributes(TargetDeliveryRequest targetRequest, params string[] mboxes)
```

## 매개 변수

| 이름 | 유형 | 필수 | 기본값 | 설명 |
| --- | --- | --- | --- | --- |
| targetRequest | TargetDeliveryRequest | 아니요 | null | [오퍼 가져오기](get-offers.md)에 사용된 것과 동일한 {0&#x200B;} 요청[!DNL Target] |
| mboxNames | 매개 변수 문자열[] | 아니요 | null | mbox 이름의 매개 변수 배열 |

## 결과

다음 속성 및 메서드를 가진 `TargetClient.GetAttributes()`에서 `TargetAttributes` 개체가 반환됩니다.

| 속성/메서드 | 반환 유형 | 설명 |
| --- | --- | --- |
| 응답 | TargetDeliveryResponse | 일반적으로 [오퍼 가져오기](get-offers.md)에서 반환된 응답 개체를 반환합니다. |
| ToDictionary | IReadOnlyDictionary | mbox 이름으로 그룹화된 키 값 쌍을 가진 사전 사전을 반환합니다. |
| ToMboxDictionary(mboxName) | IReadOnlyDictionary | 제공된 mbox에 대한 키 값 쌍이 있는 사전을 반환합니다. |
| GetBoolean(mboxName, key, defaultValue) | 부울 | 지정된 mbox 이름 및 속성 키에 대한 값을 반환합니다. |
| GetString(mboxName, key, defaultValue) | string | 지정된 mbox 이름 및 속성 키에 대한 값을 반환합니다. |
| GetInteger(mboxName, key, defaultValue) | int | 지정된 mbox 이름 및 속성 키에 대한 값을 반환합니다. |
| GetDouble(mboxName, key, defaultValue) | 더블 | 지정된 mbox 이름 및 속성 키에 대한 값을 반환합니다. |
| GetValue(mboxName, key, defaultValue) | T | 지정된 mbox 이름 및 속성 키에 대한 값을 반환합니다. |

## 예

### \.NET

```dotnet {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("acmeClient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
    .Build();

var targetClient = TargetClient.Create(targetClientConfig);

var mboxRequests = new List<MboxRequest> { new (index: 1, name: "a1-serverside-ab") };

var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
    .Build();

var offerAttributes = targetClient.GetAttributes(targetDeliveryRequest, "demo-engineering-flags");

//returns just the value of searchProviderId from the mbox offer
var searchProviderId = offerAttributes.GetString("demo-engineering-flags", "searchProviderId");

//returns a simple Dictionary representing the mbox offer
var engineeringFlags = offerAttributes.ToMboxDictionary("demo-engineering-flags");

//  the value of engineeringFlags looks like this
//  {
//      "cdnHostname": "cdn.cloud.corp.net",
//      "searchProviderId": 143,
//      "hasLegacyAccess": false
//  }

var assetUrl = $"http://{engineeringFlags["cdnHostname"]}/path/to/asset";
```
