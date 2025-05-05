---
title: Experience Cloud AAM 세그먼트와 통합
description: Experience Cloud과 통합, Audience Manager 통합
keywords: 배달 api, 서버측, 서버측, 통합, audience manager, aam
exl-id: c21e0200-23ba-4a0b-adf4-38e03c087f00
feature: Implement Server-side
source-git-commit: e3f14e97fa48ffb1f07b29aca5711d16e75faa80
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 4%

---

# AAM 세그먼트

[!DNL Adobe Target] SDK를 통해 [!DNL Adobe Audience Manager] 세그먼트를 활용할 수 있습니다. AAM 세그먼트를 활용하려면 다음 필드를 제공해야 합니다.

>[!NOTE]
>
>AAM 세그먼트는 온디바이스 의사 결정 활동에 대해 지원되지 않습니다.

| 필드 이름 | 필수 | 설명 |
| --- | --- | --- |
| `locationHint` | 예 | DCS 위치 힌트는 프로필을 검색하기 위해 히트할 AAM DCS 끝점을 결정하는 데 사용됩니다. 1보다 크거나 같아야 합니다. |
| `marketingCloudVisitorId` | 예 | Marketing Cloud 방문자 ID |
| `blob` | 예 | AAM Blob을 사용하여 추가 데이터를 AAM에 보낼 수 있습니다. 비워 둘 수 없으며 크기는 1024 미만이어야 합니다. |

`getOffers` 메서드를 호출할 때 SDK에서 이 필드를 자동으로 채우지만 올바른 방문자 쿠키가 제공되었는지 확인해야 합니다. 이 쿠키를 가져오려면 브라우저에서 VisitorAPI.js를 구현해야 합니다.

## Implementation 안내서

### 쿠키 사용

쿠키는 [!DNL Adobe Audience Manager] 요청을 [!DNL Adobe Target] 요청과 상호 연결하는 데 사용됩니다. 이러한 쿠키는 이 구현에 사용되는 쿠키입니다.

| 쿠키 | 이름 | 설명 |
| --- | --- | --- |
| 방문자 쿠키 | `AMCVS_XXXXXXXXXXXXXXXXXXXXXXXX%40AdobeOrg` | 이 쿠키는 대상 `getOffers` 응답에서 `visitorState`(으)로 초기화될 때 `VisitorAPI.js`에 의해 설정됩니다. |
| target 쿠키 | `mbox` | 웹 서버는 대상 `getOffers` 응답의 `targetCookie` 이름과 값을 사용하여 이 쿠키를 설정해야 합니다. |

### 단계 개요

사용자가 웹 서버에 요청을 보내는 브라우저에 URL을 입력한다고 가정합니다. 해당 요청을 이행하는 경우:

1. 서버는 요청에서 방문자 및 타겟 쿠키를 읽습니다.
1. 서버가 [!DNL Target] SDK의 `getOffers` 메서드를 호출하여 사용 가능한 경우 방문자 및 대상 쿠키를 지정합니다.
1. `getOffers` 호출이 이행되면 응답의 `targetCookie` 및 `visitorState`에 대한 값이 사용됩니다.
   1. 쿠키는 `targetCookie`에서 가져온 값으로 응답에 설정됩니다. 이 작업은 브라우저에 타겟 쿠키를 지속하도록 알리는 `Set-Cookie` 응답 헤더를 사용하여 수행됩니다.
   1. `VisitorAPI.js`을(를) 초기화하고 대상 응답에서 `visitorState`을(를) 전달하는 HTML 응답이 준비되었습니다.
1. HTML 응답이 브라우저에 로드되었습니다.
   1. `VisitorAPI.js`이(가) 문서 헤더에 포함되어 있습니다.
   1. VisitorAPI가 `getOffers` SDK 응답에서 `visitorState`(으)로 초기화되었습니다. 그러면 방문자 쿠키가 브라우저에서 설정되므로, 후속 요청 시 서버로 전송됩니다.

