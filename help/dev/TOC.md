---
user-guide-title: Adobe Target 개발자 안내서
breadcrumb-title: Target 개발자 안내서
user-guide-description: 고객의 경험을 맞춤화 및 개인화하여 웹 및 모바일 사이트, 앱, 소셜 미디어 및 기타 디지털 채널에서 매출을 극대화하는 방법을 알아봅니다.
source-git-commit: 734bda64915a08f2edba37cbbb66b2de581c2237
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 55%

---


# Adobe Target 개발자 안내서 {#developer}

+ [Adobe Target 개발자 안내서](overview.md)
+ 시작하기 {#implementation}
   + 구현하기 전에 {#before-implement}
      + [구현하기 전에](before-implement/considerations-before-you-implement-target.md)
      + [Target 구현 준비](before-implement/prepare-to-implement-target.md)
   + 개인정보보호 및 보안 {#privacy}
      + [개인정보 보호 개요](before-implement/privacy/privacy.md)
      + [개인정보 보호 및 데이터 보호 규정](before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md)
      + [Target 쿠키](before-implement/privacy/cookie-behavior.md)
      + [Target 쿠키 삭제](before-implement/privacy/cookie-deleting.md)
      + [Google Chrome samesite 쿠키 정책](before-implement/privacy/google-chrome-samesite-cookie-policies.md)
      + [Apple ITP(Intelligent Tracking Prevention) 2.x](before-implement/privacy/apple-itp-2x.md)
      + [콘텐츠 보안 정책(CSP) 지침](before-implement/privacy/content-security-policy.md)
      + [Target 에지 노드를 허용 목록에 추가](before-implement/privacy/allowlist-edges.md)
   + 데이터를 Target에 가져오는 방법 {#methods}
      + [메서드 개요](before-implement/methods-to-get-data-into-target/methods-to-get-data-into-target.md)
      + [페이지 매개 변수](before-implement/methods-to-get-data-into-target/page-parameters.md)
      + [페이지 내 프로필 속성](before-implement/methods-to-get-data-into-target/in-page-profile-attributes.md)
      + [스크립트 프로필 속성](before-implement/methods-to-get-data-into-target/script-profile-attributes.md)
      + [데이터 공급자](before-implement/methods-to-get-data-into-target/data-providers.md)
      + [벌크 프로필 업데이트 API](before-implement/methods-to-get-data-into-target/bulk-profile-update-api.md)
      + [단일 프로필 업데이트 API](before-implement/methods-to-get-data-into-target/single-profile-update-api.md)
      + [고객 속성](before-implement/methods-to-get-data-into-target/customer-attributes.md)
      + [프로필 API 설정](before-implement/methods-to-get-data-into-target/profile-api-settings.md)
   + [Target 보안 개요](before-implement/target-security-overview.md)
   + [지원되는 브라우저](before-implement/supported-browsers.md)
   + [TLS(전송 계층 보안) 암호화 변경 사항](before-implement/tls-transport-layer-security-encryption.md)
   + [CNAME 및 Adobe Target](before-implement/implement-cname-support-in-target.md)
+ 클라이언트측 구현 {#client-side}
   + [개요: 클라이언트측 웹용 Target 구현](implement/client-side/overview.md)
   + [Adobe Experience Platform Web SDK 구현 개요](implement/client-side/aep-web-sdk.md)
   + at.js 구현 {#at-js-implementation}
      + [at.js 개요](implement/client-side/atjs/how-atjs-works/overview.md)
      + at.js 작동 방식 {#at-js}
         + [at.js 작동 방식 개요](implement/client-side/atjs/how-atjs-works/how-atjs-works.md)
         + [at.js에서 플리커를 관리하는 방법](implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md)
         + [at.js 통합](implement/client-side/atjs/how-atjs-works/target-atjs-integrations.md)
      + at.js를 배포하는 방법 {#deploy-at-js}
         + [at.js를 배포하는 방법](implement/client-side/atjs/how-to-deployatjs/how-to-deployatjs.md)
         + [Adobe Experience Platform을 사용하여 Target 구현](implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md)
         + [태그 관리자 없이 Target 구현](implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)
         + [Dynamic Tag Manager(DTM)를 사용하는 Target 구현](implement/client-side/atjs/how-to-deployatjs/implement-target-using-dtm.md)
         + [단일 페이지 애플리케이션(SPA)에 대한 Target 구현](implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md)
      + 온디바이스 의사 결정 {#on-device-decisioning}
         + [온디바이스 의사 결정 개요](implement/client-side/atjs/on-device-decisioning/on-device-decisioning.md)
         + [지원되는 기능](implement/client-side/atjs/on-device-decisioning/supported-features.md)
         + [규칙 아티팩트](implement/client-side/atjs/on-device-decisioning/rule-artifact.md)
         + [문제 해결](implement/client-side/atjs/on-device-decisioning/troubleshooting-on-device-decisioning.md)
      + at.js 함수 {#functions-overview}
         + [at.js 함수 개요](implement/client-side/atjs/atjs-functions/atjs-functions.md)
         + [adobe.target.getOffer()](implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md)
         + [adobe.target.getOffers() - at.js 2.x](implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
         + [adobe.target.applyOffer()](implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md)
         + [adobe.target.applyOffers() - at.js 2.x](implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)
         + [adobe.target.triggerView() - at.js 2.x](implement/client-side/atjs/atjs-functions/adobe-target-triggerview-atjs-2.md)
         + [adobe.target.trackEvent()](implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)
         + [mboxCreate() - at.js 1.x](implement/client-side/atjs/atjs-functions/mboxcreate-atjs.md)
         + [targetGlobalSettings()](implement/client-side/atjs/atjs-functions/targetglobalsettings.md)
         + [mboxDefine() 및 mboxUpdate() - at.js 1.x](implement/client-side/atjs/atjs-functions/mboxdefine-mboxupdate-atjs-1x.md)
         + [targetPageParams()](implement/client-side/atjs/atjs-functions/targetpageparams.md)
         + [targetPageParamsAll()](implement/client-side/atjs/atjs-functions/targetpageparamsall.md)
         + [registerExtension() - at.js 1.x](implement/client-side/atjs/atjs-functions/registerextension-atjs-1x.md)
         + [sendNotifications() - at.js 2.1](implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21.md)
         + [at.js 사용자 지정 이벤트](implement/client-side/atjs/atjs-functions/atjs-custom-events.md)
         + [Adobe Experience Cloud Debugger를 사용하여 at.js 디버그](implement/client-side/target-debugging-atjs/target-debugging-atjs.md)
         + [Target에서 클라우드 기반 인스턴스 사용](implement/client-side/target-debugging-atjs/targeting-using-cloud-based-instances.md)
      + [at.js FAQ](implement/client-side/atjs/target-atjs-faq.md)
      + [at.js 버전 세부 사항](implement/client-side/atjs/target-atjs-versions.md)
      + [at.js 1.x에서 at.js 2.x로 업그레이드](implement/client-side/atjs/upgrading-from-atjs-1x-to-atjs-20.md)
      + [at.js 쿠키](implement/client-side/atjs/atjs-cookies.md)
   + [사용자 에이전트 및 클라이언트 힌트](implement/client-side/atjs/user-agent-and-client-hints.md)
   + 글로벌 mbox 이해 {#global-mbox}
      + [글로벌 mbox 이해 개요](implement/client-side/atjs/global-mbox/global-mbox-overview.md)
      + [글로벌 mbox 사용자 지정](implement/client-side/atjs/global-mbox/customize-global-mbox.md)
      + [이전 구현에서 글로벌 mbox를 사용](implement/client-side/atjs/global-mbox/mbox-global-target-standard.md)
      + [글로벌 mbox에 매개 변수 전달](implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md)
      + [글로벌 mbox 자주 묻는 질문](implement/client-side/atjs/global-mbox/global-mbox-faq.md)
+ 서버 측 구현 {#server-side}
   + [서버측: Target 구현 개요](implement/server-side/server-side-overview.md)
   + [Target SDK 시작하기](implement/server-side/sdk-guides/getting-started/getting-started.md)
   + [샘플 앱](implement/server-side/sdk-guides/sample-apps/sample-apps.md)
   + [Target의 이전 API에서 Adobe I/O로 전환](implement/server-side/transition-from-target-classic-apis.md)
   + 핵심 원칙 {#core-principles}
      + [핵심 원칙 개요](implement/server-side/sdk-guides/core-principles/overview.md)
      + [사용자 ID 및 버킷팅](implement/server-side/sdk-guides/core-principles/user-identification-and-bucketing.md)
      + [대상 타기팅](implement/server-side/sdk-guides/core-principles/audience-targeting.md)
      + [이벤트 추적](implement/server-side/sdk-guides/core-principles/event-tracking.md)
      + [사용자 권한 및 속성](implement/server-side/sdk-guides/core-principles/user-permissions-and-properties.md)
   + 통합 {#integration}
      + [통합 개요](implement/server-side/sdk-guides/integration-with-experience-cloud/overview.md)
      + [Experience Cloud ID 서비스(ECID)](implement/server-side/sdk-guides/integration-with-experience-cloud/ecid.md)
      + [A4T (Analytics for Target) 보고](implement/server-side/sdk-guides/integration-with-experience-cloud/a4t-reporting.md)
      + [AAM 세그먼트](implement/server-side/sdk-guides/integration-with-experience-cloud/aam-segments.md)
   + 온디바이스 의사 결정 {#on-device-decisioning}
      + [온디바이스 의사 결정 개요](implement/server-side/sdk-guides/on-device-decisioning/overview.md)
      + 규칙 아티팩트 {#rule-artifact}
         + [규칙 아티팩트 개요](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md)
         + [Adobe Target SDK를 통해 다운로드](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-sdk.md)
         + [JSON 페이로드를 통해 다운로드](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-json.md)
         + [규칙 아티팩트 예](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-example.md)
      + [기능 플래그를 사용하여 A/B 테스트 실행](implement/server-side/sdk-guides/on-device-decisioning/execute-ab-tests-with-feature-flags.md)
      + [속성을 사용하여 기능 테스트 실행](implement/server-side/sdk-guides/on-device-decisioning/execute-feature-tests-with-attributes.md)
      + [기능 테스트에 대한 롤아웃 관리](implement/server-side/sdk-guides/on-device-decisioning/manage-rollouts-for-feature-tests.md)
      + [개인화 게재](implement/server-side/sdk-guides/on-device-decisioning/deliver-personalization.md)
      + [지원되는 기능 개요](implement/server-side/sdk-guides/on-device-decisioning/supported-features.md)
      + [온디바이스 의사 결정 문제 해결](implement/server-side/sdk-guides/on-device-decisioning/troubleshooting.md)
      + [우수 사례](implement/server-side/sdk-guides/best-practices/best-practices.md)
   + Node.js SDK 참조 {#node-js}
      + [Node.js SDK 개요](implement/server-side/node-js/overview.md)
      + [Node.js SDK 설치](implement/server-side/node-js/install-sdk.md)
      + [Node.js SDK 초기화](implement/server-side/node-js/initialize-sdk.md)
      + [오퍼 가져오기(Node.js)](implement/server-side/node-js/get-offers.md)
      + [속성 가져오기(Node.js)](implement/server-side/node-js/get-attributes.md)
      + [알림 보내기(Node.js)](implement/server-side/node-js/send-notifications.md)
      + [SDK 이벤트(Node.js)](implement/server-side/node-js/sdk-events.md)
      + [로거(Node.js)](implement/server-side/node-js/logger.md)
      + [프록시 구성(Node.js)](implement/server-side/node-js/proxy-configuration.md)
   + Java SDK 참조 {#java}
      + [Java SDK 개요](implement/server-side/java/overview.md)
      + [Java SDK 설치](implement/server-side/java/install-sdk.md)
      + [Java SDK 초기화](implement/server-side/java/initialize-sdk.md)
      + [오퍼 가져오기(Java)](implement/server-side/java/get-offers.md)
      + [속성 가져오기(Java)](implement/server-side/java/get-attributes.md)
      + [알림 보내기(Java)](implement/server-side/java/send-notifications.md)
      + [SDK 이벤트(Java)](implement/server-side/java/sdk-events.md)
      + [로거(Java)](implement/server-side/java/logger.md)
      + [비동기 요청(Java)](implement/server-side/java/asynchronous-requests.md)
      + [프록시 구성(Java)](implement/server-side/java/proxy-configuration.md)
      + [사용자 지정 HTTP 클라이언트 구성(Java)](implement/server-side/java/custom-http-client.md)
      + [유틸리티 메서드(Java)](implement/server-side/java/utility-methods.md)
   + .NET SDK 참조 {#net}
      + [.NET SDK 개요](implement/server-side/net/overview.md)
      + [.Net SDK 설치](implement/server-side/net/install-sdk.md)
      + [.NET SDK 초기화](implement/server-side/net/initialize-sdk.md)
      + [오퍼 가져오기(.NET)](implement/server-side/net/get-offers.md)
      + [속성 가져오기(.NET)](implement/server-side/net/get-attributes.md)
      + [알림 보내기(.NET)](implement/server-side/net/send-notifications.md)
      + [SDK 이벤트(.NET)](implement/server-side/net/sdk-events.md)
      + [비동기 요청(.NET)](implement/server-side/net/asynchronous-requests.md)
   + Python SDK 참조 {#python}
      + [Python SDK 개요](implement/server-side/python/overview.md)
      + [Python SDK 설치](implement/server-side/python/install-sdk.md)
      + [Python SDK 초기화](implement/server-side/python/initialize-sdk.md)
      + [오퍼 가져오기(Python)](implement/server-side/python/get-offers.md)
      + [속성 가져오기(Python)](implement/server-side/python/get-attributes.md)
      + [알림 보내기(Python)](implement/server-side/python/send-notifications.md)
      + [SDK 이벤트(Python)](implement/server-side/python/sdk-events.md)
      + [비동기 요청(Python)](implement/server-side/python/asynchronous-requests.md)
      + [로거(Python)](implement/server-side/python/logger.md)
+ [하이브리드 구현](implement/hybrid/hybrid-overview.md)
+ [Recommendations 구현](implement/recommendations/recommendations.md)
+ 모바일 앱 구현 {#mobile-apps}
   + [모바일 앱을 위한 Target 개요](implement/mobile/overview.md)
   + [Target 모바일 미리보기](implement/mobile/target-mobile-preview.md)
   + [위치 서비스 사용](implement/mobile/use-location-service.md)
   + [모바일 앱을 위한 Target FAQ](implement/mobile/mobile-faq.md)
   + [웹 보기가 있는 기본 앱에서 AEP Mobile SDK를 사용하여 Target 구현](/help/dev/implement/mobile/native-app.md)
+ 이메일 구현 {#implement-email}
   + [이메일: Target 구현 개요](implement/email/overview.md)
   + [이미지용 Adbox 만들기](implement/email/testing-content-with-the-adbox.md)
   + [이메일 이미지 Adbox 테스트](implement/email/testing-email-image-adbox.md)
   + [리디렉터 작업](implement/email/working-with-redirectors.md)
+ API 안내서 {#api}
   + [Target API 개요](/help/dev/before-administer/target-api-overview.md)
   + [Target API에 대한 인증 구성](/help/dev/before-administer/configure-authentication.md)
   + 배달 API 안내서 {#delivery-api}
      + [게재 API 개요](/help/dev/implement/delivery-api/overview.md)
      + [게재 API와 상호 작용하는 SDK](/help/dev/before-implement/delivery-api-overview/sdks.md)
      + [시작하기](/help/dev/before-implement/delivery-api-overview/getting-started.md)
      + [사용자 권한(Premium)](/help/dev/before-implement/delivery-api-overview/user-permissions.md)
      + [방문자 식별](/help/dev/before-implement/delivery-api-overview/identifying-visitors.md)
      + [단일 또는 일괄 게재](/help/dev/before-implement/delivery-api-overview/single-or-batch.md)
      + [미리 가져오기](/help/dev/before-implement/delivery-api-overview/prefetch.md)
      + [알림](/help/dev/before-implement/delivery-api-overview/notifications.md)
      + [Experience Cloud과 통합](before-implement/delivery-api-overview/integration.md)
      + [고려 사항 및 알려진 제한 사항](/help/dev/before-implement/delivery-api-overview/known-limitations.md)
      + [클라이언트 힌트](/help/dev/before-implement/delivery-api-overview/client-hints.md)
      + [배달 API](/help/dev/implement/delivery-api/delivery-api.md)
   + 관리 API {#admin-api}
      + [관리 API 개요](before-administer/admin-api-overview/admin-api-overview.md)
      + [Adobe Target 관리 API](/help/dev/administer/admin-api/admin-api-overview-new.md)
   + [프로필 API](/help/dev/administer/profile-api/profile-api-overview.md)
   + [보고 API](/help/dev/administer/reporting-api/reporting-api.md)
   + RECOMMENDATIONS API {#recommendations-api}
      + [Recommendations API 개요](before-administer/recs-api/overview.md)
      + [API를 사용하여 카탈로그 관리](before-administer/recs-api/manage-catalog.md)
      + [사용자 지정 기준 관리](before-administer/recs-api/manage-custom-criteria.md)
      + [Recommendations에서 배달 API 사용](before-administer/recs-api/fetch-recs-server-side-delivery-api.md)
      + [RECOMMENDATIONS API](/help/dev/administer/recommendations-api/recommendations-api.md)
   + 모델 API {#models-api}
      + [모델 API(차단 목록에 추가) 개요](before-administer/models-api.md)
      + [모델 API](/help/dev/administer/models-api/models-api-overview.md)
   + [ADOBE ADMIN CONSOLE API](/help/dev/before-implement/delivery-api-overview/adobe-console-api.md)
   + [Adobe Experience Platform Edge Network Server API](/help/dev/before-implement/delivery-api-overview/aep-edge-network-server-api.md)
+ 구현 패턴 {#implementation-patterns}
   + [구현 패턴 개요](/help/dev/patterns/pattern-overview.md)
   + at.js를 사용한 Recommendations 구현 패턴 {#atjs}
      + [at.js를 사용하는 Recommendations 구현 패턴 개요](/help/dev/patterns/recs-atjs/recs-implementation-pattern-atjs.md)
      + [SDK 초기화](/help/dev/patterns/recs-atjs/initialize-sdk.md)
      + [데이터 컬렉션 구성](/help/dev/patterns/recs-atjs/data-collection.md)
      + [렌더링 경험](/help/dev/patterns/recs-atjs/render-experiences.md)
      + [타겟에게 알림](/help/dev/patterns/recs-atjs/notify-target.md)


