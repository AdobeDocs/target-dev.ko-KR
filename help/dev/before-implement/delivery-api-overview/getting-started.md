---
title: Adobe Target 배달 API 시작
description: 사용 방법 [!UICONTROL Adobe Target 게재 API]?
keywords: 배달 api
exl-id: 142ec3be-b017-4cdc-9079-b1cc173a710a
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# 시작하기 [!UICONTROL Adobe Target 게재 API]

A [!UICONTROL Target 배달 API] 호출은 다음과 같습니다.

```
curl -X POST \
  'https://`clientCode`.tt.omtrdc.net/rest/v1/delivery?client=`clientCode`&sessionId=d359234570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
      "context": {
        "channel": "web",
        "browser" : {
          "host" : "demo"
        },
        "address" : {
          "url" : "http://demo.dev.tt-demo.com/demo/store/index.html"
        },
        "screen" : {
          "width" : 1200,
          "height": 1400
        }
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
            "index" : 1
          }
        ]
      }
    }'
```

다음 `clientCode` 에서 검색 가능 [!DNL Target] 로 이동하여 UI **[!UICONTROL 관리]** > **[!UICONTROL 구현]**.

만들기 전 [!UICONTROL Target 배달 API] 를 호출하고 다음 단계에 따라 응답에 최종 사용자에게 표시할 관련 경험이 포함되어 있는지 확인합니다.

1. 만들기 [!DNL Target] 를 사용하는 활동(A/B, XT, AP 또는 Recommendations) [양식 기반 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en) 또는 [시각적 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html).
1. 게재 API를 사용하여에 사용되는 mbox에 대한 응답을 가져옵니다. [!DNL Target] 2단계에서 활동을 만들었습니다.
1. 방문자에게 경험을 선물합니다.

## Postman 컬렉션 {#postman}

Postman은 API 호출을 쉽게 실행할 수 있는 애플리케이션입니다. [이 Postman 컬렉션](https://run.pstmn.io/button.svg) 샘플 배달 API 호출을 포함합니다.
