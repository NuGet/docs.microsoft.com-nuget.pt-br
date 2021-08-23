---
title: notas de versão do NuGet 5,10
description: notas de versão do NuGet 5,10, incluindo novos recursos, correções de bugs e DCRs.
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 80a372074604f5c0073f78927b84de00e78acc74
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726945"
---
# <a name="nuget-510-release-notes"></a>notas de versão do NuGet 5,10

Veículos de distribuição do NuGet:

| Versão do NuGet | Disponível na versão do Visual Studio | Disponível em SDKs do .NET |
|:---|:---|:---|
| [**5.10.0**](https://nuget.org/downloads) | [Visual Studio 2019 versão 16,10](https://visualstudio.microsoft.com/downloads/) | [5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> instalado com o Visual Studio 2019 com carga de trabalho do .net Core
  
> [!NOTE]
> Visual Studio 16,10, MSBuild 16,10 e .net 5.0.300 + requer NuGet.exe 5,10 ou posterior.

## <a name="summary-whats-new-in-510"></a>Resumo: o que há de novo no 5,10

* Assinatura: implementar dotnet confiável-comandos de entrada- [#8053](https://github.com/NuGet/Home/issues/8053)

* tornar a validação padrão desabilitada no Linux, mas habilitada por padrão em Windows [#10713](https://github.com/NuGet/Home/issues/10713)

* Adicionar uma variável ENV para verificação de assinatura de pacote no .NET 5 + Linux/MAC- [#10742](https://github.com/NuGet/Home/issues/10742)

* Melhorar o desempenho da instalação de novo pacote para soluções grandes – [#10166](https://github.com/NuGet/Home/issues/10166)

* Adicione o tipo de projeto `nfproj` à lista de supportedProjectExtensions para a CLI do NuGet. - [#10562](https://github.com/NuGet/Home/issues/10562)

### <a name="issues-fixed-in-this-release"></a>Problemas corrigidos nesta versão

* Suprimir o `<requireLicenseAcceptance>` elemento ao empacotar um projeto- [#5133](https://github.com/NuGet/Home/issues/5133)

* [CPVM] aviso de visualização deve ser mostrado na CLI do dotnet- [#10226](https://github.com/NuGet/Home/issues/10226)

* Atualize os tokens de cor de primeiro e segundo plano do PMUI para CommonDocumentColors- [#10608](https://github.com/NuGet/Home/issues/10608)

* [Bash de Bug] Erro "a operação cancelada pelo usuário" aparece na janela Lista de Erros ao alternar entre guias rapidamente na interface do usuário do PM- [#10671](https://github.com/NuGet/Home/issues/10671)

* Interface do usuário do PM: melhorar o desempenho de instalação do pacote no nível da solução- [#10210](https://github.com/NuGet/Home/issues/10210)

* Substitua GetService por GetServiceAsync em todos os lugares em NuGet. Clientes- [#3784](https://github.com/NuGet/Home/issues/3784)

* Problema de desempenho do NuGet.exe Pack com `..` caminho relativo- [#5016](https://github.com/NuGet/Home/issues/5016)

* O desempenho do "pacote NuGet" diminui com os níveis crescentes nos caminhos de origem- [#5706](https://github.com/NuGet/Home/issues/5706)

* NuGet não erro ao empacotar nuspec com arquivos duplicados. - [#6941](https://github.com/NuGet/Home/issues/6941)

* NuGet pack "o DateTimeOffset especificado não pode ser convertido em um carimbo de data/hora de arquivo Zip"- [#7001](https://github.com/NuGet/Home/issues/7001)

* Os carimbos de data/hora do arquivo do pacote empacotado são deslocados pelo fuso horário [#7395](https://github.com/NuGet/Home/issues/7395)

* NU1004 deve conter mais informações acionáveis- [#7696](https://github.com/NuGet/Home/issues/7696)

* [Bash de Bug] [Falha de teste] O arquivo de bloqueio vazio/malformado não deve ser atualizado ao executar ' dotnet restore--use-Lock-File--Locked-Mode '- [#8640](https://github.com/NuGet/Home/issues/8640)

* NuGetVersionRange permite que intervalos logicamente incorretos sejam analisados- [#9145](https://github.com/NuGet/Home/issues/9145)

* A interface do usuário PM não pode mostrar a cor de fundo distinguivel entre origens de pacote selecionadas e focalizadas- [#9538](https://github.com/NuGet/Home/issues/9538)

* A caixa de seleção para selecionar projetos para instalar não está sendo lida pelo leitor de tela- [#9578](https://github.com/NuGet/Home/issues/9578)

* A seleção padrão da lista suspensa de versões do painel de detalhes deve ser instalada/LatestStable nas guias instalado/atualizações- [#9887](https://github.com/NuGet/Home/issues/9887)

* Remova a conta de solução alternativa para alguns TargetPlatformMoniker de relatório de SDKs do .NET 5 de ` ,Version= `  -  [#9913](https://github.com/NuGet/Home/issues/9913)

* a verificação do NuGet do dotnet está muito silenciosa- [#10316](https://github.com/NuGet/Home/issues/10316)

* VersionRange não pode analisar intervalos de um único dígito- [#10342](https://github.com/NuGet/Home/issues/10342)

* O VS Solution Manager gera uma exceção nula durante a depuração- [#10352](https://github.com/NuGet/Home/issues/10352)

* Mover mensagens de exceção da CLI para arquivos de recursos de cadeia de caracteres- [#10392](https://github.com/NuGet/Home/issues/10392)

* Remover código inativo (TabItemButtonAutomationPeer)- [#10435](https://github.com/NuGet/Home/issues/10435)

* O menu de contexto atualizar deve rolar para o primeiro item selecionado- [#10498](https://github.com/NuGet/Home/issues/10498)

* Detalhes da solução PMUI estão sobrepondo barras horizontais- [#10533](https://github.com/NuGet/Home/issues/10533)

* Assinatura: detalhes da assinatura primária não exibidos quando o certificado expirou e o carimbo de data/hora não confiável- [#10535](https://github.com/NuGet/Home/issues/10535)

* Não ter fontes habilitadas impede que a interface do usuário da PM mostre- [#10541](https://github.com/NuGet/Home/issues/10541)

* Os metadados do pacote (detalhes, substituição) às vezes não são extraídos de nuget.org em CodeSpaces- [#10549](https://github.com/NuGet/Home/issues/10549)

* Falha na inicialização do PMUI com exceção durante a sessão de depuração- [#10559](https://github.com/NuGet/Home/issues/10559)

* a restauração do NuGet resulta em uma falha de verificação de integridade do pacote no sistema big endian [#10567](https://github.com/NuGet/Home/issues/10567)

* FormatException é lançado em vez de Packagexception- [#10595](https://github.com/NuGet/Home/issues/10595)

* CPVM-problemas de simultaneidade no algoritmo de movimentação de grafo- [#10598](https://github.com/NuGet/Home/issues/10598)

* Adicionar telemetria da versão do PMC PowerShell- [#10609](https://github.com/NuGet/Home/issues/10609)

* Melhorar o desempenho de classificação NuGetVersion- [#10611](https://github.com/NuGet/Home/issues/10611)

* Os assinantes confiáveis Add têm argumentos inconsistentes- [#10647](https://github.com/NuGet/Home/issues/10647)

* Vs2019 v 16.9.0: alternando guias no NuGet Gerenciador de Pacotes de "atualizações" para "instalado" não atualiza o quadro. - [#10654](https://github.com/NuGet/Home/issues/10654)

* Remova o "v" do número de versão em PMUI- [#10677](https://github.com/NuGet/Home/issues/10677)

* INuGetProjectService. GetInstalledPackagesAsync gera antes de receber a indicação do sistema de projeto do CPS- [#10681](https://github.com/NuGet/Home/issues/10681)

* os ícones inseridos causam acesso negado da origem "pacotes Offline Microsoft Visual Studio" na guia procurar – [#10687](https://github.com/NuGet/Home/issues/10687)

* INuGetProjectService. GetInstalledPackagesAsync gera quando MSBuildProjectExtensionsPath não está definido- [#10739](https://github.com/NuGet/Home/issues/10739)

* "dotnet NuGet remove Source nuget.org" não funciona na primeira vez que [#10745](https://github.com/NuGet/Home/issues/10745)

* O NuGet bloqueia um thread de ThreadPool em um método assíncrono fazendo uma chamada síncrona para o thread de interface do usuário- [#10775](https://github.com/NuGet/Home/issues/10775)

* `PackageLoadContext.GetInstalledAndTransitivePackagesAsync` é um código inativo e desempenho prejudicando- [#10790](https://github.com/NuGet/Home/issues/10790)

* usar o ícone inserido em pacotes NuGet SDK- [#10795](https://github.com/NuGet/Home/issues/10795)

* Atualizar a lista de licenças do SPDX- [#10806](https://github.com/NuGet/Home/issues/10806)

**[Lista de todos os problemas corrigidos nesta versão-5,10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**
  
**[Lista de confirmações nesta versão-5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**
  
### <a name="community-contributions"></a>Contribuições da comunidade

obrigado a todos os colaboradores que ajudaram a tornar essa NuGet versão incrível!

|Quem|PRs|Problemas|
|----|----|----|
[Louis-z](https://github.com/louis-z) | [3991](https://github.com/NuGet/NuGet.Client/pull/3991) | VersionRange não pode analisar intervalos de um único dígito- [#10342](https://github.com/NuGet/Home/issues/10342)
[omajid](https://github.com/omajid) | [3860](https://github.com/NuGet/NuGet.Client/pull/3860) | NuGet. O build.sh do cliente está desfeito [#10139](https://github.com/NuGet/Home/issues/10139)
[Nirmal4G](https://github.com/Nirmal4G) | [3623](https://github.com/NuGet/NuGet.Client/pull/3623) | NuGet. O build.sh do cliente está desfeito [#10139](https://github.com/NuGet/Home/issues/10139)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | O desempenho do "pacote NuGet" diminui com os níveis crescentes nos caminhos de origem- [#5706](https://github.com/NuGet/Home/issues/5706)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | Problema de desempenho do NuGet.exe Pack com.. caminho relativo- [#5016](https://github.com/NuGet/Home/issues/5016)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3940](https://github.com/NuGet/NuGet.Client/pull/3940) | CPVM-problemas de simultaneidade no algoritmo de movimentação de grafo- [#10598](https://github.com/NuGet/Home/issues/10598)
[josesimoes](https://github.com/josesimoes) | [3943](https://github.com/NuGet/NuGet.Client/pull/3943) | Adicione o tipo de projeto nfproj à lista de supportedProjectExtensions para a CLI do NuGet. - [#10562](https://github.com/NuGet/Home/issues/10562)

## <a name="feedback-welcome"></a>Comentários de boas-vindas

Seus comentários são importantes para nós.  se houver problemas com esta versão, verifique nossos [GitHub problemas](https://github.com/NuGet/Home/issues) e [Visual Studio Community do desenvolvedor](https://developercommunity.visualstudio.com/) para problemas existentes.  Para novos problemas no NuGet, informe um [GitHub problema](https://github.com/NuGet/Home/issues/new).
Para problemas NuGet experiência geral, informe-nos [](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) por meio da opção Relatar um Problema encontrada em seu IDE favorito em Ajuda **> Relatar um Problema**.
