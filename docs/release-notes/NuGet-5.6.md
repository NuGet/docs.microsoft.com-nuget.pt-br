---
title: Notas de versão do NuGet 5,6
description: Notas de versão do NuGet 5,6, incluindo novos recursos, correções de bugs e DCRs.
author: chgill-msft
ms.author: chgill
ms.date: 05/19/2020
ms.topic: conceptual
ms.openlocfilehash: e8d80a247da1cd18b53b35c51fb3d3dcf1cf68fa
ms.sourcegitcommit: 3529348ed394595d0fa01271486b831af9c97597
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/21/2020
ms.locfileid: "83727817"
---
# <a name="nuget-56-release-notes"></a>Notas de versão do NuGet 5,6

Veículos de distribuição do NuGet:

| Versão do NuGet | Disponível na versão do Visual Studio| Disponível em SDKs do .NET|
|:---|:---|:---|
| [**5.6.0**](https://nuget.org/downloads) | [Visual Studio 2019 versão 16,6](https://visualstudio.microsoft.com/downloads/) | [3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> Instalado com o Visual Studio 2019 com carga de trabalho do .NET Core

## <a name="summary-whats-new-in-56"></a>Resumo: o que há de novo no 5,6

* Suporte a pacotes de pré-lançamento com versões flutuantes. `Version="*-*"`, `Version="1.*-*"` e float semelhante às versões mais recentes, incluindo versões de pré-lançamento, dentro do intervalo especificado- [#912](https://github.com/NuGet/Home/issues/912)

### <a name="issues-fixed-in-this-release"></a>Problemas corrigidos nesta versão

**Soluciona**

* `nuget push *.nupkg`falha quando snupkg não existe- [#8148](https://github.com/NuGet/Home/issues/8148)

* Pack, e vários outros caminhos de código, falham dependendo da localidade. Usar RegexOptions. CultureInvariant- [#8246](https://github.com/NuGet/Home/issues/8246)

* Perf: a especificação de DG para cenários de projetos descarregados não deve ser escrita em restaurações de visualização- [#8793](https://github.com/NuGet/Home/issues/8793)

* Restauração: melhorar o desempenho ao armazenar em cache a especificação do grafo de dependência de solução- [#9201](https://github.com/NuGet/Home/issues/9201)

* A interface do usuário do PM não funciona para projetos de estilo do SDK após a instalação de um pacote com o console PM- [#9203](https://github.com/NuGet/Home/issues/9203)

* O ícone inserido não pode ser mostrado na interface do usuário do PM com feed de pacote local-dependendo de/vs \ [#9225](https://github.com/NuGet/Home/issues/9225)

* NuGetVersion. TryParseStrict () deverá retornar false se falhar ao analisar- [#9255](https://github.com/NuGet/Home/issues/9255)

* `nuget.exe push`ajuda para `-source` , deve sugerir o uso do nome de origem, não da URL de origem- [#9265](https://github.com/NuGet/Home/issues/9265)

* `dotnet nuget add package SourceUri`Cria um nome de origem de pacote padrão inválido- [#9277](https://github.com/NuGet/Home/issues/9277)

* O leitor de tela não anuncia "pesquisando..." mensagem ao alternar guias- [#9307](https://github.com/NuGet/Home/issues/9307)

* Acessibilidade: a cor do retângulo de foco não está acessível nas guias de interface do usuário do PM no tema escuro- [#9336](https://github.com/NuGet/Home/issues/9336)

* falha na restauração do NuGet. exe 5,5 com o MSBuild 14 ou inferior- [#9458](https://github.com/NuGet/Home/issues/9458)

* Não registrar horas de milissegundos em mensagens de restauração- [#8977](https://github.com/NuGet/Home/issues/8977)

* Tornar IOutputConsole Async- [#9268](https://github.com/NuGet/Home/issues/9268)

* A seleção de versão do MSBuild funciona mal em algumas culturas que não estão em inglês – [#9322](https://github.com/NuGet/Home/issues/9322)

* Padrão de formato ausente em `dotnet nuget list source`  -  [#9337](https://github.com/NuGet/Home/issues/9337)

* Perf: RestoreOperationLogger tem afinidade de thread desnecessária- [#9288](https://github.com/NuGet/Home/issues/9288)

* Criação automatizada de documentos para `dotnet nuget` comandos – [#9146](https://github.com/NuGet/Home/issues/9146)

* O detalhamento padrão não deve relatar a restauração de NOOP de cada projeto- [#8792](https://github.com/NuGet/Home/issues/8792)

* `-DependencyVersion`Parâmetro de suporte para `NuGet.exe update` , semelhante ao comando de instalação [#7694](https://github.com/NuGet/Home/issues/7694)


**DCRs**

* Adicionar suporte inicial à estrutura de destino do NET 5.0- [#9584](https://github.com/NuGet/Home/issues/9584)

* Classificar pacotes por ID na guia Atualizações da interface do usuário do PM- [#9278](https://github.com/NuGet/Home/issues/9278)


**[Lista de todos os problemas corrigidos nesta versão-5,6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**
