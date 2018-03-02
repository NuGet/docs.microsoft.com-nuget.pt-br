---
title: Formas de instalar pacotes NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Descreve o processo de instalação de pacotes NuGet em um projeto, incluindo o que acontece no disco e com os arquivos de projeto aplicáveis."
keywords: "instalar o NuGet, consumo de pacote NuGet, instalação de pacotes NuGet, referências de pacote NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3bae03e148a366388c10d08e83c89dac6ff56d06
ms.sourcegitcommit: 33436d122873249dbb20616556cd8c6783f38909
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2018
---
# <a name="different-ways-to-install-a-nuget-package"></a><span data-ttu-id="01ff6-104">Maneiras diferentes de instalar um pacote NuGet</span><span class="sxs-lookup"><span data-stu-id="01ff6-104">Different ways to install a NuGet Package</span></span>

<span data-ttu-id="01ff6-105">Os pacotes NuGet são baixados e instalados usando qualquer um dos métodos a seguir (veja [Instalar ferramentas de cliente NuGet](../install-nuget-client-tools.md) se eles ainda não estiverem instalados):</span><span class="sxs-lookup"><span data-stu-id="01ff6-105">NuGet packages are downloaded and installed using any of the following methods (see [Install NuGet client tools](../install-nuget-client-tools.md) if you don't have these installed already):</span></span>

| <span data-ttu-id="01ff6-106">Método</span><span class="sxs-lookup"><span data-stu-id="01ff6-106">Method</span></span> | <span data-ttu-id="01ff6-107">Descrição</span><span class="sxs-lookup"><span data-stu-id="01ff6-107">Description</span></span> |
| --- | --- |
| <span data-ttu-id="01ff6-108">CLI do dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="01ff6-108">dotnet.exe CLI</span></span><br/>`dotnet install <package_name>` | <span data-ttu-id="01ff6-109">(Todas as plataformas) Baixa o pacote identificado por \<package_name\>, expande seu conteúdo para uma pasta no diretório atual e adiciona uma referência ao arquivo do projeto.</span><span class="sxs-lookup"><span data-stu-id="01ff6-109">(All platforms) Downloads the package identified by \<package_name\>, expands its contents into a folder in the current directory, and adds a reference to the project file.</span></span> <span data-ttu-id="01ff6-110">Além disso, baixa e instala as dependências.</span><span class="sxs-lookup"><span data-stu-id="01ff6-110">Also downloads and installs dependencies.</span></span><ul><li>[<span data-ttu-id="01ff6-111">Instalar e usar um pacote (CLI do dotnet)</span><span class="sxs-lookup"><span data-stu-id="01ff6-111">Install and use a package (dotnet CLI)</span></span>](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[<span data-ttu-id="01ff6-112">Comandos dotnet</span><span class="sxs-lookup"><span data-stu-id="01ff6-112">dotnet commands</span></span>](../tools/dotnet-commands.md)</li></ul> |
| <span data-ttu-id="01ff6-113">Interface do Usuário do Gerenciador de Pacotes (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="01ff6-113">Package Manager UI (Visual Studio)</span></span> | <span data-ttu-id="01ff6-114">(Windows e Mac) Fornece uma interface do usuário por meio da qual você pode procurar, selecionar e instalar pacotes e suas dependências em um projeto.</span><span class="sxs-lookup"><span data-stu-id="01ff6-114">(Windows and Mac) Provides a UI through which you can browse, select, and install packages and their dependencies into a project.</span></span> <span data-ttu-id="01ff6-115">Adicione referências a pacotes instalados ao arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="01ff6-115">Adds references to installed packages to the project file.</span></span><ul><li>[<span data-ttu-id="01ff6-116">Instalar e usar um pacote (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="01ff6-116">Install and use a package (Visual Studio)</span></span>](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[<span data-ttu-id="01ff6-117">Referência da interface do usuário do Gerenciador de Pacotes (Windows)</span><span class="sxs-lookup"><span data-stu-id="01ff6-117">Package Manager UI reference (Windows)</span></span>](../tools/package-manager-ui.md)</li><li>[<span data-ttu-id="01ff6-118">Incluir um pacote NuGet ao seu projeto (Mac)</span><span class="sxs-lookup"><span data-stu-id="01ff6-118">Including a NuGet package in your project (Mac)</span></span>](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| <span data-ttu-id="01ff6-119">Console do Gerenciador de Pacotes (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="01ff6-119">Package Manager Console (Visual Studio)</span></span><br/>`Install-Package <package_name>` | <span data-ttu-id="01ff6-120">(Somente Windows) Baixa e instala o pacote identificado por \<package_name\> em um projeto especificado na solução, depois adiciona uma referência ao arquivo do projeto.</span><span class="sxs-lookup"><span data-stu-id="01ff6-120">(Windows only) Downloads and installs the package identified by \<package_name\> into a specified project in the solution, then adds a reference to the project file.</span></span> <span data-ttu-id="01ff6-121">Além disso, baixa e instala as dependências.</span><span class="sxs-lookup"><span data-stu-id="01ff6-121">Also downloads and installs dependencies.</span></span><ul><li>[<span data-ttu-id="01ff6-122">Instalar e usar um pacote (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="01ff6-122">Install and use a package (Visual Studio)</span></span>](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[<span data-ttu-id="01ff6-123">Guia do Console do Gerenciador de Pacotes</span><span class="sxs-lookup"><span data-stu-id="01ff6-123">Package Manager Console guide</span></span>](../tools/package-manager-console.md)</li></ul> |
| <span data-ttu-id="01ff6-124">CLI do nuget.exe</span><span class="sxs-lookup"><span data-stu-id="01ff6-124">nuget.exe CLI</span></span><br/>`nuget install <package_name>` | <span data-ttu-id="01ff6-125">(Todas as plataformas) Baixa o pacote identificado por \<package_name\> e expande seu conteúdo em uma pasta no diretório atual; também pode baixar todos os pacotes listados em um arquivo do `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="01ff6-125">(All platforms) Downloads the package identified by \<package_name\> and expands its contents into a folder in the current directory; can also download all packages listed in a `packages.config` file.</span></span> <span data-ttu-id="01ff6-126">Também baixa e instala as dependências, mas não altera os arquivos do projeto.</span><span class="sxs-lookup"><span data-stu-id="01ff6-126">Also downloads and installs dependencies, but makes no changes to project files.</span></span><ul><li>[<span data-ttu-id="01ff6-127">comando install</span><span class="sxs-lookup"><span data-stu-id="01ff6-127">install command</span></span>](../tools/cli-ref-install.md)</li></ul> |

## <a name="general-install-process"></a><span data-ttu-id="01ff6-128">Processo de instalação geral</span><span class="sxs-lookup"><span data-stu-id="01ff6-128">General install process</span></span>

<span data-ttu-id="01ff6-129">Em geral, o NuGet faz o seguinte ao receber uma solicitação de instalação de um pacote:</span><span class="sxs-lookup"><span data-stu-id="01ff6-129">In general, NuGet does the following then asked to install a package:</span></span>

1. <span data-ttu-id="01ff6-130">Adquira o pacote:</span><span class="sxs-lookup"><span data-stu-id="01ff6-130">Acquire the package:</span></span>
    - <span data-ttu-id="01ff6-131">Verifique se o pacote solicitado já existe em um cache (veja [Gerenciar o cache do NuGet](managing-the-nuget-cache.md)).</span><span class="sxs-lookup"><span data-stu-id="01ff6-131">Check if the requested package already exists in a cache (see [Managing the NuGet cache](managing-the-nuget-cache.md)).</span></span>
    - <span data-ttu-id="01ff6-132">Se o pacote não estiver armazenado no cache, tente baixá-lo das fontes listadas nos [arquivos de configuração](Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="01ff6-132">If the package is not in the cache, attempt to download the package from the sources listed in the [configuration files](Configuring-NuGet-Behavior.md).</span></span>
      - <span data-ttu-id="01ff6-133">No caso dos projetos que usam o formato de referência `packages.config`, o NuGet usa a ordem das fontes na configuração.</span><span class="sxs-lookup"><span data-stu-id="01ff6-133">For projects using the `packages.config` reference format, NuGet uses the order of the sources in the configuration.</span></span>
      - <span data-ttu-id="01ff6-134">No caso dos projetos que usam o formato PackageReference, o NuGet verifica primeiro as fontes que estão em pastas locais, em seguida, verifica as fontes de compartilhamentos de rede e depois as fontes HTTP (Internet).</span><span class="sxs-lookup"><span data-stu-id="01ff6-134">For projects using the PackageReference format, NuGet checks sources that are local folders first, then checks sources on network shares, then checks HTTP (Internet) sources.</span></span>
      - <span data-ttu-id="01ff6-135">De modo geral, a ordem em que o NuGet verifica as fontes não é especialmente significativa, porque todos os pacotes fornecidos com um identificador e número de versão específicos são exatamente os mesmos em todas as fontes encontradas.</span><span class="sxs-lookup"><span data-stu-id="01ff6-135">In general, the order in which NuGet checks sources isn't particularly meaningful, because any given package with a specific identifier and version number is exactly the same on whatever source it's found.</span></span>
    - <span data-ttu-id="01ff6-136">Se o pacote for adquirido com êxito de uma das fontes, o NuGet o adicionará ao cache.</span><span class="sxs-lookup"><span data-stu-id="01ff6-136">If the package is successfully acquired from one of the sources, NuGet adds it to the cache.</span></span> <span data-ttu-id="01ff6-137">Caso contrário, a instalação falhará.</span><span class="sxs-lookup"><span data-stu-id="01ff6-137">Otherwise, installation fails.</span></span>

1. <span data-ttu-id="01ff6-138">Expanda o pacote no projeto.</span><span class="sxs-lookup"><span data-stu-id="01ff6-138">Expand the package into the project.</span></span>
    - <span data-ttu-id="01ff6-139">Expandir significa descompactar o conteúdo do pacote em uma subpasta apropriada.</span><span class="sxs-lookup"><span data-stu-id="01ff6-139">Expanding means unzipping the package's contents into an appropriate subfolder.</span></span> <span data-ttu-id="01ff6-140">Uma cópia do próprio `.nupkg` também é colocada na subpasta.</span><span class="sxs-lookup"><span data-stu-id="01ff6-140">A copy of the `.nupkg` itself is also placed in the subfolder.</span></span>
    - <span data-ttu-id="01ff6-141">Se o pacote estiver sendo instalado em um projeto do Visual Studio ou do .NET Core, somente os arquivos relevantes à estrutura de destino do projeto serão expandidos.</span><span class="sxs-lookup"><span data-stu-id="01ff6-141">If the package is being installed into a Visual Studio or .NET Core project, only the files relevant to the project's target framework are expanded.</span></span> <span data-ttu-id="01ff6-142">Quando é instalado usando a linha de comando do nuget.exe, ocorre a expansão de todos os assemblies.</span><span class="sxs-lookup"><span data-stu-id="01ff6-142">When installed using the nuget.exe command line, all assemblies are expanded.</span></span>

1. <span data-ttu-id="01ff6-143">Se o pacote for instalado no Visual Studio ou na CLI do dotnet, uma referência será adicionada ao arquivo de projeto apropriado (ou `packages.config` para alguns tipos de projeto no Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="01ff6-143">If the package is installed within Visual Studio or the dotnet CLI, a reference is added to the appropriate project file (or `packages.config` for some project types in Visual Studio).</span></span>

## <a name="related-topics"></a><span data-ttu-id="01ff6-144">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="01ff6-144">Related topics</span></span>

- [<span data-ttu-id="01ff6-145">Visão geral e fluxo de trabalho do consumo de pacote</span><span class="sxs-lookup"><span data-stu-id="01ff6-145">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="01ff6-146">Localizando e escolhendo pacotes</span><span class="sxs-lookup"><span data-stu-id="01ff6-146">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="01ff6-147">Configuração do comportamento de NuGet</span><span class="sxs-lookup"><span data-stu-id="01ff6-147">Configuring NuGet behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
- [<span data-ttu-id="01ff6-148">Gerenciamento do cache do NuGet</span><span class="sxs-lookup"><span data-stu-id="01ff6-148">Managing the NuGet cache</span></span>](managing-the-nuget-cache.md)