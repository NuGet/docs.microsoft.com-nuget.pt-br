---
title: "Solução de problemas da restauração de pacote do NuGet no Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Uma descrição de erros de restauração de NuGet comuns no Visual Studio e como solucioná-los."
keywords: "Restauração de pacote do NuGet, restaurando pacotes, solucionando problemas, solução de problemas"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8efaed497a596921af3c73ab919831c73bf598e0
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/15/2018
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="654fb-104">Solução de problemas de erros de restauração de pacote</span><span class="sxs-lookup"><span data-stu-id="654fb-104">Troubleshooting package restore errors</span></span>

<span data-ttu-id="654fb-105">Este artigo aborda os erros comuns ao restaurar pacotes e as etapas para resolvê-los.</span><span class="sxs-lookup"><span data-stu-id="654fb-105">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> <span data-ttu-id="654fb-106">Para obter detalhes completos sobre a restauração de pacotes, veja [Restauração de pacote](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="654fb-106">For complete details on restoring packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="654fb-107">Se estas instruções não funcionarem para você, [envie um problema no GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para examinarmos o cenário mais cuidadosamente.</span><span class="sxs-lookup"><span data-stu-id="654fb-107">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="654fb-108">Não use o controle "Esta página é útil?"</span><span class="sxs-lookup"><span data-stu-id="654fb-108">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="654fb-109">que pode aparecer nesta página, pois ele não nos possibilita contatar você para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="654fb-109">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="654fb-110">Solução rápida para usuários do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="654fb-110">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="654fb-111">Se você estiver usando o Visual Studio, primeiro habilite a restauração de pacote da maneira descrita a seguir.</span><span class="sxs-lookup"><span data-stu-id="654fb-111">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="654fb-112">Caso contrário, prossiga para as seções seguintes.</span><span class="sxs-lookup"><span data-stu-id="654fb-112">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="654fb-113">Selecione o comando de menu **Ferramentas > Gerenciador de Pacotes do NuGet > Configurações do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="654fb-113">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="654fb-114">Marque as duas opções em **Restauração de Pacote**.</span><span class="sxs-lookup"><span data-stu-id="654fb-114">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="654fb-115">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="654fb-115">Select **OK**.</span></span>
1. <span data-ttu-id="654fb-116">Compile o projeto novamente.</span><span class="sxs-lookup"><span data-stu-id="654fb-116">Build your project again.</span></span>

![Habilitar a restauração de pacote do NuGet em Ferramenta/Opções](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="654fb-118">Essas configurações também podem ser alteradas no arquivo `NuGet.config`; veja a seção de [consentimento](#consent).</span><span class="sxs-lookup"><span data-stu-id="654fb-118">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="654fb-119">Este projeto faz referência a pacotes NuGet ausentes neste computador</span><span class="sxs-lookup"><span data-stu-id="654fb-119">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="654fb-120">Mensagem de erro completa:</span><span class="sxs-lookup"><span data-stu-id="654fb-120">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="654fb-121">Esse erro ocorre ao tentar compilar um projeto com referências a um ou mais pacotes do NuGet, mas, no momento, esses pacotes não estão armazenados em cache no projeto.</span><span class="sxs-lookup"><span data-stu-id="654fb-121">This error occurs you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently cached in the project.</span></span> <span data-ttu-id="654fb-122">(Os pacotes são armazenados em cache em uma pasta `packages` na raiz da solução se o projeto usa `packages.config` ou no arquivo `obj/project.assets.json` se o projeto usa o formato PackageReference.)</span><span class="sxs-lookup"><span data-stu-id="654fb-122">(Packages are cached in a `packages` folder at the solution root if the project uses `packages.config`, or in the `obj/project.assets.json` file if the project uses the PackageReference format.)</span></span>

<span data-ttu-id="654fb-123">Essa situação geralmente ocorre ao obter o código-fonte do projeto por meio do controle do código-fonte ou de outro download.</span><span class="sxs-lookup"><span data-stu-id="654fb-123">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="654fb-124">Os pacotes normalmente são omitidos do controle do código-fonte ou dos downloads, uma vez que podem ser restaurados de feeds de pacotes, como o nuget.org (veja [Pacotes e controle do código-fonte](Packages-and-Source-Control.md)).</span><span class="sxs-lookup"><span data-stu-id="654fb-124">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="654fb-125">Por outro lado, a inclusão deles sobrecarregaria o repositório ou criaria arquivos .zip desnecessariamente grandes.</span><span class="sxs-lookup"><span data-stu-id="654fb-125">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="654fb-126">Use um dos seguintes métodos para restaurar os pacotes:</span><span class="sxs-lookup"><span data-stu-id="654fb-126">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="654fb-127">No Visual Studio, habilite a restauração de pacote selecionando o comando de menu **Ferramentas > Gerenciador de Pacotes do NuGet > Configurações do Gerenciador de Pacotes** marcando ambas as opções em **Restauração de Pacote** e selecionando **OK**.</span><span class="sxs-lookup"><span data-stu-id="654fb-127">In Visual Studio, enable package restore by selecting the **Tools > NuGet Package Manager > Package Manager Settings** menu command, setting both options under **Package Restore**, and selecting **OK**.</span></span> <span data-ttu-id="654fb-128">Em seguida, compile a solução novamente.</span><span class="sxs-lookup"><span data-stu-id="654fb-128">Then build the solution again.</span></span>
- <span data-ttu-id="654fb-129">Para projetos do .NET Core, execute `dotnet restore` ou `dotnet build` (que executa automaticamente a restauração).</span><span class="sxs-lookup"><span data-stu-id="654fb-129">For .NET Core projects, run `dotnet restore` or `dotnet build` (which automatically runs restore).</span></span>
- <span data-ttu-id="654fb-130">Na linha de comando, execute `nuget restore` (exceto para projetos criados com `dotnet`, caso em que `dotnet restore` deverá ser usado).</span><span class="sxs-lookup"><span data-stu-id="654fb-130">On the command line, run `nuget restore` (except for projects created with `dotnet`, in which case use `dotnet restore`).</span></span>
- <span data-ttu-id="654fb-131">Na linha de comando com projetos usando o formato PackageReference, execute `msbuild /t:restore`.</span><span class="sxs-lookup"><span data-stu-id="654fb-131">On the command line with projects using the PackageReference format, run `msbuild /t:restore`.</span></span>

<span data-ttu-id="654fb-132">Após uma restauração bem-sucedida, você deverá ver uma pasta `packages` (ao usar `packages.config`) ou o arquivo `obj/project.assets.json` (ao usar PackageReference).</span><span class="sxs-lookup"><span data-stu-id="654fb-132">After a successful restore, you should see either a `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference).</span></span> <span data-ttu-id="654fb-133">Nesse momento, o projeto deverá ser compilado com êxito.</span><span class="sxs-lookup"><span data-stu-id="654fb-133">The project should now build successfully.</span></span> <span data-ttu-id="654fb-134">Caso contrário, [envie um problema no GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para que possamos acompanhá-lo com você.</span><span class="sxs-lookup"><span data-stu-id="654fb-134">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="654fb-135">Arquivo de ativos project.assets.json não encontrado</span><span class="sxs-lookup"><span data-stu-id="654fb-135">Assets file project.assets.json not found</span></span>

<span data-ttu-id="654fb-136">Mensagem de erro completa:</span><span class="sxs-lookup"><span data-stu-id="654fb-136">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="654fb-137">Esse erro ocorre pelos mesmos motivos que os explicados na [seção anterior](#missing) e apresentam as mesmas soluções.</span><span class="sxs-lookup"><span data-stu-id="654fb-137">This error occurs for the same reasons as explained in the [previous section](#missing), and has the same remedies.</span></span> <span data-ttu-id="654fb-138">Por exemplo, executar `msbuild` em um projeto do .NET Core obtido por meio do controle do código-fonte não restaurará automaticamente os pacotes.</span><span class="sxs-lookup"><span data-stu-id="654fb-138">For example, running `msbuild` on a .NET Core project that's been obtained from source control won't automatically restore packages.</span></span> <span data-ttu-id="654fb-139">Nesse caso, execute `msbuild /t:restore` seguido por `msbuild` ou use `dotnet build` (que restaura automaticamente os pacotes).</span><span class="sxs-lookup"><span data-stu-id="654fb-139">In this case, run `msbuild /t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="654fb-140">Um ou mais pacotes NuGet precisam ser restaurados, mas não foi possível porque o consentimento não foi concedido</span><span class="sxs-lookup"><span data-stu-id="654fb-140">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="654fb-141">Mensagem de erro completa:</span><span class="sxs-lookup"><span data-stu-id="654fb-141">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="654fb-142">Esse erro indica que a restauração de pacote está desabilitada na configuração do NuGet.</span><span class="sxs-lookup"><span data-stu-id="654fb-142">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="654fb-143">Você pode alterar as configurações aplicáveis no Visual Studio, conforme descrito anteriormente em [Solução rápida para usuários do Visual Studio](#quick-solution-for-visual-studio-users).</span><span class="sxs-lookup"><span data-stu-id="654fb-143">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="654fb-144">Você também pode editar essas configurações diretamente no arquivo `nuget.config` aplicável (normalmente `%AppData%\NuGet\NuGet.Config` no Windows e `~/.nuget/NuGet/NuGet.Config` no Linux/Mac).</span><span class="sxs-lookup"><span data-stu-id="654fb-144">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="654fb-145">Verifique se as chaves `enabled` e `automatic` em `packageRestore` estão definidas como True:</span><span class="sxs-lookup"><span data-stu-id="654fb-145">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

<span data-ttu-id="654fb-146">Observe que, se você editar as configurações de `packageRestore` diretamente em `nuget.config`, reinicie o Visual Studio para que a caixa de diálogo de opções mostre os valores atuais.</span><span class="sxs-lookup"><span data-stu-id="654fb-146">Note that if you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="654fb-147">Outras condições possíveis</span><span class="sxs-lookup"><span data-stu-id="654fb-147">Other potential conditions</span></span>

- <span data-ttu-id="654fb-148">Você pode encontrar erros de build devido a arquivos ausentes, com uma mensagem indicando para usar a restauração do NuGet para baixá-los.</span><span class="sxs-lookup"><span data-stu-id="654fb-148">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="654fb-149">No entanto, ao executar uma restauração, a seguinte mensagem poderá aparecer: "Todos os pacotes já estão instalados e não há nada para ser restaurado".</span><span class="sxs-lookup"><span data-stu-id="654fb-149">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="654fb-150">Nesse caso, exclua a pasta `packages` (ao usar `packages.config`) ou o arquivo `obj/project.assets.json` (ao usar PackageReference) e execute a restauração novamente.</span><span class="sxs-lookup"><span data-stu-id="654fb-150">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span>

- <span data-ttu-id="654fb-151">Ao obter um projeto por meio do controle do código-fonte, as pastas do projeto poderão ser definidas como somente leitura.</span><span class="sxs-lookup"><span data-stu-id="654fb-151">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="654fb-152">Altere as permissões de pasta e tente restaurar os pacotes novamente.</span><span class="sxs-lookup"><span data-stu-id="654fb-152">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="654fb-153">Talvez você esteja usando uma versão antiga do NuGet.</span><span class="sxs-lookup"><span data-stu-id="654fb-153">You may be using an old version of NuGet.</span></span> <span data-ttu-id="654fb-154">Acesse [nuget.org/downloads](https://www.nuget.org/downloads) para obter as versões mais recentes recomendadas.</span><span class="sxs-lookup"><span data-stu-id="654fb-154">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="654fb-155">Para o Visual Studio 2015, recomendamos a versão 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="654fb-155">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="654fb-156">Se você encontrar outros problemas, [envie um problema no GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para que possamos obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="654fb-156">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>