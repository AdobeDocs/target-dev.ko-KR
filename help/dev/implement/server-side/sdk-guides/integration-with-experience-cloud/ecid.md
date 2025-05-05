---
title: Experience Cloud ID(ECID) 서비스
description: ' [!DNL Target] 에서 콘텐츠를 가져오는 데  [!DNL Target] SDK를 사용하는 것은 강력한 기능이지만 사용자 추적을 위해 [!UICONTROL Experience Cloud ID] (ECID)를 사용하는 것의 추가 가치는 A4T 보고 및 [!DNL Adobe Audience Manager] (AAM) 세그먼트와 같은 Adobe [!DNL Target]. The ECID enables you to leverage [!DNL Adobe Experience Cloud] 제품 및 기능 이상으로 확장됩니다.'
exl-id: fd7e5c3e-51c1-4965-ab6a-f50a6b0c910b
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# [!UICONTROL Experience Cloud ID] (ECID) 서비스

## [!UICONTROL Experience Cloud ID] (ECID) 통합

[!DNL Target]에서 콘텐츠를 가져오는 데 [!DNL Target] SDK를 사용하는 것이 강력할 수 있지만 사용자 추적을 위해 [!UICONTROL Experience Cloud ID] (ECID)을 사용하는 추가 가치는 [!DNL Adobe Target]을(를) 초과합니다. ECID를 사용하면 A4T 보고 및 [!DNL Adobe Audience Manager] (AAM) 세그먼트와 같은 [!DNL Adobe Experience Cloud]개의 제품 및 기능을 활용할 수 있습니다.

ECID는 자체 상태를 유지하는 `visitor.js`에 의해 생성 및 유지 관리됩니다. `visitor.js` 파일은 ECID 통합을 위해 [!DNL Target] SDK에서 사용하는 `AMCV_{organizationId}` 쿠키를 만듭니다. [!DNL Target] 응답이 반환되면 클라이언트측의 방문자 인스턴스를 [!DNL Target] SDK에서 반환된 `thevisitorState`(으)로 업데이트해야 합니다.

```html {line-numbers="true"}
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ECID (Visitor API) Integration Sample</title>
  <script src="VisitorAPI.js"></script>
  <script>
    Visitor.getInstance("${organizationId}", {serverState: ${visitorState}});
  </script>
</head>
<body>
  <pre>Sample content</pre>
</body>
</html>
```

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const express = require("express");
const cookieParser = require("cookie-parser");
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};
const TEMPLATE = `
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ECID (Visitor API) Integration Sample</title>
  <script src="VisitorAPI.js"></script>
  <script>
    Visitor.getInstance("${organizationId}", {serverState: ${visitorState}});
  </script>
</head>
<body>
  <pre>${content}</pre>
</body>
</html>
`;

const app = express();
const targetClient = TargetClient.create(CONFIG);

app.use(cookieParser());
// We assume that VisitorAPI.js is stored in "public" folder
app.use(express.static(__dirname + "/public"));

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

  const result = TEMPLATE
  .replace("${organizationId}", CONFIG.organizationId)
  .replace("${visitorState}", JSON.stringify(response.visitorState))
  .replace("${content}", response);

  saveCookie(res, response.targetCookie);

  res.status(200).send(result);
}

function sendErrorResponse(res, error) {
  res.set(getResponseHeaders());
  res.status(500).send(error);
}

