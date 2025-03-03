---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-21"

keywords: cli, docker, docker container, ibmcloud docker, docker run, docker pull, ibmcloud cli, dockerfile, ibmcloud login

subcollection: cloud-cli

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# Docker 컨테이너에서 {{site.data.keyword.dev_cli_notm}} 사용
{: #using-idt-from-docker}

{{site.data.keyword.dev_cli_notm}} Docker 컨테이너를 사용하여 {{site.data.keyword.cloud}} CLI 및 다음 도구를 사용할 수 있습니다.

* `Git`
* `Helm`
* `kubectl`
* `curl`
* {{site.data.keyword.dev_cli_notm}} 플러그인
* {{site.data.keyword.IBM_notm}} {{site.data.keyword.openwhisk_short}} 플러그인
* {{site.data.keyword.registrylong_notm}} 플러그인
* {{site.data.keyword.containerlong_notm}} 플러그인
* `sdk-gen` 플러그인

## 시작하기 전에
{: #idt-docker-prereq}

[{{site.data.keyword.cloud_notm}} 계정](https://{DomainName}/login){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")이 필요하며 다음 단계를 수행하기 전에 안정된 최신 Docker 버전을 설치해야 합니다.

## 1단계. Docker 허브에서 Docker 이미지를 가져오십시오.
{: #step1-pull-docker-image}

```
docker pull ibmcom/ibm-cloud-developer-tools-amd64
```
{: codeblock}

## 2단계. Docker 컨테이너를 시작하십시오.
{: #step2-start-docker}

다음 명령을 사용하여 {{site.data.keyword.dev_cli_notm}} Docker 컨테이너를 시작하십시오.

```
docker run -ti ibmcom/ibm-cloud-developer-tools-amd64
```
{: codeblock}

## 3단계. IBM ID를 사용하여 {{site.data.keyword.cloud_notm}}에 로그인하십시오.
{: #step3-ibmcloud-login}

```
ibmcloud login
```
{: codeblock}

인증 정보가 거부되는 경우 연합 ID를 사용 중일 수 있습니다. 자세한 사항은 [연합 ID로 로그인](/docs/iam?topic=iam-federated_id#federated_id)을 참조하십시오.
{: tip}

{{site.data.keyword.dev_cli_notm}} CLI 플러그인은 두 개의 컨테이너를 사용하여 애플리케이션 빌드와 테스트를 용이하게 합니다. 첫 번째는 tools 컨테이너로서 앱 빌드와 테스트에 필요한 유틸리티를 포함합니다. 이 컨테이너를 위한 `Dockerfile`은 [`dockerfile-tools`](/docs/cli/idt?topic=cloud-cli-idt-cli#command-parameters) 매개변수로 정의됩니다. 특정 런타임의 개발에 일반적으로 사용되는 도구를 포함하고 있으므로 개발 컨테이너로 생각할 수 있습니다.

두 번째 컨테이너는 클라우드에 배치될 때 앱의 실제 런타임 환경을 근접하게 모방하는 run 컨테이너입니다. 이 컨테이너는 예를 들어 {{site.data.keyword.cloud_notm}}에서 사용하기 위해 배치하는 데 적합한 양식으로 되어 있습니다. 결과적으로 앱을 시작하는 시작점이 정의됩니다. {{site.data.keyword.dev_cli_notm}} CLI 플러그인 CLI를 통해 앱을 실행하도록 선택하면 이 컨테이너가 사용됩니다. 이 컨테이너를 위한 `Dockerfile`은 [`dockerfile-run`](/docs/cli/idt?topic=cloud-cli-idt-cli#run-parameters) 매개변수로 정의됩니다.

이제 {{site.data.keyword.dev_cli_notm}}를 사용하여 {{site.data.keyword.cloud_notm}} 리소스를 관리하고 앱을 개발 및 배치할 준비가 되었습니다.
