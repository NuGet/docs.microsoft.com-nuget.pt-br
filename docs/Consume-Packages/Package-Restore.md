---
title: "Restauração do pacote do NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Uma descrição de como o NuGet restaura os pacotes dos quais um projeto depende, incluindo como desabilitar a restauração e restringir as versões."
keywords: "Restauração de pacote do NuGet, instalação de pacote do NuGet, instalar o pacote, restaurando pacotes, versões de dependência, desabilitar a restauração automática, restringindo as versões do pacote"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4e819a2bb34bbe70f0f11d5adeed82b976a8cb65
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="package-restore"></a><span data-ttu-id="4f75c-104">Restauração de pacote</span><span class="sxs-lookup"><span data-stu-id="4f75c-104">Package Restore</span></span>

<span data-ttu-id="4f75c-105">Para promover um ambiente de desenvolvimento mais limpo e reduzir o tamanho do repositório, a **Restauração de pacote** do NuGet instala todos os pacotes referenciados antes de um projeto ser compilado.</span><span class="sxs-lookup"><span data-stu-id="4f75c-105">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all referenced packages before a project is built.</span></span> <span data-ttu-id="4f75c-106">Esse recurso amplamente utilizado garante que todas as dependências estejam disponíveis em um projeto sem precisar armazenar tais pacotes no controle do código-fonte (consulte [Pacotes e controle do código-fonte](../consume-packages/packages-and-source-control.md) para ver como configurar seu repositório para excluir binários de pacote).</span><span class="sxs-lookup"><span data-stu-id="4f75c-106">This widely-used feature ensures that all dependencies are available in a project without requiring those packages to be stored in source control (see [Packages and Source Control](../consume-packages/packages-and-source-control.md) on how to configure your repository to exclude package binaries).</span></span>

