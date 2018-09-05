---
title: Notas de versão 2.1 do NuGet
description: Notas da versão 2.1 do NuGet incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fd6dadc7968991c77c1b06a6a261415355b2fd73
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548591"
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="dff89-103">Notas de versão 2.1 do NuGet</span><span class="sxs-lookup"><span data-stu-id="dff89-103">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="dff89-104">[Notas de versão do NuGet 2.0](../release-notes/nuget-2.0.md) | [notas de versão do NuGet 2.2](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="dff89-104">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="dff89-105">2.1 do NuGet foi lançado em 4 de outubro de 2012.</span><span class="sxs-lookup"><span data-stu-id="dff89-105">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="dff89-106">NuGet. config hierárquica</span><span class="sxs-lookup"><span data-stu-id="dff89-106">Hierarchical Nuget.Config</span></span>

<span data-ttu-id="dff89-107">2.1 do NuGet fornece maior flexibilidade no controle de configurações do NuGet por meio de recursivamente, percorra a estrutura de pastas procurando `NuGet.Config` arquivos e, em seguida, compilar a configuração do conjunto de todos os arquivos encontrados.</span><span class="sxs-lookup"><span data-stu-id="dff89-107">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="dff89-108">Por exemplo, considere o cenário em que uma equipe tem um repositório do pacote interno para compilações de CI de outras dependências internas.</span><span class="sxs-lookup"><span data-stu-id="dff89-108">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="dff89-109">A estrutura de pastas para um projeto individual pode parecer com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="dff89-109">The folder structure for an individual project might look like the following:</span></span>

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

<span data-ttu-id="dff89-110">Além disso, se a restauração do pacote está habilitada para a solução, a pasta a seguir também existirá:</span><span class="sxs-lookup"><span data-stu-id="dff89-110">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

    C:\myteam\solution1\.nuget

<span data-ttu-id="dff89-111">Para ter um repositório de pacote interno da equipe disponível para todos os projetos que a equipe trabalha em, ao mesmo tempo, tornando-o não disponível para todos os projetos na máquina, podemos criar um novo arquivo NuGet. config e colocá-lo na pasta c:\myteam.</span><span class="sxs-lookup"><span data-stu-id="dff89-111">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="dff89-112">Não há nenhuma maneira para especificar uma pasta de pacotes por projeto.</span><span class="sxs-lookup"><span data-stu-id="dff89-112">There is no way to specificy a packages folder per project.</span></span>

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

<span data-ttu-id="dff89-113">Agora podemos ver que a fonte foi adicionada executando o comando 'nuget.exe fontes' de qualquer pasta abaixo c:\myteam conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="dff89-113">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![Fontes de pacote de configuração do nuget pai](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="dff89-115">`NuGet.Config` arquivos são pesquisados na seguinte ordem:</span><span class="sxs-lookup"><span data-stu-id="dff89-115">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="dff89-116">Recursiva ir da pasta do projeto raiz</span><span class="sxs-lookup"><span data-stu-id="dff89-116">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="dff89-117">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span><span class="sxs-lookup"><span data-stu-id="dff89-117">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="dff89-118">As configurações são aplicadas na *ordem inversa*, que significa que, com base na classificação acima, o NuGet. config global seria ser aplicada primeiro, seguido por descobertos arquivos NuGet. config de raiz a pasta do projeto, seguidos por `.nuget\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="dff89-118">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="dff89-119">Isso é particularmente importante se você estiver usando o `<clear/>` elemento para remover um conjunto de itens de configuração.</span><span class="sxs-lookup"><span data-stu-id="dff89-119">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="dff89-120">Especifique 'pacotes' local da pasta</span><span class="sxs-lookup"><span data-stu-id="dff89-120">Specify ‘packages’ Folder Location</span></span>

<span data-ttu-id="dff89-121">No passado, o NuGet tem gerenciado pacotes da solução de uma pasta de pacotes' conhecidos' encontrada sob a pasta raiz da solução.</span><span class="sxs-lookup"><span data-stu-id="dff89-121">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="dff89-122">Para equipes de desenvolvimento que têm muitas soluções diferentes que têm pacotes NuGet instalados, isso pode resultar no mesmo pacote que está sendo instalado em diversos lugares no sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="dff89-122">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="dff89-123">2.1 do NuGet fornece controle mais granular sobre o local da pasta de pacotes por meio de `repositoryPath` elemento no `NuGet.Config` arquivo.</span><span class="sxs-lookup"><span data-stu-id="dff89-123">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="dff89-124">Compilando o exemplo anterior de suporte hierárquico do NuGet. config, suponha que desejamos ter todos os projetos em C:\myteam\ compartilhar a mesma pasta de pacotes.</span><span class="sxs-lookup"><span data-stu-id="dff89-124">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="dff89-125">Para fazer isso, basta adicionar a seguinte entrada à `c:\myteam\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="dff89-125">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="dff89-126">Neste exemplo, o compartilhado `Nuget.Config` arquivo Especifica uma pasta de pacotes compartilhados para cada projeto que é criada abaixo C:\myteam, independentemente de profundidade.</span><span class="sxs-lookup"><span data-stu-id="dff89-126">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="dff89-127">Observe que, se você tiver uma pasta de pacotes existente sob a raiz da solução, você precisa excluí-lo antes do NuGet colocará pacotes no novo local.</span><span class="sxs-lookup"><span data-stu-id="dff89-127">Note that if you have an existing packages folder underneath your solution root, you need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="dff89-128">Suporte para bibliotecas portáteis</span><span class="sxs-lookup"><span data-stu-id="dff89-128">Support for Portable Libraries</span></span>

<span data-ttu-id="dff89-129">[Bibliotecas portáteis](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) é um recurso introduzido pela primeira vez com o .NET 4 que permite que você crie assemblies que podem funcionar sem modificação em diferentes plataformas da Microsoft, de versões do.NET Framework para Silverlight para Windows Phone e Xbox até mesmo 360 (embora neste momento, o NuGet não suporta o destino de biblioteca portátil do Xbox).</span><span class="sxs-lookup"><span data-stu-id="dff89-129">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="dff89-130">Estendendo o [convenções de pacote](../create-packages/supporting-multiple-target-frameworks.md) para versões do framework e perfis, 2.1 do NuGet agora dá suporte a bibliotecas portáteis, permitindo que você criar pacotes que têm composto framework e o perfil de destino `lib` pastas.</span><span class="sxs-lookup"><span data-stu-id="dff89-130">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="dff89-131">Por exemplo, considere a possibilidade de plataformas de destino disponíveis da biblioteca de classes portátil seguintes.</span><span class="sxs-lookup"><span data-stu-id="dff89-131">As an example, consider the following portable class library’s available target platforms.</span></span>

![Caixa de diálogo de criação de biblioteca portátil](./media/releasenotes-21-plib.png)

<span data-ttu-id="dff89-133">Depois que a biblioteca é compilada e o comando `nuget.exe pack MyPortableProject.csproj` é executado, portátil nova estrutura de pastas de pacote de biblioteca pode ser vista examinando o conteúdo do pacote do NuGet gerado.</span><span class="sxs-lookup"><span data-stu-id="dff89-133">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![Layout do pacote de biblioteca portátil](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="dff89-135">Como você pode ver, a convenção de nomes de pasta de biblioteca portátil segue o padrão 'portable-{framework 1} + {framework n}' em que os identificadores de framework siga existente [convenções de nome e a versão do framework](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="dff89-135">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../reference/target-frameworks.md).</span></span> <span data-ttu-id="dff89-136">Uma exceção com as convenções de nome e a versão for encontrada no identificador de estrutura usado para o Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="dff89-136">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="dff89-137">Esse moniker deve usar o nome da estrutura 'wp' (wp7, wp71 ou wp8).</span><span class="sxs-lookup"><span data-stu-id="dff89-137">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="dff89-138">Usar 'silverlight wp7', por exemplo, resultará em erro.</span><span class="sxs-lookup"><span data-stu-id="dff89-138">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="dff89-139">Ao instalar o pacote que é criado a partir dessa estrutura de pasta, o NuGet agora pode aplicar suas regras de estrutura e o perfil para vários destinos, conforme especificado no nome da pasta.</span><span class="sxs-lookup"><span data-stu-id="dff89-139">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="dff89-140">Por trás de regras de correspondência do NuGet é o princípio de que os destinos "mais específicos" terá precedência sobre "menos específicas".</span><span class="sxs-lookup"><span data-stu-id="dff89-140">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="dff89-141">Isso significa que monikers visando uma plataforma específica sempre será preferenciais sobre aqueles portátil se eles são compatíveis com um projeto.</span><span class="sxs-lookup"><span data-stu-id="dff89-141">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="dff89-142">Além disso, se vários destinos portáteis são compatíveis com um projeto, o NuGet vai preferir aquele em que o conjunto de plataformas com suporte é "mais próximo" para o projeto referenciando o pacote.</span><span class="sxs-lookup"><span data-stu-id="dff89-142">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="dff89-143">Direcionamento do Windows 8 e Windows Phone 8 projetos</span><span class="sxs-lookup"><span data-stu-id="dff89-143">Targeting Windows 8 and Windows Phone 8 Projects</span></span>

<span data-ttu-id="dff89-144">Além de adicionar suporte para projetos de biblioteca portátil de direcionamento, 2.1 do NuGet fornece novos monikers de estrutura para projetos do Windows 8 Store e Windows Phone 8, bem como alguns novos monikers gerais para a Windows Store e projetos do Windows Phone que será mais fácil de gerenciar em versões futuras das respectivas plataformas.</span><span class="sxs-lookup"><span data-stu-id="dff89-144">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="dff89-145">Para aplicativos do Windows 8 Store, os identificadores semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="dff89-145">For Windows 8 Store applications, the identifiers look as follows:</span></span>

| <span data-ttu-id="dff89-146">NuGet 2.0 e versões anterior</span><span class="sxs-lookup"><span data-stu-id="dff89-146">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="dff89-147">2.1 do NuGet</span><span class="sxs-lookup"><span data-stu-id="dff89-147">NuGet 2.1</span></span> |
| ---------------- | ----------- |
| <span data-ttu-id="dff89-148">winRT45, .NETCore45</span><span class="sxs-lookup"><span data-stu-id="dff89-148">winRT45, .NETCore45</span></span> | <span data-ttu-id="dff89-149">Win do Windows, Windows8, win8</span><span class="sxs-lookup"><span data-stu-id="dff89-149">Windows, Windows8, win, win8</span></span> |

<br/>
<span data-ttu-id="dff89-150">Para projetos do Windows Phone, os identificadores semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="dff89-150">For Windows Phone projects, the identifiers look as follows:</span></span>

| <span data-ttu-id="dff89-151">Sistema operacional do telefone</span><span class="sxs-lookup"><span data-stu-id="dff89-151">Phone OS</span></span> | <span data-ttu-id="dff89-152">NuGet 2.0 e versões anterior</span><span class="sxs-lookup"><span data-stu-id="dff89-152">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="dff89-153">2.1 do NuGet</span><span class="sxs-lookup"><span data-stu-id="dff89-153">NuGet 2.1</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dff89-154">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="dff89-154">Windows Phone 7</span></span> | <span data-ttu-id="dff89-155">silverlight3 wp</span><span class="sxs-lookup"><span data-stu-id="dff89-155">silverlight3-wp</span></span> | <span data-ttu-id="dff89-156">WP, wp7, WindowsPhone, WindowsPhone7</span><span class="sxs-lookup"><span data-stu-id="dff89-156">wp, wp7, WindowsPhone, WindowsPhone7</span></span> |
| <span data-ttu-id="dff89-157">Windows Phone 7.5 (Mango)</span><span class="sxs-lookup"><span data-stu-id="dff89-157">Windows Phone 7.5 (Mango)</span></span> | <span data-ttu-id="dff89-158">silverlight4 wp71</span><span class="sxs-lookup"><span data-stu-id="dff89-158">silverlight4-wp71</span></span> | <span data-ttu-id="dff89-159">wp71, WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="dff89-159">wp71, WindowsPhone71</span></span> |
| <span data-ttu-id="dff89-160">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="dff89-160">Windows Phone 8</span></span> | <span data-ttu-id="dff89-161">(sem suporte)</span><span class="sxs-lookup"><span data-stu-id="dff89-161">(not supported)</span></span> | <span data-ttu-id="dff89-162">wp8, WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="dff89-162">wp8, WindowsPhone8</span></span> |

<br/>
<span data-ttu-id="dff89-163">Em todas as alterações acima, os nomes antigos do framework continuarão tendo suporte completo pelo NuGet 2.1.</span><span class="sxs-lookup"><span data-stu-id="dff89-163">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="dff89-164">Mais adiante, os novos nomes devem ser usados como eles serão mais estáveis entre versões futuras das respectivas plataformas.</span><span class="sxs-lookup"><span data-stu-id="dff89-164">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="dff89-165">Os novos nomes serão *não* ser, portanto, no entanto, com suporte nas versões do NuGet anteriores à 2.1, planeje adequadamente para quando a transição.</span><span class="sxs-lookup"><span data-stu-id="dff89-165">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="dff89-166">Pesquisa aperfeiçoada na caixa de diálogo Gerenciador de pacotes</span><span class="sxs-lookup"><span data-stu-id="dff89-166">Improved Search in Package Manager Dialog</span></span>

<span data-ttu-id="dff89-167">Ao longo de várias iterações anteriores, as alterações foram introduzidas na Galeria do NuGet que melhorou muito a velocidade e a relevância das pesquisas de pacote.</span><span class="sxs-lookup"><span data-stu-id="dff89-167">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="dff89-168">No entanto, esses aprimoramentos eram limitados para o site nuget.org.</span><span class="sxs-lookup"><span data-stu-id="dff89-168">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="dff89-169">NuGet 2.1 torna a pesquisa aperfeiçoada experiência disponível por meio da caixa de diálogo do Gerenciador de pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="dff89-169">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="dff89-170">Por exemplo, imagine que você queira localizar o pacote de versão prévia do Windows Azure de cache.</span><span class="sxs-lookup"><span data-stu-id="dff89-170">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="dff89-171">Uma consulta de pesquisa razoável para esse pacote pode ser "Cache do Azure".</span><span class="sxs-lookup"><span data-stu-id="dff89-171">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="dff89-172">Nas versões anteriores da caixa de diálogo de Gerenciador de pacote, o pacote desejado ainda não é listado na primeira página de resultados.</span><span class="sxs-lookup"><span data-stu-id="dff89-172">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="dff89-173">No entanto, o NuGet 2.1, o pacote desejado agora aparece na parte superior dos resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="dff89-173">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![Pesquisa de caixa de diálogo de Gerenciador de pacote](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="dff89-175">Forçar a atualização de pacote</span><span class="sxs-lookup"><span data-stu-id="dff89-175">Force Package Update</span></span>

<span data-ttu-id="dff89-176">Antes de 2.1 do NuGet, NuGet seria ignorar a atualização de um pacote quando havia uma não um número de versão de alta.</span><span class="sxs-lookup"><span data-stu-id="dff89-176">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="dff89-177">Essa introduzida atrito para determinados cenários – especialmente no caso de compilação ou CI cenários em que a equipe não queria incrementar o número com cada compilação de versão do pacote.</span><span class="sxs-lookup"><span data-stu-id="dff89-177">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="dff89-178">Era o comportamento desejado forçar uma atualização independentemente.</span><span class="sxs-lookup"><span data-stu-id="dff89-178">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="dff89-179">2.1 do NuGet aborda isso com o sinalizador 'reinstalar'.</span><span class="sxs-lookup"><span data-stu-id="dff89-179">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="dff89-180">Por exemplo, as versões anteriores do NuGet resultaria no seguinte ao tentar atualizar um pacote que não tem uma versão mais recente do pacote:</span><span class="sxs-lookup"><span data-stu-id="dff89-180">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

<span data-ttu-id="dff89-181">Com o sinalizador de reinstalação, o pacote será atualizado independentemente se há uma versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="dff89-181">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

<span data-ttu-id="dff89-182">Outro cenário em que o sinalizador de reinstalação é vantajoso é de estrutura redirecionar.</span><span class="sxs-lookup"><span data-stu-id="dff89-182">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="dff89-183">Ao alterar a estrutura de destino de um projeto (por exemplo, do .NET 4 para o .NET 4.5), Update-Package-reinstalar pode atualizar as referências aos assemblies corretos para todos os pacotes NuGet instalados no projeto.</span><span class="sxs-lookup"><span data-stu-id="dff89-183">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="dff89-184">Editar fontes de pacote dentro do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dff89-184">Edit Package Sources Within Visual Studio</span></span>

<span data-ttu-id="dff89-185">Nas versões anteriores do NuGet, atualizando uma origem de pacote a partir a caixa de diálogo de opções do Visual Studio necessária excluir e adicionar novamente a origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="dff89-185">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="dff89-186">2.1 do NuGet melhora este fluxo de trabalho com o suporte à atualização como uma função de primeira classe da interface do usuário de configuração.</span><span class="sxs-lookup"><span data-stu-id="dff89-186">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![Diálogo de configuração do Gerenciador de pacote](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="dff89-188">Correções de Bug</span><span class="sxs-lookup"><span data-stu-id="dff89-188">Bug Fixes</span></span>

<span data-ttu-id="dff89-189">2.1 do NuGet inclui muitas correções de bugs.</span><span class="sxs-lookup"><span data-stu-id="dff89-189">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="dff89-190">Para obter uma lista completa de trabalho itens corrigidos no NuGet 2.0, por favor, modo de exibição de [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="dff89-190">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
