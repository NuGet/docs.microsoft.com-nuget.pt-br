---
title: Consumindo pacotes de feeds autenticados
description: Consumir pacotes de feeds autenticados em todos os cenários do cliente NuGet
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231787"
---
# <a name="consuming-packages-from-authenticated-feeds"></a>Consumindo pacotes de feeds autenticados

Além do feed [público](https://api.nuget.org/v3/index.json)nuget.org, os clientes NuGet têm a capacidade de interagir com feeds de arquivos e feeds http privados.


Para autenticar com feeds http privados, as 2 abordagens são:

* Adicionar credenciais no [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)
* Autenticar usando um dos muitos modelos de extensibilidade dependendo do cliente utilizado.

## <a name="nuget-clients-authentication-extensibility"></a>Extensibilidade de autenticação dos clientes NuGet

Para os vários clientes NuGet, o próprio provedor de ração privada é responsável pela autenticação.
Todos os clientes NuGet têm métodos de extensibilidade para suportar isso. Estes são uma extensão do Visual Studio ou um plugin que pode se comunicar com o NuGet para recuperar credenciais.

### <a name="visual-studio"></a>Visual Studio

No Visual Studio, o NuGet expõe uma interface que os provedores de feed podem implementar e fornecer aos seus clientes. Para obter mais detalhes, consulte a documentação sobre [como criar um provedor de credenciais do Visual Studio.](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md)

#### <a name="available-nuget-credential-providers-for-visual-studio"></a>Provedores de credenciais NuGet disponíveis para Visual Studio

Há um provedor de credenciais incorporado ao Visual Studio para suportar DevOps Azure.


Os provedores de credenciais plug-in disponíveis incluem:

* [Provedor de credencial MyGet para visual studio](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a>nuget.exe

Quando `nuget.exe` precisa de credenciais para autenticar com um feed, ele procura por eles da seguinte maneira:

1. Procure credenciais `NuGet.config` nos arquivos.
1. Use provedores de credenciais plug-in V2
1. Use provedores de credenciais plug-in V1
1. O NuGet solicita ao usuário credenciais na linha de comando.

#### <a name="nugetexe-and-v2-credential-providers"></a>nuget.exe e V2 provedores de credenciais

Na `4.8` versão NuGet definiu um novo mecanismo de plugin de autenticação, doravante referido como provedores de credenciais V2.
Para a instalação e descoberta desses provedores, consulte [os plugins de plataforma cruzada NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="nugetexe-and-v1-credential-providers"></a>nuget.exe e V1 provedores de credenciais

Na `3.3` versão NuGet introduziu a primeira versão de plugins de autenticação.
Para a instalação e descoberta desses provedores, consulte [os provedores de credenciais nuget.exe](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)

#### <a name="available-credential-providers-for-nugetexe"></a>Provedores de credenciais disponíveis para nuget.exe

* [Azure DevOps V2 Provedores de Credenciais](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) ou Provedor de [Credenciais de Artefatos Azure](https://github.com/microsoft/artifacts-credprovider)

Com visual studio 2017 versão 15.9 e posterior, o provedor de credenciais Azure DevOps é empacotado no Visual Studio.
Se `nuget.exe` usar o MSBuild a partir desse conjunto de ferramentas específicos do Visual Studio, o plugin será descoberto automaticamente.

### <a name="dotnetexe"></a>dotnet.exe

Quando `dotnet.exe` precisa de credenciais para autenticar com um feed, ele procura por eles da seguinte maneira:

1. Procure credenciais `NuGet.config` nos arquivos.
1. Use provedores de credenciais plug-in V2

Por `dotnet.exe` padrão não é interativo, então você `--interactive` pode precisar passar um sinalizador para obter a ferramenta para bloquear para autenticação.

#### <a name="dotnetexe-and-v2-credential-providers"></a>provedores de credenciais dotnet.exe e V2

Na `2.2.100` versão do SDK, o NuGet definiu um mecanismo de plugin de autenticação que funciona em todos os clientes.
Para a instalação e descoberta desses provedores, consulte [os plugins de plataforma cruzada NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-dotnetexe"></a>Provedores de credenciais disponíveis para dotnet.exe

* [Provedor de credenciais de artefatos azure](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a>Msbuild.exe

Quando `MSBuild.exe` precisa de credenciais para autenticar com um feed, ele procura por eles da seguinte maneira:

1. Procure credenciais `NuGet.config` em arquivos
1. Use provedores de credenciais plug-in V2

Por `MSBuild.exe` padrão não é interativo, então você `/p:NuGetInteractive=true` pode precisar definir a propriedade para obter a ferramenta para bloquear para autenticação.

#### <a name="msbuildexe-and-v2-credential-providers"></a>Provedores de credenciais MSBuild.exe e V2

No Visual Studio 2019 Update 9, o NuGet definiu um mecanismo de plugin de autenticação que funciona em todos os clientes.
Para a instalação e descoberta desses provedores, consulte [os plugins de plataforma cruzada NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-msbuildexe"></a>Provedores de credenciais disponíveis para MSBuild.exe

* [Provedor de credenciais de artefatos azure](https://github.com/microsoft/artifacts-credprovider)

Com o Visual Studio 2017 Update 9 e posterior, o provedor de credenciais Azure DevOps é empacotado no Visual Studio. Não são necessárias etapas adicionais.
