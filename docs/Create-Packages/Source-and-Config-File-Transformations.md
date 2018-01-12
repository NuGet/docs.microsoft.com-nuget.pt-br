---
title: "Transformações de origem e arquivo de configuração para pacotes do NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 4/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 20991d69-9e2e-4881-bbf2-96ae634e1872
description: "Detalhes sobre a capacidade de pacotes do NuGet transformarem arquivos de código-fonte e da configuração (XML) quando instalado."
keywords: "Instalação de pacote do NuGet, transformações de pacote do NuGet, modificando arquivos de configuração, modificando o código-fonte"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: 89a55716ccbc9043cfce4c7f38ec8ab9a0e2f768
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="transforming-source-code-and-configuration-files"></a>Transformando o código-fonte e os arquivos de configuração

Para projetos que usam `packages.config` ou `project.json`, o NuGet dá suporte à capacidade de fazer as transformações no código-fonte e nos arquivos de configuração nos tempos de instalação e desinstalação de pacote.

> [!Note]
> Transformações de arquivo de origem e de configuração não são aplicadas quando um pacote é instalado em um projeto que usa [Referências de pacote em arquivos de projeto](../Consume-Packages/Package-References-in-Project-Files.md). 

Uma **transformação de código-fonte** se aplica à substituição de token unidirecional para arquivos na pasta `content` do pacote quando este for instalado, em que os tokens se referem às [propriedades do projeto](/dotnet/api/vslangproj.projectproperties?redirectedfrom=MSDN&view=visualstudiosdk-2017#properties_) do Visual Studio. Isso permite inserir um arquivo de namespace de projeto ou personalizar código que geralmente iria para `global.asax` em um projeto do ASP.NET.

Uma **transformação do arquivo de configuração** permite que você modifique os arquivos que já existem em um projeto de destino, como `web.config` e `app.config`. Por exemplo, seu pacote pode ser necessário para adicionar um item à seção `modules` no arquivo de configuração. Essa transformação são feitas incluindo arquivos especiais no pacote que descreve as seções a serem adicionadas aos arquivos de configuração. Quando um pacote é desinstalado, essas mesmas alterações são revertidas, tornando esta uma transformação bidirecional.

## <a name="specifying-source-code-transformations"></a>Especificar as transformações do código-fonte

1. Arquivos do pacote que você deseja inserir no projeto devem estar localizados dentro da pasta `content` do pacote. Por exemplo, se você quiser que um arquivo chamado `ContosoData.cs` seja instalado em uma pasta `Models` do projeto de destino, ele deverá estar dentro da pasta `content\Models` no pacote.

1. Para instruir o NuGet a aplicar a substituição de token no momento da instalação, acrescente `.pp` ao nome do arquivo de código-fonte. Após a instalação, o arquivo não terá a extensão `.pp`.

    Por exemplo, para realizar transformações em `ContosoData.cs`, nomeie o arquivo no pacote `ContosoData.cs.pp`. Após a instalação, ele será exibido como `ContosoData.cs`.

1. No arquivo de código-fonte, use tokens que não diferenciam maiúsculas e minúsculas no formato `$token$` para indicar os valores que o NuGet deve substituir com as propriedades do projeto:

    ```cs
    namespace $rootnamespace$.Models
    {
        public struct CategoryInfo
        {
            public string categoryid;
            public string description;
            public string htmlUrl;
            public string rssUrl;
            public string title;
        }
    }
    ```

    Após a instalação, o NuGet substitui `$rootnamespace$` por `Fabrikam`, considerando o projeto de destino cujo namespace da raiz é `Fabrikam`.

O token `$rootnamespace$` é a propriedade de projeto mais usada; todas as outras são listadas na documentação [Propriedades do projeto](/dotnet/api/vslangproj.projectproperties?redirectedfrom=MSDN&view=visualstudiosdk-2017#properties_) no MSDN. Lembre-se, obviamente, algumas propriedades podem ser específicas ao tipo de projeto.

## <a name="specifying-config-file-transformations"></a>Especificar as transformações do arquivo de configuração

Conforme descrito nas seções a seguir, as transformações do arquivo de configuração podem ser feitas de duas maneiras:

- Inclua os arquivos `app.config.transform` e `web.config.transform` na pasta `content` do seu pacote, em que a extensão `.transform` diz ao NuGet que esses arquivos contêm o XML para serem mesclados com os arquivos de configuração existentes quando o pacote é instalado. Quando um pacote é desinstalado, esse mesmo XML é removido.
- (NuGet 2.6 e posterior) Inclua os arquivos `app.config.install.xdt` e `web.config.install.xdt` na pasta `content` do seu pacote usando [sintaxe XDT](https://msdn.microsoft.com/library/dd465326.aspx) para descrever as alterações desejadas. Com essa opção, também é possível incluir um arquivo `.uninstall.xdt` para reverter as alterações quando o pacote é removido de um projeto.

> [!Note]
> As transformações não são aplicadas a arquivos `.config` referenciados como um link no Visual Studio.

A vantagem de usar o XDT é que, em vez de simplesmente mesclar dois arquivos estáticos, ele fornece uma sintaxe para manipular a estrutura de um XML DOM usando correspondência de elemento e atributo com total suporte do XPath. O XDT pode então adicionar, atualizar ou remover os elementos, colocar novos elementos em um local específico ou substituir/remover elementos (incluindo nós filho). Isso simplifica a criação de transformações de desinstalação que retornam todas as transformações durante a instalação do pacote.

### <a name="xml-transforms"></a>Transformações XML

Os `app.config.transform` e `web.config.transform` na pasta `content` de um pacote contém apenas os elementos para mesclar os arquivos `app.config` e `web.config` existentes do projeto.

Por exemplo, suponha que o projeto inicialmente contém o conteúdo a seguir em `web.config`:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    <system.webServer>
</configuration>
```

Para adicionar um elemento `MyNuModule` à seção `modules` durante a instalação do pacote, crie um arquivo `web.config.transform` na pasta `content` do pacote que se assemelhará a esta:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    <system.webServer>
</configuration>
```

Depois que o NuGet instala o pacote, `web.config` será exibido da seguinte maneira:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    <system.webServer>
</configuration>
```

Observe que o NuGet não substituiu a seção `modules`, ele só mesclou a nova entrada com ele adicionando somente novos elementos e atributos. O NuGet não alterará nenhum atributo ou elemento existente.

Quando o pacote é desinstalado, o NuGet examinará os arquivos `.transform` novamente e remove os elementos que ele contém dos arquivos `.config` apropriados. Observe que esse processo não afetará as linhas no arquivo `.config` que podem ser modificadas após a instalação do pacote.

Como um exemplo mais amplo, o pacote [Módulos e manipuladores de log de erros para ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) adiciona várias entradas a `web.config`, que são removidas novamente quando um pacote é desinstalado.

Para examinar seu arquivo `web.config.transform`, baixe o pacote ELMAH do link acima, altere a extensão do pacote de `.nupkg` para `.zip` e abra `content\web.config.transform` nesse arquivo ZIP.

Para ver o efeito de instalação e desinstalação do pacote, crie um novo projeto do ASP.NET no Visual Studio (o modelo está em **Visual C# > Web** na caixa de diálogo Novo Projeto) e selecione um aplicativo ASP.NET vazio. Abra `web.config` para ver seu estado inicial. Em seguida, clique com botão direito do mouse no projeto, selecione **Gerenciar pacotes do NuGet**, procurar ELMAH no nuget.org e instalar a versão mais recente. Observe todas as alterações em `web.config`. Agora, desinstale o pacote e você verá o `web.config` reverter para seu estado anterior.

### <a name="xdt-transforms"></a>Transformações XDT

Com o NuGet 2.6 e posterior, você pode modificar os arquivos de configuração usando a [sintaxe XDT](https://msdn.microsoft.com/library/dd465326.aspx). Você também pode fazer com que o NuGet substitua os tokens pelas [Propriedades do projeto](/dotnet/api/vslangproj.projectproperties?redirectedfrom=MSDN&view=visualstudiosdk-2017#properties_) incluindo o nome da propriedade dentro dos delimitadores `$`(não diferencia maiúsculas de minúsculas).

Por exemplo, o arquivo `app.config.install.xdt` a seguir inserirá um elemento `appSettings` em `app.config` que contém os valores `FullPath`, `FileName` e `ActiveConfigurationSettings` valores do projeto:

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <appSettings xdt:Transform="Insert">
        <add key="FullPath" value="$FullPath$" />
        <add key="FileName" value="$filename$" />
        <add key="ActiveConfigurationSettings " value="$ActiveConfigurationSettings$" />
    </appSettings>
</configuration>
```

Para ver outro exemplo, considere que o projeto inicialmente tem o conteúdo a seguir em `web.config`:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    <system.webServer>
</configuration>
```

Para adicionar um elemento `MyNuModule` à seção `modules` durante a instalação de pacotes, o `web.config.install.xdt` do pacote poderia conter o seguinte:

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" xdt:Transform="Insert" />
        </modules>
    </system.webServer>
</configuration>
```

Depois de instalar o pacote, `web.config` se parecerá com o seguinte:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    <system.webServer>
</configuration>
```

Para remover apenas o elemento `MyNuModule` durante a desinstalação do pacote, o arquivo `web.config.uninstall.xdt` deve conter o seguinte:

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" xdt:Transform="Remove" xdt:Locator="Match(name)" />
        </modules>
    </system.webServer>
</configuration>
```
