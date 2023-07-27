---
title: Adobe Target 배달 API 클라이언트 힌트
description: 에서 클라이언트 힌트를 사용하는 방법 [!DNL Adobe Target] 배달 API?
exl-id: 317b9d7d-5b98-464e-9113-08b899ee1455
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# 클라이언트 힌트 및 [!UICONTROL Adobe Target 게재 API]

클라이언트 힌트를 (으)로 보내야 합니다. [!DNL Adobe Target] 오퍼 요청 시.

일반적으로 사용 가능한 모든 클라이언트 힌트를 로 전송하는 것이 좋습니다. [!DNL Target]. 자세한 내용은 [사용자 에이전트 및 클라이언트 힌트](/help/dev/implement/client-side/atjs/user-agent-and-client-hints.md) 다음에서 [클라이언트측 구현](../../implement/client-side/overview.md) 섹션.

## 배달 API 직접 호출

### 브라우저에서

이 경우 브라우저는 낮은 엔트로피 클라이언트 힌트를 로 보냅니다. [!DNL Target] 요청 헤더를 통해 자동으로. 그러나 이 구현에는 두 가지 브라우저 수준의 제한이 있습니다. 첫 번째 - https를 통해 요청을 하는 경우가 아니면 브라우저에서 클라이언트 힌트 헤더가 전송되지 않습니다. 두 번째 - 클라이언트 힌트는 첫 번째 요청에서에 전송되지 않습니다. [!DNL Target] 페이지에서 참조할 수 있습니다. 클라이언트 힌트 헤더는 두 번째 요청과 그 이후의 모든 요청에 대해서만 전송됩니다. 즉, 대상자 세분화 및 개인화는에서 수행할 수 없습니다 [!DNL Target] 첫 번째 페이지에서 를 방문하십시오. 이러한 두 가지 제한 사항을 모두 해결하려면 브라우저에서 사용자 에이전트 클라이언트 힌트 API 를 사용하여 클라이언트 힌트를 직접 수집한 다음 요청 페이로드에서 전송하는 것이 좋습니다.

### 서버에서

이 경우 클라이언트 힌트를 브라우저에서 로 수동으로 전달해야 합니다. [!DNL Target] 게재 API 요청 시.

```
curl -X POST 'http://mboxedge28.tt.omtrdc.net/rest/v1/delivery?client=myClientCode&sessionId=abcdefghijkl00014' -d '{
  "context": {
    "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Safari/537.36",
    "clientHints": {
      "Sec-CH-UA-Model": "iPhone",
      "Sec-CH-UA-Mobile": true,
      "Sec-CH-UA-Platform": "iOS",
      "Sec-CH-UA": "[ { \"brand\": \"Chromium\", \"version\": \"91\" }, { \"brand\": \" Not;A Brand\", \"version\": \"99\" } ]",
      "Sec-CH-UA-Full-Version-List": "[ { \"brand\": \"Chromium\", \"version\": \"91.1.1.1\" }, { \"brand\": \" Not;A Brand\", \"version\": \"99.1.1.1\" } ]",
      "Sec-CH-UA-Platform-Version": "10.0.0",
      "Sec-CH-UA-Arch": "x86",
      "Sec-CH-UA-Bitness": "64"
    }
  },
  "execute": {
    "mboxes": [{
      "name": "home",
      "index": 1
    }]
  }
}'
```

## 서식 지정

클라이언트 힌트 헤더 Sec-CH-UA 및 Sec-CH-UA-Full-Version-List의 형식이 클라이언트 힌트 브라우저 API(navigator.userAgentData.brands/navigator.userAgentData.getHighEntropyValues)의 결과와 다릅니다. 이러한 두 형식은 모두 배달 API에서 허용됩니다. 게재 API는 값을 요청 헤더에 사용된 형식으로 정규화합니다. 이는 프로필 스크립트의 클라이언트 힌트에 액세스할 때 유의해야 합니다.
