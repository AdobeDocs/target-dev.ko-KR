---
title: Adobe Target 배달 API 시작
description: '[!UICONTROL Adobe Target Delivery API]을(를) 사용하는 방법'
keywords: 배달 api
exl-id: 142ec3be-b017-4cdc-9079-b1cc173a710a
feature: APIs/SDKs
source-git-commit: e5a1c38d448cb7446b7b26cd0dc882976ba94dd3
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# [!UICONTROL Adobe Target Delivery API] 시작

[!UICONTROL Target Delivery API] 호출은 다음과 같습니다.

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

**[!UICONTROL Administration]** > **[!UICONTROL Implementation]**(으)로 이동하여 [!DNL Target] UI에서 `clientCode`을(를) 검색할 수 있습니다.

[!UICONTROL Target Delivery API] 호출을 수행하기 전에 다음 단계에 따라 응답에 관련 경험이 포함되어 있는지 확인하여 최종 사용자에게 표시합니다.

1. [양식 기반 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en) 또는 [시각적 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)를 사용하여 [!DNL Target] 활동(A/B, XT, AP 또는 Recommendations)을 만듭니다.
1. 배달 API를 사용하여 2단계에서 만든 [!DNL Target] 활동에 사용된 mbox에 대한 응답을 가져옵니다.
1. 방문자에게 경험을 선물합니다.
