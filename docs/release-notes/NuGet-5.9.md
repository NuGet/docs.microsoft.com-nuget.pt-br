---
title: Notas de versão do NuGet 5.9
description: Notas sobre a versão do NuGet 5.9, incluindo novos recursos, correções de bugs e DCRs.
author: erdembayar
ms.author: eryondon
ms.date: 3/11/2021
ms.topic: conceptual
ms.openlocfilehash: 1152af99cf1421918a42d0d1faa33f1452f54a8f
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323876"
---
# <a name="nuget-59-release-notes"></a>Notas de versão do NuGet 5.9

Veículos de distribuição do NuGet:

| Versão do NuGet | Disponível na versão do Visual Studio | Disponível em SDKs do .NET |
|:---|:---|:---|
| [**5.9.0**](https://nuget.org/downloads) | [Visual Studio 2019 versão 16.9](https://visualstudio.microsoft.com/downloads/) | [5.0.200](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |
| [**5.9.1**](https://nuget.org/downloads) | [Visual Studio 2019 versão 16.9](https://visualstudio.microsoft.com/downloads/) | [5.0.202](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> Instalado com o Visual Studio 2019 com carga de trabalho do .NET Core
  
> [!NOTE]
> Visual Studio 16.9, o MSBuild 16.9 e o .NET 5.0.200+ exigem NuGet.exe 5.9 ou posterior.

## <a name="summary-whats-new-in-59"></a>Resumo: Novidades na versão 5.9

* Adicione o item de menu de contexto "Atualizar" para dependências de pacote que inicia Gerenciador de Pacotes interface do usuário com pacotes pré-selecionados a atualizar – [#10378](https://github.com/NuGet/Home/issues/10378)

    ![Clique com o botão direito do mouse na experiência "Atualizar" do pacote](media/releasenotes-59-update.png)

* Mostrar a versão solicitada (incluindo a solicitação de intervalo de versão ou versão flutuante) na coluna "Versão" da lista de projetos no nível da solução Gerenciador de Pacotes interface do usuário – [#9827](https://github.com/NuGet/Home/issues/9827)

    ![Versão solicitada no nível da solução Gerenciador de Pacotes interface do usuário](media/releasenotes-59-requested-version.png)

* Sugestões de pacote do IntelliCode na guia Procurar Gerenciador de Pacotes interface do usuário lançada como um teste A/B – [#10053](https://github.com/NuGet/Home/issues/10053)

* Estenda `.nupkg.metadata` o arquivo para incluir a origem da instalação – [#10354](https://github.com/NuGet/Home/issues/10354)

* Introduzir uma nova propriedade msbuild para excluir a saída de build para TFMs específicos durante a tarefa de pacote – [#10396](https://github.com/NuGet/Home/issues/10396)

### <a name="issues-fixed-in-this-release"></a>Problemas corrigidos nesta versão

**DCRs(Solicitação de Alteração de Design):**

* O ícone de ícone para baixo quando a versão mais recente do pacote é instalada não é intuitivo. O tique verde antigo era perfeito – [#9789](https://github.com/NuGet/Home/issues/9789)

* O detalhes de depuração do Nuget deve dizer de onde um pacote veio – [#3055](https://github.com/NuGet/Home/issues/3055)

* O pacote NuGet deve capturar a omissão incorreta do ponto nos números de versão – [#9215](https://github.com/NuGet/Home/issues/9215)

* [CPVM] Desabilitar a alfinetes das dependências transitivas centrais [– #10132](https://github.com/NuGet/Home/issues/10132)

* net5 TFM: produzir erro quando TPV ausente – [#9441](https://github.com/NuGet/Home/issues/9441)

* Contenthash do pacote de log durante o log de restauração (durante a [extração)](https://github.com/NuGet/Home/issues/10384) – #10384

* Implementar um mecanismo de pré-registro para projetos de PR herdado que chamam a restauração na solução aberta – [#9986](https://github.com/NuGet/Home/issues/9986)

* O recomendador de pacote NuGet deve funcionar quando mais de uma fonte é selecionada no gerenciador de pacotes – [#10433](https://github.com/NuGet/Home/issues/10433)

* Ao restaurar em detalhes normais, registre em log a origem de um pacote que está sendo restaurado – [#10461](https://github.com/NuGet/Home/issues/10461)

**Bugs:**

* INuGetPackageFileService – Buscar imagens e licenças inseridas para codespaces conectados e [autônomos](https://github.com/NuGet/Home/issues/10151) – #10151

* VS OE: formattter ausente IProjectMetadataContextInfo – [#10079](https://github.com/NuGet/Home/issues/10079)

* [CPVM-Perf] Reduzir as informações escritas em centralTransitiveDependencyGroups – [#10002](https://github.com/NuGet/Home/issues/10002)

* As operações de restauração que lançam devido a um projeto que não está sendo carregado são relatadas como `NoOp` em [telemetria](https://github.com/NuGet/Home/issues/9985) – #9985

* Ícones com determinadas paletas de cores faz com que a interface do usuário do PM falha no VS – [#10037](https://github.com/NuGet/Home/issues/10037)

* [CPVM-Perf] Reduzir o clone PackageSpec ao adicionar as informações de CPVM – [#10003](https://github.com/NuGet/Home/issues/10003)

* Interface do usuário do PM – carregamento de ícone assíncrono [– #10009](https://github.com/NuGet/Home/issues/10009)

* Atraso na interface do usuário ao carregar URLs de ícone na interface do usuário do PM [– #8505](https://github.com/NuGet/Home/issues/8505)

* Afinidade de thread em threads de interface do usuário bitmapSource e WPF [– #9161](https://github.com/NuGet/Home/issues/9161)

* Aviso para aviso NU5128 quando packastool com alias targetframework – [#10097](https://github.com/NuGet/Home/issues/10097)

* A lógica OutputPath em destinos de pacote em um build personalizado não funciona corretamente – [#9234](https://github.com/NuGet/Home/issues/9234)

* VS OE: instância de IServiceBroker de cache no cliente – [#10141](https://github.com/NuGet/Home/issues/10141)

* Tornar a criação de NuGetProjectActions para desinstalação da interface do usuário do PM uma operação paralela – [#9956](https://github.com/NuGet/Home/issues/9956)

* Desempenho: reduzir UIDelays em GetPackageSpecsAsync para projetos herdados e projetos não PR – [#9953](https://github.com/NuGet/Home/issues/9953)

* ``dotnet nuget push *.nupkg`` não e push de mais de um arquivo – [#4393](https://github.com/NuGet/Home/issues/4393)

* A saída é envolvida em 80 caracteres no macOS quando redirecionada – [#10198](https://github.com/NuGet/Home/issues/10198)

* A restauração falha com a opção -Source <Relative Path>  -  [#9406](https://github.com/NuGet/Home/issues/9406)

* netcoreapp5.0-windows não faz viagem de ida e volta e não analisar informações da plataforma – [#10177](https://github.com/NuGet/Home/issues/10177)

* Projetos CPS personalizados exigem a funcionalidade do projeto AssemblyReferences para restaurar. - [#8071](https://github.com/NuGet/Home/issues/8071)

* A verificação de existência do arquivo de licença e ícone sempre deve usar uma comparação que faz a confidencialidade de [#9817](https://github.com/NuGet/Home/issues/9817)

* Restaurações dotnetCLiToolReference dificultam a razão sobre projetos não op count/uptodateprojectscount [– #10038](https://github.com/NuGet/Home/issues/10038)

* Difícil ver a caixa de linha tracejada do formato de pacote ao navegar pela guia por meio da caixa de diálogo "Escolher Formato Gerenciador de Pacotes NuGet" no tema Escuro – [#9729](https://github.com/NuGet/Home/issues/9729)

* Excluir referências de estrutura transitiva de `CollectFrameworkReferences`  -  [#10314](https://github.com/NuGet/Home/issues/10314)

* As propriedades estáticas do comparador devem ser idempotentes [– #10339](https://github.com/NuGet/Home/issues/10339)

* resolver o carregamento de assembly de contratos internos (corrigir RPS ou obter exceção) – [#9919](https://github.com/NuGet/Home/issues/9919)

* Substitua GetService por GetServiceAsync em NuGet.Clients, Parte 1 – [#10362](https://github.com/NuGet/Home/issues/10362)

* As instalação da CLI não devem instalar pacotes não listados – [#7466](https://github.com/NuGet/Home/issues/7466)

* Restauração estática do grafo do msbuild – registro em log não desastório sobre MSBuildStartupDirectory – [#10335](https://github.com/NuGet/Home/issues/10335)

* Dependências de projeto de ProjectReferences marcadas como PrivateAssets não devem ser incluídas na verificação atualizada do arquivo de bloqueio – [#8565](https://github.com/NuGet/Home/issues/8565)

* Projetos do SDK com dados ruins que não mostram erros de restauração no VS – [#10406](https://github.com/NuGet/Home/issues/10406)

* NU1004 ao restaurar uma solução que tenha projetos herdados mistos e netstandard2 da linha cmd com LockedMode – [#9623](https://github.com/NuGet/Home/issues/9623)

* O pacote inclui o conteúdo trazido por meio de pacotes de dependência para o pacote do projeto atual (somente projetos baseados em SDK) – [#8867](https://github.com/NuGet/Home/issues/8867)

* Adicionar telemetria para falhas da API de extensibilidade do VS do NuGet – [#10062](https://github.com/NuGet/Home/issues/10062)

* Adicione GenerateRestoreGraphFile na restauração de grafo estático para melhorar a depuração.  - [#10365](https://github.com/NuGet/Home/issues/10365)

* Não é possível abrir o Gerenciador de Pacotes NuGet [– #10336](https://github.com/NuGet/Home/issues/10336)

* O NVDA/Narrador não está lendo o rótulo "Licença" para o link "Apache-2.0" [– #10425](https://github.com/NuGet/Home/issues/10425)

* A mensagem da barra de status atualizada não é excelente no VS – [#9402](https://github.com/NuGet/Home/issues/9402)

* packages.config package.lock.json usa uma estrutura de destino incorreta – [#10257](https://github.com/NuGet/Home/issues/10257)

* Codespaces: corrigir telemetria https://github.com/NuGet/NuGet.Client/pull/3786  -  [de #10439](https://github.com/NuGet/Home/issues/10439)

* O erro NU1004 desaparece ao criar a solução depois de habilitá-lo como "RestoreLockedMode" [– #8973](https://github.com/NuGet/Home/issues/8973)

* A tabulação pelo PMUI no sentido inverso deve espelhar a direção para [frente – #10234](https://github.com/NuGet/Home/issues/10234)

* A depuração do PMUI na Instância Experimental às vezes lança InvalidCastException de SolutionView para ProjectView – [#10416](https://github.com/NuGet/Home/issues/10416)

* A versão padrão é nula depois de clicar em um pacote preterido na guia Procurar – [#10380](https://github.com/NuGet/Home/issues/10380)

* O gerenciador do NuGet Visual Studio recarrega quando o foco é recuperado – [#4176](https://github.com/NuGet/Home/issues/4176)

* Remover IPackageSourceProvider2 e tipos relacionados – [#10098](https://github.com/NuGet/Home/issues/10098)

* O pacote 'NameOfPackage' é incompatível com as estruturas 'all' no projeto – [#5127](https://github.com/NuGet/Home/issues/5127)

* CreateVersionsAsync faz comparações desnecessárias do NuGetVersion – [#10436](https://github.com/NuGet/Home/issues/10436)

* O NuGet.Client deve substituir o uso de ManagedImageMonikers por KnownMonikers – [#9977](https://github.com/NuGet/Home/issues/9977)

* O ícone preterido se sobrepõe à versão do pacote preterido na guia Procurar – [#10452](https://github.com/NuGet/Home/issues/10452)

* O tratamento de erro PackageReference NU1604 é diferente no VS e na linha de comando (restaurar & Gerenciador de Pacotes interface do usuário) – [#9289](https://github.com/NuGet/Home/issues/9289)

* Codespaces: formattters necessários não registrados – [#10467](https://github.com/NuGet/Home/issues/10467)

* Remover net45 como uma estrutura de destino do NuGet.Frameworks – [#10470](https://github.com/NuGet/Home/issues/10470)

* Implementação – adicione novas telemetrias para acompanhar eventos relacionados ao uso do PMC e do PowerShell. - [#10142](https://github.com/NuGet/Home/issues/10142)

* Somente um pacote aparece na janela Visualizar Alterações quando há vários pacotes disponíveis para atualização na interface do usuário do Gerenciador de Pacotes – [#10483](https://github.com/NuGet/Home/issues/10483)

* Os grupos frameworkReferences vazios devem ser gerados ao empacotar projetos multiplatafe – [#10218](https://github.com/NuGet/Home/issues/10218)

* É difícil ver a caixa de seleção do pacote na guia 'Atualizações' com uma caixa de linha tracejada ao navegar pela Guia em Azul/Azul (Contraste Extra)/Temas claros [– #8963](https://github.com/NuGet/Home/issues/8963)

* As caixas de seleção Da guia Atualizações não funcionam bem com leitores de tela – [#10449](https://github.com/NuGet/Home/issues/10449)

* A atualização no PMUI faz com que a referência de objeto não seja definida como uma instância de um [objeto – #9882](https://github.com/NuGet/Home/issues/9882)

* Implementação – adicione novas telemetrias para acompanhar eventos relacionados ao PMC e ao acompanhamento de uso do PowerShell. - [#10478](https://github.com/NuGet/Home/issues/10478)

* Erro de copiar e colar em V2FeedPackageInfo – [#10480](https://github.com/NuGet/Home/issues/10480)

* Correção de NuGetPackageFileService – use usando para [#10503](https://github.com/NuGet/Home/issues/10503) de MemoryStream descartáveis

**[Lista de todos os problemas corrigidos nesta versão-5.9.0](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f6be8c10485c0236b7ef889)**

**[Lista de confirmações nesta versão-5.9.0](https://github.com/NuGet/NuGet.Client/compare/5.8.1.7021...5.9.0.7134)**

### <a name="community-contributions"></a>Contribuições da comunidade

Obrigado a todos os colaboradores que ajudaram a tornar esta versão do NuGet incrível!

|Quem|PRs|Problemas|
|----|----|----|
[omajid](https://github.com/omajid) | [3865](https://github.com/NuGet/NuGet.Client/pull/3865) | Copiar-colar erro em V2FeedPackageInfo- [#10480](https://github.com/NuGet/Home/issues/10480)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3812](https://github.com/NuGet/NuGet.Client/pull/3812) | Testes ausentes para o caso em que os pacotes são referenciados com PrivateAssets = atributo "All"- [#10397](https://github.com/NuGet/Home/issues/10397)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3739](https://github.com/NuGet/NuGet.Client/pull/3739) | Adicionando suporte para enviar vários pacotes por push- [#4393](https://github.com/NuGet/Home/issues/4393)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3723](https://github.com/NuGet/NuGet.Client/pull/3723) | A compilação de bibliotecas NuGet é interrompida quando a assinatura de assembly está desabilitada- [#10173](https://github.com/NuGet/Home/issues/10173)
[kant2002](https://github.com/kant2002) | [3807](https://github.com/NuGet/NuGet.Client/pull/3807) | Limpar os documentos de contribuição- [#10399](https://github.com/NuGet/Home/issues/10399)
[PathogenDavid](https://github.com/PathogenDavid) | [3754](https://github.com/NuGet/NuGet.Client/pull/3754) | A verificação de existência de arquivos de licença e ícone sempre deve usar uma comparação que diferencia maiúsculas de minúsculas- [#9817](https://github.com/NuGet/Home/issues/9817)
[campersau](https://github.com/campersau) | [3677](https://github.com/NuGet/NuGet.Client/pull/3677) | Use BitmapCreateOptions. IgnoreColorProfile para solucionar problemas do WPF ao usar o DecodePixelWidth- [#10037](https://github.com/NuGet/Home/issues/10037)
[bjorkstromm](https://github.com/bjorkstromm) | [3697](https://github.com/NuGet/NuGet.Client/pull/3697) | O link do SDK do Windows 10 está quebrado no guia de contribuição do NuGet. cliente- [#10099](https://github.com/NuGet/Home/issues/10099)
[bjorkstromm](https://github.com/bjorkstromm) | [3696](https://github.com/NuGet/NuGet.Client/pull/3696) | Os links relativos são quebrados no guia de depuração NuGet. Client- [#10100](https://github.com/NuGet/Home/issues/10100)
[Nirmal4G](https://github.com/Nirmal4G) | [3637](https://github.com/NuGet/NuGet.Client/pull/3637) | Melhorar os acessórios de teste e o código relacionado [#9996](https://github.com/NuGet/Home/issues/9996)
[rolfbjarne](https://github.com/rolfbjarne) | [3743](https://github.com/NuGet/NuGet.Client/pull/3743) | A saída é encapsulada a 80 caracteres no macOS quando Redirecionado- [#10198](https://github.com/NuGet/Home/issues/10198)
[xen2](https://github.com/xen2) | [2861](https://github.com/NuGet/NuGet.Client/pull/2861) | Tornar o NuGet. PackageManagement disponível como um pacote .NET Standard- [#6150](https://github.com/NuGet/Home/issues/6150)
[Anipik](https://github.com/Anipik) | [3810](https://github.com/NuGet/NuGet.Client/pull/3810) | Introduzir uma nova propriedade do MSBuild para excluir a saída da compilação para tfms específicas durante a tarefa do pacote- [#10396](https://github.com/NuGet/Home/issues/10396)

## <a name="summary-whats-new-in-591"></a>Resumo: o que há de novo no 5.9.1

* "dotnet NuGet remove Source nuget.org" não funciona na primeira vez que [#10745](https://github.com/NuGet/Home/issues/10745)
* Tornar a validação padrão desabilitada no Linux, mas habilitada por padrão no Windows- [#10713](https://github.com/NuGet/Home/issues/10713)

**[Lista de todos os problemas corrigidos nesta versão-5.9.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f42efd068017639b4036)**

**[Lista de confirmações nesta versão-5.9.1](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.9.1.8)**

## <a name="known-issues"></a>Problemas conhecidos

### <a name="nuget-59-pack-raises-null-reference-exception---10685"></a>o pacote NuGet 5,9 gera uma `Null Reference` exceção. - [#10685](https://github.com/NuGet/Home/issues/10685)

#### <a name="issue"></a>Problema
Quando a aString `pack` usar um `.nuspec` arquivo, `NuGet 5.9` a versão gerará uma `null reference` exceção se [referências de assembly explícitas](../reference/nuspec.md#explicit-assembly-references) forem especificadas sem adicionar nenhum `reference groups` para projetos destinados `multiple frameworks` .

#### <a name="workaround"></a>Solução alternativa
Use `nuget.exe` [5.8.1](https://dist.nuget.org/win-x86-commandline/v5.8.1/nuget.exe)  ou versão mais recente diferente de `5.9.1` .

## <a name="feedback-welcome"></a>Comentários de boas-vindas

Seus comentários são importantes para nós.  Se houver problemas com esta versão, verifique os problemas do [GitHub](https://github.com/NuGet/Home/issues) e a [comunidade de desenvolvedores do Visual Studio](https://developercommunity.visualstudio.com/) para obter os problemas existentes.  Para novos problemas no NuGet, informe um [problema do GitHub](https://github.com/NuGet/Home/issues/new).
Para problemas gerais de experiência do NuGet, informe-nos por meio do [relatório uma opção de problema](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) encontrada em seu IDE favorito em **ajuda > relatar um problema**.
