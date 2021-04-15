---
title: Notas de versão do NuGet 5,7
description: Notas de versão do NuGet 5,7, incluindo novos recursos, correções de bugs e DCRs.
author: chgill-msft
ms.author: chgill
ms.date: 8/14/2020
ms.topic: conceptual
ms.openlocfilehash: 58ab481f0c6a6cb5549c269788170b8c3ff6002f
ms.sourcegitcommit: 1462f9f42ae36b3c990762ad4f02e38ab799ad09
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2021
ms.locfileid: "107508781"
---
# <a name="nuget-57-release-notes"></a>Notas de versão do NuGet 5,7

Veículos de distribuição do NuGet:

| Versão do NuGet | Disponível na versão do Visual Studio | Disponível em SDKs do .NET |
|:---|:---|:---|
| [**5.7.0**](https://nuget.org/downloads) | [Visual Studio 2019 versão 16,7](https://visualstudio.microsoft.com/downloads/) | [3.1.401](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |
| [**5.7.1**](https://nuget.org/downloads) | [Visual Studio 2019 versão 16,7](https://visualstudio.microsoft.com/downloads/) | [3.1.408](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> instalado com o Visual Studio 2019 com carga de trabalho do .NET Core

## <a name="summary-whats-new-in-57"></a>Resumo: o que há de novo no 5,7

### <a name="features-added-in-this-release"></a>Recursos adicionados nesta versão

* Adicionado suporte de alias externo para referências de pacote NuGet- [#4989](https://github.com/NuGet/Home/issues/4989)

* Fez a alternância entre as guias installed e updates mais rápido, permitindo que eles compartilhem uma fonte de dados e reduzindo o resfreshing- [#8294](https://github.com/NuGet/Home/issues/8294)

* Tornar a restauração mais rápida-acelerar avaliações chamando APIs de grafo estático do MSBuild (dotnet.exe)- [#9644](https://github.com/NuGet/Home/issues/9644)

* Adição de restauração parcial do Visual Studio para projetos PackageReference (no-op + +)- [#9513](https://github.com/NuGet/Home/issues/9513)

* A interface do usuário do Gerenciador de pacotes do Visual Studio falhará com menos frequência ao pesquisar origens de pacotes com comportamento inadequado que retornem mais do que o número solicitado de resultados por solicitação HTTP. - [#8478](https://github.com/NuGet/Home/issues/8478)

* Adicionada a integração das informações de PackageVersion para projetos de estilo não-SDK no VS Restore- [#9236](https://github.com/NuGet/Home/issues/9236)

* Suporte adicionado para atualização de nuget.exe `-self -Source` https://feed  -  [#1783](https://github.com/NuGet/Home/issues/1783)

* Suporte adicionado para vários arquivos de configuração no%APPDATA%\NuGet Directory- [#9394](https://github.com/NuGet/Home/issues/9394)

* O DeterministicSourcePaths agora usa pacotes de origem do NuGet em [#9431](https://github.com/NuGet/Home/issues/9431) de conta

* INuGetProjectService. GetInstalledPackagesAsync API de extensibilidade adicionada- [#9702](https://github.com/NuGet/Home/issues/9702)

* API de interoperabilidade adicionada para enumerar pastas de fallback sem exigir uma solução/projeto- [#9395](https://github.com/NuGet/Home/issues/9395)

* `latest`Opção adicionada para `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)

### <a name="issues-fixed-in-this-release"></a>Problemas corrigidos nesta versão

**Soluciona**

* Em uma restauração de CLI dotnet, ao iniciar plugins de credenciais, tente a CLI do dotnet no caminho do sistema se a `DOTNET_HOST_PATH`  variável de ambiente não estiver definida. - [#7438](https://github.com/NuGet/Home/issues/7438)

* nuget.exe spec gera uma marca de direitos autorais com texto embutido em código de Copyright aaaa em vez de `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)

* NuGet.exe gera a exceção ' autores necessários ' durante o pacote de um csproj ignorando espaços reservados e atributos AssemblyInfo se o nome do assembly for alterado- [#4234](https://github.com/NuGet/Home/issues/4234)

* HttpRequestMessage é reutilizado várias vezes, o que não é suportado com o SocketHttpHandler- [#8661](https://github.com/NuGet/Home/issues/8661)

* NuGet. Indexing 5.6.0 visualização 3 e posterior use um token de chave pública diferente- [#9481](https://github.com/NuGet/Home/issues/9481)

* Honrar TreatWarningsAsErrors durante a criação do pacote NuGet- [#7404](https://github.com/NuGet/Home/issues/7404)

* [CPVM] Downgrades de pacotes falsos para vários projetos P2P- [#9549](https://github.com/NuGet/Home/issues/9549)

* A guia "procurar" não está alinhada à esquerda com a caixa de pesquisa- [#9559](https://github.com/NuGet/Home/issues/9559)

* A versão instalada está inconsistente com o ícone inserido na interface do usuário do nível da solução PM para uma ID de pacote com várias versões instaladas- [#9321](https://github.com/NuGet/Home/issues/9321)

* Vazamento: PartCreationPolicy (CreationPolicy. nonshareed) NuGet. SolutionRestoreManager. RestoreOperationLogger- [#9595](https://github.com/NuGet/Home/issues/9595)

* Evite ler o arquivo de ativos em restaurações no-op- [#9693](https://github.com/NuGet/Home/issues/9693)

* O NuGet. Protocol não dá suporte à obtenção de uma contagem de download de versão do [#9086](https://github.com/NuGet/Home/issues/9086) de pesquisa

* Melhorar o desempenho de memória do PackageMetadataResourceV3 reduzindo as dependências de JObject- [#9719](https://github.com/NuGet/Home/issues/9719)

**Solicitações de alteração de design:**

* Suprimido o `<owners>` elemento quando ele é redundante- [#5134](https://github.com/NuGet/Home/issues/5134)

* Registrar IntervalTrackers como eventos ETW- [#9593](https://github.com/NuGet/Home/issues/9593)

* Adicionada uma mensagem informativa na restauração para informar aos usuários do CPVM que o recurso está em versão prévia- [#9340](https://github.com/NuGet/Home/issues/9340)

* Popule Gerenciador de Soluções dependências transitivas de pacote/projeto do arquivo de ativos- [#9580](https://github.com/NuGet/Home/issues/9580)

* A guia pacotes instalados não deve paginar a lista de pacotes- [#6995](https://github.com/NuGet/Home/issues/6995)

**[Lista de todos os problemas corrigidos nesta versão-5,7](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ea77f51ab1a972297db2e92)**

### <a name="community-contributions"></a>Contribuições da comunidade

Obrigado a todos os colaboradores que ajudaram a tornar esta versão do NuGet incrível!

|Quem|PRs|Problemas|
|----|----|----|
|[campersau](https://github.com/campersau)|[3433](https://github.com/NuGet/NuGet.Client/pull/3433), [3120](https://github.com/NuGet/NuGet.Client/pull/3120)|O NuGet. Protocol não dá suporte à obtenção de uma contagem de download de versão do [#9086](https://github.com/NuGet/Home/issues/9086) de pesquisa </br>HttpRequestMessage é reutilizado várias vezes, o que não é suportado com o SocketHttpHandler- [#8661](https://github.com/NuGet/Home/issues/8661)|
|[Joseph Musser (jnm2)](https://github.com/jnm2)|[3241](https://github.com/NuGet/NuGet.Client/pull/3241)|Suprimido o `<owners>` elemento quando ele é redundante- [#5134](https://github.com/NuGet/Home/issues/5134)|
|[Volodymyr Shkolka (BlackGad)](https://github.com/BlackGad)|[3273](https://github.com/NuGet/NuGet.Client/pull/3273)|O NuGet não pode restaurar de fontes HTTPS que exigem certificados de cliente- [#5773](https://github.com/NuGet/Home/issues/5773)|
|[Marius Ungureanu (Therzok)](https://github.com/Therzok)|[3357](https://github.com/NuGet/NuGet.Client/pull/3357)|[#9463](https://github.com/NuGet/Home/issues/9463) de verificação futura do HttpSourceAuthenticationHandler SemaphoreSlim|
|[Sunner (SuNNjek)](https://github.com/SuNNjek)|[3088](https://github.com/NuGet/NuGet.Client/pull/3088)|nuget.exe spec gera uma marca de direitos autorais com texto embutido em código de Copyright aaaa em vez de `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)|
|[Olivier Spinelli (olivier-spinelli)](https://github.com/olivier-spinelli)|[3335](https://github.com/NuGet/NuGet.Client/pull/3335)|Em uma restauração de CLI dotnet, ao iniciar plugins de credenciais, tente a CLI do dotnet no caminho do sistema se a `DOTNET_HOST_PATH`  variável de ambiente não estiver definida. - [#7438](https://github.com/NuGet/Home/issues/7438)|
|[goyzhang](https://github.com/goyzhang)|[3370](https://github.com/NuGet/NuGet.Client/pull/3370)|`latest`Opção adicionada para `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)|

## <a name="summary-whats-new-in-571"></a>Resumo: o que há de novo na 5.7.1

* Estenda o arquivo. nupkg. Metadata para incluir a fonte de instalação- [#10354](https://github.com/NuGet/Home/issues/10354)

* Registrar o pacote contenthash durante o log de restauração (durante a extração)- [#10384](https://github.com/NuGet/Home/issues/10384)

* Ao restaurar em detalhes normais, registre em qual fonte um pacote está sendo restaurado- [#10461](https://github.com/NuGet/Home/issues/10461)

**[Lista de todos os problemas corrigidos nesta versão-5.7.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f5724f84579cc29a79ee)**

**[Lista de confirmações nesta versão-5.7.1](https://github.com/NuGet/NuGet.Client/compare/80512866a2c127e52ce3e86fd803fff77e9b9b52...5.7.1.4)**
