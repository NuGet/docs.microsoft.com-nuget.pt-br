---
title: Como gerenciar as pastas de pacotes globais, de cache e temporárias no NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Como gerenciar a pasta de instalação de pacote global, o cache de pacote e as pastas temporárias que existem em um computador, usados durante a instalação, restauração e atualização de pacotes.
keywords: Pasta de pacotes globais do NuGet, cache de pacote do NuGet, cache de pacote, pasta de instalação de pacote, caches do NuGet, gerenciar caches, cache local do NuGet, cache global do NuGet, comando locals do NuGet, limpar um cache
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e9f4383a3f1700b96e3d6fe9ea4c0a7c24daa45a
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a><span data-ttu-id="04abc-104">Como gerenciar as pastas de pacotes globais, de cache e temporárias</span><span class="sxs-lookup"><span data-stu-id="04abc-104">Managing the global packages, cache, and temp folders</span></span>

<span data-ttu-id="04abc-105">Sempre que você instala, atualiza ou restaura um pacote, o NuGet gerencia pacotes e informações do pacote em várias pastas fora da estrutura do seu projeto:</span><span class="sxs-lookup"><span data-stu-id="04abc-105">Whenever you install, update, or restore a package, NuGet manages packages and package information in several folders outside of your project structure:</span></span>

| <span data-ttu-id="04abc-106">Nome</span><span class="sxs-lookup"><span data-stu-id="04abc-106">Name</span></span> | <span data-ttu-id="04abc-107">Descrição e localização (por usuário)</span><span class="sxs-lookup"><span data-stu-id="04abc-107">Description and Location (per user)</span></span>|
| --- | --- |
| <span data-ttu-id="04abc-108">global&#8209;packages</span><span class="sxs-lookup"><span data-stu-id="04abc-108">global&#8209;packages</span></span> | <span data-ttu-id="04abc-109">A pasta *global-packages* é onde o NuGet instala qualquer pacote baixado.</span><span class="sxs-lookup"><span data-stu-id="04abc-109">The *global-packages* folder is where NuGet installs any downloaded package.</span></span> <span data-ttu-id="04abc-110">Cada pacote é totalmente expandido em uma subpasta que corresponde ao identificador de pacote e ao número de versão.</span><span class="sxs-lookup"><span data-stu-id="04abc-110">Each package is fully expanded into a subfolder that matches the package identifier and version number.</span></span> <span data-ttu-id="04abc-111">Os projetos que usam o formato PackageReference sempre usam pacotes diretamente dessa pasta.</span><span class="sxs-lookup"><span data-stu-id="04abc-111">Projects using the PackageReference format always use packages directly from this folder.</span></span> <span data-ttu-id="04abc-112">Ao usar o `packages.config`, os pacotes são instalados na pasta *global-packages*, depois são copiados para a pasta `packages` do projeto.</span><span class="sxs-lookup"><span data-stu-id="04abc-112">When using the `packages.config`, packages are installed to the *global-packages* folder, then copied into the project's `packages` folder.</span></span><br/><ul><li><span data-ttu-id="04abc-113">Windows: `%userprofile%\.nuget\packages`</span><span class="sxs-lookup"><span data-stu-id="04abc-113">Windows: `%userprofile%\.nuget\packages`</span></span></li><li><span data-ttu-id="04abc-114">Mac/Linux: `~/.nuget/packages`</span><span class="sxs-lookup"><span data-stu-id="04abc-114">Mac/Linux: `~/.nuget/packages`</span></span></li><li><span data-ttu-id="04abc-115">Substitua usando a variável de ambiente NUGET_PACKAGES, as [definições de configuração](../reference/nuget-config-file.md#config-section) de `globalPackagesFolder` ou `repositoryPath` (ao usar PackageReference e `packages.config`, respectivamente) ou a propriedade do MSBuild `RestorePackagesPath` (somente MSBuild).</span><span class="sxs-lookup"><span data-stu-id="04abc-115">Override using the NUGET_PACKAGES environment variable, the `globalPackagesFolder` or `repositoryPath` [configuration settings](../reference/nuget-config-file.md#config-section) (when using PackageReference and `packages.config`, respectively), or the `RestorePackagesPath` MSBuild property (MSBuild only).</span></span> <span data-ttu-id="04abc-116">A variável de ambiente tem precedência sobre a definição de configuração.</span><span class="sxs-lookup"><span data-stu-id="04abc-116">The environment variable takes precedence over the configuration setting.</span></span></li></ul> |
| <span data-ttu-id="04abc-117">http&#8209;cache</span><span class="sxs-lookup"><span data-stu-id="04abc-117">http&#8209;cache</span></span> | <span data-ttu-id="04abc-118">O Gerenciador de Pacotes do Visual Studio (NuGet 3.x ou posterior) e a ferramenta `dotnet` armazenam cópias de pacotes baixados nesse cache (salvos como arquivos `.dat`), organizados em subpastas para cada origem de pacote.</span><span class="sxs-lookup"><span data-stu-id="04abc-118">The Visual Studio Package Manager (NuGet 3.x+) and the `dotnet` tool store copies of downloaded packages in this cache (saved as `.dat` files), organized into subfolders for each package source.</span></span> <span data-ttu-id="04abc-119">Os pacotes não são expandidos, e o cache tem um tempo de expiração de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="04abc-119">Packages are not expanded, and the cache has an expiration time of 30 minutes.</span></span><br/><ul><li><span data-ttu-id="04abc-120">Windows: `%localappdata%\NuGet\v3-cache`</span><span class="sxs-lookup"><span data-stu-id="04abc-120">Windows: `%localappdata%\NuGet\v3-cache`</span></span></li><li><span data-ttu-id="04abc-121">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span><span class="sxs-lookup"><span data-stu-id="04abc-121">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span></span></li><li><span data-ttu-id="04abc-122">Substitua usando a variável de ambiente NUGET_HTTP_CACHE_PATH.</span><span class="sxs-lookup"><span data-stu-id="04abc-122">Override using the NUGET_HTTP_CACHE_PATH environment variable.</span></span></li></ul> |
| <span data-ttu-id="04abc-123">temp</span><span class="sxs-lookup"><span data-stu-id="04abc-123">temp</span></span> | <span data-ttu-id="04abc-124">Uma pasta em que o NuGet armazena arquivos temporários durante suas várias operações.</span><span class="sxs-lookup"><span data-stu-id="04abc-124">A folder where NuGet stores temporary files during its various operations.</span></span><br/><li><span data-ttu-id="04abc-125">Windows: `%temp%\NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="04abc-125">Windows: `%temp%\NuGetScratch`</span></span></li><li><span data-ttu-id="04abc-126">Mac/Linux: `/tmp/NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="04abc-126">Mac/Linux: `/tmp/NuGetScratch`</span></span></li></ul> |

