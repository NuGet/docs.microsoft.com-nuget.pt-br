---
title: Provedores de credenciais NuGet para Visual Studio
description: Autenticar os provedores de credenciais NuGet com feeds, Implementando a interface de IVsCredentialProvider em uma extensão do Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: e8d8ae22300b55b93badb65864163d959105dca2
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42793897"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="637d6-103">Autenticando feeds no Visual Studio com provedores de credenciais NuGet</span><span class="sxs-lookup"><span data-stu-id="637d6-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="637d6-104">A extensão do Studio Visual NuGet 3.6 + dá suporte a provedores de credenciais, que permitem que o NuGet trabalhar com feeds autenticados.</span><span class="sxs-lookup"><span data-stu-id="637d6-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="637d6-105">Depois de instalar um provedor de credenciais NuGet para Visual Studio, a extensão do NuGet Visual Studio automaticamente adquirirá e atualizar as credenciais para feeds autenticados conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="637d6-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="637d6-106">Uma implementação de exemplo pode ser encontrada no [o exemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="637d6-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="637d6-107">Começando com 4.8 + NuGet no Visual Studio oferece suporte os nova plataforma cruzada autenticação plug-ins, bem, mas eles não são a abordagem recomendada por motivos de desempenho.</span><span class="sxs-lookup"><span data-stu-id="637d6-107">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="637d6-108">Provedores de credenciais NuGet para Visual Studio deve ser instalados como uma extensão do Visual Studio regular e exigirá [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) ou superior.</span><span class="sxs-lookup"><span data-stu-id="637d6-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="637d6-109">Provedores de credenciais NuGet para Visual Studio funcionam somente no Visual Studio (não na restauração do dotnet ou nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="637d6-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="637d6-110">Para provedores de credenciais com nuget.exe, consulte [nuget.exe provedores de credenciais](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="637d6-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="637d6-111">Credencial provedores no dotnet e o msbuild consulte [NuGet cruzada plugins de plataforma](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="637d6-111">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="637d6-112">Provedores de credenciais NuGet disponíveis para o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="637d6-112">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="637d6-113">Há um provedor de credenciais incorporado a extensão do NuGet do Visual Studio para dar suporte ao Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="637d6-113">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="637d6-114">A extensão do NuGet Visual Studio usa interno `VsCredentialProviderImporter` que também examina de provedores de credenciais de plug-in.</span><span class="sxs-lookup"><span data-stu-id="637d6-114">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="637d6-115">Esses provedores de credenciais de plug-in devem ser detectáveis como uma exportação de MEF do tipo `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="637d6-115">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="637d6-116">Provedores de credenciais de plug-in disponíveis incluem:</span><span class="sxs-lookup"><span data-stu-id="637d6-116">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="637d6-117">Provedor de credenciais MyGet para Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="637d6-117">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="637d6-118">Criando um provedor de credenciais NuGet para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="637d6-118">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="637d6-119">A extensão do Studio Visual NuGet 3.6 + implementa um CredentialService interno que é usado para adquirir as credenciais.</span><span class="sxs-lookup"><span data-stu-id="637d6-119">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="637d6-120">O CredentialService tem uma lista de provedores de credenciais de plug-in e internos.</span><span class="sxs-lookup"><span data-stu-id="637d6-120">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="637d6-121">Cada provedor é tentada na sequência até que as credenciais são adquiridas.</span><span class="sxs-lookup"><span data-stu-id="637d6-121">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="637d6-122">Durante a aquisição de credencial, o serviço de credencial tentarão provedores de credenciais na seguinte ordem, parando assim que as credenciais são adquiridas:</span><span class="sxs-lookup"><span data-stu-id="637d6-122">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="637d6-123">As credenciais serão obtidas de arquivos de configuração do NuGet (usando o interno `SettingsCredentialProvider`).</span><span class="sxs-lookup"><span data-stu-id="637d6-123">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="637d6-124">Se a origem do pacote é no Visual Studio Team Services, o `VisualStudioAccountProvider` será usado.</span><span class="sxs-lookup"><span data-stu-id="637d6-124">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="637d6-125">Todos os outros plug-in Visual Studio provedores de credenciais serão tentadas sequencialmente.</span><span class="sxs-lookup"><span data-stu-id="637d6-125">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="637d6-126">Tente usar o NuGet todos entre provedores de credenciais de plataforma em sequência.</span><span class="sxs-lookup"><span data-stu-id="637d6-126">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="637d6-127">Se nenhuma credencial tiver sido adquirido, o usuário será solicitado para credenciais usando uma caixa de diálogo de autenticação básica padrão.</span><span class="sxs-lookup"><span data-stu-id="637d6-127">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="637d6-128">Implementando IVsCredentialProvider.GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="637d6-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="637d6-129">Para criar um provedor de credenciais NuGet para Visual Studio, crie uma extensão do Visual Studio que expõe uma pública exportação MEF que implementa o `IVsCredentialProvider` digite e segue os princípios descritos abaixo.</span><span class="sxs-lookup"><span data-stu-id="637d6-129">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="637d6-130">Uma implementação de exemplo pode ser encontrada no [o exemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="637d6-130">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="637d6-131">Cada provedor de credenciais NuGet para Visual Studio deve:</span><span class="sxs-lookup"><span data-stu-id="637d6-131">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="637d6-132">Determine se ele pode fornecer credenciais para o URI de destino antes de iniciar a aquisição de credencial.</span><span class="sxs-lookup"><span data-stu-id="637d6-132">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="637d6-133">Se o provedor não pode fornecer credenciais para a fonte de destino e, em seguida, ele deverá retornar `null`.</span><span class="sxs-lookup"><span data-stu-id="637d6-133">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="637d6-134">Se o provedor de manipular solicitações para o URI de destino, mas não é possível fornecer credenciais, uma exceção deve ser lançada.</span><span class="sxs-lookup"><span data-stu-id="637d6-134">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="637d6-135">Um provedor de credenciais personalizado do NuGet para Visual Studio deve implementar o `IVsCredentialProvider` interface disponível na [pacote do NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="637d6-135">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="637d6-136">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="637d6-136">GetCredentialAsync</span></span>

| <span data-ttu-id="637d6-137">Parâmetro de entrada</span><span class="sxs-lookup"><span data-stu-id="637d6-137">Input Parameter</span></span> |<span data-ttu-id="637d6-138">Descrição</span><span class="sxs-lookup"><span data-stu-id="637d6-138">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="637d6-139">URI de uri</span><span class="sxs-lookup"><span data-stu-id="637d6-139">Uri uri</span></span> | <span data-ttu-id="637d6-140">O Uri de origem do pacote para os quais credenciais estão sendo solicitadas.</span><span class="sxs-lookup"><span data-stu-id="637d6-140">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="637d6-141">Proxy IWebProxy</span><span class="sxs-lookup"><span data-stu-id="637d6-141">IWebProxy proxy</span></span> | <span data-ttu-id="637d6-142">Proxy da Web para usar ao se comunicar na rede.</span><span class="sxs-lookup"><span data-stu-id="637d6-142">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="637d6-143">NULL se não houver nenhuma autenticação de proxy configurada.</span><span class="sxs-lookup"><span data-stu-id="637d6-143">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="637d6-144">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="637d6-144">bool isProxyRequest</span></span> | <span data-ttu-id="637d6-145">True se essa solicitação obter as credenciais de autenticação de proxy.</span><span class="sxs-lookup"><span data-stu-id="637d6-145">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="637d6-146">Se a implementação não é válida para adquirir as credenciais do proxy, null deve ser retornado.</span><span class="sxs-lookup"><span data-stu-id="637d6-146">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="637d6-147">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="637d6-147">bool isRetry</span></span> | <span data-ttu-id="637d6-148">True se as credenciais foram solicitadas anteriormente para esse Uri, mas as credenciais fornecidas não permitiu o acesso autorizado.</span><span class="sxs-lookup"><span data-stu-id="637d6-148">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="637d6-149">bool não interativa</span><span class="sxs-lookup"><span data-stu-id="637d6-149">bool nonInteractive</span></span> | <span data-ttu-id="637d6-150">Se for true, o provedor de credenciais deve Suprimir todos os prompts de usuário e usar valores padrão em vez disso.</span><span class="sxs-lookup"><span data-stu-id="637d6-150">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="637d6-151">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="637d6-151">CancellationToken cancellationToken</span></span> | <span data-ttu-id="637d6-152">Esse token de cancelamento deve ser verificada para determinar se as credenciais do solicitante de operação foi cancelada.</span><span class="sxs-lookup"><span data-stu-id="637d6-152">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="637d6-153">**Valor de retorno**: um objeto de credenciais que implementa o [ `System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span><span class="sxs-lookup"><span data-stu-id="637d6-153">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
