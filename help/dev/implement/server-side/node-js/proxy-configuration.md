---
title: ' [!DNL Adobe Target] Node.js SDK에서 프록시 구성 구현'
description: ' [!DNL Adobe Target] Node.js SDK에서 [!UICONTROL TargetClient] 프록시 구성을 구성하는 방법에 대해 알아봅니다.'
feature: APIs/SDKs
exl-id: c9f04e81-3fa3-4e64-a974-379420b0518a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# 프록시 구성(Node.js)

노드 SDK의 HTTP 요청에 대한 프록시를 구성하려면 초기화하는 동안 SDK에서 사용한 가져오기 API를 재정의합니다.

다음은 프록시를 추가하기 위해 `TargetClient`을(를) 초기화하는 동안 `fetchApi`을(를) 재정의하는 방법을 보여주는 기본 예입니다.

```javascript {line-numbers="true"}
const { ProxyAgent } = require("undici");

const proxyAgent = new ProxyAgent("your proxy address here");

const fetchImpl = (url, options) => {
  const fetchOptions = options;
  fetchOptions.dispatcher = proxyAgent;
  return fetch(url, fetchOptions);
};

client = TargetClient.create({
    ...,
    fetchApi: fetchImpl
});
```

이 기능은 노드 버전 18.2+에서만 작동하며, 여기서 `undici.fetch`은(는) 노드의 기본 `fetch`입니다.
[노드 SDK 샘플 저장소](https://github.com/adobe/target-nodejs-sdk-samples/tree/master/proxy-configuration)를 방문하십시오.
프록시 구성 예제를 참조하십시오.
