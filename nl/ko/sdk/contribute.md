---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-29"

keywords: cli, contribute plug-in, sdk plug-in, cloud foundry cli, go environment, internationalization, ginkgo, govendor

subcollection: cloud-cli

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}

# SDK 플러그인에 대한 컨트리뷰션
{: #contribute}

다음 가이드라인에 따라 {{site.data.keyword.cloud}} CLI SDK 플러그인에 컨트리뷰션하십시오.

## 개발 환경 설정
{: #dev-env}

* Cloud Foundry [CLI ](https://github.com/cloudfoundry/cli/releases){: new_window} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘").

   Cloud Foundry CLI는 필수는 아니지만 터미널에서 {{site.data.keyword.cloud_notm}}에 액세스하도록 도와줍니다.

   Cloud Foundry CLI에 대한 자세한 정보는 [문서](/docs/cli?topic=cloud-cli-cf#cf)를 참조하십시오.

* {{site.data.keyword.cloud_notm}} [CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).

   이 플러그인은 {{site.data.keyword.cloud_notm}} CLI에 추가되며 명령행에서 {{site.data.keyword.cloud_notm}}에 액세스하기 위한 유용한 리소스를 제공합니다.

* [개발 환경 ](https://golang.org/doc/code.html){: new_window} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")으로 이동하십시오.

   Go는 패키지 위치에 엄격하게 처리되므로 소스를 `$GOPATH` 디렉토리 구조 내에 정의해야 합니다. `$GOPATH` 및 `$GOROOT` 변수를 정의하고 `$GOPATH/bin`을 `$PATH` 환경 변수에 포함해야 합니다. `~/.bash_profile` 구성 파일(Mac)을 편집하여 이러한 변경을 수행할 수 있습니다.

   ```
   ### SET Go's GOPATH and GOROOT                                                                                                                   
   export GOPATH=$HOME/Development/go                                                                                                               
   export GOROOT=/usr/local/opt/go/libexec                                                                                                          
   export PATH=$PATH:$GOPATH/bin
   ```
   {: codeblock}

* 종속성 관리자: [`govendor `](https://github.com/kardianos/govendor){: new_window} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")

   `govendor` 도구는 Go 종속 항목을 작성하고 관리합니다. 공급업체 디렉토리를 업데이트할 계획이 아니라면 이 도구가 필요하지 않습니다.

   * 다음 명령을 사용하여 이를 설치하십시오.

      ```
      go get -u github.com/kardianos/govendor
      ```
      {: codeblock}

   * 다음 명령을 사용하여 프로젝트 디렉토리에서 `govendor`를 초기화하십시오.

      ```
      govendor init
      ```
      {: codeblock}

   * 다음 명령을 사용하여 `$GOPATH`의 종속 항목을 공급업체 디렉토리에 추가하십시오.

      ```
      govendor add +local
      ```
      {: codeblock}

* BDD 테스트 프레임워크: [Ginkgo ](http://onsi.github.io/ginkgo/){: new_window} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")

테스트 프레임워크는 Go의 BDD 테스트 프레임워크인 Ginkgo를 기반으로 하며 Ginkgo의 매처(matcher) 및 어설션 라이브러리인 [`gomega`](http://onsi.github.io/gomega/){: new_window} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")와 함께 사용됩니다.

   * 다음 명령을 사용하여 `ginkgo`를 설치하십시오.

      ```
      go get -u github.com/onsi/ginkgo/ginkgo
      ```
      {: codeblock}

   * 다음 명령을 사용하여 `gomega`를 설치하십시오.

      ```
      go get -u github.com/onsi/gomega
      ```
      {: codeblock}

   * 다음 명령을 사용하여 단위 테스트를 실행하십시오.

      ```
ginkgo -r
      ```
      {: codeblock}

      * 코드 적용 범위를 추가하려면 명령의 끝에 `-cover`를 추가하십시오.

   * 익숙한 HTML 양식의 코드 적용 범위를 얻으려면 다음 명령을 사용하십시오.

      ```
      go tool -html={package}.coverprofile
      ```
      {: codeblock}

      * `.coverprofile` 파일이 있는 디렉토리로 이동합니다.

* 다국어 지원: [go-i18n](https://github.com/nicksnyder/go-i18n){: new_window} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘") 및 [go-bindata](https://github.com/jteeuwen/go-bindata){: new_window} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")

다국어 지원은 Go 애플리케이션을 여러 언어로 번역하도록 지원하는 명령행 도구이자 패키지인 `go-i18n`을 기반으로 합니다. 번역 번들은 입력 파일을 관리 가능한 Go 소스 코드로 변환하는 `go-bindata` 명령으로 사전 처리됩니다.

   * 다음 명령을 사용하여 `go-i18n`을 설치하십시오.

      ```
      go get -u github.com/nicksnyder/go-i18n/goi18n
      ```
      {: codeblock}

   * 다음 명령을 사용하여 `go-bindata`를 설치하십시오.

      ```
      go get -u github/com/jteeuwen/go-bindata/go-bindata
      ```
      {: codeblock}

* 디버깅: [delve ](https://github.com/go-delve/delve){: new_window} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")

Delve는 Go 프로그래밍 언어를 위한 디버거로 [Visual Studio 코드 ](https://code.visualstudio.com/){: new_window} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")에서 사용됩니다.

   * 다음 명령을 사용하여 `delve`를 설치하십시오.

      ```
      go get -u github.com/derekparker/delve/cmd/dlv
      ```
      {: codeblock}

      * Mac OS의 경우 [지시사항 ](http://blog.ralch.com/tutorial/golang-debug-with-delve/){: new_window} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")에 따라 필수 자체 서명 인증서를 작성하십시오.


## 필수 런타임 라이브러리
{: #runtime-libs}

필수 런타임 라이브러리는 Go에서 강력한 종속성 관리자를 제공하지 않으므로 안정성을 보장하기 위해 `vendor` 디렉토리 아래에서 관리되고 Git 저장소로 커미트됩니다.

### 런타임 종속 항목
{: #runtime-dependencies}

중첩된 종속 항목은 나열되지 않습니다.

* [github.ibm.com/Bluemix/bluemix-cli-sdk ](https://github.ibm.com/Bluemix/bluemix-cli-sdk){: new_window} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")

   {{site.data.keyword.cloud_notm}} CLI 플러그인을 개발하기 위한 인프라를 제공하는 {{site.data.keyword.cloud_notm}} CLI 플러그인 SDK.

* [github.com/urfave/cli ](https://github.com/urfave/cli){: new_window} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")

   이 패키지는 Go에서 명령행 앱을 빌드하기 위한 인프라를 제공합니다. {{site.data.keyword.cloud_notm}} CLI 플러그인은 이 라이브러리의 이전 버전(github.com/codegangsta/cli)에 종속적입니다.

* [github.com/asaskevich/govalidator ](https://github.com/asaskevich/govalidator){: new_window} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")

   이 패키지는 문자열, 구조체 및 콜렉션을 위한 다수의 유효성 검증기 및 무결 처리기를 제공합니다. 사용자 고유 유효성 검증기를 구현하는 대신 이 패키지를 사용하십시오.

* [github.com/parnurzeal/gorequest ](https://github.com/parnurzeal/gorequest){: new_window} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")

   이 패키지는 HTTP 요청 및 응답을 처리하는 데 도움을 주는 단순한 HTTP 클라이언트를 구현합니다.

* [github.com/briandowns/spinner ](https://github.com/briandowns/spinner){: new_window} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")

   이 패키지는 SDK 생성과 같이 긴 오퍼레이션이 처리되는 동안 사용자 피드백을 제공하기 위한 CLI 스피너를 구현합니다.

* [github.com/cloudfoundry-attic/jibber_jabber ](https://github.com/cloudfoundry-attic/jibber_jabber){: new_window} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")

   이 패키지는 운영 체제의 현재 언어를 발견하는 데 사용됩니다.

## 저장소 복제
{: #clone-repo}

이 저장소는 Go의 우수 사례를 따르는 `govendor`의 작동 방식으로 인해 Go의 [디렉토리 구조 ](https://golang.org/doc/code.html){: new_window} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")로 복제되어야 합니다.

* 완전한 패키지 이름을 통해 내부 종속 항목을 가져오십시오.

   ```
   import (
      ...
      "github.ibm.com/bluemix-mobile-services/bmd-codegen-sdkgen-cli-plugin/plugin"
   )
   ```
   {: codeblock}

* 저장소를 복제하십시오.

   ```
   mkdir -p $GOPATH/src/github.ibm.com/bluemix-mobile-services
   cd $GOPATH/src/github.ibm.com/bluemix-mobile-services
   git clone https://github.ibm.com/bluemix-mobile-services/bmd-codegen-sdkgen-cli-plugin.git -b compute
   ```
   {: codeblock}


## 플러그인 빌드, 테스트 및 설치
{: #build-plug-in}

다음 명령 중 하나를 선택하여 플러그인을 빌드하십시오.
```
cd $GOPATH/src/github.ibm.com/bluemix-mobile-services/bmd-codegen-sdkgen-cli-plugin
go build main.go
```
{: codeblock}

```
cd $GOPATH/src/github.ibm.com/bluemix-mobile-services/bmd-codegen-sdkgen-cli-plugin
sh bin/build.sh
```
{: codeblock}

빌드 스크립트는 플러그인을 {{site.data.keyword.Bluemix_notm}} CLI에도 설치합니다.
{: note}

다음 명령 중 하나를 선택하여 플러그인을 테스트하십시오.
```
ginkgo -r
```
{: codeblock}

```
go test ./plugin/...
```
{: codeblock}

단위 테스트 및 적용 범위로 통합 테스트를 실행하십시오.
```
sh bin/testAll.sh
```
{: codeblock}

독립형 CLI로 플러그인을 실행하십시오.
```
./main
```
{: codeblock}

다음 명령 중 하나를 선택하여 {{site.data.keyword.cloud_notm}} CLI로 플러그인을 설치 및 호출하십시오.
```
ibmcloud plugin install main
ibmcloud help sdk
```
{: codeblock}

```
sh bin/build.sh
```
{: codeblock}
