---
title: Criar pacotes do NuGet do .NET Standard 2.0 com o Visual Studio 2017 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 5/23/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c1de334-fdc9-4e1e-8ef6-a90b3e77ff0f
description: "Uma explicação passo a passo de ponta a ponta da criação de pacotes do NuGet do .NET Standard 2.0 usando o NuGet 4.x e o Visual Studio 2017."
keywords: criar um pacote, pacotes do .NET Standard, .NET Core
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5b48ad2f062fd3a9b99985dbda6f89e6039dac4d
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="create-net-standard-20-packages-with-visual-studio-2017"></a><span data-ttu-id="729b4-104">Criar pacotes do .NET Standard 2.0 com o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="729b4-104">Create .NET Standard 2.0 packages with Visual Studio 2017</span></span>

<span data-ttu-id="729b4-105">*Aplica-se ao NuGet 4.x ou superior e o MSBuild 15.3 ou superior fornecido com o Visual Studio 2017 Atualização 3. Para versões anteriores do Visual Studio 2017, estas instruções se aplicam ao .NET Standard 1.4 a 1.6 alterando a propriedade \<TargetFramework\>. Consulte também [Criar pacotes do .NET Standard com o Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md) para trabalhar com o NuGet 3.x ou superior.*</span><span class="sxs-lookup"><span data-stu-id="729b4-105">*Applies to NuGet 4.x+ and MSBuild 15.3+ as provided with Visual Studio 2017 Update 3. For earlier versions of Visual Studio 2017, these instructions apply to .NET Standard 1.4 to 1.6 by changing the \<TargetFramework\> property. Also see [Create .NET Standard Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md) for working with NuGet 3.x+.*</span></span>

<span data-ttu-id="729b4-106">A [Biblioteca do .NET Standard](/dotnet/articles/standard/library) é uma especificação formal de APIs .NET que devem estar disponíveis em todos os tempos de execução do .NET, estabelecendo dessa forma uma maior uniformidade no ecossistema do .NET.</span><span class="sxs-lookup"><span data-stu-id="729b4-106">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="729b4-107">A Biblioteca do .NET Standard define um conjunto uniforme de APIs de BCL (Biblioteca de Classes Base) para implementação em todas as plataformas do .NET, independentemente da carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="729b4-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="729b4-108">Ele permite que os desenvolvedores produzam PCLs que podem ser usados em todos os tempos de execução do .NET e reduz ou elimina as diretivas de compilação condicional específicas da plataforma em código compartilhado.</span><span class="sxs-lookup"><span data-stu-id="729b4-108">It enables developers to produce PCLs that are usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="729b4-109">Este guia orientará você durante a criação de um pacote do nuget direcionado para a Biblioteca do .NET Standard 2.0 com o Visual Studio 2017 Atualização 3 e o NuGet 4.0.</span><span class="sxs-lookup"><span data-stu-id="729b4-109">This guide will walk you through creating a nuget package targeting .NET Standard Library 2.0 with Visual Studio 2017 Update 3 and NuGet 4.0.</span></span>

