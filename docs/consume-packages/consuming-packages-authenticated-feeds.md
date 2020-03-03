---
title: Consumindo pacotes de feeds autenticados
description: Consumindo pacotes de feeds autenticados em todos os cenários de cliente NuGet
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231787"
---
# <a name="consuming-packages-from-authenticated-feeds"></a><span data-ttu-id="6be65-103">Consumindo pacotes de feeds autenticados</span><span class="sxs-lookup"><span data-stu-id="6be65-103">Consuming packages from authenticated feeds</span></span>

<span data-ttu-id="6be65-104">Além do [feed público](https://api.nuget.org/v3/index.json)do NuGet.org, os clientes do NuGet têm a capacidade de interagir com feeds de arquivos e feeds http privados.</span><span class="sxs-lookup"><span data-stu-id="6be65-104">In addition to the nuget.org [public feed](https://api.nuget.org/v3/index.json), NuGet clients have the ability to interact with file feeds and private http feeds.</span></span>


<span data-ttu-id="6be65-105">Para autenticar com feeds http privados, as duas abordagens são:</span><span class="sxs-lookup"><span data-stu-id="6be65-105">To authenticate with private http feeds, the 2 approaches are:</span></span>

* <span data-ttu-id="6be65-106">Adicionar credenciais no [NuGet. config](../reference/nuget-config-file.md#packagesourcecredentials)</span><span class="sxs-lookup"><span data-stu-id="6be65-106">Add credentials in the [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span></span>
* <span data-ttu-id="6be65-107">Autentique usando um dos vários modelos de extensibilidade dependendo do cliente usado.</span><span class="sxs-lookup"><span data-stu-id="6be65-107">Authenticate using one of the many extensibility models depending on the client used.</span></span>

## <a name="nuget-clients-authentication-extensibility"></a><span data-ttu-id="6be65-108">Extensibilidade de autenticação dos clientes NuGet</span><span class="sxs-lookup"><span data-stu-id="6be65-108">NuGet clients' authentication extensibility</span></span>

<span data-ttu-id="6be65-109">Para os vários clientes NuGet, o próprio provedor de feed privado é responsável pela autenticação.</span><span class="sxs-lookup"><span data-stu-id="6be65-109">For the various NuGet clients, the private feed provider itself is responsible for authentication.</span></span>
<span data-ttu-id="6be65-110">Todos os clientes NuGet têm métodos de extensibilidade para dar suporte a isso.</span><span class="sxs-lookup"><span data-stu-id="6be65-110">All NuGet clients have extensibility methods to support this.</span></span> <span data-ttu-id="6be65-111">Elas são uma extensão do Visual Studio ou um plug-in que pode se comunicar com o NuGet para recuperar credenciais.</span><span class="sxs-lookup"><span data-stu-id="6be65-111">These are either a Visual Studio extension or a plugin that can communicate with NuGet to retrieve credentials.</span></span>

### <a name="visual-studio"></a><span data-ttu-id="6be65-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6be65-112">Visual Studio</span></span>

<span data-ttu-id="6be65-113">No Visual Studio, o NuGet expõe uma interface que os provedores de feed podem implementar e fornecer aos seus clientes.</span><span class="sxs-lookup"><span data-stu-id="6be65-113">In Visual Studio, NuGet exposes an interface that feed providers can implement and provide to their customers.</span></span> <span data-ttu-id="6be65-114">Para obter mais detalhes, consulte a documentação sobre [como criar um provedor de credenciais do Visual Studio](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span><span class="sxs-lookup"><span data-stu-id="6be65-114">For more details, please refer to the documentation on [how to create a Visual Studio credential provider](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span></span>

#### <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="6be65-115">Provedores de credenciais NuGet disponíveis para o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6be65-115">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="6be65-116">Há um provedor de credenciais interno do Visual Studio para dar suporte ao Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="6be65-116">There is a credential provider built into Visual Studio to support Azure DevOps.</span></span>


<span data-ttu-id="6be65-117">Os provedores de credenciais de plug-in disponíveis incluem:</span><span class="sxs-lookup"><span data-stu-id="6be65-117">Available plug-in credential providers include:</span></span>

* [<span data-ttu-id="6be65-118">Provedor de credenciais MyGet para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6be65-118">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a><span data-ttu-id="6be65-119">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="6be65-119">nuget.exe</span></span>

<span data-ttu-id="6be65-120">Quando `nuget.exe` precisa de credenciais para autenticar com um feed, ele o procura da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="6be65-120">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="6be65-121">Procure as credenciais em `NuGet.config` arquivos.</span><span class="sxs-lookup"><span data-stu-id="6be65-121">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="6be65-122">Usar provedores de credenciais de plug-in v2</span><span class="sxs-lookup"><span data-stu-id="6be65-122">Use V2 plug-in credential providers</span></span>
1. <span data-ttu-id="6be65-123">Usar provedores de credenciais de plug-in v1</span><span class="sxs-lookup"><span data-stu-id="6be65-123">Use V1 plug-in credential providers</span></span>
1. <span data-ttu-id="6be65-124">Em seguida, o NuGet solicita ao usuário as credenciais na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="6be65-124">NuGet then prompts the user for credentials on the command line.</span></span>

#### <a name="nugetexe-and-v2-credential-providers"></a><span data-ttu-id="6be65-125">provedores de credenciais NuGet. exe e v2</span><span class="sxs-lookup"><span data-stu-id="6be65-125">nuget.exe and V2 credential providers</span></span>

<span data-ttu-id="6be65-126">Na versão `4.8` o NuGet definiu um novo mecanismo de plug-in de autenticação, daqui em diante, chamado de provedores de credenciais v2.</span><span class="sxs-lookup"><span data-stu-id="6be65-126">In version `4.8` NuGet defined a new authentication plugin mechanism, hereafter referred to as V2 credential providers.</span></span>
<span data-ttu-id="6be65-127">Para a instalação e a descoberta desses provedores, consulte [plug-ins de plataforma cruzada do NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="6be65-127">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="nugetexe-and-v1-credential-providers"></a><span data-ttu-id="6be65-128">provedores de credenciais NuGet. exe e v1</span><span class="sxs-lookup"><span data-stu-id="6be65-128">nuget.exe and V1 credential providers</span></span>

<span data-ttu-id="6be65-129">Na versão `3.3` o NuGet introduziu a primeira versão dos plug-ins de autenticação.</span><span class="sxs-lookup"><span data-stu-id="6be65-129">In version `3.3` NuGet introduced the first version of authentication plugins.</span></span>
<span data-ttu-id="6be65-130">Para a instalação e a descoberta desses provedores, consulte [provedores de credenciais NuGet. exe](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span><span class="sxs-lookup"><span data-stu-id="6be65-130">For the installation and discovery of those providers refer to [nuget.exe credential providers](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span></span>

#### <a name="available-credential-providers-for-nugetexe"></a><span data-ttu-id="6be65-131">Provedores de credenciais disponíveis para NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="6be65-131">Available credential providers for nuget.exe</span></span>

* <span data-ttu-id="6be65-132">[Provedores de credenciais do Azure DevOps v2](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) ou [provedor de credenciais de Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)</span><span class="sxs-lookup"><span data-stu-id="6be65-132">[Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) or [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)</span></span>

<span data-ttu-id="6be65-133">Com o Visual Studio 2017 versão 15,9 e posterior, o provedor de credenciais do Azure DevOps é fornecido no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6be65-133">With Visual Studio 2017 version 15.9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span>
<span data-ttu-id="6be65-134">Se `nuget.exe` usar o MSBuild desse conjunto de ferramentas específico do Visual Studio, o plug-in será descoberto automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6be65-134">If `nuget.exe` uses MSBuild from that specific Visual Studio toolset, then the plugin will be discovered automatically.</span></span>

### <a name="dotnetexe"></a><span data-ttu-id="6be65-135">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="6be65-135">dotnet.exe</span></span>

<span data-ttu-id="6be65-136">Quando `dotnet.exe` precisa de credenciais para autenticar com um feed, ele o procura da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="6be65-136">When `dotnet.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="6be65-137">Procure as credenciais em `NuGet.config` arquivos.</span><span class="sxs-lookup"><span data-stu-id="6be65-137">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="6be65-138">Usar provedores de credenciais de plug-in v2</span><span class="sxs-lookup"><span data-stu-id="6be65-138">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="6be65-139">Por padrão `dotnet.exe` não é interativo, portanto, talvez seja necessário passar um sinalizador `--interactive` para que a ferramenta seja bloqueada para autenticação.</span><span class="sxs-lookup"><span data-stu-id="6be65-139">By default `dotnet.exe` is not interactive, so you might need to pass an `--interactive` flag to get the tool to block for authentication.</span></span>

#### <a name="dotnetexe-and-v2-credential-providers"></a><span data-ttu-id="6be65-140">provedores de credenciais dotnet. exe e v2</span><span class="sxs-lookup"><span data-stu-id="6be65-140">dotnet.exe and V2 credential providers</span></span>

<span data-ttu-id="6be65-141">Na versão `2.2.100` do SDK, o NuGet definiu um mecanismo de plug-in de autenticação que funciona em todos os clientes.</span><span class="sxs-lookup"><span data-stu-id="6be65-141">In version `2.2.100` of the SDK, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="6be65-142">Para a instalação e a descoberta desses provedores, consulte [plug-ins de plataforma cruzada do NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="6be65-142">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-dotnetexe"></a><span data-ttu-id="6be65-143">Provedores de credenciais disponíveis para dotnet. exe</span><span class="sxs-lookup"><span data-stu-id="6be65-143">Available credential providers for dotnet.exe</span></span>

* [<span data-ttu-id="6be65-144">Provedor de credenciais Azure Artifacts</span><span class="sxs-lookup"><span data-stu-id="6be65-144">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a><span data-ttu-id="6be65-145">MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="6be65-145">MSBuild.exe</span></span>

<span data-ttu-id="6be65-146">Quando `MSBuild.exe` precisa de credenciais para autenticar com um feed, ele o procura da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="6be65-146">When `MSBuild.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="6be65-147">Procurar credenciais em arquivos `NuGet.config`</span><span class="sxs-lookup"><span data-stu-id="6be65-147">Look for credentials in `NuGet.config` files</span></span>
1. <span data-ttu-id="6be65-148">Usar provedores de credenciais de plug-in v2</span><span class="sxs-lookup"><span data-stu-id="6be65-148">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="6be65-149">Por padrão `MSBuild.exe` não é interativo, portanto, talvez seja necessário definir a propriedade `/p:NuGetInteractive=true` para obter a ferramenta a ser bloqueada para autenticação.</span><span class="sxs-lookup"><span data-stu-id="6be65-149">By default `MSBuild.exe` is not interactive, so you might need to set the `/p:NuGetInteractive=true` property to get the tool to block for authentication.</span></span>

#### <a name="msbuildexe-and-v2-credential-providers"></a><span data-ttu-id="6be65-150">Provedores de credenciais do MSBuild. exe e v2</span><span class="sxs-lookup"><span data-stu-id="6be65-150">MSBuild.exe and V2 credential providers</span></span>

<span data-ttu-id="6be65-151">No Visual Studio 2019 atualização 9, o NuGet definiu um mecanismo de plug-in de autenticação que funciona em todos os clientes.</span><span class="sxs-lookup"><span data-stu-id="6be65-151">In Visual Studio 2019 Update 9, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="6be65-152">Para a instalação e a descoberta desses provedores, consulte [plug-ins de plataforma cruzada do NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="6be65-152">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-msbuildexe"></a><span data-ttu-id="6be65-153">Provedores de credenciais disponíveis para MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="6be65-153">Available credential providers for MSBuild.exe</span></span>

* [<span data-ttu-id="6be65-154">Provedor de credenciais Azure Artifacts</span><span class="sxs-lookup"><span data-stu-id="6be65-154">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

<span data-ttu-id="6be65-155">Com o Visual Studio 2017 atualização 9 e posterior, o provedor de credenciais do Azure DevOps é fornecido no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6be65-155">With Visual Studio 2017 Update 9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span> <span data-ttu-id="6be65-156">Nenhuma etapa adicional é necessária.</span><span class="sxs-lookup"><span data-stu-id="6be65-156">No additional steps are required.</span></span>
