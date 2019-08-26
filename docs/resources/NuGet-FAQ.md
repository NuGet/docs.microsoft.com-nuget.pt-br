---
title: Perguntas frequentes do NuGet
description: Perguntas e respostas comuns sobre como usar o NuGet na linha de comando e no Visual Studio
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9b12b1fa27308cf41b58b0c244ea648d3eecdc95
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69520386"
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="40ec3-103">Perguntas frequentes do NuGet</span><span class="sxs-lookup"><span data-stu-id="40ec3-103">NuGet frequently-asked questions</span></span>

<span data-ttu-id="40ec3-104">**O que é necessário para executar o NuGet?**</span><span class="sxs-lookup"><span data-stu-id="40ec3-104">**What is required to run NuGet?**</span></span>

<span data-ttu-id="40ec3-105">Todas as informações sobre a interface do usuário e as ferramentas de linha de comando estão disponíveis na [Guia de instalação](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="40ec3-105">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="40ec3-106">**O NuGet é compatível com o Mono?**</span><span class="sxs-lookup"><span data-stu-id="40ec3-106">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="40ec3-107">A ferramenta de linha de comando, `nuget.exe`, compila e executa em Mono 3.2 e superior, e pode criar pacotes em Mono.</span><span class="sxs-lookup"><span data-stu-id="40ec3-107">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="40ec3-108">Embora `nuget.exe` funcione completamente no Windows, existem alguns problemas conhecidos no Linux e no OS X. Consulte [Problemas do Mono](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) no GitHub.</span><span class="sxs-lookup"><span data-stu-id="40ec3-108">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="40ec3-109">Um [cliente gráfico](https://github.com/mrward/monodevelop-nuget-addin) está disponível como um suplemento para MonoDevelop.</span><span class="sxs-lookup"><span data-stu-id="40ec3-109">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="40ec3-110">**Como fazer para determinar o que um pacote contém e se ele é estável e útil para meu aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="40ec3-110">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="40ec3-111">A origem primária para aprender sobre um pacote é a página de listagem em nuget.org (ou outro feed privado).</span><span class="sxs-lookup"><span data-stu-id="40ec3-111">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="40ec3-112">Cada página do pacote em nuget.org inclui uma descrição do pacote, seu histórico de versão e as estatísticas de uso.</span><span class="sxs-lookup"><span data-stu-id="40ec3-112">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="40ec3-113">A seção **Informações** na página do pacote também contém um link para o site da Web do projeto em que você normalmente encontrar muitos exemplos e documentação para ajudá-lo a aprender como o pacote é usado.</span><span class="sxs-lookup"><span data-stu-id="40ec3-113">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="40ec3-114">Para obter mais informações, consulte [Localizando e escolhendo pacotes](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="40ec3-114">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="40ec3-115">NuGet no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="40ec3-115">NuGet in Visual Studio</span></span>

<span data-ttu-id="40ec3-116">**Como é a compatibilidade do NuGet com os diferentes produtos do Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="40ec3-116">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="40ec3-117">O Visual Studio no Windows é compatível com a [Interface do usuário do Gerenciador de Pacotes](../consume-packages/install-use-packages-visual-studio.md) e o [Console do Gerenciador de Pacotes](../consume-packages/install-use-packages-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="40ec3-117">Visual Studio on Windows supports the [Package Manager UI](../consume-packages/install-use-packages-visual-studio.md) and the [Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>
- <span data-ttu-id="40ec3-118">O Visual Studio para Mac tem recursos internos do NuGet, conforme descrito em [Incluindo um pacote do NuGet em seu projeto](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="40ec3-118">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="40ec3-119">O Visual Studio Code (todas as plataformas) não tem nenhuma integração direta do NuGet.</span><span class="sxs-lookup"><span data-stu-id="40ec3-119">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="40ec3-120">Usar a [CLI do NuGet](../reference/nuget-exe-cli-reference.md) ou a [CLI do dotnet](../reference/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="40ec3-120">Use the [NuGet CLI](../reference/nuget-exe-cli-reference.md) or the [dotnet CLI](../reference/dotnet-commands.md).</span></span>
- <span data-ttu-id="40ec3-121">O Azure DevOps fornece [uma etapa de build para restaurar os pacotes do NuGet](/vsts/build-release/tasks/package/nuget).</span><span class="sxs-lookup"><span data-stu-id="40ec3-121">Azure DevOps provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="40ec3-122">Você também pode [hospedar feeds privados de pacote do NuGet no Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="40ec3-122">You can also [host private NuGet package feeds on Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).</span></span>

<span data-ttu-id="40ec3-123">**Como fazer para verificar a versão exata das ferramentas do NuGet que estão instaladas?**</span><span class="sxs-lookup"><span data-stu-id="40ec3-123">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="40ec3-124">No Visual Studio, use o comando **Ajuda > Sobre o Microsoft Visual Studio** e examine a versão exibida ao lado de **Gerenciador de Pacotes do NuGet**.</span><span class="sxs-lookup"><span data-stu-id="40ec3-124">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="40ec3-125">Como alternativa, inicie o Console do Gerenciador de Pacotes (**Ferramentas > Gerenciador de Pacotes do NuGet > Console do Gerenciador de Pacotes**) e digite `$host` para ver informações sobre o NuGet, incluindo a versão.</span><span class="sxs-lookup"><span data-stu-id="40ec3-125">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="40ec3-126">**Quais linguagens de programação são compatíveis com o NuGet?**</span><span class="sxs-lookup"><span data-stu-id="40ec3-126">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="40ec3-127">O NuGet geralmente funciona para linguagens .NET e foi projetado para trazer bibliotecas .NET em um projeto.</span><span class="sxs-lookup"><span data-stu-id="40ec3-127">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="40ec3-128">Como também há suporte para a automação do MSBuild e do Visual Studio em alguns tipos de projeto, também há suporte para outros projetos e idiomas em diversos níveis.</span><span class="sxs-lookup"><span data-stu-id="40ec3-128">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="40ec3-129">A versão mais recente do NuGet é compatível com C#, Visual Basic, F#, WiX e C++.</span><span class="sxs-lookup"><span data-stu-id="40ec3-129">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="40ec3-130">**Quais modelos de projeto são compatíveis com o NuGet?**</span><span class="sxs-lookup"><span data-stu-id="40ec3-130">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="40ec3-131">O NuGet tem suporte completo para uma variedade de modelos de projeto como Windows, Web, Cloud, SharePoint, Wix e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="40ec3-131">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="40ec3-132">**Como fazer para atualizar pacotes que fazem parte dos modelos do Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="40ec3-132">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="40ec3-133">Acesse a guia **Atualizações** na interface do usuário do Gerenciador de Pacotes e selecione **Atualizar tudo** [ou use o comando `Update-Package`](../reference/ps-reference/ps-ref-update-package.md) do Console do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="40ec3-133">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../reference/ps-reference/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="40ec3-134">Para atualizar o próprio modelo, você precisa atualizar manualmente o repositório de modelos.</span><span class="sxs-lookup"><span data-stu-id="40ec3-134">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="40ec3-135">Consulte o [blog de Xavier Decoster](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) sobre este assunto.</span><span class="sxs-lookup"><span data-stu-id="40ec3-135">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="40ec3-136">Observe que isso é feito por seu próprio risco, pois atualizações manuais podem corromper o modelo se a versão mais recente de todas as dependências não forem compatível entre si.</span><span class="sxs-lookup"><span data-stu-id="40ec3-136">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="40ec3-137">**Posso usar o NuGet fora do Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="40ec3-137">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="40ec3-138">Sim, o NuGet funciona diretamente da linha de comando.</span><span class="sxs-lookup"><span data-stu-id="40ec3-138">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="40ec3-139">Consulte o [Guia de instalação](../install-nuget-client-tools.md) e a [CLI de referência](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="40ec3-139">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="40ec3-140">Linha de comando do NuGet</span><span class="sxs-lookup"><span data-stu-id="40ec3-140">NuGet command line</span></span>

<span data-ttu-id="40ec3-141">**Como fazer para obter a versão mais recente da ferramenta de linha de comando do NuGet?**</span><span class="sxs-lookup"><span data-stu-id="40ec3-141">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="40ec3-142">Consulte o [Guia de instalação](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="40ec3-142">See the [Install guide](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="40ec3-143">Para verificar a versão atual instalada da ferramenta, use `nuget help`.</span><span class="sxs-lookup"><span data-stu-id="40ec3-143">To check the current installed version of the tool, use `nuget help`.</span></span>

<span data-ttu-id="40ec3-144">**O que é a licença para nuget.exe?**</span><span class="sxs-lookup"><span data-stu-id="40ec3-144">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="40ec3-145">Você pode redistribuir o nuget.exe sob os termos da licença do MIT.</span><span class="sxs-lookup"><span data-stu-id="40ec3-145">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="40ec3-146">Você é responsável pela atualização e manutenção das cópias do nuget.exe que você escolhe redistribuir.</span><span class="sxs-lookup"><span data-stu-id="40ec3-146">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="40ec3-147">**É possível estender a ferramenta de linha de comando do NuGet?**</span><span class="sxs-lookup"><span data-stu-id="40ec3-147">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="40ec3-148">Sim, é possível adicionar comandos personalizados para `nuget.exe`, conforme descrito na [postagem de Rob Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="40ec3-148">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="40ec3-149">Console do Gerenciador de Pacotes do NuGet (Visual Studio no Windows)</span><span class="sxs-lookup"><span data-stu-id="40ec3-149">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="40ec3-150">**Como fazer para obter acesso ao objeto DTE no console do Gerenciador de Pacotes?**</span><span class="sxs-lookup"><span data-stu-id="40ec3-150">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="40ec3-151">O objeto de nível superior no modelo de objeto de automação do Visual Studio é chamado o objeto DTE (Ambiente de Ferramentas de Desenvolvimento).</span><span class="sxs-lookup"><span data-stu-id="40ec3-151">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="40ec3-152">O console fornece isso por meio de uma variável chamada `$DTE`.</span><span class="sxs-lookup"><span data-stu-id="40ec3-152">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="40ec3-153">Para obter mais informações, consulte [Visão geral do modelo de automação](/visualstudio/extensibility/internals/automation-model-overview) na documentação de Extensibilidade do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="40ec3-153">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="40ec3-154">**Tento converter a variável $DTE para o tipo DTE2, mas eu recebo um erro: Não é possível converter o valor de "EnvDTE.DTEClass" do tipo "EnvDTE.DTEClass" para o tipo "EnvDTE80.DTE2". Qual é o problema?**</span><span class="sxs-lookup"><span data-stu-id="40ec3-154">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="40ec3-155">Este é um problema conhecido em como o PowerShell interage com um objeto COM.</span><span class="sxs-lookup"><span data-stu-id="40ec3-155">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="40ec3-156">Experimente o seguinte:</span><span class="sxs-lookup"><span data-stu-id="40ec3-156">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="40ec3-157">`Get-Interface` é uma função auxiliar adicionada pelo host do NuGet PowerShell.</span><span class="sxs-lookup"><span data-stu-id="40ec3-157">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="40ec3-158">Criar e publicar pacotes</span><span class="sxs-lookup"><span data-stu-id="40ec3-158">Creating and publishing packages</span></span>

<span data-ttu-id="40ec3-159">**Como fazer para listar meu pacote em um feed?**</span><span class="sxs-lookup"><span data-stu-id="40ec3-159">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="40ec3-160">Consulte [Criar e publicar um pacote](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="40ec3-160">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="40ec3-161">**Tenho várias versões da minha biblioteca que usam versões diferentes do .NET Framework. Como fazer para compilar um único pacote compatível com isso?**</span><span class="sxs-lookup"><span data-stu-id="40ec3-161">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="40ec3-162">Consulte [Suporte a várias versões e perfis do .NET Framework](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="40ec3-162">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="40ec3-163">**Como fazer para configurar meu próprio repositório ou feed?**</span><span class="sxs-lookup"><span data-stu-id="40ec3-163">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="40ec3-164">Consulte a [Visão geral de hospedagem de pacotes](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="40ec3-164">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="40ec3-165">**Como posso carregar pacotes para meu feed do NuGet em massa?**</span><span class="sxs-lookup"><span data-stu-id="40ec3-165">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="40ec3-166">Consulte [Publicação de pacotes do NuGet em massa](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="40ec3-166">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="40ec3-167">Trabalhando com pacotes</span><span class="sxs-lookup"><span data-stu-id="40ec3-167">Working with packages</span></span>

<span data-ttu-id="40ec3-168">**Qual é a diferença entre um pacote de nível de projeto e um pacote de nível de solução?**</span><span class="sxs-lookup"><span data-stu-id="40ec3-168">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="40ec3-169">Um pacote de nível de solução (NuGet 3.x ou superior) é instalado apenas uma vez em uma solução e fica disponível para todos os projetos na solução.</span><span class="sxs-lookup"><span data-stu-id="40ec3-169">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="40ec3-170">Um pacote de nível de projeto está instalado em cada projeto que o utiliza.</span><span class="sxs-lookup"><span data-stu-id="40ec3-170">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="40ec3-171">Um pacote de nível de solução também pode instalar novos comandos que podem ser chamados de dentro do Console do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="40ec3-171">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="40ec3-172">**É possível instalar os pacotes do NuGet sem conectividade com a Internet?**</span><span class="sxs-lookup"><span data-stu-id="40ec3-172">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="40ec3-173">Sim, consulte a postagem no blog de Scott Hanselman [How to access NuGet when nuget.org is down (or you're on a plane) [Como acessar o NuGet quando o nuget.org estiver inativo (ou você estiver a bordo de um avião)]](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span><span class="sxs-lookup"><span data-stu-id="40ec3-173">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="40ec3-174">**Como fazer para instalar pacotes em um local diferente da pasta de pacotes padrão?**</span><span class="sxs-lookup"><span data-stu-id="40ec3-174">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="40ec3-175">Defina a configuração [`repositoryPath`](../reference/nuget-config-file.md#config-section) em `Nuget.Config` usando `nuget config -set repositoryPath=<path>`.</span><span class="sxs-lookup"><span data-stu-id="40ec3-175">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="40ec3-176">**Como evitar adicionar a pasta de pacotes do NuGet ao controle do código-fonte?**</span><span class="sxs-lookup"><span data-stu-id="40ec3-176">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="40ec3-177">Defina o [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) em `Nuget.Config` para `true`.</span><span class="sxs-lookup"><span data-stu-id="40ec3-177">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="40ec3-178">Essa chave funciona no nível da solução e, portanto, precisa ser adicionada ao arquivo `$(Solutiondir)\.nuget\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="40ec3-178">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="40ec3-179">Habilitando a restauração do pacote do Visual Studio cria esse arquivo automaticamente.</span><span class="sxs-lookup"><span data-stu-id="40ec3-179">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="40ec3-180">**Como fazer para desligar a restauração do pacote?**</span><span class="sxs-lookup"><span data-stu-id="40ec3-180">**How do I turn off package restore?**</span></span>

<span data-ttu-id="40ec3-181">Consulte [Habilitar e desabilitar a restauração de pacote](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="40ec3-181">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).</span></span>

<span data-ttu-id="40ec3-182">**Por que recebo um “Não é possível resolver o erro de dependência” ao instalar um pacote local com dependências remotas?**</span><span class="sxs-lookup"><span data-stu-id="40ec3-182">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="40ec3-183">Você precisa selecionar a origem **Todos** ao instalar um pacote local para o projeto.</span><span class="sxs-lookup"><span data-stu-id="40ec3-183">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="40ec3-184">Isso agrega todos os feeds em vez de usar apenas um.</span><span class="sxs-lookup"><span data-stu-id="40ec3-184">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="40ec3-185">O motivo pelo qual este erro ocorre é que os usuários de um repositório local geralmente desejam evitar instalar acidentalmente um pacote remoto devido a políticas corporativa.</span><span class="sxs-lookup"><span data-stu-id="40ec3-185">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="40ec3-186">**Tenho vários projetos na mesma pasta, como posso usar arquivos packages.config separados para cada projeto?**</span><span class="sxs-lookup"><span data-stu-id="40ec3-186">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="40ec3-187">Na maioria dos projetos em que projetos separados residem em pastas separadas, isso não é um problema, pois o NuGet identifica os arquivos `packages.config` em cada projeto.</span><span class="sxs-lookup"><span data-stu-id="40ec3-187">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="40ec3-188">Com o NuGet 3.3 e superior, e com vários projetos na mesma pasta, você pode inserir o nome do projeto nos nomes de arquivo `packages.config` que usam o padrão `packages.{project-name}.config` e o NuGet usará esse arquivo.</span><span class="sxs-lookup"><span data-stu-id="40ec3-188">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="40ec3-189">Isso não é um problema ao usar PackageReference, pois cada arquivo de projeto contém sua própria lista de dependências.</span><span class="sxs-lookup"><span data-stu-id="40ec3-189">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="40ec3-190">**Não vejo o nuget.org na minha lista de repositórios, como faço para obtê-lo novamente?**</span><span class="sxs-lookup"><span data-stu-id="40ec3-190">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="40ec3-191">Adicione `https://api.nuget.org/v3/index.json` à lista de fontes ou</span><span class="sxs-lookup"><span data-stu-id="40ec3-191">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="40ec3-192">Exclua `%appdata%\.nuget\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) e deixe o NuGet recriá-lo.</span><span class="sxs-lookup"><span data-stu-id="40ec3-192">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>
