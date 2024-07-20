---
title: 요청을 기록하려면  [!DNL Adobe Target] Node.js SDK를 초기화하십시오.
description: ' [!DNL Adobe Target] Node.js SDK에서 요청을 기록하는 방법에 대해 알아봅니다.'
feature: APIs/SDKs
exl-id: 5db3e301-47b3-4330-b185-c0c03f72e790
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 2%

---

# 로거(Node.js)

## 설명

[SDK를 초기화](initialize-sdk.md)할 때 `options.logger` 개체는 선택적 개체입니다. 그러나 문제가 발생할 때 효과적으로 디버깅하려면 SDK를 초기화할 때 `logger` 개체를 제공해야 합니다.

`logger` 개체에는 `debug()` 및 `error()` 메서드가 있어야 합니다. `console`과(와) 같은 적절한 로거가 제공되면 [!DNL Target]개의 요청 및 응답이 기록됩니다.

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
