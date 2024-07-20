---
title: Adobe Target Delivery API 사용자 권한
description: Adobe Target Delivery API 사용자 권한
badgePremium: label="Premium" type="Positive" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=en#premium newtab=true" tooltip="Target Premium에 포함된 내용을 확인하십시오."
keywords: 배달 api
exl-id: 332f90bd-4079-4653-aa38-b35837631c94
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# 사용자 권한(Premium)

[!DNL Adobe]을(를) 사용하면 고객이 Adobe Target을 사용할 때 사용자에 대한 권한을 관리할 수 있습니다. [!UICONTROL Adobe Target Delivery API]을(를) 성공적으로 호출하려면 올바른 권한이 있는 토큰을 API 호출 내에 전달해야 합니다. 사용자 권한 부여 및 토큰을 검색하는 방법에 대해 자세히 알아보려면 [이 설명서](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html)를 참조하세요.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e04f14e1faeeba02d6ab9914e' \
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
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
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

해당 토큰이 있으면 모든 API 호출에 대해 `property` -> `token`에 전달합니다. 모든 API 호출 내에서 `property` -> `token`이(가) 전달되지 않으면 Adobe Target에서 `content`을(를) 다시 가져올 수 없습니다.

```
{
    "status": 200,
    "requestId": "07ce783d-58b9-461c-9f4c-6873aeb00c01",
    "client": "demo",
    "id": {
        "tntId": "d359234570e04f14e1faeeba02d6ab9914e.28_7"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "execute": {
        "mboxes": [
            {
                "index": 1,
                "name": "homepage"
            }
        ]
    }
}
```

위에서 보듯이 `property` -> `token`을(를) 전달하지 않으면 콘텐츠를 다시 가져올 수 없습니다. API 호출에서 콘텐츠가 필요하지만 응답에서 콘텐츠를 검색하지 않는 경우, `property` -> `token`이(가) 제공되지 않았거나 올바른 권한 없이 전달되고 있기 때문일 수 있습니다.
