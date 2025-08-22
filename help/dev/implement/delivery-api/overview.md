---
title: Adobe Target 게재 API 개요
description: Adobe Target 게재 API 개요
keywords: 배달 api
exl-id: e760bddc-b1ae-4b7b-bff2-aba81c6b6d34
feature: APIs/SDKs
source-git-commit: ccc27e66207e58dcd33865e5d28a51644e8e1931
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# 게재 API 개요

[!DNL Adobe Target Delivery API]은(는) REST를 기반으로 합니다. 이 설명서에서는 [!DNL Adobe Target] [!DNL Delivery API]을(를) 구성하는 리소스에 대해 설명합니다. HTTP 메서드는 이러한 리소스에서 작업을 실행하는 데 사용됩니다.

[!UICONTROL Adobe Target's Delivery API]을(를) 사용하여 다음을 수행할 수 있습니다.

* 연결된 TV, 키오스크 또는 매장 내 디지털 화면과 같은 비브라우저 기반 IoT 장치뿐만 아니라 SPA 및 모바일 채널을 포함하여 웹에서 경험을 제공합니다.
* HTTP/s를 호출할 수 있는 모든 서버측 플랫폼 또는 애플리케이션에서 경험을 제공합니다.
* 사용자가 귀하의 비즈니스에 관여한 채널 또는 장치에 관계없이 일관되고 개인화된 경험을 사용자에게 제공합니다.
* 서버의 세션 내에서 사용자에 대한 경험을 캐시하므로 여러 API 호출을 방지하고 결과적으로 더 나은 성능을 얻을 수 있습니다.
* 서버측에서 [!DNL Adobe Experience Cloud], [!DNL Adobe Analytics] 및 [!DNL Adobe Audience Manager]과(와) 같은 [!DNL Experience Cloud ID Service] 제품과 원활하게 통합됩니다.

>[!IMPORTANT]
>
>[!DNL Recommendations]을(를) 통해 [!UICONTROL Catalog] [!DNL Delivery API]을(를) 업데이트할 때는 주의하십시오. [!DNL Delivery API]은(는) 공개 항목이므로 권장 사항 카탈로그에서 클릭 가능한 항목을 채우는 데 사용하지 마십시오. 이렇게 하면 무효화된 콘텐츠를 소개하고 카탈로그를 오염시킬 수 있습니다.
>
>모범 사례:
>
>다음 카탈로그 특성을 업데이트하는 경우에만 [!DNL Delivery API]을(를) 사용하십시오.
>* 자주 변경합니다(예: 가격, 재고 수준).
>* 웹 사이트에서 쉽게 확인할 수 있는 사전 정의된 형식을 따르십시오.
>* 클릭 가능한 항목 또는 기타 확인되지 않은 콘텐츠를 추가하거나 수정하는 데 사용하지 마십시오.
>
>필요한 경우 고객 지원 팀에 배달 API를 통해 카탈로그 업데이트를 비활성화하도록 요청할 수 있습니다.

자세한 내용은 [[!UICONTROL Adobe Target Delivery API]](https://developer.adobe.com/target/implement/delivery-api/){target=_blank} 설명서를 참조하십시오.

>[!NOTE]
>
>[레거시 /v1/mbox 및 /v2/batchmbox API 설명서](https://developers.adobetarget.com/api/legacy-api/index.html)에 액세스할 수 있습니다. 그러나 게재 API에서는 기능이 개발되어 기존 API로 백포팅되지 않습니다(여기에 설명됨).
