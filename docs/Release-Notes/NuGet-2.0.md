---
title: Notas de versão 2.0 do NuGet
description: Notas de versão do NuGet 2.0, incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0e637a953d9d5d10394857a352be96a7f68dc4e8
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="9aabd-103">Notas de versão 2.0 do NuGet</span><span class="sxs-lookup"><span data-stu-id="9aabd-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="9aabd-104">[Notas de versão do NuGet 1.8](../release-notes/nuget-1.8.md) | [notas de versão 2.1 do NuGet](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="9aabd-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="9aabd-105">NuGet 2.0 foi lançada em 19 de junho de 2012.</span><span class="sxs-lookup"><span data-stu-id="9aabd-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="9aabd-106">Problema de instalação conhecidos</span><span class="sxs-lookup"><span data-stu-id="9aabd-106">Known Installation Issue</span></span>
<span data-ttu-id="9aabd-107">Se você estiver executando o VS 2010 SP1, você pode executar em um erro de instalação durante a tentativa de atualizar o NuGet se você tiver uma versão mais antiga.</span><span class="sxs-lookup"><span data-stu-id="9aabd-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="9aabd-108">A solução alternativa é simplesmente desinstalar NuGet e, em seguida, instalá-lo a partir da Galeria de extensão do VS.</span><span class="sxs-lookup"><span data-stu-id="9aabd-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="9aabd-109">Consulte [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) para obter mais informações, ou [vá diretamente para o hotfix VS](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="9aabd-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="9aabd-110">Observação: Se o Visual Studio não permitirão que você desinstalar a extensão (o botão de desinstalação estiver desabilitado), em seguida, provavelmente você precisa reiniciar o Visual Studio usando "Executar como administrador".</span><span class="sxs-lookup"><span data-stu-id="9aabd-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="9aabd-111">Consentimento de restauração do pacote agora está ativo</span><span class="sxs-lookup"><span data-stu-id="9aabd-111">Package restore consent is now active</span></span>

<span data-ttu-id="9aabd-112">Conforme descrito neste [postar no pacote restauração consentimento](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 agora exigirá que receber consentimento para permitir a restauração do pacote ficar online e baixar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="9aabd-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="9aabd-113">Certifique-se de que você forneceu consentimento via o diálogo de configuração do Gerenciador de pacote ou a variável de ambiente EnableNuGetPackageRestore.</span><span class="sxs-lookup"><span data-stu-id="9aabd-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="9aabd-114">Dependências de grupo pela estrutura de destino</span><span class="sxs-lookup"><span data-stu-id="9aabd-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="9aabd-115">Dependências podem variar de pacote a partir da versão 2.0, baseada no perfil de estrutura de projeto de destino.</span><span class="sxs-lookup"><span data-stu-id="9aabd-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="9aabd-116">Isso é feito usando atualizada `.nuspec` esquema.</span><span class="sxs-lookup"><span data-stu-id="9aabd-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="9aabd-117">O `<dependencies>` elemento agora pode conter um conjunto de `<group>` elementos.</span><span class="sxs-lookup"><span data-stu-id="9aabd-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="9aabd-118">Cada grupo contém zero ou mais `<dependency>` elementos e um `targetFramework` atributo.</span><span class="sxs-lookup"><span data-stu-id="9aabd-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="9aabd-119">Todas as dependências dentro de um grupo são instaladas juntos, se a estrutura de destino é compatível com o perfil de estrutura de projeto de destino.</span><span class="sxs-lookup"><span data-stu-id="9aabd-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="9aabd-120">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9aabd-120">For example:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<span data-ttu-id="9aabd-121">Observe que um grupo pode conter **zero** dependências.</span><span class="sxs-lookup"><span data-stu-id="9aabd-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="9aabd-122">No exemplo acima, se o pacote for instalado em um projeto que tem como alvo o Silverlight 3.0 ou posterior, nenhuma dependência será instalada.</span><span class="sxs-lookup"><span data-stu-id="9aabd-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="9aabd-123">Se o pacote for instalado em um projeto que tem como alvo o .NET 4.0 ou posterior, duas dependências, jQuery e WebActivator, serão instaladas.</span><span class="sxs-lookup"><span data-stu-id="9aabd-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="9aabd-124">Se o pacote for instalado em um projeto que tem como alvo uma versão anterior dessas estruturas de 2 ou qualquer outra estrutura, RouteMagic 1.1.0 será instalado.</span><span class="sxs-lookup"><span data-stu-id="9aabd-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="9aabd-125">Não há nenhuma herança entre grupos.</span><span class="sxs-lookup"><span data-stu-id="9aabd-125">There is no inheritance between groups.</span></span> <span data-ttu-id="9aabd-126">Se a estrutura de destino do projeto corresponde a `targetFramework` atributo de um grupo, somente as dependências dentro desse grupo será instalado.</span><span class="sxs-lookup"><span data-stu-id="9aabd-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="9aabd-127">Um pacote pode especificar as dependências do pacote em um dos dois formatos: o formato antigo de uma lista simples de `<dependency>` elementos ou grupos.</span><span class="sxs-lookup"><span data-stu-id="9aabd-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="9aabd-128">Se o `<group>` formato é usado, o pacote não pode ser instalado em versões anteriores à 2.0 do NuGet.</span><span class="sxs-lookup"><span data-stu-id="9aabd-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="9aabd-129">Observe que não é permitido misturar os dois formatos.</span><span class="sxs-lookup"><span data-stu-id="9aabd-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="9aabd-130">Por exemplo, o trecho a seguir é **inválido** e serão rejeitadas pelo NuGet.</span><span class="sxs-lookup"><span data-stu-id="9aabd-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="9aabd-131">Agrupando arquivos de conteúdo e scripts do PowerShell do framework de destino</span><span class="sxs-lookup"><span data-stu-id="9aabd-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="9aabd-132">Além de referências de assembly, arquivos de conteúdo e scripts do PowerShell também podem ser agrupados pela estrutura de destino.</span><span class="sxs-lookup"><span data-stu-id="9aabd-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="9aabd-133">A mesma estrutura de pasta encontrado no `lib` agora pode ser aplicada a pasta para especificar a estrutura de destino da mesma forma para o `content` e `tools` pastas.</span><span class="sxs-lookup"><span data-stu-id="9aabd-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="9aabd-134">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9aabd-134">For example:</span></span>

    \content
        \net11
            \MyContent.txt
        \net20
            \MyContent20.txt
        \net40
        \sl40
            \MySilverlightContent.html

    \tools
        \init.ps1
        \net40
            \install.ps1
            \uninstall.ps1
        \sl40
            \install.ps1
            \uninstall.ps1

<span data-ttu-id="9aabd-135">**Observação**: porque `init.ps1` é executada no nível da solução e é independente de qualquer projeto individual, ele deve ser colocado diretamente sob o `tools` pasta.</span><span class="sxs-lookup"><span data-stu-id="9aabd-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="9aabd-136">Se colocado dentro de uma pasta específica da estrutura, ele será ignorado.</span><span class="sxs-lookup"><span data-stu-id="9aabd-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="9aabd-137">Além disso, um novo recurso do NuGet 2.0 é que uma pasta da estrutura pode ser *vazio*, nesse caso, o NuGet não adicionará referências de assembly, adicionar arquivos de conteúdo ou executar scripts do PowerShell para a versão do framework específico.</span><span class="sxs-lookup"><span data-stu-id="9aabd-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="9aabd-138">No exemplo acima, a pasta `content\net40` está vazio.</span><span class="sxs-lookup"><span data-stu-id="9aabd-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="9aabd-139">Desempenho de conclusão de guia aprimorado</span><span class="sxs-lookup"><span data-stu-id="9aabd-139">Improved tab completion performance</span></span>
<span data-ttu-id="9aabd-140">O recurso de preenchimento no Console do Gerenciador de pacotes do NuGet foi atualizado para melhorar significativamente o desempenho.</span><span class="sxs-lookup"><span data-stu-id="9aabd-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="9aabd-141">Haverá menos atraso entre o momento em que a tecla tab é pressionada até que seja exibida a lista suspensa de sugestões.</span><span class="sxs-lookup"><span data-stu-id="9aabd-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="9aabd-142">Correções de Bug</span><span class="sxs-lookup"><span data-stu-id="9aabd-142">Bug Fixes</span></span>
<span data-ttu-id="9aabd-143">NuGet 2.0 inclui muitas correções de bugs com ênfase em consentimento de restauração do pacote e o desempenho.</span><span class="sxs-lookup"><span data-stu-id="9aabd-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="9aabd-144">Para obter uma lista completa de trabalho itens corrigidos no NuGet 2.0, por favor, exibição de [NuGet Issue Tracker para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="9aabd-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