<span data-ttu-id="4f75c-107">Neste tópico:</span><span class="sxs-lookup"><span data-stu-id="4f75c-107">In this topic:</span></span>
- [<span data-ttu-id="4f75c-108">Guia rápido de restauração de pacote</span><span class="sxs-lookup"><span data-stu-id="4f75c-108">Quick guide to package restore</span></span>](#quick-guide-to-package-restore)
- [<span data-ttu-id="4f75c-109">Visão geral de restauração de pacote</span><span class="sxs-lookup"><span data-stu-id="4f75c-109">Package restore overview</span></span>](#package-restore-overview)
- [<span data-ttu-id="4f75c-110">Habilitar e desabilitar a restauração do pacote</span><span class="sxs-lookup"><span data-stu-id="4f75c-110">Enabling and disabling package restore</span></span>](#enabling-and-disabling-package-restore)
- [<span data-ttu-id="4f75c-111">Restrições de versões de pacote com restauração</span><span class="sxs-lookup"><span data-stu-id="4f75c-111">Constraining package versions with restore</span></span>](#constraining-package-versions-with-restore)
- <span data-ttu-id="4f75c-112">[Restauração de linha de comando](#command-line-restore) para todas as versões do NuGet</span><span class="sxs-lookup"><span data-stu-id="4f75c-112">[Command-line restore](#command-line-restore), for all versions of NuGet</span></span>
- <span data-ttu-id="4f75c-113">[Restauração automática no Visual Studio](#automatic-restore-in-visual-studio) para o NuGet 2.7 e posterior.</span><span class="sxs-lookup"><span data-stu-id="4f75c-113">[Automatic restore in Visual Studio](#automatic-restore-in-visual-studio), for NuGet 2.7 and later.</span></span>
- <span data-ttu-id="4f75c-114">[Restauração integrada do MSBuild no Visual Studio](#msbuild-integrated-restore) para o NuGet 2.6 e versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="4f75c-114">[MSBuild-integrated restore in Visual Studio](#msbuild-integrated-restore), for NuGet 2.6 and earlier.</span></span>
- [<span data-ttu-id="4f75c-115">Restauração de pacote com o Team Foundation Build</span><span class="sxs-lookup"><span data-stu-id="4f75c-115">Package restore with Team Foundation Build</span></span>](#package-restore-with-team-foundation-build)

<span data-ttu-id="4f75c-116">O comportamento de restauração varia de acordo com a versão; para verificar a versão do NuGet, basta executar `nuget.exe` na linha de comando e examinar a primeira linha de saída.</span><span class="sxs-lookup"><span data-stu-id="4f75c-116">Restore behavior does vary by version; to check your NuGet version, simply run `nuget.exe` on the command line and look at the first line of output.</span></span>

<span data-ttu-id="4f75c-117">Para ver detalhes adicionais sobre a restauração de pacote nos servidores de build, consulte [Restauração de pacote com TFBuild](../consume-packages/team-foundation-build.md).</span><span class="sxs-lookup"><span data-stu-id="4f75c-117">For additional details on package restore on build servers, see [Package restore with TFBuild](../consume-packages/team-foundation-build.md).</span></span>

> [!Note]
> <span data-ttu-id="4f75c-118">Projetos configurados para restauração de pacote também funcionam com xbuild no Mono.</span><span class="sxs-lookup"><span data-stu-id="4f75c-118">Projects configured for package restore also work with xbuild on Mono.</span></span>

## <a name="quick-guide-to-package-restore"></a><span data-ttu-id="4f75c-119">Guia rápido de restauração de pacote</span><span class="sxs-lookup"><span data-stu-id="4f75c-119">Quick guide to package restore</span></span>

[!INCLUDE[package-restore](../includes/package-restore.md)]

> [!Note]
> <span data-ttu-id="4f75c-120">Se você encontrar o erro “Este projeto faz referência a pacotes do NuGet que estão ausentes neste computador” ou “Um ou mais pacotes do NuGet precisam ser restaurados, mas não foi possível fazer isso, pois o consentimento não foi concedido”, ative a restauração automática seguindo as instruções em [Habilitando e desabilitando a restauração do pacote](#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="4f75c-120">If you see the error "This project references NuGet package(s) that are missing on this computer" or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," turn on automatic restore by following the instructions under [Enabling and disabling package restore](#enabling-and-disabling-package-restore).</span></span>

## <a name="package-restore-overview"></a><span data-ttu-id="4f75c-121">Visão geral de restauração de pacote</span><span class="sxs-lookup"><span data-stu-id="4f75c-121">Package restore overview</span></span>

<span data-ttu-id="4f75c-122">Primeiro, as referências de pacote são mantidas em um dos seguintes formatos de gerenciamento de pacotes, dependendo do tipo de projeto e a versão do NuGet.</span><span class="sxs-lookup"><span data-stu-id="4f75c-122">First, package references are maintained in one of the following package management formats, depending on project type and NuGet version.</span></span> <span data-ttu-id="4f75c-123">(Observe que o NuGet 4 e o MSBuild 15.1 são instalados com o Visual Studio 2017.)</span><span class="sxs-lookup"><span data-stu-id="4f75c-123">(Note that NuGet 4 and MSBuild 15.1 are installed with Visual Studio 2017.)</span></span>

| <span data-ttu-id="4f75c-124">Método</span><span class="sxs-lookup"><span data-stu-id="4f75c-124">Method</span></span> | <span data-ttu-id="4f75c-125">Versão do NuGet</span><span class="sxs-lookup"><span data-stu-id="4f75c-125">NuGet Version</span></span> | <span data-ttu-id="4f75c-126">Descrição</span><span class="sxs-lookup"><span data-stu-id="4f75c-126">Description</span></span> | 
| --- | --- | --- |
| `packages.config` | <span data-ttu-id="4f75c-127">2.x ou superior</span><span class="sxs-lookup"><span data-stu-id="4f75c-127">2.x+</span></span> | <span data-ttu-id="4f75c-128">Lista o conjunto aprofundado completo de dependências.</span><span class="sxs-lookup"><span data-stu-id="4f75c-128">Lists the complete deep set of dependencies.</span></span> <span data-ttu-id="4f75c-129">Pacotes adicionados ao `packages.config` também precisam ser adicionados ao arquivo de projeto, assim como os Destinos e Objetos.</span><span class="sxs-lookup"><span data-stu-id="4f75c-129">Packages added to `packages.config` must also be added to the project file, and Targets and Props must also be added to the project file.</span></span> <span data-ttu-id="4f75c-130">Esse é o método de linha de base para todas as versões do NuGet, mas tem um desempenho mais lento comparado com as outras opções.</span><span class="sxs-lookup"><span data-stu-id="4f75c-130">This is the baseline method for all versions of NuGet, but has slower performance compared with the other options.</span></span> <span data-ttu-id="4f75c-131">(Consulte [Esquema packages.config](../schema/packages-config.md).)</span><span class="sxs-lookup"><span data-stu-id="4f75c-131">(See [packages.config schema](../schema/packages-config.md).)</span></span> | 
| `project.json` | <span data-ttu-id="4f75c-132">3.x ou superior</span><span class="sxs-lookup"><span data-stu-id="4f75c-132">3.x+</span></span> | <span data-ttu-id="4f75c-133">Usado somente por padrão com os projetos UWP, mas projetos podem ser convertidos de `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="4f75c-133">Used only by default with UWP projects, but projects can be converted from `packages.config`.</span></span> <span data-ttu-id="4f75c-134">`project.json` lista somente as dependências de nível superior.</span><span class="sxs-lookup"><span data-stu-id="4f75c-134">`project.json` lists only top-level dependencies.</span></span> <span data-ttu-id="4f75c-135">Referências, Destinos e Objetos são adicionados dinamicamente ao projeto durante o build, resultando em um melhor desempenho em comparação com `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="4f75c-135">References, Targets, and Props are added dynamically to the project during build, resulting in better performance compared with `packages.config`.</span></span> <span data-ttu-id="4f75c-136">(Consulte [Esquema project.json](../schema/project-json.md).)</span><span class="sxs-lookup"><span data-stu-id="4f75c-136">(See [project.json schema](../schema/project-json.md).)</span></span>|
| <span data-ttu-id="4f75c-137">PackageReference</span><span class="sxs-lookup"><span data-stu-id="4f75c-137">PackageReference</span></span> | <span data-ttu-id="4f75c-138">4.x ou superior</span><span class="sxs-lookup"><span data-stu-id="4f75c-138">4.x+</span></span> | <span data-ttu-id="4f75c-139">Lista as dependências diretamente no arquivo de projeto no nó `<PackageReference>`, junto com `<Reference>` e `<ProjectReference>`.</span><span class="sxs-lookup"><span data-stu-id="4f75c-139">Lists dependencies directly in the project file in the `<PackageReference>` node, alongside `<Reference>` and `<ProjectReference>`.</span></span> <span data-ttu-id="4f75c-140">Funciona de forma semelhante com o `project.json`; consulte [Referências de pacote em arquivos de projeto](../Consume-Packages/Package-References-in-Project-Files.md).</span><span class="sxs-lookup"><span data-stu-id="4f75c-140">Works similarly to `project.json`; see [Package references in project files](../Consume-Packages/Package-References-in-Project-Files.md).</span></span> |

<span data-ttu-id="4f75c-141">Em segundo, você iniciará uma restauração usando a lista de referência de várias maneiras:</span><span class="sxs-lookup"><span data-stu-id="4f75c-141">Second, you start a restore using the reference list in a variety of ways:</span></span>

<span data-ttu-id="4f75c-142">Na linha de comando ou no [Console de Gerenciador de Pacotes](../tools/Package-Manager-Console.md):</span><span class="sxs-lookup"><span data-stu-id="4f75c-142">From the command line or [Package Manager Console](../tools/Package-Manager-Console.md):</span></span>

| <span data-ttu-id="4f75c-143">Comando</span><span class="sxs-lookup"><span data-stu-id="4f75c-143">Command</span></span> | <span data-ttu-id="4f75c-144">Cenários aplicáveis</span><span class="sxs-lookup"><span data-stu-id="4f75c-144">Applicable scenarios</span></span> |
| --- | --- | 
| `nuget restore` | <span data-ttu-id="4f75c-145">Todas as versões do NuGet e todos os tipos de referência.</span><span class="sxs-lookup"><span data-stu-id="4f75c-145">All versions of NuGet and all reference types.</span></span> <span data-ttu-id="4f75c-146">Consulte [Restauração da linha de comando](#command-line-restore) abaixo.</span><span class="sxs-lookup"><span data-stu-id="4f75c-146">See [Command-line restore](#command-line-restore) below.</span></span> | 
| `dotnet restore` | <span data-ttu-id="4f75c-147">O mesmo que `nuget restore` para projetos .NET Core.</span><span class="sxs-lookup"><span data-stu-id="4f75c-147">Same as `nuget restore` for .NET Core projects.</span></span> <span data-ttu-id="4f75c-148">Consulte [dotnet restore](/dotnet/articles/core/tools/dotnet-restore).</span><span class="sxs-lookup"><span data-stu-id="4f75c-148">See [dotnet restore](/dotnet/articles/core/tools/dotnet-restore).</span></span> |
| `msbuild /t:restore` | <span data-ttu-id="4f75c-149">Nuget 4.x e superior e MSBuild 15.1 e superior somente com [referências de pacote em arquivos de projeto](../Consume-Packages/Package-References-in-Project-Files.md).</span><span class="sxs-lookup"><span data-stu-id="4f75c-149">Nuget 4.x+ and MSBuild 15.1+ with [package references in project files](../Consume-Packages/Package-References-in-Project-Files.md) only.</span></span> <span data-ttu-id="4f75c-150">`nuget restore` e `dotnet restore` usam esse comando para projetos aplicável.</span><span class="sxs-lookup"><span data-stu-id="4f75c-150">`nuget restore` and `dotnet restore` both use this command for applicable projects.</span></span> <span data-ttu-id="4f75c-151">Consulte [Empacotamento e restauração do NuGet como destinos do MSBuild- restore target](../schema/msbuild-targets.md#restore-target).</span><span class="sxs-lookup"><span data-stu-id="4f75c-151">See [NuGet pack and restore as MSBuild targets- restore target](../schema/msbuild-targets.md#restore-target).</span></span>|

<span data-ttu-id="4f75c-152">O próprio Visual Studio também restaura pacotes em momentos diferentes:</span><span class="sxs-lookup"><span data-stu-id="4f75c-152">Visual Studio itself also restores packages at different times:</span></span>

| <span data-ttu-id="4f75c-153">Tipo</span><span class="sxs-lookup"><span data-stu-id="4f75c-153">Type</span></span> | <span data-ttu-id="4f75c-154">Quando ocorre a restauração</span><span class="sxs-lookup"><span data-stu-id="4f75c-154">When restore happens</span></span> |
| --- | --- |
| <span data-ttu-id="4f75c-155">Restauração de modelo</span><span class="sxs-lookup"><span data-stu-id="4f75c-155">Template restore</span></span> | <span data-ttu-id="4f75c-156">Durante a criação de um novo projeto, visto que alguns modelos dependem de pacotes externos.</span><span class="sxs-lookup"><span data-stu-id="4f75c-156">During creation of a new project, as some templates depend on external packages.</span></span> |
| <span data-ttu-id="4f75c-157">Restauração de build</span><span class="sxs-lookup"><span data-stu-id="4f75c-157">Build restore</span></span> | <span data-ttu-id="4f75c-158">Como a primeira etapa de um build.</span><span class="sxs-lookup"><span data-stu-id="4f75c-158">As the first step of a build.</span></span> |
| <span data-ttu-id="4f75c-159">Restauração de solução</span><span class="sxs-lookup"><span data-stu-id="4f75c-159">Solution restore</span></span> | <span data-ttu-id="4f75c-160">Quando o usuário clica com o botão direito do mouse em uma solução e seleciona **Restaurar pacotes do NuGet**.</span><span class="sxs-lookup"><span data-stu-id="4f75c-160">When user right-clicks a solution and selects **Restore NuGet Packages**.</span></span> |
| <span data-ttu-id="4f75c-161">Restaurar na alteração do projeto</span><span class="sxs-lookup"><span data-stu-id="4f75c-161">Restore on project change</span></span> | <span data-ttu-id="4f75c-162">*(Somente NuGet 4.x)* Quando um projeto baseado no SDK do .NET Core é usado, incluindo quando as alterações de estado do projeto.</span><span class="sxs-lookup"><span data-stu-id="4f75c-162">*(NuGet 4.x only)* When a .NET Core SDK-based project is used, including when project state changes.</span></span> |

## <a name="enabling-and-disabling-package-restore"></a><span data-ttu-id="4f75c-163">Habilitar e desabilitar a restauração do pacote</span><span class="sxs-lookup"><span data-stu-id="4f75c-163">Enabling and disabling package restore</span></span>

<span data-ttu-id="4f75c-164">A restauração do pacote é habilitada primariamente por meio de **Ferramentas > Opções > Gerenciador de Pacotes do NuGet** no Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="4f75c-164">Package restore is primarily enabled through **Tools > Options > NuGet Package Manager** in Visual Studio:</span></span>

![Controlar comportamentos de restauração do pacote por meio de opções do Gerenciador de Pacotes do NuGet](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="4f75c-166">**Permitir que o NuGet baixe pacotes ausentes**: controla todas as formas de restauração de pacotes alterando a configuração `packageRestore/enabled` no arquivo `%AppData%\NuGet\NuGet.Config` conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="4f75c-166">**Allow NuGet to download missing packages**: controls all forms of package restore by changing the `packageRestore/enabled` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    <br/>
    > [!Note]
    >  <span data-ttu-id="4f75c-167">A configuração `packageRestore/enabled` pode ser substituída globalmente definindo uma variável de ambiente chamada **EnableNuGetPackageRestore** com um valor de TRUE ou FALSE antes de abrir o Visual Studio ou iniciar um build.</span><span class="sxs-lookup"><span data-stu-id="4f75c-167">The `packageRestore/enabled` setting can be overridden globally by setting an environment variable called **EnableNuGetPackageRestore** with a value of TRUE or FALSE before launching Visual Studio or starting a build.</span></span>
    

- <span data-ttu-id="4f75c-168">**Verificar automaticamente os pacotes ausentes durante o build no Visual Studio**: controla a restauração automática para NuGet 2.7 e posterior, alterando a configuração `packageRestore/automatic` no arquivo `%AppData%\NuGet\NuGet.Config` conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="4f75c-168">**Automatically check for missing packages during build in Visual Studio**: controls automatic restore for NuGet 2.7 and later by changing the `packageRestore/automatic` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>
            
    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

<span data-ttu-id="4f75c-169">Para referência, consulte o [Arquivo de configuração do NuGet – Seção packageRestore](../Schema/nuget-config-file.md#packagerestore-section).</span><span class="sxs-lookup"><span data-stu-id="4f75c-169">For reference, see the [NuGet config file - packageRestore section](../Schema/nuget-config-file.md#packagerestore-section).</span></span>

<span data-ttu-id="4f75c-170">Em alguns casos, um desenvolvedor ou empresa podem optar por habilitar ou desabilitar a restauração de pacotes em um computador por padrão para todos os usuários.</span><span class="sxs-lookup"><span data-stu-id="4f75c-170">In some cases, a developer or company might want to enable or disable package restore on a machine by default for all users.</span></span> <span data-ttu-id="4f75c-171">Isso pode ser feito adicionando as mesmas configurações acima ao arquivo de configuração global do NuGet localizado em `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span><span class="sxs-lookup"><span data-stu-id="4f75c-171">This can be done by adding the same settings above to the global NuGet configuration file located in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span></span> <span data-ttu-id="4f75c-172">Usuários individuais poderão, então, habilitar seletivamente a restauração conforme necessário no nível do projeto.</span><span class="sxs-lookup"><span data-stu-id="4f75c-172">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="4f75c-173">Consulte [Configurando o comportamento do NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) para ver os detalhes sobre como o NuGet prioriza vários arquivos de configuração.</span><span class="sxs-lookup"><span data-stu-id="4f75c-173">See [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) for exact details on how NuGet prioritizes multiple config files.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="4f75c-174">Restrições de versões de pacote com restauração</span><span class="sxs-lookup"><span data-stu-id="4f75c-174">Constraining package versions with restore</span></span>

<span data-ttu-id="4f75c-175">Quando o NuGet restaura pacotes por meio de qualquer método, ele aceitará quaisquer restrições especificadas no `packages.config`, `project.json` ou no arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="4f75c-175">When NuGet restores packages through any method, it will honor any constraints specified in `packages.config`, `project.json`, or the project file:</span></span>

- <span data-ttu-id="4f75c-176">`packages.config`: especifique um intervalo de versão na propriedade `allowedVersion` da dependência.</span><span class="sxs-lookup"><span data-stu-id="4f75c-176">`packages.config`: Specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="4f75c-177">Consulte [Reinstalando e atualizando pacotes](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="4f75c-177">See [Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="4f75c-178">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="4f75c-178">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="4f75c-179">`project.json`: especifique um intervalo de versão diretamente com o número de versão da dependência.</span><span class="sxs-lookup"><span data-stu-id="4f75c-179">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="4f75c-180">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="4f75c-180">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

- <span data-ttu-id="4f75c-181">Referências de pacote nos arquivos de projeto: especifique um intervalo de versão diretamente com o número de versão da dependência.</span><span class="sxs-lookup"><span data-stu-id="4f75c-181">Package references in project files: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="4f75c-182">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="4f75c-182">For example:</span></span>
 
    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />  
    ```

<span data-ttu-id="4f75c-183">Em todo os casos, use a notação descrita em [Controle de versão do pacote](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="4f75c-183">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="command-line-restore"></a><span data-ttu-id="4f75c-184">Restauração da linha de comando</span><span class="sxs-lookup"><span data-stu-id="4f75c-184">Command-line restore</span></span>

<span data-ttu-id="4f75c-185">Para NuGet 2.7 e posterior, use o [restaurar](../tools/cli-ref-restore.md) comando para restaurar todos os pacotes em uma solução (independente de se ele usa `packages.config`, `project.json` ou as referências de pacote em arquivos de projeto).</span><span class="sxs-lookup"><span data-stu-id="4f75c-185">For NuGet 2.7 and above, use the [Restore](../tools/cli-ref-restore.md) command to restore all packages in a solution (whether it uses `packages.config`, `project.json`, or package references in project files).</span></span> <span data-ttu-id="4f75c-186">Para determinada pasta de projeto como `c:\proj\app`, as variações comuns abaixo restauram os pacotes:</span><span class="sxs-lookup"><span data-stu-id="4f75c-186">For a given project folder such as `c:\proj\app`, the common variations below each restore the packages:</span></span>

```
c:\proj\app\> nuget restore
c:\proj\app\> nuget.exe restore app.sln
c:\proj\> nuget restore app
```

<span data-ttu-id="4f75c-187">Para NuGet 4.0 ou superior e MSBuild 15.1 ou superior, também é possível usar `MSBuild /t:restore` conforme descrito em [Empacotamento e restauração do NuGet como destinos do MSBuild](../schema/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="4f75c-187">For NuGet 4.0+ and MSBuild 15.1+, you can also use `MSBuild /t:restore` as described on [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="build-time-restore-in-visual-studio"></a><span data-ttu-id="4f75c-188">Restauração de tempo de build no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4f75c-188">Build-time restore in Visual Studio</span></span>

<span data-ttu-id="4f75c-189">O Visual Studio restaura automaticamente os pacotes ausentes por padrão no início de um build.</span><span class="sxs-lookup"><span data-stu-id="4f75c-189">Visual Studio automatically restores missing packages by default at the beginning of a build.</span></span> <span data-ttu-id="4f75c-190">Esse comportamento pode ser alterado desmarcando **Ferramentas > Opções > Gerenciador do Pacote do NuGet > Geral > Verificar automaticamente os pacotes ausentes durante o build no Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="4f75c-190">This behavior can be changed by clearing **Tools > Options > NuGet Package Manager > General > Automatically check for missing packages during build in Visual Studio**.</span></span>

<span data-ttu-id="4f75c-191">Quando habilitada, a restauração automática funciona da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="4f75c-191">When enabled, automatic restore works as follows:</span></span>

1. <span data-ttu-id="4f75c-192">Quando um build é iniciado, o Visual Studio instrui o NuGet a restaurar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="4f75c-192">When a build begins, Visual Studio instructs NuGet to restore packages.</span></span>
1. <span data-ttu-id="4f75c-193">O NuGet busca recursivamente todos os arquivos `packages.config` na solução, busca por `project.json` ou procura no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="4f75c-193">NuGet recursively looks for all `packages.config` files in the solution, looks for `project.json`, or looks in the project file.</span></span>
1. <span data-ttu-id="4f75c-194">Para cada pacote listados nos arquivos de referência, o NuGet verifica se ele já existe na solução (o pasta `packages`, `project.lock.json` ou `project.assets.json`, dependendo se o projeto está usando `packages.config`, `project.json` ou referências de pacote nos arquivos do projeto).</span><span class="sxs-lookup"><span data-stu-id="4f75c-194">For each packages listed in the reference files, NuGet checks if it already exists in the solution (the `packages` folder, `project.lock.json`, or `project.assets.json` depending on whether the project is using `packages.config`, `project.json`, or package references in project files).</span></span>
1. <span data-ttu-id="4f75c-195">Se o pacote não for encontrado, o NuGet tentará recuperá-lo do seu cache primeiro (consulte [Gerenciamento do cache do NuGet](../consume-packages/managing-the-nuget-cache.md).</span><span class="sxs-lookup"><span data-stu-id="4f75c-195">If the package is not found, NuGet attempts to retrieve the package from its cache first (see [Managing the NuGet cache](../consume-packages/managing-the-nuget-cache.md).</span></span> <span data-ttu-id="4f75c-196">Se o pacote não estiver no cache, o NuGet tentará baixá-lo das origens habilitadas, conforme listado em **Ferramentas > Opções > Gerenciador de Pacotes do NuGet > Origens de Pacote**, na ordem em que elas aparecem.</span><span class="sxs-lookup"><span data-stu-id="4f75c-196">If the package is not in the cache, NuGet attempts to download the package from the enabled sources as listed in **Tools > Options > NuGet Package Manager > Package Sources**, in the order that the sources appear.</span></span> <span data-ttu-id="4f75c-197">Nesse caso, o NuGet não indica uma falha ao localizar o pacote até que todas as origens tenham sido verificadas, quando então ele relata a falha somente para a última origem na lista.</span><span class="sxs-lookup"><span data-stu-id="4f75c-197">In this case, NuGet does not indicate a failure to find the package until all the sources have been checked, at which time it reports the failure only for the last source in the list.</span></span> <span data-ttu-id="4f75c-198">Implicitamente, esse erro também significa que o pacote não estava presente em nenhuma das outras fontes, mesmo que os erros não tenham sido mostrados para as fontes individualmente.</span><span class="sxs-lookup"><span data-stu-id="4f75c-198">By implication such an error also means that the package wasn't present on any of the other sources either, even though errors were not shown for those sources individually.</span></span>
1. <span data-ttu-id="4f75c-199">Se o download for bem-sucedido, o NuGet armazena o pacote em cache e o instala na solução (novamente, na pasta `packages`, `project.lock.json` ou `project.assets.json`); caso contrário o NuGet falhará e o build falhará.</span><span class="sxs-lookup"><span data-stu-id="4f75c-199">If the download is successful, NuGet caches the package and installs it into the solution (again, into either the `packages` folder, `project.lock.json`, or `project.assets.json`); otherwise NuGet fails and the build fails.</span></span>

<span data-ttu-id="4f75c-200">Durante esse processo, você verá uma caixa de diálogo de andamento com a opção para cancelar a restauração do pacote.</span><span class="sxs-lookup"><span data-stu-id="4f75c-200">During this process, you see a progress dialog with the option to cancel package restore.</span></span>

## <a name="package-restore-with-team-foundation-build"></a><span data-ttu-id="4f75c-201">Restauração de Pacote com o Team Foundation Build</span><span class="sxs-lookup"><span data-stu-id="4f75c-201">Package Restore with Team Foundation Build</span></span>

<span data-ttu-id="4f75c-202">A restauração do pacote normalmente é usada ao criar projetos em servidores de build, assim como acontece com o TFS (Team Foundation Server) e o Visual Studio Team Services (bem como outros sistemas de build, que não são abordados aqui).</span><span class="sxs-lookup"><span data-stu-id="4f75c-202">Package restore is commonly used when building projects on build servers, as with Team Foundation Server (TFS) and Visual Studio Team Services (as well as other build systems, which are not covered here).</span></span>

### <a name="visual-studio-team-services"></a><span data-ttu-id="4f75c-203">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="4f75c-203">Visual Studio Team Services</span></span>

<span data-ttu-id="4f75c-204">Ao criar uma definição de build do Team Services, basta incluir a tarefa Restaurar pacotes do NuGet na definição do antes de qualquer tarefa de build.</span><span class="sxs-lookup"><span data-stu-id="4f75c-204">When creating a build definition on Team Services, simply include the Restore NuGet Packages task in the definition before any build task.</span></span> <span data-ttu-id="4f75c-205">Essa tarefa é incluída por padrão em diversos modelos de build.</span><span class="sxs-lookup"><span data-stu-id="4f75c-205">This task is included by default in a number of build templates.</span></span>

![Tarefa de restauração de pacote do NuGet em uma definição de build do Visual Studio Team Service](media/Restore-02-VSTSBuild.png)

### <a name="team-foundation-server"></a><span data-ttu-id="4f75c-207">Team Foundation Server</span><span class="sxs-lookup"><span data-stu-id="4f75c-207">Team Foundation Server</span></span>

<span data-ttu-id="4f75c-208">Com o TFS 2013 e posterior, os pacotes são automaticamente restaurados por padrão durante o build, desde que você esteja usando um modelo do Team Build para Team Foundation Server 2013 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="4f75c-208">With TFS 2013 and later, packages are automatically restored by default during build, provided that you're using a Team Build Template for Team Foundation Server 2013 or later.</span></span>

<span data-ttu-id="4f75c-209">Se estiver usando uma versão anterior dos modelos de build (como em um projeto que foi migrado de versões anteriores do TFS), você também precisará migrar esses modelos de build para o TFS 2013.</span><span class="sxs-lookup"><span data-stu-id="4f75c-209">If you're using a previous version of build templates (such as in a project that's been migrated from earlier versions of TFS), you'll need to also migrate those build templates to TFS 2013.</span></span> <span data-ttu-id="4f75c-210">Isso significa basicamente recriar as partes personalizadas dos Modelos de build usando o modelo apropriado para o controle do código-fonte (TFVC ou Git).</span><span class="sxs-lookup"><span data-stu-id="4f75c-210">This essentially means recreating the custom parts of the Build Templates using the appropriate template for your source control (TFVC or Git).</span></span>

<span data-ttu-id="4f75c-211">Para obter uma versão anterior do TFS, você pode simplesmente incluir uma etapa de build para invocar [restauração de linha de comando](#command-line-restore) conforme descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4f75c-211">For earlier version of TFS, you can simply include a build step to invoke [command-line restore](#command-line-restore) as described earlier.</span></span>

<span data-ttu-id="4f75c-212">Para obter mais detalhes, consulte [Explicação passo a passo da restauração de pacotes com o Team Foundation Build](../consume-packages/team-foundation-build.md).</span><span class="sxs-lookup"><span data-stu-id="4f75c-212">For more details see then [Walkthrough of Package Restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>    
