---
title: 사용자 권한 및 속성
description: ' [!DNL Target] SDK에는 사용자 권한 및 속성에 대한 지원이 포함되어 있습니다.'
exl-id: 612faf1a-e8f9-4321-b831-90fba69ead3a
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# 사용자 권한 및 속성

[!DNL Target] SDK에는 사용자 권한 및 속성에 대한 지원이 포함되어 있습니다. [!DNL Adobe Target]이(가) 작업 공간 및 속성을 통해 엔터프라이즈 권한을 처리하는 방법에 익숙하지 않다면 [엔터프라이즈 사용자 권한](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=ko-KR)에서 자세한 내용을 볼 수 있습니다.

클라이언트는 두 가지 방법 중 하나로 속성 토큰을 사용할 수 있습니다.

## 전역 속성 토큰

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    propertyToken: "8c4630b1-16db-e2fc-3391-8b3d81436cfb"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({...})
```

>[!TAB Java]

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("emeaprod4")
    .organizationId("0DD934B85278256B0A490D44@AdobeOrg")
    .defaultPropertyToken("8c4630b1-16db-e2fc-3391-8b3d81436cfb")
    .build();

TargetClient targetClient = TargetClient.create(clientConfig);
```

>[!ENDTABS]

## getOffers 호출의 부수적 속성 토큰

개별 `getOffers` 호출에서도 속성 토큰을 지정할 수 있습니다. 이 작업은 요청에 속성 개체를 추가하여 수행합니다. 이 방법으로 지정된 속성 토큰은 구성의 한 세트에 대해 선례를 갖습니다.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
    request: {
        execute: {
            pageLoad: {}
        },
        property: {
            token: "8c4630b1-16db-e2fc-3391-8b3d81436cfb"
        }           
    }
})
```

>[!TAB Java]

```java {line-numbers="true"}
ExecuteRequest executeRequest = new ExecuteRequest()
    .mboxes(getMboxRequests(mbox));

TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
    .context(getContext(request))
    .execute(executeRequest)
    .cookies(getTargetCookies(request.getCookies()))
    .property(new Property().token("8c4630b1-16db-e2fc-3391-8b3d81436cfb"))
    .build();

TargetDeliveryResponse targetResponse = targetClient.getOffers(targetDeliveryRequest);
```

>[!ENDTABS]
