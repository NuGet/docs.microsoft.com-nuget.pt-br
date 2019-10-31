---
title: Arquivo project.json do NuGet com projetos UWP
description: Descrição de como o arquivo project.json é usado para rastrear dependências do NuGet em projetos UWP (Plataforma Universal do Windows).
author: karann-msft
ms.author: karann
ms.date: 07/17/2017
ms.topic: conceptual
ms.openlocfilehash: ac3c137dd0ba50571737093eef11c8ab0ef932b2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548658"
---
# <a name="projectjson-and-uwp"></a><span data-ttu-id="cd1c5-103">project.json e UWP</span><span class="sxs-lookup"><span data-stu-id="cd1c5-103">project.json and UWP</span></span>

> [!Important]
> <span data-ttu-id="cd1c5-104">Este conteúdo foi preterido.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-104">This content is deprecated.</span></span> <span data-ttu-id="cd1c5-105">Os projetos devem usar os formatos `packages.config` ou PackageReference.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-105">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="cd1c5-106">Este documento descreve a estrutura do pacote que utiliza os recursos do NuGet 3 ou superior (Visual Studio 2015 e posterior).</span><span class="sxs-lookup"><span data-stu-id="cd1c5-106">This document describes the package structure that employs features in NuGet 3+ (Visual Studio 2015 and later).</span></span> <span data-ttu-id="cd1c5-107">A propriedade `minClientVersion` do seu `.nuspec` pode ser usada para indicar que você requer os recursos descritos aqui definindo-a para 3.1.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-107">The `minClientVersion` property of your `.nuspec` can be used to state that you require the features described here by setting it to 3.1.</span></span>

## <a name="adding-uwp-support-to-an-existing-package"></a><span data-ttu-id="cd1c5-108">Adicionar suporte para UWP a um pacote existente</span><span class="sxs-lookup"><span data-stu-id="cd1c5-108">Adding UWP support to an existing package</span></span>

<span data-ttu-id="cd1c5-109">Se você tiver um pacote existente e desejar adicionar suporte para aplicativos UWP, não será necessário adotar o formato de empacotamento descrito aqui.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-109">If you have an existing package and you want to add support for UWP applications, then you don’t need to adopt the  packaging format described here.</span></span> <span data-ttu-id="cd1c5-110">Você só precisa adotar esse formato se precisar dos recursos que ele descreve e estiver disposto a trabalhar somente com clientes que foram atualizados para a versão 3 ou superior do cliente do NuGet.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-110">You only need to adopt this format if you require the features it describes and are willing to  work only with clients that have updated to version 3+ of the NuGet client.</span></span>

## <a name="i-already-target-netcore45"></a><span data-ttu-id="cd1c5-111">Já direcionado para netcore45</span><span class="sxs-lookup"><span data-stu-id="cd1c5-111">I already target netcore45</span></span>

<span data-ttu-id="cd1c5-112">Se seu projeto já se destina ao `netcore45` e você não precisa aproveitar os recursos descritos aqui, nenhuma ação é necessária.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-112">If you target `netcore45` already, and you don’t need to take advantage of the features here, no action is needed.</span></span> <span data-ttu-id="cd1c5-113">Pacotes `netcore45` podem ser consumidos por aplicativos UWP.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-113">`netcore45` packages can be consumed by UWP applications.</span></span>

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a><span data-ttu-id="cd1c5-114">Desejo aproveitar as APIs específicas do Windows 10</span><span class="sxs-lookup"><span data-stu-id="cd1c5-114">I want to take advantage of Windows 10 specific APIs</span></span>

<span data-ttu-id="cd1c5-115">Nesse caso, será necessário adicionar o moniker da estrutura de destino `uap10.0` (TFM ou TxM) ao seu pacote.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-115">In this case you need to add the `uap10.0` target framework moniker (TFM or TxM) to your package.</span></span> <span data-ttu-id="cd1c5-116">Crie uma nova pasta no seu pacote e adicione o assembly que foi compilado para funcionar com o Windows 10 para essa pasta.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-116">Create a new folder in your package and add the assembly that has been compiled to work with Windows 10 to that folder.</span></span>

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a><span data-ttu-id="cd1c5-117">Não preciso de APIs específicas do Windows 10, mas desejo novos recursos do .NET ou ainda não tenho o netcore45</span><span class="sxs-lookup"><span data-stu-id="cd1c5-117">I don’t need Windows 10 specific APIs, but want new .NET features or don’t have netcore45 already</span></span>

