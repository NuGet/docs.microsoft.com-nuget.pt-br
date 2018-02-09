---
title: Usando NuGet.Server para hospedar feeds do NuGet Feeds | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Como criar e hospedar um feed de pacote do NuGet em qualquer servidor que executa o IIS usando NuGet.Server, tornando os pacotes disponíveis por meio de HTTP e OData."
keywords: Feed do NuGet, Galeria do NuGet, feed de pacote remoto, NuGet.Server
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4cb3f04954fac1b4a39284be187776ab4a19b364
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
---
# <a name="nugetserver"></a>NuGet.Server

O NuGet.Server é um pacote fornecido pelo .NET Foundation que cria um aplicativo ASP.NET que pode hospedar um feed de pacote em qualquer servidor que executa o IIS. Em poucas palavras, o NuGet.Server disponibiliza uma pasta no servidor por meio de HTTP(S) (especificamente OData). É fácil de configurar e é melhor para cenários simples.

1. Crie um aplicativo Web ASP.NET vazio no Visual Studio e adicione o pacote do NuGet.Server a ele.
1. Configure a pasta `Packages` no aplicativo e adicione pacotes.
1. Implantar o aplicativo em um servidor adequado.

As seções a seguir abordam esse processo em detalhes usando o C#.

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>Criar e implantar um aplicativo Web ASP.NET com o NuGet.Server

1. No Visual Studio, selecione **Arquivo > Novo > Projeto**, defina a estrutura de destino para o .NET Framework 4.6 (veja abaixo), pesquise por “ASP.NET” e selecione o modelo de C# **Aplicativo Web ASP.NET (.NET Framework)**.

    ![Definindo o destino do .NET Framework 4.6](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Dê um nome adequado para o aplicativo *diferente* do NuGet.Server, selecione OK e, na próxima caixa de diálogo, escolha o modelo **Vazio** e clique em OK.

1. Clique com o botão direito do mouse no projeto, selecione **Gerenciar pacotes do NuGet** e, na interface do usuário do Gerenciador de Pacotes, pesquise e instale a versão mais recente do pacote do NuGet.Server se voltado para o .NET Framework 4.6. (Também é possível instalá-lo do Console do Gerenciador de Pacotes com `Install-Package NuGet.Server`.)

    ![Instalando o pacote do NuGet.Server](media/Hosting_02-NuGet.Server-Package.png)

    > [!Important]
    > Se seu aplicativo Web destina-se ao .NET Framework 4.5.2, você precisa instalar o NuGet Server **2.10.3** em vez disso.

1. Instalar o NuGet.Server converte o aplicativo Web vazio em uma origem de pacote. Ele cria uma pasta `Packages` no aplicativo e substitui `web.config` para incluir configurações adicionais (consulte os comentários no arquivo para obter detalhes).

1. Para disponibilizar esses pacotes no feed quando você publicar o aplicativo em um servidor, adicione seus arquivos `.nupkg` para a pasta `Packages` no Visual Studio e, em seguida, defina sua **Ação de build** para **Conteúdo** e **Copiar para diretório de saída** para **Sempre copiar**:

    ![Copiando pacotes para a pasta Pacotes no projeto](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. Execute o site localmente no Visual Studio (sem depuração, que é Ctrl + F5). A página inicial fornece as URLs do feed do pacote:

    ![A página inicial padrão de um aplicativo com NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. Clique em **aqui** na área descrita acima para ver o feed OData de pacotes.

1. Na primeira vez que você executar o aplicativo, o NuGet.Server reestrutura a pasta `Packages` para conter uma pasta para cada pacote. Isso corresponde ao [layout de armazenamento local](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduzido no NuGet 3.3 para melhorar o desempenho. Ao adicionar mais pacotes, continue seguindo esta estrutura.

1. Depois de testar sua implantação local, implante o aplicativo para qualquer outro site interno ou externo, conforme necessário.
1. Uma vez implantado no `http://<domain>`, a URL que você usa para a origem do pacote será `http://<domain>/nuget`.

## <a name="configuring-the-packages-folder"></a>Configurar a pasta Pacotes

Com o `NuGet.Server` 1.5 e posterior, é possível configurar a pasta de pacote mais especificamente usando o valor `appSetting/packagesPath` em `web.config`:

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath` pode ser um caminho absoluto ou virtual.

Quando o `packagesPath` for omitido ou deixado em branco, a pasta de pacotes é o `~/Packages` padrão.

## <a name="adding-packages-to-the-feed-externally"></a>Adicionar pacotes ao feed externamente

Quando um site do NuGet.Server está em execução, você pode adicionar ou excluir pacotes usando o nuget.exe fornecido para os quais você definiu um valor de chave de API em `web.config`.

Depois de instalar o pacote do NuGet.Server, o `web.config` contém um valor `appSetting/apiKey` vazio:

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

Quando `apiKey` for omitido ou estiver em branco, o push de pacotes para o feed está desabilitado.

Para habilitar essa capacidade, defina o `apiKey` para um valor (o ideal é uma senha forte) e adicione uma chave denominada `appSettings/requireApiKey` com o valor de `true`:

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

Se o servidor já está protegido ou você não exige uma chave de API (por exemplo, ao usar um servidor privado em uma rede de equipe local), é possível definir `requireApiKey` para `false`. Todos os usuários com acesso ao servidor poderão, então, efetuar push ou excluir pacotes.