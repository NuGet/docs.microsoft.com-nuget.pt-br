---
title: Notas de versão do NuGet 2,0
description: Notas de versão do NuGet 2,0 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 01fdbfafcaea009cf119dfa880b2b16539c9b088
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383061"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="258de-103">Notas de versão do NuGet 2,0</span><span class="sxs-lookup"><span data-stu-id="258de-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="258de-104">[Notas de versão do nuget 1,8](../release-notes/nuget-1.8.md) | [notas de versão do NuGet 2,1](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="258de-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="258de-105">O NuGet 2,0 foi lançado em 19 de junho de 2012.</span><span class="sxs-lookup"><span data-stu-id="258de-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="258de-106">Problema de instalação conhecido</span><span class="sxs-lookup"><span data-stu-id="258de-106">Known Installation Issue</span></span>
<span data-ttu-id="258de-107">Se você estiver executando o VS 2010 SP1, poderá encontrar um erro de instalação ao tentar atualizar o NuGet se tiver uma versão mais antiga instalada.</span><span class="sxs-lookup"><span data-stu-id="258de-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="258de-108">A solução alternativa é simplesmente desinstalar o NuGet e, em seguida, instalá-lo a partir da Galeria de extensões do VS.</span><span class="sxs-lookup"><span data-stu-id="258de-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="258de-109">Consulte <https://support.microsoft.com/kb/2581019> para obter mais informações ou [vá diretamente para o hotfix do vs](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="258de-109">See <https://support.microsoft.com/kb/2581019> for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="258de-110">Observação: se o Visual Studio não permitir que você desinstale a extensão (o botão desinstalar está desabilitado), provavelmente, você precisará reiniciar o Visual Studio usando "executar como administrador".</span><span class="sxs-lookup"><span data-stu-id="258de-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="258de-111">O consentimento de restauração do pacote agora está ativo</span><span class="sxs-lookup"><span data-stu-id="258de-111">Package restore consent is now active</span></span>

<span data-ttu-id="258de-112">Conforme descrito nesta [postagem no consentimento de restauração de pacote](http://blog.nuget.org/20120518/package-restore-and-consent.html), o NuGet 2,0 agora exigirá que o consentimento seja fornecido para habilitar a restauração do pacote para ficar online e baixar pacotes.</span><span class="sxs-lookup"><span data-stu-id="258de-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="258de-113">Verifique se você forneceu o consentimento por meio da caixa de diálogo configuração do Gerenciador de pacotes ou da variável de ambiente EnableNuGetPackageRestore.</span><span class="sxs-lookup"><span data-stu-id="258de-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="258de-114">Agrupar dependências por estruturas de destino</span><span class="sxs-lookup"><span data-stu-id="258de-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="258de-115">A partir da versão 2,0, as dependências de pacote podem variar com base no perfil de estrutura do projeto de destino.</span><span class="sxs-lookup"><span data-stu-id="258de-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="258de-116">Isso é feito usando um esquema de `.nuspec` atualizado.</span><span class="sxs-lookup"><span data-stu-id="258de-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="258de-117">O elemento `<dependencies>` agora pode conter um conjunto de elementos `<group>`.</span><span class="sxs-lookup"><span data-stu-id="258de-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="258de-118">Cada grupo contém zero ou mais elementos `<dependency>` e um atributo `targetFramework`.</span><span class="sxs-lookup"><span data-stu-id="258de-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="258de-119">Todas as dependências dentro de um grupo serão instaladas juntas se a estrutura de destino for compatível com o perfil de estrutura do projeto de destino.</span><span class="sxs-lookup"><span data-stu-id="258de-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="258de-120">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="258de-120">For example:</span></span>

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

<span data-ttu-id="258de-121">Observe que um grupo pode conter **zero** dependências.</span><span class="sxs-lookup"><span data-stu-id="258de-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="258de-122">No exemplo acima, se o pacote for instalado em um projeto direcionado ao Silverlight 3,0 ou posterior, nenhuma dependência será instalada.</span><span class="sxs-lookup"><span data-stu-id="258de-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="258de-123">Se o pacote for instalado em um projeto direcionado ao .NET 4,0 ou posterior, duas dependências, jQuery e webactivator serão instaladas.</span><span class="sxs-lookup"><span data-stu-id="258de-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="258de-124">Se o pacote for instalado em um projeto direcionado a uma versão anterior dessas duas estruturas, ou qualquer outra estrutura, o RouteMagic 1.1.0 será instalado.</span><span class="sxs-lookup"><span data-stu-id="258de-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="258de-125">Não há herança entre grupos.</span><span class="sxs-lookup"><span data-stu-id="258de-125">There is no inheritance between groups.</span></span> <span data-ttu-id="258de-126">Se a estrutura de destino de um projeto corresponder ao atributo `targetFramework` de um grupo, somente as dependências dentro desse grupo serão instaladas.</span><span class="sxs-lookup"><span data-stu-id="258de-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="258de-127">Um pacote pode especificar dependências de pacote em um dos dois formatos: o formato antigo de uma lista simples de elementos de `<dependency>` ou grupos.</span><span class="sxs-lookup"><span data-stu-id="258de-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="258de-128">Se o formato de `<group>` for usado, o pacote não poderá ser instalado em versões do NuGet anteriores a 2,0.</span><span class="sxs-lookup"><span data-stu-id="258de-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="258de-129">Observe que a combinação dos dois formatos não é permitida.</span><span class="sxs-lookup"><span data-stu-id="258de-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="258de-130">Por exemplo, o trecho a seguir é **inválido** e será rejeitado pelo NuGet.</span><span class="sxs-lookup"><span data-stu-id="258de-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="258de-131">Agrupando arquivos de conteúdo e scripts do PowerShell por estrutura de destino</span><span class="sxs-lookup"><span data-stu-id="258de-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="258de-132">Além das referências de assembly, os arquivos de conteúdo e os scripts do PowerShell também podem ser agrupados por estrutura de destino.</span><span class="sxs-lookup"><span data-stu-id="258de-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="258de-133">A mesma estrutura de pastas encontrada na pasta `lib` para especificar a estrutura de destino agora pode ser aplicada da mesma maneira com as pastas `content` e `tools`.</span><span class="sxs-lookup"><span data-stu-id="258de-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="258de-134">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="258de-134">For example:</span></span>

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

<span data-ttu-id="258de-135">**Observação**: como `init.ps1` é executado no nível da solução e não é dependente de nenhum projeto individual, ele deve ser colocado diretamente na pasta `tools`.</span><span class="sxs-lookup"><span data-stu-id="258de-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="258de-136">Se colocado em uma pasta específica da estrutura, ele será ignorado.</span><span class="sxs-lookup"><span data-stu-id="258de-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="258de-137">Além disso, um novo recurso no NuGet 2,0 é que uma pasta de estrutura pode estar *vazia*, nesse caso, o NuGet não adicionará referências de assembly, adicionará arquivos de conteúdo ou executará scripts do PowerShell para a versão específica do Framework.</span><span class="sxs-lookup"><span data-stu-id="258de-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="258de-138">No exemplo acima, a pasta `content\net40` está vazia.</span><span class="sxs-lookup"><span data-stu-id="258de-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="258de-139">Desempenho de preenchimento com Tab aprimorado</span><span class="sxs-lookup"><span data-stu-id="258de-139">Improved tab completion performance</span></span>
<span data-ttu-id="258de-140">O recurso de preenchimento de guia no console do Gerenciador de pacotes NuGet foi atualizado para melhorar significativamente o desempenho.</span><span class="sxs-lookup"><span data-stu-id="258de-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="258de-141">Haverá muito menos atraso desde o momento em que a tecla Tab é pressionada até que a lista suspensa de sugestões seja exibida.</span><span class="sxs-lookup"><span data-stu-id="258de-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="258de-142">Correções de Bug</span><span class="sxs-lookup"><span data-stu-id="258de-142">Bug Fixes</span></span>
<span data-ttu-id="258de-143">O NuGet 2,0 inclui muitas correções de bugs com ênfase no consentimento e no desempenho da restauração de pacotes.</span><span class="sxs-lookup"><span data-stu-id="258de-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="258de-144">Para obter uma lista completa de itens de trabalho corrigidos no NuGet 2,0, consulte o [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="258de-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
