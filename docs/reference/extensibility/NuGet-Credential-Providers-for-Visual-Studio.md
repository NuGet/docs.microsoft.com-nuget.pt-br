---
title: Provedores de credenciais do NuGet para Visual Studio
description: Provedores de credenciais do NuGet autenticar com feeds ao implementar a interface IVsCredentialProvider em uma extensão do Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: d4dbcab7c4005efcdc7efe96df3a70e666c558cc
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817827"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>Autenticando feeds no Visual Studio com provedores de credenciais do NuGet

O NuGet extensão do Visual Studio 3.6 + oferece suporte a provedores de credenciais, que permitem que o NuGet funcionar com feeds autenticados.
Depois de instalar um provedor de credenciais do NuGet para Visual Studio, a extensão do NuGet Visual Studio automaticamente adquirirá e atualizar as credenciais para feeds autenticados conforme necessário.

Uma implementação de exemplo pode ser encontrada em [o exemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

> [!Note]
> Provedores de credenciais do NuGet para Visual Studio deve ser instalados como uma extensão do Visual Studio regular e exigirá [2017 do Visual Studio](https://aka.ms/vs/15/preview/vs_enterprise) (atualmente na visualização) ou superior.
>
> Provedores de credenciais do NuGet para Visual Studio funcionam somente no Visual Studio (não na restauração dotnet ou nuget.exe). Para provedores de credenciais com nuget.exe, consulte [nuget.exe provedores de credenciais](nuget-exe-Credential-providers.md).

## <a name="available-nuget-credential-providers-for-visual-studio"></a>Provedores de credencial disponíveis do NuGet para Visual Studio

Não há um provedor de credenciais incorporado a extensão do NuGet do Visual Studio para dar suporte ao Visual Studio Team Services.

A extensão do NuGet Visual Studio usa interno `VsCredentialProviderImporter` que também procura os provedores de credenciais de plug-in. Esses provedores de credencial de plug-in devem ser detectáveis como uma exportação MEF do tipo `IVsCredentialProvider`.

Provedores de credencial de plug-in disponíveis incluem:

- [Provedor de credenciais MyGet para Visual Studio 2017](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Criando um provedor de credenciais do NuGet para Visual Studio

O NuGet extensão do Visual Studio 3.6 + implementa um CredentialService interno que é usado para adquirir credenciais. O CredentialService tem uma lista de provedores de credenciais internos e plug-in. Cada provedor é tentada sequencialmente, até que as credenciais são adquiridas.

Durante a aquisição de credencial, o serviço de credencial tentará provedores de credenciais na seguinte ordem, parando assim que as credenciais são adquiridas:

1. As credenciais serão obtidas de arquivos de configuração do NuGet (usando o interno `SettingsCredentialProvider`).
1. Se a origem do pacote é no Visual Studio Team Services, o `VisualStudioAccountProvider` será usado.
1. Todos os outros provedores de credencial de plug-in serão tentados sequencialmente.
1. Se nenhuma credencial adquiriu, o usuário será solicitado para credenciais usando uma caixa de diálogo de autenticação básica padrão.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>Implementando IVsCredentialProvider.GetCredentialsAsync

Para criar um provedor de credenciais do NuGet para Visual Studio, crie uma extensão do Visual Studio que expõe uma implementação exportação MEF pública a `IVsCredentialProvider` digite e obedece aos princípios descritos abaixo.

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

Uma implementação de exemplo pode ser encontrada em [o exemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

Cada provedor de credenciais do NuGet para Visual Studio deve:

1. Determine se ele pode fornecer credenciais para o URI de destino antes de iniciar a aquisição de credencial. Se o provedor não pode fornecer credenciais para a fonte de destino, ele deverá retornar `null`.
1. Se o provedor de manipular solicitações para o URI de destino, mas não é possível fornecer credenciais, uma exceção deve ser gerada.

Um provedor de credenciais personalizado do NuGet para Visual Studio deve implementar o `IVsCredentialProvider` interface disponível no [pacote do NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).

#### <a name="getcredentialasync"></a>GetCredentialAsync

| Parâmetro de entrada |Descrição|
| ----------------|-----------|
| Uri de URI | O Uri de origem do pacote para o qual as credenciais estão sendo solicitadas.|
| IWebProxy proxy | Proxy da Web para usar ao se comunicar na rede. NULL se não houver nenhuma autenticação de proxy configurada. |
| bool isProxyRequest | True se essa solicitação obter as credenciais de autenticação de proxy. Se a implementação não é válida para adquirir credenciais de proxy, null deve ser retornado. |
| bool isRetry | True se as credenciais foram solicitadas anteriormente para esse Uri, mas as credenciais fornecidas não permitiu o acesso autorizado. |
| bool não interativo | Se for true, o provedor de credenciais deve Suprimir todos os prompts de usuário e usar valores padrão em vez disso. |
| CancellationToken cancellationToken | Esse token de cancelamento deve ser verificada para determinar se as credenciais de solicitação de operação foi cancelada. |

**Valor de retorno**: um objeto de credenciais que implementa o [ `System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).
