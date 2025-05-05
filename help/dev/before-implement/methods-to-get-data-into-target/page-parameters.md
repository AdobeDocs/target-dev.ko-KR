---
keywords: 구현, 구현, 설정, 설정, 페이지 매개 변수
description: 페이지 매개 변수를 사용하여  [!DNL Target] 에 데이터를 가져옵니다.
title: 페이지 매개 변수를 사용하여 데이터를  [!DNL Target] 로 가져오려면 어떻게 해야 합니까?
feature: Implementation
exl-id: 9bb7157e-a938-4150-8a15-c9bf0a0e2296
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 32%

---

# 페이지 매개 변수

페이지 매개 변수(&quot;mbox 매개 변수&quot;라고도 함)는 나중에 사용하기 위해 방문자의 프로필에 저장되지 않은 페이지 코드를 통해 직접 전달되는 이름/값 쌍입니다.

페이지 매개 변수는 나중에 타깃팅할 때 방문자 프로필과 함께 저장할 필요가 없는 페이지 데이터를 [!DNL Adobe Target]에 보내는 데 유용합니다. 대신 이 값은 페이지나, 특정 페이지에서 사용자가 취하는 행동을 설명하는 데 사용됩니다.

## 형식

페이지 매개 변수는 서버 호출을 통해 문자열 이름/값 쌍으로 [!DNL Target]에 전달됩니다. 매개 변수 이름과 값은 사용자 지정할 수 있습니다(특정 용도로 &quot;예약된 이름&quot;도 있음).

다음은 페이지 매개 변수의 몇 가지 예입니다

* `page=productPage`

* `categoryId=homeLoans`

## 예시 사용 사례

* **제품 페이지**: 표시된 특정 제품에 대한 정보를 보냅니다(이 메서드는 Recommendations 작동 방식).
* **주문 세부 사항**: 주문 수집을 위해 주문 ID, orderTotal 등을 보냅니다.
* **카테고리 관심도**: 특정 사이트 카테고리에 대한 사용자의 관심도에 대한 지식을 구축하기 위해 본 카테고리 정보를 [!DNL Target]에 보냅니다.
* **타사 데이터**: 날씨 타깃팅 제공자, 계정 데이터(예: DemandBase), 인구 데이터(예: Experian) 등과 같은 타사 데이터 소스의 정보를 보냅니다.

## 메서드의 이점

데이터는 실시간으로 [!DNL Target] (으)로 전송되며 데이터가 들어오는 동일한 서버 호출에서 사용할 수 있습니다.

## 주의 사항

* 페이지 코드 업데이트가 필요합니다(직접 또는 태그 관리 시스템 사용).
* 후속 페이지/서버 호출에서 타겟팅하는 데 데이터를 사용해야 하는 경우 프로필 스크립트로 변환해야 합니다.
* 쿼리 문자열은 [IETF(Internet Engineering Task Force) 표준](https://www.ietf.org/rfc/rfc3986.txt)에 따라 문자만 포함할 수 있습니다.

  IETF 사이트에 언급된 문자 외에 [!DNL Target]에서는 쿼리 문자열에 다음 문자를 사용할 수 있습니다.

  ```< > # % " { } | \ ^ [ ] ` ``` {line-numbers=&quot;true&quot;}

  다른 모든 문자는 URL로 인코딩해야 합니다. 이 표준에서는 아래 그림과 같이 다음 형식을 지정합니다( [https://www.ietf.org/rfc/rfc1738.txt](https://www.ietf.org/rfc/rfc1738.txt)).

  ![대체 이미지](assets/ietf1.png)

  또는 간단하게 전체 목록을 지정합니다.

  ![대체 이미지](assets/ietf2.png)

## 코드 예

targetPageParamsAll(매개 변수를 페이지의 모든 mbox 호출에 추가합니다.):

`function targetPageParamsAll() { return "param1=value1&param2=value2&p3=hello%20world";`

targetPageParams(매개 변수를 페이지의 글로벌 mbox에 추가합니다.):

`function targetPageParams() { return "param1=value1&param2=value2&p3=hello%20world";`

## 관련 정보 링크

권장 사항: [페이지 유형에 따른 구현](https://experienceleague.adobe.com/docs/target/using/recommendations/plan-implement.html?lang=ko)

주문 확인: [전환 추적](../../implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions)

카테고리 친화성: [카테고리 친화성](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/category-affinity.html?lang=ko)