app.get("/abtest", async (req, res) => {
  const visitorCookie = req.cookies[TargetClient.getVisitorCookieName(CONFIG.organizationId)];
  const targetCookie = req.cookies[TargetClient.TargetCookieName];
  const request = {
      execute: {
        mboxes: [{
          address: { url: req.headers.host + req.originalUrl },
          name: "a1-serverside-ab"
        }]
      }};
```

>[!TAB Java]

```java {line-numbers="true"
  console.log("Request", request);

  try {
      const response = await targetClient.getOffers({ request, visitorCookie, targetCookie });
      sendSuccessResponse(res, response);
    } catch (error) {
      sendErrorResponse(res, error);
    }
});

app.listen(3000, function () {
  console.log("Listening on port 3000 and watching!");
});
@Controller
public class TargetControllerSample {

  @Autowired
  private TargetClient targetClient;

  @GetMapping("/")
  public String targetMcid(Model model, HttpServletRequest request, HttpServletResponse response) {
    Context context = getContext(request);
    TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
        .context(context)
        .prefetch(getPrefetchRequest())
        .cookies(getTargetCookies(request.getCookies()))
        .build();

    TargetDeliveryResponse targetResponse = targetClient.getOffers(targetDeliveryRequest);
    model.addAttribute("visitorState", targetResponse.getVisitorState());
    model.addAttribute("organizationId", "0DD934B85278256B0A490D44@AdobeOrg");
    setCookies(targetResponse.getCookies(), response);
    return "targetMcid";
  }
}
```

>[!ENDTABS]

## 고객 ID가 통합된 ECID

방문자 사용자 계정 및 로그인 상태 세부 정보를 추적하기 위해 [!DNL Target] SDK를 통해 `customerIds`을(를) 전달할 수 있습니다.

```html {line-numbers="true"
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ECID (Visitor API) Integration Sample</title>
  <script src="VisitorAPI.js"></script>
  <script>
    Visitor.getInstance("${organizationId}", {serverState: ${visitorState}});
  </script>
</head>
<body>
  <pre>Sample content</pre>
</body>
</html>
```

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const express = require("express");
const cookieParser = require("cookie-parser");
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};
const TEMPLATE = `
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ECID (Visitor API) with Customer IDs Integration Sample</title>
  <script src="VisitorAPI.js"></script>
  <script>
    Visitor.getInstance("${organizationId}", {serverState: ${visitorState}});
  </script>
</head>
<body>
  <pre>${content}</pre>
</body>
</html>
`;

const app = express();
const targetClient = TargetClient.create(CONFIG);

app.use(cookieParser());
// We assume that VisitorAPI.js is stored in "public" folder
app.use(express.static(__dirname + "/public"));

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

  const result = TEMPLATE
  .replace("${organizationId}", CONFIG.organizationId)
  .replace("${visitorState}", JSON.stringify(response.visitorState))
  .replace("${content}", response);

  saveCookie(res, response.targetCookie);

  res.status(200).send(result);
}

function sendErrorResponse(res, error) {
  res.set(getResponseHeaders());
  res.status(500).send(error);
}

app.get("/abtest", async (req, res) => {
  const visitorCookie = req.cookies[TargetClient.getVisitorCookieName(CONFIG.organizationId)];
  const targetCookie = req.cookies[TargetClient.TargetCookieName];
  const customerIds = {
      "userid": {
        "id": "67312378756723456",
        "authState": TargetClient.AuthState.AUTHENTICATED
      }
    };
  const request = {
    execute: {
      mboxes: [{
        address: { url: req.headers.host + req.originalUrl },
        name: "a1-serverside-ab"
      }]
    }};

  try {
    const response = await targetClient.getOffers({ request, visitorCookie, targetCookie, customerIds });
    sendSuccessResponse(res, response);
  } catch (error) {
    sendErrorResponse(res, error);
  }
});

app.listen(3000, function () {
  console.log("Listening on port 3000 and watching!");
});
```

>[!TAB Java]

```java {line-numbers="true"}
@Controller
public class TargetControllerSample {

  @Autowired
  private TargetClient targetJavaClient;

  @GetMapping("/targetMcid")
  public String targetMcid(Model model, HttpServletRequest request, HttpServletResponse response) {
    Context context = getContext(request);
    Map<String, CustomerState> customerIds = new HashMap<>();
    customerIds.put("userid", CustomerState.authenticated("67312378756723456"));
    customerIds.put("puuid", CustomerState.unknown("550e8400-e29b-41d4-a716-446655440000"));
    TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
       .context(context)
       .prefetch(getPrefetchRequest())
       .cookies(getTargetCookies(request.getCookies()))
       .customerIds(customerIds)
       .build();

    TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);
    model.addAttribute("visitorState", targetResponse.getVisitorState());
    model.addAttribute("organizationId", "0DD934B85278256B0A490D44@AdobeOrg");
    setCookies(targetResponse.getCookies(), response);
    return "targetMcid";
  }
}
```

>[!ENDTABS]

## ECID 및 [!DNL Analytics] 통합

[!DNL Target] SDK를 최대한 활용하고 [!DNL Adobe Analytics]에서 제공하는 강력한 분석 기능을 사용하려면 ECID, [!DNL Analytics] 및 [!DNL Target] 간의 통합을 사용할 수 있습니다.

ECID, [!DNL Analytics] 및 [!DNL Target]에서 통합을 사용하면 다음 작업을 수행할 수 있습니다.

* Adobe Audience Manager(AAM)의 세그먼트 사용
* [!DNL Target]에서 검색한 콘텐츠를 기반으로 사용자 경험 사용자 지정
* 모든 이벤트 및 성공 지표가 [!DNL Analytics]에 수집되었는지 확인합니다.
* [!DNL Analytics]의 강력한 쿼리를 사용하고 멋진 보고서 시각화를 활용할 수 있습니다.

ECID, [!DNL Analytics] 및 [!DNL Target] 간의 통합에서는 서버측에서 분석을 특별히 처리할 필요가 없습니다. 대신 ECID가 통합되면 클라이언트측에서 `AppMeasurement.js`([!DNL Analytics] 라이브러리)을(를) 추가합니다. 그런 다음 [!DNL Analytics]은(는) 방문자 인스턴스를 사용하여 [!DNL Target]과(와) 동기화합니다.

```html {line-numbers="true"}
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ECID and Analytics integration Sample</title>
  <script src="VisitorAPI.js"></script>
  <script>
    Visitor.getInstance("${organizationId}", {serverState: ${visitorState}});
  </script>
</head>
<body>
  <p>Sample content</p>
  <script src="AppMeasurement.js"></script>
  <script>var s_code=s.t();if(s_code)document.write(s_code);</script>
</body>
</html>
```

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const express = require("express");
const cookieParser = require("cookie-parser");
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};
const TEMPLATE = `
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ECID and Analytics integration Sample</title>
  <script src="VisitorAPI.js"></script>
  <script>
    Visitor.getInstance("${organizationId}", {serverState: ${visitorState}});
  </script>
</head>
<body>
  <p>${content}</p>
  <script src="AppMeasurement.js"></script>
  <script>var s_code=s.t();if(s_code)document.write(s_code);</script>
</body>
</html>
`;

const app = express();
const targetClient = TargetClient.create(CONFIG);

app.use(cookieParser());
// We assume that VisitorAPI.js and AppMeasurement.js are stored in "public" directory
app.use(express.static(__dirname + "/public"));

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

  const result = TEMPLATE
  .replace("${organizationId}", CONFIG.organizationId)
  .replace("${visitorState}", JSON.stringify(response.visitorState))
  .replace("${content}", response);

  saveCookie(res, response.targetCookie);

  res.status(200).send(result);
}

