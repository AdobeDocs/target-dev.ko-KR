---
keywords: 허용 목록에 추가하다 구현, 구현, 화이트 리스트, 화이트 리스트, 허용 목록, 에지, $9
description: 허용 목록에 추가하다 도움이 되는 호스트 목록 보기 [!DNL Adobe Target] 에지(최종 사용자에게 최적의 응답 시간을 보장하는 지리적으로 분산된 서비스 노드).
title: How Do I 허용 목록 [!DNL Target] 에지 노드
feature: Privacy & Security
exl-id: a7e5d2fc-da8e-414d-a3da-2441ea21503d
source-git-commit: 3f4147d521b1fb3ee12e879e52a48d459f6b24b9
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 6%

---

# 허용 목록 [!DNL Target] 에지 노드

허용 목록에 추가하다에 도움이 되는 정보 및 최신 호스트 목록 [!DNL Adobe Target] 가장자리.

에지(edge)는 콘텐츠를 요청하는 최종 사용자가 어디에 있든지 상관없이 최적의 응답 시간을 보장하는 지리적으로 분산된 서비스 아키텍처입니다. 각 에지 노드에는 사용자의 콘텐츠 요청에 응답하고, 해당 요청에 대한 분석 데이터를 추적하는 데 필요한 모든 정보가 있습니다. 사용자 요청은 가장 가까운 에지 노드로 라우팅됩니다. 자세한 내용은 [에지 네트워크](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#concept_0AE2ED8E9DE64288A8B30FCBF1040934).

허용 목록 [!DNL Target] 원하는 경우 에지 노드

>[!IMPORTANT]
>
>네트워크 주소 변환(NAT) IP 주소 허용 목록에 추가 [!DNL Target] 가장자리 및 [!DNL Target] 기사에 설명된 에지 IP 주소, 당신은 또한 모든 허용 목록에 추가하다를 해야 [!DNL Adobe Analytics] IP 주소 블록.
>
>자세한 내용은 [모든 Adobe Analytics IP 주소 블록](https://experienceleague.adobe.com/docs/analytics/technotes/ip-addresses.html?lang=en#all-adobe-analytics-ip-address-blocks){target=_blank} 다음에서 *Adobe Analytics 기술 노트* 설명서를 참조하십시오.
>
>[!DNL Adobe Target] 인프라가 업데이트되고 있으며 허용 목록에 추가하다 주소를 원하는 고객은 두 세트의 IP를 모두 사용해야 합니다. 그렇게 하지 않으면 경험을 가져오기 위한 Target API 호출이 허용 목록에 추가하다를 사용하도록 구성된 방화벽 뒤의 네트워크 내에서 비롯된 서버측 또는 하이브리드 구현을 사용하는 고객에게 영향을 미칩니다.
>
>모든 Edge4 *x* 아래 두 표에 모두 나열된 주소는 2023년 8월 9일에 업데이트될 예정입니다.

## 네트워크 주소 변환(NAT) IP 주소 [!DNL Target] 가장자리

송신 IP 주소 목록 [!DNL Target] 가장자리. 이 IP를 보유하고 있다면 허용 목록 [!DNL Target] 귀하의 서비스에 연결하십시오.

| 가장자리 위치 | 이그레스 IP 주소 |
| --- | --- |
| Edge31(뭄바이) | 13.126.131.246<br />13.234.229.8 |
| Edge32(도쿄) | 3.115.154.28<br />3.115.227.146 |
| Edge34(미국 동부 해안) | 34.232.149.249<br />52.21.139.93 |
| Edge35(미국 서해안) | 52.10.11.139<br />44.231.171.161 |
| Edge36(시드니) | 13.237.227.20<br />13.210.93.142 |
| Edge37(아일랜드) | 54.72.21.68<br />52.208.139.19 |
| Edge38(싱가포르) | 18.141.132.96<br />54.179.187.167 |
| Edge41(뭄바이) | 3.6.2.221<br />13.235.112.4 <br />52.66.66.192 |
| Edge42(도쿄) | 52.69.55.232<br />43.206.61.43 <br />13.113.73.214 |
| Edge44(미국 동부 해안) | 54.164.192.223<br />52.86.86.203 <br />54.88.167.98 |
| Edge45(미국 서해안) | 52.40.124.129<br />54.148.219.69 <br />54.189.208.212 |
| Edge46(시드니) | 54.253.144.4<br />54.66.198.142 <br />13.211.218.51 |
| Edge47(아일랜드) | 52.208.136.136<br />54.170.28.19 <br />99.80.111.82 |
| Edge48(싱가포르) | 3.1.141.36<br />18.143.112.116 <br />52.76.61.44 |

## [!DNL Target] 에지 IP 주소

의 IP 주소 목록 [!DNL Target] 가장자리. API를 호출하려는 경우 다음 IP 허용 목록 [!DNL Target] 가장자리.

로드 밸런서가 트래픽 프로필에 따라 확장 및 축소되므로 이 목록은 자주 변경됩니다.

| 가장자리 위치 | 도메인 | IP 주소 |
| --- | --- | --- |
|  | `CLIENTCODE.tt.omtrdc.net`<br />(여기서 CLIENTCODE는 [!DNL Target] 클라이언트 ID) |  |
| Edge31(뭄바이) | `mboxedge31.tt.omtrdc.net` | 13.235.211.15<br />35.154.193.2<br />35.154.53.50<br />15.206.4.195<br />13.234.45.112<br />3.7.14.31<br />3.7.182.1<br />52.66.52.225<br />3.6.64.110<br />65.0.222.85<br />65.1.67.35<br />43.205.52.220 |
| Edge32(도쿄) | `mboxedge32.tt.omtrdc.net` | 3.112.121.190<br />54.65.158.134<br />52.199.9.11<br />54.95.35.22<br />52.68.152.188<br />52.196.181.152<br />54.150.112.230<br />52.198.235.210 |
| Edge34(미국 동부 해안) | `mboxedge34.tt.omtrdc.net` | 44.195.255.231<br />52.207.142.243<br />52.54.50.225<br />35.169.35.160<br />52.71.135.138<br />35.169.227.120<br />23.22.33.42<br />52.54.152.40<br />54.243.116.94<br />3.233.250.116<br />50.16.29.53<br />54.86.98.238<br />44.210.41.177<br />3.211.200.163<br />54.210.15.1<br />34.199.251.113 |
| Edge35(미국 서해안) | `mboxedge35.tt.omtrdc.net` | 44.238.17.94<br />52.27.37.224<br />52.89.178.205<br />52.24.182.215<br />44.241.83.238<br />52.24.177.17<br />35.165.241.91<br />52.36.84.148<br />52.40.70.235<br />52.11.244.25<br />35.83.17.210<br />52.42.219.24<br />54.218.0.208<br />34.218.165.70<br />44.239.131.209<br />52.37.121.114<br />35.164.96.150<br />52.40.11.173<br />52.32.91.22<br />35.82.102.174<br />50.112.233.80<br />44.241.57.139<br />44.233.4.154<br />54.69.42.127<br />34.211.73.73<br />54.148.130.206<br />44.238.29.100<br />44.228.116.36<br />52.40.119.218<br />52.25.253.33 |
| Edge36(시드니) | `mboxedge36.tt.omtrdc.net` | 54.206.232.103<br />54.206.183.241<br />3.24.158.129<br />54.253.0.242 |
| Edge37(아일랜드) | `mboxedge37.tt.omtrdc.net` | 54.77.63.43<br />63.35.113.29<br />63.34.224.124<br />54.246.171.67<br />99.80.163.253<br />34.253.167.75<br />52.211.90.101<br />54.246.201.164<br />34.249.148.170<br />54.76.19.168<br />52.209.9.253 |
| Edge38(싱가포르) | `mboxedge38.tt.omtrdc.net` | 52.220.75.199<br />52.221.116.71 |
| Edge41(뭄바이) | `mboxedge41.tt.omtrdc.net` | 15.206.104.6<br />3.109.14.178 <br />13.234.139.131 |
| Edge42(도쿄) | `mboxedge42.tt.omtrdc.net` | 52.194.84.34<br />3.115.158.39 <br />18.180.123.21 |
| Edge44(미국 동부 해안) | `mboxedge44.tt.omtrdc.net` | 54.205.210.54<br />23.20.189.8 <br />35.169.173.155 |
| Edge45(미국 서해안) | `mboxedge45.tt.omtrdc.net` | 35.161.163.45<br />44.230.114.101 <br />35.161.120.22 |
| Edge46(시드니) | `mboxedge46.tt.omtrdc.net` | 3.104.142.61<br />52.62.4.152 <br />54.253.105.140 |
| Edge47(아일랜드) | `mboxedge47.tt.omtrdc.net` | 18.203.168.186<br />54.228.83.91 <br />54.217.181.83 |
| Edge48(싱가포르) | `mboxedge48.tt.omtrdc.net` | 54.179.6.70<br />13.215.150.94 <br />18.136.47.70 |

로드 밸런서가 트래픽 프로필의 변경을 감지하면 로드 밸런서가 증가하거나 감소합니다. Elastic Load Balancing이 확장되는 데 필요한 시간은 감지된 변경 사항에 따라 1분에서 7분 사이일 수 있습니다. 로드 밸런서가 확장되면 새 IP 주소 목록으로 DNS 레코드를 업데이트합니다. Elastic Load Balancing은 증가된 용량을 활용하기 위해 DNS 기록인 60초에서 TTL 설정을 사용합니다.
