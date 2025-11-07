---
title: ' [!DNL Adobe Target] Node.js SDK에서 이벤트 구독'
description: '[!UICONTROL OnDeviceDecisioningHandler] 개체를 사용하여 Node.js SDK 내에서 발생하는 다양한 이벤트에 가입하는 방법에 대해 알아봅니다.'
feature: APIs/SDKs
exl-id: 40c53840-a560-4819-ae04-f527c36b22fe
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 2%

---

# SDK 이벤트(Node.js)

## 설명

[SDK을 초기화](initialize-sdk.md)할 때 `options.events` 개체는 이벤트 이름 키와 콜백 함수 값을 가진 선택적 개체입니다. SDK 내에서 발생하는 다양한 이벤트를 구독하는 데 사용할 수 있습니다. 예를 들어 `clientReady` 이벤트는 SDK에서 메서드 호출을 수행할 준비가 되었을 때 호출되는 콜백 함수와 함께 사용할 수 있습니다.

콜백 함수가 호출되면 이벤트 개체가 전달됩니다. 각 이벤트에는 이벤트 이름에 해당하는 `type`이(가) 있습니다. 일부 이벤트에는 관련 정보가 포함된 추가 속성이 포함됩니다.

## 이벤트

| 이벤트 이름(유형) | 설명 | 추가 이벤트 속성 |
| --- | --- | --- |
| clientReady | 아티팩트가 다운로드되고 SDK이 `getOffers` 호출을 위해 준비되면 내보냅니다. 온디바이스 의사 결정 방법을 사용할 때 권장됩니다. |  |
| artifactDownloadSucceeded | 새 아티팩트가 다운로드될 때마다 내보내집니다. | artifactPayload, artifactLocation |
| artifactDownloadFailed | 아티팩트가 다운로드되지 않을 때마다 내보내집니다. | artifactLocation, 오류 |

## 예

### Node.js

```js {line-numbers="true"}
const targetClient = TargetClient.create({
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    decisioningMethod: "on-device",
    events: {
        clientReady: onTargetClientReady,
        artifactDownloadSucceeded: onArtifactDownloadSucceeded,
        artifactDownloadFailed: onArtifactDownloadFailed
    }
});

function onTargetClientReady() {
    // make getOffers requests
    targetClient.getOffers({...})            
}

function onArtifactDownloadSucceeded(event) {
    console.log(`The artifact was successfully downloaded from '${event.artifactLocation}'`);
    // optionally do something with event.artifactPayload, like persist it
}

function onArtifactDownloadFailed(event) {
    console.log(`The artifact failed to download from '${event.artifactLocation}' with the following error message: ${event.error.message}`);
}
```
