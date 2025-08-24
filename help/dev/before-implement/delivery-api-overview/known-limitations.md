---
title: Adobe Target 배달 API 고려 사항 및 알려진 제한 사항
description: '[!UICONTROL Adobe Target Delivery API]을(를) 사용할 때 고려해야 할 고려 사항과 알려진 제한 사항은 무엇입니까?'
keywords: 배달 api
exl-id: 49fe13b0-efcb-4b1c-a4cb-03b64fbd9214
feature: APIs/SDKs
source-git-commit: 413b16ed0b098de6914558fa29b9ca59aaba958e
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 3%

---

# 고려 사항 및 알려진 제한 사항

다음 정보에는 [!DNL Adobe Target] [!DNL Delivery API] 사용에 대한 고려 사항 및 알려진 제한 사항이 나와 있습니다.

* [!DNL Target] 배달 API에 대한 인증이 없습니다.
* 이 API는 쿠키를 처리하거나 호출을 리디렉션하지 않습니다.
* HTTP/1.1과 HTTP/2 헤더 이름은 모두 대소문자를 구분하지 않지만, HTTP/2는 소문자 헤더 이름을 적용합니다. 자세한 내용은 [HTTP/2(Hypertext Transfer Protocol Version 2) 설명서](https://www.rfc-editor.org/rfc/rfc7540#section-8.1.2){target=_blank}를 참조하십시오.

  새 로드 밸런서 인프라를 통해 방문자를 라우팅하는 엔드포인트를 사용하는 경우 해당 연결이 자동으로 HTTP/2로 업그레이드됩니다. 이 업그레이드 프로세스는 요청 헤더를 소문자 헤더로 전환하므로 잘못된 헤더로 간주되지 않습니다.

  이 문제는 라이브러리가 대/소문자를 구분하지 않는(특히 소문자가 아닌) 요청/응답 헤더를 찾도록 설정된 경우 고객에게 문제가 될 수 있습니다.

* [!DNL Recommendations]을(를) 통해 [!UICONTROL Catalog] [!DNL Delivery API]을(를) 업데이트할 때는 주의하십시오. [!DNL Delivery API]은(는) 공개 항목이므로 권장 사항 카탈로그에서 클릭 가능한 항목을 채우는 데 사용하지 마십시오. 이렇게 하면 무효화된 콘텐츠를 소개하고 카탈로그를 오염시킬 수 있습니다.

  **모범 사례**:

  다음 카탈로그 특성을 업데이트하는 경우에만 [!DNL Delivery API]을(를) 사용하십시오.
   * 자주 변경합니다(예: 가격, 재고 수준).
   * 웹 사이트에서 쉽게 확인할 수 있는 사전 정의된 형식을 따르십시오.
   * 클릭 가능한 항목 또는 기타 확인되지 않은 콘텐츠를 추가하거나 수정하는 데 사용하지 마십시오.
   * 필요한 경우 고객 지원 팀에 배달 API를 통해 카탈로그 업데이트를 비활성화하도록 요청할 수 있습니다.

  자세한 내용은 [[!UICONTROL Adobe Target Delivery API]](https://developer.adobe.com/target/implement/delivery-api/){target=_blank} 설명서를 참조하십시오.