function sendErrorResponse(res, error) {
  res.set(getResponseHeaders());

  res.status(500).send(error);
}

app.get("/abtest", async (req, res) => {
  const visitorCookie = req.cookies[TargetClient.getVisitorCookieName(CONFIG.organizationId)];
  const targetCookie = req.cookies[TargetClient.TargetCookieName];
  const request = {
      execute: {
        mboxes: [{
          address: { url: req.headers.host + req.originalUrl },
          name: "a1-serverside-ab"
        }]
      }};

    try {
      const response = await targetClient.getOffers({ request, visitorCookie, targetCookie });
      sendSuccessResponse(res, response);
    } catch (error) {
      sendErrorResponse(res, error);
    }
});

app.listen(3000, function () {
  console.log("Listening on port 3000 and watching!");
});
```

>[!TAB Java]

```java {line-numbers="true"}
@Controller
public class TargetControllerSample {

    @Autowired
    private TargetClient targetJavaClient;

    @GetMapping("/targetAnalytics")
    public String targetMcid(Model model, HttpServletRequest request, HttpServletResponse response) {
        Context context = getContext(request);
        Map<String, CustomerState> customerIds = new HashMap<>();
        customerIds.put("userid", CustomerState.authenticated("67312378756723456"));
        customerIds.put("puuid", CustomerState.unknown("550e8400-e29b-41d4-a716-446655440000"));
        TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
                .context(context)
                .prefetch(getPrefetchRequest())
                .cookies(getTargetCookies(request.getCookies()))
                .customerIds(customerIds)
                .trackingServer("imsbrims.sc.omtrds.net")
                .build();

        TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);
        model.addAttribute("visitorState", targetResponse.getVisitorState());
        model.addAttribute("organizationId", "0DD934B85278256B0A490D44@AdobeOrg");
        setCookies(targetResponse.getCookies(), response);
        return "targetAnalytics";
    }
```

>[!ENDTABS]
