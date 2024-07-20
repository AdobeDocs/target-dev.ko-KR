---
keywords: 이메일, adbox, 이메일 이미지 adbox
description: ' [!DNL Adobe Target] 을(를) 사용하여 이메일에서 이미지를 동적으로 테스트하고, 누군가 이메일을 열면 해당 이미지를 즉시 변경하는 방법에 대해 알아봅니다.'
title: 이메일 이미지 Adbox를 테스트하려면 어떻게 합니까?
feature: Implement Email
exl-id: 4512741a-567f-41bb-9721-3e1c4f5302e1
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 79%

---

# 이메일 이미지 Adbox 테스트

이메일에서 이미지를 동적으로 테스트하고, 누군가 이메일을 열면 해당 이미지를 즉시 변경합니다.

클릭 수를 추적하고 사람들이 도달하는 랜딩 페이지를 동적으로 제어하기 위해 리디렉터를 이메일에서 사용할 수 있습니다.

이메일 이미지 테스트는 수정된 adbox 버전을 사용하여 수행할 수 있습니다. 이메일 클라이언트는 쿠키 설정을 허용하지 않으므로 각 이메일에 대해 고유한 식별자를 생성해야 합니다. 이 숫자는 adbox URL 및 이메일에 사용되는 모든 리디렉터에 추가되어, 이메일로부터의 클릭 수를 추적합니다.

>[!NOTE]
>
>[!DNL Target]에서 공개 시간에 이미지 최적화를 기술적으로 제공할 수 있지만 각 이메일 클라이언트는 캐싱을 다르게 처리하므로 성공할 경우 다양하게 변경됩니다. 사용된 이메일 서비스 공급자에 관계없이 최종 사용자가 이메일을 여는 데 사용하는 이메일 클라이언트(Gmail 앱, Outlook, Hotmail 등)는 이미지를 연 시간에 실제로 가져올지 여부를 결정합니다. 예를 들어, Gmail은 거의 모든 것을 캐시에 저장하므로 최종 사용자에게 표시되는 이미지는 Gmail이 이미지를 호출하고 캐시에 저장한 시간에 따라 달라집니다.

**이메일 이미지 adbox에 대한 샘플 코드:**

```
<img src="https://{clientcode}.tt.omtrdc.net/m2/​{clientcode}/ubox/​image?
mbox={email_header}&
mboxDefault=​{http%3A%2F%2Fwww.domain.com%2Fheader.jpg}&
mboxXDomain=disabled&
mboxSession={123456}&
mboxPC={123456}" border=:"0"/>
```

여기서 아래 값은 적절히 수정해야 합니다.

| 값 | 설명 |
|--- |--- |
| clientcode | 회사의 클라이언트 코드입니다. `clientCode='yourclientcode'`(으)로 나열된 at.js에서 찾으십시오. 모두 소문자이고 특수 문자를 포함하지 않습니다. |
| 이미지 | 오퍼 유형입니다. 그래픽 광고의 경우 항상 &quot;image&quot;이며 리디렉터의 경우에는 &quot;page&quot;입니다. |
| email_header | adbox의 이름입니다. |
| `mboxDefault=http%3A%2F%2Fwww.domain.com%2Fheader.jpg` | 필수. URL을 adbox의 적절한 기본 콘텐츠로 바꿉니다. 이것은 절대 참조이며 URL로 인코딩되어야 합니다. |
| `mboxXDomain=disabled` | [!DNL Target]에게 쿠키를 설정하지 않도록 지시합니다. |
| `mboxSession=123456` 및 `mboxPC=123456` | [!DNL Target]이(가) 이 사용자의 프로필을 사이트의 기존 프로필과 병합하는 데 필요한 두 개의 값입니다. 123456은 이메일에 대해 생성된 고유한 식별자입니다. 이 값을 모든 adbox와 리디렉터 URL에 동적으로 삽입하십시오. 이 숫자는 각 사용자에게 전송된 각 이메일에 대해 고유해야 합니다. 주별 이메일을 1,000명에게 전송하면 1,000개의 고유한 ID가 생성되어야 합니다.<br />이메일에 대한 고유한 식별자는 각 adbox와 리디렉터 URL에서 mboxSession 및 mboxPC에 할당해야 합니다. 이 식별자의 권장 형식은 timestamp-NNNNN이고 여기서 NNNNN은 임의의 5자리 숫자지만 모든 영숫자 형식을 사용할 수 있습니다. 일부 대량 이메일 서비스와 모든 프로그래밍 언어는 이 고유 식별자를 생성할 수 있습니다. |
