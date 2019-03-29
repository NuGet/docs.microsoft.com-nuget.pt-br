---
title: Notas de Versão do NuGet 4.5 RTM
description: Notas de versão do NuGet 4.5 RTM incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: anangaur
ms.author: anangaur
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 321aedb471bc6f86e9c03878093b199267e31195
ms.sourcegitcommit: 74bf831e013470da8b0c1f43193df10bfb1f4fe6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/26/2019
ms.locfileid: "58432498"
---
# <a name="nuget-45-release-notes"></a>Notas sobre a versão do NuGet 4.5

O [Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) vem com o [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).

## <a name="summary-whats-new-in-450"></a>Resumo: Novidades na versão 4.5.0

## <a name="summary-whats-new-in-452"></a>Resumo: Novidades na versão 4.5.2

* Correção de segurança: Permissões em arquivos criados dentro de ~/.nuget são muito abertas [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-453"></a>Resumo: Novidades na versão 4.5.3

* Correção de segurança: Arquivos dentro de NUPKGs podem ter um caminho relativo acima do diretório NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Problemas conhecidos

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problemas com o .NET Standard 2.0 com o .NET Framework & NuGet 

O .NET Standard e suas ferramentas foram projetados de modo que os projetos destinados ao .NET Framework 4.6.1 podem consumir pacotes do NuGet e projetos destinados ao .NET Standard 2.0 ou anterior. [Este documento](https://github.com/dotnet/standard/issues/481) resume os problemas desse cenário, o plano para lidar com eles e soluções alternativas que você pode implantar com o estado atual das ferramentas.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Você não consegue exibir, adicionar ou atualizar o DotNetCLITools usando o Gerenciador de Pacotes NuGet

#### <a name="issue"></a>Problema

O Gerenciador de Pacotes do NuGet não exibe nem permite a adição/atualização de DotNetCLITools. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Solução alternativa

O DotNetCLIToolReferences deve ser editado manualmente no arquivo de projeto.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Redirecionar a versão da estrutura de destino pode levar a um IntelliSense incompleto

#### <a name="issue"></a>Problema

Redirecionar a versão da estrutura de destino pode levar a um IntelliSense incompleto no Visual Studio. Isso acontece quando você está usando PackageReferences como o formato do gerenciador de pacotes. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Solução alternativa

Faça uma restauração manual.

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>Um pacote em um projeto do .NET Core que contém um assembly com uma assinatura inválida pode disparar um loop de restauração infinito

#### <a name="issue"></a>Problema

Às vezes, quando você usa um pacote que contém um assembly com uma assinatura inválida ou quando a versão do pacote é definida com o ticker 'DateTime', isso faz com que a restauração automática de pacotes seja executada em loop infinito [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).

#### <a name="workaround"></a>Solução alternativa

Não há nenhuma solução alternativa no momento.

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a>Problemas corrigidos no período de tempo do NuGet 4.5 RTM

Para problemas corrigidos no NuGet 4.4 RTM, consulte as [Notas de Versão do NuGet 4.4 RTM](../release-notes/nuget-4.4-RTM.md) 

### <a name="features"></a>Recursos

- Desabilitar push automático do pacote de símbolos – [#6113](https://github.com/NuGet/Home/issues/6113)

### <a name="bugs"></a>Bugs

- [Regressão] em 15.5p1: Portable0.0 é ignorado – [#6105](https://github.com/NuGet/Home/issues/6105)
- Ativos de pacotes ausentes após a restauração – [#5995](https://github.com/NuGet/Home/issues/5995)
- Provedores de credenciais de plug-in não funcionam com URIs que contém espaços – [#5982](https://github.com/NuGet/Home/issues/5982)
- Em caso de falha ao restaurar o pacote, o erro deve ser impresso na saída mesmo com Detalhamento mínimo ATIVADO – [#5658](https://github.com/NuGet/Home/issues/5658)
- dotnet
  - dotnetcore restore no nível da solução não segue a ProjectReference com ReferenceOutputAssembly falso, levando a falhas de build aleatórias – [#5490](https://github.com/NuGet/Home/issues/5490)
- Preenchimento automático em PMC funciona incorretamente com métodos de objeto – [#4800](https://github.com/NuGet/Home/issues/4800)
- A restauração do nuget.exe falha com o conjunto de ferramentas do Visual Studio 2015 – [#4713](https://github.com/NuGet/Home/issues/4713)
- perf – pmc é caro para ser instanciado no vs2017 – [#4205](https://github.com/NuGet/Home/issues/4205)
- Lentidão para obter informações de dependência em uma conexão lenta – [#4089](https://github.com/NuGet/Home/issues/4089)
- uninstall-package com -RemoveDependencies falhará se vários pacotes compartilharem uma dependência comum – [#4026](https://github.com/NuGet/Home/issues/4026)
- Finalizar NuGet.Core.nupkg para publicação – [#3581](https://github.com/NuGet/Home/issues/3581)
- O pacote do NuGet resolve a ID de dependência do nome de diretório quando -IncludeProjectReferences é usado para csproj + project.json – [#3566](https://github.com/NuGet/Home/issues/3566)
- O inicializador de tipo para 'NuGet.ProxyCache' gerou uma exceção – [#3144](https://github.com/NuGet/Home/issues/3144)
- Problema de desempenho de restauração do nuget com kudu – [#3087](https://github.com/NuGet/Home/issues/3087)
- O cliente da interface do usuário falha ao mostrar qualquer erro ou aviso quando a pesquisa está à frente de blobs do Registro – [#2149](https://github.com/NuGet/Home/issues/2149)
- Get-Packages – Atualizações geram uma consulta incorreta – [#2135](https://github.com/NuGet/Home/issues/2135)

## <a name="links-to-github-issues-fixed-in-45-rtm"></a>Links para problemas do GitHub corrigidos no RTM 4.5

[Lista de problemas](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
