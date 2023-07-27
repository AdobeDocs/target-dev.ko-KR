---
title: 온디바이스 의사 결정 규칙 아티팩트 자동 다운로드, 저장 및 업데이트
description: 를 초기화하는 동안 온디바이스 의사 결정 규칙 아티팩트로 작업하는 방법을 알아봅니다. [!DNL Adobe Target] SDK.
feature: APIs/SDKs
exl-id: be41a723-616f-4aa3-9a38-8143438bd18a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 1%

---

# 를 통해 규칙 아티팩트를 자동으로 다운로드, 저장 및 업데이트 [!DNL Adobe Target] SDK

이 방법은 를 초기화할 수 있을 때 가장 적합합니다. [!DNL Adobe Target] 웹 서버를 초기화하고 시작하는 동시에 SDK를 사용할 수 있습니다. 규칙 아티팩트는 [!DNL Adobe Target] 웹 서버 애플리케이션이 요청을 제공하기 전에 SDK를 통해 메모리에 캐시됩니다. 웹 애플리케이션이 실행되면 다음을 모두 수행합니다 [!DNL Adobe Target] 결정은 메모리 내 규칙 아티팩트를 사용하여 실행됩니다. 캐시된 규칙 아티팩트는 다음을 기반으로 업데이트됩니다. `pollingInterval` sdk 초기화 단계에서 를 지정합니다.

## 단계 요약

1. SDK 설치
1. SDK 초기화
1. 규칙 아티팩트 저장 및 사용

## 1. SDK 설치

>[!BEGINTABS]

>[!TAB NPM]

```javascript {line-numbers="true"}
npm i @adobe/target-nodejs-sdk -P
```

>[!TAB MVN]

```javascript {line-numbers="true"}
<dependency>
    <groupId>com.adobe.target</groupId>
    <artifactId>java-sdk</artifactId>
    <version>1.0</version>
</dependency>
```

>[!ENDTABS]

## 2. SDK 초기화

1. 먼저 SDK를 가져옵니다. 서버 시작을 제어할 수 있는 동일한 파일로 가져옵니다.

   **Node.js**

   ```javascript {line-numbers="true"}
   const TargetClient = require("@adobe/target-nodejs-sdk");
   ```

   **Java**

   ```javascript {line-numbers="true"}
   import com.adobe.target.edge.client.ClientConfig;
   import com.adobe.target.edge.client.TargetClient;
   ```

1. SDK를 구성하려면 create 메서드를 사용합니다.

   **Node.js**

   ```javascript {line-numbers="true"}
   const CONFIG = {
       client: "<your target client code>",
       organizationId: "your EC org id",
       decisioningMethod: "on-device",
       pollingInterval : 300000,
       events: {
           clientReady: startWebServer
       }
   };
   
   const TargetClient = TargetClient.create(CONFIG);
   
   function startWebServer() {
       //Adobe Target SDK has now downloaded the JSON Artifacts and is available in the memory.
       //You can start your web server now to serve requests now.
   }
   ```

   **Java**

   ```javascript {line-numbers="true"}
   ClientConfig config = ClientConfig.builder()
       .client("<you target client code>")
       .organizationId("<your EC org id>")
       .build();
   TargetClient targetClient = TargetClient.create(config);
   ```

1. 클라이언트와 organizationId를 모두 검색할 수 있습니다. [!DNL Adobe Target] 로 이동하여 **[!UICONTROL 관리]** > **[!UICONTROL 구현]**, 여기에 표시된 대로

   &lt;!— image-client-code.png 삽입 —>
   ![Target의 관리 아래에 있는 구현 페이지](assets/asset-rule-artifact-3.png)

## 3. 규칙 아티팩트 저장 및 사용

규칙 아티팩트를 직접 관리할 필요는 없으며 SDK 메서드를 호출하는 것은 간단해야 합니다.

>[!BEGINTABS]

>[!TAB Node.js]

```javascript {line-numbers="true"}
//req is the request object from the server request listener method
const targetCookie = req.cookies[TargetClient.TargetCookieName];
const request = {
    context: {
        channel: "web"
    },
    execute: {
        mboxes: [{
            address: { url: req.headers.host + req.originalUrl },
            name: "on-device-homepage-banner"
        }],
    },
};

TargetClient.getOffers({
    request,
    targetCookie
}).then(function(response) {
    //This Target response is coming from the In-memory Target artifact.
    console.log("Target response", response);
}).catch(function(err) {
    console.error("Target:", err);
})
```

>[!TAB Java]