> [!Note]
> <span data-ttu-id="04abc-127">O NuGet 3.5 e versões anteriores usam *packages-cache* em vez de *http-cache*, que está localizado em `%localappdata%\NuGet\Cache`.</span><span class="sxs-lookup"><span data-stu-id="04abc-127">NuGet 3.5 and earlier uses *packages-cache* instead of the *http-cache*, which is located in `%localappdata%\NuGet\Cache`.</span></span>

<span data-ttu-id="04abc-128">Ao usar as pastas de cache e *global-packages*, geralmente o NuGet evita o download de pacotes que já existem no computador, melhorando o desempenho da instalação, atualização e restauração de operações.</span><span class="sxs-lookup"><span data-stu-id="04abc-128">By using the cache and *global-packages* folders, NuGet generally avoids downloading packages that already exist on the computer, improving the performance of install, update, and restore operations.</span></span> <span data-ttu-id="04abc-129">Quando PackageReference é usado, a pasta *global-packages* também evita o armazenamento de pacotes baixados dentro das pastas de projeto, onde eles podem ser inadvertidamente adicionados ao controle do código-fonte, e reduz o impacto geral do NuGet no armazenamento do computador.</span><span class="sxs-lookup"><span data-stu-id="04abc-129">When using PackageReference, the *global-packages* folder also avoids keeping downloaded packages inside project folders, where they might be inadvertently added to source control, and reduces NuGet's overall impact on computer storage.</span></span>

