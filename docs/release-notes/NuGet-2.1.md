---
title: Notas de versão do NuGet 2,1
description: Notas de versão do NuGet 2,1 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c44ad32c8c4018ccb517b41bffda674eef1f11f3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777026"
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="5a701-103">Notas de versão do NuGet 2,1</span><span class="sxs-lookup"><span data-stu-id="5a701-103">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="5a701-104">Notas de versão do [NuGet 2,0](../release-notes/nuget-2.0.md)  |  [Notas de versão do NuGet 2,2](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="5a701-104">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="5a701-105">O NuGet 2,1 foi lançado em 4 de outubro de 2012.</span><span class="sxs-lookup"><span data-stu-id="5a701-105">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="5a701-106">Nuget.Config hierárquica</span><span class="sxs-lookup"><span data-stu-id="5a701-106">Hierarchical Nuget.Config</span></span>

<span data-ttu-id="5a701-107">O NuGet 2,1 proporciona maior flexibilidade no controle das configurações do NuGet por meio da movimentação recursiva da estrutura de pastas procurando `NuGet.Config` arquivos e, em seguida, compilando a configuração do conjunto de todos os arquivos encontrados.</span><span class="sxs-lookup"><span data-stu-id="5a701-107">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="5a701-108">Como exemplo, considere o cenário em que uma equipe tem um repositório de pacotes interno para compilações de CI de outras dependências internas.</span><span class="sxs-lookup"><span data-stu-id="5a701-108">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="5a701-109">A estrutura de pastas de um projeto individual pode ser semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="5a701-109">The folder structure for an individual project might look like the following:</span></span>

```
C:\
C:\myteam\
C:\myteam\solution1
C:\myteam\solution1\project1
```

<span data-ttu-id="5a701-110">Além disso, se a restauração do pacote estiver habilitada para a solução, a seguinte pasta também existirá:</span><span class="sxs-lookup"><span data-stu-id="5a701-110">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

```
C:\myteam\solution1\.nuget
```

<span data-ttu-id="5a701-111">Para que o repositório de pacotes interno da equipe esteja disponível para todos os projetos nos quais a equipe trabalha, embora não o esteja disponibilizando para cada projeto no computador, podemos criar um novo arquivo Nuget.Config e colocá-lo na pasta c:\myteam</span><span class="sxs-lookup"><span data-stu-id="5a701-111">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="5a701-112">Não há nenhuma maneira de especificar uma pasta de pacotes por projeto.</span><span class="sxs-lookup"><span data-stu-id="5a701-112">There is no way to specificy a packages folder per project.</span></span>

```xml
<configuration>
    <packageSources>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </packageSources>
    <disabledPackageSources />
    <activePackageSource>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="5a701-113">Agora podemos ver que a fonte foi adicionada executando o comando ' nuget.exe Sources ' de qualquer pasta abaixo de c:\myteam, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="5a701-113">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![Origens do pacote da configuração pai do NuGet](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="5a701-115">`NuGet.Config` os arquivos são pesquisados na seguinte ordem:</span><span class="sxs-lookup"><span data-stu-id="5a701-115">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="5a701-116">Movimentação recursiva da pasta do projeto para a raiz</span><span class="sxs-lookup"><span data-stu-id="5a701-116">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="5a701-117">Global `Nuget.Config` ( `%appdata%\NuGet\Nuget.Config` )</span><span class="sxs-lookup"><span data-stu-id="5a701-117">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="5a701-118">As configurações são as aplicadas na *ordem inversa*, o que significa que com base na ordenação acima, a Nuget.Config global seria aplicada primeiro, seguida pelos arquivos de Nuget.Config descobertos da raiz para a pasta do projeto, seguido por `.nuget\Nuget.Config` .</span><span class="sxs-lookup"><span data-stu-id="5a701-118">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="5a701-119">Isso é particularmente importante se você estiver usando o `<clear/>` elemento para remover um conjunto de itens da configuração.</span><span class="sxs-lookup"><span data-stu-id="5a701-119">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="5a701-120">Especificar o local da pasta ' Packages '</span><span class="sxs-lookup"><span data-stu-id="5a701-120">Specify ‘packages’ Folder Location</span></span>

<span data-ttu-id="5a701-121">No passado, o NuGet gerenciava os pacotes de uma solução de uma pasta ' Packages ' conhecida encontrada abaixo da pasta raiz da solução.</span><span class="sxs-lookup"><span data-stu-id="5a701-121">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="5a701-122">Para equipes de desenvolvimento que têm muitas soluções diferentes que têm pacotes NuGet instalados, isso pode resultar na instalação do mesmo pacote em vários locais diferentes no sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="5a701-122">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="5a701-123">O NuGet 2,1 fornece um controle mais granular sobre o local da pasta de pacotes por meio do `repositoryPath` elemento no `NuGet.Config` arquivo.</span><span class="sxs-lookup"><span data-stu-id="5a701-123">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="5a701-124">Criando o exemplo anterior de suporte hierárquico de Nuget.Config, suponha que desejamos que todos os projetos em C:\myteam\ compartilhem a mesma pasta de pacotes.</span><span class="sxs-lookup"><span data-stu-id="5a701-124">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="5a701-125">Para fazer isso, basta adicionar a entrada a seguir ao `c:\myteam\Nuget.Config` .</span><span class="sxs-lookup"><span data-stu-id="5a701-125">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="5a701-126">Neste exemplo, o arquivo compartilhado `Nuget.Config` especifica uma pasta de pacotes compartilhados para cada projeto criado sob C:\myteam, independentemente da profundidade.</span><span class="sxs-lookup"><span data-stu-id="5a701-126">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="5a701-127">Observe que, se você tiver uma pasta pacotes existente sob a raiz da solução, será necessário excluí-la antes que o NuGet Coloque os pacotes no novo local.</span><span class="sxs-lookup"><span data-stu-id="5a701-127">Note that if you have an existing packages folder underneath your solution root, you need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="5a701-128">Suporte para bibliotecas portáteis</span><span class="sxs-lookup"><span data-stu-id="5a701-128">Support for Portable Libraries</span></span>

<span data-ttu-id="5a701-129">As [bibliotecas portáteis](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) são um recurso introduzido pela primeira vez com o .NET 4, que permite que você crie assemblies que podem funcionar sem modificação em diferentes plataformas da Microsoft, desde versões do The.NET Framework até o Silverlight até Windows Phone e até mesmo o Xbox 360 (embora, no momento, o NuGet não ofereça suporte ao destino da biblioteca portátil do Xbox).</span><span class="sxs-lookup"><span data-stu-id="5a701-129">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="5a701-130">Ao estender as [convenções de pacote](../create-packages/supporting-multiple-target-frameworks.md) para versões e perfis do Framework, o NuGet 2,1 agora dá suporte a bibliotecas portáteis, permitindo que você crie pacotes que tenham pastas compostas de estrutura e perfil de destino `lib` .</span><span class="sxs-lookup"><span data-stu-id="5a701-130">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="5a701-131">Como exemplo, considere as seguintes plataformas de destino disponíveis da biblioteca de classes portátil.</span><span class="sxs-lookup"><span data-stu-id="5a701-131">As an example, consider the following portable class library’s available target platforms.</span></span>

![Diálogo de criação de biblioteca portátil](./media/releasenotes-21-plib.png)

<span data-ttu-id="5a701-133">Depois que a biblioteca é criada e o comando `nuget.exe pack MyPortableProject.csproj` é executado, a nova estrutura de pasta de pacote de biblioteca portátil pode ser vista examinando o conteúdo do pacote NuGet gerado.</span><span class="sxs-lookup"><span data-stu-id="5a701-133">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![Layout do pacote de biblioteca portátil](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="5a701-135">Como você pode ver, a Convenção de nome da pasta de biblioteca portátil segue o padrão ' Portable-{Framework 1} + {Framework n} ', em que os identificadores de estrutura seguem o [nome da estrutura e as convenções de versão](../reference/target-frameworks.md)existentes.</span><span class="sxs-lookup"><span data-stu-id="5a701-135">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../reference/target-frameworks.md).</span></span> <span data-ttu-id="5a701-136">Uma exceção às convenções de nome e versão é encontrada no identificador de estrutura usado para Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="5a701-136">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="5a701-137">Esse moniker deve usar o nome de estrutura ' wp ' (WP7, wp71 ou WP8).</span><span class="sxs-lookup"><span data-stu-id="5a701-137">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="5a701-138">O uso de ' Silverlight-WP7 ', por exemplo, resultará em um erro.</span><span class="sxs-lookup"><span data-stu-id="5a701-138">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="5a701-139">Ao instalar o pacote criado a partir dessa estrutura de pastas, o NuGet agora pode aplicar sua estrutura e regras de perfil a vários destinos, conforme especificado no nome da pasta.</span><span class="sxs-lookup"><span data-stu-id="5a701-139">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="5a701-140">Por trás das regras de correspondência do NuGet, é o princípio de que destinos "mais específicos" terão precedência sobre os "menos específicos".</span><span class="sxs-lookup"><span data-stu-id="5a701-140">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="5a701-141">Isso significa que os monikers que se destinam a uma plataforma específica sempre serão preferidos sobre os portáteis se forem ambos compatíveis com um projeto.</span><span class="sxs-lookup"><span data-stu-id="5a701-141">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="5a701-142">Além disso, se vários destinos portáteis forem compatíveis com um projeto, o NuGet preferirá aquele em que o conjunto de plataformas com suporte é "mais próximo" ao projeto que faz referência ao pacote.</span><span class="sxs-lookup"><span data-stu-id="5a701-142">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="5a701-143">Direcionando projetos do Windows 8 e do Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="5a701-143">Targeting Windows 8 and Windows Phone 8 Projects</span></span>

<span data-ttu-id="5a701-144">Além de adicionar suporte para o direcionamento de projetos de biblioteca portátil, o NuGet 2,1 fornece novos monikers de estrutura para projetos do Windows 8 Store e do Windows Phone 8, bem como alguns novos monikers gerais para a Windows Store e Windows Phone projetos que serão mais fáceis de gerenciar em versões futuras das respectivas plataformas.</span><span class="sxs-lookup"><span data-stu-id="5a701-144">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="5a701-145">Para aplicativos da loja do Windows 8, os identificadores têm a seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="5a701-145">For Windows 8 Store applications, the identifiers look as follows:</span></span>

| <span data-ttu-id="5a701-146">NuGet 2,0 e anterior</span><span class="sxs-lookup"><span data-stu-id="5a701-146">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="5a701-147">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="5a701-147">NuGet 2.1</span></span> |
| ---------------- | ----------- |
| <span data-ttu-id="5a701-148">winRT45, . NETCore45</span><span class="sxs-lookup"><span data-stu-id="5a701-148">winRT45, .NETCore45</span></span> | <span data-ttu-id="5a701-149">Windows, windows8, Win, win8</span><span class="sxs-lookup"><span data-stu-id="5a701-149">Windows, Windows8, win, win8</span></span> |

<br/>
<span data-ttu-id="5a701-150">Para projetos Windows Phone, os identificadores têm a seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="5a701-150">For Windows Phone projects, the identifiers look as follows:</span></span>

| <span data-ttu-id="5a701-151">SO do telefone</span><span class="sxs-lookup"><span data-stu-id="5a701-151">Phone OS</span></span> | <span data-ttu-id="5a701-152">NuGet 2,0 e anterior</span><span class="sxs-lookup"><span data-stu-id="5a701-152">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="5a701-153">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="5a701-153">NuGet 2.1</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a701-154">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="5a701-154">Windows Phone 7</span></span> | <span data-ttu-id="5a701-155">silverlight3-wp</span><span class="sxs-lookup"><span data-stu-id="5a701-155">silverlight3-wp</span></span> | <span data-ttu-id="5a701-156">WP, WP7, WindowsPhone, WindowsPhone7</span><span class="sxs-lookup"><span data-stu-id="5a701-156">wp, wp7, WindowsPhone, WindowsPhone7</span></span> |
| <span data-ttu-id="5a701-157">Windows Phone 7,5 (Mango)</span><span class="sxs-lookup"><span data-stu-id="5a701-157">Windows Phone 7.5 (Mango)</span></span> | <span data-ttu-id="5a701-158">silverlight4-wp71</span><span class="sxs-lookup"><span data-stu-id="5a701-158">silverlight4-wp71</span></span> | <span data-ttu-id="5a701-159">wp71, WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="5a701-159">wp71, WindowsPhone71</span></span> |
| <span data-ttu-id="5a701-160">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="5a701-160">Windows Phone 8</span></span> | <span data-ttu-id="5a701-161">(sem suporte)</span><span class="sxs-lookup"><span data-stu-id="5a701-161">(not supported)</span></span> | <span data-ttu-id="5a701-162">WP8, WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="5a701-162">wp8, WindowsPhone8</span></span> |

<br/>
<span data-ttu-id="5a701-163">Em todas as alterações acima, os nomes de estrutura antigos continuarão a ser totalmente suportados pelo NuGet 2,1.</span><span class="sxs-lookup"><span data-stu-id="5a701-163">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="5a701-164">Avançando, os novos nomes devem ser usados, pois eles serão mais estáveis em versões futuras das respectivas plataformas.</span><span class="sxs-lookup"><span data-stu-id="5a701-164">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="5a701-165">Os novos nomes *não* terão suporte em versões do NuGet anteriores a 2,1. no entanto, planeje adequadamente para quando fazer a alternância.</span><span class="sxs-lookup"><span data-stu-id="5a701-165">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="5a701-166">Pesquisa aprimorada na caixa de diálogo Gerenciador de pacotes</span><span class="sxs-lookup"><span data-stu-id="5a701-166">Improved Search in Package Manager Dialog</span></span>

<span data-ttu-id="5a701-167">Nas últimas várias iterações, foram introduzidas alterações na galeria do NuGet que melhoraram muito a velocidade e a relevância das pesquisas de pacote.</span><span class="sxs-lookup"><span data-stu-id="5a701-167">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="5a701-168">No entanto, essas melhorias eram limitadas ao site da nuget.org.</span><span class="sxs-lookup"><span data-stu-id="5a701-168">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="5a701-169">O NuGet 2,1 torna a experiência de pesquisa aprimorada disponível por meio da caixa de diálogo Gerenciador de pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="5a701-169">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="5a701-170">Como exemplo, imagine que você queria encontrar o pacote de visualização do Windows Azure Caching.</span><span class="sxs-lookup"><span data-stu-id="5a701-170">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="5a701-171">Uma consulta de pesquisa razoável para esse pacote pode ser "cache do Azure".</span><span class="sxs-lookup"><span data-stu-id="5a701-171">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="5a701-172">Nas versões anteriores da caixa de diálogo Gerenciador de pacotes, o pacote desejado nem mesmo seria listado na primeira página de resultados.</span><span class="sxs-lookup"><span data-stu-id="5a701-172">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="5a701-173">No entanto, no NuGet 2,1, o pacote desejado agora aparece na parte superior dos resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="5a701-173">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![Pesquisa de diálogo do Gerenciador de pacotes](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="5a701-175">Forçar atualização do pacote</span><span class="sxs-lookup"><span data-stu-id="5a701-175">Force Package Update</span></span>

<span data-ttu-id="5a701-176">Antes do NuGet 2,1, o NuGet ignoraria a atualização de um pacote quando não havia um número de versão alto.</span><span class="sxs-lookup"><span data-stu-id="5a701-176">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="5a701-177">Isso introduziu o problema para determinados cenários – particularmente no caso de cenários de compilação ou CI, em que a equipe não queria incrementar o número de versão do pacote com cada compilação.</span><span class="sxs-lookup"><span data-stu-id="5a701-177">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="5a701-178">O comportamento desejado foi forçar uma atualização, independentemente.</span><span class="sxs-lookup"><span data-stu-id="5a701-178">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="5a701-179">O NuGet 2,1 resolve isso com o sinalizador ' Reinstall '.</span><span class="sxs-lookup"><span data-stu-id="5a701-179">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="5a701-180">Por exemplo, as versões anteriores do NuGet resultarão no seguinte ao tentar atualizar um pacote que não tinha uma versão mais recente do pacote:</span><span class="sxs-lookup"><span data-stu-id="5a701-180">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

```
PM> Update-Package Moq
No updates available for 'Moq' in project 'MySolution.MyConsole'.
```

<span data-ttu-id="5a701-181">Com o sinalizador REINSTALL, o pacote será atualizado independentemente de haver uma versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="5a701-181">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

```
PM> Update-Package Moq -Reinstall
Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
Successfully uninstalled 'Moq 4.0.10827'.
Successfully installed 'Moq 4.0.10827'.
Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.
```

<span data-ttu-id="5a701-182">Outro cenário em que o sinalizador reinstalar comprova benéfico é o de redirecionamento de estrutura.</span><span class="sxs-lookup"><span data-stu-id="5a701-182">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="5a701-183">Ao alterar a estrutura de destino de um projeto (por exemplo, do .NET 4 para o .NET 4,5), a reinstalação do Update-Package pode atualizar as referências aos assemblies corretos para todos os pacotes do NuGet instalados no projeto.</span><span class="sxs-lookup"><span data-stu-id="5a701-183">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="5a701-184">Editar fontes de pacote no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5a701-184">Edit Package Sources Within Visual Studio</span></span>

<span data-ttu-id="5a701-185">Nas versões anteriores do NuGet, a atualização de uma origem de pacote de dentro da caixa de diálogo opções do Visual Studio exigia a exclusão e a adição da origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="5a701-185">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="5a701-186">O NuGet 2,1 melhora esse fluxo de trabalho ao dar suporte à atualização como uma função de primeira classe da interface do usuário de configuração.</span><span class="sxs-lookup"><span data-stu-id="5a701-186">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![Caixa de diálogo de configuração do Gerenciador de pacotes](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="5a701-188">Correções de bugs</span><span class="sxs-lookup"><span data-stu-id="5a701-188">Bug Fixes</span></span>

<span data-ttu-id="5a701-189">O NuGet 2,1 inclui muitas correções de bugs.</span><span class="sxs-lookup"><span data-stu-id="5a701-189">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="5a701-190">Para obter uma lista completa de itens de trabalho corrigidos no NuGet 2,0, consulte o [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="5a701-190">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
