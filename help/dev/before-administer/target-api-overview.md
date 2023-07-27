---
title: Adobe Target API 개요
description: 배달 api, 보고 api, 관리 api, 프로필 api, 권장 사항 api 및 postman 컬렉션 링크를 포함한 다양한 Adobe Target API의 개요입니다.
exl-id: bf886103-36af-4061-b8be-2fe645f45ff3
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 1%

---

# Target API 개요

이 문서에서는 관리자 및 프로필 API와 관련된 요구 사항에 초점을 맞추기 전에 일반적으로 다양한 Target API에 대해 설명합니다. UI를 통해 Target을 관리하려면 다음을 참조하십시오. [의 관리 섹션 *Adobe Target 비즈니스 사용 안내서*](https://experienceleague.adobe.com/docs/target/using/administer/administrating-target.html?lang=en).

## API 유형

Adobe Target API는 Adobe Recommendations과 같은 Adobe Target 제품을 제공하는 API 컬렉션입니다. 이러한 API를 사용하면 데이터를 조작하고 통합하는 데 사용할 수 있는 데이터가 풍부한 사용자 인터페이스를 만들 수 있습니다.

Adobe Target API는 관리자, 프로필, 게재 및 보고 유형에 따라 그룹화할 수 있습니다.

>[!NOTE]
>
>관리 API 및 프로필 API는 종종 총괄적으로(&quot;관리 및 프로필 API&quot;) 참조되지만, 별도로(&quot;관리 API&quot; 및 &quot;프로필 API&quot;) 참조할 수도 있습니다. Recommendations API는 Target 관리 API의 특정 구현입니다.

| API 유형 | 이를 통해 수행할 수 있는 작업 | 다운로드 링크 | 기타 유용한 링크 |
| --- | --- | --- |--- |
| [관리](../administer/admin-api/admin-api-overview-new.md) | 활동, 대상, 오퍼 및 기타 개체(Recommendations 엔티티, 기준, 디자인 등)를 만들고, 수정하고, 삭제합니다. Recommendations API는 관리 API의 유형입니다.) | <UL><li>[Target 관리 API Postman 컬렉션](https://developers.adobetarget.com/api/#admin-postman-collection)</li><li>[Recommendations API Postman 컬렉션](https://developers.adobetarget.com/api/recommendations/#section/Postman)</li></UL> | [Recommendations API 사용](../before-administer/recs-api/overview.md) |
| 프로필 | Adobe Target에 저장된 사용자 프로필을 검색하고 수정합니다. | [Target 프로필 API Postman 컬렉션](https://developers.adobetarget.com/api/#profiles) |  |
| [배달](../implement/delivery-api/overview.md) | 최종 사용자에게 전달하기 위해 Target에서 최적화되고 개인화된 콘텐츠를 검색합니다. | [Target 배달 API Postman 컬렉션](/help/dev/before-implement/delivery-api-overview/getting-started.md#postman) |  |
| [보고](../administer/admin-api/admin-api-overview-new.md) | 활동 결과 및 기타 보고 결과를 내보냅니다. | 보고 API는 [Target 관리 API Postman 컬렉션](https://developers.adobetarget.com/api/#admin-postman-collection). |  |
| [모델](../administer/models-api/models-api-overview.md) | Target이 해당 머신 러닝 모델(&quot;차단 목록&quot;)에서 제외할 기능 목록을 관리합니다. 모델 API는 관리 API의 한 유형이지만 UI를 통해 액세스할 수 없는 개체(차단 목록)에 대한 고유한 작업 때문에 여기에 별도로 나열됩니다. |  |  |

## API 차이점

Target 관리 API(Recommendations API 포함)와 Target 배달 API 사이에는 중요한 차이점이 있습니다.

* 관리 API를 사용하면 Target UI에서 구성할 수 있는 다양한 Target 측면을 구성할 수 있습니다. 단, UI에서 사용할 수 없는 Target 측면을 구성할 수 있는 모델 API는 예외입니다. 상관없이 **모든 관리 API에는 인증이 필요합니다.**

* 게재 API를 사용하면 콘텐츠를 검색할 수 있습니다. 배달 API에는 인증이 필요하지 않습니다.

Target 관리 API를 사용하려면 다음을 사용하여 인증을 구성해야 합니다 [Adobe Developer 콘솔](https://developer.adobe.com/console/home). 자세한 내용은 [인증 구성 방법](../before-administer/configure-authentication.md).
