---
keywords: 개인 정보, ip 주소, 지리 특성, 옵트아웃, 옵트아웃, 옵트아웃, 데이터 개인 정보, 정부 규정, 규정, gdpr, ccpa, 개인 정보, 개인 정보, PII
description: 방법 알아보기 [!DNL Adobe Target] 는 IP 주소, PII 및 옵트아웃 명령의 수집 및 처리를 포함하여 해당하는 데이터 개인정보 보호법을 준수합니다.
title: Target은 PII를 포함한 개인 정보 보호 문제를 어떻게 처리합니까?
feature: Privacy & Security
exl-id: 4330e034-2483-4a25-9c87-48dbef6fc9de
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 47%

---

# 개인정보 보호

[!DNL Adobe Target]은 사용자가 해당하는 데이터 개인정보 보호법을 준수하여 [!DNL Target]을 사용할 수 있도록 하는 프로세스 및 설정을 활성화했습니다.

## IP 주소 및 PII(개인 식별 정보) 컬렉션

웹 사이트에 대한 방문자의 IP 주소가 Adobe Data Processing Center(DPC)로 전송됩니다. 방문자에 대한 네트워크 구성에 따라 IP 주소가 반드시 방문자 컴퓨터의 IP 주소를 나타내지는 않습니다. 예를 들어 IP 주소가 NAT(Network Address Translation) 방화벽, HTTP 프록시 또는 인터넷 게이트웨이의 외부 IP 주소일 수 있습니다.

>[!IMPORTANT]
>
>[!DNL Target] 은 사용자의 IP 주소 또는 PII(개인 식별 정보)를 저장하지 않습니다. IP 주소는 [!DNL Target] 세션 중에(인메모리, 지속되지 않음).

## IP 주소의 마지막 옥텟 대체

Adobe은 사용자가 Adobe에 대해 활성화할 수 있는 &quot;계획적 개인 정보 보호&quot; 설정을 개발했습니다 [!DNL Target]. 활성화된 경우 Adobe [!DNL Target] 즉시 IP 주소가 수집된 시점에 IP 주소의 마지막 옥텟(마지막 부분)을 난독화합니다. 이러한 익명화는 선택 사항인 IP 주소의 지역 조회를 포함하여, IP 주소의 모든 처리 이전에 수행됩니다.

이 기능이 활성화되어 있으면 IP 주소가 충분히 익명으로 변경되므로 더 이상 개인 정보로 식별되지 않습니다. 그 결과, [!DNL Target] 개인 정보 수집을 허용하지 않는 국가의 데이터 개인정보 보호법을 준수하여 사용할 수 있습니다. 도시 수준의 정보를 획득하는 것은 IP 주소 난독화의 영향을 크게 받을 수 있습니다. 지역 및 국가 수준의 정보를 획득하는 것은 IP 주소 난독화의 영향을 약간만 받아야 합니다.

다음은에서 설정할 수 있습니다. [!DNL Target] 로 이동하여 UI **[!UICONTROL 관리]** > **[!UICONTROL 구현]**:

* [!UICONTROL 마지막 옥텟 난독화]: [!DNL Target] ip 주소의 마지막 옥텟을 숨깁니다.
* [!UICONTROL 전체 IP 난독화]: [!DNL Target] 전체 IP 주소를 숨깁니다.
* [!UICONTROL 없음]: [!DNL Target] 는 IP 주소의 일부를 숨기지 않습니다.

  ![난독화-ip-options](assets/obfuscate-ip.png)

[!DNL Target] 전체 IP 주소를 수신하고 지정된 대로 이를 난독화합니다([마지막 옥텟] 또는 [전체 IP]로 설정한 경우). [!DNL Target] 그런 다음 난독화된 IP 주소를 현재 세션 동안에만 메모리에 보관합니다.

## 지리 특성

IP 주소의 마지막 옥텟 대체를 활성화하는 경우, IP 주소의 나머지 값은 의 보고서를 사용하여 분석할 수 있습니다 [!DNL Target]. IP 주소의 마지막 옥텟이 난독화되지 않았다면 전체 IP 주소를에서 분석할 수 있습니다. [!DNL Target]. 지리 특성 기능을 사용하여 지리적 영역별로 방문자 위치를 매핑할 수 있습니다. 지리 특성 데이터는 개인 수준이 아니라 도시 수준이나 우편번호 수준으로만 세분화됩니다.

IP 주소가 완전히 난독화된 경우 지리 특성 및 지역 타기팅을 사용할 수 없습니다.

## 옵트아웃 링크

옵트아웃 링크를 사이트에 추가하여 방문자가 모든 계산 및 콘텐츠 제공을 옵트아웃(탈퇴)할 수 있도록 합니다.

1. 사이트에 다음 링크를 추가합니다.

   `<a href="https://clientcode.tt.omtrdc.net/optout"> Your Opt Out Language Here</a>`

1. (조건부) CNAME을 사용 중인 경우 링크에 &quot;client=&quot;가 포함되어야 합니다.`clientcode` 매개 변수(예: )
   `https://my.cname.domain/optout?client=clientcode`를 참조하십시오.

1. `clientcode`를 귀하의 클라이언트 코드로 대체한 다음 옵트아웃 URL에 연결할 텍스트 또는 이미지를 추가하십시오.

이 링크를 클릭하는 모든 방문자는 쿠키를 삭제하기 전까지 또는 2년 동안(어느 쪽이든 먼저 만족되는 조건 적용) 브라우징 세션에서 호출된 어떤 mbox 요청에도 포함되지 않습니다. 이 기능은 `disableClient`라는 방문자의 쿠키를 `clientcode.tt.omtrdc.net` 도메인에서 설정하면 작동합니다.

퍼스트 파티 쿠키 구현을 사용하더라도 제공된 옵트아웃은 서드파티 쿠키를 통해 설정됩니다. 클라이언트가 퍼스트 파티 쿠키만 사용하는 경우 [!DNL Target] 옵트아웃 쿠키가 설정되어 있는지 확인합니다.

## 개인정보 보호 및 데이터 보호 규정

다음을 참조하십시오 [개인 정보 보호 및 데이터 보호 규정](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md) 유럽 연합의 일반 데이터 정보 보호 규정(GDPR), 캘리포니아 소비자 개인정보 보호법(CCPA) 및 기타 국제 개인정보 보호 요구 사항, 그리고 이러한 규정이 귀사 및 조직에 미치는 영향에 대한 정보입니다. [!DNL Target].

## 기능 사용 데이터 수집

개별 기능 사용 데이터는 내부 Adobe 목적으로 수집되어 [!DNL Target] 기능은 의도한 대로 작동하거나 활용도가 낮은 기능을 식별하기 위해 수행됩니다. 성능 관련 문제를 해결하기 위해 다양한 지연 시간 측정값이 수집됩니다. 개인 데이터는 수집되지 않습니다.

클라이언트 초기화 옵션에서 `telemetryEnabled`를 false로 설정하여 SDK의 사용 데이터를 보고하지 않도록 선택할 수 있습니다. 자세한 내용은 [telemetryEnabled in targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#telemetryenabled)를 참조하십시오.
