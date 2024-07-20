---
title: Adobe Target 배달 API 클라이언트 힌트
description: ' [!DNL Adobe Target] 배달 API에서 클라이언트 힌트를 사용하는 방법은 무엇입니까?'
exl-id: 317b9d7d-5b98-464e-9113-08b899ee1455
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# 클라이언트 힌트 및 [!UICONTROL Adobe Target Delivery API]

오퍼 요청 시 클라이언트 힌트를 [!DNL Adobe Target](으)로 보내야 합니다.

일반적으로 사용 가능한 모든 클라이언트 힌트를 [!DNL Target]에 보내는 것이 좋습니다. 자세한 내용은 [클라이언트측 구현](../../implement/client-side/overview.md) 섹션에서 [사용자 에이전트 및 클라이언트 힌트](/help/dev/implement/client-side/atjs/user-agent-and-client-hints.md)를 참조하십시오.

## 배달 API 직접 호출

### 브라우저에서

이 경우 브라우저는 요청 헤더를 통해 낮은 엔트로피 클라이언트 힌트를 [!DNL Target]에 자동으로 전송합니다. 그러나 이 구현에는 두 가지 브라우저 수준의 제한이 있습니다. 첫 번째 - https를 통해 요청을 하는 경우가 아니면 브라우저에서 클라이언트 힌트 헤더가 전송되지 않습니다. 두 번째 - 페이지의 [!DNL Target]에게 첫 번째 요청 시 클라이언트 힌트가 전송되지 않습니다. 클라이언트 힌트 헤더는 두 번째 요청과 그 이후의 모든 요청에 대해서만 전송됩니다. 즉, [!DNL Target]이(가) 첫 번째 페이지 방문 시 대상 세분화 및 개인화를 수행할 수 없습니다. 이러한 두 가지 제한 사항을 모두 해결하려면 브라우저에서 사용자 에이전트 클라이언트 힌트 API 를 사용하여 클라이언트 힌트를 직접 수집한 다음 요청 페이로드에서 전송하는 것이 좋습니다.

### 서버에서

이 경우 배달 API 요청 시 브라우저에서 [!DNL Target](으)로 클라이언트 힌트를 수동으로 전달해야 합니다.

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
