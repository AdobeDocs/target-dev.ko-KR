---
keywords: client care, cname, 인증서 프로그램, 표준 이름, 쿠키, 인증서, amc, adobe 관리 인증서, digicert, 도메인 제어 유효성 검사, dcv, client care2
description: '[!UICONTROL Adobe Client Care]과(와) 함께  [!DNL Adobe Target] 에서 CNAME(표준 이름) 지원을 구현하여 광고 차단 문제를 해결합니다.'
title: Target에서 CNAME을 사용하는 방법
feature: Privacy & Security
exl-id: 5709df5b-6c21-4fea-b413-ca2e4912d6cb
source-git-commit: dd99cf1753e4fa5033ee463b79a31c6eddcd02b5
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 1%

---

# CNAME 및 Target

[!DNL Adobe Target]에서 CNAME(표준 이름) 지원을 구현하기 위한 [!DNL Adobe Client Care] 작업 지침. CNAME을 사용하여 광고 차단 문제 또는 ITP 관련(Intelligent Tracking Prevention) 쿠키 정책을 처리합니다. CNAME을 사용하면 Adobe이 소유한 도메인이 아니라 고객이 소유한 도메인이 호출됩니다.

## Target에서 CNAME 지원 요청

1. SSL 인증서에 필요한 호스트 이름 목록을 확인합니다(아래 FAQ 참조).

1. 각 호스트 이름에 대해 일반 [!DNL Target] 호스트 이름 `clientcode.tt.omtrdc.net`을(를) 가리키는 DNS에 CNAME 레코드를 만듭니다.

   예를 들어 클라이언트 코드가 &quot;cnamecustomer&quot;이고 제안된 호스트 이름이 `target.example.com`인 경우 DNS CNAME 레코드는 다음과 비슷합니다.

   ```
   target.example.com.  IN  CNAME  cnamecustomer.tt.omtrdc.net.
   ```

   >[!WARNING]
   >
   >Adobe의 인증 기관인 DigiCert는 이 단계가 완료될 때까지 인증서를 발급할 수 없습니다. 따라서 Adobe은 이 단계가 완료될 때까지 CNAME 구현에 대한 요청을 이행할 수 없습니다.

