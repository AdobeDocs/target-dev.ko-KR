---
keywords: 허용 목록에 추가하다 구현, 구현, 화이트 리스트, 화이트 리스트, 허용 목록, 에지, $9
description: 호스트 목록을 확인하여 허용 목록에 추가하다 [!DNL Adobe Target] 에지(최종 사용자에게 최적의 응답 시간을 보장하는 지리적으로 분산된 노드)를 제공합니다.
title: 허용 목록에 추가하다 [!DNL Target] Edge 노드는 어떻게 합니까?
feature: Privacy & Security
exl-id: a7e5d2fc-da8e-414d-a3da-2441ea21503d
source-git-commit: 275c3fabdcaf3152d7d6161f3c325e54c840c805
workflow-type: tm+mt
source-wordcount: '563'
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
>
>아래 두 표에 모두 나열된 모든 Edge4 *x* 주소는 2023년 8월 9일에 업데이트될 예정입니다.

## [!DNL Target] 가장자리의 NAT(Network Address Translation) IP 주소

[!DNL Target] 에지의 이그레스 IP 주소 목록입니다. 허용 목록에 추가하다 [!DNL Target]에서 서비스에 연결할 수 있는 경우 해당 IP를 다운로드하십시오.

| Edge 위치 | 이그레스 IP 주소 |
| --- | --- |
| Edge41 (뭄바이) | 3.6.2.221<P>13.235.112.4 <P>52.66.66.192 |
| Edge42 (도쿄) | 52.69.55.232<P>43.206.61.43 <P>13.113.73.214 |
| Edge44 (미국 동부 해안) | 54.164.192.223<P>52.86.86.203 <P>54.88.167.98 |
| Edge45 (미국 서부 해안) | 52.40.124.129<P>54.148.219.69 <P>54.189.208.212 |
| Edge46(시드니) | 54.253.144.4<P>54.66.198.142 <P>13.211.218.51 |
| Edge47 (아일랜드) | 52.208.136.136<P>54.170.28.19 <P>99.80.111.82 |
| Edge48 (싱가포르) | 3.1.141.36<P>18.143.112.116 <P>52.76.61.44 |

## [!DNL Target] 에지 IP 주소

[!DNL Target] 가장자리의 IP 주소 목록입니다. 허용 목록에 추가하다 API를 [!DNL Target] 에지로 호출하려는 경우 해당 IP를 다운로드합니다.

로드 밸런서가 트래픽 프로필에 따라 확장 및 축소되므로 이 목록은 자주 변경됩니다.

| Edge 위치 | 도메인 | IP 주소 |
| --- | --- | --- |
|  | `CLIENTCODE.tt.omtrdc.net`<br />(여기서 CLIENTCODE는 [!DNL Target] 클라이언트 ID임) |  |
| Edge41 (뭄바이) | `mboxedge41.tt.omtrdc.net` | 3.6.2.221<P>52.66.66.192<P>13.235.112.4 |
| Edge42 (도쿄) | `mboxedge42.tt.omtrdc.net` | 43.206.61.43<P>13.113.73.214<P>52.69.55.232 |
| Edge44 (미국 동부 해안) | `mboxedge44.tt.omtrdc.net` | 54.88.167.98<P>54.164.192.223<P>52.86.86.203 |
| Edge45 (미국 서부 해안) | `mboxedge45.tt.omtrdc.net` | 52.40.124.129<P>54.148.219.69<P>54.189.208.212 |
| Edge46(시드니) | `mboxedge46.tt.omtrdc.net` | 54.66.198.142<P>54.253.144.4<P>13.211.218.51 |
| Edge47 (아일랜드) | `mboxedge47.tt.omtrdc.net` | 54.170.28.19<P>52.208.136.136<P>99.80.111.82 |
| Edge48 (싱가포르) | `mboxedge48.tt.omtrdc.net` | 52.76.61.44<P>3.1.141.36<P>18.143.112.116 |

로드 밸런서가 트래픽 프로필의 변경을 감지하면 로드 밸런서가 증가하거나 감소합니다. Elastic Load Balancing이 확장되는 데 필요한 시간은 감지된 변경 사항에 따라 1분에서 7분 사이일 수 있습니다. 로드 밸런서가 확장되면 새 IP 주소 목록으로 DNS 레코드를 업데이트합니다. Elastic Load Balancing은 증가된 용량을 활용하기 위해 DNS 기록인 60초에서 TTL 설정을 사용합니다.

## [!DNL Target] 프록시 서비스에 대한 허용 목록에 추가 요구 사항

EEC([!DNL Target])를 통해 [!DNL Experience Edge Connector]에 중단 없이 액세스하려면 고객이 프록시 서비스에 대한 트래픽을 허용하도록 네트워크 구성을 업데이트해야 할 수 있습니다.

### 프록시 서비스 개요

* **서비스 끝점**: `https://tnt-web-proxy.adobe.io`.
* **인프라**: [!DNL Adobe] Ethos 플랫폼에서 호스팅됩니다.
* **참고**: 이 서비스는 지연 기반 DNS 라우팅을 사용하며 고정 IP 주소를 사용하지 않습니다.

### CNAME 대상

프록시 서비스는 CNAME 레코드를 사용하여 여러 지역에서 트래픽을 동적으로 라우팅합니다. 다음은 현재 대상입니다.

| Edge 위치 | 이그레스 IP 주소 |
| --- | --- |
| 지역 | CNAME 대상 |
| 유럽(eu-west-1) | `ethos.pub.ethos11-prod-nld2.ethos.adobe.net` |
| 미국 동부(us-east-2) | `ethos.pub.ethos11-prod-va7.ethos.adobe.net` |
| 미국 동부(us-east-1) | `ethos.pub.ethos11-prod-aus5.ethos.adobe.net` |

### 권장 허용 목록 항목

허용 목록에 추가하다 신뢰할 수 있는 연결을 보장하려면 다음 호스트 이름을 입력하십시오.

* `ethos.pub.ethos11-prod-nld2.ethos.adobe.net`
* `ethos.pub.ethos11-prod-va7.ethos.adobe.net`
* `ethos.pub.ethos11-prod-aus5.ethos.adobe.net`

### 선택 사항: IP 검색

네트워크 정책에 IP 기반 허용 목록에 추가가 필요한 경우 이 도구를 사용하여 프록시 서비스와 연관된 현재 공용 IP 주소를 볼 수 있습니다.

* `DNSChecker – A Record Lookup for tnt-web-proxy.adobe.io`