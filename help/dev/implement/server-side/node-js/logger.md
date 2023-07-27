---
title: 초기화 [!DNL Adobe Target] 요청을 기록할 Node.js SDK
description: 에 요청을 기록하는 방법 알아보기 [!DNL Adobe Target] Node.js SDK.
feature: APIs/SDKs
exl-id: 5db3e301-47b3-4330-b185-c0c03f72e790
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 2%

---

# 로거(Node.js)

## 설명

날짜 [sdk 초기화](initialize-sdk.md), `options.logger` 개체는 선택 사항입니다. 그러나 문제가 발생할 때 효과적으로 디버깅하려면 `logger` sdk를 초기화할 때 개체를 제공해야 합니다.

다음 `logger` 개체에 다음이 있어야 합니다. `debug()` 및 `error()` 메서드를 사용합니다. 적절한 로거가 제공될 때, 예: `console`, [!DNL Target] 요청 및 응답이 기록됩니다.

## 예

### Node.js

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg",
  logger: console
};

const targetClient = TargetClient.create(CONFIG);

const request = {
    execute: {
        mboxes: [{
            name: "a1-serverside-ab",
            index: 1
        }]
    }
};

const response = await targetClient.getOffers({ request, targetCookie });
```

콘솔에 요청 및 응답이 인쇄되는 것을 볼 수 있습니다.