1. [<span data-ttu-id="729b4-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="729b4-110">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="729b4-111">Criar o projeto da biblioteca de classes</span><span class="sxs-lookup"><span data-stu-id="729b4-111">Create the class library project</span></span>](#create-the-netstandard-class-library-project)
1. [<span data-ttu-id="729b4-112">Editar metadados no arquivo .csproj</span><span class="sxs-lookup"><span data-stu-id="729b4-112">Edit metadata in the .csproj file</span></span>](#edit-metadata-in-the-csproj-file)
1. [<span data-ttu-id="729b4-113">Empacotar o componente</span><span class="sxs-lookup"><span data-stu-id="729b4-113">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="729b4-114">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="729b4-114">Related topics</span></span>](#related-topics)

## <a name="pre-requisites"></a><span data-ttu-id="729b4-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="729b4-115">Pre-requisites</span></span>

<span data-ttu-id="729b4-116">Esta explicação passo a passo requer o Visual Studio 2017 Atualização 3 com a carga de trabalho **Desenvolvimento de multiplaforma do .NET Core**.</span><span class="sxs-lookup"><span data-stu-id="729b4-116">This walkthrough requires Visual Studio 2017 Update 3 with the **.NET Core cross-platform development** workload.</span></span> <span data-ttu-id="729b4-117">Você pode instalar a edição Community gratuitamente no [visualstudio.com](https://www.visualstudio.com/) ou usar as edições Professional e Enterprise.</span><span class="sxs-lookup"><span data-stu-id="729b4-117">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/), or use the Professional and Enterprise editions.</span></span>

<span data-ttu-id="729b4-118">A carga de trabalho exigida aparece da seguinte maneira no instalador do Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="729b4-118">The require workload appears as follows in the Visual Studio installer:</span></span>

![Carga de trabalho de desenvolvimento multiplataforma do .NET Core no Instalador do Visual Studio](media/NuGet4-01-Workload.png)

## <a name="create-the-net-standard-class-library-project"></a><span data-ttu-id="729b4-120">Cria o projeto da biblioteca de classe do .NET Standard</span><span class="sxs-lookup"><span data-stu-id="729b4-120">Create the .NET Standard class library project</span></span>

1. <span data-ttu-id="729b4-121">No Visual Studio, **Arquivo > Novo > Projeto**, expanda o nó **Visual C# > .NET Standard**, selecione **Biblioteca de Classes (Net Standard)**, altere o nome para AppLogger e clique em OK.</span><span class="sxs-lookup"><span data-stu-id="729b4-121">In Visual Studio, **File > New > Project**, expand the **Visual C# > .NET Standard** node, select **Class Library (Net Standard)**, change the name to AppLogger, and click OK.</span></span>

    ![Criar um novo projeto de biblioteca de classes](media/NuGet4-02-NewProject.png)

1. <span data-ttu-id="729b4-123">Altere a configuração de build para **Versão**.</span><span class="sxs-lookup"><span data-stu-id="729b4-123">Change the build configuration to **Release**.</span></span>
1. <span data-ttu-id="729b4-124">Clique com o botão direito do mouse no projeto `AppLogger` no Gerenciador de Soluções, selecione **Propriedades**, selecione a guia **Criar**, marque a caixa de **arquivo de documentação XML** e defina o nome de arquivo para apenas `AppLogger.xml`.</span><span class="sxs-lookup"><span data-stu-id="729b4-124">Right-click the `AppLogger` project in Solution Explorer, select **Properties**, select the **Build** tab, check the box for **XML documentation file**, and set the filename to just `AppLogger.xml`.</span></span> <span data-ttu-id="729b4-125">Em seguida, salve o projeto.</span><span class="sxs-lookup"><span data-stu-id="729b4-125">Then save the project.</span></span>

1. <span data-ttu-id="729b4-126">Adicione seu código ao componente, como mostrado a seguir (que claramente apenas envia as mensagens como saída para o console):</span><span class="sxs-lookup"><span data-stu-id="729b4-126">Add your code to the component, such as the following (which clearly just outputs messages to the console):</span></span>

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. <span data-ttu-id="729b4-127">Compile o projeto (com a configuração de Versão) e verifique se os arquivos DLL e XML são produzidos dentro da pasta `bin\Release\netstandard2.0`.</span><span class="sxs-lookup"><span data-stu-id="729b4-127">Build the project (with the Release configuration) and check that DLL and XML files are produced within the `bin\Release\netstandard2.0` folder.</span></span>

## <a name="edit-metadata-in-the-csproj-file"></a><span data-ttu-id="729b4-128">Editar metadados no arquivo .csproj</span><span class="sxs-lookup"><span data-stu-id="729b4-128">Edit metadata in the .csproj file</span></span>

<span data-ttu-id="729b4-129">Com projetos do NuGet 4.0 e .NET Core, os metadados de pacote estão contidos diretamente no arquivo `.csproj` em vez de arquivos externos, como um `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="729b4-129">With NuGet 4.0 and .NET Core projects, package metadata is contained directly in the `.csproj` file instead of external files such as a `.nuspec`.</span></span> <span data-ttu-id="729b4-130">Uma descrição completa dos metadados é encontrada em [Empacotamento e restauração do NuGet como destinos do MSBuild](../schema/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="729b4-130">A full description of that metadata is found in [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target).</span></span>

1. <span data-ttu-id="729b4-131">Clique com botão direito do mouse no projeto no Gerenciador de Soluções, selecione **Editar AppLogger.csproj** e, em seguida, edite o primeiro grupo de propriedades para incluir informações de pacote como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="729b4-131">Right-click the project in Solution Explorer, select **Edit AppLogger.csproj**, and then edit the first property group to include package information such as the following:</span></span>

    ```xml
    <PropertyGroup>
        <TargetFramework>netstandard2.0</TargetFramework>
        <PackageId>AppLogger.YOUR_NAME</PackageId>
        <PackageVersion>1.0.0</PackageVersion>
        <Authors>YOUR_NAME</Authors>
        <Description>Awesome application logging utility</Description>
        <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
        <PackageReleaseNotes>First release</PackageReleaseNotes>
        <Copyright>Copyright 2017 (c) Contoso Corporation. All rights reserved.</Copyright>
        <PackageTags>logger logging logs</PackageTags>
    </PropertyGroup>
    ```

1. <span data-ttu-id="729b4-132">Salve o projeto, clique com o botão direito do mouse na solução e selecione **Compilar solução**, novamente, para gerar todos os arquivos de pacote, dessa vez com os metadados corretos.</span><span class="sxs-lookup"><span data-stu-id="729b4-132">Save the project, then right-click the solution and select **Build Solution** to again generate all the files for the package, this time with the correct metadata.</span></span>


## <a name="package-the-component"></a><span data-ttu-id="729b4-133">Empacotar o componente</span><span class="sxs-lookup"><span data-stu-id="729b4-133">Package the component</span></span>

<span data-ttu-id="729b4-134">O NuGet 4.0 é compatível com um destino de pacote que usa o MSBuild versão 15.1 ou superior (incluindo MSBuild 15.3 como parte do Visual Studio 2017 Atualização 3) quando o projeto contém os metadados de pacote necessários, que foi adicionado na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="729b4-134">NuGet 4.0 supports a pack target using MSBuild version 15.1+ (including MSBuild 15.3 as part of Visual Studio 2017 Update 3) when the project contains the necessary package metadata, as was added in the previous section.</span></span> <span data-ttu-id="729b4-135">Para invocar o MSBuild dessa forma, basta especificar o destino do pacote na linha de comando na mesma pasta que o arquivo `.csproj`:</span><span class="sxs-lookup"><span data-stu-id="729b4-135">To invoke MSBuild in this way, simply specify the pack target on the command line in the same folder as the `.csproj` file:</span></span>

    msbuild /t:pack /p:Configuration=Release

<span data-ttu-id="729b4-136">Para ver opções adicionais com `msbuild /t:pack`, tal como incluir arquivos de conteúdo, símbolos e código-fonte, consulte [Empacotamento e restauração do NuGet como destinos do MSBuild](../schema/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="729b4-136">For additional options with `msbuild /t:pack`, such as including content files, symbols, and source code, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target).</span></span>

<span data-ttu-id="729b4-137">Em qualquer caso, o comando acima gera `AppLogger.YOUR_NAME.1.0.0.nupkg` na pasta `bin\Release` por padrão, pois ele compila essa configuração.</span><span class="sxs-lookup"><span data-stu-id="729b4-137">In any case, the command above generates `AppLogger.YOUR_NAME.1.0.0.nupkg` in the `bin\Release` folder by default, as it builds that configuration.</span></span> <span data-ttu-id="729b4-138">Se você omitir a opção `/p`, a configuração padrão será `Debug`.</span><span class="sxs-lookup"><span data-stu-id="729b4-138">If you omit the `/p` switch, the default configuration will be `Debug`.</span></span> 

<span data-ttu-id="729b4-139">Ao abrir este arquivo em uma ferramenta como o [Explorador de Pacotes do NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) e expandir todos os nós, você verá o seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="729b4-139">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![O Explorador de Pacotes do NuGet mostrando o pacote AppLogger](media/NuGet4-03-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="729b4-141">O arquivo `.nupkg` é apenas um arquivo ZIP com uma extensão diferente.</span><span class="sxs-lookup"><span data-stu-id="729b4-141">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="729b4-142">Também é possível examinar o conteúdo do pacote alterando `.nupkg` para `.zip`, mas lembre-se de restaurar a extensão antes de carregar um pacote para o nuget.org.</span><span class="sxs-lookup"><span data-stu-id="729b4-142">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="729b4-143">Para disponibilizar seu pacote para outros desenvolvedores, siga as instruções em [Publicar um pacote](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="729b4-143">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="729b4-144">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="729b4-144">Related topics</span></span>

- <span data-ttu-id="729b4-145">[Referências de pacote nos arquivos de projeto](../consume-packages/package-references-in-project-files.md) descreve todos os detalhes de descrever seu pacote diretamente no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="729b4-145">[Package References in Project Files](../consume-packages/package-references-in-project-files.md) describes all the details of describing your package directly in the project file.</span></span>
- <span data-ttu-id="729b4-146">[Empacotamento e restauração do NuGet como destinos do MSBuild](../schema/msbuild-targets.md) descreve todas as opções para usar `msbuild /t:pack` para criar o pacote.</span><span class="sxs-lookup"><span data-stu-id="729b4-146">[NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md) describes all the options for using `msbuild /t:pack` to create the package.</span></span>
- [<span data-ttu-id="729b4-147">Documentação da Biblioteca do .NET Standard</span><span class="sxs-lookup"><span data-stu-id="729b4-147">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="729b4-148">Portabilidade para o .NET Core do .NET Framework</span><span class="sxs-lookup"><span data-stu-id="729b4-148">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
