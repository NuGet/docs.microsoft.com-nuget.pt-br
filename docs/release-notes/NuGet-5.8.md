---
title: Notas de versão do NuGet 5,8
description: Notas de versão do NuGet 5,8, incluindo novos recursos, correções de bugs e DCRs.
author: dominofire
ms.author: feaguila
ms.date: 11/9/2020
ms.topic: conceptual
ms.openlocfilehash: 86e173b9d760578454df8f5f817533f64e193996
ms.sourcegitcommit: 0cc6ac680c3202d0b036c0bed7910f6709215682
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/12/2020
ms.locfileid: "94550751"
---
# <a name="nuget-58-release-notes"></a>Notas de versão do NuGet 5,8

Veículos de distribuição do NuGet:

| Versão do NuGet | Disponível na versão do Visual Studio | Disponível em SDKs do .NET |
|:---|:---|:---|
| [**5.8**](https://nuget.org/downloads) | [Visual Studio 2019 versão 16,8](https://visualstudio.microsoft.com/downloads/) | [5,0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> instalado com o Visual Studio 2019 com carga de trabalho do .NET Core
  
> [!NOTE]
> O Visual Studio 16,8, o MSBuild 16,8 e o .NET 5,0 exigem NuGet.exe 5,8 ou posterior.


## <a name="summary-whats-new-in-58"></a>Resumo: o que há de novo no 5,8
🎉 **esta é a primeira versão a oferecer suporte completo e restauração para os pacotes NuGet destinados ao .net 5,0** 🎉

* Exibir detalhes da vulnerabilidade do pacote no painel de detalhes do pacote de interface do usuário do Gerenciador de pacotes- [#9850](https://github.com/NuGet/Home/issues/9850)

* Verificar pacotes NuGet assinados com o novo [`dotnet nuget verify`](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-verify) comando- [#8051](https://github.com/NuGet/Home/issues/8051)

* [`dotnet add package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples) dá suporte `--prerelease` à opção para adicionar a versão mais recente de um pacote, incluindo versões de pré-lançamento- [#4699](https://github.com/NuGet/Home/issues/4699)

* Pesquisar pacotes na CLI com [`nuget.exe search`](https://docs.microsoft.com/nuget/reference/cli-reference/cli-ref-search) [#9704](https://github.com/NuGet/Home/issues/9704) de comando

* [`dotnet list package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-list-package) o comando oferece suporte à `--verbosity` opção- [#9600](https://github.com/NuGet/Home/issues/9600)

* Habilitar a otimização de restauração rápida de No-Op para projetos com estilo csproj, PackageReference no Visual Studio- [#9565](https://github.com/NuGet/Home/issues/9565)

* As operações de interface do usuário do Gerenciador de pacotes de nível de solução, como instalações de pacotes e atualizações, são até 10 vezes mais rápidas- [#6010](https://github.com/NuGet/Home/issues/6010)

* Várias outras melhorias de desempenho do NuGet no Visual Studio – [#9982](https://github.com/NuGet/Home/issues/9982), [#9984](https://github.com/NuGet/Home/issues/9984), [#10052](https://github.com/NuGet/Home/issues/10052) [#9903](https://github.com/NuGet/Home/issues/9903)


### <a name="issues-fixed-in-this-release"></a>Problemas corrigidos nesta versão

**DCRs**

* .NET 5,0 TFM: regras de precedência de estrutura- [#9436](https://github.com/NuGet/Home/issues/9436)

* O NuGet não deve inferir a versão da plataforma de pontos ao analisar TargetFramework- [#9842](https://github.com/NuGet/Home/issues/9842)

* Use TargetFrameworkMoniker & TargetPlatformMoniker para inferir as estruturas em vez de usar TFI individuais, TFV, TPI, TPV Properties- [#9895](https://github.com/NuGet/Home/issues/9895)

* Atualização `GetReferenceNearestTargetFrameworkTask()` para dar suporte a estruturas de destino com plataformas (como NET 5.0-Windows)- [#9894](https://github.com/NuGet/Home/issues/9894)

* APIs do .NET 5,0 do Visual Studio- [#9650](https://github.com/NuGet/Home/issues/9650)

* Interface do usuário do Gerenciador de pacotes: as operações de consolidar ou atualizar pacotes não devem ser bloqueadas devido a erros (downgrade de pacote, etc.)- [#9224](https://github.com/NuGet/Home/issues/9224)

* Os recursos do NuGet devem se acender em projetos que têm a capacidade; "PackageReferences"- [#9957](https://github.com/NuGet/Home/issues/9957)

* Suprimir No-Op restaurar mensagens no Visual Studio – [#6384](https://github.com/NuGet/Home/issues/6384)

**Soluciona**

* O Construtor OutputWindowTextWriter não deve ser chamado no thread em segundo plano- [#9764](https://github.com/NuGet/Home/issues/9764)

* Restaurar pacotes assinados em CPUs big endian- [#9547](https://github.com/NuGet/Home/issues/9547)

* OutputConsoleLogger não deve chamar métodos relacionados em construtores de MEF- [#9591](https://github.com/NuGet/Home/issues/9591)

* Bug no método NuGet. CommandLine. console `PrintJustified()` - [#9737](https://github.com/NuGet/Home/issues/9737)

* Vazamento de memória da interface do usuário do Gerenciador de pacotes quando os metadados do pacote são coletados pelo lixo devido a um [#9757](https://github.com/NuGet/Home/issues/9757) de associação

* Sair Nenhum aviso é mostrado na Lista de Erros ao instalar um pacote assinado com o formato de packages.config na interface do usuário do Gerenciador de pacotes- [#9798](https://github.com/NuGet/Home/issues/9798)

* NuGet. CommandLine. XPlat não deve ter APIs públicas- [#9821](https://github.com/NuGet/Home/issues/9821)

* Reduzir a contenção de recursos no tempo de carregamento da solução causado pelo bloqueio de um thread de pool de threads com `BlockingCollection.Take()`  -  [#9822](https://github.com/NuGet/Home/issues/9822)

* Na restauração da linha de comando, com projetos de vários destinos, o NuGet deve ler as informações relacionadas à estrutura de destino da compilação interna- [#9869](https://github.com/NuGet/Home/issues/9869)

* Ler o grafo do identificador de tempo de execução por meio do TargetFrameworkInformation item- [#9874](https://github.com/NuGet/Home/issues/9874)

* A restauração estática do grafo é inconsistente com relação à propriedade CrossTargeting em comparação com o Visual Studio e a restauração de avaliação regular do MSBuild- [#9881](https://github.com/NuGet/Home/issues/9881)

* Na restauração estática de grafo, com projetos de vários destinos, o NuGet deve ler as informações relacionadas à estrutura de destino da compilação interna. - [#9870](https://github.com/NuGet/Home/issues/9870)

* Permitir que os `net5.0-platform` projetos sejam carregados e restaurados no Visual Studio- [#9863](https://github.com/NuGet/Home/issues/9863)

* Exibir a versão resolvida na interface do usuário do Gerenciador de pacotes- [#9826](https://github.com/NuGet/Home/issues/9826)

* Interface do usuário do Gerenciador de pacotes: Gerenciador de Soluções não está mostrando todas as dependências do pacote NuGet- [#9898](https://github.com/NuGet/Home/issues/9898)

* Atualizar a lista de licenças do SPDX- [#9946](https://github.com/NuGet/Home/issues/9946)

* VS 2019 falhas depois de abrir gerenciar pacotes NuGet: o ícone causa exceção sem tratamento no Image conversio- [#9696](https://github.com/NuGet/Home/issues/9696)

* NuGet. Packaging. Extraction precisa de ILMerge para excluir Newtonsoft.Js[#9966](https://github.com/NuGet/Home/issues/9966)

* O empacotamento com ContinuePackingAfterGeneratingNuspec = false não deve falhar quando não há erros- [#9786](https://github.com/NuGet/Home/issues/9786)

* Interface do usuário do Gerenciador de pacotes: os ícones não estão invertendo as cores corretamente- [#10017](https://github.com/NuGet/Home/issues/10017)

* Contagens de projeto incorretas para projetos atualizados e No-Op em Restore- [#10026](https://github.com/NuGet/Home/issues/10026)

* O uso `/p:RestoreUseStaticGraphEvaluation=true` de resultados em valor não pode ser nulo- [#9280](https://github.com/NuGet/Home/issues/9280)

* `dotnet pack` usa erroneamente o alias para projetos de biblioteca do WPF- [#10020](https://github.com/NuGet/Home/issues/10020)

* Interface do usuário do Gerenciador de pacotes: NullReferenceException quando a validação da assinatura falha- [#10042](https://github.com/NuGet/Home/issues/10042)

* Codespaces: não use o `object` tipo para os valores de metadados do projeto- [#10055](https://github.com/NuGet/Home/issues/10055)

* Codespaces: salvar as fontes de pacote nas opções de ferramentas substituirá as credenciais- [#9711](https://github.com/NuGet/Home/issues/9711)


**[Lista de todos os problemas corrigidos nesta versão-5,8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**

**[Lista de problemas/confirmações corrigidos nesta versão-5,8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**

### <a name="community-contributions"></a>Contribuições da comunidade

Obrigado a todos os colaboradores que ajudaram a tornar esta versão do NuGet incrível!

|Quem|PRs|Problemas|
|----|----|----|
[omajid](https://github.com/omajid) | [3437](https://github.com/NuGet/NuGet.Client/pull/3437) | Erros de digitação na mensagem de erro. "administrador" em vez de "administrador"- [#9662](https://github.com/NuGet/Home/issues/9662)
[odalet](https://github.com/odalet) | [3341](https://github.com/NuGet/NuGet.Client/pull/3341) | Pacote NuGet com relatórios AssemblyInformationalVersion inválidos "a descrição é necessária"- [#5548](https://github.com/NuGet/Home/issues/5548)
[campersau](https://github.com/campersau) | [3501](https://github.com/NuGet/NuGet.Client/pull/3501) | `RepositoryMetadata.Equals()` Não conta as propriedades Branch e commit- [#9613](https://github.com/NuGet/Home/issues/9613)
[Youssef1313](https://github.com/Youssef1313) | [3599](https://github.com/NuGet/NuGet.Client/pull/3599) | Clicar no código de nu no Visual Studio lista de erros janela deve ir para https://docs.microsoft.com/nuget/reference/errors-and-warnings/  -  [#9934](https://github.com/NuGet/Home/issues/9934)
[ChrisMaddock](https://github.com/ChrisMaddock) | [3624](https://github.com/NuGet/NuGet.Client/pull/3624) | Use ' https://' ao adicionar uma nova origem do pacote por meio de opções do Visual Studio- [#9974](https://github.com/NuGet/Home/issues/9974)
[Therzok](https://github.com/Therzok) | [3636](https://github.com/NuGet/NuGet.Client/pull/3636) | `RuntimeEnvironmentHelper.IsRunningOnVisualStudio` problema de desempenho em mono- [#9989](https://github.com/NuGet/Home/issues/9989)
[thomaslevesque](https://github.com/thomaslevesque) | [3442](https://github.com/NuGet/NuGet.Client/pull/3442) | Adicionar um TypeConverter para a classe SemanticVersion- [#9125](https://github.com/NuGet/Home/issues/9125)


## <a name="feedback-welcome"></a>Comentários de boas-vindas

Seus comentários são importantes para nós.  Se houver problemas com esta versão, verifique os problemas do [GitHub](https://github.com/NuGet/Home/issues) e a [comunidade de desenvolvedores do Visual Studio](https://developercommunity.visualstudio.com/) para obter os problemas existentes.  Para novos problemas no NuGet, informe um [problema do GitHub](hhttps://github.com/NuGet/Home/issues/new).
Para problemas gerais de experiência do NuGet, informe-nos por meio do [relatório uma opção de problema](https://docs.microsoft.com/visualstudio/ide/how-to-report-a-problem-with-visual-studio) encontrada em seu IDE favorito em **ajuda > relatar um problema**.
