---
title: Solucionando problemas de restauração de pacote do NuGet no Visual Studio
description: Uma descrição de erros de restauração de NuGet comuns no Visual Studio e como solucioná-los.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: c552941c896d1a7136310c0a8bc6755d5974809a
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="cce0e-103">Solução de problemas de erros de restauração de pacote</span><span class="sxs-lookup"><span data-stu-id="cce0e-103">Troubleshooting package restore errors</span></span>

<span data-ttu-id="cce0e-104">Este artigo aborda os erros comuns ao restaurar pacotes e as etapas para resolvê-los.</span><span class="sxs-lookup"><span data-stu-id="cce0e-104">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> <span data-ttu-id="cce0e-105">Para obter detalhes completos sobre a restauração de pacotes, veja [Restauração de pacote](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="cce0e-105">For complete details on restoring packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="cce0e-106">Se estas instruções não funcionarem para você, [envie um problema no GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para examinarmos o cenário mais cuidadosamente.</span><span class="sxs-lookup"><span data-stu-id="cce0e-106">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="cce0e-107">Não use o controle “Esta página é útil?”</span><span class="sxs-lookup"><span data-stu-id="cce0e-107">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="cce0e-108">que pode aparecer nesta página, pois ele não nos permite entrar em contato com você para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="cce0e-108">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="cce0e-109">Solução rápida para usuários do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cce0e-109">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="cce0e-110">Se você estiver usando o Visual Studio, primeiro habilite a restauração de pacote da maneira descrita a seguir.</span><span class="sxs-lookup"><span data-stu-id="cce0e-110">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="cce0e-111">Caso contrário, prossiga para as seções seguintes.</span><span class="sxs-lookup"><span data-stu-id="cce0e-111">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="cce0e-112">Selecione o comando de menu **Ferramentas > Gerenciador de Pacotes do NuGet > Configurações do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="cce0e-112">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="cce0e-113">Marque as duas opções em **Restauração de Pacote**.</span><span class="sxs-lookup"><span data-stu-id="cce0e-113">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="cce0e-114">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="cce0e-114">Select **OK**.</span></span>
1. <span data-ttu-id="cce0e-115">Compile o projeto novamente.</span><span class="sxs-lookup"><span data-stu-id="cce0e-115">Build your project again.</span></span>

![Habilitar a restauração de pacote do NuGet em Ferramenta/Opções](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="cce0e-117">Essas configurações também podem ser alteradas no arquivo `NuGet.config`; veja a seção de [consentimento](#consent).</span><span class="sxs-lookup"><span data-stu-id="cce0e-117">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="cce0e-118">Este projeto faz referência a pacotes NuGet ausentes neste computador</span><span class="sxs-lookup"><span data-stu-id="cce0e-118">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="cce0e-119">Mensagem de erro completa:</span><span class="sxs-lookup"><span data-stu-id="cce0e-119">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="cce0e-120">Esse erro ocorre ao tentar compilar um projeto com referências a um ou mais pacotes do NuGet, mas, no momento, esses pacotes não estão instalados no computador ou no projeto.</span><span class="sxs-lookup"><span data-stu-id="cce0e-120">This error occurs you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="cce0e-121">Quando o formato de gerenciamento PackageReference é usado, o erro significa que o pacote não está instalado na pasta *global-packages* conforme descrito em [Como gerenciar as pastas de pacotes globais e de cache](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="cce0e-121">When using the PackageReference management format, the error means that the package is not installed in the *global-packages* folder as described on as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>
- <span data-ttu-id="cce0e-122">Quando `packages.config` é usado, o erro significa que o pacote não está instalado na pasta `packages` na raiz da solução.</span><span class="sxs-lookup"><span data-stu-id="cce0e-122">When using `packages.config`, the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="cce0e-123">Essa situação geralmente ocorre ao obter o código-fonte do projeto por meio do controle do código-fonte ou de outro download.</span><span class="sxs-lookup"><span data-stu-id="cce0e-123">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="cce0e-124">Os pacotes normalmente são omitidos do controle do código-fonte ou dos downloads, uma vez que podem ser restaurados de feeds de pacotes, como o nuget.org (veja [Pacotes e controle do código-fonte](Packages-and-Source-Control.md)).</span><span class="sxs-lookup"><span data-stu-id="cce0e-124">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="cce0e-125">Por outro lado, a inclusão deles sobrecarregaria o repositório ou criaria arquivos .zip desnecessariamente grandes.</span><span class="sxs-lookup"><span data-stu-id="cce0e-125">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="cce0e-126">Use um dos seguintes métodos para restaurar os pacotes:</span><span class="sxs-lookup"><span data-stu-id="cce0e-126">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="cce0e-127">No Visual Studio, habilite a restauração de pacote selecionando o comando de menu **Ferramentas > Gerenciador de Pacotes do NuGet > Configurações do Gerenciador de Pacotes** marcando ambas as opções em **Restauração de Pacote** e selecionando **OK**.</span><span class="sxs-lookup"><span data-stu-id="cce0e-127">In Visual Studio, enable package restore by selecting the **Tools > NuGet Package Manager > Package Manager Settings** menu command, setting both options under **Package Restore**, and selecting **OK**.</span></span> <span data-ttu-id="cce0e-128">Em seguida, compile a solução novamente.</span><span class="sxs-lookup"><span data-stu-id="cce0e-128">Then build the solution again.</span></span>
- <span data-ttu-id="cce0e-129">Para projetos do .NET Core, execute `dotnet restore` ou `dotnet build` (que executa automaticamente a restauração).</span><span class="sxs-lookup"><span data-stu-id="cce0e-129">For .NET Core projects, run `dotnet restore` or `dotnet build` (which automatically runs restore).</span></span>
- <span data-ttu-id="cce0e-130">Na linha de comando, execute `nuget restore` (exceto para projetos criados com `dotnet`, caso em que `dotnet restore` deverá ser usado).</span><span class="sxs-lookup"><span data-stu-id="cce0e-130">On the command line, run `nuget restore` (except for projects created with `dotnet`, in which case use `dotnet restore`).</span></span>
- <span data-ttu-id="cce0e-131">Na linha de comando com projetos usando o formato PackageReference, execute `msbuild /t:restore`.</span><span class="sxs-lookup"><span data-stu-id="cce0e-131">On the command line with projects using the PackageReference format, run `msbuild /t:restore`.</span></span>

<span data-ttu-id="cce0e-132">Após uma restauração bem-sucedida, o pacote deve estar presente na pasta *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="cce0e-132">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="cce0e-133">Em caso de projetos que usam PackageReference, uma restauração deve recriar o arquivo `obj/project.assets.json`; em projetos que usam `packages.config`, o pacote deve aparecer na pasta `packages` do projeto.</span><span class="sxs-lookup"><span data-stu-id="cce0e-133">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="cce0e-134">Nesse momento, o projeto deverá ser compilado com êxito.</span><span class="sxs-lookup"><span data-stu-id="cce0e-134">The project should now build successfully.</span></span> <span data-ttu-id="cce0e-135">Caso contrário, [envie um problema no GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para que possamos acompanhá-lo com você.</span><span class="sxs-lookup"><span data-stu-id="cce0e-135">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="cce0e-136">Arquivo de ativos project.assets.json não encontrado</span><span class="sxs-lookup"><span data-stu-id="cce0e-136">Assets file project.assets.json not found</span></span>

<span data-ttu-id="cce0e-137">Mensagem de erro completa:</span><span class="sxs-lookup"><span data-stu-id="cce0e-137">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="cce0e-138">O arquivo `project.assets.json` mantém um grafo de dependência do projeto quando ocorre o uso do formato de gerenciamento PackageReference, que é usado para garantir que todos os pacotes necessários sejam instalados no computador.</span><span class="sxs-lookup"><span data-stu-id="cce0e-138">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="cce0e-139">Como esse arquivo é gerado de modo dinâmico por meio da restauração do pacote, ele geralmente não é adicionado ao controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="cce0e-139">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="cce0e-140">Como resultado, esse erro ocorre ao compilar um projeto com uma ferramenta como o `msbuild`, que não restaura os pacotes automaticamente.</span><span class="sxs-lookup"><span data-stu-id="cce0e-140">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="cce0e-141">Nesse caso, execute `msbuild /t:restore` seguido por `msbuild` ou use `dotnet build` (que restaura automaticamente os pacotes).</span><span class="sxs-lookup"><span data-stu-id="cce0e-141">In this case, run `msbuild /t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="cce0e-142">Também é possível usar algum dos métodos de restauração de pacote descritos na [seção anterior](#missing).</span><span class="sxs-lookup"><span data-stu-id="cce0e-142">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="cce0e-143">Um ou mais pacotes NuGet precisam ser restaurados, mas não foi possível porque o consentimento não foi concedido</span><span class="sxs-lookup"><span data-stu-id="cce0e-143">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="cce0e-144">Mensagem de erro completa:</span><span class="sxs-lookup"><span data-stu-id="cce0e-144">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="cce0e-145">Esse erro indica que a restauração de pacote está desabilitada na configuração do NuGet.</span><span class="sxs-lookup"><span data-stu-id="cce0e-145">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="cce0e-146">Você pode alterar as configurações aplicáveis no Visual Studio, conforme descrito anteriormente em [Solução rápida para usuários do Visual Studio](#quick-solution-for-visual-studio-users).</span><span class="sxs-lookup"><span data-stu-id="cce0e-146">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="cce0e-147">Você também pode editar essas configurações diretamente no arquivo `nuget.config` aplicável (normalmente `%AppData%\NuGet\NuGet.Config` no Windows e `~/.nuget/NuGet/NuGet.Config` no Linux/Mac).</span><span class="sxs-lookup"><span data-stu-id="cce0e-147">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="cce0e-148">Verifique se as chaves `enabled` e `automatic` em `packageRestore` estão definidas como True:</span><span class="sxs-lookup"><span data-stu-id="cce0e-148">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

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
> <span data-ttu-id="cce0e-149">Se você editar as configurações de `packageRestore` diretamente em `nuget.config`, reinicie o Visual Studio para que a caixa de diálogo de opções mostre os valores atuais.</span><span class="sxs-lookup"><span data-stu-id="cce0e-149">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="cce0e-150">Outras condições possíveis</span><span class="sxs-lookup"><span data-stu-id="cce0e-150">Other potential conditions</span></span>

- <span data-ttu-id="cce0e-151">Você pode encontrar erros de build devido a arquivos ausentes, com uma mensagem indicando para usar a restauração do NuGet para baixá-los.</span><span class="sxs-lookup"><span data-stu-id="cce0e-151">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="cce0e-152">No entanto, ao executar uma restauração, a seguinte mensagem poderá aparecer: "Todos os pacotes já estão instalados e não há nada para ser restaurado".</span><span class="sxs-lookup"><span data-stu-id="cce0e-152">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="cce0e-153">Nesse caso, exclua a pasta `packages` (ao usar `packages.config`) ou o arquivo `obj/project.assets.json` (ao usar PackageReference) e execute a restauração novamente.</span><span class="sxs-lookup"><span data-stu-id="cce0e-153">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="cce0e-154">Se o erro continuar, use `nuget locals all -clear` ou `dotnet locals all --clear` pela linha de comando para limpar as pastas *global-packages* e de cache, conforme descrito em [Como gerenciar as pastas de pacotes globais e de cache](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="cce0e-154">If the error still persists, use `nuget locals all -clear` or `dotnet locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="cce0e-155">Ao obter um projeto por meio do controle do código-fonte, as pastas do projeto poderão ser definidas como somente leitura.</span><span class="sxs-lookup"><span data-stu-id="cce0e-155">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="cce0e-156">Altere as permissões de pasta e tente restaurar os pacotes novamente.</span><span class="sxs-lookup"><span data-stu-id="cce0e-156">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="cce0e-157">Talvez você esteja usando uma versão antiga do NuGet.</span><span class="sxs-lookup"><span data-stu-id="cce0e-157">You may be using an old version of NuGet.</span></span> <span data-ttu-id="cce0e-158">Acesse [nuget.org/downloads](https://www.nuget.org/downloads) para obter as versões mais recentes recomendadas.</span><span class="sxs-lookup"><span data-stu-id="cce0e-158">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="cce0e-159">Para o Visual Studio 2015, recomendamos a versão 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="cce0e-159">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="cce0e-160">Se você encontrar outros problemas, [envie um problema no GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para que possamos obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="cce0e-160">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>