### 예제 코드

다음 코드 샘플은 위에 설명된 각 단계를 구현합니다. 각 단계는 구현 옆에 인라인 주석으로 코드에 표시됩니다.

#### Node.js

이 샘플은 [express, Node.js 웹 프레임워크](https://expressjs.com/)를 사용합니다.

>[!BEGINTABS]

>[!TAB server.js]

```js {line-numbers="true"}
const fs = require("fs");
const express = require("express");
const cookieParser = require("cookie-parser");
const Handlebars = require("handlebars");
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg",
  timeout: 10000,
  logger: console,
};
const targetClient = TargetClient.create(CONFIG);
const TEMPLATE = fs.readFileSync(`${__dirname}/index.handlebars`).toString();
const handlebarsTemplate = Handlebars.compile(TEMPLATE);

Handlebars.registerHelper("toJSON", function (object) {
  return new Handlebars.SafeString(JSON.stringify(object, null, 4));
});

const app = express();
app.use(cookieParser());
app.use(express.static(__dirname + "/public"));

app.get("/", async (req, res) => {
  // The server reads the visitor and target cookies from the request.
  const visitorCookie =
    req.cookies[
      encodeURIComponent(
        TargetClient.getVisitorCookieName(CONFIG.organizationId)
      )
    ];
  const targetCookie = req.cookies[TargetClient.TargetCookieName];
  const address = { url: req.headers.host + req.originalUrl };

  const targetRequest = {
    execute: {
      mboxes: [
        { name: "homepage", index: 1, address },
        { name: "SummerShoesOffer", index: 2, address },
        { name: "SummerDressOffer", index: 3, address }
      ],
    },
  };

  res.set({
    "Content-Type": "text/html",
    Expires: new Date().toUTCString(),
  });

  try {
    // The server makes a call to the `getOffers` method of the Target SDK specifying the visitor and target cookies if available.
    const targetResponse = await targetClient.getOffers({
      request: targetRequest,
      visitorCookie,
      targetCookie,
    });

    // When the `getOffers` call is fulfilled, values for `targetCookie` and `visitorState` from the response are used.
    // A cookie is set on the response with values taken from `targetCookie`.  This is done using the `Set-Cookie` response header which tells the browser to persist the target cookie.
    res.cookie(
      targetResponse.targetCookie.name,
      targetResponse.targetCookie.value,
      { maxAge: targetResponse.targetCookie.maxAge * 1000 }
    );

    // An HTML response is prepared that initializes VisitorAPI.js and passes in `visitorState` from the target response.
    const html = handlebarsTemplate({
      organizationId: CONFIG.organizationId,
      targetResponse,
    });

    res.status(200).send(html);
  } catch (error) {
    console.error("Target:", error);
    res.status(500).send(error);
  }
});

app.listen(3000, function () {
  console.log("Listening on port 3000 and watching!");
});
```

>[!TAB index.handlebars]

```html {line-numbers="true"}
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ECID (Visitor API) Integration Sample</title>

  <!-- VisitorAPI.js is included in the document header. -->
  <script src="VisitorAPI.js"></script>
  <script>
    // VisitorAPI is initialized with visitorState from the `getOffers` SDK response. This will cause the visitor cookie to be set in the browser so it will be sent to the server on subsequent requests.
    Visitor.getInstance("{{organizationId}}", {serverState: {{toJSON targetResponse.visitorState}} });
  </script>
</head>
<body>
  <h1>response</h1>
  <pre>{{toJSON targetResponse}}</pre>
</body>
</html>
```

>[!ENDTABS]

#### Java

이 샘플은 [spring, Java 웹 프레임워크](https://spring.io/)를 사용합니다.

>[!BEGINTABS]

>[!TAB ClientSampleApplication.java]

```java {line-numbers="true"}
@SpringBootApplication
public class ClientSampleApplication {

    public static void main(String[] args) {
        System.setProperty(SimpleLogger.DEFAULT_LOG_LEVEL_KEY, "DEBUG");
        SpringApplication.run(ClientSampleApplication.class, args);
    }

    @Bean
    TargetClient marketingCloudClient() {
        ClientConfig clientConfig = ClientConfig.builder()
                .client("acmeclient")
                .organizationId("1234567890@AdobeOrg")
                .defaultDecisioningMethod(DecisioningMethod.SERVER_SIDE)
                .build();

        return TargetClient.create(clientConfig);
    }
}
```

>[!TAB TargetController.java]

```java {line-numbers="true"}
@Controller
@RequestMapping("/")
public class TargetController {

    @Autowired
    private TargetClientService targetClientService;

    @GetMapping
    public String index(Model model, HttpServletRequest request, HttpServletResponse response) {
        // The server reads the visitor and target cookies from the request.
        List<TargetCookie> targetCookies = getTargetCookies(request.getCookies());

        Address address = getAddress(request);

        List<MboxRequest> mboxRequests = new ArrayList<>();
        mboxRequests.add((MboxRequest) new MboxRequest().name("homepage").index(1).address(address));
        mboxRequests.add((MboxRequest) new MboxRequest().name("SummerShoesOffer").index(2).address(address));
        mboxRequests.add((MboxRequest) new MboxRequest().name("SummerDressOffer").index(3).address(address));

        TargetDeliveryResponse targetDeliveryResponse = targetClientService.getOffers(mboxRequests, targetCookies, request,
                response);

        // An HTML response is prepared that initializes VisitorAPI.js and passes in `visitorState` from the target response.
        model.addAttribute("visitorState", targetDeliveryResponse.getVisitorState());
        model.addAttribute("targetResponse", targetDeliveryResponse);
        model.addAttribute("organizationId", "1234567890@AdobeOrg");

        return "index";
    }
}
```

>[!TAB TargetClientService.java]

```java {line-numbers="true"}
@Service
public class TargetClientService {

    private final TargetClient targetJavaClient;

    public TargetClientService(TargetClient targetJavaClient) {
        this.targetJavaClient = targetJavaClient;
    }

    public TargetDeliveryResponse getOffers(List<MboxRequest> executeMboxes, List<TargetCookie> cookies, HttpServletRequest request, HttpServletResponse response) {

        Context context = getContext(request);
        ExecuteRequest executeRequest = new ExecuteRequest();
        executeRequest.setMboxes(executeMboxes);

        TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
                .context(context)
                .execute(executeRequest)
                .cookies(cookies)
                .build();

        // The server makes a call to the `getOffers` method of the Target SDK specifying the visitor and target cookies if available.
        TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);

        // When the `getOffers` call is fulfilled, values for `targetCookie` and `visitorState` from the response are used.
        // A cookie is set on the response with values taken from `targetCookie`.  This is done using the `Set-Cookie` response header which tells the browser to persist the target cookie.
        setCookies(targetResponse.getCookies(), response);
        return targetResponse;
    }
}
```

>[!TAB TargetRequestUtils.java]

```java {line-numbers="true"}
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Target Only : GetOffer</title>

    <!-- VisitorAPI.js is included in the document header. -->
    <script src="../../js/VisitorAPI.js"></script>
    <script th:inline="javascript">
        // VisitorAPI is initialized with visitorState from the `getOffers` SDK response. This will cause the visitor cookie to be set in the browser so it will be sent to the server on subsequent requests.
        Visitor.getInstance(/*[[${organizationId}]]*/ "", {serverState: /*[[${visitorState}]]*/ {}});
    </script>
</head>
<body>
    <h1>response</h1>
    <pre>[[${targetResponse}]]</pre>
</body>
</html>
```

>[!ENDTABS]

`TargetRequestUtils.java`에 대한 자세한 내용은 [유틸리티 메서드(Java)](https://experienceleague.adobe.com/docs/target-dev/developer/server-side/java/utility-methods.html?lang=ko){target=_blank}를 참조하십시오.
