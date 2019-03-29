---
title: Notas de Versão do NuGet 4.3 RTM
description: Notas de versão do NuGet 4.3 RTM incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 72d707cb9bacd8abbac873ee10b2fd00f233d3cc
ms.sourcegitcommit: 74bf831e013470da8b0c1f43193df10bfb1f4fe6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/26/2019
ms.locfileid: "58432472"
---
# <a name="nuget-43-release-notes"></a>Notas sobre a versão do NuGet 4.3

O [Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) vem com o NuGet 4.3 RTM, que adiciona suporte para novos cenários como o .NET Standard 2.0/.NET Core 2.0, contém várias correções de qualidade e melhora o desempenho. Esta versão também oferece várias melhorias, como suporte para Controle de versão semântico 2.0.0, integração do MSBuild de avisos e erros do NuGet e muito mais.

## <a name="summary-whats-new-in-430"></a>Resumo: Novidades na versão 4.3.0

## <a name="summary-whats-new-in-431"></a>Resumo: Novidades na versão 4.3.1

* Correção de segurança: Permissões em arquivos criados dentro de ~/.nuget são muito abertas [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)
* Correção de segurança: Arquivos dentro de NUPKGs podem ter um caminho relativo acima do diretório NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Problemas conhecidos

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a>A restauração do NuGet pode tratar as origens de pacotes desabilitadas como habilitadas em alguns casos

#### <a name="issue"></a>Problema

As seguintes técnicas de linha de comando de restauração tratam as origens de pacotes desabilitadas como habilitadas. [NuGet#5704](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- `dotnet restore` (com o dotnet.exe que acompanha o VS ou com o que vem com o SDK do NetCore 2.0.0)

#### <a name="workaround"></a>Solução alternativa

1. Usar o Visual Studio (2017 15.3 ou posterior) ou o NuGet.exe (v4.3.0 ou posterior)
1. Exclua a fonte desabilitada e continue a usar o msbuild ou o dotnet.exe.
1. Para sua solução, você poderá usar "Limpar" no NuGet.config e, em seguida, definir as fontes necessárias para a solução.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Ao usar o Console do Gerenciador de Pacotes, talvez a tecla 'Enter' não funcione

#### <a name="issue"></a>Problema

Às vezes, a tecla enter não funciona no Console do Gerenciador de Pacotes. Se isso ocorrer, confira o progresso na correção e forneça informações úteis adicionais sobre as etapas de reprodução. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Solução alternativa

Reinicie o Visual Studio e abra o PMC antes de abrir a solução. Como alternativa, experimente excluir o `project.lock.json` e restaurá-lo novamente.

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

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a>Problemas corrigidos no período de tempo do NuGet 4.3 RTM

[Notas de Versão do NuGet 4.0 RTM](../release-notes/nuget-4.0-RTM.md) – Lista todos os problemas corrigidos no NuGet 4.0 RTM

### <a name="features"></a>Recursos

- Melhorar o desempenho da restauração do NuGet – Implementar NoOp para restaurações de linha de comando e do VS – [#5080](https://github.com/NuGet/Home/issues/5080)

- NET Core 2.0: A CLI do VS/Dotnet deve começar a usar a funcionalidade NuGet existente: Pastas de FallBack – [#4939](https://github.com/NuGet/Home/issues/4939)

- NET Core 2.0: Permitir que os usuários ignorem os avisos específicos de restauração (ou elevar para erro) – [#4898](https://github.com/NuGet/Home/issues/4898)

- NET Core 2.0: Assemblies localizadas de CLI – [#4896](https://github.com/NuGet/Home/issues/4896)

- NET Core 2.0: registrar todos os avisos/erros no arquivo de ativos (incluindo PackageTargetFallback) – [#4895](https://github.com/NuGet/Home/issues/4895)

- Habilitar o suporte do TFM: NetStandard2.0, Tizen – [#4892](https://github.com/NuGet/Home/issues/4892)

- Reduzir o número de projetos NuGet.Core e NuGet.Client (e, portanto, de DLLs) – [#2446](https://github.com/NuGet/Home/issues/2446)

- Adicionar capacidade de marcar avisos nuget como erros – [#2395](https://github.com/NuGet/Home/issues/2395)

### <a name="bugs"></a>Bugs

- msbuild /t:pack falha, pois o parâmetro “DevelopmentDependency” é incompatível com a tarefa “PackTask” – [#5584](https://github.com/NuGet/Home/issues/5584)

- A estrutura do diretórios para arquivos de conteúdo nivelados se o separador de diretório do Windows não for adicionado ao final de PackagePath – [#4795](https://github.com/NuGet/Home/issues/4795)

- Projetos netcore não são compatíveis com a configuração como developmentDependency – [#4694](https://github.com/NuGet/Home/issues/4694)

- RestoreManagerPackage está sendo carregado de forma síncrona, o que bloqueou o thread de interface do usuário e VS em deadlock – [#4679](https://github.com/NuGet/Home/issues/4679)

- dotnet
  - dotnet Restore (e, portanto, /t:restore do msbuild) ignora projetos com uma dependência explícita de projeto da solução [#4578](https://github.com/NuGet/Home/issues/4578)

- Se a solução tiver projectreferences que se referem ao mesmo projeto, mas com maiúsculas e minúsculas diferentes, a restauração poderá não funcionar. Isso também afeta diferentes caminhos relativos, sem diferenciação de maiúsculas e minúsculas – [#4574](https://github.com/NuGet/Home/issues/4574)

- Executáveis restaurados de pacotes do NuGet não podem mais ser executados com o .NET Core 2.0 – [#4424](https://github.com/NuGet/Home/issues/4424)

- O NuGet.exe absorve detalhes da exceção ao analisar o arquivo da solução – [#4411](https://github.com/NuGet/Home/issues/4411)

- O pacote coloca os arquivos de conteúdo no local errado se ContentTargetFolders contiver um caminho que termina com '/' no Windows – [#4407](https://github.com/NuGet/Home/issues/4407)

- Não é possível restaurar um DotNetCliToolReference para um pacote de ferramentas voltado para o netcoreapp1.1 – [#4396](https://github.com/NuGet/Home/issues/4396)

- A CLI de atualização do Nuget deixa a condição de versão do pacote antigo no arquivo de projeto (C++) – [#2449](https://github.com/NuGet/Home/issues/2449)

### <a name="dcrs"></a>DCRs

- Ler DotnetCliToolTargetFramework da indicação do CPS – [#5397](https://github.com/NuGet/Home/issues/5397)

- A verificação de TPMinV deve funcionar para o pj estilo UWP – [#4763](https://github.com/NuGet/Home/issues/4763)

- Melhorar a descrição da interface do usuário para pacotes AutoReferenced – [#4471](https://github.com/NuGet/Home/issues/4471)

- A restauração do NuGet está selecionando ativos de compilação da seção de tempo de execução. - [#4207](https://github.com/NuGet/Home/issues/4207)

- Colocar o diagnóstico de dependência no arquivo de bloqueio – [#1599](https://github.com/NuGet/Home/issues/1599)

## <a name="links-to-github-issues-fixed-in-43-rtm"></a>Links para problemas do GitHub corrigidos no RTM 4.3

[Lista de Problemas](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
