---
title: Notas de versão do NuGet 5,9
description: Notas de versão do NuGet 5,9, incluindo novos recursos, correções de bugs e DCRs.
author: erdembayar
ms.author: eryondon
ms.date: 3/11/2021
ms.topic: conceptual
ms.openlocfilehash: 24933ebb51851da2583b03e7fd3e55fade5e8a18
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859547"
---
# <a name="nuget-59-release-notes"></a>Notas de versão do NuGet 5,9

Veículos de distribuição do NuGet:

| Versão do NuGet | Disponível na versão do Visual Studio | Disponível em SDKs do .NET |
|:---|:---|:---|
| [**5.9**](https://nuget.org/downloads) | [Visual Studio 2019 versão 16,9](https://visualstudio.microsoft.com/downloads/) | [5,0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> instalado com o Visual Studio 2019 com carga de trabalho do .NET Core
  
> [!NOTE]
> O Visual Studio 16,9, o MSBuild 16,9 e o .NET 5.0.3 + exigem NuGet.exe 5,9 ou posterior.

## <a name="summary-whats-new-in-59"></a>Resumo: o que há de novo no 5,9

* Adicionar item de menu de contexto "atualizar" para dependências de pacote que inicia a interface do usuário do Gerenciador de pacotes com pacotes predefinidos para atualizar- [#10378](https://github.com/NuGet/Home/issues/10378)

    ![Clique com o botão direito do mouse em experiência de "atualização" do pacote](media/releasenotes-59-update.png)

* Mostre a versão solicitada (incluindo a versão flutuante ou a solicitação de intervalo de versão) na coluna "versão" da lista de projetos na interface do usuário do Gerenciador de pacotes de nível de solução- [#9827](https://github.com/NuGet/Home/issues/9827)

    ![Versão solicitada na interface do usuário do Gerenciador de pacotes de nível de solução](media/releasenotes-59-requested-version.png)

* Sugestões de pacote IntelliCode na guia de navegação da interface do usuário do Gerenciador de pacotes liberada como um teste A/B [#10053](https://github.com/NuGet/Home/issues/10053)

* Estenda o `.nupkg.metadata` arquivo para incluir a fonte de instalação- [#10354](https://github.com/NuGet/Home/issues/10354)

* Introduzir uma nova propriedade do MSBuild para excluir a saída da compilação para TFMs específicas durante a tarefa do pacote- [#10396](https://github.com/NuGet/Home/issues/10396)

### <a name="issues-fixed-in-this-release"></a>Problemas corrigidos nesta versão

**DCRs (solicitação de alteração de Design):**

* O ícone de ícone para baixo quando a versão mais recente do pacote é instalada não é intuitivo. A marca verde antiga foi perfeita- [#9789](https://github.com/NuGet/Home/issues/9789)

* O detalhamento de depuração do NuGet deve dizer de onde veio um pacote- [#3055](https://github.com/NuGet/Home/issues/3055)

* O pacote NuGet deve capturar a omissão incorreta do ponto nos números de versão- [#9215](https://github.com/NuGet/Home/issues/9215)

* [CPVM] Desabilitar fixação das dependências transitivas centrais- [#10132](https://github.com/NuGet/Home/issues/10132)

* net5 TFM: produz erro quando falta TPV- [#9441](https://github.com/NuGet/Home/issues/9441)

* Registrar o pacote contenthash durante o log de restauração (durante a extração)- [#10384](https://github.com/NuGet/Home/issues/10384)

* Implementar um mecanismo de pré-registro para projetos de RP existentes que chamam a restauração na solução aberta- [#9986](https://github.com/NuGet/Home/issues/9986)

* O recomendador de pacote NuGet deve funcionar quando mais de uma fonte for selecionada no Gerenciador de pacotes- [#10433](https://github.com/NuGet/Home/issues/10433)

* Ao restaurar em detalhes normais, registre em qual fonte um pacote está sendo restaurado- [#10461](https://github.com/NuGet/Home/issues/10461)

**Soluciona**

* INuGetPackageFileService-buscar imagens e licenças incorporadas para Codespaces e autônomos- [#10151](https://github.com/NuGet/Home/issues/10151)

* VS OE: IProjectMetadataContextInfo com formatador ausente- [#10079](https://github.com/NuGet/Home/issues/10079)

* [CPVM-perf] Reduzir as informações gravadas no centralTransitiveDependencyGroups- [#10002](https://github.com/NuGet/Home/issues/10002)

* As operações de restauração que geram devido a um projeto que não está sendo carregado são relatadas como `NoOp` em telemetria- [#9985](https://github.com/NuGet/Home/issues/9985)

* Os ícones com determinados paletes de cores fazem com que a IU de PM falhe em vez de [#10037](https://github.com/NuGet/Home/issues/10037)

* [CPVM-perf] Reduzir o clone do especificação ao adicionar as informações do CPVM- [#10003](https://github.com/NuGet/Home/issues/10003)

* Interface do usuário da PM-ícone asyncify carregando- [#10009](https://github.com/NuGet/Home/issues/10009)

* Atraso da interface do usuário ao carregar URLs de ícone na interface do usuário do PM- [#8505](https://github.com/NuGet/Home/issues/8505)

* Afinidade de thread em threads de interface de usuário do BitmapSource e do WPF- [#9161](https://github.com/NuGet/Home/issues/9161)

* Aviso para NU5128 de aviso quando packastool com alias TargetFramework- [#10097](https://github.com/NuGet/Home/issues/10097)

* A lógica OutputPath em destinos de pacotes em uma compilação personalizada não funciona corretamente- [#9234](https://github.com/NuGet/Home/issues/9234)

* VS OE: cache de instância de IServiceBroker no cliente- [#10141](https://github.com/NuGet/Home/issues/10141)

* Tornar a criação de NuGetProjectActions para desinstalação do PM interface do usuário uma operação paralela- [#9956](https://github.com/NuGet/Home/issues/9956)

* Desempenho: reduzir UIDelays em GetPackageSpecsAsync para projetos herdados e projetos que não são de PR- [#9953](https://github.com/NuGet/Home/issues/9953)

* ``dotnet nuget push *.nupkg`` não envia mais de um arquivo- [#4393](https://github.com/NuGet/Home/issues/4393)

* A saída é encapsulada a 80 caracteres no macOS quando Redirecionado- [#10198](https://github.com/NuGet/Home/issues/10198)

* Falha na restauração com-source <Relative Path>  -  [#9406](https://github.com/NuGet/Home/issues/9406)

* netcoreapp 5.0-o Windows não faz a viagem de ida e volta e não analisa as informações da plataforma- [#10177](https://github.com/NuGet/Home/issues/10177)

* Projetos personalizados do CPS exigem a funcionalidade de projeto AssemblyReferences para restaurar. - [#8071](https://github.com/NuGet/Home/issues/8071)

* A verificação de existência de arquivos de licença e ícone sempre deve usar uma comparação que diferencia maiúsculas de minúsculas- [#9817](https://github.com/NuGet/Home/issues/9817)

* As restaurações do DotnetCLiToolReference dificultam o motivo da contagem de projetos sem operação/uptodateprojectscount- [#10038](https://github.com/NuGet/Home/issues/10038)

* É difícil ver a caixa de linha tracejada do formato do pacote ao navegar por Tab por meio do diálogo "escolher formato do Gerenciador de pacotes NuGet" em tema escuro- [#9729](https://github.com/NuGet/Home/issues/9729)

* Excluir referências de estrutura transitivas de `CollectFrameworkReferences`  -  [#10314](https://github.com/NuGet/Home/issues/10314)

* As propriedades estáticas do comparador devem ser idempotentes- [#10339](https://github.com/NuGet/Home/issues/10339)

* resolver o carregamento do assembly de contratos internos (corrigir RPS ou obter exceção)- [#9919](https://github.com/NuGet/Home/issues/9919)

* Substitua GetService por GetServiceAsync em NuGet. clients, parte 1- [#10362](https://github.com/NuGet/Home/issues/10362)

* As instalações da CLI não devem instalar pacotes não listados- [#7466](https://github.com/NuGet/Home/issues/7466)

* Log estático do MSBuild Restore-unnnecessary Logging sobre MSBuildStartupDirectory- [#10335](https://github.com/NuGet/Home/issues/10335)

* As dependências do projeto ProjectReferences marcadas como PrivateAssets não devem ser incluídas na verificação do arquivo de bloqueio até a data [#8565](https://github.com/NuGet/Home/issues/8565)

* Projetos do SDK com dados inválidos que não mostram erros de restauração no VS- [#10406](https://github.com/NuGet/Home/issues/10406)

* NU1004 ao restaurar uma solução que tem projetos herdados e netstandard2 misturados da linha cmd com o Lockedmode- [#9623](https://github.com/NuGet/Home/issues/9623)

* O pacote inclui o conteúdo trazido por meio de pacotes de dependências para o pacote do projeto atual (somente em projetos baseados em SDK)- [#8867](https://github.com/NuGet/Home/issues/8867)

* Adicionar telemetria para falhas da API de extensibilidade VS do NuGet- [#10062](https://github.com/NuGet/Home/issues/10062)

* Adicione GenerateRestoreGraphFile na restauração estática do grafo para melhorar a depuração.  - [#10365](https://github.com/NuGet/Home/issues/10365)

* Não é possível abrir o Gerenciador de pacotes NuGet- [#10336](https://github.com/NuGet/Home/issues/10336)

* O NVDA/Narrator não está lendo o rótulo "licença" para o link "Apache-2,0" [#10425](https://github.com/NuGet/Home/issues/10425)

* A mensagem da barra de status atualizada não é ótima no VS- [#9402](https://github.com/NuGet/Home/issues/9402)

* packages.config package.lock.jsno usa uma estrutura de destino incorreta- [#10257](https://github.com/NuGet/Home/issues/10257)

* Codespaces: corrigir telemetria de https://github.com/NuGet/NuGet.Client/pull/3786  -  [#10439](https://github.com/NuGet/Home/issues/10439)

* Erro NU1004 desaparece ao compilar a solução depois de habilitar "RestoreLockedMode"- [#8973](https://github.com/NuGet/Home/issues/8973)

* A Tabulação por meio de PMUI no inverso deve direcionar a direção do espelho- [#10234](https://github.com/NuGet/Home/issues/10234)

* A depuração de PMUI na instância experimental às vezes lança a InvalidCastException de SolutionView para ProjectView- [#10416](https://github.com/NuGet/Home/issues/10416)

* A versão padrão é NULL depois de clicar em um pacote preterido na guia procurar- [#10380](https://github.com/NuGet/Home/issues/10380)

* O Gerenciador do NuGet no Visual Studio recarrega quando o foco é reobtido- [#4176](https://github.com/NuGet/Home/issues/4176)

* Remover IPackageSourceProvider2 e tipos relacionados- [#10098](https://github.com/NuGet/Home/issues/10098)

* O pacote ' NameOfPackage ' é incompatível com as estruturas ' all' no projeto- [#5127](https://github.com/NuGet/Home/issues/5127)

* CreateVersionsAsync faz a NuGetVersion de comparação desnecessária- [#10436](https://github.com/NuGet/Home/issues/10436)

* O NuGet. Client deve substituir o uso de ManagedImageMonikers por KnownMonikers- [#9977](https://github.com/NuGet/Home/issues/9977)

* O ícone preterido se sobrepõe à versão do pacote preterido na guia procurar- [#10452](https://github.com/NuGet/Home/issues/10452)

* O tratamento de erros do PackageReference NU1604 é diferente em relação à VS e à linha de comando (restaurar & interface do usuário do Gerenciador de pacotes)- [#9289](https://github.com/NuGet/Home/issues/9289)

* Codespaces: formatadores necessários não registrados- [#10467](https://github.com/NuGet/Home/issues/10467)

* Remover Net45 como uma estrutura de destino do NuGet. frameworks- [#10470](https://github.com/NuGet/Home/issues/10470)

* Implementação-Adicione novos telemetrias para acompanhar eventos relacionados ao uso do PMC e do PowerShell. - [#10142](https://github.com/NuGet/Home/issues/10142)

* Somente um pacote é mostrado na janela de visualização de alterações quando há vários pacotes disponíveis para atualização na interface do usuário do Gerenciador de pacotes- [#10483](https://github.com/NuGet/Home/issues/10483)

* Grupos de frameworkReferences vazios devem ser gerados ao empacotar projetos multidirecionados- [#10218](https://github.com/NuGet/Home/issues/10218)

* É difícil ver a caixa de seleção do pacote na guia ' atualizações ' concentra-se em uma caixa de linha tracejada ao navegar pela guia em azul/azul (contraste extra) temas de/Light- [#8963](https://github.com/NuGet/Home/issues/8963)

* As caixas de seleção da guia Atualizações não funcionam bem com leitores de tela- [#10449](https://github.com/NuGet/Home/issues/10449)

* A atualização no PMUI faz com que a referência de objeto não seja definida como uma instância de um objeto- [#9882](https://github.com/NuGet/Home/issues/9882)

* Implementação-Adicione novos telemetrias para acompanhar eventos relacionados ao uso do PMC e do PowerShell. - [#10478](https://github.com/NuGet/Home/issues/10478)

* Copiar-colar erro em V2FeedPackageInfo- [#10480](https://github.com/NuGet/Home/issues/10480)

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

## <a name="feedback-welcome"></a>Comentários de boas-vindas

Seus comentários são importantes para nós.  Se houver problemas com esta versão, verifique os problemas do [GitHub](https://github.com/NuGet/Home/issues) e a [comunidade de desenvolvedores do Visual Studio](https://developercommunity.visualstudio.com/) para obter os problemas existentes.  Para novos problemas no NuGet, informe um [problema do GitHub](https://github.com/NuGet/Home/issues/new).
Para problemas gerais de experiência do NuGet, informe-nos por meio do [relatório uma opção de problema](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) encontrada em seu IDE favorito em **ajuda > relatar um problema**.
