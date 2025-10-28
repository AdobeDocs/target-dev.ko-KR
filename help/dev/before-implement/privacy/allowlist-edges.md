---
keywords: 허용 목록에 추가하다 구현, 구현, 화이트 리스트, 화이트 리스트, 허용 목록, 에지, $9
description: 호스트 목록을 확인하여 허용 목록에 추가하다 [!DNL Adobe Target] 에지(최종 사용자에게 최적의 응답 시간을 보장하는 지리적으로 분산된 노드)를 제공합니다.
title: 허용 목록에 추가하다 [!DNL Target] Edge 노드는 어떻게 합니까?
feature: Privacy & Security
exl-id: a7e5d2fc-da8e-414d-a3da-2441ea21503d
source-git-commit: 662d415bc3c216bcd038f07dcaa0fd83f6518690
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# [!DNL Target] 에지 노드 허용 목록

허용 목록에 추가하다 [!DNL Adobe Target] 가장자리를 연결하는 데 도움이 되는 정보와 최신 호스트 목록입니다.

에지(edge)는 콘텐츠를 요청하는 최종 사용자가 어디에 있든지 상관없이 최적의 응답 시간을 보장하는 지리적으로 분산된 서비스 아키텍처입니다. 각 에지 노드에는 사용자의 콘텐츠 요청에 응답하고, 해당 요청에 대한 분석 데이터를 추적하는 데 필요한 모든 정보가 있습니다. 사용자 요청은 가장 가까운 에지 노드로 라우팅됩니다. 자세한 내용은 [에지 네트워크](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html?lang=ko#concept_0AE2ED8E9DE64288A8B30FCBF1040934)를 참조하십시오.

원하는 경우 [!DNL Target] 에지 노드를 허용 목록 할 수 있습니다.

>[!IMPORTANT]
>
>문서에 설명된 [!DNL Target] 에지 및 [!DNL Target] 에지 IP 주소의 NAT(Network Address Translation) IP 주소 허용 목록에 추가 외에 모든 [!DNL Adobe Analytics] IP 주소 블록에도 허용 목록에 추가하다해야 합니다.
>
>자세한 내용은 [Adobe Analytics 기술 노트](https://experienceleague.adobe.com/docs/analytics/technotes/ip-addresses.html?lang=ko#all-adobe-analytics-ip-address-blocks){target=_blank} 설명서에서 *모든 Adobe Analytics IP 주소 블록*&#x200B;을(를) 참조하십시오.
>
>[!DNL Adobe Target] 인프라가 업데이트되고 허용 목록에 추가하다 주소를 업데이트하려는 고객은 두 IP 집합을 모두 사용해야 합니다. 이렇게 하지 않으면 경험을 가져오기 위한 Target API 호출이 허용 목록에 추가하다를 사용하도록 구성된 방화벽 뒤의 네트워크 내에서 비롯된 서버측 또는 하이브리드 구현을 사용하는 고객에게 영향을 줍니다.

[!DNL Target]을(를) 통해 [!DNL Experience Edge Connector]에 중단 없이 액세스하려면 고객은 프록시 서비스에 대한 트래픽을 허용하도록 네트워크 구성을 업데이트할 수 있습니다.

## 프록시 서비스 개요

* **서비스 끝점**: `https://tnt-web-proxy.adobe.io`.
* **인프라**: [!DNL Adobe] Ethos 플랫폼에서 호스팅됩니다.
* **참고**: 이 서비스는 지연 기반 DNS 라우팅을 사용하며 고정 IP 주소를 사용하지 않습니다.

## CNAME 대상

프록시 서비스는 CNAME 레코드를 사용하여 여러 지역에서 트래픽을 동적으로 라우팅합니다. 다음은 현재 대상입니다.

| Edge 위치 | 이그레스 IP 주소 |
| --- | --- |
| 지역 | CNAME 대상 |
| 유럽(eu-west-1) | `ethos.pub.ethos11-prod-nld2.ethos.adobe.net` |
| 미국 동부(us-east-2) | `ethos.pub.ethos11-prod-va7.ethos.adobe.net` |
| 미국 동부(us-east-1) | `ethos.pub.ethos11-prod-aus5.ethos.adobe.net` |

## 권장 허용 목록 항목

허용 목록에 추가하다 신뢰할 수 있는 연결을 보장하려면 다음 호스트 이름을 입력하십시오.

* `ethos.pub.ethos11-prod-nld2.ethos.adobe.net`
* `ethos.pub.ethos11-prod-va7.ethos.adobe.net`
* `ethos.pub.ethos11-prod-aus5.ethos.adobe.net`

## 선택 사항: IP 검색

네트워크 정책에 IP 기반 허용 목록에 추가가 필요한 경우 이 도구를 사용하여 프록시 서비스와 연관된 현재 공용 IP 주소를 볼 수 있습니다.

* `DNSChecker – A Record Lookup for tnt-web-proxy.adobe.io`