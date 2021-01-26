---
title: Solucionando problemas de restauração de pacote do NuGet no Visual Studio
description: Uma descrição de erros de restauração de NuGet comuns no Visual Studio e como solucioná-los.
author: JonDouglas
ms.author: jodou
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: f1c7c4ce2872e18b1ed35ccbf3355a6192ab4a9c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775024"
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="f13e0-103">Solução de problemas de erros de restauração de pacote</span><span class="sxs-lookup"><span data-stu-id="f13e0-103">Troubleshooting package restore errors</span></span>

<span data-ttu-id="f13e0-104">Este artigo aborda os erros comuns ao restaurar pacotes e as etapas para resolvê-los.</span><span class="sxs-lookup"><span data-stu-id="f13e0-104">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> 

<span data-ttu-id="f13e0-105">A Restauração de Pacote tenta instalar todas as dependências de pacotes no estado correto correspondente às referências de pacote do arquivo de projeto (*.csproj*) ou do arquivo *packages.config*.</span><span class="sxs-lookup"><span data-stu-id="f13e0-105">Package Restore tries to install all package dependencies to the correct state matching the package references in your project file (*.csproj*) or your *packages.config* file.</span></span> <span data-ttu-id="f13e0-106">(No Visual Studio, as referências aparecem em Gerenciador de Soluções sob as **dependências \ NuGet** ou o nó **References** .) Para seguir as etapas necessárias para restaurar pacotes, consulte [restaurar pacotes](../consume-packages/package-restore.md#restore-packages).</span><span class="sxs-lookup"><span data-stu-id="f13e0-106">(In Visual Studio, the references appear in Solution Explorer under the **Dependencies \ NuGet** or the **References** node.) To follow the required steps to restore packages, see [Restore packages](../consume-packages/package-restore.md#restore-packages).</span></span> <span data-ttu-id="f13e0-107">Se as referências de pacote no arquivo de projeto (*.csproj*) ou no arquivo *packages.config* estiverem incorretas (não corresponderem ao estado desejado após a Restauração de Pacote), instale ou atualize os pacotes em vez de usar a Restauração de Pacote.</span><span class="sxs-lookup"><span data-stu-id="f13e0-107">If the package references in your project file (*.csproj*) or your *packages.config* file are incorrect (they do not match your desired state following Package Restore), then you need to either install or update packages instead of using Package Restore.</span></span>

<span data-ttu-id="f13e0-108">Se estas instruções não funcionarem para você, [envie um problema no GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para examinarmos o cenário mais cuidadosamente.</span><span class="sxs-lookup"><span data-stu-id="f13e0-108">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="f13e0-109">Não use o controle “Esta página é útil?”</span><span class="sxs-lookup"><span data-stu-id="f13e0-109">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="f13e0-110">que pode aparecer nesta página, pois ele não nos permite entrar em contato com você para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="f13e0-110">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="f13e0-111">Solução rápida para usuários do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f13e0-111">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="f13e0-112">Se você estiver usando o Visual Studio, primeiro habilite a restauração de pacote da maneira descrita a seguir.</span><span class="sxs-lookup"><span data-stu-id="f13e0-112">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="f13e0-113">Caso contrário, prossiga para as seções seguintes.</span><span class="sxs-lookup"><span data-stu-id="f13e0-113">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="f13e0-114">Selecione o comando de menu **Ferramentas > Gerenciador de Pacotes do NuGet > Configurações do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="f13e0-114">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="f13e0-115">Marque as duas opções em **Restauração de Pacote**.</span><span class="sxs-lookup"><span data-stu-id="f13e0-115">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="f13e0-116">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="f13e0-116">Select **OK**.</span></span>
1. <span data-ttu-id="f13e0-117">Compile o projeto novamente.</span><span class="sxs-lookup"><span data-stu-id="f13e0-117">Build your project again.</span></span>

![Habilitar a restauração de pacote do NuGet em Ferramenta/Opções](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="f13e0-119">Essas configurações também podem ser alteradas no arquivo `NuGet.config`; veja a seção de [consentimento](#consent).</span><span class="sxs-lookup"><span data-stu-id="f13e0-119">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span> <span data-ttu-id="f13e0-120">Se seu projeto for um projeto mais antigo que usa a restauração de pacote integrada ao MSBuild, talvez seja [necessário](package-restore.md#migrate-to-automatic-package-restore-visual-studio) migrar para a restauração automática de pacote.</span><span class="sxs-lookup"><span data-stu-id="f13e0-120">If your project is an older project that uses the MSBuild-integrated package restore, you may need to [migrate](package-restore.md#migrate-to-automatic-package-restore-visual-studio) to automatic package restore.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="f13e0-121">Este projeto faz referência a pacotes NuGet ausentes neste computador</span><span class="sxs-lookup"><span data-stu-id="f13e0-121">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="f13e0-122">Mensagem de erro completa:</span><span class="sxs-lookup"><span data-stu-id="f13e0-122">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="f13e0-123">Esse erro ocorre ao tentar compilar um projeto com referências a um ou mais pacotes do NuGet, mas, no momento, esses pacotes não estão instalados no computador ou no projeto.</span><span class="sxs-lookup"><span data-stu-id="f13e0-123">This error occurs when you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="f13e0-124">Ao usar o formato de gerenciamento [PackageReference](package-references-in-project-files.md) , esse erro pode ser um sobra de um packages.config para a migração do PackageReference e precisa ser [removido manualmente](../resources/NuGet-FAQ.md#working-with-packages) do arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="f13e0-124">When using the [PackageReference](package-references-in-project-files.md) management format, this error might be a leftover from a packages.config to PackageReference migration and needs to be [manually removed](../resources/NuGet-FAQ.md#working-with-packages) from the project file.</span></span>
- <span data-ttu-id="f13e0-125">Ao usar o [packages.config](../reference/packages-config.md), o erro significa que o pacote não está instalado na pasta `packages` na raiz da solução.</span><span class="sxs-lookup"><span data-stu-id="f13e0-125">When using [packages.config](../reference/packages-config.md), the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="f13e0-126">Essa situação geralmente ocorre ao obter o código-fonte do projeto por meio do controle do código-fonte ou de outro download.</span><span class="sxs-lookup"><span data-stu-id="f13e0-126">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="f13e0-127">Os pacotes normalmente são omitidos do controle do código-fonte ou dos downloads, uma vez que podem ser restaurados de feeds de pacotes, como o nuget.org (veja [Pacotes e controle do código-fonte](Packages-and-Source-Control.md)).</span><span class="sxs-lookup"><span data-stu-id="f13e0-127">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="f13e0-128">Por outro lado, a inclusão deles sobrecarregaria o repositório ou criaria arquivos .zip desnecessariamente grandes.</span><span class="sxs-lookup"><span data-stu-id="f13e0-128">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="f13e0-129">O erro também poderá ocorrer se o arquivo de projeto contiver caminhos absolutos para locais de pacote e você mover o projeto.</span><span class="sxs-lookup"><span data-stu-id="f13e0-129">The error can also happen if your project file contains absolute paths to package locations, and you move the project.</span></span>

<span data-ttu-id="f13e0-130">Use um dos seguintes métodos para restaurar os pacotes:</span><span class="sxs-lookup"><span data-stu-id="f13e0-130">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="f13e0-131">Se você moveu o arquivo de projeto, edite o arquivo diretamente para atualizar as referências do pacote.</span><span class="sxs-lookup"><span data-stu-id="f13e0-131">If you've moved the project file, edit the file directly to update the package references.</span></span>
- <span data-ttu-id="f13e0-132">[Visual Studio](package-restore.md#restore-using-visual-studio) ([restauração automática](package-restore.md#restore-packages-automatically-using-visual-studio) ou [restauração manual](package-restore.md#restore-packages-manually-using-visual-studio))</span><span class="sxs-lookup"><span data-stu-id="f13e0-132">[Visual Studio](package-restore.md#restore-using-visual-studio) ([automatic restore](package-restore.md#restore-packages-automatically-using-visual-studio) or [manual restore](package-restore.md#restore-packages-manually-using-visual-studio))</span></span>
- [<span data-ttu-id="f13e0-133">CLI do dotnet</span><span class="sxs-lookup"><span data-stu-id="f13e0-133">dotnet CLI</span></span>](package-restore.md#restore-using-the-dotnet-cli)
- [<span data-ttu-id="f13e0-134">CLI do nuget.exe</span><span class="sxs-lookup"><span data-stu-id="f13e0-134">nuget.exe CLI</span></span>](package-restore.md#restore-using-the-nugetexe-cli)
- [<span data-ttu-id="f13e0-135">MSBuild</span><span class="sxs-lookup"><span data-stu-id="f13e0-135">MSBuild</span></span>](package-restore.md#restore-using-msbuild)
- [<span data-ttu-id="f13e0-136">Azure Pipelines</span><span class="sxs-lookup"><span data-stu-id="f13e0-136">Azure Pipelines</span></span>](package-restore.md#restore-using-azure-pipelines)
- [<span data-ttu-id="f13e0-137">Azure DevOps Server</span><span class="sxs-lookup"><span data-stu-id="f13e0-137">Azure DevOps Server</span></span>](package-restore.md#restore-using-azure-devops-server)

<span data-ttu-id="f13e0-138">Após uma restauração bem-sucedida, o pacote deve estar presente na pasta *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="f13e0-138">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="f13e0-139">Em caso de projetos que usam PackageReference, uma restauração deve recriar o arquivo `obj/project.assets.json`; em projetos que usam `packages.config`, o pacote deve aparecer na pasta `packages` do projeto.</span><span class="sxs-lookup"><span data-stu-id="f13e0-139">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="f13e0-140">Nesse momento, o projeto deverá ser compilado com êxito.</span><span class="sxs-lookup"><span data-stu-id="f13e0-140">The project should now build successfully.</span></span> <span data-ttu-id="f13e0-141">Caso contrário, [envie um problema no GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para que possamos acompanhá-lo com você.</span><span class="sxs-lookup"><span data-stu-id="f13e0-141">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="f13e0-142">Arquivo de ativos project.assets.json não encontrado</span><span class="sxs-lookup"><span data-stu-id="f13e0-142">Assets file project.assets.json not found</span></span>

<span data-ttu-id="f13e0-143">Mensagem de erro completa:</span><span class="sxs-lookup"><span data-stu-id="f13e0-143">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="f13e0-144">O arquivo `project.assets.json` mantém um grafo de dependência do projeto quando ocorre o uso do formato de gerenciamento PackageReference, que é usado para garantir que todos os pacotes necessários sejam instalados no computador.</span><span class="sxs-lookup"><span data-stu-id="f13e0-144">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="f13e0-145">Como esse arquivo é gerado de modo dinâmico por meio da restauração do pacote, ele geralmente não é adicionado ao controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="f13e0-145">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="f13e0-146">Como resultado, esse erro ocorre ao compilar um projeto com uma ferramenta como o `msbuild`, que não restaura os pacotes automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f13e0-146">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="f13e0-147">Nesse caso, execute `msbuild -t:restore` seguido por `msbuild` ou use `dotnet build` (que restaura automaticamente os pacotes).</span><span class="sxs-lookup"><span data-stu-id="f13e0-147">In this case, run `msbuild -t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="f13e0-148">Também é possível usar algum dos métodos de restauração de pacote descritos na [seção anterior](#missing).</span><span class="sxs-lookup"><span data-stu-id="f13e0-148">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="f13e0-149">Um ou mais pacotes NuGet precisam ser restaurados, mas não foi possível porque o consentimento não foi concedido</span><span class="sxs-lookup"><span data-stu-id="f13e0-149">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="f13e0-150">Mensagem de erro completa:</span><span class="sxs-lookup"><span data-stu-id="f13e0-150">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="f13e0-151">Esse erro indica que a restauração de pacote está desabilitada na configuração do NuGet.</span><span class="sxs-lookup"><span data-stu-id="f13e0-151">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="f13e0-152">Você pode alterar as configurações aplicáveis no Visual Studio, conforme descrito anteriormente em [Solução rápida para usuários do Visual Studio](#quick-solution-for-visual-studio-users).</span><span class="sxs-lookup"><span data-stu-id="f13e0-152">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="f13e0-153">Você também pode editar essas configurações diretamente no arquivo `nuget.config` aplicável (normalmente `%AppData%\NuGet\NuGet.Config` no Windows e `~/.nuget/NuGet/NuGet.Config` no Linux/Mac).</span><span class="sxs-lookup"><span data-stu-id="f13e0-153">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="f13e0-154">Verifique se as chaves `enabled` e `automatic` em `packageRestore` estão definidas como True:</span><span class="sxs-lookup"><span data-stu-id="f13e0-154">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

> [!Important]
> <span data-ttu-id="f13e0-155">Se você editar as configurações de `packageRestore` diretamente em `nuget.config`, reinicie o Visual Studio para que a caixa de diálogo de opções mostre os valores atuais.</span><span class="sxs-lookup"><span data-stu-id="f13e0-155">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="f13e0-156">Outras condições possíveis</span><span class="sxs-lookup"><span data-stu-id="f13e0-156">Other potential conditions</span></span>

- <span data-ttu-id="f13e0-157">Você pode encontrar erros de build devido a arquivos ausentes, com uma mensagem indicando para usar a restauração do NuGet para baixá-los.</span><span class="sxs-lookup"><span data-stu-id="f13e0-157">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="f13e0-158">No entanto, ao executar uma restauração, a seguinte mensagem poderá aparecer: "Todos os pacotes já estão instalados e não há nada para ser restaurado".</span><span class="sxs-lookup"><span data-stu-id="f13e0-158">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="f13e0-159">Nesse caso, exclua a pasta `packages` (ao usar `packages.config`) ou o arquivo `obj/project.assets.json` (ao usar PackageReference) e execute a restauração novamente.</span><span class="sxs-lookup"><span data-stu-id="f13e0-159">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="f13e0-160">Se o erro continuar, use `nuget locals all -clear` ou `dotnet nuget locals all --clear` pela linha de comando para limpar as pastas *global-packages* e de cache, conforme descrito em [Como gerenciar as pastas de pacotes globais e de cache](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="f13e0-160">If the error still persists, use `nuget locals all -clear` or `dotnet nuget locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="f13e0-161">Ao obter um projeto por meio do controle do código-fonte, as pastas do projeto poderão ser definidas como somente leitura.</span><span class="sxs-lookup"><span data-stu-id="f13e0-161">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="f13e0-162">Altere as permissões de pasta e tente restaurar os pacotes novamente.</span><span class="sxs-lookup"><span data-stu-id="f13e0-162">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="f13e0-163">Talvez você esteja usando uma versão antiga do NuGet.</span><span class="sxs-lookup"><span data-stu-id="f13e0-163">You may be using an old version of NuGet.</span></span> <span data-ttu-id="f13e0-164">Acesse [nuget.org/downloads](https://www.nuget.org/downloads) para obter as versões mais recentes recomendadas.</span><span class="sxs-lookup"><span data-stu-id="f13e0-164">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="f13e0-165">Para o Visual Studio 2015, recomendamos a versão 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="f13e0-165">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="f13e0-166">Se você encontrar outros problemas, [envie um problema no GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para que possamos obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="f13e0-166">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>