1. [이 양식을 작성](assets/FPC_Request_Form.xlsx)한 다음 [CNAME 지원을 요청하는 Adobe Client Care 티켓을 열 때 포함](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html?#reference_ACA3391A00EF467B87930A450050077C):

   * [!DNL Adobe Target] 클라이언트 코드:
   * SSL 인증서 호스트 이름(예: `target.example.com target.example.org`):
   * SSL 인증서 구매자(Adobe이 적극 권장됨, FAQ 참조): Adobe/고객
   * 고객이 &quot;자체 인증서 가져오기&quot;(BYOC)라고도 하는 인증서를 구입할 경우 다음 추가 세부 정보를 작성하십시오.
      * 인증서 조직(예: Company Inc):
      * 인증서 조직 단위(선택 사항, 예: 마케팅):
      * 인증서 국가(예: 미국):
      * 인증서 주/지역(예: 캘리포니아):
      * 인증서 도시(예: 산호세):

1. Adobe이 인증서를 구매하는 경우 Adobe은 DigiCert와 협력하여 Adobe의 프로덕션 서버에 인증서를 구매하고 배포합니다.

   고객이 인증서(BYOC)를 구매하는 경우 Adobe Client Care가 CSR(인증서 서명 요청)을 보냅니다. 선택한 인증 기관을 통해 인증서를 구입할 때는 CSR을 사용하십시오. 인증서가 발급되면 인증서의 사본과 중간 인증서를 배포를 위해 Adobe Client Care로 보냅니다.

   Adobe Client Care는 구현이 준비되면 알려줍니다.

1. `serverDomain` [설명서](../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#serverdomain)를 새 CNAME 호스트 이름으로 업데이트하고 at.js 구성에서 `overrideMboxEdgeServer`을(를) `false` [설명서](../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#overridemboxedgeserver)(으)로 설정합니다.

## 자주 묻는 질문

다음 정보는 Target에서 CNAME 지원 요청 및 구현에 대해 자주 묻는 질문에 대한 답을 제공합니다.

### 자체 인증서를 제공할 수 있습니까(자체 인증서 또는 BYOC 가져오기)?

고유한 인증서를 제공할 수 있습니다. 그러나 Adobe은 이 방법을 권장하지 않습니다. Adobe과 사용자는 Adobe에서 인증서를 구매하고 제어하는 경우 SSL 인증서 라이프사이클을 보다 쉽게 관리할 수 있습니다. SSL 인증서는 매년 갱신해야 합니다. 따라서 Adobe Client Care는 적시에 새 인증서를 받기 위해 매년 귀하에게 연락해야 합니다. 일부 고객은 갱신된 인증서를 적시에 생산하는 데 어려움을 겪을 수 있습니다. 브라우저에서 연결을 거부하므로 인증서가 만료되면 [!DNL Target] 구현이 위태롭게 됩니다.

>[!WARNING]
>
>[!DNL Target] 자체 인증서 가져오기 CNAME 구현을 요청하는 경우 매년 Adobe Client Care에 갱신된 인증서를 제공해야 합니다. Adobe에서 갱신된 인증서를 배포하기 전에 CNAME 인증서가 만료되도록 허용하면 특정 [!DNL Target] 구현이 중단됩니다.

### 새 SSL 인증서가 만료될 때까지 얼마나 걸립니까?

Adobe에서 구입한 모든 인증서는 1년 동안 유효합니다. 자세한 내용은 1년 인증서에 대한 [DigiCert의 문서](https://www.digicert.com/blog/position-on-1-year-certificates)를 참조하십시오.

### 어떤 호스트 이름을 선택해야 합니까? 도메인당 몇 개의 호스트 이름을 선택해야 합니까?

Target CNAME 구현에는 SSL 인증서 및 고객 DNS에서 도메인당 하나의 호스트 이름만 필요합니다. Adobe은 도메인당 하나의 호스트 이름을 권장합니다. 일부 고객은 자체 목적(예: 스테이징에서 테스트)을 위해 도메인당 더 많은 호스트 이름을 필요로 하는데, 이는 지원됩니다.

대부분의 고객이 `target.example.com`과(와) 같은 호스트 이름을 선택합니다. Adobe은 이 방법을 따를 것을 권장하지만, 선택은 결국 귀하의 것입니다. 기존 DNS 레코드의 호스트 이름을 요청하지 마십시오. 이렇게 하면 충돌이 발생하고 [!DNL Target] CNAME 요청을 해결하는 데 걸리는 시간이 지연됩니다.

### Adobe Analytics에 대한 CNAME 구현이 이미 있습니다. 동일한 인증서 또는 호스트 이름을 사용할 수 있습니까?

아니요. [!DNL Target]에는 별도의 호스트 이름과 인증서가 필요합니다.

### 현재 [!DNL Target] 구현이 ITP 2.x의 영향을 받습니까?

Apple ITP(Intelligent Tracking Prevention) 버전 2.3에서는 [!DNL Target]개의 CNAME 구현을 감지하고 쿠키의 만료를 7일로 줄이는 CNAME 클로킹 완화 기능을 도입했습니다. 현재 [!DNL Target]에는 ITP의 CNAME 클로킹 완화에 대한 해결 방법이 없습니다. ITP에 대한 자세한 내용은 [Apple ITP(Intelligent Tracking Prevention) 2.x](../before-implement/privacy/apple-itp-2x.md)을 참조하십시오.

### CNAME 구현이 배포될 때 예상되는 서비스 중단 유형은 무엇입니까?

인증서가 배포되면(인증서 갱신 포함) 서비스가 중단되지 않습니다.

그러나 [!DNL Target] 구현 코드(`serverDomain` at.js)의 호스트 이름을 새 CNAME 호스트 이름(`target.example.com`)으로 변경하면 웹 브라우저에서는 재방문자를 새 방문자로 취급합니다. 이전 호스트 이름(`clientcode.tt.omtrdc.net`)에서 이전 쿠키에 액세스할 수 없으므로 재방문자의 프로필 데이터가 손실됩니다. 브라우저 보안 모델로 인해 이전 쿠키에 액세스할 수 없습니다. 이 중단은 새 CNAME에 대한 초기 컷오버 시에만 발생합니다. 호스트 이름이 변경되지 않으므로 인증서 갱신에는 동일한 효과가 없습니다.

### 내 CNAME 구현에 사용되는 키 유형 및 인증서 서명 알고리즘은 무엇입니까?

모든 인증서는 RSA SHA-256이며 키는 기본적으로 RSA 2048비트입니다. 2048비트보다 큰 키 크기는 현재 지원되지 않습니다.

### CNAME 구현이 트래픽에 대해 준비되었는지 어떻게 확인할 수 있습니까?

macOS 또는 Linux 명령줄 터미널에서 bash 및 curl >=7.49를 사용하여 다음 명령 세트를 사용합니다.

1. 이 bash 함수를 복사하여 터미널에 붙여넣거나 함수를 bash 시작 스크립트 파일(일반적으로 `~/.bash_profile` 또는 `~/.bashrc`)에 붙여넣어 터미널 세션에서 함수를 사용할 수 있도록 하십시오.

   ```
   function adobeTargetCnameValidation {
     local hostname="$1"
     if [ -z "$hostname" ]; then
       echo "ERROR: no hostname specified"
       return 1
     fi  local service="Adobe Target CNAME implementation"
     local edges="41 42 44 45 46 47 48"
     local edgeDomain="tt.omtrdc.net"
     local edgeFormat="mboxedge%d%s.$edgeDomain"
     local poolDomain="pool.data.adobedc.net"
     local shards=5
     local shardsFoundCount=0
     local shardsFound
     local shardsFoundOutput
     local curlRegex="subject:.*CN=|expire date:|issuer:"
     local curlValidation="SSL certificate verify ok"
     local curlResponseValidation='"OK"'
     local curlEndpoint="/uptime?mboxClient=uptime3"
     local url="https://$hostname$curlEndpoint"
     local sslShopperUrl="https://www.sslshopper.com/ssl-checker.html#hostname=$hostname"
     local success="✅"
     local failure="🚫"
     local info="🔎"
     local rule="="
     local horizontalRule="$(seq ${COLUMNS:-30} | xargs printf "$rule%.0s")"
     local miniRule="$(seq 5 | xargs printf "$rule%.0s")"
     local curlVersion="$(curl --version | head -1 | cut -d' ' -f2 )"
     local curlVersionRequired=">=7.49"
     local edgeCount="$(wc -w <<< "$edges" | tr -d ' ')"
     local shard
     local currShard
     local dnsOutput
     local cnameExists
     local endToEndTestSucceeded
     local curlResult  for region in IRL1 IND1 SIN OR SYD VA TYO; do
       currShard="${region}-${poolDomain}"
       curlResult="$(curl -vsm20 --connect-to "$hostname:443:$currShard:443" "$url" 2>&1)"
       if grep -q "$curlValidation" <<< "$curlResult"; then
         shardsFound+=" $currShard"
         if grep -q "$curlResponseValidation" <<< "$curlResult"; then
           shardsFoundCount=$((shardsFoundCount+1))
           shardsFoundOutput+="\n\n$miniRule $success $hostname [edge shard: $currShard] $miniRule\n"
         else
           shardsFoundOutput+="\n\n$miniRule $failure $hostname [edge shard: $currShard] $miniRule\n"
         fi
         shardsFoundOutput+="$(grep -E "$curlRegex" <<< "$curlResult" | sort)"
         if ! grep -q "$curlResponseValidation" <<< "$curlResult"; then
           shardsFoundOutput+="\nERROR: unexpected HTTP response from this shard using $url"
         fi
       fi
     done
     echo
     echo "$horizontalRule"
     echo
     echo "$service validation for hostname $hostname:"
     dnsOutput="$(dig -t CNAME +short "$hostname" 2>&1)"
     if grep -qFi ".$edgeDomain" <<< "$dnsOutput"; then
       echo "$success $hostname passes DNS CNAME validation"
       cnameExists=true
     else
       echo -n "$failure $hostname FAILED DNS CNAME validation -- "
       if [ -n "$dnsOutput" ]; then
         echo -e "$dnsOutput is not in the subdomain $edgeDomain"
       else
         echo "required DNS CNAME record pointing to <target-client-code>.$edgeDomain not found"
       fi
     fi  for region in IRL1 IND1 SIN OR SYD VA TYO; do
       curlResult="$(curl -vsm20 --connect-to "$hostname:443:${region}-pool.data.adobedc.net:443" "https://$hostname$curlEndpoint" 2>&1)"
       if grep -q "$curlValidation" <<< "$curlResult"; then
         if grep -q "$curlResponseValidation" <<< "$curlResult"; then
           echo -en "$success $hostname passes TLS and HTTP response validation for region $region"
           if [ -n "$cnameExists" ]; then
             echo
           else
             echo " -- the DNS CNAME is not pointing to the correct subdomain for ${service}s with Adobe-managed certificates" \
               "(bring-your-own-certificate implementations don't have this requirement), but this test passes as configured"
           fi
           endToEndTestSucceeded=true
         else
           echo -n "$failure $hostname FAILED HTTP response validation for region $region --" \
             "unexpected response from $url -- "
           if [ -n "$cnameExists" ]; then
             echo "DNS is NOT pointing to the correct shard, notify Adobe Client Care"
           else
             echo "the required DNS CNAME record is missing, see above"
           fi
         fi
       else
         echo -n "$failure $hostname FAILED TLS validation for region $region -- "
         if [ -n "$cnameExists" ]; then
           echo "DNS is likely NOT pointing to the correct shard or there's a validation issue with the certificate or" \
             "protocols, see curl output below and optionally SSL Shopper ($sslShopperUrl):"
           echo ""
           echo "$horizontalRule"
           echo "$curlResult" | sed 's/^/    /g'
           echo "$horizontalRule"
           echo ""
         else
           echo "the required DNS CNAME record is missing, see above"
         fi
       fi
     done  if [ "$shardsFoundCount" -ge "$edgeCount" ]; then
       echo -n "$success $hostname passes shard validation for the following $shardsFoundCount edge shards:"
       echo -e "$shardsFoundOutput"
       echo    if [ -n "$cnameExists" ] && [ -n "$endToEndTestSucceeded" ]; then
         echo "$horizontalRule"
         echo ""
         echo "  For additional TLS/SSL validation, see SSL Shopper:"
         echo ""
         echo "    $info  $sslShopperUrl"
         echo ""
         echo "  To check DNS propagation around the world, see whatsmydns.net:"
         echo ""
         echo "    $info  DNS A records:     https://whatsmydns.net/#A/$hostname"
         echo "    $info  DNS CNAME record:  https://whatsmydns.net/#CNAME/$hostname"
       fi
     else
       echo -n "$failure $hostname FAILED shard validation -- shards found: $shardsFoundCount," \
         "expected: $edgeCount"
       if bc -l <<< "$(cut -d. -f1,2 <<< "$curlVersion") $curlVersionRequired" 2>/dev/null | grep -q 0; then
         echo -n " -- insufficient curl version installed: $curlVersion, but this script requires curl version" \
           "$curlVersionRequired because it uses the curl --connect-to flag to bypass DNS and directly test" \
           "each Adobe Target edge shards' SNI configuration for $hostname"
       fi
       if [ -n "$shardsFoundOutput" ]; then
         echo -e ":\n$shardsFoundOutput"
       fi
       echo
     fi
     echo
     echo "$horizontalRule"
     echo
   }
   ```

1. `target.example.com`을(를) 호스트 이름으로 바꾸면서 이 명령을 붙여 넣습니다.

   ```
   adobeTargetCnameValidation target.example.com
   ```

   구현이 준비되면 아래와 같은 출력이 표시됩니다. 중요한 점은 모든 유효성 검사 상태 줄에 `🚫`이(가) 아닌 `✅`이(가) 표시된다는 것입니다. 각 Target 에지 CNAME 분할에는 요청된 인증서의 기본 호스트 이름과 일치하는 `CN=target.example.com`이(가) 표시됩니다(인증서의 추가 SAN 호스트 이름은 이 출력에 인쇄되지 않음).

   ```
      $ adobeTargetCnameValidation
    target.example.com==========================================================Adobe Target CNAME implementation validation for hostname target.example.com:
    ✅ target.example.com passes DNS CNAME validation
    ✅ target.example.com passes TLS and HTTP response validation for region IRL1
    ✅ target.example.com passes TLS and HTTP response validation for region IND1
    ✅ target.example.com passes TLS and HTTP response validation for region SIN
    ✅ target.example.com passes TLS and HTTP response validation for region OR
    ✅ target.example.com passes TLS and HTTP response validation for region SYD
    ✅ target.example.com passes TLS and HTTP response validation for region VA
    ✅ target.example.com passes TLS and HTTP response validation for region TYO
    ✅ target.example.com passes shard validation for the following 7 edge shards:===== ✅ target.example.com [edge shard: IRL1-pool.data.adobedc.net] =====
    *  expire date: Feb 20 23:59:59 2026 GMT
    *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
    *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com===== ✅ target.example.com [edge shard: IND1-pool.data.adobedc.net] =====
    *  expire date: Feb 20 23:59:59 2026 GMT
    *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
    *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com===== ✅ target.example.com [edge shard: SIN-pool.data.adobedc.net] =====
    *  expire date: Feb 20 23:59:59 2026 GMT
    *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
    *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com===== ✅ target.example.com [edge shard: OR-pool.data.adobedc.net] =====
    *  expire date: Feb 20 23:59:59 2026 GMT
    *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
    *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com===== ✅ target.example.com [edge shard: SYD-pool.data.adobedc.net] =====
    *  expire date: Feb 20 23:59:59 2026 GMT
    *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
    *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com===== ✅ target.example.com [edge shard: VA-pool.data.adobedc.net] =====
    *  expire date: Feb 20 23:59:59 2026 GMT
    *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
    *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com===== ✅ target.example.com [edge shard: TYO-pool.data.adobedc.net] =====
    *  expire date: Feb 20 23:59:59 2026 GMT
    *  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
    *  subject: C=US; ST=California; L=San Jose; O=Adobe Systems Incorporated; CN=target.example.com==========================================================  For additional TLS/SSL validation, see SSL Shopper:    🔎  https://www.sslshopper.com/ssl-checker.html#hostname=target.example.com  To check DNS propagation around the world, see whatsmydns.net:    🔎  DNS A records:     https://whatsmydns.net/#A/target.example.com
        🔎  DNS CNAME record:  https://whatsmydns.net/#CNAME/target.example.com
   ```

>[!NOTE]
>
>DNS 유효성 검사 시 이 유효성 검사 명령이 실패하지만 이미 필요한 DNS 변경 사항을 적용한 경우에는 DNS 업데이트가 완전히 전파될 때까지 기다려야 할 수 있습니다. DNS 레코드에는 해당 레코드의 DNS 회신에 대한 캐시 만료 시간을 나타내는 연결된 [TTL(time-to-live)](https://en.wikipedia.org/wiki/Time_to_live#DNS_records)이(가) 있습니다. 따라서 TTL만큼 기다려야 할 수도 있습니다. `dig target.example.com` 명령 또는 [G Suite 도구 상자](https://toolbox.googleapps.com/apps/dig/#CNAME)를 사용하여 특정 TTL을 조회할 수 있습니다. 전 세계의 DNS 전파를 확인하려면 [whatsmydns.net](https://whatsmydns.net/#CNAME)을 참조하세요.

### CNAME으로 옵트아웃 링크를 사용하는 방법

CNAME을 사용하는 경우 옵트아웃 링크에 &quot;client=`clientcode` 매개 변수가 포함되어야 합니다. 예:
`https://my.cname.domain/optout?client=clientcode`.

`clientcode`을(를) 클라이언트 코드로 바꾼 다음 [옵트아웃 URL](privacy/privacy.md)에 연결할 텍스트나 이미지를 추가하십시오.

## 알려진 제한 사항

* CNAME 및 at.js 1.x가 있는 경우 QA 모드는 서드파티 쿠키를 기반으로 하므로 고정되지 않습니다. 해결 방법은 탐색하는 각 URL에 미리보기 매개 변수를 추가하는 것입니다. CNAME 및 at.js 2.x가 있는 경우 QA 모드는 고정적입니다.
* CNAME을 사용하는 경우 [!DNL Target] 호출에 대한 쿠키 헤더의 크기가 증가할 수 있습니다. Adobe에서는 쿠키 크기를 8KB 미만으로 유지하는 것이 좋습니다.
