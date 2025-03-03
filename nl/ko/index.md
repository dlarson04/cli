---

copyright:
  years: 2015, 2019
lastupdated: "2019-05-21"

keywords: cli, IBM Cloud Developer Tools CLI, ibmcloud cli, download cli, ibmcloud dev, cloud cli, dev plugin, dev plug-in, cloud command line, developer tools, dev tools, install cloud cli, getting started cli

subcollection: cloud-cli

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}
{:note: .note}

# {{site.data.keyword.cloud_notm}} CLI 시작하기
{: #ibmcloud-cli}

이 튜토리얼에서는 {{site.data.keyword.cloud}} 개발자 도구 세트를 설치하고, 설치를 확인하고, 환경을 구성합니다. {{site.data.keyword.dev_cli_notm}}는 클라우드 애플리케이션의 작성, 개발 및 배치를 위한 명령행 접근 방식을 제공합니다.
{: shortdesc}

이 튜토리얼의 설치 명령은 사용 가능한 최신 독립형 {{site.data.keyword.cloud_notm}} CLI 버전을 설치하며 다음과 같은 도구도 설치합니다.

* `Homebrew`(Mac 전용)
* `Git`
* `Docker`
* `Helm`
* `kubectl`
* `curl`
* {{site.data.keyword.dev_cli_notm}} 플러그인
* {{site.data.keyword.IBM_notm}} {{site.data.keyword.openwhisk_short}} 플러그인
* {{site.data.keyword.registrylong_notm}} 플러그인
* {{site.data.keyword.containerlong_notm}} 플러그인
* `sdk-gen` 플러그인

## 시작하기 전에
{: #idt-prereq}

[{{site.data.keyword.cloud_notm}} 계정](https://cloud.ibm.com/){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘") 및 다음 시스템 요구사항이 필요합니다.

* Windows&trade;를 실행 중인 경우 Windows&trade; 10 Pro를 실행하지 않는 한 일부 기능이 지원되지 않습니다.
* 최소 버전 1.13.1의 안정된 Docker 채널을 사용해야 합니다.

## 1단계: 설치 명령 실행
{: #step1-install-idt}

명령을 실행하면 최신 버전의 {{site.data.keyword.cloud_notm}} CLI가 설치됩니다.

* Mac 및 Linux&trade;의 경우 다음 명령을 실행하십시오.
  ```
curl -sL https://ibm.biz/idt-installer | bash
  ```
  {: codeblock}

* Windows&trade; 10 Pro의 경우 관리자로 다음 명령을 실행하십시오.
  ```
  [Net.ServicePointManager]::SecurityProtocol = "Tls12"; iex(New-Object Net.WebClient).DownloadString('https://ibm.biz/idt-win-installer')
  ```
  {: codeblock}

  Windows&trade; PowerShell 아이콘을 마우스 오른쪽 단추로 클릭한 후 **관리자로 실행**을 선택하십시오.
  {: tip}

[GitHub 저장소](https://github.com/IBM-Cloud/ibm-cloud-developer-tools){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")에서 설치 프로그램 스크립트를 다운로드할 수도 있습니다.

{{site.data.keyword.cloud_notm}} 데디케이티드 환경용으로 최신 버전이 아닌 32비트 버전의 CLI나 이전 버전을 사용해야 하는 경우에는 [{{site.data.keyword.cloud_notm}} CLI 릴리스](https://github.com/IBM-Cloud/ibm-cloud-cli-release/releases/){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")를 참조하십시오.
{: note}

## 2단계. 설치 확인
{: #step2-verify-idt}

CLI 및 개발자 도구가 설치되었는지 확인하려면 `help` 명령을 실행하십시오.
```
ibmcloud dev help
```
{: codeblock}

출력에 사용법 지시사항, 현재 버전 및 지원되는 명령이 나열됩니다.

## 3단계. 환경 구성
{: #step3-configure-idt-env}

1. IBM ID를 사용하여 {{site.data.keyword.cloud_notm}}에 로그인하십시오. 여러 계정이 있는 경우 사용할 계정을 선택하도록 프롬프트가 표시됩니다. `-r` 플래그로 지역을 지정하지 않은 경우, 지역도 선택해야 합니다.
  ```
ibmcloud login
  ```
  {: codeblock}
  
  인증 정보가 거부되는 경우 연합 ID를 사용 중일 수 있습니다. 연합 ID로 로그인하려면 `--sso` 플래그를 사용하십시오. 자세한 사항은 [연합 ID로 로그인](/docs/iam/federated_id?topic=iam-federated_id#federated_id)을 참조하십시오.
  {: tip}

2. Cloud Foundry 서비스에 액세스하려면 Cloud Foundry 조직과 영역을 지정해야 합니다. 다음 명령을 실행하여 조직 및 영역을 대화식으로 식별할 수 있습니다.
  ```
  ibmcloud target --cf
  ```
  {: codeblock}

  또는 서비스가 속하는 조직 및 영역을 알고 있는 경우 다음 명령을 사용할 수 있습니다.
  ```
ibmcloud target -o <value> -s <value>
  ```
  {: codeblock}

## 다음 단계
{: #next-steps}

* 이제 첫 번째 앱을 개발하고 배치할 준비가 되었습니다. 자세한 정보는 [CLI를 사용하여 앱 작성 및 배치](/docs/apps?topic=creating-apps-create-deploy-app-cli#create-deploy-app-cli)를 참조하십시오.

* 새 {{site.data.keyword.cloud_notm}} CLI 릴리스에 대한 알림을 받을 수 있습니다. [{{site.data.keyword.cloud_notm}} CLI 릴리스 저장소](https://github.com/IBM-Cloud/ibm-cloud-cli-release/releases/){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")를 구독하십시오.
