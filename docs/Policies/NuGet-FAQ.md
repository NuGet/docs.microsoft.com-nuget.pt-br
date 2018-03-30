---
title: Perguntas frequentes do NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/11/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Perguntas e respostas comuns sobre usar o NuGet na linha de comando e no Visual Studio e trabalhar com a Galeria do NuGet.
keywords: P e R do NuGet, perguntas e respostas, problemas comuns, versões do NuGet, versões do pacote
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 33e4776054b1cdd874dcd7e955552ef873dbbf5b
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="0c4a8-104">Perguntas frequentes do NuGet</span><span class="sxs-lookup"><span data-stu-id="0c4a8-104">NuGet frequently-asked questions</span></span>

<span data-ttu-id="0c4a8-105">**O que é necessário para executar o NuGet?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-105">**What is required to run NuGet?**</span></span>

<span data-ttu-id="0c4a8-106">Todas as informações sobre a interface do usuário e as ferramentas de linha de comando estão disponíveis na [Guia de instalação](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="0c4a8-106">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="0c4a8-107">**O NuGet é compatível com o Mono?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-107">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="0c4a8-108">A ferramenta de linha de comando, `nuget.exe`, compila e executa em Mono 3.2 e superior, e pode criar pacotes em Mono.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-108">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="0c4a8-109">Embora `nuget.exe` funcione completamente no Windows, existem alguns problemas conhecidos no Linux e no OS X. Consulte [Problemas do Mono](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) no GitHub.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-109">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="0c4a8-110">Um [cliente gráfico](https://github.com/mrward/monodevelop-nuget-addin) está disponível como um suplemento para MonoDevelop.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-110">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="0c4a8-111">**Como fazer para determinar o que um pacote contém e se ele é estável e útil para meu aplicativo?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-111">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="0c4a8-112">A origem primária para aprender sobre um pacote é a página de listagem em nuget.org (ou outro feed privado).</span><span class="sxs-lookup"><span data-stu-id="0c4a8-112">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="0c4a8-113">Cada página do pacote em nuget.org inclui uma descrição do pacote, seu histórico de versão e as estatísticas de uso.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-113">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="0c4a8-114">A seção **Informações** na página do pacote também contém um link para o site da Web do projeto em que você normalmente encontrar muitos exemplos e documentação para ajudá-lo a aprender como o pacote é usado.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-114">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="0c4a8-115">Para obter mais informações, consulte [Localizando e escolhendo pacotes](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="0c4a8-115">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="0c4a8-116">NuGet no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0c4a8-116">NuGet in Visual Studio</span></span>

<span data-ttu-id="0c4a8-117">**Como é a compatibilidade do NuGet com os diferentes produtos do Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-117">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="0c4a8-118">O Visual Studio no Windows é compatível com a [Interface do usuário do Gerenciador de Pacotes](../tools/package-manager-ui.md) e o [Console do Gerenciador de Pacotes](../tools/package-manager-console.md).</span><span class="sxs-lookup"><span data-stu-id="0c4a8-118">Visual Studio on Windows supports the [Package Manager UI](../tools/package-manager-ui.md) and the [Package Manager Console](../tools/package-manager-console.md).</span></span>
- <span data-ttu-id="0c4a8-119">O Visual Studio para Mac tem recursos internos do NuGet, conforme descrito em [Incluindo um pacote do NuGet em seu projeto](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="0c4a8-119">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="0c4a8-120">O Visual Studio Code (todas as plataformas) não tem nenhuma integração direta do NuGet.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-120">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="0c4a8-121">Usar a [CLI do NuGet](../tools/nuget-exe-cli-reference.md) ou a [CLI do dotnet](../tools/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="0c4a8-121">Use the [NuGet CLI](../tools/nuget-exe-cli-reference.md) or the [dotnet CLI](../tools/dotnet-commands.md).</span></span>
- <span data-ttu-id="0c4a8-122">O Visual Studio Team Services fornece [uma etapa de build para restaurar os pacotes do NuGet](/vsts/build-release/tasks/package/nuget).</span><span class="sxs-lookup"><span data-stu-id="0c4a8-122">Visual Studio Team Services provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="0c4a8-123">Você também pode [hospedar feeds privados de pacote do NuGet no Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="0c4a8-123">You can also [host private NuGet package feeds on Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

<span data-ttu-id="0c4a8-124">**Como fazer para verificar a versão exata das ferramentas do NuGet que estão instaladas?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-124">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="0c4a8-125">No Visual Studio, use o comando **Ajuda > Sobre o Microsoft Visual Studio** e examine a versão exibida ao lado de **Gerenciador de Pacotes do NuGet**.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-125">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="0c4a8-126">Como alternativa, inicie o Console do Gerenciador de Pacotes (**Ferramentas > Gerenciador de Pacotes do NuGet > Console do Gerenciador de Pacotes**) e digite `$host` para ver informações sobre o NuGet, incluindo a versão.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-126">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="0c4a8-127">**Quais linguagens de programação são compatíveis com o NuGet?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-127">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="0c4a8-128">O NuGet geralmente funciona para linguagens .NET e foi projetado para trazer bibliotecas .NET em um projeto.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-128">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="0c4a8-129">Como também há suporte para a automação do MSBuild e do Visual Studio em alguns tipos de projeto, também há suporte para outros projetos e idiomas em diversos níveis.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-129">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="0c4a8-130">A versão mais recente do NuGet é compatível com C#, Visual Basic, F#, WiX e C++.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-130">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="0c4a8-131">**Quais modelos de projeto são compatíveis com o NuGet?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-131">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="0c4a8-132">O NuGet tem suporte completo para uma variedade de modelos de projeto como Windows, Web, Cloud, SharePoint, Wix e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-132">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="0c4a8-133">**Como fazer para atualizar pacotes que fazem parte dos modelos do Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-133">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="0c4a8-134">Acesse a guia **Atualizações** na interface do usuário do Gerenciador de Pacotes e selecione **Atualizar tudo** ou use o comando [`Update-Package`](../tools/ps-ref-update-package.md) do Console do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-134">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../tools/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="0c4a8-135">Para atualizar o próprio modelo, você precisa atualizar manualmente o repositório de modelos.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-135">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="0c4a8-136">Consulte o [blog de Xavier Decoster](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) sobre este assunto.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-136">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="0c4a8-137">Observe que isso é feito por seu próprio risco, pois atualizações manuais podem corromper o modelo se a versão mais recente de todas as dependências não forem compatível entre si.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-137">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="0c4a8-138">**Posso usar o NuGet fora do Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-138">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="0c4a8-139">Sim, o NuGet funciona diretamente da linha de comando.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-139">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="0c4a8-140">Consulte o [Guia de instalação](../install-nuget-client-tools.md) e a [CLI de referência](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="0c4a8-140">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../tools/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="0c4a8-141">Linha de comando do NuGet</span><span class="sxs-lookup"><span data-stu-id="0c4a8-141">NuGet command line</span></span>

<span data-ttu-id="0c4a8-142">**Como fazer para obter a versão mais recente da ferramenta de linha de comando do NuGet?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-142">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="0c4a8-143">Consulte o [Guia de instalação](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="0c4a8-143">See the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="0c4a8-144">**O que é a licença para nuget.exe?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-144">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="0c4a8-145">Você pode redistribuir o nuget.exe sob os termos da licença do MIT.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-145">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="0c4a8-146">Você é responsável pela atualização e manutenção das cópias do nuget.exe que você escolhe redistribuir.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-146">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="0c4a8-147">**É possível estender a ferramenta de linha de comando do NuGet?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-147">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="0c4a8-148">Sim, é possível adicionar comandos personalizados para `nuget.exe`, conforme descrito na [postagem de Rob Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c4a8-148">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="0c4a8-149">Console do Gerenciador de Pacotes do NuGet (Visual Studio no Windows)</span><span class="sxs-lookup"><span data-stu-id="0c4a8-149">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="0c4a8-150">**Como fazer para obter acesso ao objeto DTE no console do Gerenciador de Pacotes?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-150">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="0c4a8-151">O objeto de nível superior no modelo de objeto de automação do Visual Studio é chamado o objeto DTE (Ambiente de Ferramentas de Desenvolvimento).</span><span class="sxs-lookup"><span data-stu-id="0c4a8-151">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="0c4a8-152">O console fornece isso por meio de uma variável chamada `$DTE`.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-152">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="0c4a8-153">Para obter mais informações, consulte [Visão geral do modelo de automação](/visualstudio/extensibility/internals/automation-model-overview) na documentação de Extensibilidade do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-153">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="0c4a8-154">**Tento converter a variável $DTE para o tipo DTE2, mas recebo um erro: não é possível converter o valor de “EnvDTE.DTEClass” do tipo “EnvDTE.DTEClass” para o tipo “EnvDTE80.DTE2”. Qual é o problema?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-154">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="0c4a8-155">Este é um problema conhecido em como o PowerShell interage com um objeto COM.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-155">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="0c4a8-156">Experimente o seguinte:</span><span class="sxs-lookup"><span data-stu-id="0c4a8-156">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="0c4a8-157">`Get-Interface` é uma função auxiliar adicionada pelo host do NuGet PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-157">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="0c4a8-158">Criar e publicar pacotes</span><span class="sxs-lookup"><span data-stu-id="0c4a8-158">Creating and publishing packages</span></span>

<span data-ttu-id="0c4a8-159">**Como fazer para listar meu pacote em um feed?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-159">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="0c4a8-160">Consulte [Criar e publicar um pacote](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="0c4a8-160">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="0c4a8-161">**Tenho várias versões da minha biblioteca que usam versões diferentes do .NET Framework. Como fazer para compilar um único pacote compatível com isso?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-161">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="0c4a8-162">Consulte [Suporte a várias versões e perfis do .NET Framework](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="0c4a8-162">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="0c4a8-163">**Como fazer para configurar meu próprio repositório ou feed?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-163">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="0c4a8-164">Consulte a [Visão geral de hospedagem de pacotes](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="0c4a8-164">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="0c4a8-165">**Como posso carregar pacotes para meu feed do NuGet em massa?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-165">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="0c4a8-166">Consulte [Publicação de pacotes do NuGet em massa](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="0c4a8-166">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="0c4a8-167">Trabalhando com pacotes</span><span class="sxs-lookup"><span data-stu-id="0c4a8-167">Working with packages</span></span>

<span data-ttu-id="0c4a8-168">**Qual é a diferença entre um pacote de nível de projeto e um pacote de nível de solução?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-168">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="0c4a8-169">Um pacote de nível de solução (NuGet 3.x ou superior) é instalado apenas uma vez em uma solução e fica disponível para todos os projetos na solução.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-169">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="0c4a8-170">Um pacote de nível de projeto está instalado em cada projeto que o utiliza.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-170">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="0c4a8-171">Um pacote de nível de solução também pode instalar novos comandos que podem ser chamados de dentro do Console do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-171">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="0c4a8-172">**É possível instalar os pacotes do NuGet sem conectividade com a Internet?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-172">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="0c4a8-173">Sim, consulte a postagem no blog de Scott Hanselman [How to access NuGet when nuget.org is down (or you're on a plane) [Como acessar o NuGet quando o nuget.org estiver inativo (ou você estiver a bordo de um avião)]](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span><span class="sxs-lookup"><span data-stu-id="0c4a8-173">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="0c4a8-174">**Como fazer para instalar pacotes em um local diferente da pasta de pacotes padrão?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-174">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="0c4a8-175">Defina a configuração [`repositoryPath`](../reference/nuget-config-file.md#config-section) em `Nuget.Config` usando `nuget config -set repositoryPath=<path>`.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-175">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="0c4a8-176">**Como evitar adicionar a pasta de pacotes do NuGet ao controle do código-fonte?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-176">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="0c4a8-177">Defina o [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) em `Nuget.Config` para `true`.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-177">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="0c4a8-178">Essa chave funciona no nível da solução e, portanto, precisa ser adicionada ao arquivo `$(Solutiondir)\.nuget\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-178">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="0c4a8-179">Habilitando a restauração do pacote do Visual Studio cria esse arquivo automaticamente.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-179">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="0c4a8-180">**Como fazer para desligar a restauração do pacote?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-180">**How do I turn off package restore?**</span></span>

<span data-ttu-id="0c4a8-181">Consulte [Habilitar e desabilitar a restauração de pacote](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="0c4a8-181">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="0c4a8-182">**Por que recebo um “Não é possível resolver o erro de dependência” ao instalar um pacote local com dependências remotas?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-182">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="0c4a8-183">Você precisa selecionar a origem **Todos** ao instalar um pacote local para o projeto.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-183">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="0c4a8-184">Isso agrega todos os feeds em vez de usar apenas um.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-184">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="0c4a8-185">O motivo pelo qual este erro ocorre é que os usuários de um repositório local geralmente desejam evitar instalar acidentalmente um pacote remoto devido a políticas corporativa.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-185">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="0c4a8-186">**Tenho vários projetos na mesma pasta, como posso usar arquivos packages.config separados para cada projeto?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-186">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="0c4a8-187">Na maioria dos projetos em que projetos separados residem em pastas separadas, isso não é um problema, pois o NuGet identifica os arquivos `packages.config` em cada projeto.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-187">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="0c4a8-188">Com o NuGet 3.3 e superior, e com vários projetos na mesma pasta, você pode inserir o nome do projeto nos nomes de arquivo `packages.config` que usam o padrão `packages.{project-name}.config` e o NuGet usará esse arquivo.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-188">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="0c4a8-189">Isso não é um problema ao usar PackageReference, pois cada arquivo de projeto contém sua própria lista de dependências.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-189">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="0c4a8-190">**Não vejo o nuget.org na minha lista de repositórios, como faço para obtê-lo novamente?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-190">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="0c4a8-191">Adicione `https://api.nuget.org/v3/index.json` à lista de fontes ou</span><span class="sxs-lookup"><span data-stu-id="0c4a8-191">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="0c4a8-192">Exclua `%appdata%\.nuget\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) e deixe o NuGet recriá-lo.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-192">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>

<span data-ttu-id="0c4a8-193">**Quais são os termos de licença padrão se um pacote não fornecer informações de licença específicas?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-193">**What are the default license terms if a package doesn't provide specific license information?**</span></span>

<span data-ttu-id="0c4a8-194">Cada pacote é regido pelos termos incluídos no pacote.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-194">Each package is governed by the terms that are included with the package.</span></span> <span data-ttu-id="0c4a8-195">Você deve examinar os termos aplicáveis antes de acessar, baixar ou adquirir os pacotes.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-195">You should review the applicable terms before accessing, downloading, or acquiring any packages.</span></span> <span data-ttu-id="0c4a8-196">Em nuget.org, use o link **Informações de Licença** na página do pacote.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-196">On nuget.org, use the **License Info** link on the package page.</span></span>

<span data-ttu-id="0c4a8-197">Se um pacote não especificar os termos de licença, entre em contato com o proprietário do pacote diretamente usando o link **Contatar os proprietários** na página do pacote em nuget.org.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-197">If a package does not specify the licensing terms, contact the package owner directly using the **Contact owners** link on the nuget.org package page.</span></span> <span data-ttu-id="0c4a8-198">A Microsoft não licencia nenhuma propriedade intelectual para você de provedores de pacotes de terceiros, nem é responsável pelas informações fornecidas por terceiros.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-198">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>

## <a name="managing-packages-on-nugetorg"></a><span data-ttu-id="0c4a8-199">Gerenciando pacotes em nuget.org</span><span class="sxs-lookup"><span data-stu-id="0c4a8-199">Managing packages on nuget.org</span></span>

<span data-ttu-id="0c4a8-200">**Posso editar os metadados do pacote depois que ele é carregado? Por que é exigido editar o nuspec e carregar um novo pacote para fazer alterações nos metadados do pacote?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-200">**Can I edit package metadata after it's been uploaded? Why do you require editing the nuspec and uploading a new package for making changes to package metadata?**</span></span>

<span data-ttu-id="0c4a8-201">O NuGet requer que todos os pacotes sejam assinados.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-201">NuGet requires all packages to be signed.</span></span> <span data-ttu-id="0c4a8-202">Um princípio de design da assinatura de pacote é que o conteúdo do pacote assinado deve ser imutável, que inclui o nuspec.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-202">A design principle of package signing is that signed package content must be immutable, which includes the nuspec.</span></span> <span data-ttu-id="0c4a8-203">Editar os resultados de metadados de pacote em alterações de nuspec, invalidando assinaturas existentes.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-203">Editing the package metadata results in changes to the nuspec, invalidating existing signatures.</span></span> <span data-ttu-id="0c4a8-204">É recomendável modificar fluxos de trabalho existentes para não exigir a edição dos metadados do pacote depois que o este foi criado.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-204">We recommend modifying existing workflows to not require editing the package metadata after the package has been created.</span></span>

<span data-ttu-id="0c4a8-205">Observe que as dependências listadas para seu pacote são geradas automaticamente do próprio pacote e não podem ser editadas.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-205">Note that dependencies listed for your package are generated automatically from the package itself and cannot be edited.</span></span>

<span data-ttu-id="0c4a8-206">Além disso, carregar pacotes para [staging.nuget.org](http://staging.nuget.org) é uma ótima maneira de testar e validar seu pacote sem disponibilizá-lo na galeria pública.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-206">In addition, uploading packages to [staging.nuget.org](http://staging.nuget.org) is a great way to test and validate your package without making a package available in the public gallery.</span></span>

<span data-ttu-id="0c4a8-207">**É possível reservar nomes para os pacotes que serão publicados no futuro?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-207">**Is it possible to reserve names for packages that will be published in future?**</span></span>

<span data-ttu-id="0c4a8-208">Sim.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-208">Yes.</span></span> <span data-ttu-id="0c4a8-209">Você pode reservar IDs para os pacotes em [nuget.org](https://www.nuget.org/) solicitando um prefixo de ID de pacote para a sua conta.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-209">You can reserve IDs for packages on [nuget.org](https://www.nuget.org/) by requesting a package ID prefix for your account.</span></span> <span data-ttu-id="0c4a8-210">Para solicitar um prefixo da ID do pacote, siga as instruções na [documentação](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).</span><span class="sxs-lookup"><span data-stu-id="0c4a8-210">In order to request a package ID prefix, follow the instructions in the [documentation](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).</span></span>

<span data-ttu-id="0c4a8-211">**Como fazer para declarar a propriedade de pacotes?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-211">**How do I claim ownership for packages ?**</span></span>

<span data-ttu-id="0c4a8-212">Consulte [Gerenciando os proprietários de pacote no nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="0c4a8-212">See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span>

<span data-ttu-id="0c4a8-213">**Como fazer para lidar com um proprietário de pacote que está violando minha licença de software?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-213">**How do I deal with a package owner who is violating my software license?**</span></span>

<span data-ttu-id="0c4a8-214">Estimulamos a comunidade do NuGet para trabalhar juntos para resolver as controvérsias que podem surgir entre os proprietários do pacote e os proprietários de outro software.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-214">We encourage the NuGet community to work together to resolve any disputes that may arise between package owners and the owners of other software.</span></span> <span data-ttu-id="0c4a8-215">Criamos um [processo de solução de controvérsias](../policies/dispute-resolution.md) que deve ser seguido antes de solicitar a intervenção dos administradores do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-215">We have crafted a [dispute resolution process](../policies/dispute-resolution.md) to follow before asking nuget.org administrators to intercede.</span></span>

<span data-ttu-id="0c4a8-216">**É recomendável carregar pacotes meu teste para o nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-216">**Is it recommended to upload my test packages to nuget.org?**</span></span>

<span data-ttu-id="0c4a8-217">Para fins de teste, você pode usar [staging.nuget.org](http://staging.nuget.org) ou os servidores NuGet públicos alternativos como [myget.org](https://myget.org) ou do [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span><span class="sxs-lookup"><span data-stu-id="0c4a8-217">For test purposes, you can use [staging.nuget.org](http://staging.nuget.org), or alternative public NuGet servers like [myget.org](https://myget.org) or [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span></span>

<span data-ttu-id="0c4a8-218">Observe que os pacotes carregados para o staging.nuget.org podem não ser preservados.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-218">Note that packages uploaded to staging.nuget.org may not be preserved.</span></span> <span data-ttu-id="0c4a8-219">Consulte [Versão prévia do Goodbye](http://blog.nuget.org/20130419/goodbye-preview.html).</span><span class="sxs-lookup"><span data-stu-id="0c4a8-219">See [Goodbye preview](http://blog.nuget.org/20130419/goodbye-preview.html).</span></span>

<span data-ttu-id="0c4a8-220">**Qual é o tamanho máximo dos pacotes que posso carregar para o nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-220">**What is the maximum size of packages I can upload to nuget.org?**</span></span>

<span data-ttu-id="0c4a8-221">O nuget.org permite usar pacotes com até 250 MB, mas é recomendável manter os pacotes abaixo de 1 MB se possível e usar as dependências para unir pacotes.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-221">nuget.org allows packages up to 250MB, but we recommend keeping packages under 1MB if possible and using dependencies to link packages together.</span></span> <span data-ttu-id="0c4a8-222">Como regra geral, os pacotes contêm apenas um assembly para evitar colisões.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-222">As a rule of thumb, packages contain only one assembly to avoid collisions.</span></span>

<span data-ttu-id="0c4a8-223">O NuGet usa HTTP para baixar os pacotes, por isso pacotes maiores têm maior probabilidade de apresentar falha na instalação do que os menores.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-223">NuGet uses HTTP to download packages, so larger packages have a higher likelihood of failed installs than smaller ones.</span></span>

<span data-ttu-id="0c4a8-224">É possível compartilhar as dependências entre vários pacotes, reduzindo o tamanho total do download para os consumidores de seus pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-224">It is possible to share dependencies between multiple packages, making the total download size for consumers of your NuGet packages smaller.</span></span>

<span data-ttu-id="0c4a8-225">As dependências são principalmente estáticas e nunca mudam.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-225">Dependencies are mostly static and never change.</span></span> <span data-ttu-id="0c4a8-226">Ao corrigir um bug no código, as dependências não precisarão ser atualizadas.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-226">When fixing a bug in code, the dependencies may not need to be updated.</span></span> <span data-ttu-id="0c4a8-227">Se você agrupar dependências, pacotes cada vez maiores são distribuídos a cada vez.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-227">If you bundle dependencies, you end up reshipping larger packages every time.</span></span> <span data-ttu-id="0c4a8-228">Dividir os pacotes do NuGet em dependências relacionadas torna os upgrades muito mais refinados para os consumidores do seu pacote.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-228">By splitting NuGet packages into related dependencies, upgrades are much more fine-grained for consumers of your package.</span></span>

## <a name="nugetorg-not-accessible"></a><span data-ttu-id="0c4a8-229">O nuget.org não está acessível</span><span class="sxs-lookup"><span data-stu-id="0c4a8-229">nuget.org not accessible</span></span>

<span data-ttu-id="0c4a8-230">**Por que não é possível baixar ou carregar pacotes para o nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-230">**Why can't I download packages from or upload packages to nuget.org?**</span></span>

<span data-ttu-id="0c4a8-231">Primeiro, verifique se que você está usando as versões mais recentes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-231">First, make sure you're using the latest versions of NuGet.</span></span> <span data-ttu-id="0c4a8-232">Se essa versão continuar falhando, [entre em contato com o suporte](https://www.nuget.org/policies/Contact) e forneça as informações de solução de problemas de conexão adicionais, incluindo:</span><span class="sxs-lookup"><span data-stu-id="0c4a8-232">If that version continues to fail, [contact support](https://www.nuget.org/policies/Contact) and provide additional connection troubleshooting information including:</span></span>

- <span data-ttu-id="0c4a8-233">A versão do NuGet que você está usando</span><span class="sxs-lookup"><span data-stu-id="0c4a8-233">The version of NuGet you're using</span></span>
- <span data-ttu-id="0c4a8-234">As origens de pacote que você está usando</span><span class="sxs-lookup"><span data-stu-id="0c4a8-234">The package sources you're using</span></span>
- <span data-ttu-id="0c4a8-235">Um log de restauração detalhado</span><span class="sxs-lookup"><span data-stu-id="0c4a8-235">A restore log with detailed verbosity</span></span>
- <span data-ttu-id="0c4a8-236">MTR ou um rastreamento do Fiddler (veja abaixo)</span><span class="sxs-lookup"><span data-stu-id="0c4a8-236">MTR or a Fiddler traces (see below)</span></span>
- <span data-ttu-id="0c4a8-237">Sua área geográfica</span><span class="sxs-lookup"><span data-stu-id="0c4a8-237">Your geographical area</span></span>
- <span data-ttu-id="0c4a8-238">A versão do seu sistema operacional</span><span class="sxs-lookup"><span data-stu-id="0c4a8-238">Your operating system version</span></span>
- <span data-ttu-id="0c4a8-239">Configuração do computador (CPU, rede e disco rígido)</span><span class="sxs-lookup"><span data-stu-id="0c4a8-239">Machine configuration (CPU, Network, hard drive)</span></span>
- <span data-ttu-id="0c4a8-240">Se seu computador estiver atrás de um proxy ou firewall</span><span class="sxs-lookup"><span data-stu-id="0c4a8-240">Whether is your machine behind a proxy or firewall</span></span>
- <span data-ttu-id="0c4a8-241">As versões do .NET que estão instaladas no computador</span><span class="sxs-lookup"><span data-stu-id="0c4a8-241">The versions of .NET that are installed on the machine</span></span>
- <span data-ttu-id="0c4a8-242">Versões de ferramentas de multiplataforma como CLI do .NET ou DNU que você está usando</span><span class="sxs-lookup"><span data-stu-id="0c4a8-242">Versions of cross-platform tools such as .NET CLI, or DNU that you're using</span></span>

<span data-ttu-id="0c4a8-243">*Para capturar MTR:*</span><span class="sxs-lookup"><span data-stu-id="0c4a8-243">*To capture MTR:*</span></span>

- <span data-ttu-id="0c4a8-244">Baixe o WinMTR em [http://winmtr.net/download/](http://winmtr.net/)</span><span class="sxs-lookup"><span data-stu-id="0c4a8-244">Download WinMTR from [http://winmtr.net/download/](http://winmtr.net/)</span></span>
- <span data-ttu-id="0c4a8-245">Digite `api.nuget.org` como o nome do host e clique em **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-245">Enter `api.nuget.org` as the hostname and click **Start**.</span></span>
- <span data-ttu-id="0c4a8-246">Aguarde até a coluna **Sent** ser >= 100.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-246">Wait until the **Sent** column is >= 100.</span></span>

    ![Capturando MTR](media/mtr.png)

- <span data-ttu-id="0c4a8-248">Copie texto para a área de transferência.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-248">Copy text to clipboard.</span></span>

<span data-ttu-id="0c4a8-249">*Para capturar o Fiddler:*</span><span class="sxs-lookup"><span data-stu-id="0c4a8-249">*To capture Fiddler:*</span></span>

- <span data-ttu-id="0c4a8-250">Instale a versão mais recente do [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="0c4a8-250">Install the latest version of [Fiddler](http://www.telerik.com/download/fiddler).</span></span>
- <span data-ttu-id="0c4a8-251">Inicie o Fiddler e desabilite a captura de tráfego usando o menu **Arquivo > Capturar tráfego**.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-251">Start Fiddler and disable capturing traffic using the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="0c4a8-252">Remova todas as sessões (selecione todos os itens na lista, pressione a tecla **Delete**).</span><span class="sxs-lookup"><span data-stu-id="0c4a8-252">Remove all sessions (select all items in the list, press the **Delete** key).</span></span>
- <span data-ttu-id="0c4a8-253">Configure o Fiddler para capturar o tráfego HTTPS marcando **Descriptografar tráfego HTTPS** na guia **HTTPS** do menu **Ferramentas > Opções do Fiddler...**.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-253">Configure Fiddler to capture HTTPS traffic by checking **Decrypt HTTPS traffic** in the **HTTPS** tab of the **Tools > Fiddler Options...** menu.</span></span>
- <span data-ttu-id="0c4a8-254">Feche o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-254">Close Visual Studio.</span></span>
- <span data-ttu-id="0c4a8-255">Habilitar o menu **Arquivo > Capturar Tráfego**.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-255">Enable the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="0c4a8-256">Inicie o Visual Studio ou .exe do nuget.exe e execute as ações que não estão funcionando.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-256">Start Visual Studio or nuget.exe .exe and perform the actions that are not working.</span></span> <span data-ttu-id="0c4a8-257">O tráfego gerado por essas ações deve ser exibido no Fiddler.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-257">The traffic generated by these actions should show up in Fiddler.</span></span>
- <span data-ttu-id="0c4a8-258">Depois das ações serem executadas, use **Arquivo > Salvar > Todas as sessões** para armazenar as sessões capturadas.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-258">Once the actions have run, use **File > Save > All Sessions** to store the captured sessions.</span></span>

<span data-ttu-id="0c4a8-259">Observação: pode ser necessário definir a variável de ambiente `HTTP_PROXY` para `http://127.0.0.1:8888` para rotear o tráfego do NuGet através do Fiddler.</span><span class="sxs-lookup"><span data-stu-id="0c4a8-259">Note: it may be required to set the `HTTP_PROXY` environment variable to `http://127.0.0.1:8888` for routing NuGet traffic through Fiddler.</span></span>

<span data-ttu-id="0c4a8-260">Se isso falhar, experimente as [dicas mencionadas nesta postagem do StackOverflow](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span><span class="sxs-lookup"><span data-stu-id="0c4a8-260">If that fails, try the [tips mentioned in this StackOverflow post](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span></span>

<span data-ttu-id="0c4a8-261">**Quais são os pontos de extremidade de API para nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="0c4a8-261">**What are the API endpoints for nuget.org?**</span></span>

<span data-ttu-id="0c4a8-262">V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (Observe que a API V2 foi preterida e não funciona com o NuGet 4 ou superior.)</span><span class="sxs-lookup"><span data-stu-id="0c4a8-262">V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (Note that the V2 API is deprecated and does not work with NuGet 4+.)</span></span>