<span data-ttu-id="cd1c5-118">Nesse caso, você adicionaria o `dotnet` TxM ao seu pacote.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-118">In this case you would add the `dotnet` TxM to your package.</span></span> <span data-ttu-id="cd1c5-119">Ao contrário de outros TxMs, o `dotnet` não implica em uma plataforma ou área da superfície.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-119">Unlike other TxMs, `dotnet` doesn't imply a surface area or platform.</span></span> <span data-ttu-id="cd1c5-120">É informado que seu pacote funciona em qualquer plataforma com as quais suas dependências funcionam.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-120">It is stating that your package works on any platform that your dependencies work on.</span></span> <span data-ttu-id="cd1c5-121">Ao criar um pacote com o `dotnet` TxM, você provavelmente terá muitas outras dependências específicas de TxM no seu `.nuspec`, conforme necessário para definir os pacotes de BCL dos quais você depende, como `System.Text`, `System.Xml`, etc. Os locais em que essas dependências funcionam definem onde seu pacote funciona.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-121">When building a package with the `dotnet` TxM, you are likely to have many more TxM-specific dependencies in your `.nuspec`, as you need to define the BCL packages you depend on, such `System.Text`, `System.Xml`, etc. The locations that those dependencies work on define where your package works.</span></span>

### <a name="how-do-i-find-out-my-dependencies"></a><span data-ttu-id="cd1c5-122">Como fazer para localizar minhas dependências</span><span class="sxs-lookup"><span data-stu-id="cd1c5-122">How do I find out my dependencies</span></span>

<span data-ttu-id="cd1c5-123">Há duas maneiras de descobrir quais dependências listar:</span><span class="sxs-lookup"><span data-stu-id="cd1c5-123">There are two ways to figure out which dependencies to list:</span></span>

