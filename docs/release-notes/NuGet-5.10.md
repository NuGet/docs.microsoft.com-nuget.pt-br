---
title: Notas de versão do NuGet 5.10
description: Notas sobre a versão do NuGet 5.10, incluindo novos recursos, correções de bugs e DCRs.
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 666eda5803b540dc18a9310f61c92dc74ff2089e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112356532"
---
# <a name="nuget-510-release-notes"></a>Notas de versão do NuGet 5.10

Veículos de distribuição do NuGet:

| Versão do NuGet | Disponível na versão do Visual Studio | Disponível em SDKs do .NET |
|:---|:---|:---|
| [**5.10.0**](https://nuget.org/downloads) | [Visual Studio 2019 versão 16.10](https://visualstudio.microsoft.com/downloads/) | [5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> Instalado com o Visual Studio 2019 com carga de trabalho do .NET Core
  
> [!NOTE]
> Visual Studio 16.10, MSBuild 16.10 e .NET 5.0.300+ requer NuGet.exe 5.10 ou posterior.

## <a name="summary-whats-new-in-510"></a>Resumo: Novidades na versão 5.10

* Assinatura: implementar o comando dotnet trusted-signers – [#8053](https://github.com/NuGet/Home/issues/8053)

* Tornar a validação padrão desabilitada no Linux, mas habilitada por padrão no Windows – [#10713](https://github.com/NuGet/Home/issues/10713)

* Adicionar uma variável ENV para verificação de assinatura de pacote no .NET 5+ Linux/MAC – [#10742](https://github.com/NuGet/Home/issues/10742)

* Melhorar o desempenho da instalação do novo pacote para soluções [grandes – #10166](https://github.com/NuGet/Home/issues/10166)

* Adicione o tipo de `nfproj` projeto à lista de supportedProjectExtensions para a CLI do Nuget. - [#10562](https://github.com/NuGet/Home/issues/10562)

### <a name="issues-fixed-in-this-release"></a>Problemas corrigidos nesta versão

* Suprimir <requireLicenseAcceptance> o elemento ao empacotar um projeto – [#5133](https://github.com/NuGet/Home/issues/5133)

* O aviso de visualização [CPVM] deve ser mostrado na cli do dotnet – [#10226](https://github.com/NuGet/Home/issues/10226)

* Atualize os tokens de cor da tela de fundo e de primeiro plano do PMUI para CommonDocumentColors – [#10608](https://github.com/NuGet/Home/issues/10608)

* [Bug Bash] O erro "operação cancelada pelo usuário" aparece na janela Lista de Erros ao alternar entre guias rapidamente na interface do usuário do PM [– #10671](https://github.com/NuGet/Home/issues/10671)

* Interface do usuário do PM: melhorar o desempenho da instalação do pacote no nível da solução – [#10210](https://github.com/NuGet/Home/issues/10210)

* Substitua GetService por GetServiceAsync em todos os lugares no NuGet.Clients – [#3784](https://github.com/NuGet/Home/issues/3784)

* NuGet.exe de desempenho do pacote com `..` caminho relativo – [#5016](https://github.com/NuGet/Home/issues/5016)

* O desempenho do "pacote nuget" diminui com níveis crescentes nos caminhos de origem – [#5706](https://github.com/NuGet/Home/issues/5706)

* O NuGet não erro ao empacotar nuspec com arquivos duplicados. - [#6941](https://github.com/NuGet/Home/issues/6941)

* Pacote NuGet "O DateTimeOffset especificado não pode ser convertido em um data/hora do arquivo Zip" – [#7001](https://github.com/NuGet/Home/issues/7001)

* Os tempos de data/hora do arquivo do pacote empacotado são deslocados pelo timezone – [#7395](https://github.com/NuGet/Home/issues/7395)

* NU1004 deve conter informações [](https://github.com/NuGet/Home/issues/7696) mais a #7696

* [Bug Bash] [Falha de teste] O arquivo de bloqueio vazio/malformado não deve ser atualizado ao executar 'dotnet restore --use-lock-file --locked-mode' – [#8640](https://github.com/NuGet/Home/issues/8640)

* NuGetVersionRange permite que intervalos logicamente incorretos sejam analisados – [#9145](https://github.com/NuGet/Home/issues/9145)

* A interface do usuário do PM não pode mostrar a cor da tela de fundo distinguível entre as fontes de pacote selecionadas e com foco – [#9538](https://github.com/NuGet/Home/issues/9538)

* A caixa de seleção para selecionar projetos a serem instalados não está sendo lida pelo leitor de tela – [#9578](https://github.com/NuGet/Home/issues/9578)

* A seleção padrão do menu suspenso Versões do Painel de Detalhes deve ser Installed/LatestStable nas guias [Instalados/Atualizações – #9887](https://github.com/NuGet/Home/issues/9887)

* Remover a conta alternativa de alguns SDKs do .NET 5 report TargetPlatformMoniker da ` ,Version= `  -  [#9913](https://github.com/NuGet/Home/issues/9913)

* dotnet nuget verify is too quiet - [#10316](https://github.com/NuGet/Home/issues/10316)

* VersionRange não pode analisar intervalos de dígito único [– #10342](https://github.com/NuGet/Home/issues/10342)

* O Gerenciador de Soluções do VS lança uma exceção nula para durante a depuração [– #10352](https://github.com/NuGet/Home/issues/10352)

* Mover mensagens de exceção da CLI para arquivos de Recurso de Cadeia de Caracteres [– #10392](https://github.com/NuGet/Home/issues/10392)

* Remover código morto (TabItemButtonAutomationPeer) – [#10435](https://github.com/NuGet/Home/issues/10435)

* O menu de contexto de atualização deve rolar até o primeiro item [selecionado – #10498](https://github.com/NuGet/Home/issues/10498)

* Detalhes da PMUI da Solução tem barra horizontal sobreposta – [#10533](https://github.com/NuGet/Home/issues/10533)

* Assinatura: detalhes da assinatura primária não exibidos quando o certificado expirou e o registro de data/hora não é [#10535](https://github.com/NuGet/Home/issues/10535)

* Não ter fontes habilitadas impede que a interface do usuário do PM seja [#10541](https://github.com/NuGet/Home/issues/10541)

* Os metadados do pacote (detalhes, preterição) às vezes não são retirados nuget.org em CodeSpaces – [#10549](https://github.com/NuGet/Home/issues/10549)

* A inicialização do PMUI falha com exceção durante a sessão de depuração – [#10559](https://github.com/NuGet/Home/issues/10559)

* A restauração do nuget resulta em uma falha de verificação de integridade do pacote big endian sistema – [#10567](https://github.com/NuGet/Home/issues/10567)

* FormatException é lançada em vez de PackagingException [– #10595](https://github.com/NuGet/Home/issues/10595)

* CPVM – Problemas de concurreência no algoritmo de trilha de grafo – [#10598](https://github.com/NuGet/Home/issues/10598)

* Adicionar telemetria de versão do PMC powershell [– #10609](https://github.com/NuGet/Home/issues/10609)

* Melhorar o desempenho de classificação do NuGetVersion [– #10611](https://github.com/NuGet/Home/issues/10611)

* Trusted-signers Add tem argumentos inconsistentes – [#10647](https://github.com/NuGet/Home/issues/10647)

* Vs2019 v16.9.0: Alternar guias no NuGet Gerenciador de Pacotes de "Atualizações" para "Instalado" não atualiza o quadro. - [#10654](https://github.com/NuGet/Home/issues/10654)

* Remova o "v" do número de versão no PMUI – [#10677](https://github.com/NuGet/Home/issues/10677)

* INuGetProjectService.GetInstalledPackagesAsync é lançado antes de receber a indicação do sistema de projeto CPS – [#10681](https://github.com/NuGet/Home/issues/10681)

* Ícones inseridos causam Acesso Negado da fonte "Microsoft Visual Studio offline" na guia Procurar – [#10687](https://github.com/NuGet/Home/issues/10687)

* INuGetProjectService.GetInstalledPackagesAsync é lançado quando MSBuildProjectExtensionsPath não está [definido – #10739](https://github.com/NuGet/Home/issues/10739)

* "dotnet nuget remove source nuget.org" não funciona na primeira vez – [#10745](https://github.com/NuGet/Home/issues/10745)

* O Nuget bloqueia um threadpool em um método assíncrono que faz uma chamada síncrona para o thread da interface do usuário – [#10775](https://github.com/NuGet/Home/issues/10775)

* Ferramentas -> Opções -> cadeia de caracteres Gerenciador de Pacotes NuGet está truncada - [#10779](https://github.com/NuGet/Home/issues/10779)

* `PackageLoadContext.GetInstalledAndTransitivePackagesAsync` é código inodado e prejudica o desempenho [– #10790](https://github.com/NuGet/Home/issues/10790)

* Usar o ícone inserido em pacotes do SDK do NuGet [– #10795](https://github.com/NuGet/Home/issues/10795)

* Atualizar a lista de licenças SPDX [– #10806](https://github.com/NuGet/Home/issues/10806)

**[Lista de todos os problemas corrigidos nesta versão – 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**
  
**[Lista de confirmações nesta versão – 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**
  
### <a name="community-contributions"></a>Contribuições da comunidade

Agradecemos a todos os colaboradores que ajudaram a tornar essa versão do NuGet incrível!

|Quem|Prs|Problemas|
|----|----|----|
[oda-z](https://github.com/louis-z) | [3991](https://github.com/NuGet/NuGet.Client/pull/3991) | VersionRange não pode analisar intervalos de dígito único [– #10342](https://github.com/NuGet/Home/issues/10342)
[omajid](https://github.com/omajid) | [3860](https://github.com/NuGet/NuGet.Client/pull/3860) | O build.sh NuGet.Client está [desfeito – #10139](https://github.com/NuGet/Home/issues/10139)
[Nirmal4G](https://github.com/Nirmal4G) | [3623](https://github.com/NuGet/NuGet.Client/pull/3623) | O build.sh NuGet.Client está [desfeito – #10139](https://github.com/NuGet/Home/issues/10139)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | O desempenho do "pacote nuget" diminui com níveis crescentes nos caminhos de origem – [#5706](https://github.com/NuGet/Home/issues/5706)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | NuGet.exe de desempenho do pacote com .. caminho relativo – [#5016](https://github.com/NuGet/Home/issues/5016)
[marcin-kryscianc](https://github.com/marcin-krystianc) | [3940](https://github.com/NuGet/NuGet.Client/pull/3940) | CPVM – Problemas de concurreência no algoritmo de trilha de grafo – [#10598](https://github.com/NuGet/Home/issues/10598)
[simoes](https://github.com/josesimoes) | [3943](https://github.com/NuGet/NuGet.Client/pull/3943) | Adicione o tipo de projeto nfproj à lista de supportedProjectExtensions para a CLI do Nuget. - [#10562](https://github.com/NuGet/Home/issues/10562)

## <a name="feedback-welcome"></a>Boas-vindas aos comentários

Seus comentários são importantes para nós.  Se houver problemas com esta versão, verifique os problemas do [GitHub](https://github.com/NuGet/Home/issues) e a [comunidade de desenvolvedores do Visual Studio](https://developercommunity.visualstudio.com/) para obter os problemas existentes.  Para novos problemas no NuGet, informe um [problema do GitHub](https://github.com/NuGet/Home/issues/new).
Para problemas gerais de experiência do NuGet, informe-nos por meio do [relatório uma opção de problema](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) encontrada em seu IDE favorito em **ajuda > relatar um problema**.
