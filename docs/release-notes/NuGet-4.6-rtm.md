---
title: Notas de versão do NuGet 4.6 RTM
description: Notas de versão do NuGet 4.6.0, incluindo problemas conhecidos, correções de bugs, funcionalidades adicionadas e DCRs.
author: anangaur
ms.author: anangaur
ms.date: 3/7/2018
ms.topic: conceptual
ms.openlocfilehash: eacd29d4c9340a0f015fcdf6c5b9dd41bf781419
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64498679"
---
# <a name="nuget-46-release-notes"></a>Notas sobre a versão do NuGet 4.6

O [Visual Studio 2017 15.6 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) vem com o [NuGet 4.6.0](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe).

## <a name="summary-whats-new-in-460"></a>Resumo: O que há de novo em 4.6.0

* Adicionamos compatibilidade com [pacotes de assinatura](../create-packages/sign-a-package.md).
* O Visual Studio 2017 e o nuget.exe agora verificam a integridade do pacote antes de instalá-lo, restaurando os pacotes para [pacotes assinados](../reference/signed-packages-reference.md).
* Melhoramos o desempenho das restaurações sucessivas.

## <a name="summary-whats-new-in-463"></a>Resumo: O que há de novo em 4.6.3

* Correção de segurança: permissões em arquivos criados dentro ~/.nuget estão muito abertas [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-464"></a>Resumo: O que há de novo em 4.6.4

* Correção de segurança: arquivos dentro de NUPKGs podem ter um caminho relativo acima do diretório NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Problemas conhecidos

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problemas com o .NET Standard 2.0 com o .NET Framework & NuGet 

O .NET Standard e suas ferramentas foram projetados de modo que os projetos destinados ao .NET Framework 4.6.1 podem consumir pacotes do NuGet e projetos destinados ao .NET Standard 2.0 ou anterior. [Este documento](https://github.com/dotnet/standard/issues/481) resume os problemas desse cenário, o plano para lidar com eles e soluções alternativas que você pode implantar com o estado atual das ferramentas.

## <a name="top-issues-fixed-in-this-release"></a>Principais problemas corrigidos nesta versão

**Correções de desempenho**

* Não grave arquivos de ativo quando não houver alterações – [6491](https://github.com/NuGet/Home/issues/6491)
* A restauração provoca avaliações adicionais do MSBuild quando o TFM dos projetos filho não coincidem com o do projeto pai – [6311](https://github.com/NuGet/Home/issues/6311)
* Melhorar o desempenho da restauração NoOp otimizando a criação das especificações do grafo de dependência – [6252](https://github.com/NuGet/Home/issues/6252)

**Bugs**

* Efetuar push para a pasta local deixa nupkg bloqueado – [6325](https://github.com/NuGet/Home/issues/6325)
* Implementação do plug-in do NuGet: vários problemas – [6149](https://github.com/NuGet/Home/issues/6149)
* UIHang – remover chamada de serviço de consulta de inicialização do MEF no VSSolutionManager – [6110](https://github.com/NuGet/Home/issues/6110)
* Exceção de relatório de erro para tarefa cancelada de download de pacote – [6096](https://github.com/NuGet/Home/issues/6096)
* O NuGet.exe substitui '+' por '%2B' no nome do assembly – [5956](https://github.com/NuGet/Home/issues/5956)
* Fn + F1 não leva para a página de ajuda adequada da interface do usuário e do console do PM – [#5912](https://github.com/NuGet/Home/issues/5912)
* O VS NuGet grava caminhos absolutos em arquivos de projeto em circunstâncias específicas – [5888](https://github.com/NuGet/Home/issues/5888)
* Corrigir regressão 4.3 – os espaços reservados $product$ e $AssemblyGuid$ não são substituídos no contentfile por meio de transformação – [5880](https://github.com/NuGet/Home/issues/5880)
* Comando dotnet restore com falhas de várias fontes – [5817](https://github.com/NuGet/Home/issues/5817)
* O pacote deve reavaliar as versões do projeto para permitir o controle de versão do GIT – [4790](https://github.com/NuGet/Home/issues/4790)
* Melhorar bastante o entendimento dos erros ao instalar um pacote incompatível – [4555](https://github.com/NuGet/Home/issues/4555)
* O TemplateWizard precisa de uma opção para instalar os pacotes como PackageReferences – [4549](https://github.com/NuGet/Home/issues/4549)
* Arquivos de propriedades entregues no pacote ignorados quando o MSBuild.exe é executado de fora de um Prompt de Comando do Desenvolvedor – [4530](https://github.com/NuGet/Home/issues/4530)
* Corrigir mensagem de erro ao fazer referência à Biblioteca do .NET Standard não aplicável ao projeto – [4423](https://github.com/NuGet/Home/issues/4423)
* Falha no comando dotnet add package para perfil portável de direcionamento de pacote com poucas diretrizes – [4349](https://github.com/NuGet/Home/issues/4349)
* dotnet pack – sufixo de versão ausente de ProjectReference – [4337](https://github.com/NuGet/Home/issues/4337)
* Erros de build e falha do VS com o modelo do .NET Core – [3973](https://github.com/NuGet/Home/issues/3973)
* Não é possível carregar o índice de serviço do https de origem:* – [3681](https://github.com/NuGet/Home/issues/3681)
* Lista do nuget.exe -allversions não funciona – [3441](https://github.com/NuGet/Home/issues/3441)
* Mensagem de erro de resolução de dependência enganosa – [2984](https://github.com/NuGet/Home/issues/2984)
* A restauração do nuget.exe não produz arquivos .props nem .targets para .msbuildproj (regressão a atualização v3.3.0-3.4.4) – [2921](https://github.com/NuGet/Home/issues/2921)
* Atraso da interface do usuário ao atualizar um pacote NuGet com arquivo XAML aberto – [2878](https://github.com/NuGet/Home/issues/2878)
* Falha em projeto de site do IIS com caracteres inválidos no caminho – [2798](https://github.com/NuGet/Home/issues/2798)
* NuGet adiciona travamentos no CentOS – [2708](https://github.com/NuGet/Home/issues/2708)
* Falha na restauração com packagesavemode -nupkg para json.net – [2706](https://github.com/NuGet/Home/issues/2706)
* Filtro do Gerenciador de Pacotes não disponível na Janela de Saída do VS para o comando restore – [2704](https://github.com/NuGet/Home/issues/2704)

[Lista de todos os problemas corrigidos nesta versão](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.6")
