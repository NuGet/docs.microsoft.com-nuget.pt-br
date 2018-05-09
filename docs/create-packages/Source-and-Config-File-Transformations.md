---
title: Transformações de arquivos de origem e de configuração para pacotes do NuGet
description: Detalhes sobre a capacidade de pacotes do NuGet transformarem arquivos de código-fonte e da configuração (XML) quando instalado.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 863bf22780313a34690617dd6a1604531272808b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="transforming-source-code-and-configuration-files"></a><span data-ttu-id="52d59-103">Transformando o código-fonte e os arquivos de configuração</span><span class="sxs-lookup"><span data-stu-id="52d59-103">Transforming source code and configuration files</span></span>

<span data-ttu-id="52d59-104">Para projetos que usam `packages.config`, o NuGet dá suporte à capacidade de fazer as transformações no código-fonte e nos arquivos de configuração nos tempos de instalação e desinstalação de pacote.</span><span class="sxs-lookup"><span data-stu-id="52d59-104">For projects using `packages.config`, NuGet supports the ability to make transformations to source code and configuration files at package install and uninstall times.</span></span> <span data-ttu-id="52d59-105">As transformações de código-fonte são aplicadas somente quando um pacote é instalado em um projeto que usa [PackageReference](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="52d59-105">Only Source code transformations are applied when a package is installed in a project using [PackageReference](../consume-packages/package-references-in-project-files.md).</span></span>

<span data-ttu-id="52d59-106">Uma **transformação de código-fonte** aplicará a substituição de token unidirecional aos arquivos na pasta `content` ou `contentFiles` do pacote (`content` para clientes usando `packages.config` e `contentFiles` para `PackageReference`) quando o pacote estiver instalado e quando os tokens fizerem referência às [propriedades do projeto](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="52d59-106">A **source code transformation** applies one-way token replacement to files in the package's `content` or `contentFiles` folder (`content` for customers using `packages.config` and `contentFiles` for `PackageReference`) when the package is installed, where tokens refer to Visual Studio [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="52d59-107">Isso permite inserir um arquivo de namespace de projeto ou personalizar código que geralmente iria para `global.asax` em um projeto do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="52d59-107">This allows you to insert a file into the project's namespace, or to customize code that would typically go into `global.asax` in an ASP.NET project.</span></span>

<span data-ttu-id="52d59-108">Uma **transformação do arquivo de configuração** permite que você modifique os arquivos que já existem em um projeto de destino, como `web.config` e `app.config`.</span><span class="sxs-lookup"><span data-stu-id="52d59-108">A **config file transformation** allows you to modify files that already exist in a target project, such as `web.config` and `app.config`.</span></span> <span data-ttu-id="52d59-109">Por exemplo, seu pacote pode ser necessário para adicionar um item à seção `modules` no arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="52d59-109">For example, your package might need to add an item to the `modules` section in the config file.</span></span> <span data-ttu-id="52d59-110">Essa transformação são feitas incluindo arquivos especiais no pacote que descreve as seções a serem adicionadas aos arquivos de configuração.</span><span class="sxs-lookup"><span data-stu-id="52d59-110">This transformation is done by including special files in the package that describe the sections to add to the configuration files.</span></span> <span data-ttu-id="52d59-111">Quando um pacote é desinstalado, essas mesmas alterações são revertidas, tornando esta uma transformação bidirecional.</span><span class="sxs-lookup"><span data-stu-id="52d59-111">When a package is uninstalled, those same changes are then reversed, making this a two-way transformation.</span></span>

## <a name="specifying-source-code-transformations"></a><span data-ttu-id="52d59-112">Especificar as transformações do código-fonte</span><span class="sxs-lookup"><span data-stu-id="52d59-112">Specifying source code transformations</span></span>

1. <span data-ttu-id="52d59-113">Os arquivos do pacote que você deseja inserir no projeto devem estar localizados nas pastas `content` e `contentFiles` do pacote.</span><span class="sxs-lookup"><span data-stu-id="52d59-113">Files that you want to insert from the package into the project must be located within the package's `content` and `contentFiles` folders.</span></span> <span data-ttu-id="52d59-114">Por exemplo, se você desejar que um arquivo chamado `ContosoData.cs` seja instalado em uma pasta `Models` do projeto de destino, ele precisará estar nas pastas `content\Models` e `contentFiles\{lang}\{tfm}\Models` no pacote.</span><span class="sxs-lookup"><span data-stu-id="52d59-114">For example, if you want a file called `ContosoData.cs` to be installed in a `Models` folder of the target project, it must be inside the `content\Models` and `contentFiles\{lang}\{tfm}\Models` folders in the package.</span></span>

1. <span data-ttu-id="52d59-115">Para instruir o NuGet a aplicar a substituição de token no momento da instalação, acrescente `.pp` ao nome do arquivo de código-fonte.</span><span class="sxs-lookup"><span data-stu-id="52d59-115">To instruct NuGet to apply token replacement at install time, append `.pp` to the source code file name.</span></span> <span data-ttu-id="52d59-116">Após a instalação, o arquivo não terá a extensão `.pp`.</span><span class="sxs-lookup"><span data-stu-id="52d59-116">After installation, the file will not have the `.pp` extension.</span></span>

    <span data-ttu-id="52d59-117">Por exemplo, para realizar transformações em `ContosoData.cs`, nomeie o arquivo no pacote `ContosoData.cs.pp`.</span><span class="sxs-lookup"><span data-stu-id="52d59-117">For example, to make transformations in `ContosoData.cs`, name the file in the package `ContosoData.cs.pp`.</span></span> <span data-ttu-id="52d59-118">Após a instalação, ele será exibido como `ContosoData.cs`.</span><span class="sxs-lookup"><span data-stu-id="52d59-118">After installation it will appear as `ContosoData.cs`.</span></span>

1. <span data-ttu-id="52d59-119">No arquivo de código-fonte, use tokens que não diferenciam maiúsculas e minúsculas no formato `$token$` para indicar os valores que o NuGet deve substituir com as propriedades do projeto:</span><span class="sxs-lookup"><span data-stu-id="52d59-119">In the source code file, use case-insensitive tokens of the form `$token$` to indicate values that NuGet should replace with project properties:</span></span>

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

    <span data-ttu-id="52d59-120">Após a instalação, o NuGet substitui `$rootnamespace$` por `Fabrikam`, considerando o projeto de destino cujo namespace da raiz é `Fabrikam`.</span><span class="sxs-lookup"><span data-stu-id="52d59-120">Upon installation, NuGet replaces `$rootnamespace$` with `Fabrikam` assuming the target project's whose root namespace is `Fabrikam`.</span></span>

<span data-ttu-id="52d59-121">O token `$rootnamespace$` é a propriedade de projeto mais usada; todas as outras são listadas nas [propriedades do projeto](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span><span class="sxs-lookup"><span data-stu-id="52d59-121">The `$rootnamespace$` token is the most commonly used project property; all others are listed in [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="52d59-122">Lembre-se, obviamente, algumas propriedades podem ser específicas ao tipo de projeto.</span><span class="sxs-lookup"><span data-stu-id="52d59-122">Be mindful, of course, that some properties might be specific to the project type.</span></span>

## <a name="specifying-config-file-transformations"></a><span data-ttu-id="52d59-123">Especificar as transformações do arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="52d59-123">Specifying config file transformations</span></span>

<span data-ttu-id="52d59-124">Conforme descrito nas seções a seguir, as transformações do arquivo de configuração podem ser feitas de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="52d59-124">As described in the sections that follow, config file transformations can be done in two ways:</span></span>

- <span data-ttu-id="52d59-125">Inclua os arquivos `app.config.transform` e `web.config.transform` na pasta `content` do seu pacote, em que a extensão `.transform` diz ao NuGet que esses arquivos contêm o XML para serem mesclados com os arquivos de configuração existentes quando o pacote é instalado.</span><span class="sxs-lookup"><span data-stu-id="52d59-125">Include `app.config.transform` and `web.config.transform` files in your package's `content` folder, where the `.transform` extension tells NuGet that these files contain the XML to merge with existing config files when the package is installed.</span></span> <span data-ttu-id="52d59-126">Quando um pacote é desinstalado, esse mesmo XML é removido.</span><span class="sxs-lookup"><span data-stu-id="52d59-126">When a package is uninstalled, that same XML is removed.</span></span>
- <span data-ttu-id="52d59-127">Inclua os arquivos `app.config.install.xdt` e `web.config.install.xdt` na pasta `content` do pacote usando [sintaxe XDT](https://msdn.microsoft.com/library/dd465326.aspx) para descrever as alterações desejadas.</span><span class="sxs-lookup"><span data-stu-id="52d59-127">Include `app.config.install.xdt` and `web.config.install.xdt` files in your package's `content` folder, using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx) to describe the desired changes.</span></span> <span data-ttu-id="52d59-128">Com essa opção, também é possível incluir um arquivo `.uninstall.xdt` para reverter as alterações quando o pacote é removido de um projeto.</span><span class="sxs-lookup"><span data-stu-id="52d59-128">With this option you can also include a `.uninstall.xdt` file to reverse changes when the package is removed from a project.</span></span>

> [!Note]
> <span data-ttu-id="52d59-129">As transformações não são aplicadas a arquivos `.config` referenciados como um link no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="52d59-129">Transformations are not applied to `.config` files referenced as a link in Visual Studio.</span></span>

<span data-ttu-id="52d59-130">A vantagem de usar o XDT é que, em vez de simplesmente mesclar dois arquivos estáticos, ele fornece uma sintaxe para manipular a estrutura de um XML DOM usando correspondência de elemento e atributo com total suporte do XPath.</span><span class="sxs-lookup"><span data-stu-id="52d59-130">The advantage of using XDT is that instead of simply merging two static files, it provides a syntax for manipulating the structure of an XML DOM using element and attribute matching using full XPath support.</span></span> <span data-ttu-id="52d59-131">O XDT pode então adicionar, atualizar ou remover os elementos, colocar novos elementos em um local específico ou substituir/remover elementos (incluindo nós filho).</span><span class="sxs-lookup"><span data-stu-id="52d59-131">XDT can then add, update, or remove elements, place new elements at a specific location, or replace/remove elements (including child nodes).</span></span> <span data-ttu-id="52d59-132">Isso simplifica a criação de transformações de desinstalação que retornam todas as transformações durante a instalação do pacote.</span><span class="sxs-lookup"><span data-stu-id="52d59-132">This makes it straightforward to create uninstall transforms that back out all transformations done during package installation.</span></span>

### <a name="xml-transforms"></a><span data-ttu-id="52d59-133">Transformações XML</span><span class="sxs-lookup"><span data-stu-id="52d59-133">XML transforms</span></span>

<span data-ttu-id="52d59-134">Os `app.config.transform` e `web.config.transform` na pasta `content` de um pacote contém apenas os elementos para mesclar os arquivos `app.config` e `web.config` existentes do projeto.</span><span class="sxs-lookup"><span data-stu-id="52d59-134">The `app.config.transform` and `web.config.transform` in a package's `content` folder contain only those elements to merge into the project's existing `app.config` and `web.config` files.</span></span>

<span data-ttu-id="52d59-135">Por exemplo, suponha que o projeto inicialmente contém o conteúdo a seguir em `web.config`:</span><span class="sxs-lookup"><span data-stu-id="52d59-135">As an example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="52d59-136">Para adicionar um elemento `MyNuModule` à seção `modules` durante a instalação do pacote, crie um arquivo `web.config.transform` na pasta `content` do pacote que se assemelhará a esta:</span><span class="sxs-lookup"><span data-stu-id="52d59-136">To add a `MyNuModule` element to the `modules` section during package install, create a `web.config.transform` file in the package's `content` folder that looks like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="52d59-137">Depois que o NuGet instala o pacote, `web.config` será exibido da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="52d59-137">After NuGet installs the package, `web.config` will appear as follows:</span></span>

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

<span data-ttu-id="52d59-138">Observe que o NuGet não substituiu a seção `modules`, ele só mesclou a nova entrada com ele adicionando somente novos elementos e atributos.</span><span class="sxs-lookup"><span data-stu-id="52d59-138">Notice that NuGet didn't replace the `modules` section, it just merged the new entry into it by adding only new elements and attributes.</span></span> <span data-ttu-id="52d59-139">O NuGet não alterará nenhum atributo ou elemento existente.</span><span class="sxs-lookup"><span data-stu-id="52d59-139">NuGet will not change any existing elements or attributes.</span></span>

<span data-ttu-id="52d59-140">Quando o pacote é desinstalado, o NuGet examinará os arquivos `.transform` novamente e remove os elementos que ele contém dos arquivos `.config` apropriados.</span><span class="sxs-lookup"><span data-stu-id="52d59-140">When the package is uninstalled, NuGet will examine the `.transform` files again and remove the elements it contains from the appropriate `.config` files.</span></span> <span data-ttu-id="52d59-141">Observe que esse processo não afetará as linhas no arquivo `.config` que podem ser modificadas após a instalação do pacote.</span><span class="sxs-lookup"><span data-stu-id="52d59-141">Note that this process will not affect any lines in the `.config` file that you modify after package installation.</span></span>

<span data-ttu-id="52d59-142">Como um exemplo mais amplo, o pacote [Módulos e manipuladores de log de erros para ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) adiciona várias entradas a `web.config`, que são removidas novamente quando um pacote é desinstalado.</span><span class="sxs-lookup"><span data-stu-id="52d59-142">As a more extensive example, the [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) package adds many entries into `web.config`, which are again removed when a package is uninstalled.</span></span>

<span data-ttu-id="52d59-143">Para examinar seu arquivo `web.config.transform`, baixe o pacote ELMAH do link acima, altere a extensão do pacote de `.nupkg` para `.zip` e abra `content\web.config.transform` nesse arquivo ZIP.</span><span class="sxs-lookup"><span data-stu-id="52d59-143">To examine its `web.config.transform` file, download the ELMAH package from the link above, change the package extension from `.nupkg` to `.zip`, and then open `content\web.config.transform` in that ZIP file.</span></span>

<span data-ttu-id="52d59-144">Para ver o efeito de instalação e desinstalação do pacote, crie um novo projeto do ASP.NET no Visual Studio (o modelo está em **Visual C# > Web** na caixa de diálogo Novo Projeto) e selecione um aplicativo ASP.NET vazio.</span><span class="sxs-lookup"><span data-stu-id="52d59-144">To see the effect of installing and uninstalling the package, create a new ASP.NET project in Visual Studio (the template is under **Visual C# > Web** in the New Project dialog), and select an empty ASP.NET application.</span></span> <span data-ttu-id="52d59-145">Abra `web.config` para ver seu estado inicial.</span><span class="sxs-lookup"><span data-stu-id="52d59-145">Open `web.config` to see its initial state.</span></span> <span data-ttu-id="52d59-146">Em seguida, clique com botão direito do mouse no projeto, selecione **Gerenciar pacotes do NuGet**, procurar ELMAH no nuget.org e instalar a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="52d59-146">Then right-click the project, select **Manage NuGet Packages**, browse for ELMAH on nuget.org, and install the latest version.</span></span> <span data-ttu-id="52d59-147">Observe todas as alterações em `web.config`.</span><span class="sxs-lookup"><span data-stu-id="52d59-147">Notice all the changes to `web.config`.</span></span> <span data-ttu-id="52d59-148">Agora, desinstale o pacote e você verá o `web.config` reverter para seu estado anterior.</span><span class="sxs-lookup"><span data-stu-id="52d59-148">Now uninstall the package and you see `web.config` revert to its prior state.</span></span>

### <a name="xdt-transforms"></a><span data-ttu-id="52d59-149">Transformações XDT</span><span class="sxs-lookup"><span data-stu-id="52d59-149">XDT transforms</span></span>

<span data-ttu-id="52d59-150">Você pode modificar os arquivos de configuração usando [sintaxe XDT](https://msdn.microsoft.com/library/dd465326.aspx).</span><span class="sxs-lookup"><span data-stu-id="52d59-150">You can modify config files using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx).</span></span> <span data-ttu-id="52d59-151">Você também pode fazer com que o NuGet substitua os tokens pelas [Propriedades do projeto](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) incluindo o nome da propriedade dentro dos delimitadores `$`(não diferencia maiúsculas de minúsculas).</span><span class="sxs-lookup"><span data-stu-id="52d59-151">You can also have NuGet replace tokens with [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) by including the property name within `$` delimeters (case-insensitive).</span></span>

<span data-ttu-id="52d59-152">Por exemplo, o arquivo `app.config.install.xdt` a seguir inserirá um elemento `appSettings` em `app.config` que contém os valores `FullPath`, `FileName` e `ActiveConfigurationSettings` valores do projeto:</span><span class="sxs-lookup"><span data-stu-id="52d59-152">For example, the following `app.config.install.xdt` file will insert an `appSettings` element into `app.config` containing the `FullPath`, `FileName`, and `ActiveConfigurationSettings` values from the project:</span></span>

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

<span data-ttu-id="52d59-153">Para ver outro exemplo, considere que o projeto inicialmente tem o conteúdo a seguir em `web.config`:</span><span class="sxs-lookup"><span data-stu-id="52d59-153">For another example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="52d59-154">Para adicionar um elemento `MyNuModule` à seção `modules` durante a instalação de pacotes, o `web.config.install.xdt` do pacote poderia conter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="52d59-154">To add a `MyNuModule` element to the `modules` section during package install, the package's `web.config.install.xdt` would contain the following:</span></span>

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

<span data-ttu-id="52d59-155">Depois de instalar o pacote, `web.config` se parecerá com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="52d59-155">After installing the package, `web.config` will look like this:</span></span>

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

<span data-ttu-id="52d59-156">Para remover apenas o elemento `MyNuModule` durante a desinstalação do pacote, o arquivo `web.config.uninstall.xdt` deve conter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="52d59-156">To remove only the `MyNuModule` element during package uninstall, the `web.config.uninstall.xdt` file should contain the following:</span></span>

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
