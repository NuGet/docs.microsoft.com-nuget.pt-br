---
title: Notas de versão do NuGet 1,5
description: Notas de versão do NuGet 1,5 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940a19cdc485d611d03b52ee3102bc95a78a36bb
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383343"
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="66a09-103">Notas de versão do NuGet 1,5</span><span class="sxs-lookup"><span data-stu-id="66a09-103">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="66a09-104">[Notas de versão do nuget 1,4](../release-notes/nuget-1.4.md) | [notas de versão do NuGet 1,6](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="66a09-104">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="66a09-105">O NuGet 1,5 foi lançado em 30 de agosto de 2011.</span><span class="sxs-lookup"><span data-stu-id="66a09-105">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="66a09-106">Recursos</span><span class="sxs-lookup"><span data-stu-id="66a09-106">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="66a09-107">Modelos de projeto com pacotes NuGet pré-instalados</span><span class="sxs-lookup"><span data-stu-id="66a09-107">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="66a09-108">Ao criar um novo modelo de projeto do ASP.NET MVC 3, as bibliotecas de script do jQuery incluídas no projeto são realmente colocadas lá instalando os pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="66a09-108">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="66a09-109">O modelo de projeto ASP.NET MVC 3 inclui um conjunto de pacotes NuGet que são instalados quando o modelo de projeto é invocado.</span><span class="sxs-lookup"><span data-stu-id="66a09-109">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="66a09-110">Essa capacidade de incluir pacotes NuGet com um modelo de projeto agora é um recurso do NuGet que _qualquer_ modelo de projeto agora pode aproveitar.</span><span class="sxs-lookup"><span data-stu-id="66a09-110">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="66a09-111">Para obter mais detalhes sobre esse recurso, leia esta [postagem de blog pelo desenvolvedor do recurso](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span><span class="sxs-lookup"><span data-stu-id="66a09-111">For more details about this feature, read this [blog post by the developer of the feature](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="66a09-112">Referências explícitas de assembly</span><span class="sxs-lookup"><span data-stu-id="66a09-112">Explicit Assembly References</span></span>

<span data-ttu-id="66a09-113">Adicionado um novo elemento `<references />` usado para especificar explicitamente quais assemblies no pacote devem ser referenciados.</span><span class="sxs-lookup"><span data-stu-id="66a09-113">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="66a09-114">Por exemplo, se você adicionar o seguinte:</span><span class="sxs-lookup"><span data-stu-id="66a09-114">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="66a09-115">Em seguida, somente os `xunit.dll` e `xunit.extensions.dll` serão referenciados da [subpasta estrutura/perfil](../reference/nuspec.md#explicit-assembly-references) apropriada da pasta `lib`, mesmo se houver outros assemblies na pasta.</span><span class="sxs-lookup"><span data-stu-id="66a09-115">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="66a09-116">Se esse elemento for omitido, o comportamento usual se aplicará, que é fazer referência a cada assembly na pasta `lib`.</span><span class="sxs-lookup"><span data-stu-id="66a09-116">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="66a09-117">__Para que esse recurso é usado?__</span><span class="sxs-lookup"><span data-stu-id="66a09-117">__What is this feature used for?__</span></span>

<span data-ttu-id="66a09-118">Esse recurso dá suporte apenas a assemblies de tempo de design.</span><span class="sxs-lookup"><span data-stu-id="66a09-118">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="66a09-119">Por exemplo, ao usar contratos de código, os assemblies de contrato precisam estar ao lado dos assemblies de tempo de execução que eles aumentam para que o Visual Studio possa encontrá-los, mas os assemblies de contrato não devem realmente ser referenciados pelo projeto e não devem ser copiados para a pasta `bin`.</span><span class="sxs-lookup"><span data-stu-id="66a09-119">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="66a09-120">Da mesma forma, o recurso pode ser usado para estruturas de teste de unidade, como XUnit, que precisam que seus assemblies de ferramentas estejam localizados ao lado dos assemblies de tempo de execução, mas excluídos de referências de projeto.</span><span class="sxs-lookup"><span data-stu-id="66a09-120">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="66a09-121">Capacidade adicional de excluir arquivos no. nuspec</span><span class="sxs-lookup"><span data-stu-id="66a09-121">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="66a09-122">O elemento `<file>` dentro de um arquivo de `.nuspec` pode ser usado para incluir um arquivo específico ou um conjunto de arquivos usando um caractere curinga.</span><span class="sxs-lookup"><span data-stu-id="66a09-122">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="66a09-123">Ao usar um caractere curinga, não há como excluir um subconjunto específico dos arquivos incluídos.</span><span class="sxs-lookup"><span data-stu-id="66a09-123">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="66a09-124">Por exemplo, suponha que você queira todos os arquivos de texto dentro de uma pasta, exceto um específico.</span><span class="sxs-lookup"><span data-stu-id="66a09-124">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="66a09-125">Use ponto e vírgula para especificar vários arquivos.</span><span class="sxs-lookup"><span data-stu-id="66a09-125">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="66a09-126">Ou use um curinga para excluir um conjunto de arquivos, como todos os arquivos de backup</span><span class="sxs-lookup"><span data-stu-id="66a09-126">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="66a09-127">Removendo pacotes usando os prompts da caixa de diálogo para remover dependências</span><span class="sxs-lookup"><span data-stu-id="66a09-127">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="66a09-128">Ao desinstalar um pacote com dependências, os prompts do NuGet, permitindo a remoção das dependências de um pacote junto com o pacote.</span><span class="sxs-lookup"><span data-stu-id="66a09-128">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![Removendo pacotes dependentes](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="66a09-130">aperfeiçoamento do comando `Get-Package`</span><span class="sxs-lookup"><span data-stu-id="66a09-130">`Get-Package` command improvement</span></span>
<span data-ttu-id="66a09-131">O comando `Get-Package` agora dá suporte a um parâmetro `-ProjectName`.</span><span class="sxs-lookup"><span data-stu-id="66a09-131">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="66a09-132">Portanto, o comando</span><span class="sxs-lookup"><span data-stu-id="66a09-132">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="66a09-133">listará todos os pacotes instalados no projeto A.</span><span class="sxs-lookup"><span data-stu-id="66a09-133">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="66a09-134">Suporte para proxies que exigem autenticação</span><span class="sxs-lookup"><span data-stu-id="66a09-134">Support for Proxies that require authentication</span></span>
<span data-ttu-id="66a09-135">Ao usar o NuGet por trás de um proxy que requer autenticação, o NuGet agora solicitará credenciais de proxy.</span><span class="sxs-lookup"><span data-stu-id="66a09-135">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="66a09-136">A inserção de credenciais permite que o NuGet se conecte ao repositório remoto.</span><span class="sxs-lookup"><span data-stu-id="66a09-136">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="66a09-137">Suporte para repositórios que exigem autenticação</span><span class="sxs-lookup"><span data-stu-id="66a09-137">Support for Repositories that require authentication</span></span>
<span data-ttu-id="66a09-138">O NuGet agora dá suporte à conexão com [repositórios privados](../hosting-packages/local-feeds.md) que exigem autenticação básica ou NTLM.</span><span class="sxs-lookup"><span data-stu-id="66a09-138">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="66a09-139">O suporte para autenticação Digest será adicionado em uma versão futura.</span><span class="sxs-lookup"><span data-stu-id="66a09-139">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="66a09-140">Melhorias de desempenho no repositório nuget.org</span><span class="sxs-lookup"><span data-stu-id="66a09-140">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="66a09-141">Fizemos várias melhorias de desempenho na Galeria de nuget.org para tornar a listagem e a pesquisa de pacotes mais rápidas.</span><span class="sxs-lookup"><span data-stu-id="66a09-141">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="66a09-142">Filtragem de projeto de caixa de diálogo de solução</span><span class="sxs-lookup"><span data-stu-id="66a09-142">Solution dialog project filtering</span></span>
<span data-ttu-id="66a09-143">Na caixa de diálogo nível da solução, ao solicitar quais projetos instalar, mostramos apenas os projetos que são compatíveis com o pacote selecionado.</span><span class="sxs-lookup"><span data-stu-id="66a09-143">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="66a09-144">Notas de versão do pacote</span><span class="sxs-lookup"><span data-stu-id="66a09-144">Package Release Notes</span></span>
<span data-ttu-id="66a09-145">Agora, os pacotes NuGet incluem suporte para notas de versão.</span><span class="sxs-lookup"><span data-stu-id="66a09-145">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="66a09-146">As notas de versão aparecem apenas ao exibir _atualizações_ para um pacote, portanto, não faz sentido adicioná-las à sua primeira versão.</span><span class="sxs-lookup"><span data-stu-id="66a09-146">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![Notas de versão na guia Atualizações](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="66a09-148">Para adicionar notas de versão a um pacote, use o novo elemento de metadados `<releaseNotes />` em seu arquivo NuSpec.</span><span class="sxs-lookup"><span data-stu-id="66a09-148">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="66a09-149">. nuspec & melhoria de ltfiles/&gt;</span><span class="sxs-lookup"><span data-stu-id="66a09-149">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="66a09-150">O arquivo de `.nuspec` agora permite o elemento de `<files />` vazio, o que informa ao NuGet. exe para não incluir nenhum arquivo no pacote.</span><span class="sxs-lookup"><span data-stu-id="66a09-150">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="66a09-151">Correções de Bug</span><span class="sxs-lookup"><span data-stu-id="66a09-151">Bug Fixes</span></span>
<span data-ttu-id="66a09-152">O NuGet 1,5 tinha um total de 107 itens de trabalho corrigidos.</span><span class="sxs-lookup"><span data-stu-id="66a09-152">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="66a09-153">103 deles foram marcados como bugs.</span><span class="sxs-lookup"><span data-stu-id="66a09-153">103 of those were marked as bugs.</span></span>

<span data-ttu-id="66a09-154">Para obter uma lista completa de itens de trabalho corrigidos no NuGet 1,5, consulte o [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="66a09-154">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="66a09-155">Correções de bugs vale a pena observar:</span><span class="sxs-lookup"><span data-stu-id="66a09-155">Bug fixes worth noting:</span></span>

* <span data-ttu-id="66a09-156">[Problema 1273](http://nuget.codeplex.com/workitem/1273): fez `packages.config` mais controle de versão amigável classificando os pacotes em ordem alfabética e removendo espaços em branco extras.</span><span class="sxs-lookup"><span data-stu-id="66a09-156">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="66a09-157">[Problema 844](http://nuget.codeplex.com/workitem/844): os números de versão agora são normalizados para que `Install-Package 1.0` funcione em um pacote com a versão `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="66a09-157">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="66a09-158">[Problema 1060](http://nuget.codeplex.com/workitem/1060): ao criar um pacote usando NuGet. exe, o sinalizador `-Version` substitui o elemento `<version />`.</span><span class="sxs-lookup"><span data-stu-id="66a09-158">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
