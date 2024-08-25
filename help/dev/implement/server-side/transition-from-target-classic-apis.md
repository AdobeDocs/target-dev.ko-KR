---
keywords: api, adobe i/o, classic, adobe 개발자 콘솔
description: ' [!DNL Adobe Developer Console]의  [!DNL Adobe Target Classic] API에서  [!DNL Target] API로 전환하는 방법에 대해 알아봅니다.'
title: ' [!DNL Adobe Developer Console]에서  [!DNL Target Classic] API에서  [!DNL Target] API로 전환하는 방법은 무엇입니까?'
feature: APIs/SDKs
exl-id: b84e3767-89ad-4e2d-9bb4-7e31bffbc285
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 38%

---

# [!DNL Adobe Developer Console]에서 [!DNL Target Classic] API에서 [!DNL Target] API로 전환

[!DNL Target Classic] API에서 [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home)의 [!DNL Target] API로 전환하는 데 도움이 되는 정보입니다.

[!DNL Adobe Target Classic]의 서비스 해제로 [!DNL Target Classic] 계정에 연결된 API도 사용할 수 없게 되었습니다. 이 문서는 [!DNL Target Classic] API 기반 통합을 [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home)에서 제공하는 [!DNL Target] API로 전환하는 데 도움이 됩니다.

[!DNL Target] API에 대한 자세한 내용은 [[!DNL Target] API](/help/dev/before-administer/target-api-overview.md)를 참조하십시오. [!DNL Target]개의 SDK에 대한 자세한 내용은 [[!DNL Target] 서버측 구현](/help/dev/implement/server-side/server-side-overview.md)을 참조하십시오.

## Terminology

| 용어 | 설명 |
|--- |--- |
| 클래식 API | [!DNL Target Classic] 계정에 연결된 API. 이 API 호출은 사용자 이름 및 암호 기반 인증을 기반으로 하며 호스트 이름 `testandtarget.omniture.com`을 사용합니다. API 호출에 요청 URL에 사용자 이름과 암호가 포함된 경우 [!DNL Adobe Developer Console] API로 전환해야 합니다. |
| [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home) | [!DNL Adobe Developer Console]은(는) [!DNL Target] API의 게이트웨이입니다. 이 API는 [!DNL Target Standard/Premium] 계정에 연결되어 있습니다. [!DNL Adobe Developer Console]의 [!DNL Target] API는 보안 엔터프라이즈 API의 업계 표준인 [JWT 기반 인증](../../before-administer/configure-authentication.md)을(를) 사용합니다. |

## 타임라인

[!DNL Target Classic]이(가) 서비스 해제될 때 다음 API가 서비스 해제되었습니다.

| 날짜 | 세부 사항 |
|--- |--- |
| 2017년 10월 17일 | 쓰기 작업을 수행하는 모든 API 메서드(`saveCampaign`, `copyCampaign`, `saveHTMLOfferContent` 및 `setCampaignState`)가 폐기되었습니다.<P>모든 [!DNL Target Classic] 사용자 계정이 읽기 전용 상태로 설정된 날짜와 동일한 날짜입니다. |
| 2017년 11월 14일 | 나머지 API는 삭제되었습니다. [!DNL Target Classic] 사용자 인터페이스가 폐기된 날짜입니다. |

[!DNL Recommendations Classic]개의 API가 이 타임라인의 영향을 받지 않았습니다.

## 동등한 메서드

다음 표에는 클래식 API 메서드에 해당하는 [!DNL Adobe Developer Console] API 메서드가 나와 있습니다. [!DNL Adobe Developer Console] API는 JSON을 반환하지만 클래식 API는 XML을 반환합니다.

[!DNL Adobe Developer Console] API 메서드는 API 설명서 사이트의 해당 섹션에 연결되어 있습니다. 여기에는 각 API 메서드에 대한 예가 제공됩니다. [!DNL Adobe Developer Console]의 모든 Adobe API 메서드에 대한 샘플 API 호출이 포함된 [!DNL Target] 관리 API Postman 컬렉션을 사용할 수도 있습니다.

| 그룹 | 클래식 API 메서드 | [!DNL Adobe Developer Console] API 메서드 | 참고 |
|--- |--- |--- |--- |
| 캠페인/활동 | 캠페인 만들기 | [AB 활동 만들기](https://developers.adobetarget.com/api/#create-ab-activity)<P>[XT 활동 만들기](https://developers.adobetarget.com/api/#create-xt-activity) | 새 API에서는 AB 및 XT용으로 별도의 만들기 메서드를 제공합니다. |
|  | 캠페인 업데이트 | [AB 활동 업데이트](https://developers.adobetarget.com/api/#update-ab-activity)<P>[XT 활동 업데이트](https://developers.adobetarget.com/api/#update-xt-activity) |  |
|  | 캠페인 복사 | 해당 없음 | 활동 만들기 API를 사용하십시오. |
|  | 캠페인 목록 | [활동 나열](https://developers.adobetarget.com/api/#list-activities) |  |
|  | 캠페인 상태 | [활동 상태 업데이트](https://developers.adobetarget.com/api/#update-activity-state) |  |
|  | 캠페인 보기 | [ID별 AB 활동 가져오기](https://developers.adobetarget.com/api/#get-ab-activity-by-id)<P>[ID별 XT 활동 가져오기](https://developers.adobetarget.com/api/#get-xt-activity-by-id) |  |
|  | 타사 캠페인 ID | 해당 없음 | thirdpartyID를 사용하는 경우 관련 활동 메서드를 사용할 수 있습니다. |
| 오퍼 | 오퍼 만들기 | [오퍼 만들기](https://developers.adobetarget.com/api/#create-offer) |  |
|  | 오퍼 가져오기 | [ID별 오퍼 가져오기](https://developers.adobetarget.com/api/#get-offer-by-id) |  |
|  | 오퍼 목록 | [오퍼 나열](https://developers.adobetarget.com/api/#list-offers) |  |
|  | 폴더 목록 | 해당 없음 | 폴더가 [!DNL Target Standard/Premium]에서 지원되지 않습니다. |
| 보고 | 캠페인 성과 보고서 | [AB 성과 보고서 가져오기](https://developers.adobetarget.com/api/#get-ab-performance-report)<P>[XT 성과 보고서 가져오기](https://developers.adobetarget.com/api/#get-xt-performance-report) |  |
|  | 감사 보고서 | [감사 보고서 가져오기](https://developers.adobetarget.com/api/#get-audit-report) |  |
|  | 1-1 컨텐츠 보고서 | [AP 성과 보고서 가져오기](https://developers.adobetarget.com/api/#get-ap-activity-performance-report) |  |
| 계정 설정 | 호스트 그룹 가져오기 | [환경 나열](https://developers.adobetarget.com/api/#list-environments) |  |

## 예외

예외가 필요한 경우 Customer Success Manager에게 문의하십시오.

## 도움말

질문이 있거나 Classic API에서 [!DNL Adobe Developer Console]의 [!DNL Target] API로 전환하는 데 도움이 필요한 경우 [!DNL Adobe Target Client Care](tt-support@adobe.com)에 문의하십시오.
