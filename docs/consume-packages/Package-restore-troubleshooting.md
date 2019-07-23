---
title: Solucionando problemas de restauração de pacote do NuGet no Visual Studio
description: Uma descrição de erros de restauração de NuGet comuns no Visual Studio e como solucioná-los.
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: 287237cf4041870c562a6a7f48f233d8fdc8ef33
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842379"
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="e078e-103">Solução de problemas de erros de restauração de pacote</span><span class="sxs-lookup"><span data-stu-id="e078e-103">Troubleshooting package restore errors</span></span>

<span data-ttu-id="e078e-104">Este artigo aborda os erros comuns ao restaurar pacotes e as etapas para resolvê-los.</span><span class="sxs-lookup"><span data-stu-id="e078e-104">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> <span data-ttu-id="e078e-105">Para obter detalhes completos sobre a restauração de pacotes, veja [Restauração de pacote](../consume-packages/package-restore.md#enable-and-disable-package-restore-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="e078e-105">For complete details on restoring packages, see [Package restore](../consume-packages/package-restore.md#enable-and-disable-package-restore-visual-studio).</span></span>

<span data-ttu-id="e078e-106">Se estas instruções não funcionarem para você, [envie um problema no GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para examinarmos o cenário mais cuidadosamente.</span><span class="sxs-lookup"><span data-stu-id="e078e-106">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="e078e-107">Não use o controle “Esta página é útil?”</span><span class="sxs-lookup"><span data-stu-id="e078e-107">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="e078e-108">que pode aparecer nesta página, pois ele não nos permite entrar em contato com você para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="e078e-108">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="e078e-109">Solução rápida para usuários do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e078e-109">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="e078e-110">Se você estiver usando o Visual Studio, primeiro habilite a restauração de pacote da maneira descrita a seguir.</span><span class="sxs-lookup"><span data-stu-id="e078e-110">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="e078e-111">Caso contrário, prossiga para as seções seguintes.</span><span class="sxs-lookup"><span data-stu-id="e078e-111">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="e078e-112">Selecione o comando de menu **Ferramentas > Gerenciador de Pacotes do NuGet > Configurações do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="e078e-112">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="e078e-113">Marque as duas opções em **Restauração de Pacote**.</span><span class="sxs-lookup"><span data-stu-id="e078e-113">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="e078e-114">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="e078e-114">Select **OK**.</span></span>
1. <span data-ttu-id="e078e-115">Compile o projeto novamente.</span><span class="sxs-lookup"><span data-stu-id="e078e-115">Build your project again.</span></span>

![Habilitar a restauração de pacote do NuGet em Ferramenta/Opções](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="e078e-117">Essas configurações também podem ser alteradas no arquivo `NuGet.config`; veja a seção de [consentimento](#consent).</span><span class="sxs-lookup"><span data-stu-id="e078e-117">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span> <span data-ttu-id="e078e-118">Se seu projeto for um projeto mais antigo que usa a restauração de pacote integrada ao MSBuild, talvez seja [necessário](package-restore.md#migrate-to-automatic-package-restore-visual-studio) migrar para a restauração automática de pacote.</span><span class="sxs-lookup"><span data-stu-id="e078e-118">If your project is an older project that uses the MSBuild-integrated package restore, you may need to [migrate](package-restore.md#migrate-to-automatic-package-restore-visual-studio) to automatic package restore.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="e078e-119">Este projeto faz referência a pacotes NuGet ausentes neste computador</span><span class="sxs-lookup"><span data-stu-id="e078e-119">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="e078e-120">Mensagem de erro completa:</span><span class="sxs-lookup"><span data-stu-id="e078e-120">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="e078e-121">Esse erro ocorre ao tentar compilar um projeto com referências a um ou mais pacotes do NuGet, mas, no momento, esses pacotes não estão instalados no computador ou no projeto.</span><span class="sxs-lookup"><span data-stu-id="e078e-121">This error occurs when you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="e078e-122">Quando o formato de gerenciamento PackageReference é usado, o erro significa que o pacote não está instalado na pasta *global-packages* conforme descrito em [Como gerenciar as pastas de pacotes globais e de cache](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="e078e-122">When using the PackageReference management format, the error means that the package is not installed in the *global-packages* folder as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>
- <span data-ttu-id="e078e-123">Quando `packages.config` é usado, o erro significa que o pacote não está instalado na pasta `packages` na raiz da solução.</span><span class="sxs-lookup"><span data-stu-id="e078e-123">When using `packages.config`, the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="e078e-124">Essa situação geralmente ocorre ao obter o código-fonte do projeto por meio do controle do código-fonte ou de outro download.</span><span class="sxs-lookup"><span data-stu-id="e078e-124">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="e078e-125">Os pacotes normalmente são omitidos do controle do código-fonte ou dos downloads, uma vez que podem ser restaurados de feeds de pacotes, como o nuget.org (veja [Pacotes e controle do código-fonte](Packages-and-Source-Control.md)).</span><span class="sxs-lookup"><span data-stu-id="e078e-125">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="e078e-126">Por outro lado, a inclusão deles sobrecarregaria o repositório ou criaria arquivos .zip desnecessariamente grandes.</span><span class="sxs-lookup"><span data-stu-id="e078e-126">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="e078e-127">O erro também poderá ocorrer se o arquivo de projeto contiver caminhos absolutos para locais de pacote e você mover o projeto.</span><span class="sxs-lookup"><span data-stu-id="e078e-127">The error can also happen if your project file contains absolute paths to package locations, and you move the project.</span></span>

<span data-ttu-id="e078e-128">Use um dos seguintes métodos para restaurar os pacotes:</span><span class="sxs-lookup"><span data-stu-id="e078e-128">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="e078e-129">Se você moveu o arquivo de projeto, edite o arquivo diretamente para atualizar as referências do pacote.</span><span class="sxs-lookup"><span data-stu-id="e078e-129">If you've moved the project file, edit the file directly to update the package references.</span></span>
- <span data-ttu-id="e078e-130">(Visual Studio) Habilite a restauração de pacote selecionando o comando de menu **Ferramentas > Gerenciador de Pacotes do NuGet > Configurações do Gerenciador de Pacotes** marcando ambas as opções em **Restauração de Pacote** e selecionando **OK**.</span><span class="sxs-lookup"><span data-stu-id="e078e-130">(Visual Studio) Enable package restore by selecting the **Tools > NuGet Package Manager > Package Manager Settings** menu command, setting both options under **Package Restore**, and selecting **OK**.</span></span> <span data-ttu-id="e078e-131">Em seguida, compile a solução novamente.</span><span class="sxs-lookup"><span data-stu-id="e078e-131">Then build the solution again.</span></span>
- <span data-ttu-id="e078e-132">(CLI do dotnet) Na linha de comando, alterne para a pasta que contém o projeto e execute `dotnet restore` ou `dotnet build` (que executa a restauração automaticamente).</span><span class="sxs-lookup"><span data-stu-id="e078e-132">(dotnet CLI) In the command line, switch to the folder that contains your project, and then run `dotnet restore` or `dotnet build` (which automatically runs restore).</span></span>
- <span data-ttu-id="e078e-133">(CLI do nuget.exe) Na linha de comando, alterne para a pasta que contém o projeto e execute `nuget restore` (exceto os projetos criados com a CLI do `dotnet`, nesse caso, use `dotnet restore`).</span><span class="sxs-lookup"><span data-stu-id="e078e-133">(nuget.exe CLI) In the command line, switch to the folder that contains your project, and then run `nuget restore` (except for projects created with `dotnet` CLI, in which case use `dotnet restore`).</span></span>
- <span data-ttu-id="e078e-134">(Projetos migrados para PackageReference) Na linha de comando, execute `msbuild -t:restore`.</span><span class="sxs-lookup"><span data-stu-id="e078e-134">(Projects migrated to PackageReference) On the command line, run `msbuild -t:restore`.</span></span>

<span data-ttu-id="e078e-135">Após uma restauração bem-sucedida, o pacote deve estar presente na pasta *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="e078e-135">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="e078e-136">Em caso de projetos que usam PackageReference, uma restauração deve recriar o arquivo `obj/project.assets.json`; em projetos que usam `packages.config`, o pacote deve aparecer na pasta `packages` do projeto.</span><span class="sxs-lookup"><span data-stu-id="e078e-136">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="e078e-137">Nesse momento, o projeto deverá ser compilado com êxito.</span><span class="sxs-lookup"><span data-stu-id="e078e-137">The project should now build successfully.</span></span> <span data-ttu-id="e078e-138">Caso contrário, [envie um problema no GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para que possamos acompanhá-lo com você.</span><span class="sxs-lookup"><span data-stu-id="e078e-138">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="e078e-139">Arquivo de ativos project.assets.json não encontrado</span><span class="sxs-lookup"><span data-stu-id="e078e-139">Assets file project.assets.json not found</span></span>

<span data-ttu-id="e078e-140">Mensagem de erro completa:</span><span class="sxs-lookup"><span data-stu-id="e078e-140">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="e078e-141">O arquivo `project.assets.json` mantém um grafo de dependência do projeto quando ocorre o uso do formato de gerenciamento PackageReference, que é usado para garantir que todos os pacotes necessários sejam instalados no computador.</span><span class="sxs-lookup"><span data-stu-id="e078e-141">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="e078e-142">Como esse arquivo é gerado de modo dinâmico por meio da restauração do pacote, ele geralmente não é adicionado ao controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="e078e-142">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="e078e-143">Como resultado, esse erro ocorre ao compilar um projeto com uma ferramenta como o `msbuild`, que não restaura os pacotes automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e078e-143">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="e078e-144">Nesse caso, execute `msbuild -t:restore` seguido por `msbuild` ou use `dotnet build` (que restaura automaticamente os pacotes).</span><span class="sxs-lookup"><span data-stu-id="e078e-144">In this case, run `msbuild -t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="e078e-145">Também é possível usar algum dos métodos de restauração de pacote descritos na [seção anterior](#missing).</span><span class="sxs-lookup"><span data-stu-id="e078e-145">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="e078e-146">Um ou mais pacotes NuGet precisam ser restaurados, mas não foi possível porque o consentimento não foi concedido</span><span class="sxs-lookup"><span data-stu-id="e078e-146">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="e078e-147">Mensagem de erro completa:</span><span class="sxs-lookup"><span data-stu-id="e078e-147">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="e078e-148">Esse erro indica que a restauração de pacote está desabilitada na configuração do NuGet.</span><span class="sxs-lookup"><span data-stu-id="e078e-148">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="e078e-149">Você pode alterar as configurações aplicáveis no Visual Studio, conforme descrito anteriormente em [Solução rápida para usuários do Visual Studio](#quick-solution-for-visual-studio-users).</span><span class="sxs-lookup"><span data-stu-id="e078e-149">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="e078e-150">Você também pode editar essas configurações diretamente no arquivo `nuget.config` aplicável (normalmente `%AppData%\NuGet\NuGet.Config` no Windows e `~/.nuget/NuGet/NuGet.Config` no Linux/Mac).</span><span class="sxs-lookup"><span data-stu-id="e078e-150">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="e078e-151">Verifique se as chaves `enabled` e `automatic` em `packageRestore` estão definidas como True:</span><span class="sxs-lookup"><span data-stu-id="e078e-151">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

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
> <span data-ttu-id="e078e-152">Se você editar as configurações de `packageRestore` diretamente em `nuget.config`, reinicie o Visual Studio para que a caixa de diálogo de opções mostre os valores atuais.</span><span class="sxs-lookup"><span data-stu-id="e078e-152">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="e078e-153">Outras condições possíveis</span><span class="sxs-lookup"><span data-stu-id="e078e-153">Other potential conditions</span></span>

- <span data-ttu-id="e078e-154">Você pode encontrar erros de build devido a arquivos ausentes, com uma mensagem indicando para usar a restauração do NuGet para baixá-los.</span><span class="sxs-lookup"><span data-stu-id="e078e-154">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="e078e-155">No entanto, ao executar uma restauração, a seguinte mensagem poderá aparecer: "Todos os pacotes já estão instalados e não há nada para ser restaurado".</span><span class="sxs-lookup"><span data-stu-id="e078e-155">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="e078e-156">Nesse caso, exclua a pasta `packages` (ao usar `packages.config`) ou o arquivo `obj/project.assets.json` (ao usar PackageReference) e execute a restauração novamente.</span><span class="sxs-lookup"><span data-stu-id="e078e-156">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="e078e-157">Se o erro continuar, use `nuget locals all -clear` ou `dotnet locals all --clear` pela linha de comando para limpar as pastas *global-packages* e de cache, conforme descrito em [Como gerenciar as pastas de pacotes globais e de cache](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="e078e-157">If the error still persists, use `nuget locals all -clear` or `dotnet locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="e078e-158">Ao obter um projeto por meio do controle do código-fonte, as pastas do projeto poderão ser definidas como somente leitura.</span><span class="sxs-lookup"><span data-stu-id="e078e-158">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="e078e-159">Altere as permissões de pasta e tente restaurar os pacotes novamente.</span><span class="sxs-lookup"><span data-stu-id="e078e-159">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="e078e-160">Talvez você esteja usando uma versão antiga do NuGet.</span><span class="sxs-lookup"><span data-stu-id="e078e-160">You may be using an old version of NuGet.</span></span> <span data-ttu-id="e078e-161">Acesse [nuget.org/downloads](https://www.nuget.org/downloads) para obter as versões mais recentes recomendadas.</span><span class="sxs-lookup"><span data-stu-id="e078e-161">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="e078e-162">Para o Visual Studio 2015, recomendamos a versão 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="e078e-162">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="e078e-163">Se você encontrar outros problemas, [envie um problema no GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para que possamos obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="e078e-163">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>