<span data-ttu-id="04abc-130">Quando solicitado a recuperar um pacote, o NuGet primeiro examina a pasta *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="04abc-130">When asked to retrieve a package, NuGet first looks in the *global-packages* folder.</span></span> <span data-ttu-id="04abc-131">Se a versão exata do pacote não estiver lá, o NuGet verificará todas as origens de pacote não HTTP.</span><span class="sxs-lookup"><span data-stu-id="04abc-131">If the exact version of package is not there, then NuGet checks all non-HTTP package sources.</span></span> <span data-ttu-id="04abc-132">Se ainda assim o pacote não for encontrado, o NuGet procurará o pacote no *http-cache*, a menos que você especifique `--no-cache` com comandos `dotnet.exe` ou `-NoCache` com comandos `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="04abc-132">If the package is still not found, NuGet looks for the package in the *http-cache* unless you specify `--no-cache` with `dotnet.exe` commands or `-NoCache` with `nuget.exe` commands.</span></span> <span data-ttu-id="04abc-133">Se o pacote não estiver no cache ou se o cache não for usado, o NuGet recuperará o pacote via HTTP.</span><span class="sxs-lookup"><span data-stu-id="04abc-133">If the package is not in the cache, or the cache isn't used, NuGet then retrieves the package over HTTP .</span></span>

<span data-ttu-id="04abc-134">Para saber mais, confira [O que acontece quando um pacote é instalado](ways-to-install-a-package.md#what-happens-when-a-package-is-installed).</span><span class="sxs-lookup"><span data-stu-id="04abc-134">For more information, see [What happens when a package is installed](ways-to-install-a-package.md#what-happens-when-a-package-is-installed).</span></span>

## <a name="viewing-folder-locations"></a><span data-ttu-id="04abc-135">Exibir os locais de pastas</span><span class="sxs-lookup"><span data-stu-id="04abc-135">Viewing folder locations</span></span>

<span data-ttu-id="04abc-136">É possível exibir os locais de pasta usando o [comando dotnet nuget locals](/dotnet/core/tools/dotnet-nuget-locals):</span><span class="sxs-lookup"><span data-stu-id="04abc-136">You can view folder locations using the [dotnet nuget locals command](/dotnet/core/tools/dotnet-nuget-locals):</span></span>

```cli
dotnet nuget locals all --list
```

<span data-ttu-id="04abc-137">Saída típica (Mac/Linux; "user1" é o nome de usuário atual):</span><span class="sxs-lookup"><span data-stu-id="04abc-137">Typical output (Mac/Linux; "user1" is the current username):</span></span>

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
```

<span data-ttu-id="04abc-138">Para exibir a localização de uma única pasta, use `http-cache`, `global-packages` ou `temp`, em vez de `all`.</span><span class="sxs-lookup"><span data-stu-id="04abc-138">To display the location of a single folder, use `http-cache`, `global-packages`, or `temp` instead of `all`.</span></span> 

<span data-ttu-id="04abc-139">Também é possível exibir os locais usando o [comando nuget locals](../tools/cli-ref-locals.md):</span><span class="sxs-lookup"><span data-stu-id="04abc-139">You also view locations using the [nuget locals command](../tools/cli-ref-locals.md):</span></span>

```cli
# Display locals for all folders: global-packages, cache, and temp
nuget locals all -list
```

<span data-ttu-id="04abc-140">Saída típica (Windows; "user1" é o nome de usuário atual):</span><span class="sxs-lookup"><span data-stu-id="04abc-140">Typical output (Windows; "user1" is the current username):</span></span>

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
```

<span data-ttu-id="04abc-141">(`package-cache` é usado no NuGet 2.x e aparece no NuGet 3.5 e versões anteriores).</span><span class="sxs-lookup"><span data-stu-id="04abc-141">(`package-cache` is used in NuGet 2.x and appears with NuGet 3.5 and earlier.)</span></span>

## <a name="clearing-local-folders"></a><span data-ttu-id="04abc-142">Limpar pastas locais</span><span class="sxs-lookup"><span data-stu-id="04abc-142">Clearing local folders</span></span>

<span data-ttu-id="04abc-143">Se você encontrar problemas de instalação do pacote ou se desejar garantir que esteja instalando pacotes de uma galeria remota, use a opção `locals --clear` (dotnet.exe) ou `locals -clear` (nuget.exe), especificando a pasta a ser limpa, ou `all` para limpar todas as pastas:</span><span class="sxs-lookup"><span data-stu-id="04abc-143">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals --clear` option (dotnet.exe) or `locals -clear` (nuget.exe), specifying the folder to clear, or `all` to clear all folders:</span></span>

