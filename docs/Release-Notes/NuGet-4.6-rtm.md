---
title: Notas de versão do NuGet 4.6 RTM | Microsoft Docs
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 3/7/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Notas de versão do NuGet 4.6.0, incluindo problemas conhecidos, correções de bugs, funcionalidades adicionadas e DCRs.
keywords: Notas de versão do NuGet 4.6.0, correções de bugs, problemas conhecidos, funcionalidades adicionadas, DCRs
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 004ad16018443292840b00fa88aa78350e371414
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-46-rtm-release-notes"></a>Notas de versão do NuGet 4.6 RTM

O [Visual Studio 2017 15.6 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) vem com o [NuGet 4.6.0](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe).

## <a name="summary-whats-new-in-this-release"></a>Resumo: novidades desta versão
* Adicionamos compatibilidade com [pacotes de assinatura](https://docs.microsoft.com/en-us/nuget/create-packages/sign-a-package).  
* O Visual Studio 2017 e o nuget.exe agora verificam a integridade do pacote antes de instalá-lo, restaurando os pacotes para [pacotes assinados](https://docs.microsoft.com/en-us/nuget/reference/signed-packages-reference).
* Melhoramos o desempenho das restaurações sucessivas.

## <a name="known-issues"></a>Problemas conhecidos
### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problemas com o .NET Standard 2.0 com o .NET Framework & NuGet 

O .NET Standard e suas ferramentas foram projetados de modo que os projetos destinados ao .NET Framework 4.6.1 podem consumir pacotes do NuGet e projetos destinados ao .NET Standard 2.0 ou anterior. [Este documento](https://github.com/dotnet/standard/issues/481) resume os problemas desse cenário, o plano para lidar com eles e soluções alternativas que você pode implantar com o estado atual das ferramentas.

## <a name="top-issues-fixed-in-this-release"></a>Principais problemas corrigidos nesta versão

**Correções de desempenho**
* Não grave arquivos de ativo quando não houver alterações – [6491](https://github.com/NuGet/Home/issues/6491)
* A restauração provoca avaliações adicionais do MSBuild quando o TFM dos projetos filho não coincidem com o do projeto pai – [6311](https://github.com/NuGet/Home/issues/6311)
* Melhorar o desempenho da restauração NoOp otimizando a criação das especificações do grafo de dependência – [6252](https://github.com/NuGet/Home/issues/6252)

**•s**
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
