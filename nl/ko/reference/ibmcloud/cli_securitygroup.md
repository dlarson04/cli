---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-03"

keywords: cli, manage security groups, ingress, egress, traffic, virtual server cli, classic infrastructure cli, securitygroup, ibmcloud sl securitygroup, security group cli

subcollection: cloud-cli

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

# 가상 서버 트래픽에 대한 보안 그룹 관리
{: #sl-manage-securitygroups}

보안 그룹은 가상 서버 인스턴스의 퍼블릭 및 프라이빗 인터페이스 둘 다에 대한 수신(ingress) 및 발신(egress) 트래픽의 처리 방법을 정의하는 IP 필터 규칙 세트입니다. 보안 그룹에 추가하는 규칙을 보안 그룹 규칙이라고 합니다.

다음 명령을 사용하여 {{site.data.keyword.cloud}} 클래식 인프라 보안 그룹 서비스를 통해 보안 그룹을 관리하십시오.
{: shortdesc}

## ibmcloud sl securitygroup create
{: #sl_securitygroup_create}

보안 그룹을 작성합니다.
```
ibmcloud sl securitygroup create [OPTIONS]
```

<strong>명령 옵션</strong>:
<dl>
<dt>-n, --name</dt>
<dd>보안 그룹의 이름입니다.</dd>
<dt>-d, --description</dt>
<dd>보안 그룹의 설명입니다.</dd>
</dl>

## ibmcloud sl securitygroup delete
{: #sl_securitygroup_delete}

제공된 보안 그룹을 삭제합니다.
```
ibmcloud sl securitygroup delete SECURITYGROUP_ID [OPTIONS]
```

<strong>명령 옵션</strong>:
<dl>
<dt>-f, --force</dt>
<dd>확인 없이 조작 강제 실행.</dd>
</dl>

## ibmcloud sl securitygroup detail
{: #sl_securitygroup_detail}

보안 그룹에 대한 세부사항을 가져옵니다.
```
ibmcloud sl securitygroup detail SECURITYGROUP_ID [OPTIONS]
```

## ibmcloud sl securitygroup edit
{: #sl_securitygroup_edit}

보안 그룹에 대한 세부사항을 편집합니다.
```
ibmcloud sl securitygroup edit SECURITYGROUP_ID [OPTIONS]
```

<strong>명령 옵션</strong>:
<dl>
<dt>-n, --name</dt>
<dd>보안 그룹의 이름입니다.</dd>
<dt>-d, --description</dt>
<dd>보안 그룹의 설명입니다.</dd>
</dl>

## ibmcloud sl securitygroup interface-add
{: #sl_securitygroup_interface_add}

보안 그룹에 인터페이스를 연결합니다.
```
ibmcloud sl securitygroup interface-add SECURITYGROUP_ID [OPTIONS]
```

<strong>명령 옵션</strong>:
<dl>
<dt>-n, --network-component</dt>
<dd>보안 그룹과 연관시킬 네트워크 컴포넌트 ID입니다.</dd>
<dt>-s, --server</dt>
<dd>보안 그룹과 연관시킬 서버 ID입니다.</dd>
<dt>-i, --interface</dt>
<dd>연관시킬 서버의 인터페이스입니다(공용/사설).</dd>
</dl>

## ibmcloud sl securitygroup interface-list
{: #sl_securitygroup_interface_list}

보안 그룹과 연관된 인터페이스를 나열합니다.
```
ibmcloud sl securitygroup interface-list SECURITYGROUP_ID [OPTIONS]
```

<strong>명령 옵션</strong>:
<dl>
<dt>--sortby</dt>
<dd>정렬 기준 열, 옵션: id,virtualServerId,hostname.</dd>
</dl>

## ibmcloud sl securitygroup interface-remove
{: #sl_securitygroup_interface_remove}

보안 그룹에서 인터페이스를 분리합니다.
```
ibmcloud sl securitygroup interface-remove SECURITYGROUP_ID [OPTIONS]
```

<strong>명령 옵션</strong>:
<dl>
<dt>-n, --network-component</dt>
<dd>보안 그룹에서 제거할 네트워크 컴포넌트입니다.</dd>
<dt>-s, --server</dt>
<dd>보안 그룹에서 제거할 서버 ID입니다.</dd>
<dt>-i, --interface</dt>
<dd>제거할 서버의 인터페이스입니다(공용/사설).</dd>
</dl>

## ibmcloud sl securitygroup list
{: #sl_securitygroup_list}

보안 그룹을 나열합니다.
```
List security groups
```

<strong>명령 옵션</strong>:
<dl>
<dt>--sortby</dt>
<dd>정렬 기준 열, 옵션: id,name,description,created.</dd>
</dl>

## ibmcloud sl securitygroup rule-add
{: #sl_securitygroup_rule_add}

보안 그룹 규칙을 보안 그룹에 추가합니다.
```
ibmcloud sl securitygroup rule-add SECURITYGROUP_ID [OPTIONS]
```

<strong>명령 옵션</strong>:
<dl>
<dt>-r, --remote-ip</dt>
<dd>적용할 원격 IP/CIDR입니다.</dd>
<dt>-s, --remote-group</dt>
<dd>적용할 원격 보안 그룹의 ID입니다.</dd>
<dt>-d, --direction</dt>
<dd>적용할 트래픽의 방향이며(ingress,egress), 필수입니다.</dd>
<dt>-e, --ether-type</dt>
<dd>적용할 ethertype(IPv4 또는 IPv6)이며, 지정되지 않은 경우 기본값은 IPv4입니다.</dd>
<dt>-M, --port-max</dt>
<dd>적용할 상위 포트입니다.</dd>
<dt>-m, --port-min</dt>
<dd>적용할 하위 포트입니다.</dd>
<dt>-p, --protocol</dt>
<dd>적용할 프로토콜(icmp, tcp, udp)입니다.</dd>
</dl>

## ibmcloud sl securitygroup rule-edit
{: #sl_securitygroup_rule_edit}

보안 그룹의 보안 그룹 규칙을 편집합니다.
```
ibmcloud sl securitygroup rule-edit SECURITYGROUP_ID RULE_ID [OPTIONS]
```

<strong>명령 옵션</strong>:
<dl>
<dt>-r, --remote-ip</dt>
<dd>적용할 원격 IP/CIDR입니다.</dd>
<dt>-s, --remote-group</dt>
<dd>적용할 원격 보안 그룹의 ID입니다.</dd>
<dt>-d, --direction</dt>
<dd>적용할 트래픽의 방향이며(ingress,egress), 필수입니다.</dd>
<dt>-e, --ether-type</dt>
<dd>적용할 ethertype(IPv4 또는 IPv6)이며, 지정되지 않은 경우 기본값은 IPv4입니다.</dd>
<dt>-M, --port-max</dt>
<dd>적용할 상위 포트입니다.</dd>
<dt>-m, --port-min</dt>
<dd>적용할 하위 포트입니다.</dd>
<dt>-p, --protocol</dt>
<dd>적용할 프로토콜(icmp, tcp, udp)입니다.</dd>
</dl>

## ibmcloud sl securitygroup rule-list
{: #sl_securitygroup_rule_list}

그룹 규칙을 나열합니다.
```
ibmcloud sl securitygroup rule-list SECURITYGROUP_ID [OPTIONS]
```

<strong>명령 옵션</strong>:
<dl>
<dt>--sortby</dt>
<dd>정렬 기준 열, 옵션: id,remoteIp,remoteGroupId,direction,ethertype,portRangeMin,portRangeMax,protocol.</dd>
</dl>

## ibmcloud sl securitygroup rule-remove
{: #sl_securitygroup_rule_remove}

보안 그룹에서 규칙을 제거합니다.
```
ibmcloud sl securitygroup rule-remove SECURITYGROUP_ID RULE_ID [OPTIONS]
```

<strong>명령 옵션</strong>:
<dl>
<dt>-f, --force</dt>
<dd>확인 없이 조작 강제 실행.</dd>
</dl>
