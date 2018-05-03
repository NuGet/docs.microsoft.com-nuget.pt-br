---
title: Provedores de credenciais do NuGet para Visual Studio
description: Provedores de credenciais do NuGet autenticar com feeds ao implementar a interface IVsCredentialProvider em uma extensão do Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 740df87b0d663aac482d888e916662528ce27030
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="1f7ef-103">Autenticando feeds no Visual Studio com provedores de credenciais do NuGet</span><span class="sxs-lookup"><span data-stu-id="1f7ef-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="1f7ef-104">O NuGet extensão do Visual Studio 3.6 + oferece suporte a provedores de credenciais, que permitem que o NuGet funcionar com feeds autenticados.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="1f7ef-105">Depois de instalar um provedor de credenciais do NuGet para Visual Studio, a extensão do NuGet Visual Studio automaticamente adquirirá e atualizar as credenciais para feeds autenticados conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="1f7ef-106">Uma implementação de exemplo pode ser encontrada em [o exemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

> [!Note]
> <span data-ttu-id="1f7ef-107">Provedores de credenciais do NuGet para Visual Studio deve ser instalados como uma extensão do Visual Studio regular e exigirá [2017 do Visual Studio](https://aka.ms/vs/15/preview/vs_enterprise) (atualmente na visualização) ou superior.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-107">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (currently in preview) or above.</span></span>
>
> <span data-ttu-id="1f7ef-108">Provedores de credenciais do NuGet para Visual Studio funcionam somente no Visual Studio (não na restauração dotnet ou nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-108">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="1f7ef-109">Para provedores de credenciais com nuget.exe, consulte [nuget.exe provedores de credenciais](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-109">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="1f7ef-110">Provedores de credencial disponíveis do NuGet para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1f7ef-110">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="1f7ef-111">Não há um provedor de credenciais incorporado a extensão do NuGet do Visual Studio para dar suporte ao Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-111">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="1f7ef-112">A extensão do NuGet Visual Studio usa interno `VsCredentialProviderImporter` que também procura os provedores de credenciais de plug-in.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-112">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="1f7ef-113">Esses provedores de credencial de plug-in devem ser detectáveis como uma exportação MEF do tipo `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-113">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="1f7ef-114">Provedores de credencial de plug-in disponíveis incluem:</span><span class="sxs-lookup"><span data-stu-id="1f7ef-114">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="1f7ef-115">Provedor de credenciais MyGet para Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="1f7ef-115">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="1f7ef-116">Criando um provedor de credenciais do NuGet para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1f7ef-116">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="1f7ef-117">O NuGet extensão do Visual Studio 3.6 + implementa um CredentialService interno que é usado para adquirir credenciais.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-117">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="1f7ef-118">O CredentialService tem uma lista de provedores de credenciais internos e plug-in.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-118">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="1f7ef-119">Cada provedor é tentada sequencialmente, até que as credenciais são adquiridas.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-119">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="1f7ef-120">Durante a aquisição de credencial, o serviço de credencial tentará provedores de credenciais na seguinte ordem, parando assim que as credenciais são adquiridas:</span><span class="sxs-lookup"><span data-stu-id="1f7ef-120">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="1f7ef-121">As credenciais serão obtidas de arquivos de configuração do NuGet (usando o interno `SettingsCredentialProvider`).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-121">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="1f7ef-122">Se a origem do pacote é no Visual Studio Team Services, o `VisualStudioAccountProvider` será usado.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-122">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="1f7ef-123">Todos os outros provedores de credencial de plug-in serão tentados sequencialmente.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-123">All other plug-in credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="1f7ef-124">Se nenhuma credencial adquiriu, o usuário será solicitado para credenciais usando uma caixa de diálogo de autenticação básica padrão.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-124">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="1f7ef-125">Implementando IVsCredentialProvider.GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="1f7ef-125">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="1f7ef-126">Para criar um provedor de credenciais do NuGet para Visual Studio, crie uma extensão do Visual Studio que expõe uma implementação exportação MEF pública a `IVsCredentialProvider` digite e obedece aos princípios descritos abaixo.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-126">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="1f7ef-127">Uma implementação de exemplo pode ser encontrada em [o exemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-127">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="1f7ef-128">Cada provedor de credenciais do NuGet para Visual Studio deve:</span><span class="sxs-lookup"><span data-stu-id="1f7ef-128">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="1f7ef-129">Determine se ele pode fornecer credenciais para o URI de destino antes de iniciar a aquisição de credencial.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-129">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="1f7ef-130">Se o provedor não pode fornecer credenciais para a fonte de destino, ele deverá retornar `null`.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-130">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="1f7ef-131">Se o provedor de manipular solicitações para o URI de destino, mas não é possível fornecer credenciais, uma exceção deve ser gerada.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-131">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="1f7ef-132">Um provedor de credenciais personalizado do NuGet para Visual Studio deve implementar o `IVsCredentialProvider` interface disponível no [pacote do NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-132">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="1f7ef-133">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="1f7ef-133">GetCredentialAsync</span></span>

| <span data-ttu-id="1f7ef-134">Parâmetro de entrada</span><span class="sxs-lookup"><span data-stu-id="1f7ef-134">Input Parameter</span></span> |<span data-ttu-id="1f7ef-135">Descrição</span><span class="sxs-lookup"><span data-stu-id="1f7ef-135">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="1f7ef-136">Uri de URI</span><span class="sxs-lookup"><span data-stu-id="1f7ef-136">Uri uri</span></span> | <span data-ttu-id="1f7ef-137">O Uri de origem do pacote para o qual as credenciais estão sendo solicitadas.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-137">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="1f7ef-138">IWebProxy proxy</span><span class="sxs-lookup"><span data-stu-id="1f7ef-138">IWebProxy proxy</span></span> | <span data-ttu-id="1f7ef-139">Proxy da Web para usar ao se comunicar na rede.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-139">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="1f7ef-140">NULL se não houver nenhuma autenticação de proxy configurada.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-140">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="1f7ef-141">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="1f7ef-141">bool isProxyRequest</span></span> | <span data-ttu-id="1f7ef-142">True se essa solicitação obter as credenciais de autenticação de proxy.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-142">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="1f7ef-143">Se a implementação não é válida para adquirir credenciais de proxy, null deve ser retornado.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-143">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="1f7ef-144">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="1f7ef-144">bool isRetry</span></span> | <span data-ttu-id="1f7ef-145">True se as credenciais foram solicitadas anteriormente para esse Uri, mas as credenciais fornecidas não permitiu o acesso autorizado.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-145">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="1f7ef-146">bool não interativo</span><span class="sxs-lookup"><span data-stu-id="1f7ef-146">bool nonInteractive</span></span> | <span data-ttu-id="1f7ef-147">Se for true, o provedor de credenciais deve Suprimir todos os prompts de usuário e usar valores padrão em vez disso.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-147">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="1f7ef-148">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="1f7ef-148">CancellationToken cancellationToken</span></span> | <span data-ttu-id="1f7ef-149">Esse token de cancelamento deve ser verificada para determinar se as credenciais de solicitação de operação foi cancelada.</span><span class="sxs-lookup"><span data-stu-id="1f7ef-149">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="1f7ef-150">**Valor de retorno**: um objeto de credenciais que implementa o [ `System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span><span class="sxs-lookup"><span data-stu-id="1f7ef-150">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
