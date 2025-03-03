---

copyright:
  years: 2016, 2019
lastupdated: "2019-05-21"

keywords: cli, bmscore, bmscore sdk, network request, ios network cli, android network cli, cordova network cli, mobile network request, mobile cli

subcollection: cloud-cli

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Fazendo uma solicitação de rede
{: #sdk-network-request}

Também é possível usar o SDK `BMSCore` para fazer solicitações de rede para qualquer recurso.

## Android
{: #request-android}

1. Certifique-se de que você tenha [importado o SDK do Cliente e o inicializado](/docs/cli/sdk?topic=cloud-cli-sdk_BMSClient#init-BMSClient-android) em seu aplicativo do Android.

2. Faça uma solicitação de rede.

	```Java
	String customResourceURL = "<your resource URL>";
	Request request = new Request(customResourceURL, "GET");

	ResponseListener listener = new ResponseListener() {
		@Override
		public void onSuccess(Response response) {
			Log.i("MyApp", "Response: " + response.getResponseText());
		}

		@Override
		public void onFailure(Response response, Throwable t, JSONObject extendedInfo) {
			Log.i("MyApp", "Request failed. Response: " + response.getResponseText() + ". Error: " + t.getLocalizedMessage());
		}
	};

	request.send(getApplicationContext(), listener);
	```
	{: codeblock}

A classe `Request` é uma maneira simples de fazer uma solicitação de HTTP e de obter a resposta após a solicitação ser concluída. Se você estiver fazendo download ou fazendo upload de arquivos grandes ou de grandes corpos de dados, será possível usar os métodos `Request`, `download` ou `upload`. Para monitorar o progresso do download ou do upload, crie um `ProgressListener` customizado e passe-o para os métodos `download` ou `upload`.

Para obter exemplos de uso completos, consulte no `BMSCore` GitHub [LEIA-ME](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo").


## iOS
{: #request-ios}

1. Certifique-se de que tenha [importado e inicializado o SDK do cliente](/docs/cli/sdk?topic=cloud-cli-sdk_BMSClient#init-BMSClient-ios) em seu app iOS.

2. Crie uma solicitação de rede.

	### Swift 3.0
	{: #ios-swift3 notoc}

	```Swift
	let customResourceURL = "<your resource URL>"
	let request = Request(url: customResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: Error?) in
  if error == nil {
			print ("Response: \(response?.responseText), no error")
		} else {
			print ("Error: \(error)")
		}
	}
	request.send(completionHandler: callBack)
	```
	{: codeblock}

	### Swift 2.2
	{: #ios-swift22 notoc}

	```Swift
	let customResourceURL = "<your resource URL>"
	let request = Request(url: customResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: NSError?) in
  if error == nil {
			print ("Response: \(response?.responseText), no error")
		} else {
			print ("Error: \(error)")
		}
	}
	request.send(completionHandler: callBack)
	```
	{: codeblock}

A classe `Request` é uma maneira simples de fazer uma solicitação de HTTP e de obter a resposta após a solicitação ser concluída. Se deseja mais flexibilidade e controle do que é possível obter com a classe `Request`, a classe `BMSURLSession` pode ser usada. Alguns recursos da classe `BMSURLSession` incluem monitoramento do progresso de uploads e pausa ou cancelamento de solicitações. Para obter as respostas, é possível escolher manipuladores de conclusão ou delegados.

A classe `BMSURLSession` está disponível somente para iOS.

Para obter exemplos de uso completos, consulte o [LEIA-ME](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window} do `BMSCore` GitHub ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo").

## Cordova
{: #request-cordova}

1. Certifique-se de que tenha [importado e inicializado o SDK do cliente](/docs/cli/sdk?topic=cloud-cli-sdk_BMSClient#init-BMSClient-cordova) em seu app Cordova.

2. Crie uma solicitação de rede.

	```Javascript
	var success = function(data) {
		console.log("success", data);
	}
	var failure = function(error)
		{console.log("failure", error);
	}
	var request = new BMSRequest("<your application route>", BMSRequest.GET);
	request.send(success, failure);
	```
	{: codeblock}
