---
title: 사용자 지정 기준을 관리하는 방법
description: Adobe Target API를 사용하여 Adobe Target Recommendations 기준을 관리, 만들기, 나열, 편집, 가져오기 및 삭제하는 데 필요한 단계입니다.
feature: APIs/SDKs, Recommendations, Administration & Configuration
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: 51a67a49-a92d-4377-9a9f-27116e011ab1
source-git-commit: 2fba03b3882fd23a16342eaab9406ae4491c9044
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 0%

---

# 사용자 지정 기준 관리

경우에 따라 Recommendations에서 제공하는 알고리즘에서 홍보하려는 특정 항목을 표시하지 못할 수 있습니다. 이러한 상황에서 사용자 지정 기준은 주어진 주요 항목 또는 카테고리에 대한 특정 권장 항목 세트를 전달할 수 있는 방법을 제공합니다.

사용자 지정 기준을 만들려면 키 항목 또는 범주와 권장 항목 간에 원하는 매핑을 정의하고 가져옵니다. 이 프로세스는 [사용자 지정 기준 설명서](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html?lang=ko)에 설명되어 있습니다. 해당 설명서에서 설명한 대로 Target UI(사용자 인터페이스)를 통해 사용자 지정 기준을 만들고, 편집하고, 삭제할 수 있습니다. 하지만 Target에서는 사용자 지정 기준을 더 자세히 관리할 수 있는 사용자 지정 기준 API 세트를 제공합니다.

>[!WARNING]
>
>사용자 지정 기준의 경우 API를 사용하여 지정된 사용자 지정 기준에 대한 모든 작업(만들기, 편집, 삭제)을 수행하거나 UI를 사용하여 모든 작업(만들기, 편집, 삭제)을 수행합니다. UI와 API의 조합을 통해 사용자 지정 기준을 관리하면 정보가 충돌하거나 예기치 않은 결과가 발생할 수 있습니다. 예를 들어, UI에서 사용자 지정 기준을 만든 다음 API를 통해 편집하면 API를 통해 볼 수 있듯이 백엔드에서 업데이트되더라도 UI에서 업데이트가 반영되지 않습니다.

## 사용자 지정 기준 만들기

