---
title: Provedores de credenciais NuGet para Visual Studio
description: Os provedores de credenciais do NuGet são autenticados com feeds implementando a interface IVsCredentialProvider em uma extensão do Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 13b6f5abe93a17c809564265990f86f6780aa67e
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230805"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="67a67-103">Autenticando feeds no Visual Studio com provedores de credenciais do NuGet</span><span class="sxs-lookup"><span data-stu-id="67a67-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="67a67-104">A extensão do NuGet do Visual Studio 3.6 + dá suporte a provedores de credenciais, que permitem que o NuGet funcione com feeds autenticados.</span><span class="sxs-lookup"><span data-stu-id="67a67-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="67a67-105">Depois de instalar um provedor de credenciais do NuGet para o Visual Studio, a extensão NuGet do Visual Studio adquirirá e atualizará automaticamente as credenciais para feeds autenticados, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="67a67-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="67a67-106">Uma implementação de exemplo pode ser encontrada no [exemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="67a67-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="67a67-107">No Visual Studio, o NuGet usa um `VsCredentialProviderImporter` interno que também verifica os provedores de credenciais de plug-in.</span><span class="sxs-lookup"><span data-stu-id="67a67-107">Within Visual Studio, NuGet uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="67a67-108">Esses provedores de credenciais de plug-in devem ser detectáveis como uma exportação de MEF do tipo `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="67a67-108">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="67a67-109">A partir do mais de 4.8, o NuGet no Visual Studio também dá suporte aos novos plug-ins de autenticação entre plataformas, mas eles não são a abordagem recomendada por motivos de desempenho.</span><span class="sxs-lookup"><span data-stu-id="67a67-109">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="67a67-110">Os provedores de credenciais do NuGet para Visual Studio devem ser instalados como uma extensão regular do Visual Studio e exigirão o [visual studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) ou superior.</span><span class="sxs-lookup"><span data-stu-id="67a67-110">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="67a67-111">Os provedores de credenciais do NuGet para o Visual Studio funcionam apenas no Visual Studio (não no dotnet restore ou NuGet. exe).</span><span class="sxs-lookup"><span data-stu-id="67a67-111">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="67a67-112">Para provedores de credenciais com NuGet. exe, consulte [provedores de credenciais NuGet. exe](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="67a67-112">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="67a67-113">Para provedores de credenciais no dotnet e MSBuild, consulte [plug-ins de plataforma cruzada do NuGet](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="67a67-113">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="67a67-114">Criando um provedor de credenciais do NuGet para o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="67a67-114">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="67a67-115">A extensão do NuGet do Visual Studio 3.6 + implementa um CredentialService interno que é usado para adquirir credenciais.</span><span class="sxs-lookup"><span data-stu-id="67a67-115">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="67a67-116">O CredentialService tem uma lista de provedores de credenciais internos e de plug-in.</span><span class="sxs-lookup"><span data-stu-id="67a67-116">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="67a67-117">Cada provedor é tentado sequencialmente até que as credenciais sejam adquiridas.</span><span class="sxs-lookup"><span data-stu-id="67a67-117">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="67a67-118">Durante a aquisição da credencial, o serviço de credenciais tentará provedores de credenciais na seguinte ordem, parando assim que as credenciais forem adquiridas:</span><span class="sxs-lookup"><span data-stu-id="67a67-118">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="67a67-119">As credenciais serão buscadas nos arquivos de configuração do NuGet (usando o `SettingsCredentialProvider`interno).</span><span class="sxs-lookup"><span data-stu-id="67a67-119">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="67a67-120">Se a origem do pacote estiver em Visual Studio Team Services, o `VisualStudioAccountProvider` será usado.</span><span class="sxs-lookup"><span data-stu-id="67a67-120">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="67a67-121">Todos os outros provedores de credenciais de plug-in do Visual Studio serão tentados sequencialmente.</span><span class="sxs-lookup"><span data-stu-id="67a67-121">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="67a67-122">Tente usar todos os provedores de credenciais de plataforma cruzada do NuGet sequencialmente.</span><span class="sxs-lookup"><span data-stu-id="67a67-122">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="67a67-123">Se nenhuma credencial tiver sido adquirida ainda, o usuário será solicitado a fornecer credenciais usando uma caixa de diálogo de autenticação básica padrão.</span><span class="sxs-lookup"><span data-stu-id="67a67-123">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="67a67-124">Implementando IVsCredentialProvider. GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="67a67-124">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="67a67-125">Para criar um provedor de credenciais do NuGet para o Visual Studio, crie uma extensão do Visual Studio que exponha uma exportação de MEF pública implementando o tipo de `IVsCredentialProvider` e siga os princípios descritos abaixo.</span><span class="sxs-lookup"><span data-stu-id="67a67-125">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="67a67-126">Uma implementação de exemplo pode ser encontrada no [exemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="67a67-126">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="67a67-127">Cada provedor de credenciais do NuGet para Visual Studio deve:</span><span class="sxs-lookup"><span data-stu-id="67a67-127">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="67a67-128">Determine se ele pode fornecer credenciais para o URI de destino antes de iniciar a aquisição de credencial.</span><span class="sxs-lookup"><span data-stu-id="67a67-128">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="67a67-129">Se o provedor não puder fornecer credenciais para a origem de destino, ele deverá retornar `null`.</span><span class="sxs-lookup"><span data-stu-id="67a67-129">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="67a67-130">Se o provedor processar solicitações para o URI de destino, mas não puder fornecer credenciais, uma exceção deverá ser lançada.</span><span class="sxs-lookup"><span data-stu-id="67a67-130">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="67a67-131">Um provedor de credenciais NuGet personalizado para Visual Studio deve implementar a interface `IVsCredentialProvider` disponível no [pacote NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="67a67-131">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="67a67-132">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="67a67-132">GetCredentialAsync</span></span>

| <span data-ttu-id="67a67-133">Parâmetro de entrada</span><span class="sxs-lookup"><span data-stu-id="67a67-133">Input Parameter</span></span> |<span data-ttu-id="67a67-134">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="67a67-134">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="67a67-135">URI do URI</span><span class="sxs-lookup"><span data-stu-id="67a67-135">Uri uri</span></span> | <span data-ttu-id="67a67-136">O URI de origem do pacote para o qual as credenciais estão sendo solicitadas.</span><span class="sxs-lookup"><span data-stu-id="67a67-136">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="67a67-137">Proxy IWebProxy</span><span class="sxs-lookup"><span data-stu-id="67a67-137">IWebProxy proxy</span></span> | <span data-ttu-id="67a67-138">Proxy Web a ser usado ao se comunicar na rede.</span><span class="sxs-lookup"><span data-stu-id="67a67-138">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="67a67-139">NULL se não houver nenhuma autenticação de proxy configurada.</span><span class="sxs-lookup"><span data-stu-id="67a67-139">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="67a67-140">isProxyRequest bool</span><span class="sxs-lookup"><span data-stu-id="67a67-140">bool isProxyRequest</span></span> | <span data-ttu-id="67a67-141">True se esta solicitação for obter credenciais de autenticação de proxy.</span><span class="sxs-lookup"><span data-stu-id="67a67-141">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="67a67-142">Se a implementação não for válida para adquirir credenciais de proxy, NULL deverá ser retornado.</span><span class="sxs-lookup"><span data-stu-id="67a67-142">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="67a67-143">bool isrepetir</span><span class="sxs-lookup"><span data-stu-id="67a67-143">bool isRetry</span></span> | <span data-ttu-id="67a67-144">True se as credenciais tiverem sido solicitadas anteriormente para esse URI, mas as credenciais fornecidas não permitiram acesso autorizado.</span><span class="sxs-lookup"><span data-stu-id="67a67-144">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="67a67-145">bool não interativo</span><span class="sxs-lookup"><span data-stu-id="67a67-145">bool nonInteractive</span></span> | <span data-ttu-id="67a67-146">Se for true, o provedor de credenciais deverá suprimir todos os prompts de usuário e usar valores padrão em vez disso.</span><span class="sxs-lookup"><span data-stu-id="67a67-146">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="67a67-147">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="67a67-147">CancellationToken cancellationToken</span></span> | <span data-ttu-id="67a67-148">Esse token de cancelamento deve ser verificado para determinar se a operação que solicita credenciais foi cancelada.</span><span class="sxs-lookup"><span data-stu-id="67a67-148">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="67a67-149">**Valor de retorno**: um objeto de credenciais que implementa a [interface`System.Net.ICredentials`](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span><span class="sxs-lookup"><span data-stu-id="67a67-149">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
