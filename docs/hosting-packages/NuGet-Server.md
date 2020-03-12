---
title: Usando NuGet.Server para hospedar feeds do NuGet
description: Como criar e hospedar um feed de pacote do NuGet em qualquer servidor que executa o IIS usando NuGet.Server, tornando os pacotes disponíveis por meio de HTTP e OData.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 098375b2bba13675ba5d80a27e0226dc2ee39e77
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/10/2020
ms.locfileid: "79059502"
---
# <a name="nugetserver"></a>NuGet.Server

O NuGet.Server é um pacote fornecido pelo .NET Foundation que cria um aplicativo ASP.NET que pode hospedar um feed de pacote em qualquer servidor que executa o IIS. Em poucas palavras, o NuGet.Server disponibiliza uma pasta no servidor por meio de HTTP(S) (especificamente OData). É fácil de configurar e é melhor para cenários simples.

1. Crie um aplicativo Web ASP.NET vazio no Visual Studio e adicione o pacote do NuGet.Server a ele.
1. Configure a pasta `Packages` no aplicativo e adicione pacotes.
1. Implantar o aplicativo em um servidor adequado.

As seções a seguir abordam esse processo em detalhes usando o C#.

Caso tenha outras dúvidas sobre o NuGet.Server, crie um problema no [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>Criar e implantar um aplicativo Web ASP.NET com o NuGet.Server

1. No Visual Studio, selecione **arquivo > novo projeto de >** , pesquise "aplicativo Web ASP.NET (.NET Framework)", selecione o modelo correspondente para C#.

    ![Selecione o modelo de projeto Web .NET Framework](media/Hosting_00-NuGet.Server-ProjectType.png)

1. Defina a **estrutura** como ".NET Framework 4,6".

    ![Definindo a estrutura de destino para um novo projeto](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Dê um nome adequado ao aplicativo *diferente* de NuGet.Server, selecione OK e, na próxima caixa de diálogo, selecione o modelo **Vazio** e selecione **OK**.

    ![Selecione o projeto Web vazio](media/Hosting_02-NuGet.Server-Empty.png)

1. Clique com o botão direito do mouse no projeto e escolha **Gerenciar Pacotes NuGet**.

1. Na interface do usuário do Gerenciador de Pacotes, selecione a guia **Procurar** e, em seguida, pesquise e instale a versão mais recente do pacote NuGet.Server se você estiver direcionando para o .NET Framework 4.6. (Você também pode instalá-lo no console do Gerenciador de pacotes com o `Install-Package NuGet.Server`.) Aceite os termos de licença, se solicitado.

    ![Instalando o pacote do NuGet.Server](media/Hosting_03-NuGet.Server-Package.png)

1. Instalar o NuGet.Server converte o aplicativo Web vazio em uma origem de pacote. Ele instala uma variedade de outros pacotes, cria uma pasta `Packages` no aplicativo e modifica `web.config` para incluir as configurações adicionais (veja os comentários no arquivo para obter detalhes).

    > [!Important]
    > Inspecione cuidadosamente `web.config` depois que o pacote NuGet.Server tiver concluído as modificações desse arquivo. O NuGet.Server talvez não substituirá os elementos existentes, mas criará elementos duplicados. Essas duplicatas provocarão um "Erro Interno do Servidor" quando você tentar executar o projeto mais tarde. Por exemplo, se o seu `web.config` contiver `<compilation debug="true" targetFramework="4.5.2" />` antes de instalar o NuGet.Server, o pacote não o substituirá, mas sim inserirá um segundo `<compilation debug="true" targetFramework="4.6" />`. Nesse caso, exclua o elemento com a versão mais antiga da estrutura.

1. Execute o site localmente no Visual Studio (usando **Depurar > Iniciar sem Depurar** ou Ctrl + F5). A home page fornece as URLs do feed do pacote, conforme mostrado abaixo. Se você encontrar erros, inspecione atentamente sua `web.config` em busca de elementos duplicados, conforme observado anteriormente.

    ![A página inicial padrão de um aplicativo com NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1.  Na primeira vez que você executar o aplicativo, o NuGet.Server reestrutura a pasta `Packages` para conter uma pasta para cada pacote. Isso corresponde ao [layout de armazenamento local](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduzido no NuGet 3.3 para melhorar o desempenho. Ao adicionar mais pacotes, continue seguindo esta estrutura.

1. Depois de testar sua implantação local, implante o aplicativo para qualquer outro site interno ou externo, conforme necessário.

1. Uma vez implantado no `http://<domain>`, a URL que você usa para a origem do pacote será `http://<domain>/nuget`.

## <a name="adding-packages-to-the-feed-externally"></a>Adicionar pacotes ao feed externamente

Quando um site do NuGet.Server está em execução, você pode adicionar pacotes usando o comando [nuget push](../reference/cli-reference/cli-ref-push.md), desde que você defina um valor de chave de API em `web.config`.

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

Se o servidor já está protegido ou você não exige uma chave de API (por exemplo, ao usar um servidor privado em uma rede de equipe local), é possível definir `requireApiKey` para `false`. Todos os usuários com acesso ao servidor poderão efetuar push dos pacotes.

A partir do NuGet. Server 3.0.0, a URL para envio de pacotes foi alterada para `http://<domain>/nuget`. Antes da versão 3.0.0, a URL de push foi `http://<domain>/api/v2/package`.

Com o NuGet 3.2.1 e mais recente, essa URL herdada `/api/v2/package` é habilitada além de `/nuget` por padrão por meio da opção `enableLegacyPushRoute: true` em sua configuração de inicialização (`NuGetODataConfig.cs` por padrão). Observe que esse recurso não funciona quando vários feeds são hospedados no mesmo projeto.

## <a name="removing-packages-from-the-feed"></a>Removendo pacotes do feed

Com o NuGet.Server, o comando [nuget delete](../reference/cli-reference/cli-ref-delete.md) remove um pacote do repositório, desde que você inclua a chave de API com o comentário.

Se, em vez disso, você desejar alterar o comportamento para remover o pacote da lista (deixando-o disponível para a restauração de pacote), altere a chave `enableDelisting` em `web.config` para true.

## <a name="configuring-the-packages-folder"></a>Configurar a pasta Pacotes

Com o `NuGet.Server` 1,5 e posterior, você pode personalizar a pasta do pacote usando o valor de `appSettings/packagesPath` no `web.config`:

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath` pode ser um caminho absoluto ou virtual.

Quando o `packagesPath` for omitido ou deixado em branco, a pasta de pacotes é o `~/Packages` padrão.

## <a name="making-packages-available-when-you-publish-the-web-app"></a>Disponibilizando pacotes quando você publica o aplicativo Web

Para disponibilizar esses pacotes no feed quando você publicar o aplicativo em um servidor, adicione os arquivos `.nupkg` à pasta `Packages` no Visual Studio e, em seguida, defina a **Ação de Build** deles como **Conteúdo** e **Copiar para Diretório de Saída** como **Sempre copiar**:

![Copiando pacotes para a pasta Pacotes no projeto](media/Hosting_05-NuGet.Server-Package-Folder.png)

## <a name="release-notes"></a>Notas de Versão

As notas de versão do NuGet. Server estão disponíveis na [página de versão do GitHub](https://github.com/NuGet/NuGet.Server/releases).
Isso inclui detalhes sobre correções de bugs e novos recursos que são adicionados.

## <a name="nugetserver-support"></a>Suporte do NuGet.Server

Para obter ajuda adicional sobre o uso do NuGet.Server, crie um problema no [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).
