---
title: Consumindo pacotes de feeds autenticados
description: Consumir pacotes de feeds autenticados em todos os cenários do cliente NuGet
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231787"
---
# <a name="consuming-packages-from-authenticated-feeds"></a><span data-ttu-id="07f2d-103">Consumindo pacotes de feeds autenticados</span><span class="sxs-lookup"><span data-stu-id="07f2d-103">Consuming packages from authenticated feeds</span></span>

<span data-ttu-id="07f2d-104">Além do feed [público](https://api.nuget.org/v3/index.json)nuget.org, os clientes NuGet têm a capacidade de interagir com feeds de arquivos e feeds http privados.</span><span class="sxs-lookup"><span data-stu-id="07f2d-104">In addition to the nuget.org [public feed](https://api.nuget.org/v3/index.json), NuGet clients have the ability to interact with file feeds and private http feeds.</span></span>


<span data-ttu-id="07f2d-105">Para autenticar com feeds http privados, as 2 abordagens são:</span><span class="sxs-lookup"><span data-stu-id="07f2d-105">To authenticate with private http feeds, the 2 approaches are:</span></span>

* <span data-ttu-id="07f2d-106">Adicionar credenciais no [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span><span class="sxs-lookup"><span data-stu-id="07f2d-106">Add credentials in the [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span></span>
* <span data-ttu-id="07f2d-107">Autenticar usando um dos muitos modelos de extensibilidade dependendo do cliente utilizado.</span><span class="sxs-lookup"><span data-stu-id="07f2d-107">Authenticate using one of the many extensibility models depending on the client used.</span></span>

## <a name="nuget-clients-authentication-extensibility"></a><span data-ttu-id="07f2d-108">Extensibilidade de autenticação dos clientes NuGet</span><span class="sxs-lookup"><span data-stu-id="07f2d-108">NuGet clients' authentication extensibility</span></span>

<span data-ttu-id="07f2d-109">Para os vários clientes NuGet, o próprio provedor de ração privada é responsável pela autenticação.</span><span class="sxs-lookup"><span data-stu-id="07f2d-109">For the various NuGet clients, the private feed provider itself is responsible for authentication.</span></span>
<span data-ttu-id="07f2d-110">Todos os clientes NuGet têm métodos de extensibilidade para suportar isso.</span><span class="sxs-lookup"><span data-stu-id="07f2d-110">All NuGet clients have extensibility methods to support this.</span></span> <span data-ttu-id="07f2d-111">Estes são uma extensão do Visual Studio ou um plugin que pode se comunicar com o NuGet para recuperar credenciais.</span><span class="sxs-lookup"><span data-stu-id="07f2d-111">These are either a Visual Studio extension or a plugin that can communicate with NuGet to retrieve credentials.</span></span>

### <a name="visual-studio"></a><span data-ttu-id="07f2d-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="07f2d-112">Visual Studio</span></span>

<span data-ttu-id="07f2d-113">No Visual Studio, o NuGet expõe uma interface que os provedores de feed podem implementar e fornecer aos seus clientes.</span><span class="sxs-lookup"><span data-stu-id="07f2d-113">In Visual Studio, NuGet exposes an interface that feed providers can implement and provide to their customers.</span></span> <span data-ttu-id="07f2d-114">Para obter mais detalhes, consulte a documentação sobre [como criar um provedor de credenciais do Visual Studio.](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md)</span><span class="sxs-lookup"><span data-stu-id="07f2d-114">For more details, please refer to the documentation on [how to create a Visual Studio credential provider](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span></span>

#### <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="07f2d-115">Provedores de credenciais NuGet disponíveis para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="07f2d-115">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="07f2d-116">Há um provedor de credenciais incorporado ao Visual Studio para suportar DevOps Azure.</span><span class="sxs-lookup"><span data-stu-id="07f2d-116">There is a credential provider built into Visual Studio to support Azure DevOps.</span></span>


<span data-ttu-id="07f2d-117">Os provedores de credenciais plug-in disponíveis incluem:</span><span class="sxs-lookup"><span data-stu-id="07f2d-117">Available plug-in credential providers include:</span></span>

* [<span data-ttu-id="07f2d-118">Provedor de credencial MyGet para visual studio</span><span class="sxs-lookup"><span data-stu-id="07f2d-118">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a><span data-ttu-id="07f2d-119">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="07f2d-119">nuget.exe</span></span>

<span data-ttu-id="07f2d-120">Quando `nuget.exe` precisa de credenciais para autenticar com um feed, ele procura por eles da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="07f2d-120">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="07f2d-121">Procure credenciais `NuGet.config` nos arquivos.</span><span class="sxs-lookup"><span data-stu-id="07f2d-121">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="07f2d-122">Use provedores de credenciais plug-in V2</span><span class="sxs-lookup"><span data-stu-id="07f2d-122">Use V2 plug-in credential providers</span></span>
1. <span data-ttu-id="07f2d-123">Use provedores de credenciais plug-in V1</span><span class="sxs-lookup"><span data-stu-id="07f2d-123">Use V1 plug-in credential providers</span></span>
1. <span data-ttu-id="07f2d-124">O NuGet solicita ao usuário credenciais na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="07f2d-124">NuGet then prompts the user for credentials on the command line.</span></span>

#### <a name="nugetexe-and-v2-credential-providers"></a><span data-ttu-id="07f2d-125">nuget.exe e V2 provedores de credenciais</span><span class="sxs-lookup"><span data-stu-id="07f2d-125">nuget.exe and V2 credential providers</span></span>

<span data-ttu-id="07f2d-126">Na `4.8` versão NuGet definiu um novo mecanismo de plugin de autenticação, doravante referido como provedores de credenciais V2.</span><span class="sxs-lookup"><span data-stu-id="07f2d-126">In version `4.8` NuGet defined a new authentication plugin mechanism, hereafter referred to as V2 credential providers.</span></span>
<span data-ttu-id="07f2d-127">Para a instalação e descoberta desses provedores, consulte [os plugins de plataforma cruzada NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="07f2d-127">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="nugetexe-and-v1-credential-providers"></a><span data-ttu-id="07f2d-128">nuget.exe e V1 provedores de credenciais</span><span class="sxs-lookup"><span data-stu-id="07f2d-128">nuget.exe and V1 credential providers</span></span>

<span data-ttu-id="07f2d-129">Na `3.3` versão NuGet introduziu a primeira versão de plugins de autenticação.</span><span class="sxs-lookup"><span data-stu-id="07f2d-129">In version `3.3` NuGet introduced the first version of authentication plugins.</span></span>
<span data-ttu-id="07f2d-130">Para a instalação e descoberta desses provedores, consulte [os provedores de credenciais nuget.exe](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span><span class="sxs-lookup"><span data-stu-id="07f2d-130">For the installation and discovery of those providers refer to [nuget.exe credential providers](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span></span>

#### <a name="available-credential-providers-for-nugetexe"></a><span data-ttu-id="07f2d-131">Provedores de credenciais disponíveis para nuget.exe</span><span class="sxs-lookup"><span data-stu-id="07f2d-131">Available credential providers for nuget.exe</span></span>

* <span data-ttu-id="07f2d-132">[Azure DevOps V2 Provedores de Credenciais](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) ou Provedor de [Credenciais de Artefatos Azure](https://github.com/microsoft/artifacts-credprovider)</span><span class="sxs-lookup"><span data-stu-id="07f2d-132">[Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) or [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)</span></span>

<span data-ttu-id="07f2d-133">Com visual studio 2017 versão 15.9 e posterior, o provedor de credenciais Azure DevOps é empacotado no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="07f2d-133">With Visual Studio 2017 version 15.9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span>
<span data-ttu-id="07f2d-134">Se `nuget.exe` usar o MSBuild a partir desse conjunto de ferramentas específicos do Visual Studio, o plugin será descoberto automaticamente.</span><span class="sxs-lookup"><span data-stu-id="07f2d-134">If `nuget.exe` uses MSBuild from that specific Visual Studio toolset, then the plugin will be discovered automatically.</span></span>

### <a name="dotnetexe"></a><span data-ttu-id="07f2d-135">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="07f2d-135">dotnet.exe</span></span>

<span data-ttu-id="07f2d-136">Quando `dotnet.exe` precisa de credenciais para autenticar com um feed, ele procura por eles da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="07f2d-136">When `dotnet.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="07f2d-137">Procure credenciais `NuGet.config` nos arquivos.</span><span class="sxs-lookup"><span data-stu-id="07f2d-137">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="07f2d-138">Use provedores de credenciais plug-in V2</span><span class="sxs-lookup"><span data-stu-id="07f2d-138">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="07f2d-139">Por `dotnet.exe` padrão não é interativo, então você `--interactive` pode precisar passar um sinalizador para obter a ferramenta para bloquear para autenticação.</span><span class="sxs-lookup"><span data-stu-id="07f2d-139">By default `dotnet.exe` is not interactive, so you might need to pass an `--interactive` flag to get the tool to block for authentication.</span></span>

#### <a name="dotnetexe-and-v2-credential-providers"></a><span data-ttu-id="07f2d-140">provedores de credenciais dotnet.exe e V2</span><span class="sxs-lookup"><span data-stu-id="07f2d-140">dotnet.exe and V2 credential providers</span></span>

<span data-ttu-id="07f2d-141">Na `2.2.100` versão do SDK, o NuGet definiu um mecanismo de plugin de autenticação que funciona em todos os clientes.</span><span class="sxs-lookup"><span data-stu-id="07f2d-141">In version `2.2.100` of the SDK, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="07f2d-142">Para a instalação e descoberta desses provedores, consulte [os plugins de plataforma cruzada NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="07f2d-142">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-dotnetexe"></a><span data-ttu-id="07f2d-143">Provedores de credenciais disponíveis para dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="07f2d-143">Available credential providers for dotnet.exe</span></span>

* [<span data-ttu-id="07f2d-144">Provedor de credenciais de artefatos azure</span><span class="sxs-lookup"><span data-stu-id="07f2d-144">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a><span data-ttu-id="07f2d-145">Msbuild.exe</span><span class="sxs-lookup"><span data-stu-id="07f2d-145">MSBuild.exe</span></span>

<span data-ttu-id="07f2d-146">Quando `MSBuild.exe` precisa de credenciais para autenticar com um feed, ele procura por eles da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="07f2d-146">When `MSBuild.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="07f2d-147">Procure credenciais `NuGet.config` em arquivos</span><span class="sxs-lookup"><span data-stu-id="07f2d-147">Look for credentials in `NuGet.config` files</span></span>
1. <span data-ttu-id="07f2d-148">Use provedores de credenciais plug-in V2</span><span class="sxs-lookup"><span data-stu-id="07f2d-148">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="07f2d-149">Por `MSBuild.exe` padrão não é interativo, então você `/p:NuGetInteractive=true` pode precisar definir a propriedade para obter a ferramenta para bloquear para autenticação.</span><span class="sxs-lookup"><span data-stu-id="07f2d-149">By default `MSBuild.exe` is not interactive, so you might need to set the `/p:NuGetInteractive=true` property to get the tool to block for authentication.</span></span>

#### <a name="msbuildexe-and-v2-credential-providers"></a><span data-ttu-id="07f2d-150">Provedores de credenciais MSBuild.exe e V2</span><span class="sxs-lookup"><span data-stu-id="07f2d-150">MSBuild.exe and V2 credential providers</span></span>

<span data-ttu-id="07f2d-151">No Visual Studio 2019 Update 9, o NuGet definiu um mecanismo de plugin de autenticação que funciona em todos os clientes.</span><span class="sxs-lookup"><span data-stu-id="07f2d-151">In Visual Studio 2019 Update 9, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="07f2d-152">Para a instalação e descoberta desses provedores, consulte [os plugins de plataforma cruzada NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="07f2d-152">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-msbuildexe"></a><span data-ttu-id="07f2d-153">Provedores de credenciais disponíveis para MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="07f2d-153">Available credential providers for MSBuild.exe</span></span>

* [<span data-ttu-id="07f2d-154">Provedor de credenciais de artefatos azure</span><span class="sxs-lookup"><span data-stu-id="07f2d-154">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

<span data-ttu-id="07f2d-155">Com o Visual Studio 2017 Update 9 e posterior, o provedor de credenciais Azure DevOps é empacotado no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="07f2d-155">With Visual Studio 2017 Update 9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span> <span data-ttu-id="07f2d-156">Não são necessárias etapas adicionais.</span><span class="sxs-lookup"><span data-stu-id="07f2d-156">No additional steps are required.</span></span>
