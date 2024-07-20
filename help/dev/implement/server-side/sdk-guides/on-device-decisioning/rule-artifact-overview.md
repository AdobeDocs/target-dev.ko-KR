---
title: 온디바이스 의사 결정 규칙 아티팩트 이해
description: ' [!DNL Adobe Target] [!UICONTROL on-device decisioning] 활동의 JSON 표현인 규칙 아티팩트를 사용하는 방법을 알아봅니다.'
feature: APIs/SDKs
exl-id: 3dfb08df-eaa9-43d4-b009-e5f64c3a96d7
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 규칙 아티팩트 개요

규칙 아티팩트는 [!DNL Adobe Target] [!UICONTROL on-device decisioning] 활동의 JSON 표현입니다. [!DNL Adobe Target]에서 생성한 다음 Akamai CDN으로 전파하여 최종 사용자가 가능한 한 가까운 곳에서 규칙 아티팩트를 사용할 수 있도록 합니다. 여기에는 활동을 정확하게 실행 및 전달하는 동시에 이벤트 추적을 통해 실시간 분석을 허용하는 메타데이터가 포함되어 있습니다. [!DNL Adobe Target] SDK는 규칙 아티팩트를 자동으로 관리할 수 있는 방식으로 구성할 수 있으며, 사용자 지정 시간 간격에 따라 다운로드하거나 업데이트할 수 있습니다. 또한 [Memcached](https://memcached.org/)와 같은 분산 메모리 캐싱 시스템을 사용하여 규칙 아티팩트의 로컬 복사본을 유지 관리하여 [!DNL Adobe Target] SDK를 초기화할 수 있으므로 상태 비저장 서버가 요청을 즉시 제공할 수 있습니다. 이러한 옵션에 대한 자세한 내용은 다음 안내서를 참조하십시오.

* [ [!DNL Adobe Target] SDK를 통해 규칙 아티팩트를 자동으로 다운로드, 저장 및 업데이트](rule-artifact-sdk.md)
* [JSON 페이로드를 통해 규칙 아티팩트 다운로드, 저장 및 업데이트](rule-artifact-json.md)

## 규칙 아티팩트 예

[규칙 아티팩트](rule-artifact-example.md)의 예제를 보려면 여기를 클릭하십시오.

## 클라이언트에 대한 규칙 아티팩트를 보는 방법

추적을 사용하도록 설정하면 [!DNL Adobe Target]에서 규칙 아티팩트, 특히 URL과 관련된 추가 정보를 출력합니다.

1. Target UI로 이동합니다.

   &lt;!— image-target-ui-1.png 삽입 —>
   ![대체 이미지](assets/asset-rule-artifact-1.png)

1. **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**(으)로 이동한 다음 **[!UICONTROL Generate New Authorization Token]**&#x200B;을(를) 클릭합니다.

   &lt;!— image-target-ui-2.png 삽입 —>
   ![대체 이미지](assets/asset-rule-artifact-2.png)

1. 새로 생성된 인증 토큰을 클립보드에 복사하고 Target 요청에 추가합니다.

   ```javascript {line-numbers="true"}
   const request = {
     trace: {
       authorizationToken: '88f1a924-6bc5-4836-8560-2f9c86aeb36b'
     },
     execute: {
       mboxes: [{
         address: getAddress(req),
         name: "node-sdk-mbox"
       }]
   }};
   ```

1. 터미널을 통해 Target 추적을 출력하여 아티팩트에 대한 세부 사항을 확인합니다. `artifactLocation` 변수를 통해 URL에 액세스할 수 있습니다.

   ```
   "trace": {
     "clientCode": "your-client-code",
     "artifact": {
       "artifactLocation": "https://assets.adobetarget.com/your-client-code/production/v1/rules.bin",
       "pollingInterval": 300000,
       "pollingHalted": false,
       "artifactVersion": "1.0.0",
       "artifactRetrievalCount": 10,
       "artifactLastRetrieved": "2020-09-20T00:09:42.707Z",
        "clientCode": "your-client-code",
      "environment": "production",
       "generatedAt": "2020-09-22T17:17:59.783Z"
     },
   ```