[사용자 지정 기준 만들기 API](https://developer.adobe.com/target/administer/recommendations-api/#operation/createCriteriaCustom)를 사용하여 사용자 지정 기준을 만들려면 구문은 다음과 같습니다.

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

>[!WARNING]
>
>이 연습에서 설명한 대로 사용자 지정 기준 만들기 API를 사용하여 만든 사용자 지정 기준이 UI에 나타나고 여기서 지속됩니다. UI에서 편집하거나 삭제할 수 없습니다. API를 통해 **편집하거나 삭제할 수 있지만** 어느 경우든 Target UI에 계속 표시됩니다. UI에서 편집하거나 삭제하는 옵션을 유지하려면 사용자 지정 기준 만들기 API와 반대로 [설명서](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html?lang=ko)에 대한 UI를 사용하여 사용자 지정 기준을 만드십시오.

위의 경고를 읽고 UI에서 이후에 삭제할 수 없는 새 사용자 지정 기준을 쉽게 만든 후에만 다음 단계를 수행하십시오.

1. **[!UICONTROL Create custom criteria]**&#x200B;에 대한 `TENANT_ID` 및 `API_KEY`이(가) 이전에 설정한 Postman 환경 변수를 참조하는지 확인합니다. 비교를 위해 아래 이미지를 사용하십시오.

   ![CreateCustomCriteria1](assets/CreateCustomCriteria1.png)

1. 사용자 지정 기준 CSV 파일의 위치를 정의하는 **본문**&#x200B;을(를) **원시** JSON으로 추가합니다. [사용자 지정 기준 API 만들기](https://developer.adobe.com/target/administer/recommendations-api/#operation/getAllCriteriaCustom) 설명서에 제공된 예제를 템플릿으로 사용하여 필요에 따라 `environmentId` 및 기타 값을 제공합니다. 이 예에서는 LAST_PURCHASED를 키로 사용합니다.

   ![CreateCustomCriteria2](assets/CreateCustomCriteria2.png)

1. 요청을 보내고 방금 만든 사용자 지정 기준의 세부 사항이 포함된 응답을 관찰합니다.

   ![CreateCustomCriteria3](assets/CreateCustomCriteria3.png)

1. 사용자 지정 기준이 생성되었는지 확인하려면 Adobe Target 내에서 **[!UICONTROL Recommendations > Criteria]**(으)로 이동하여 이름별로 기준을 검색하거나 다음 단계에서 **[!UICONTROL List Custom Criteria API]**&#x200B;을(를) 사용하십시오.

   ![CreateCustomCriteria4](assets/CreateCustomCriteria4.png)

이 경우 오류가 발생합니다. **[!UICONTROL List Custom Criteria API]**&#x200B;을(를) 사용하여 사용자 지정 기준을 더 자세히 검사하여 오류를 조사하겠습니다.

## 사용자 지정 기준 나열

각 항목에 대한 세부 정보와 함께 모든 사용자 지정 기준 목록을 검색하려면 [사용자 지정 기준 나열 API](https://developer.adobe.com/target/administer/recommendations-api/#operation/getAllCriteriaCustom)를 사용하십시오. 구문은 입니다.

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

1. 이전과 같이 `TENANT_ID` 및 `API_KEY`을(를) 확인하고 요청을 보냅니다. 응답에서 사용자 지정 기준 ID와 이전에 기록한 오류 메시지에 대한 세부 사항을 확인합니다.
   ![ListCustomCriteria](assets/ListCustomCriteria.png)

이 경우 서버 정보가 잘못되었기 때문에 오류가 발생했습니다. 즉, Target에서 사용자 지정 기준 정의가 포함된 CSV 파일에 액세스할 수 없습니다. 이 문제를 해결하기 위해 사용자 지정 기준을 편집해 보겠습니다.

## 사용자 지정 기준 편집

사용자 지정 기준 정의의 세부 정보를 변경하려면 [사용자 지정 기준 편집 API](https://developer.adobe.com/target/administer/recommendations-api/#operation/updateCriteriaCustom)를 사용하십시오. 구문은 입니다.

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. 전과 같이 `TENANT_ID` 및 `API_KEY`을(를) 확인합니다.
   ![EditCustomCriteria1](assets/EditCustomCriteria1.png)

1. 편집할 (단일) 사용자 지정 기준의 기준 ID를 지정합니다.
   ![EditCustomCriteria2](assets/EditCustomCriteria2.png)

1. 본문에서 업데이트된 JSON에 올바른 서버 정보를 제공합니다. (이 단계에서는 액세스할 수 있는 서버에 대한 FTP 액세스를 지정합니다.)
   ![EditCustomCriteria3](assets/EditCustomCriteria3.png)

1. 요청을 보내고 응답을 확인합니다.
   ![EditCustomCriteria4](assets/EditCustomCriteria4.png)

**[!UICONTROL Get Custom Criteria API]**&#x200B;을(를) 사용하여 업데이트된 사용자 지정 기준의 성공 여부를 확인하겠습니다.

## 사용자 지정 기준 가져오기

특정 사용자 지정 기준에 대한 사용자 지정 기준 세부 정보를 보려면 [사용자 지정 기준 API 가져오기](https://developer.adobe.com/target/administer/recommendations-api/#operation/getCriteriaCustom)를 사용하십시오. 구문은 입니다.

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. 세부 정보를 가져오려는 사용자 지정 기준의 기준 ID를 지정합니다. 요청을 보내고 응답을 검토합니다.
   ![GetCustomCriteria.png](assets/GetCustomCriteria.png)
1. 성공 여부를 확인합니다. (이 예제에서는 더 이상의 FTP 오류가 없는지 확인합니다.)
   ![GetCustomCriteria1.png](assets/GetCustomCriteria1.png)
1. (선택 사항) 업데이트가 UI에 정확하게 반영되는지 확인합니다.
   ![GetCustomCriteria2.png](assets/GetCustomCriteria2.png)

## 사용자 지정 기준 삭제

앞에서 언급한 기준 ID를 사용하여 [사용자 지정 기준 API 삭제](https://developer.adobe.com/target/administer/recommendations-api/#operation/deleteCriteriaCustom)를 사용하여 사용자 지정 기준을 삭제합니다. 구문은 입니다.

`DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. 삭제하려는 (단일) 사용자 지정 기준의 기준 ID를 지정합니다. **[!UICONTROL Send]** 아이콘을 클릭합니다.
   ![DeleteCustomCriteria1](assets/DeleteCustomCriteria1.png)

1. 사용자 지정 기준 가져오기를 사용하여 기준이 삭제되었는지 확인합니다.
   ![DeleteCustomCriteria2](assets/DeleteCustomCriteria2.png)
이 경우 예상 404 오류는 삭제된 기준을 찾을 수 없음을 나타냅니다.

>[!NOTE]
>
>다시 말해서, 기준은 사용자 정의 기준 만들기 API를 사용하여 생성되었기 때문에 삭제되더라도 Target UI에서 제거되지 않습니다.

축하합니다! 이제 Recommendations API를 사용하여 사용자 지정 기준을 만들고, 나열하고, 편집하고, 삭제하고, 세부 정보를 가져올 수 있습니다. 다음 섹션에서는 Target 게재 API를 사용하여 권장 사항을 검색합니다.

&lt;!— [다음 &quot;서버측 배달 API로 Recommendations 가져오기&quot; >](fetch-recs-server-side-delivery-api.md) —>
