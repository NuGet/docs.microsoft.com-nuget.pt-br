---
title: Consumindo pacotes de feeds autenticados
description: Consumindo pacotes de feeds autenticados em todos os cenários de cliente NuGet
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: e76fefaf4d3c86aa15cf279090c0adb8ed779aab
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901506"
---
# <a name="consuming-packages-from-authenticated-feeds"></a><span data-ttu-id="e31b0-103">Consumindo pacotes de feeds autenticados</span><span class="sxs-lookup"><span data-stu-id="e31b0-103">Consuming packages from authenticated feeds</span></span>

<span data-ttu-id="e31b0-104">Além do [feed público](https://api.nuget.org/v3/index.json)do NuGet.org, os clientes do NuGet têm a capacidade de interagir com feeds de arquivos e feeds http privados.</span><span class="sxs-lookup"><span data-stu-id="e31b0-104">In addition to the nuget.org [public feed](https://api.nuget.org/v3/index.json), NuGet clients have the ability to interact with file feeds and private http feeds.</span></span>


<span data-ttu-id="e31b0-105">Para autenticar com feeds http privados, as duas abordagens são:</span><span class="sxs-lookup"><span data-stu-id="e31b0-105">To authenticate with private http feeds, the 2 approaches are:</span></span>

* <span data-ttu-id="e31b0-106">Adicionar credenciais no [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span><span class="sxs-lookup"><span data-stu-id="e31b0-106">Add credentials in the [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span></span>
* <span data-ttu-id="e31b0-107">Autentique usando um dos vários modelos de extensibilidade dependendo do cliente usado.</span><span class="sxs-lookup"><span data-stu-id="e31b0-107">Authenticate using one of the many extensibility models depending on the client used.</span></span>

## <a name="nuget-clients-authentication-extensibility"></a><span data-ttu-id="e31b0-108">Extensibilidade de autenticação dos clientes NuGet</span><span class="sxs-lookup"><span data-stu-id="e31b0-108">NuGet clients' authentication extensibility</span></span>

<span data-ttu-id="e31b0-109">Para os vários clientes NuGet, o próprio provedor de feed privado é responsável pela autenticação.</span><span class="sxs-lookup"><span data-stu-id="e31b0-109">For the various NuGet clients, the private feed provider itself is responsible for authentication.</span></span>
<span data-ttu-id="e31b0-110">Todos os clientes NuGet têm métodos de extensibilidade para dar suporte a isso.</span><span class="sxs-lookup"><span data-stu-id="e31b0-110">All NuGet clients have extensibility methods to support this.</span></span> <span data-ttu-id="e31b0-111">Elas são uma extensão do Visual Studio ou um plug-in que pode se comunicar com o NuGet para recuperar credenciais.</span><span class="sxs-lookup"><span data-stu-id="e31b0-111">These are either a Visual Studio extension or a plugin that can communicate with NuGet to retrieve credentials.</span></span>

### <a name="visual-studio"></a><span data-ttu-id="e31b0-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e31b0-112">Visual Studio</span></span>

<span data-ttu-id="e31b0-113">No Visual Studio, o NuGet expõe uma interface que os provedores de feed podem implementar e fornecer aos seus clientes.</span><span class="sxs-lookup"><span data-stu-id="e31b0-113">In Visual Studio, NuGet exposes an interface that feed providers can implement and provide to their customers.</span></span> <span data-ttu-id="e31b0-114">Para obter mais detalhes, consulte a documentação sobre [como criar um provedor de credenciais do Visual Studio](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span><span class="sxs-lookup"><span data-stu-id="e31b0-114">For more details, please refer to the documentation on [how to create a Visual Studio credential provider](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span></span>

#### <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="e31b0-115">Provedores de credenciais NuGet disponíveis para o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e31b0-115">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="e31b0-116">Há um provedor de credenciais interno do Visual Studio para dar suporte ao Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="e31b0-116">There is a credential provider built into Visual Studio to support Azure DevOps.</span></span>


<span data-ttu-id="e31b0-117">Os provedores de credenciais de plug-in disponíveis incluem:</span><span class="sxs-lookup"><span data-stu-id="e31b0-117">Available plug-in credential providers include:</span></span>

* [<span data-ttu-id="e31b0-118">Provedor de credenciais MyGet para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e31b0-118">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a><span data-ttu-id="e31b0-119">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="e31b0-119">nuget.exe</span></span>

<span data-ttu-id="e31b0-120">Quando `nuget.exe` o precisa de credenciais para autenticar com um feed, ele o procura da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e31b0-120">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="e31b0-121">Procure as credenciais nos `NuGet.config` arquivos.</span><span class="sxs-lookup"><span data-stu-id="e31b0-121">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="e31b0-122">Usar provedores de credenciais de plug-in v2</span><span class="sxs-lookup"><span data-stu-id="e31b0-122">Use V2 plug-in credential providers</span></span>
1. <span data-ttu-id="e31b0-123">Usar provedores de credenciais de plug-in v1</span><span class="sxs-lookup"><span data-stu-id="e31b0-123">Use V1 plug-in credential providers</span></span>
1. <span data-ttu-id="e31b0-124">Em seguida, o NuGet solicita ao usuário as credenciais na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="e31b0-124">NuGet then prompts the user for credentials on the command line.</span></span>

#### <a name="nugetexe-and-v2-credential-providers"></a><span data-ttu-id="e31b0-125">Provedores de credenciais nuget.exe e v2</span><span class="sxs-lookup"><span data-stu-id="e31b0-125">nuget.exe and V2 credential providers</span></span>

<span data-ttu-id="e31b0-126">Na versão `4.8` , o NuGet definiu um novo mecanismo de plug-in de autenticação, daqui em diante, chamado de provedores de credenciais v2.</span><span class="sxs-lookup"><span data-stu-id="e31b0-126">In version `4.8` NuGet defined a new authentication plugin mechanism, hereafter referred to as V2 credential providers.</span></span>
<span data-ttu-id="e31b0-127">Para a instalação e a descoberta desses provedores, consulte [plug-ins de plataforma cruzada do NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="e31b0-127">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="nugetexe-and-v1-credential-providers"></a><span data-ttu-id="e31b0-128">Provedores de credenciais nuget.exe e v1</span><span class="sxs-lookup"><span data-stu-id="e31b0-128">nuget.exe and V1 credential providers</span></span>

<span data-ttu-id="e31b0-129">Na versão, `3.3` o NuGet introduziu a primeira versão dos plug-ins de autenticação.</span><span class="sxs-lookup"><span data-stu-id="e31b0-129">In version `3.3` NuGet introduced the first version of authentication plugins.</span></span>
<span data-ttu-id="e31b0-130">Para a instalação e a descoberta desses provedores, consulte [nuget.exe provedores de credenciais](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span><span class="sxs-lookup"><span data-stu-id="e31b0-130">For the installation and discovery of those providers refer to [nuget.exe credential providers](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span></span>

#### <a name="available-credential-providers-for-nugetexe"></a><span data-ttu-id="e31b0-131">Provedores de credenciais disponíveis para nuget.exe</span><span class="sxs-lookup"><span data-stu-id="e31b0-131">Available credential providers for nuget.exe</span></span>

* <span data-ttu-id="e31b0-132">[Provedores de credenciais do Azure DevOps v2](/azure/devops/artifacts/nuget/nuget-exe#add-a-feed-to-nuget-482-or-later) ou [provedor de credenciais de Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)</span><span class="sxs-lookup"><span data-stu-id="e31b0-132">[Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe#add-a-feed-to-nuget-482-or-later) or [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)</span></span>

<span data-ttu-id="e31b0-133">Com o Visual Studio 2017 versão 15,9 e posterior, o provedor de credenciais do Azure DevOps é fornecido no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e31b0-133">With Visual Studio 2017 version 15.9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span>
<span data-ttu-id="e31b0-134">Se `nuget.exe` o usar o MSBuild desse conjunto de ferramentas específico do Visual Studio, o plug-in será descoberto automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e31b0-134">If `nuget.exe` uses MSBuild from that specific Visual Studio toolset, then the plugin will be discovered automatically.</span></span>

### <a name="dotnetexe"></a><span data-ttu-id="e31b0-135">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="e31b0-135">dotnet.exe</span></span>

<span data-ttu-id="e31b0-136">Quando `dotnet.exe` o precisa de credenciais para autenticar com um feed, ele o procura da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e31b0-136">When `dotnet.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="e31b0-137">Procure as credenciais nos `NuGet.config` arquivos.</span><span class="sxs-lookup"><span data-stu-id="e31b0-137">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="e31b0-138">Usar provedores de credenciais de plug-in v2</span><span class="sxs-lookup"><span data-stu-id="e31b0-138">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="e31b0-139">Por padrão `dotnet.exe` , não é interativo, portanto, talvez seja necessário passar um `--interactive` sinalizador para que a ferramenta seja bloqueada para autenticação.</span><span class="sxs-lookup"><span data-stu-id="e31b0-139">By default `dotnet.exe` is not interactive, so you might need to pass an `--interactive` flag to get the tool to block for authentication.</span></span>

#### <a name="dotnetexe-and-v2-credential-providers"></a><span data-ttu-id="e31b0-140">Provedores de credenciais dotnet.exe e v2</span><span class="sxs-lookup"><span data-stu-id="e31b0-140">dotnet.exe and V2 credential providers</span></span>

<span data-ttu-id="e31b0-141">Na versão `2.2.100` do SDK, o NuGet definiu um mecanismo de plug-in de autenticação que funciona em todos os clientes.</span><span class="sxs-lookup"><span data-stu-id="e31b0-141">In version `2.2.100` of the SDK, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="e31b0-142">Para a instalação e a descoberta desses provedores, consulte [plug-ins de plataforma cruzada do NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="e31b0-142">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-dotnetexe"></a><span data-ttu-id="e31b0-143">Provedores de credenciais disponíveis para dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="e31b0-143">Available credential providers for dotnet.exe</span></span>

* [<span data-ttu-id="e31b0-144">Provedor de credenciais Azure Artifacts</span><span class="sxs-lookup"><span data-stu-id="e31b0-144">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a><span data-ttu-id="e31b0-145">MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="e31b0-145">MSBuild.exe</span></span>

<span data-ttu-id="e31b0-146">Quando `MSBuild.exe` o precisa de credenciais para autenticar com um feed, ele o procura da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e31b0-146">When `MSBuild.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="e31b0-147">Procurar credenciais em `NuGet.config` arquivos</span><span class="sxs-lookup"><span data-stu-id="e31b0-147">Look for credentials in `NuGet.config` files</span></span>
1. <span data-ttu-id="e31b0-148">Usar provedores de credenciais de plug-in v2</span><span class="sxs-lookup"><span data-stu-id="e31b0-148">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="e31b0-149">Por padrão `MSBuild.exe` , não é interativo, portanto, talvez seja necessário definir a `/p:NuGetInteractive=true` propriedade para que a ferramenta seja bloqueada para autenticação.</span><span class="sxs-lookup"><span data-stu-id="e31b0-149">By default `MSBuild.exe` is not interactive, so you might need to set the `/p:NuGetInteractive=true` property to get the tool to block for authentication.</span></span>

#### <a name="msbuildexe-and-v2-credential-providers"></a><span data-ttu-id="e31b0-150">Provedores de credenciais MSBuild.exe e v2</span><span class="sxs-lookup"><span data-stu-id="e31b0-150">MSBuild.exe and V2 credential providers</span></span>

<span data-ttu-id="e31b0-151">No Visual Studio 2019 atualização 9, o NuGet definiu um mecanismo de plug-in de autenticação que funciona em todos os clientes.</span><span class="sxs-lookup"><span data-stu-id="e31b0-151">In Visual Studio 2019 Update 9, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="e31b0-152">Para a instalação e a descoberta desses provedores, consulte [plug-ins de plataforma cruzada do NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="e31b0-152">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-msbuildexe"></a><span data-ttu-id="e31b0-153">Provedores de credenciais disponíveis para MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="e31b0-153">Available credential providers for MSBuild.exe</span></span>

* [<span data-ttu-id="e31b0-154">Provedor de credenciais Azure Artifacts</span><span class="sxs-lookup"><span data-stu-id="e31b0-154">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

<span data-ttu-id="e31b0-155">Com o Visual Studio 2017 atualização 9 e posterior, o provedor de credenciais do Azure DevOps é fornecido no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e31b0-155">With Visual Studio 2017 Update 9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span> <span data-ttu-id="e31b0-156">Nenhuma etapa adicional é necessária.</span><span class="sxs-lookup"><span data-stu-id="e31b0-156">No additional steps are required.</span></span>
