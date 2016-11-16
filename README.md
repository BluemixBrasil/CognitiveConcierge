[![Apache 2](https://img.shields.io/badge/license-Apache2-blue.svg?style=flat)](https://www.apache.org/licenses/LICENSE-2.0)
![Bluemix Deployments](https://deployment-tracker.mybluemix.net/stats/f4ae263f304ffe32cbb17f3238c3ac86/badge.svg)

[![cognitive concierge video](http://img.youtube.com/vi/kQqE0hMg0Q8/0.jpg)](http://www.youtube.com/watch?v=kQqE0hMg0Q8 "Video Title")

# CognitiveConcierge
CognitiveConcierge é um exemplo de aplicativo Swift de ponta a ponta com um front-end iOS e um back-end Kitura Web Framework. Esta aplicação também demonstra como puxar um número de diferentes serviços Watson para o seu cliente Swift e aplicativos do lado do servidor via SDKs iOS do Watson Developer Cloud, incluindo conversação, texto para voz, fala para texto e as APIs Alchemy Language.

<img src="images/CC1.png" width="250"><img src="images/CC2.png" width="250"><img src="images/CC7.png" width="250">

## IBM Cloud Tools for Swift (ICT) Instruções
### Obtenha uma Google Places API Key para Web
1. Para este projeto, você precisará de uma Chave de API do Google Places para que o aplicativo possa acessar o texto de revisão que será enviado ao serviço da API da Alchemy para análise. As instruções para obter uma chave podem ser encontradas [aqui](https://developers.google.com/places/web-service/get-api-key).
2. Depois de ter uma chave de API, vá ao Google Developer's Console e ative a API do Google Places para iOS. Anote a chave da API para uso posterior em seu servidor e aplicativos iOS.

### Deploy do Servidor de Aplicação no Bluemix usando ICT.
1. Instale [IBM Cloud Tools for Swift] (http://cloudtools.bluemix.net/) para MacOS.
2. Depois de instalar o aplicativo, você pode abri-lo para começar.
3. Clique no botão Criar (+) para configurar um novo projeto e, em seguida, selecione o Aplicativo de Concierge Cognitivo.
5. Clique em Guardar ficheiros para computador local para clonar o projeto.
6. Assim que o projeto for clonado, abra o arquivo .xcodeproj que foi criado para você no ITC dentro do Local Server Repository. Edite o arquivo Configuration.swift que está em Sources/restaurant-recommendations/Configuration.swift com a sua própria chave de API do Google.

	<img src="images/xcodeproj.png" width="500">

7. Finalmente, você pode usar o ICT para fazer o deploy do servidor no Bluemix. Clique em Provision and Deploy Sample Server na parte de Cloud Runtimes.

	<img src="images/provision.png" width="500">

8. Dê um nome único ao seu Runtime, e clique em Next. Esse dploy para o Bluemix pode levar alguns minutos.

### Aponte a aplicação iOS para o Servidor de Aplicação
	1. Em ICT, certifique-se de que o campo "Connected to:" no aplicativo Cliente esteja apontado para a instância do servidor em execução no Bluemix. Você também pode apontar para o localhost para testes locais, mas você precisa estar executando uma instância local do aplicativo de servidor para que isso funcione.

### Atualiza o Serviço de Conversação
1. Uma vez que o ITC provisionar o Cloud Runtime, você deve ter uma instância do Serviço de Conversação no painel do Bluemix. Este Serviço permite que você adicione uma interface de idioma natural para seus aplicativos. Embora você possa criar uma árvore de conversação manualmente, fornecemos a conversação para esse aplicativo na pasta Resourcesno nível superior do projeto.
2. Em ICT, clique no ícone do Bluemix no Cloud Runtime para ir para a página "Detalhes do aplicativo" no Bluemix.

	<img src="images/cloud_runtime.png" width="500">

3. Selecione o Serviço CognitiveConcierge-Conversation em Conexões.

	<img src="images/conversation_service.png" width="500">

4. Role para baixo e selecione 'Launch Tool'.
5. Inicie sessão no Watson Conversation com o seu IBM ID e você será levado para a página 'Criar Espaço de Trabalho'. Selecione Importar e envie o arquivo .JSON (Resources/conversationWorkspace.json) que representa a conversação para este aplicativo.

	<img src="images/create_workspace.png" width="500">

6. Depois que a Conversa for criada, selecione o ícone Mais Opções e clique em Exibir Detalhes. Observe a ID do espaço de trabalho para uso em seu aplicativo iOS.

	<img src="images/more_options.png" width="500">

7. Abra o arquivo CognitiveConcierge.xcworkspace do ICT. Copie o WorkspaceID no arquivo CognitiveConcierge.plist.

	<img src="images/plist.png" width="500">

8. Nota: O Watson pode levar alguns minutos para treinar com base workspace de conversação que você carregou. Verifique se o Watson terminou o treinamento clicando no workspace da conversa, em Diálogo e, em seguida, no ícone de bate-papo no canto superior direito.  

	<img src="images/conversation_dialog.png" width="500">

    Assim você também pode experimentar a conversa e testar seu bot.
	
	<img src="images/conversation_testing.png" width="500">

### Execute o aplicativo iOS 
1. Instale o Cocoapods Dependency Manager no Terminal com o comando 'sudo gem install cocoapods'

2. Instale o Carthage Dependency Manager.  Baixe e execute o arquivo .pkg para a última release https://github.com/Carthage/Carthage/releases ou simplesmente execute 'brew update' seguido por 'brew install carthage'
3. Do Terminal, mude o diretório de trabalho para NomeDoSeuProjeto/CognitiveConcierge-iOS.
4. Execute os seguintes comandos para instalar as dependências necessárias:
  ```
  carthage update --platform iOS
  
  pod install
  ```
5. Abra o arquivo CognitiveConcierge.xcworkspace no Xcode 8 do seu ICT ou do seu terminal usando `open CognitiveConcierge.xcworkspace`
6. Digite suas credenciais para cada serviço necessário para executar o aplicativo no mesmo arquivo CognitiveConcierge.plist que você inseriu o workspaceID do serviço de conversação: `CognitiveConcierge-iOS / CognitiveConcierge / CognitiveConcierge.plist`. Encontre cada credencial retornando à página de detalhes do aplicativo a qual você pode acessar clicando no ícone do Bluemix no Cloud Runtime da ICT ou seguindo estas etapas:
    1. Va para o[Bluemix](https://new-console.ng.bluemix.net/#overview) e se assegure de que está na aba 'Console':

        <img src="images/console.png" width="500">

    2. Selecione 'All Items' na tela do console e clique no nome do aplicativo listado em Aplicativos do Cloud Foundry. A rota / URL fornecida ao lado do nome só o levará à página hospedada por seu aplicativo; Não à página que estamos procurando. Isso deve trazê-lo para a página do Bluemix que você viu anteriormente ao encontrar o serviço Conversation.

7. Clique em 'Runtime', e em 'Environment Variables' para acessar todas as credenciais de acesso de todos os serviços dentro de VCAP_Services para adicionar no arquivo 'CognitiveConcierge.plist'.

      <img src="images/envmt_variables.png" width="500">

8. Aperte o botão de Play no Xcode para fazer o build e executar o projeto num simulador, ou no seu iPhone!

## Privacy Notice
This Swift application includes code to track deployments to [IBM Bluemix](https://www.bluemix.net/) and other Cloud Foundry platforms. The following information is sent to a [Deployment Tracker](https://github.com/IBM-Bluemix/cf-deployment-tracker-service) service on each deployment:

* Swift project code version (if provided)
* Swift project repository URL
* Application Name (`application_name`)
* Space ID (`space_id`)
* Application Version (`application_version`)
* Application URIs (`application_uris`)
* Labels of bound services
* Number of instances for each bound service and associated plan information

This data is collected from the parameters of the `CloudFoundryDeploymentTracker`, the `VCAP_APPLICATION` and `VCAP_SERVICES` environment variables in IBM Bluemix and other Cloud Foundry platforms. This data is used by IBM to track metrics around deployments of sample applications to IBM Bluemix to measure the usefulness of our examples, so that we can continuously improve the content we offer to you. Only deployments of sample applications that include code to ping the Deployment Tracker service will be tracked.

### Disabling Deployment Tracking
Deployment tracking can be disabled by removing the following line from main.swift:
```
CloudFoundryDeploymentTracker(repositoryURL: "https://github.ibm.com/MIL/CognitiveConcierge", codeVersion: nil).track()

```
