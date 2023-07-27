---
title: 에서 비동기 요청을 사용하는 방법 [!DNL Adobe Target] Node.js SDK
description: 방법 알아보기 [!DNL Target] Node.js SDK는 비동기 요청을 지원하므로 유효 타겟 시간을 0으로 줄일 수 있습니다.
feature: APIs/SDKs
exl-id: aa06f3ca-7d2a-4334-8092-730a8705dfb0
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 18%

---

# 속성 가져오기(Node.js)

## 설명

`[!UICONTROL getAttributes()]` 에서 실험 및 개인화된 경험을 가져오는 데 사용됩니다. [!DNL Target] 속성 값을 추출할 수 있습니다.

## 방법

### getAttributes

```js {line-numbers="true"}
TargetClient.getAttributes(mboxNames: Array, options: Object): Promise
```

## 매개 변수

| 이름 | 유형 | 필수 | 기본값 |
| --- | --- | --- |--- |
| mboxNames | 배열 | 예 | 없음 |
| options | 개체 | 아니오 | 없음 |

## 약속

다음 `Promise` 반환한 사람 `TargetClient.getAttributes()` 는 다음 방법으로 개체를 확인합니다.

| 방법 | 반환 유형 | 설명 |
| --- | --- | --- |
| getValue(mboxName, key) | Any | 지정된 mbox 이름 및 속성 키에 대한 값을 반환합니다. |
| asObject(mboxName) | 개체 | 키 값 쌍이 있는 단순 json 개체 반환 |
| getResponse() | [getOffers 응답](https://github.com/jasonwaters/target-nodejs-sdk#targetclientgetoffers) | 다음에 의해 정상적으로 반환된 응답 개체 반환: `getOffers` |

## 예

### Node.js

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);
const offerAttributes = await targetClient.getAttributes(["demo-engineering-flags"]);


//returns just the value of searchProviderId from the mbox offer
const searchProviderId = offerAttributes.getValue("demo-engineering-flags", "searchProviderId");

//returns a simple JSON object representing the mbox offer
const engineeringFlags = offerAttributes.asObject("demo-engineering-flags");

//  the value of engineeringFlags looks like this
//  {
//      "cdnHostname": "cdn.cloud.corp.net",
//      "searchProviderId": 143,
//      "hasLegacyAccess": false
//  }

const assetUrl = `http://${engineeringFlags.cdnHostname}/path/to/asset`;
```
