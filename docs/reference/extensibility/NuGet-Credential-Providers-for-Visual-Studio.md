---
title: Provedores de credenciais NuGet para Visual Studio
description: Os provedores de credenciais do NuGet são autenticados com feeds implementando a interface IVsCredentialProvider em uma extensão do Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 906d07eb22599eb423b00300954ff2601dd33369
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383545"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="7c1db-103">Autenticando feeds no Visual Studio com provedores de credenciais do NuGet</span><span class="sxs-lookup"><span data-stu-id="7c1db-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="7c1db-104">A extensão do NuGet do Visual Studio 3.6 + dá suporte a provedores de credenciais, que permitem que o NuGet funcione com feeds autenticados.</span><span class="sxs-lookup"><span data-stu-id="7c1db-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="7c1db-105">Depois de instalar um provedor de credenciais do NuGet para o Visual Studio, a extensão NuGet do Visual Studio adquirirá e atualizará automaticamente as credenciais para feeds autenticados, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="7c1db-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="7c1db-106">Uma implementação de exemplo pode ser encontrada no [exemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="7c1db-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="7c1db-107">A partir do mais de 4.8, o NuGet no Visual Studio também dá suporte aos novos plug-ins de autenticação entre plataformas, mas eles não são a abordagem recomendada por motivos de desempenho.</span><span class="sxs-lookup"><span data-stu-id="7c1db-107">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="7c1db-108">Os provedores de credenciais do NuGet para Visual Studio devem ser instalados como uma extensão regular do Visual Studio e exigirão o [visual studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) ou superior.</span><span class="sxs-lookup"><span data-stu-id="7c1db-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="7c1db-109">Os provedores de credenciais do NuGet para o Visual Studio funcionam apenas no Visual Studio (não no dotnet restore ou NuGet. exe).</span><span class="sxs-lookup"><span data-stu-id="7c1db-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="7c1db-110">Para provedores de credenciais com NuGet. exe, consulte [provedores de credenciais NuGet. exe](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="7c1db-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="7c1db-111">Para provedores de credenciais no dotnet e MSBuild, consulte [plug-ins de plataforma cruzada do NuGet](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="7c1db-111">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="7c1db-112">Provedores de credenciais NuGet disponíveis para o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7c1db-112">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="7c1db-113">Há um provedor de credenciais embutido na extensão NuGet do Visual Studio para dar suporte a Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="7c1db-113">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="7c1db-114">A extensão NuGet do Visual Studio usa um `VsCredentialProviderImporter` interno que também verifica os provedores de credenciais de plug-in.</span><span class="sxs-lookup"><span data-stu-id="7c1db-114">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="7c1db-115">Esses provedores de credenciais de plug-in devem ser detectáveis como uma exportação de MEF do tipo `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="7c1db-115">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="7c1db-116">Os provedores de credenciais de plug-in disponíveis incluem:</span><span class="sxs-lookup"><span data-stu-id="7c1db-116">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="7c1db-117">Provedor de credenciais MyGet para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7c1db-117">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="7c1db-118">Criando um provedor de credenciais do NuGet para o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7c1db-118">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="7c1db-119">A extensão do NuGet do Visual Studio 3.6 + implementa um CredentialService interno que é usado para adquirir credenciais.</span><span class="sxs-lookup"><span data-stu-id="7c1db-119">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="7c1db-120">O CredentialService tem uma lista de provedores de credenciais internos e de plug-in.</span><span class="sxs-lookup"><span data-stu-id="7c1db-120">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="7c1db-121">Cada provedor é tentado sequencialmente até que as credenciais sejam adquiridas.</span><span class="sxs-lookup"><span data-stu-id="7c1db-121">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="7c1db-122">Durante a aquisição da credencial, o serviço de credenciais tentará provedores de credenciais na seguinte ordem, parando assim que as credenciais forem adquiridas:</span><span class="sxs-lookup"><span data-stu-id="7c1db-122">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="7c1db-123">As credenciais serão buscadas nos arquivos de configuração do NuGet (usando o `SettingsCredentialProvider`interno).</span><span class="sxs-lookup"><span data-stu-id="7c1db-123">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="7c1db-124">Se a origem do pacote estiver em Visual Studio Team Services, o `VisualStudioAccountProvider` será usado.</span><span class="sxs-lookup"><span data-stu-id="7c1db-124">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="7c1db-125">Todos os outros provedores de credenciais de plug-in do Visual Studio serão tentados sequencialmente.</span><span class="sxs-lookup"><span data-stu-id="7c1db-125">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="7c1db-126">Tente usar todos os provedores de credenciais de plataforma cruzada do NuGet sequencialmente.</span><span class="sxs-lookup"><span data-stu-id="7c1db-126">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="7c1db-127">Se nenhuma credencial tiver sido adquirida ainda, o usuário será solicitado a fornecer credenciais usando uma caixa de diálogo de autenticação básica padrão.</span><span class="sxs-lookup"><span data-stu-id="7c1db-127">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="7c1db-128">Implementando IVsCredentialProvider. GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="7c1db-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="7c1db-129">Para criar um provedor de credenciais do NuGet para o Visual Studio, crie uma extensão do Visual Studio que exponha uma exportação de MEF pública implementando o tipo de `IVsCredentialProvider` e siga os princípios descritos abaixo.</span><span class="sxs-lookup"><span data-stu-id="7c1db-129">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

```cs
public interface IVsCredentialProvider
{
    Task<ICredentials> GetCredentialsAsync(
        Uri uri,
        IWebProxy proxy,
        bool isProxyRequest,
        bool isRetry,
        bool nonInteractive,
        CancellationToken cancellationToken);
}
```

<span data-ttu-id="7c1db-130">Uma implementação de exemplo pode ser encontrada no [exemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="7c1db-130">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="7c1db-131">Cada provedor de credenciais do NuGet para Visual Studio deve:</span><span class="sxs-lookup"><span data-stu-id="7c1db-131">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="7c1db-132">Determine se ele pode fornecer credenciais para o URI de destino antes de iniciar a aquisição de credencial.</span><span class="sxs-lookup"><span data-stu-id="7c1db-132">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="7c1db-133">Se o provedor não puder fornecer credenciais para a origem de destino, ele deverá retornar `null`.</span><span class="sxs-lookup"><span data-stu-id="7c1db-133">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="7c1db-134">Se o provedor processar solicitações para o URI de destino, mas não puder fornecer credenciais, uma exceção deverá ser lançada.</span><span class="sxs-lookup"><span data-stu-id="7c1db-134">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="7c1db-135">Um provedor de credenciais NuGet personalizado para Visual Studio deve implementar a interface `IVsCredentialProvider` disponível no [pacote NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="7c1db-135">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="7c1db-136">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="7c1db-136">GetCredentialAsync</span></span>

| <span data-ttu-id="7c1db-137">Parâmetro de entrada</span><span class="sxs-lookup"><span data-stu-id="7c1db-137">Input Parameter</span></span> |<span data-ttu-id="7c1db-138">Descrição</span><span class="sxs-lookup"><span data-stu-id="7c1db-138">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="7c1db-139">URI do URI</span><span class="sxs-lookup"><span data-stu-id="7c1db-139">Uri uri</span></span> | <span data-ttu-id="7c1db-140">O URI de origem do pacote para o qual as credenciais estão sendo solicitadas.</span><span class="sxs-lookup"><span data-stu-id="7c1db-140">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="7c1db-141">Proxy IWebProxy</span><span class="sxs-lookup"><span data-stu-id="7c1db-141">IWebProxy proxy</span></span> | <span data-ttu-id="7c1db-142">Proxy Web a ser usado ao se comunicar na rede.</span><span class="sxs-lookup"><span data-stu-id="7c1db-142">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="7c1db-143">NULL se não houver nenhuma autenticação de proxy configurada.</span><span class="sxs-lookup"><span data-stu-id="7c1db-143">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="7c1db-144">isProxyRequest bool</span><span class="sxs-lookup"><span data-stu-id="7c1db-144">bool isProxyRequest</span></span> | <span data-ttu-id="7c1db-145">True se esta solicitação for obter credenciais de autenticação de proxy.</span><span class="sxs-lookup"><span data-stu-id="7c1db-145">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="7c1db-146">Se a implementação não for válida para adquirir credenciais de proxy, NULL deverá ser retornado.</span><span class="sxs-lookup"><span data-stu-id="7c1db-146">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="7c1db-147">bool isrepetir</span><span class="sxs-lookup"><span data-stu-id="7c1db-147">bool isRetry</span></span> | <span data-ttu-id="7c1db-148">True se as credenciais tiverem sido solicitadas anteriormente para esse URI, mas as credenciais fornecidas não permitiram acesso autorizado.</span><span class="sxs-lookup"><span data-stu-id="7c1db-148">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="7c1db-149">bool não interativo</span><span class="sxs-lookup"><span data-stu-id="7c1db-149">bool nonInteractive</span></span> | <span data-ttu-id="7c1db-150">Se for true, o provedor de credenciais deverá suprimir todos os prompts de usuário e usar valores padrão em vez disso.</span><span class="sxs-lookup"><span data-stu-id="7c1db-150">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="7c1db-151">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="7c1db-151">CancellationToken cancellationToken</span></span> | <span data-ttu-id="7c1db-152">Esse token de cancelamento deve ser verificado para determinar se a operação que solicita credenciais foi cancelada.</span><span class="sxs-lookup"><span data-stu-id="7c1db-152">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="7c1db-153">**Valor de retorno**: um objeto de credenciais que implementa a [interface`System.Net.ICredentials`](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span><span class="sxs-lookup"><span data-stu-id="7c1db-153">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