```java {line-numbers="true"}
MboxRequest mbox = new MboxRequest().name("homepage").index(0);
TargetDeliveryRequest request = TargetDeliveryRequest.builder()
    .context(new Context().channel(ChannelType.WEB))
    .execute(new ExecuteRequest().mboxes(Arrays.asList(mbox)))
    .build();
TargetDeliveryResponse response = targetClient.getOffers(request);
```

>[!ENDTABS]

>[!NOTE]
>
>위의 코드 샘플에서 `TargetClient` 개체는 메모리 내 규칙 아티팩트에 대한 참조를 보유합니다. 표준 SDK 메서드를 호출하는 데 이 개체를 사용하면 의사 결정에 메모리 내 규칙 아티팩트가 사용됩니다. 애플리케이션이 클라이언트 요청을 초기화하여 수신하는 파일 이외의 파일에서 SDK 메서드를 호출해야 하는 구조로 되어 있고 해당 파일에 TargetClient 개체에 대한 액세스 권한이 없는 경우 JSON 페이로드를 다운로드하여 로컬 JSON 파일에 저장하여 SDK를 초기화해야 하는 다른 파일에서 사용할 수 있습니다. 이에 대해서는 다음 섹션에서 설명합니다 [json 페이로드를 사용하여 규칙 아티팩트 다운로드](rule-artifact-json.md).

다음은 를 초기화한 후 웹 애플리케이션을 시작하는 예입니다. [!DNL Adobe Target] SDK.

>[!BEGINTABS]

>[!TAB Node.js]

```javascript {line-numbers="true"}
const express = require("express");
const cookieParser = require("cookie-parser");
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
    client: "<your target client code>",
    organizationId: "your EC org id",
    decisioningMethod: "on-device",
    pollingInterval : 300000,
    events: {
        clientReady: startWebServer
    }
};

const app = express();
const targetClient = TargetClient.create(CONFIG);

app.use(cookieParser());

function saveCookie(res, cookie) {
  if (!cookie) {
    return;
  }

  res.cookie(cookie.name, cookie.value, {maxAge: cookie.maxAge * 1000});
}

const getResponseHeaders = () => ({
  "Content-Type": "text/html",
  "Expires": new Date().toUTCString()
});

function sendSuccessResponse(res, response) {
  res.set(getResponseHeaders());
  saveCookie(res, response.targetCookie);
  res.status(200).send(response);
}

function sendErrorResponse(res, error) {
  res.set(getResponseHeaders());
  res.status(500).send(error);
}

function startWebServer() {
    app.get('/*', async (req, res) => {
    const targetCookie = req.cookies[TargetClient.TargetCookieName];
    const request = {
        execute: {
        mboxes: [{
            address: { url: req.headers.host + req.originalUrl },
            name: "on-device-homepage-banner" // Ensure that you have a LIVE Activity running on this location
        }]
        }};

    try {
        const response = await targetClient.getOffers({ request, targetCookie });
        sendSuccessResponse(res, response);
    } catch (error) {
        console.error("Target:", error);
        sendErrorResponse(res, error);
    }
    });

    app.listen(3000, function () {
    console.log("Listening on port 3000 and watching!");
    });
}
```

>[!TAB Java]

```java {line-numbers="true"}
import com.adobe.target.edge.client.ClientConfig;
import com.adobe.target.edge.client.TargetClient;
import com.adobe.target.delivery.v1.model.ChannelType;
import com.adobe.target.delivery.v1.model.Context;
import com.adobe.target.delivery.v1.model.ExecuteRequest;
import com.adobe.target.delivery.v1.model.MboxRequest;
import com.adobe.target.edge.client.entities.TargetDeliveryRequest;
import com.adobe.target.edge.client.model.TargetDeliveryResponse;

@Controller
public class TargetController {

  private TargetClient targetClient;

  TargetController() {
    // You should instantiate TargetClient in a Bean and inject the instance into this class 
    // but we show the code here for demonstration purpose.
    ClientConfig config = ClientConfig.builder()
        .client("<you target client code>")
        .organizationId("<your EC org id>")
        .build();
    targetClient = TargetClient.create(config);
  }

  @GetMapping("/")
  public String homePage() {
    MboxRequest mbox = new MboxRequest().name("homepage").index(0);
    TargetDeliveryRequest request = TargetDeliveryRequest.builder()
        .context(new Context().channel(ChannelType.WEB))
        .execute(new ExecuteRequest().mboxes(Arrays.asList(mbox)))
        .build();
    TargetDeliveryResponse response = targetClient.getOffers(request);
    // ...
  }
}
```

>[!ENDTABS]