1. <span data-ttu-id="cd1c5-124">Use a ferramenta [Gerador de dependência de NuSpec](https://github.com/onovotny/ReferenceGenerator) **de terceiros**.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-124">Use the [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) **3rd party** tool.</span></span> <span data-ttu-id="cd1c5-125">A ferramenta automatiza o processo e atualiza seu arquivo `.nuspec` com os pacotes dependentes no build.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-125">The tool automates the process and updates your `.nuspec` file with the dependant packages on build.</span></span> <span data-ttu-id="cd1c5-126">Está disponível por meio de um pacote do NuGet, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span><span class="sxs-lookup"><span data-stu-id="cd1c5-126">It is available via a NuGet package, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span></span>

1. <span data-ttu-id="cd1c5-127">(A maneira mais difícil) Use `ILDasm` para examinar seu `.dll` para ver quais assemblies são realmente necessários no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-127">(The hard way) Use `ILDasm` to look at your `.dll` to see what assemblies are actually needed at runtime.</span></span> <span data-ttu-id="cd1c5-128">Em seguida, determine de qual pacote do NuGet cada um deles veio.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-128">Then determine which NuGet package they each come from.</span></span>

<span data-ttu-id="cd1c5-129">Consulte o tópico [`project.json`](project-json.md) para obter detalhes sobre os recursos que ajudam na criação de um pacote compatível com o `dotnet` TxM.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-129">See the [`project.json`](project-json.md) topic for details on features that help in the creation of a package that supports the `dotnet` TxM.</span></span>

> [!Important]
> <span data-ttu-id="cd1c5-130">Se seu pacote se destina a trabalhar com projetos PCL, é altamente recomendável criar uma pasta `dotnet` para evitar avisos e possíveis problemas de compatibilidade.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-130">If your package is intended to work with PCL projects, we highly recommend to create a `dotnet` folder, to avoid warnings and potential compatibility issues.</span></span>

## <a name="directory-structure"></a><span data-ttu-id="cd1c5-131">Estrutura do diretório</span><span class="sxs-lookup"><span data-stu-id="cd1c5-131">Directory structure</span></span>

<span data-ttu-id="cd1c5-132">Pacotes do NuGet usando esse formato tem a seguinte pasta e comportamento bem conhecidos:</span><span class="sxs-lookup"><span data-stu-id="cd1c5-132">NuGet packages using this format have the following well-known folder and behaviors:</span></span>

| <span data-ttu-id="cd1c5-133">Pasta</span><span class="sxs-lookup"><span data-stu-id="cd1c5-133">Folder</span></span> | <span data-ttu-id="cd1c5-134">Comportamentos</span><span class="sxs-lookup"><span data-stu-id="cd1c5-134">Behaviors</span></span> |
| --- | --- |
| <span data-ttu-id="cd1c5-135">Build</span><span class="sxs-lookup"><span data-stu-id="cd1c5-135">Build</span></span> | <span data-ttu-id="cd1c5-136">Contém os arquivos de objeto e destinos do MSBuild nesta pasta, que estão integrados de forma diferente no projeto, porém, exceto isso, não há nenhuma alteração.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-136">Contains MSBuild targets and props files in this folder are integrated differently into the project, but otherwise there is no change.</span></span> |
| <span data-ttu-id="cd1c5-137">Ferramentas</span><span class="sxs-lookup"><span data-stu-id="cd1c5-137">Tools</span></span> | <span data-ttu-id="cd1c5-138">`install.ps1` e `uninstall.ps1` não são executados.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-138">`install.ps1` and `uninstall.ps1` are not run.</span></span> <span data-ttu-id="cd1c5-139">O continua `init.ps1` funcionando como sempre.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-139">`init.ps1` works as it always has.</span></span> |
| <span data-ttu-id="cd1c5-140">Conteúdo</span><span class="sxs-lookup"><span data-stu-id="cd1c5-140">Content</span></span> | <span data-ttu-id="cd1c5-141">O conteúdo não é copiado automaticamente para o projeto de um usuário.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-141">Content is not copied automatically into a user's project.</span></span> <span data-ttu-id="cd1c5-142">Suporte para inclusão de conteúdo do projeto está planejado para uma versão posterior.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-142">Support for content inclusion in the project is planned for a later release.</span></span> |
| <span data-ttu-id="cd1c5-143">Lib</span><span class="sxs-lookup"><span data-stu-id="cd1c5-143">Lib</span></span> | <span data-ttu-id="cd1c5-144">Para muitos pacotes de `lib` que funcionam da mesma forma que no NuGet 2.x, mas com opções expandidas para que nomes possam ser usados dentro delas e lógica aprimorada para escolher a subpasta correta ao consumir pacotes.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-144">For many packages the `lib` works the same way it does in NuGet 2.x, but with expanded options for what names can be used inside it and better logic for picking the correct sub-folder when consuming packages.</span></span> <span data-ttu-id="cd1c5-145">No entanto, quando usado junto com `ref`, a pasta `lib` contém os assemblies que implementam a área da superfície definida pelos assemblies na pasta `ref`.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-145">However, when used in conjunction with `ref`, the `lib` folder contains assemblies that implement the surface area defined by the assemblies in the `ref` folder.</span></span> |
| <span data-ttu-id="cd1c5-146">Ref</span><span class="sxs-lookup"><span data-stu-id="cd1c5-146">Ref</span></span> | <span data-ttu-id="cd1c5-147">`ref` é uma pasta opcional que contém os assemblies .NET definindo a superfície pública (tipos e métodos públicos) para compilar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-147">`ref` is an optional folder that contains .NET assemblies defining the public surface (public types and methods) for an application to compile against.</span></span> <span data-ttu-id="cd1c5-148">Os assemblies nesta pasta não podem ter nenhuma implementação e são puramente usados para definir a área de superfície para o compilador.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-148">The assemblies in this folder may have no implementation, they are purely used to define surface area for the compiler.</span></span> <span data-ttu-id="cd1c5-149">Se o pacote não tiver nenhuma pasta `ref`, o `lib` será o assembly de referência e o assembly de implementação.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-149">If the package has no `ref` folder, then the `lib` is both the reference assembly and the implementation assembly.</span></span> |
| <span data-ttu-id="cd1c5-150">Runtimes</span><span class="sxs-lookup"><span data-stu-id="cd1c5-150">Runtimes</span></span> | <span data-ttu-id="cd1c5-151">`runtimes` é uma pasta opcional que contém o código específico do sistema operacional, como a arquitetura de CPU e binários do sistema operacional específicos ou dependentes da plataforma.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-151">`runtimes` is an optional folder that contains OS specific code, such as CPU architecture and OS specific or otherwise platform-dependent binaries.</span></span> |

## <a name="msbuild-targets-and-props-files-in-packages"></a><span data-ttu-id="cd1c5-152">Arquivos de destino e objetos do MSBuild em pacotes</span><span class="sxs-lookup"><span data-stu-id="cd1c5-152">MSBuild targets and props files in packages</span></span>

<span data-ttu-id="cd1c5-153">Pacotes do NuGet podem conter arquivos `.targets` e `.props` que são importados para qualquer projeto do MSBuild em que o pacote é instalado.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-153">NuGet packages can contain `.targets` and `.props` files which are imported into any MSBuild project that the package is installed into.</span></span> <span data-ttu-id="cd1c5-154">No NuGet 2.x, isso foi feito injetando instruções `<Import>` no arquivo `.csproj`, enquanto no NuGet 3.0 não há nenhuma ação de “instalação específica no projeto”.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-154">In NuGet 2.x, this was done by injecting `<Import>` statements into the `.csproj` file, in NuGet 3.0 there is no specific "installation to project" action.</span></span> <span data-ttu-id="cd1c5-155">Em vez disso, o processo de restauração do pacote grava dois arquivos `[projectname].nuget.props` e `[projectname].NuGet.targets`.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-155">Instead the package restore process writes two files `[projectname].nuget.props` and `[projectname].NuGet.targets`.</span></span>

<span data-ttu-id="cd1c5-156">O MSBuild sabe procurar esses dois arquivos e os importa automaticamente próximo ao início e no final do processo de build do projeto.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-156">MSBuild knows to look for these two files and automatically imports them near the beginning and near the end of the project build process.</span></span> <span data-ttu-id="cd1c5-157">Isso fornece um comportamento muito semelhante ao NuGet 2.x, mas com uma grande diferença: *não há nenhuma garantia da ordem dos arquivos de destinos/objetos neste caso*.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-157">This provides very similar behavior to NuGet 2.x, but with one major difference: *there is no guaranteed order of targets/props files in this case*.</span></span> <span data-ttu-id="cd1c5-158">No entanto, o MSBuild fornece maneiras de ordenar destinos por meio dos atributos `BeforeTargets` e `AfterTargets` da definição `<Target>` (consulte [Elemento de Destino (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span><span class="sxs-lookup"><span data-stu-id="cd1c5-158">However, MSBuild does provide ways to order targets through the `BeforeTargets` and `AfterTargets` attributes of the `<Target>` definition (see [Target Element (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span></span>

## <a name="lib-and-ref"></a><span data-ttu-id="cd1c5-159">Lib e Ref</span><span class="sxs-lookup"><span data-stu-id="cd1c5-159">Lib and Ref</span></span>

<span data-ttu-id="cd1c5-160">O comportamento da pasta `lib` ainda não foi alterado significativamente no NuGet v3.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-160">The behavior of the `lib` folder hasn't changed significantly in NuGet v3.</span></span> <span data-ttu-id="cd1c5-161">No entanto, todos os assemblies devem estar dentro de subpastas nomeadas com um TxM e não pode ser colocados diretamente na pasta `lib`.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-161">However, all assemblies must be within sub-folders named after a TxM, and can no longer be placed directly under the `lib` folder.</span></span> <span data-ttu-id="cd1c5-162">Um TxM é o nome de uma plataforma para a qual determinado ativo em um pacote trabalha.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-162">A TxM is the name of a platform that a given asset in a package is supposed to work for.</span></span> <span data-ttu-id="cd1c5-163">Logicamente, isso é uma extensão do TFM (Moniker do Framework de Destino), por exemplo, `net45`, `net46`, `netcore50` e `dnxcore50` são exemplos de TxMs (consulte [Estrutura de destino](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="cd1c5-163">Logically these are an extension of the Target Framework Monikers (TFM) e.g. `net45`, `net46`, `netcore50`, and `dnxcore50` are all examples of TxMs (see [Target Frameworks](../reference/target-frameworks.md).</span></span> <span data-ttu-id="cd1c5-164">O TxM pode se referir a uma estrutura (TFM), bem como outras áreas da superfície específicas da plataforma.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-164">TxM can refer to a framework (TFM) as well as other platform-specific surface areas.</span></span> <span data-ttu-id="cd1c5-165">Por exemplo, o TxM de UWP (`uap10.0`) representa a área de superfície do .NET, bem como a área de superfície do Windows para aplicativos UWP.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-165">For example the UWP TxM (`uap10.0`) represents the .NET surface area as well as the Windows surface area for UWP applications.</span></span>

<span data-ttu-id="cd1c5-166">Um exemplo de estrutura de lib:</span><span class="sxs-lookup"><span data-stu-id="cd1c5-166">An example lib structure:</span></span>

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

<span data-ttu-id="cd1c5-167">A pasta `lib` contém os assemblies que são usados no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-167">The `lib` folder contains assemblies that are used at runtime.</span></span> <span data-ttu-id="cd1c5-168">Para a maioria dos pacotes, tudo o que é necessário é uma pasta em `lib` para cada destino TxMs.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-168">For most packages a folder under `lib` for each of the target TxMs is all that is required.</span></span>

## <a name="ref"></a><span data-ttu-id="cd1c5-169">Ref</span><span class="sxs-lookup"><span data-stu-id="cd1c5-169">Ref</span></span>

<span data-ttu-id="cd1c5-170">Às vezes, há casos em que um assembly diferente deve ser usado durante a compilação (Assemblies de referência do .NET fazem isso atualmente).</span><span class="sxs-lookup"><span data-stu-id="cd1c5-170">There are sometimes cases where a different assembly should be used during compilation (.NET Reference Assemblies do this today).</span></span> <span data-ttu-id="cd1c5-171">Para esses casos, use uma pasta de nível superior chamada `ref` (abreviação de “Assemblies de Referência”).</span><span class="sxs-lookup"><span data-stu-id="cd1c5-171">For those cases, use a top-level folder called `ref` (short for "Reference Assemblies").</span></span>

<span data-ttu-id="cd1c5-172">A maioria dos autores de pacote não exigem a pasta `ref`.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-172">Most package authors don't require the `ref` folder.</span></span> <span data-ttu-id="cd1c5-173">É útil para os pacotes que precisam fornecer uma área de superfície consistente para compilação e IntelliSense, mas têm uma implementação diferente para TxMs diferentes.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-173">It is useful for packages that need to provide a consistent surface area for compilation and IntelliSense but then have different implementation for different TxMs.</span></span> <span data-ttu-id="cd1c5-174">O maior caso de uso são os pacotes `System.*` que estão sendo produzidos como parte do envio de .NET Core no NuGet.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-174">The biggest use case of this are the `System.*` packages that are being produced as part of shipping .NET Core on NuGet.</span></span> <span data-ttu-id="cd1c5-175">Estes pacotes têm várias implementações que estão sendo unificadas por um conjunto consistente de assemblies de referência.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-175">These packages have various implementations that are being unified by a consistent set of ref assemblies.</span></span>

<span data-ttu-id="cd1c5-176">Mecanicamente, os assemblies incluídos na pasta `ref` são os assemblies de referência que estão sendo passados para o compilador.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-176">Mechanically, the assemblies included in the `ref` folder are the reference assemblies being passed to the compiler.</span></span> <span data-ttu-id="cd1c5-177">Para aqueles dentre vocês que usaram csc.exe, esses são os assemblies que estamos passando para a opção [C# /reference option](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option).</span><span class="sxs-lookup"><span data-stu-id="cd1c5-177">For those of you who have used csc.exe these are the assemblies we are passing to the [C# /reference option](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) switch.</span></span>

<span data-ttu-id="cd1c5-178">A estrutura da pasta `ref` é o mesmo que `lib`, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="cd1c5-178">The structure of the `ref` folder is the same as `lib`, for example:</span></span>

    └───MyImageProcessingLib
         ├───lib
         │   ├───net40
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   ├───net451
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   └───win81
         │           MyImageProcessingLibrary.dll
         │
         └───ref
             ├───net40
             │       MyImageProcessingLibrary.dll
             │
             └───portable-net451-win81
                     MyImageProcessingLibrary.dll

<span data-ttu-id="cd1c5-179">Neste exemplo, os assemblies nos diretórios `ref` serão idênticos.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-179">In this example the assemblies in the `ref` directories would all be identical.</span></span>

## <a name="runtimes"></a><span data-ttu-id="cd1c5-180">Runtimes</span><span class="sxs-lookup"><span data-stu-id="cd1c5-180">Runtimes</span></span>

<span data-ttu-id="cd1c5-181">A pasta de runtimes contém os assemblies e bibliotecas nativos necessários para executar em “runtimes” específicos, que geralmente são definidos pelo sistema operacional e arquitetura de CPU.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-181">The runtimes folder contains assemblies and native libraries required to run on specific "runtimes", which are generally defined by Operating System and CPU architecture.</span></span> <span data-ttu-id="cd1c5-182">Esses tempos de execução são identificados usando [RIDs (Identificadores de tempo de execução)](/dotnet/core/rid-catalog) como `win`, `win-x86`, `win7-x86`, `win8-64`, etc.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-182">These runtimes are identified using [Runtime Identifiers (RIDs)](/dotnet/core/rid-catalog) such as `win`, `win-x86`, `win7-x86`, `win8-64`, etc.</span></span>

## <a name="native-helpers-to-use-platform-specific-apis"></a><span data-ttu-id="cd1c5-183">Auxiliares nativo para usar APIs específicas de plataforma</span><span class="sxs-lookup"><span data-stu-id="cd1c5-183">Native helpers to use platform-specific APIs</span></span>

<span data-ttu-id="cd1c5-184">O exemplo a seguir mostra um pacote que tem uma implementação totalmente gerenciada para várias plataformas, mas usa auxiliares nativos no Windows 8, em que ele pode chamar APIs nativas específicas do Windows 8.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-184">The following example shows a package that has a purely managed implementation for several platforms, but uses native helpers on Windows 8 where it can call into Windows 8-specific native APIs.</span></span>

    └───MyLibrary
         ├───lib
         │   └───net40
         │           MyLibrary.dll
         │
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net40
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyNativeLibrary.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net40
                 │           MyLibrary.dll
                 │
                 └───native
                         MyNativeLibrary.dll

<span data-ttu-id="cd1c5-185">Considerando o pacote acima, acontece o seguinte:</span><span class="sxs-lookup"><span data-stu-id="cd1c5-185">Given the above package the following things happen:</span></span>

- <span data-ttu-id="cd1c5-186">Quando não está no Windows 8, o assembly `lib/net40/MyLibrary.dll` é usado.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-186">When not on Windows 8 the `lib/net40/MyLibrary.dll` assembly is used.</span></span>

- <span data-ttu-id="cd1c5-187">No Windows 8, o `runtimes/win8-<architecture>/lib/MyLibrary.dll` é usado e o `native/MyNativeHelper.dll` é copiado para a saída do build.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-187">When on Windows 8 the `runtimes/win8-<architecture>/lib/MyLibrary.dll` is used and the `native/MyNativeHelper.dll` is copied to the output of your build.</span></span>

<span data-ttu-id="cd1c5-188">No exemplo acima, o assembly `lib/net40` é composto puramente por código gerenciado, embora os assemblies na pasta de tempos de execução serão p/invoke para o assembly auxiliar nativo para chamar as APIs específicas para o Windows 8.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-188">In the example above the `lib/net40` assembly is purely managed code, whilst the assemblies in the runtimes folder will p/invoke into the native helper assembly to call APIs specific to Windows 8.</span></span>

<span data-ttu-id="cd1c5-189">Somente uma pasta `lib` única será escolhida, por isso se houver uma pasta específica do tempo de execução, ela será escolhida em vez do `lib` específico fora do tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-189">Only a single `lib` folder is ever be picked, so if there is a runtime specific folder it's chosen over non-runtime specific `lib`.</span></span> <span data-ttu-id="cd1c5-190">A pasta nativa é aditiva, se existir, ela é copiada para a saída do build.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-190">The native folder is additive, if it exists it's copied to the output of the build.</span></span>

## <a name="managed-wrapper"></a><span data-ttu-id="cd1c5-191">Wrapper gerenciado</span><span class="sxs-lookup"><span data-stu-id="cd1c5-191">Managed wrapper</span></span>

<span data-ttu-id="cd1c5-192">Outra maneira de usar os runtimes é fornecer um pacote que é essencialmente um wrapper gerenciado em um assembly nativo.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-192">Another way to use runtimes is to ship a package that is purely a managed wrapper over a native assembly.</span></span> <span data-ttu-id="cd1c5-193">Neste cenário, você cria um pacote como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="cd1c5-193">In this scenario you create a package like the following:</span></span>

    └───MyLibrary
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net451
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyImplementation.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net451
                 │           MyLibrary.dll
                 │
                 └───native
                         MyImplementation.dll

<span data-ttu-id="cd1c5-194">Nesse caso não há pasta `lib` de nível superior, pois não há nenhuma implementação desse pacote que não conte com o assembly nativo correspondente.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-194">In this case there is no top-level `lib` folder as that folder as there is no implementation of this package that doesn't rely on the corresponding native assembly.</span></span> <span data-ttu-id="cd1c5-195">Se o assembly gerenciado, `MyLibrary.dll`, era exatamente o mesmo em ambos os casos, poderíamos colocá-lo em uma pasta `lib` de nível superior, mas como a falta de um assembly nativo não causa falha de instalação do pacote, se ele foi instalado em uma plataforma que não era win-x86 ou win-x64, a biblioteca de nível superior será usada, mas nenhum assembly nativo será copiado.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-195">If the managed assembly, `MyLibrary.dll`, was exactly the same in both of these cases then we could put it in a top level `lib` folder, but because the lack of a native assembly doesn't cause the package to fail installing if it was installed on a platform that wasn't win-x86 or win-x64 then the top level lib would be used but no native assembly would be copied.</span></span>

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a><span data-ttu-id="cd1c5-196">Criação de pacotes do NuGet 2 e 3</span><span class="sxs-lookup"><span data-stu-id="cd1c5-196">Authoring packages for NuGet 2 and NuGet 3</span></span>

<span data-ttu-id="cd1c5-197">Se você deseja criar um pacote que pode ser consumido por projetos usando o `packages.config`, bem como pacotes que usam o `project.json`, o seguinte se aplica:</span><span class="sxs-lookup"><span data-stu-id="cd1c5-197">If you want to create a package that can be consumed by projects using `packages.config` as well as packages using `project.json` then the following apply:</span></span>

- <span data-ttu-id="cd1c5-198">REF e runtimes só funcionam no NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-198">Ref and runtimes only work on NuGet 3.</span></span> <span data-ttu-id="cd1c5-199">Eles são ambos ignorados pelo NuGet 2.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-199">They are both ignored by NuGet 2.</span></span>

- <span data-ttu-id="cd1c5-200">Você não pode contar que `install.ps1` ou `uninstall.ps1` funcionem.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-200">You cannot rely on `install.ps1` or `uninstall.ps1` to function.</span></span> <span data-ttu-id="cd1c5-201">Esses arquivos são executados ao usar `packages.config`, mas são ignorados com `project.json`.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-201">These files execute when using `packages.config`, but are ignored with `project.json`.</span></span> <span data-ttu-id="cd1c5-202">Assim, seu pacote precisa ser usado quando eles não estiverem em execução.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-202">So your package needs to be usable without them running.</span></span> <span data-ttu-id="cd1c5-203">`init.ps1` ainda é executado no NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-203">`init.ps1` still runs on NuGet 3.</span></span>

- <span data-ttu-id="cd1c5-204">A instalação de Destinos e Objetos é diferente, por isso verifique se seu pacote funciona conforme o esperado em ambos os clientes.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-204">Targets and Props installation is different, so make sure that your package works as expected on both clients.</span></span>

- <span data-ttu-id="cd1c5-205">Os subdiretórios de lib devem ser um TxM do NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-205">Subdirectories of lib must be a TxM in NuGet 3.</span></span> <span data-ttu-id="cd1c5-206">Não é possível colocar as bibliotecas na raiz da pasta `lib`.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-206">You cannot place libraries at the root of the `lib` folder.</span></span>

- <span data-ttu-id="cd1c5-207">O conteúdo não é copiado automaticamente com o NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-207">Content is not copied automatically with NuGet 3.</span></span> <span data-ttu-id="cd1c5-208">Os consumidores do seu pacote poderia copiar os próprios arquivos ou usar uma ferramenta como um executor de tarefas para automatizar a cópia dos arquivos.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-208">Consumers of your package could copy the files themselves or use a tool like a task runner to automate copying the files.</span></span>

- <span data-ttu-id="cd1c5-209">Transformações de arquivo de configuração e de origem não são executadas pelo NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-209">Source and config file transforms are not run by NuGet 3.</span></span>

<span data-ttu-id="cd1c5-210">Se você estiver dando suporte ao NuGet 2 e 3, seu `minClientVersion` deverá ter a versão mais antiga do cliente do NuGet 2 na qual seu pacote funciona.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-210">If you are supporting NuGet 2 and 3 then your `minClientVersion` should be the lowest version of NuGet 2 client that your package works on.</span></span> <span data-ttu-id="cd1c5-211">No caso de um pacote existente, ele não deve precisar ser alterado.</span><span class="sxs-lookup"><span data-stu-id="cd1c5-211">In the case of an existing package it shouldn't need to change.</span></span>
