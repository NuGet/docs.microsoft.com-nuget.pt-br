---
title: Transformações de arquivos de origem e de configuração para pacotes do NuGet
description: Detalhes sobre a capacidade de pacotes do NuGet transformarem arquivos de código-fonte e da configuração (XML) quando instalado.
author: JonDouglas
ms.author: jodou
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 76c589b5ad034127675fb2bbf79ea97992883ebe
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859103"
---
# <a name="transforming-source-code-and-configuration-files"></a>Transformando o código-fonte e os arquivos de configuração

Uma **transformação de código-fonte** aplicará a substituição de token unidirecional aos arquivos na pasta `content` ou `contentFiles` do pacote (`content` para clientes usando `packages.config` e `contentFiles` para `PackageReference`) quando o pacote estiver instalado e quando os tokens fizerem referência às [propriedades do projeto](/dotnet/api/vslangproj.projectproperties) do Visual Studio. Isso permite inserir um arquivo de namespace de projeto ou personalizar código que geralmente iria para `global.asax` em um projeto do ASP.NET.

Uma **transformação do arquivo de configuração** permite que você modifique os arquivos que já existem em um projeto de destino, como `web.config` e `app.config`. Por exemplo, seu pacote pode ser necessário para adicionar um item à seção `modules` no arquivo de configuração. Essa transformação são feitas incluindo arquivos especiais no pacote que descreve as seções a serem adicionadas aos arquivos de configuração. Quando um pacote é desinstalado, essas mesmas alterações são revertidas, tornando esta uma transformação bidirecional.

## <a name="specifying-source-code-transformations"></a>Especificar as transformações do código-fonte

1. Os arquivos do pacote que você deseja inserir no projeto devem estar localizados nas pastas `content` e `contentFiles` do pacote. Por exemplo, se você desejar que um arquivo chamado `ContosoData.cs` seja instalado em uma pasta `Models` do projeto de destino, ele precisará estar nas pastas `content\Models` e `contentFiles\{lang}\{tfm}\Models` no pacote.

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

O token `$rootnamespace$` é a propriedade de projeto mais usada; todas as outras são listadas nas [propriedades do projeto](/dotnet/api/vslangproj.projectproperties). Lembre-se, obviamente, algumas propriedades podem ser específicas ao tipo de projeto.

## <a name="specifying-config-file-transformations"></a>Especificar as transformações do arquivo de configuração

Conforme descrito nas seções a seguir, as transformações do arquivo de configuração podem ser feitas de duas maneiras:

- Inclua os arquivos `app.config.transform` e `web.config.transform` na pasta `content` do seu pacote, em que a extensão `.transform` diz ao NuGet que esses arquivos contêm o XML para serem mesclados com os arquivos de configuração existentes quando o pacote é instalado. Quando um pacote é desinstalado, esse mesmo XML é removido.
- Inclua os arquivos `app.config.install.xdt` e `web.config.install.xdt` na pasta `content` do pacote usando [sintaxe XDT](/previous-versions/aspnet/dd465326(v=vs.110)) para descrever as alterações desejadas. Com essa opção, também é possível incluir um arquivo `.uninstall.xdt` para reverter as alterações quando o pacote é removido de um projeto.

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
    </system.webServer>
</configuration>
```

Para adicionar um elemento `MyNuModule` à seção `modules` durante a instalação do pacote, crie um arquivo `web.config.transform` na pasta `content` do pacote que se assemelhará a esta:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
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
    </system.webServer>
</configuration>
```

Observe que o NuGet não substituiu a seção `modules`, ele só mesclou a nova entrada com ele adicionando somente novos elementos e atributos. O NuGet não alterará nenhum atributo ou elemento existente.

Quando o pacote é desinstalado, o NuGet examinará os arquivos `.transform` novamente e remove os elementos que ele contém dos arquivos `.config` apropriados. Observe que esse processo não afetará as linhas no arquivo `.config` que podem ser modificadas após a instalação do pacote.

Como um exemplo mais amplo, o pacote [Módulos e manipuladores de log de erros para ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) adiciona várias entradas a `web.config`, que são removidas novamente quando um pacote é desinstalado.

Para examinar seu arquivo `web.config.transform`, baixe o pacote ELMAH do link acima, altere a extensão do pacote de `.nupkg` para `.zip` e abra `content\web.config.transform` nesse arquivo ZIP.

Para ver o efeito de instalação e desinstalação do pacote, crie um novo projeto do ASP.NET no Visual Studio (o modelo está em **Visual C# > Web** na caixa de diálogo Novo Projeto) e selecione um aplicativo ASP.NET vazio. Abra `web.config` para ver seu estado inicial. Em seguida, clique com botão direito do mouse no projeto, selecione **Gerenciar pacotes do NuGet**, procurar ELMAH no nuget.org e instalar a versão mais recente. Observe todas as alterações em `web.config`. Agora, desinstale o pacote e você verá o `web.config` reverter para seu estado anterior.

### <a name="xdt-transforms"></a>Transformações XDT

> [!Note]
> Conforme mencionado na [seção problemas de compatibilidade do pacote dos documentos para migrar `packages.config` do `PackageReference` para ](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues)o, as transformações xdt, conforme descrito abaixo, só têm suporte do `packages.config` . Se você adicionar os arquivos abaixo ao seu pacote, os consumidores que usam seu pacote com `PackageReference` o não terão as transformações aplicadas (consulte [Este exemplo](https://github.com/NuGet/Samples/tree/main/XDTransformExample) para fazer com que as transformações do xdt funcionem `PackageReference` ).

Você pode modificar os arquivos de configuração usando [sintaxe XDT](/previous-versions/aspnet/dd465326(v=vs.110)). Você também pode fazer com que o NuGet substitua os tokens pelas [Propriedades do projeto](/dotnet/api/vslangproj.projectproperties) incluindo o nome da propriedade dentro dos delimitadores `$`(não diferencia maiúsculas de minúsculas).

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
    </system.webServer>
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
    </system.webServer>
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