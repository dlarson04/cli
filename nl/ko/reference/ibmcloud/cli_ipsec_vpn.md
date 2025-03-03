---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-03"

keywords: cli, classic infrastructure, ipsec, vpn, ibmcloud sl ipsec, tunnel, vpn access, encryption, vpn tunnel cli, ipsec vpn tunnel

subcollection: cloud-cli

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

# IPSec VPN 터널 관리
{: #sl-manage-ipsec-vpn-tunnels}

{{site.data.keyword.cloud}} VPN 액세스를 통해 사용자는 {{site.data.keyword.cloud_notm}} 사설 네트워크에서 모든 서버를 안전하게 원격으로 관리할 수 있습니다. 사용자 위치에서 사설 네트워크로의 VPN을 연결하면 암호화된 VPN 터널을 통해 대역 외 관리 및 서버 복구를 지원할 수 있습니다.

다음 명령을 사용하여 {{site.data.keyword.cloud_notm}} 클래식 인프라 IPSec VPN 서비스에서 IPSec VPN 터널을 관리하십시오.
{: shortdesc}

## ibmcloud sl ipsec cancel
{: #sl_ipsec_cancel}

IPSec VPN 터널 컨텍스트를 취소합니다.
```
ibmcloud sl ipsec cancel CONTEXT_ID [OPTIONS]
```

<strong>명령 옵션</strong>:
<dl>
<dt>--immediate</dt>
<dd>청구 주기 대신 즉시 IPSec 취소.</dd>
<dt>--reason</dt>
<dd>취소에 대한 선택적 이유.</dd>
<dt>-f, --force</dt>
<dd>확인 없이 조작 강제 실행.</dd>
</dl>

## ibmcloud sl ipsec config
{: #sl_ipsec_config}

터널 컨텍스트의 구성을 요청합니다.
```
ibmcloud sl ipsec config CONTEXT_ID [OPTIONS]
```

## ibmcloud sl ipsec detail
{: #sl_ipsec_detail}

IPSec VPN 터널 컨텍스트 세부사항을 나열합니다.
```
ibmcloud sl ipsec detail CONTEXT_ID [OPTIONS]
```

<strong>명령 옵션</strong>:
<dl>
<dt>-i, --include</dt>
<dd>추가 리소스 포함. 옵션: at,is,rs,sr,ss.</dd>
</dl>

## ibmcloud sl ipsec list
{: #sl_ipsec_list}

IPSec VPN 터널 컨텍스트를 나열합니다.
```
ibmcloud sl ipsec list [OPTIONS]
```

<strong>명령 옵션</strong>:
<dl>
<dt>--order</dt>
<dd>IPSEC을 구매한 주문 ID별 필터링.</dd>
</dl>

## ibmcloud sl ipsec order
{: #sl_ipsec_order}

IPSec VPN 터널을 주문합니다.
```
ibmcloud sl ipsec order [OPTIONS]
```

<strong>명령 옵션</strong>:
<dl>
<dt>-d, --datacenter</dt>
<dd>필수. IPSEC에 대한 데이터 센터의 짧은 이름(예: dal09).</dd>
</dl>

## ibmcloud sl ipsec subnet-add
{: #sl_ipsec_subnet_add}

IPSec 터널 컨텍스트에 서브넷을 추가합니다.
```
ibmcloud sl ipsec subnet-add CONTEXT_ID [OPTIONS]
```

<strong>명령 옵션</strong>:
<dl>
<dt>-s, --subnet-id</dt>
<dd>추가할 서브넷 ID. 필수.</dd>
<dt>-t, --subnet-type</dt>
<dd>추가할 서브넷 유형. 필수. 옵션: internal,remote,service.</dd>
<dt>-n, --network</dt>
<dd>작성할 서브넷 네트워크 ID.</dd>
</dl>

## ibmcloud sl ipsec subnet-remove
{: #sl_ipsec_subnet_remove}

IPSEC 터널 컨텍스트에서 서브넷을 제거합니다.
```
ibmcloud sl ipsec subnet-remove CONTEXT_ID SUBNET_ID SUBNET_TYPE [OPTIONS]
```

## ibmcloud sl ipsec translation-add
{: #sl_ipsec_translation_add}

IPSec 터널에 주소 변환을 추가합니다.
```
ibmcloud sl ipsec translation-add CONTEXT_ID [OPTIONS]
```

<strong>명령 옵션</strong>:
<dl>
<dt>-s, --static-ip</dt>
<dd>정적 IP 주소. 필수.</dd>
<dt>-r, --remote-ip</dt>
<dd>원격 IP 주소. 필수.</dd>
<dt>-n, --note</dt>
<dd>참고.</dd>
</dl>

## ibmcloud sl ipsec translation-remove
{: #sl_ipsec_translation_remove}

IPSec에서 변환 항목을 제거합니다.
```
ibmcloud sl ipsec translation-remove CONTEXT_ID TRANSLATION_ID [OPTIONS]
```

## ibmcloud sl ipsec translation-update
{: #sl_ipsec_translation_update}

IPSec에 대한 주소 변환을 업데이트합니다.
```
ibmcloud sl ipsec translation-update CONTEXT_ID TRANSLATION_ID [OPTIONS]
```

<strong>명령 옵션</strong>:
<dl>
<dt>-s, --static-ip</dt>
<dd>정적 IP 주소. 필수.</dd>
<dt>-r, --remote-ip</dt>
<dd>원격 IP 주소. 필수.</dd>
<dt>-n, --note</dt>
<dd>참고.</dd>
</dl>

## ibmcloud sl ipsec update
{: #sl_ipsec_update}

터널 컨텍스트 특성을 업데이트합니다.
```
ibmcloud sl ipsec update CONTEXT_ID [OPTIONS]
```

<strong>명령 옵션</strong>:
<dl>
<dt>-n, --name</dt>
<dd>별명.</dd>
<dt>-r, --remote-peer</dt>
<dd>원격 피어 IP 주소.</dd>
<dt>-k, --preshared-key</dt>
<dd>사전 공유된 키.</dd>
<dt>-a, --phase1-auth</dt>
<dd>1단계(Phase) 인증. 옵션: MD5,SHA1,SHA256.</dd>
<dt>-c, --phase1-crypto</dt>
<dd>1단계(Phase) 암호화. 옵션: DES,3DES,AES128,AES192,AES256.</dd>
<dt>-d, --phase1-dh</dt>
<dd>1단계(Phase) diffie hellman 그룹. 옵션: 0,1,2,5.</dd>
<dt>-t, --phase1-key-ttl</dt>
<dd>1단계(Phase) 키 수명. 범위: 120 - 172800.</dd>
<dt>-u, --phase2-auth</dt>
<dd>2단계(Phase) 인증. 옵션: MD5,SHA1,SHA256.</dd>
<dt>-y, --phase2-crypto</dt>
<dd>2단계(Phase) 암호화. 옵션: DES,3DES,AES128,AES192,AES256.</dd>
<dt>-e, --phase2-dh</dt>
<dd>2단계(Phase) diffie hellman 그룹. 옵션: 0,1,2,5.</dd>
<dt>-f, --phase2-forward-secrecy</dt>
<dd>2단계(Phase) PFS(Perfect Forward Secrecy). 범위: 0 - 1.</dd>
<dt>-l, --phase2-key-ttl</dt>
<dd>2단계(Phase) 키 수명. 범위: 120 - 172800.</dd>
</dl>