```cli
# Clear the 3.x+ cache (use either command)
dotnet nuget locals http-cache --clear
nuget locals http-cache -clear

# Clear the 2.x cache (NuGet CLI 3.5 and earlier only)
nuget locals packages-cache -clear

# Clear the global packages folder (use either command)
dotnet nuget locals global-packages --clear
nuget locals global-packages -clear

# Clear the temporary cache (use either command)
dotnet nuget locals temp --clear
nuget locals temp -clear

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

<span data-ttu-id="04abc-144">Todos os pacotes usados por projetos que estejam abertos no momento no Visual Studio não serão apagados da pasta *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="04abc-144">Any packages used by projects that are currently open in Visual Studio are not cleared from the *global-packages* folder.</span></span>

<span data-ttu-id="04abc-145">No Visual Studio, use o comando de menu **Ferramentas > Gerenciador de Pacotes do NuGet > Configurações do Gerenciador de Pacotes**, depois selecione **Limpar todo o cache do NuGet**.</span><span class="sxs-lookup"><span data-stu-id="04abc-145">In Visual Studio, use the **Tools > NuGet Package Manager > Package Manager Settings** menu command, then select **Clear All NuGet Cache(s)**.</span></span> <span data-ttu-id="04abc-146">O gerenciamento de cache não está disponível atualmente por meio do Console do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="04abc-146">Managing the cache isn't presently available through the Package Manager Console.</span></span>

![Comando de opção do NuGet para limpar caches](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a><span data-ttu-id="04abc-148">Solução de erros</span><span class="sxs-lookup"><span data-stu-id="04abc-148">Troubleshooting errors</span></span>

<span data-ttu-id="04abc-149">Os seguintes erros podem ocorrer ao usar `nuget locals` ou `dotnet nuget locals`:</span><span class="sxs-lookup"><span data-stu-id="04abc-149">The following errors can occur when using `nuget locals` or `dotnet nuget locals`:</span></span>

- <span data-ttu-id="04abc-150">*Erro: o processo não pode acessar o arquivo <package> porque ele está sendo usado por outro processo* ou *Falha ao limpar os recursos locais: não é possível excluir um ou mais arquivos*</span><span class="sxs-lookup"><span data-stu-id="04abc-150">*Error: The process cannot access the file <package> because it is being used by another process* or *Clearing local resources failed: Unable to delete one or more files*</span></span>

    <span data-ttu-id="04abc-151">Um ou mais arquivos da pasta estão em uso por outro processo. Por exemplo, um projeto do Visual Studio está aberto e se refere aos pacotes da pasta *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="04abc-151">One or more files in the folder are in use by another process; for example, a Visual Studio project is open that refers to packages in the *global-packages* folder.</span></span> <span data-ttu-id="04abc-152">Feche os processos e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="04abc-152">Close those processes and try again.</span></span>

- <span data-ttu-id="04abc-153">*Erro: o acesso ao caminho <path> foi negado* ou *O diretório não está vazio*</span><span class="sxs-lookup"><span data-stu-id="04abc-153">*Error: Access to the path <path> is denied* or *The directory is not empty*</span></span>

    <span data-ttu-id="04abc-154">Você não tem permissão para excluir arquivos no cache.</span><span class="sxs-lookup"><span data-stu-id="04abc-154">You don't have permission to delete files in the cache.</span></span> <span data-ttu-id="04abc-155">Altere as permissões de pasta, se possível, e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="04abc-155">Change the folder permissions, if possible, and try again.</span></span> <span data-ttu-id="04abc-156">Senão, entre em contato com o administrador do sistema.</span><span class="sxs-lookup"><span data-stu-id="04abc-156">Otherwise, contact your system administrator.</span></span>

- <span data-ttu-id="04abc-157">*Erro: o caminho ou o nome de arquivo especificado, ou ambos, são muito longos. O nome de arquivo totalmente qualificado deve ter menos de 260 caracteres e o nome do diretório, menos de 248 caracteres.*</span><span class="sxs-lookup"><span data-stu-id="04abc-157">*Error: The specified path, file name, or both are too long. The fully qualified file name must be less than 260 characters, and the directory name must be less than 248 characters.*</span></span>

    <span data-ttu-id="04abc-158">Reduza os nomes de pasta e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="04abc-158">Shorten the folder names and try again.</span></span>