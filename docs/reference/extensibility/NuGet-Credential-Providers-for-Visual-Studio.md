---
title: Provedores de credenciais NuGet para Visual Studio
description: Os provedores de credenciais do NuGet são autenticados com feeds implementando a interface IVsCredentialProvider em uma extensão do Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: f324f1e27e0d718571525152fcf16b55b900dbaa
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777760"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>Autenticando feeds no Visual Studio com provedores de credenciais do NuGet

A extensão do NuGet do Visual Studio 3.6 + dá suporte a provedores de credenciais, que permitem que o NuGet funcione com feeds autenticados.
Depois de instalar um provedor de credenciais do NuGet para o Visual Studio, a extensão NuGet do Visual Studio adquirirá e atualizará automaticamente as credenciais para feeds autenticados, conforme necessário.

Uma implementação de exemplo pode ser encontrada no [exemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

No Visual Studio, o NuGet usa um interno `VsCredentialProviderImporter` que também verifica os provedores de credenciais de plug-in. Esses provedores de credenciais de plug-in devem ser detectáveis como uma exportação de MEF do tipo `IVsCredentialProvider` .

A partir do mais de 4.8, o NuGet no Visual Studio também dá suporte aos novos plug-ins de autenticação entre plataformas, mas eles não são a abordagem recomendada por motivos de desempenho.

> [!Note]
> Os provedores de credenciais do NuGet para Visual Studio devem ser instalados como uma extensão regular do Visual Studio e exigirão o [visual studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) ou superior.
>
> Os provedores de credenciais do NuGet para o Visual Studio funcionam apenas no Visual Studio (não em dotnet restore ou nuget.exe). Para provedores de credenciais com nuget.exe, consulte [nuget.exe provedores de credenciais](nuget-exe-Credential-providers.md).
> Para provedores de credenciais no dotnet e MSBuild, consulte [plug-ins de plataforma cruzada do NuGet](nuget-cross-platform-authentication-plugin.md)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Criando um provedor de credenciais do NuGet para o Visual Studio

A extensão do NuGet do Visual Studio 3.6 + implementa um CredentialService interno que é usado para adquirir credenciais. O CredentialService tem uma lista de provedores de credenciais internos e de plug-in. Cada provedor é tentado sequencialmente até que as credenciais sejam adquiridas.

Durante a aquisição da credencial, o serviço de credenciais tentará provedores de credenciais na seguinte ordem, parando assim que as credenciais forem adquiridas:

1. As credenciais serão buscadas nos arquivos de configuração do NuGet (usando o interno `SettingsCredentialProvider` ).
1. Se a origem do pacote estiver em Visual Studio Team Services, o `VisualStudioAccountProvider` será usado.
1. Todos os outros provedores de credenciais de plug-in do Visual Studio serão tentados sequencialmente.
1. Tente usar todos os provedores de credenciais de plataforma cruzada do NuGet sequencialmente.
1. Se nenhuma credencial tiver sido adquirida ainda, o usuário será solicitado a fornecer credenciais usando uma caixa de diálogo de autenticação básica padrão.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>Implementando IVsCredentialProvider. GetCredentialsAsync

Para criar um provedor de credenciais do NuGet para o Visual Studio, crie uma extensão do Visual Studio que exponha uma exportação de MEF pública implementando o `IVsCredentialProvider` tipo e siga os princípios descritos abaixo.

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

Uma implementação de exemplo pode ser encontrada no [exemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

Cada provedor de credenciais do NuGet para Visual Studio deve:

1. Determine se ele pode fornecer credenciais para o URI de destino antes de iniciar a aquisição de credencial. Se o provedor não puder fornecer credenciais para a origem de destino, deverá retornar `null` .
1. Se o provedor processar solicitações para o URI de destino, mas não puder fornecer credenciais, uma exceção deverá ser lançada.

Um provedor de credenciais NuGet personalizado para o Visual Studio deve implementar a `IVsCredentialProvider` interface disponível no [pacote NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).

#### <a name="getcredentialasync"></a>GetCredentialAsync

| Parâmetro de entrada |Descrição|
| ----------------|-----------|
| URI do URI | O URI de origem do pacote para o qual as credenciais estão sendo solicitadas.|
| Proxy IWebProxy | Proxy Web a ser usado ao se comunicar na rede. NULL se não houver nenhuma autenticação de proxy configurada. |
| isProxyRequest bool | True se esta solicitação for obter credenciais de autenticação de proxy. Se a implementação não for válida para adquirir credenciais de proxy, NULL deverá ser retornado. |
| bool isrepetir | True se as credenciais tiverem sido solicitadas anteriormente para esse URI, mas as credenciais fornecidas não permitiram acesso autorizado. |
| bool não interativo | Se for true, o provedor de credenciais deverá suprimir todos os prompts de usuário e usar valores padrão em vez disso. |
| CancellationToken cancellationToken | Esse token de cancelamento deve ser verificado para determinar se a operação que solicita credenciais foi cancelada. |

**Valor de retorno**: um objeto de credenciais que implementa a [ `System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).
