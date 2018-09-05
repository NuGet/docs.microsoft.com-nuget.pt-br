---
title: Provedores de credenciais NuGet para Visual Studio
description: Autenticar os provedores de credenciais NuGet com feeds, Implementando a interface de IVsCredentialProvider em uma extensão do Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: abe009fee5863c55a188f4d7c71ed0924dd067ff
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547948"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>Autenticando feeds no Visual Studio com provedores de credenciais NuGet

A extensão do Studio Visual NuGet 3.6 + dá suporte a provedores de credenciais, que permitem que o NuGet trabalhar com feeds autenticados.
Depois de instalar um provedor de credenciais NuGet para Visual Studio, a extensão do NuGet Visual Studio automaticamente adquirirá e atualizar as credenciais para feeds autenticados conforme necessário.

Uma implementação de exemplo pode ser encontrada no [o exemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

Começando com 4.8 + NuGet no Visual Studio oferece suporte os nova plataforma cruzada autenticação plug-ins, bem, mas eles não são a abordagem recomendada por motivos de desempenho.

> [!Note]
> Provedores de credenciais NuGet para Visual Studio deve ser instalados como uma extensão do Visual Studio regular e exigirá [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) ou superior.
>
> Provedores de credenciais NuGet para Visual Studio funcionam somente no Visual Studio (não na restauração do dotnet ou nuget.exe). Para provedores de credenciais com nuget.exe, consulte [nuget.exe provedores de credenciais](nuget-exe-Credential-providers.md).
> Credencial provedores no dotnet e o msbuild consulte [NuGet cruzada plugins de plataforma](nuget-cross-platform-authentication-plugin.md)

## <a name="available-nuget-credential-providers-for-visual-studio"></a>Provedores de credenciais NuGet disponíveis para o Visual Studio

Há um provedor de credenciais incorporado a extensão do NuGet do Visual Studio para dar suporte ao Visual Studio Team Services.

A extensão do NuGet Visual Studio usa interno `VsCredentialProviderImporter` que também examina de provedores de credenciais de plug-in. Esses provedores de credenciais de plug-in devem ser detectáveis como uma exportação de MEF do tipo `IVsCredentialProvider`.

Provedores de credenciais de plug-in disponíveis incluem:

- [Provedor de credenciais MyGet para Visual Studio 2017](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Criando um provedor de credenciais NuGet para Visual Studio

A extensão do Studio Visual NuGet 3.6 + implementa um CredentialService interno que é usado para adquirir as credenciais. O CredentialService tem uma lista de provedores de credenciais de plug-in e internos. Cada provedor é tentada na sequência até que as credenciais são adquiridas.

Durante a aquisição de credencial, o serviço de credencial tentarão provedores de credenciais na seguinte ordem, parando assim que as credenciais são adquiridas:

1. As credenciais serão obtidas de arquivos de configuração do NuGet (usando o interno `SettingsCredentialProvider`).
1. Se a origem do pacote é no Visual Studio Team Services, o `VisualStudioAccountProvider` será usado.
1. Todos os outros plug-in Visual Studio provedores de credenciais serão tentadas sequencialmente.
1. Tente usar o NuGet todos entre provedores de credenciais de plataforma em sequência.
1. Se nenhuma credencial tiver sido adquirido, o usuário será solicitado para credenciais usando uma caixa de diálogo de autenticação básica padrão.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>Implementando IVsCredentialProvider.GetCredentialsAsync

Para criar um provedor de credenciais NuGet para Visual Studio, crie uma extensão do Visual Studio que expõe uma pública exportação MEF que implementa o `IVsCredentialProvider` digite e segue os princípios descritos abaixo.

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

Uma implementação de exemplo pode ser encontrada no [o exemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

Cada provedor de credenciais NuGet para Visual Studio deve:

1. Determine se ele pode fornecer credenciais para o URI de destino antes de iniciar a aquisição de credencial. Se o provedor não pode fornecer credenciais para a fonte de destino e, em seguida, ele deverá retornar `null`.
1. Se o provedor de manipular solicitações para o URI de destino, mas não é possível fornecer credenciais, uma exceção deve ser lançada.

Um provedor de credenciais personalizado do NuGet para Visual Studio deve implementar o `IVsCredentialProvider` interface disponível na [pacote do NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).

#### <a name="getcredentialasync"></a>GetCredentialAsync

| Parâmetro de entrada |Descrição|
| ----------------|-----------|
| URI de uri | O Uri de origem do pacote para os quais credenciais estão sendo solicitadas.|
| Proxy IWebProxy | Proxy da Web para usar ao se comunicar na rede. NULL se não houver nenhuma autenticação de proxy configurada. |
| bool isProxyRequest | True se essa solicitação obter as credenciais de autenticação de proxy. Se a implementação não é válida para adquirir as credenciais do proxy, null deve ser retornado. |
| bool isRetry | True se as credenciais foram solicitadas anteriormente para esse Uri, mas as credenciais fornecidas não permitiu o acesso autorizado. |
| bool não interativa | Se for true, o provedor de credenciais deve Suprimir todos os prompts de usuário e usar valores padrão em vez disso. |
| CancellationToken cancellationToken | Esse token de cancelamento deve ser verificada para determinar se as credenciais do solicitante de operação foi cancelada. |

**Valor de retorno**: um objeto de credenciais que implementa o [ `System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).
