---
title: Notas de versão do NuGet 5,5
description: Notas de versão do NuGet 5,5, incluindo novos recursos, correções de bugs e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2020
ms.topic: conceptual
ms.openlocfilehash: 0fde67dd03c31e986ed89f2f8627608e279ef908
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780113"
---
# <a name="nuget-55-release-notes"></a>Notas de versão do NuGet 5,5

Veículos de distribuição do NuGet:

| Versão do NuGet | Disponível na versão do Visual Studio| Disponível em SDKs do .NET|
|:---|:---|:---|
| [**5.5.0**](https://nuget.org/downloads) | [Visual Studio 2019 versão 16,5](https://visualstudio.microsoft.com/downloads/) | [3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> Instalado com o Visual Studio 2019 com carga de trabalho do .NET Core

## <a name="summary-whats-new-in-55"></a>Resumo: o que há de novo no 5,5

* Experiência aprimorada de acessibilidade e leitor de tela para a interface do usuário do Gerenciador de pacotes NuGet no Visual Studio
    * Problemas de acessibilidade nas experiências do leitor de tela, altText ausente e nome acessível para a caixa de texto instalada, etc.,- [#9059](https://github.com/NuGet/Home/issues/9059)
    * Problemas de acessibilidade nas experiências do leitor de tela na lista de pacotes- [#9077](https://github.com/NuGet/Home/issues/9077)
    * Problemas de acessibilidade nas experiências do leitor de tela relacionadas às guias "procurar", "instalar", "atualizar"- [#9078](https://github.com/NuGet/Home/issues/9078)
    * O Narrator não anuncia o rótulo de link "blank", "no Dependencies", "NuGet. org", "MIT" [#9157](https://github.com/NuGet/Home/issues/9157)

* Suporte para ícones independentes do identificando na interface do usuário do Gerenciador de pacotes do Visual Studio para pacotes hospedados em feeds locais- [#8189](https://github.com/NuGet/Home/issues/8189)

* Melhoria significativa do desempenho de restauração não operacional usando `RestoreUseStaticGraphEvaluation` o que acelera as avaliações chamando as APIs do grafo estático do MSBuild- [8791](https://github.com/NuGet/Home/issues/8791)

* Maior confiabilidade de dotnet.exe com plug-ins de autenticação entre plataformas
    * dotnet restore falha com TaskCanceledException- [#7842](https://github.com/NuGet/Home/issues/7842)
    * Plug-in: "uma tarefa foi cancelada"-problema com a autenticação ADO devido a isso. - [#8528](https://github.com/NuGet/Home/issues/8528)

* Adicionar `dotnet nuget <add|remove|update|disable|enable|list> source` [#4126](https://github.com/NuGet/Home/issues/4126) de comando

* Suporte para `--skip-duplicate` usar dotnet [#8778](https://github.com/NuGet/Home/issues/8778) do NuGet

* Suporte `packages.config` com MSBuild/Restore- [#8506](https://github.com/NuGet/Home/issues/8506)

### <a name="issues-fixed-in-this-release"></a>Problemas corrigidos nesta versão

**Bugs**

* Retrabalho Self-Updater com APIs v3- [#4197](https://github.com/NuGet/Home/issues/4197)

* Versão de dependência de pacote incorreta se a versão de dependência do pacote estiver definida como ' * '- [#6697](https://github.com/NuGet/Home/issues/6697)

* A mensagem de erro ErrorUnsafePackageEntry não está apontando para a origem do problema- [#7505](https://github.com/NuGet/Home/issues/7505)

* O arquivo de bloqueio não é respeitado nos cenários "*"- [#8073](https://github.com/NuGet/Home/issues/8073)

* NuGet.exe não é resolvido para a versão mais recente de um pacote ao usar * no PackageReference (MSBuild/dotnet/VS Restore do) – [#8432](https://github.com/NuGet/Home/issues/8432)

* pacote de lista dotnet com várias direcionamentos de projeto WPF- [#8463](https://github.com/NuGet/Home/issues/8463)

* Melhorar o ConcurrencyUtilities (reduzir o uso da CPU)- [#8653](https://github.com/NuGet/Home/issues/8653)

* A especificação de DG para cenários de projetos descarregados não deve ser escrita em restaurações de visualização- [#8793](https://github.com/NuGet/Home/issues/8793)

* Os pacotes NuGet do Visual Studio (RestoreManagerPackage) precisam ser carregados automaticamente em eventos de compilação de solução- [#8796](https://github.com/NuGet/Home/issues/8796)

* Deadlock em VSSettings Init- [#8842](https://github.com/NuGet/Home/issues/8842)

* A caixa de ferramentas do VisualStudio não será populada a partir de um pacote NuGet se um projeto for colocado em uma pasta de solução- [#8868](https://github.com/NuGet/Home/issues/8868)

* VS: a restauração da solução falha perpétua devido a uma condição de corrida- [#8881](https://github.com/NuGet/Home/issues/8881)

* Constante "carregando." na guia instalado e "pesquisando <term>.. "na guia Atualizações – [#8890](https://github.com/NuGet/Home/issues/8890)

* Ícones inseridos ausentes na interface do usuário do VS PM após o cache expirar- [#9069](https://github.com/NuGet/Home/issues/9069)

* Inicialização da interface do usuário do FireAndForget PM – [#9112](https://github.com/NuGet/Home/issues/9112)

* Restore: a implementação de IncludeExcludeFiles. Equals (...) está incorreta- [#9167](https://github.com/NuGet/Home/issues/9167)

* Restore: especificação. Clone () cria clones desiguais [#9211](https://github.com/NuGet/Home/issues/9211)

* Lista de erros mostrada embora "sempre mostrar Lista de Erros se a compilação for concluída com erros" não está marcada- [#8190](https://github.com/NuGet/Home/issues/8190)

* A restauração estática do grafo não deve passar SolutionPath vazio- [#9061](https://github.com/NuGet/Home/issues/9061)

* Restore: fechamento calculado para cada projeto 4 vezes- [#9042](https://github.com/NuGet/Home/issues/9042)

* Restore: DependencyGraphSpec. Load (...) não precisa de JObject- [#9040](https://github.com/NuGet/Home/issues/9040)

* Restore: cadeias de caracteres grandes criadas em LOH (Large Object heap)- [#9031](https://github.com/NuGet/Home/issues/9031)

* O nuget.exe personalizado no mono mais recente pode falhar devido ao resolvedor do MSBuild SDK- [8848](https://github.com/NuGet/Home/issues/8848)

* a restauração falha quando o nuget.dgspec.json é "usado por outro processo"- [8692](https://github.com/NuGet/Home/issues/8692)

**DCRs**

* A lógica no _GetRestoreProjectStyle deve estar em uma tarefa- [#8804](https://github.com/NuGet/Home/issues/8804)

* Adicionar informações de reprovação por padrão na guia instalada- [#8541](https://github.com/NuGet/Home/issues/8541)

**[Lista de todos os problemas corrigidos nesta versão-5,5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**
