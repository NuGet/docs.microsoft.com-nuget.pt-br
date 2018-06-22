---
title: Notas de versão 1.5 do NuGet
description: Notas de versão do NuGet 1.5 incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1f2f7ebe718ce943faa31b7e19395eead8726648
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821337"
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="377f7-103">Notas de versão 1.5 do NuGet</span><span class="sxs-lookup"><span data-stu-id="377f7-103">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="377f7-104">[Notas de versão do NuGet 1.4](../release-notes/nuget-1.4.md) | [notas de versão 1.6 do NuGet](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="377f7-104">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="377f7-105">1.5 NuGet foi lançada em 30 de agosto de 2011.</span><span class="sxs-lookup"><span data-stu-id="377f7-105">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="377f7-106">Recursos</span><span class="sxs-lookup"><span data-stu-id="377f7-106">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="377f7-107">Modelos de projeto com pacotes do NuGet pré-instalado</span><span class="sxs-lookup"><span data-stu-id="377f7-107">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="377f7-108">Ao criar um novo modelo de projeto do ASP.NET MVC 3, as bibliotecas de scripts jQuery incluídas no projeto, na verdade, são colocadas nesse local instalando pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="377f7-108">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="377f7-109">O modelo de projeto do ASP.NET MVC 3 inclui um conjunto de pacotes do NuGet é instalado quando o modelo de projeto é invocado.</span><span class="sxs-lookup"><span data-stu-id="377f7-109">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="377f7-110">Essa capacidade de incluir pacotes do NuGet com um modelo de projeto agora é um recurso do NuGet que _qualquer_ modelo de projeto agora pode tirar proveito do.</span><span class="sxs-lookup"><span data-stu-id="377f7-110">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="377f7-111">Para obter mais detalhes sobre esse recurso, leia este [postagem de blog pelo desenvolvedor do recurso](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span><span class="sxs-lookup"><span data-stu-id="377f7-111">For more details about this feature, read this [blog post by the developer of the feature](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="377f7-112">Referências de Assembly explícita</span><span class="sxs-lookup"><span data-stu-id="377f7-112">Explicit Assembly References</span></span>

<span data-ttu-id="377f7-113">Adicionado um novo `<references />` usado para especificar explicitamente os assemblies dentro do elemento de pacote deve ser referenciado.</span><span class="sxs-lookup"><span data-stu-id="377f7-113">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="377f7-114">Por exemplo, se você adicionar o seguinte:</span><span class="sxs-lookup"><span data-stu-id="377f7-114">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="377f7-115">E somente a `xunit.dll` e `xunit.extensions.dll` será referenciado do apropriada [framework/perfil](../reference/nuspec.md#explicit-assembly-references) do `lib` pasta mesmo se houver outros assemblies na pasta.</span><span class="sxs-lookup"><span data-stu-id="377f7-115">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="377f7-116">Se esse elemento for omitido, o comportamento comum se aplica, que é fazer referência a cada assembly no `lib` pasta.</span><span class="sxs-lookup"><span data-stu-id="377f7-116">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="377f7-117">__O que esse recurso é usado?__</span><span class="sxs-lookup"><span data-stu-id="377f7-117">__What is this feature used for?__</span></span>

<span data-ttu-id="377f7-118">Esse recurso oferece suporte a apenas assemblies de tempo de design.</span><span class="sxs-lookup"><span data-stu-id="377f7-118">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="377f7-119">Por exemplo, ao usar contratos de código, os assemblies de contrato precisam ser próximo os assemblies de tempo de execução que eles aumentar para que o Visual Studio pode encontrá-los, mas os assemblies de contrato, na verdade, não devem ser referenciados pelo projeto e não devem ser copiados para o `bin` pasta.</span><span class="sxs-lookup"><span data-stu-id="377f7-119">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="377f7-120">Da mesma forma, o recurso pode ser usado para estruturas de teste de unidade como XUnit que precisam de seus conjuntos de ferramentas localizada ao lado de assemblies de tempo de execução, mas excluídas de referências de projeto.</span><span class="sxs-lookup"><span data-stu-id="377f7-120">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="377f7-121">Foi incluída a capacidade de excluir os arquivos. o NuSpec</span><span class="sxs-lookup"><span data-stu-id="377f7-121">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="377f7-122">O `<file>` elemento dentro de um `.nuspec` arquivo pode ser usado para incluir um arquivo específico ou um conjunto de arquivos usando um curinga.</span><span class="sxs-lookup"><span data-stu-id="377f7-122">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="377f7-123">Ao usar um caractere curinga, não é possível excluir um subconjunto específico de arquivos incluídos.</span><span class="sxs-lookup"><span data-stu-id="377f7-123">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="377f7-124">Por exemplo, suponha que você deseja que todos os arquivos de texto dentro de uma pasta, exceto um específico.</span><span class="sxs-lookup"><span data-stu-id="377f7-124">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="377f7-125">Use ponto e vírgula para especificar vários arquivos.</span><span class="sxs-lookup"><span data-stu-id="377f7-125">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="377f7-126">Ou use um caractere curinga para excluir um conjunto de arquivos, como todos os arquivos de backup</span><span class="sxs-lookup"><span data-stu-id="377f7-126">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="377f7-127">Remover pacotes usando a caixa de diálogo solicita para remover dependências</span><span class="sxs-lookup"><span data-stu-id="377f7-127">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="377f7-128">Quando você desinstala um pacote com dependências, solicita que o NuGet, que permite a remoção de dependências do pacote junto com o pacote.</span><span class="sxs-lookup"><span data-stu-id="377f7-128">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![Removendo pacotes dependentes](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="377f7-130">`Get-Package` Aperfeiçoamento de comando</span><span class="sxs-lookup"><span data-stu-id="377f7-130">`Get-Package` command improvement</span></span>
<span data-ttu-id="377f7-131">O `Get-Package` comando agora dá suporte a um `-ProjectName` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="377f7-131">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="377f7-132">Portanto o comando</span><span class="sxs-lookup"><span data-stu-id="377f7-132">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="377f7-133">lista todos os pacotes instalados no projeto A.</span><span class="sxs-lookup"><span data-stu-id="377f7-133">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="377f7-134">Suporte para Proxies que requer autenticação</span><span class="sxs-lookup"><span data-stu-id="377f7-134">Support for Proxies that require authentication</span></span>
<span data-ttu-id="377f7-135">Ao usar o NuGet atrás de um proxy que requer autenticação, NuGet agora solicitará as credenciais de proxy.</span><span class="sxs-lookup"><span data-stu-id="377f7-135">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="377f7-136">Inserir credenciais permite que o NuGet para se conectar ao repositório remoto.</span><span class="sxs-lookup"><span data-stu-id="377f7-136">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="377f7-137">Suporte para repositórios que requer autenticação</span><span class="sxs-lookup"><span data-stu-id="377f7-137">Support for Repositories that require authentication</span></span>
<span data-ttu-id="377f7-138">NuGet agora dá suporte ao conectar-se a [repositórios privados](../hosting-packages/local-feeds.md) que exigem autenticação básica ou NTLM.</span><span class="sxs-lookup"><span data-stu-id="377f7-138">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="377f7-139">Suporte para a autenticação Digest será adicionado em uma versão futura.</span><span class="sxs-lookup"><span data-stu-id="377f7-139">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="377f7-140">Aprimoramentos de desempenho para o repositório nuget.org</span><span class="sxs-lookup"><span data-stu-id="377f7-140">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="377f7-141">Fizemos vários aprimoramentos de desempenho para a Galeria nuget.org para tornar o pacote de listagem e a pesquisa mais rápida.</span><span class="sxs-lookup"><span data-stu-id="377f7-141">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="377f7-142">A filtragem do projeto da caixa de diálogo de solução</span><span class="sxs-lookup"><span data-stu-id="377f7-142">Solution dialog project filtering</span></span>
<span data-ttu-id="377f7-143">No diálogo nível de solução, ao pedir que projetos instalar, mostramos somente projetos que são compatíveis com o pacote selecionado.</span><span class="sxs-lookup"><span data-stu-id="377f7-143">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="377f7-144">Notas de versão do pacote</span><span class="sxs-lookup"><span data-stu-id="377f7-144">Package Release Notes</span></span>
<span data-ttu-id="377f7-145">Pacotes do NuGet agora incluem suporte para notas de versão.</span><span class="sxs-lookup"><span data-stu-id="377f7-145">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="377f7-146">As notas de versão só mostra backup ao exibir _atualizações_ para um pacote, portanto não faz sentido para adicioná-los para sua primeira versão.</span><span class="sxs-lookup"><span data-stu-id="377f7-146">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![Notas de versão na guia atualizações](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="377f7-148">Para adicionar notas de versão para um pacote, use o novo `<releaseNotes />` elemento de metadados em seu arquivo NuSpec.</span><span class="sxs-lookup"><span data-stu-id="377f7-148">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="377f7-149">. NuSpec & ltfiles /&gt; aperfeiçoamento</span><span class="sxs-lookup"><span data-stu-id="377f7-149">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="377f7-150">O `.nuspec` arquivo agora permite vazio `<files />` elemento, que informa o nuget.exe para não incluir qualquer arquivo no pacote.</span><span class="sxs-lookup"><span data-stu-id="377f7-150">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="377f7-151">Correções de Bug</span><span class="sxs-lookup"><span data-stu-id="377f7-151">Bug Fixes</span></span>
<span data-ttu-id="377f7-152">1.5 NuGet tinha um total de 107 fixos de itens de trabalho.</span><span class="sxs-lookup"><span data-stu-id="377f7-152">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="377f7-153">103 deles foram marcadas como bugs.</span><span class="sxs-lookup"><span data-stu-id="377f7-153">103 of those were marked as bugs.</span></span>

<span data-ttu-id="377f7-154">Para obter uma lista completa de trabalho itens corrigidos no NuGet 1.5, por favor, exibição de [NuGet Issue Tracker para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="377f7-154">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="377f7-155">Correções de bug, vale a pena observar:</span><span class="sxs-lookup"><span data-stu-id="377f7-155">Bug fixes worth noting:</span></span>

* <span data-ttu-id="377f7-156">[Problema 1273](http://nuget.codeplex.com/workitem/1273): feitas `packages.config` mais controle de versão amigável classificação pacotes em ordem alfabética e removendo o espaço em branco extra.</span><span class="sxs-lookup"><span data-stu-id="377f7-156">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="377f7-157">[Problema 844](http://nuget.codeplex.com/workitem/844): números de versão agora são normalizados para que `Install-Package 1.0` funciona em um pacote com a versão `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="377f7-157">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="377f7-158">[Problema 1060](http://nuget.codeplex.com/workitem/1060): ao criar um pacote usando o nuget.exe, o `-Version` sinalizador substituições de `<version />` elemento.</span><span class="sxs-lookup"><span data-stu-id="377f7-158">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
