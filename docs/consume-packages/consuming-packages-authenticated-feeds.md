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
# <a name="consuming-packages-from-authenticated-feeds"></a>Consumindo pacotes de feeds autenticados

Além do [feed público](https://api.nuget.org/v3/index.json)do NuGet.org, os clientes do NuGet têm a capacidade de interagir com feeds de arquivos e feeds http privados.


Para autenticar com feeds http privados, as duas abordagens são:

* Adicionar credenciais no [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)
* Autentique usando um dos vários modelos de extensibilidade dependendo do cliente usado.

## <a name="nuget-clients-authentication-extensibility"></a>Extensibilidade de autenticação dos clientes NuGet

Para os vários clientes NuGet, o próprio provedor de feed privado é responsável pela autenticação.
Todos os clientes NuGet têm métodos de extensibilidade para dar suporte a isso. Elas são uma extensão do Visual Studio ou um plug-in que pode se comunicar com o NuGet para recuperar credenciais.

### <a name="visual-studio"></a>Visual Studio

No Visual Studio, o NuGet expõe uma interface que os provedores de feed podem implementar e fornecer aos seus clientes. Para obter mais detalhes, consulte a documentação sobre [como criar um provedor de credenciais do Visual Studio](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).

#### <a name="available-nuget-credential-providers-for-visual-studio"></a>Provedores de credenciais NuGet disponíveis para o Visual Studio

Há um provedor de credenciais interno do Visual Studio para dar suporte ao Azure DevOps.


Os provedores de credenciais de plug-in disponíveis incluem:

* [Provedor de credenciais MyGet para Visual Studio](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a>nuget.exe

Quando `nuget.exe` o precisa de credenciais para autenticar com um feed, ele o procura da seguinte maneira:

1. Procure as credenciais nos `NuGet.config` arquivos.
1. Usar provedores de credenciais de plug-in v2
1. Usar provedores de credenciais de plug-in v1
1. Em seguida, o NuGet solicita ao usuário as credenciais na linha de comando.

#### <a name="nugetexe-and-v2-credential-providers"></a>Provedores de credenciais nuget.exe e v2

Na versão `4.8` , o NuGet definiu um novo mecanismo de plug-in de autenticação, daqui em diante, chamado de provedores de credenciais v2.
Para a instalação e a descoberta desses provedores, consulte [plug-ins de plataforma cruzada do NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="nugetexe-and-v1-credential-providers"></a>Provedores de credenciais nuget.exe e v1

Na versão, `3.3` o NuGet introduziu a primeira versão dos plug-ins de autenticação.
Para a instalação e a descoberta desses provedores, consulte [nuget.exe provedores de credenciais](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)

#### <a name="available-credential-providers-for-nugetexe"></a>Provedores de credenciais disponíveis para nuget.exe

* [Provedores de credenciais do Azure DevOps v2](/azure/devops/artifacts/nuget/nuget-exe#add-a-feed-to-nuget-482-or-later) ou [provedor de credenciais de Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)

Com o Visual Studio 2017 versão 15,9 e posterior, o provedor de credenciais do Azure DevOps é fornecido no Visual Studio.
Se `nuget.exe` o usar o MSBuild desse conjunto de ferramentas específico do Visual Studio, o plug-in será descoberto automaticamente.

### <a name="dotnetexe"></a>dotnet.exe

Quando `dotnet.exe` o precisa de credenciais para autenticar com um feed, ele o procura da seguinte maneira:

1. Procure as credenciais nos `NuGet.config` arquivos.
1. Usar provedores de credenciais de plug-in v2

Por padrão `dotnet.exe` , não é interativo, portanto, talvez seja necessário passar um `--interactive` sinalizador para que a ferramenta seja bloqueada para autenticação.

#### <a name="dotnetexe-and-v2-credential-providers"></a>Provedores de credenciais dotnet.exe e v2

Na versão `2.2.100` do SDK, o NuGet definiu um mecanismo de plug-in de autenticação que funciona em todos os clientes.
Para a instalação e a descoberta desses provedores, consulte [plug-ins de plataforma cruzada do NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-dotnetexe"></a>Provedores de credenciais disponíveis para dotnet.exe

* [Provedor de credenciais Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a>MSBuild.exe

Quando `MSBuild.exe` o precisa de credenciais para autenticar com um feed, ele o procura da seguinte maneira:

1. Procurar credenciais em `NuGet.config` arquivos
1. Usar provedores de credenciais de plug-in v2

Por padrão `MSBuild.exe` , não é interativo, portanto, talvez seja necessário definir a `/p:NuGetInteractive=true` propriedade para que a ferramenta seja bloqueada para autenticação.

#### <a name="msbuildexe-and-v2-credential-providers"></a>Provedores de credenciais MSBuild.exe e v2

No Visual Studio 2019 atualização 9, o NuGet definiu um mecanismo de plug-in de autenticação que funciona em todos os clientes.
Para a instalação e a descoberta desses provedores, consulte [plug-ins de plataforma cruzada do NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-msbuildexe"></a>Provedores de credenciais disponíveis para MSBuild.exe

* [Provedor de credenciais Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)

Com o Visual Studio 2017 atualização 9 e posterior, o provedor de credenciais do Azure DevOps é fornecido no Visual Studio. Nenhuma etapa adicional é necessária.
