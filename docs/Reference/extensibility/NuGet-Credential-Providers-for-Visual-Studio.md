---
title: Provedores de credenciais do NuGet para Visual Studio | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 9c7f6d16-f437-47c4-82d4-6c996e0b18ec
description: "Provedores de credenciais do NuGet autenticar com feeds ao implementar a interface IVsCredentialProvider em uma extensão do Visual Studio."
keywords: "Provedores de credenciais do NuGet, autenticar com o feed, autenticar com o gallery, extensão do visual studio NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2b2fac23102865a08509acc1cc3d09f0cd375f26
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="f5362-104">Autenticando feeds no Visual Studio com provedores de credenciais do NuGet</span><span class="sxs-lookup"><span data-stu-id="f5362-104">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="f5362-105">O NuGet extensão do Visual Studio 3.6 + oferece suporte a provedores de credenciais, que permitem que o NuGet funcionar com feeds autenticados.</span><span class="sxs-lookup"><span data-stu-id="f5362-105">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="f5362-106">Depois de instalar um provedor de credenciais do NuGet para Visual Studio, a extensão do NuGet Visual Studio automaticamente adquirirá e atualizar as credenciais para feeds autenticados conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="f5362-106">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="f5362-107">Uma implementação de exemplo pode ser encontrada em [o exemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="f5362-107">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

> [!Note]
> <span data-ttu-id="f5362-108">Provedores de credenciais do NuGet para Visual Studio deve ser instalados como uma extensão do Visual Studio regular e exigirá [2017 do Visual Studio](https://aka.ms/vs/15/preview/vs_enterprise) (atualmente na visualização) ou superior.</span><span class="sxs-lookup"><span data-stu-id="f5362-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (currently in preview) or above.</span></span>
>
> <span data-ttu-id="f5362-109">Provedores de credenciais do NuGet para Visual Studio funcionam somente no Visual Studio (não na restauração dotnet ou nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="f5362-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="f5362-110">Para provedores de credenciais com nuget.exe, consulte [nuget.exe provedores de credenciais](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="f5362-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="f5362-111">Provedores de credencial disponíveis do NuGet para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f5362-111">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="f5362-112">Não há um provedor de credenciais incorporado a extensão do NuGet do Visual Studio para dar suporte ao Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="f5362-112">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="f5362-113">A extensão do NuGet Visual Studio usa interno `VsCredentialProviderImporter` que também procura os provedores de credenciais de plug-in.</span><span class="sxs-lookup"><span data-stu-id="f5362-113">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="f5362-114">Esses provedores de credencial de plug-in devem ser detectáveis como uma exportação MEF do tipo `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="f5362-114">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="f5362-115">Provedores de credencial de plug-in disponíveis incluem:</span><span class="sxs-lookup"><span data-stu-id="f5362-115">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="f5362-116">Provedor de credenciais MyGet para Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="f5362-116">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="f5362-117">Criando um provedor de credenciais do NuGet para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f5362-117">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="f5362-118">O NuGet extensão do Visual Studio 3.6 + implementa um CredentialService interno que é usado para adquirir credenciais.</span><span class="sxs-lookup"><span data-stu-id="f5362-118">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="f5362-119">O CredentialService tem uma lista de provedores de credenciais internos e plug-in.</span><span class="sxs-lookup"><span data-stu-id="f5362-119">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="f5362-120">Cada provedor é tentada sequencialmente, até que as credenciais são adquiridas.</span><span class="sxs-lookup"><span data-stu-id="f5362-120">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="f5362-121">Durante a aquisição de credencial, o serviço de credencial tentará provedores de credenciais na seguinte ordem, parando assim que as credenciais são adquiridas:</span><span class="sxs-lookup"><span data-stu-id="f5362-121">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="f5362-122">As credenciais serão obtidas de arquivos de configuração do NuGet (usando o interno `SettingsCredentialProvider`).</span><span class="sxs-lookup"><span data-stu-id="f5362-122">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="f5362-123">Se a origem do pacote é no Visual Studio Team Services, o `VisualStudioAccountProvider` será usado.</span><span class="sxs-lookup"><span data-stu-id="f5362-123">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="f5362-124">Todos os outros provedores de credencial de plug-in serão tentados sequencialmente.</span><span class="sxs-lookup"><span data-stu-id="f5362-124">All other plug-in credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="f5362-125">Se nenhuma credencial adquiriu, o usuário será solicitado para credenciais usando uma caixa de diálogo de autenticação básica padrão.</span><span class="sxs-lookup"><span data-stu-id="f5362-125">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="f5362-126">Implementando IVsCredentialProvider.GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="f5362-126">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="f5362-127">Para criar um provedor de credenciais do NuGet para Visual Studio, crie uma extensão do Visual Studio que expõe uma implementação exportação MEF pública a `IVsCredentialProvider` digite e obedece aos princípios descritos abaixo.</span><span class="sxs-lookup"><span data-stu-id="f5362-127">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="f5362-128">Uma implementação de exemplo pode ser encontrada em [o exemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="f5362-128">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="f5362-129">Cada provedor de credenciais do NuGet para Visual Studio deve:</span><span class="sxs-lookup"><span data-stu-id="f5362-129">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="f5362-130">Determine se ele pode fornecer credenciais para o URI de destino antes de iniciar a aquisição de credencial.</span><span class="sxs-lookup"><span data-stu-id="f5362-130">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="f5362-131">Se o provedor não pode fornecer credenciais para a fonte de destino, ele deverá retornar `null`.</span><span class="sxs-lookup"><span data-stu-id="f5362-131">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="f5362-132">Se o provedor de manipular solicitações para o URI de destino, mas não é possível fornecer credenciais, uma exceção deve ser gerada.</span><span class="sxs-lookup"><span data-stu-id="f5362-132">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="f5362-133">Um provedor de credenciais personalizado do NuGet para Visual Studio deve implementar o `IVsCredentialProvider` interface disponível no [pacote do NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="f5362-133">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="f5362-134">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="f5362-134">GetCredentialAsync</span></span>

| <span data-ttu-id="f5362-135">Parâmetro de entrada</span><span class="sxs-lookup"><span data-stu-id="f5362-135">Input Parameter</span></span> |<span data-ttu-id="f5362-136">Descrição</span><span class="sxs-lookup"><span data-stu-id="f5362-136">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="f5362-137">Uri de URI</span><span class="sxs-lookup"><span data-stu-id="f5362-137">Uri uri</span></span> | <span data-ttu-id="f5362-138">O Uri de origem do pacote para o qual as credenciais estão sendo solicitadas.</span><span class="sxs-lookup"><span data-stu-id="f5362-138">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="f5362-139">IWebProxy proxy</span><span class="sxs-lookup"><span data-stu-id="f5362-139">IWebProxy proxy</span></span> | <span data-ttu-id="f5362-140">Proxy da Web para usar ao se comunicar na rede.</span><span class="sxs-lookup"><span data-stu-id="f5362-140">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="f5362-141">NULL se não houver nenhuma autenticação de proxy configurada.</span><span class="sxs-lookup"><span data-stu-id="f5362-141">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="f5362-142">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="f5362-142">bool isProxyRequest</span></span> | <span data-ttu-id="f5362-143">True se essa solicitação obter as credenciais de autenticação de proxy.</span><span class="sxs-lookup"><span data-stu-id="f5362-143">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="f5362-144">Se a implementação não é válida para adquirir credenciais de proxy, null deve ser retornado.</span><span class="sxs-lookup"><span data-stu-id="f5362-144">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="f5362-145">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="f5362-145">bool isRetry</span></span> | <span data-ttu-id="f5362-146">True se as credenciais foram solicitadas anteriormente para esse Uri, mas as credenciais fornecidas não permitiu o acesso autorizado.</span><span class="sxs-lookup"><span data-stu-id="f5362-146">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="f5362-147">bool não interativo</span><span class="sxs-lookup"><span data-stu-id="f5362-147">bool nonInteractive</span></span> | <span data-ttu-id="f5362-148">Se for true, o provedor de credenciais deve Suprimir todos os prompts de usuário e usar valores padrão em vez disso.</span><span class="sxs-lookup"><span data-stu-id="f5362-148">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="f5362-149">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="f5362-149">CancellationToken cancellationToken</span></span> | <span data-ttu-id="f5362-150">Esse token de cancelamento deve ser verificada para determinar se as credenciais de solicitação de operação foi cancelada.</span><span class="sxs-lookup"><span data-stu-id="f5362-150">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |
  
<span data-ttu-id="f5362-151">**Valor de retorno**: um objeto de credenciais que implementa o [ `System.Net.ICredentials` interface](https://msdn.microsoft.com/library/system.net.icredentials.aspx).</span><span class="sxs-lookup"><span data-stu-id="f5362-151">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](https://msdn.microsoft.com/library/system.net.icredentials.aspx).</span></span>