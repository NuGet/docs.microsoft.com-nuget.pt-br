---
title: Notas de versão do NuGet 1,0 e 1,1
description: Notas de versão do NuGet 1,1 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cdd4bad54b08d956dbfdaf54220971492fd3ab02
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777208"
---
# <a name="nuget-10-and-11-release-notes"></a>Notas de versão do NuGet 1,0 e 1,1

[Notas de versão do NuGet 1,2](../release-notes/nuget-1.2.md)

O NuGet 1,0 foi lançado em 13 de janeiro de 2011.  O NuGet 1,1 foi lançado em 12 de fevereiro de 2011.

## <a name="overview"></a>Visão geral

Este documento contém as notas de versão para as várias versões do NuGet 1,0 agrupadas de acordo com a versão de visualização principal.

O NuGet inclui os seguintes componentes:

* *NuGet. Tools. vsix* * que consiste em:
  * Caixa de diálogo **Adicionar pacote de biblioteca** * no Visual Studio usado para procurar e instalar pacotes.
  * **Console do Gerenciador de pacotes** * console baseado no PowerShell no Visual Studio.
* Ferramenta de *linha de comando do NuGet* * ferramenta usada para criar (e eventualmente publicar) pacotes.

A extensão do Visual Studio das ferramentas do NuGet (*NuGet. Tools. vsix*) requer:

* Visual Studio 2010 ou Visual Web Developer 2010 Express.

A ferramenta de linha de comando do NuGet requer:

* .NET Framework versão 4

## <a name="installation"></a>Instalação

Para usar esta [versão mais recente](http://nuget.codeplex.com/releases/view/52018):

* Primeiro, desinstale o Build mais antigo. Você precisa executar o VS como administrador para fazer isso.
* Remova todos os feeds existentes que você tem.
* Adicione um novo feed apontando para <https://go.microsoft.com/fwlink/?LinkId=206669> .

## <a name="nuget-11"></a>NuGet 1.1

A lista de problemas corrigidos nesta versão [pode ser encontrada aqui](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>NuGet 1,0 RTM

Um problema foi corrigido para o RTM desde o RC.

* [Problema 474: a remoção de pacotes afeta todos os projetos na solução](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>Release Candidate

A seguir estão as alterações feitas nesta versão Release Candidate desde o CTP 2. Visite o Issue Tracker para ver a lista completa de bugs.

* [A atualização do pacote do console não atualiza as dependências.](http://nuget.codeplex.com/workitem/443)
* [Adicionando a referência de pacote de compartimentos de lista de seleção sem pacote (CTP1)](http://nuget.codeplex.com/workitem/442)
* [A atualização de um pacote deixa referências quebradas](http://nuget.codeplex.com/workitem/440)
* [Get-Package-updates falha na caixa de diálogo ou quando a fonte de agregação ' all' é selecionada no console](http://nuget.codeplex.com/workitem/439)
* [Obtendo erros de verificação de pacote](http://nuget.codeplex.com/workitem/426)
* [Avisar os usuários quando um pacote não puder ser instalado na caixa de diálogo Adicionar pacote](http://nuget.codeplex.com/workitem/425)
* [Get-Package-updates lança ao atualizar um grande número de pacotes](http://nuget.codeplex.com/workitem/424)
* [Melhorar o tratamento de erros quando arquivos nuspec forem criados incorretamente](http://nuget.codeplex.com/workitem/423)
* [O NuGet Pack ignora os arquivos especificados](http://nuget.codeplex.com/workitem/422)
* [Removendo a origem do segundo pacote e clicando em "mover para baixo" falha VS](http://nuget.codeplex.com/workitem/418)
* [Remover referência de assembly ao instalar pacotes](http://nuget.codeplex.com/workitem/413)
* [InvalidOperationException ao abrir a caixa de diálogo Configurações](http://nuget.codeplex.com/workitem/411)
* [A chave de acesso para a origem do pacote no console do Gerenciador de pacotes não funciona](http://nuget.codeplex.com/workitem/410)
* [As chaves de acesso da caixa de diálogo Configurações do NuGet VS dão foco a campos errados](http://nuget.codeplex.com/workitem/409)
* [A ID do pacote IntelliSense não deve consultar muitos itens](http://nuget.codeplex.com/workitem/404)
* [Falha ao adicionar pacote ao projeto com um caractere de ponto no nome do projeto](http://nuget.codeplex.com/workitem/403)
* [Problema com os arquivos especificados no nuspec](http://nuget.codeplex.com/workitem/400)
* [O feed oficial correto deve ser registrado ao usar a compilação mais recente](http://nuget.codeplex.com/workitem/399)
* [As marcas devem usar espaços em vez de #](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata não tem algumas informações úteis](http://nuget.codeplex.com/workitem/388)
* [Adicionar link de abuso de relatório à caixa de diálogo](http://nuget.codeplex.com/workitem/386)
* [Usando App_Data para descompactar as quebras de pacotes no Visual Studio](http://nuget.codeplex.com/workitem/380)
* [Implementar marcas](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder permite a criação de um pacote vazio sem dependências](http://nuget.codeplex.com/workitem/373)
* [Adicionar o campo proprietários para o pacote](http://nuget.codeplex.com/workitem/365)
* [Atualizar o manifesto do VSIX para dizer o Gerenciador de pacotes NuGet em vez das ferramentas VSIX](http://nuget.codeplex.com/workitem/364)
* [O comando Get-Package gera um erro quando todas as fontes são selecionadas](http://nuget.codeplex.com/workitem/359)
* [Caixa de diálogo permitir a ordenação de fontes de pacote no Options](http://nuget.codeplex.com/workitem/356)
* [Update-Package não remove a versão mais antiga](http://nuget.codeplex.com/workitem/352)
* [Implementar a especificação do intervalo de versões para dependências](http://nuget.codeplex.com/workitem/347)
* [O Visual Studio falha ao clicar em "Adicionar novo pacote"](http://nuget.codeplex.com/workitem/346)
* [Exibir downloads e classificações na caixa de diálogo Adicionar pacote](http://nuget.codeplex.com/workitem/345)
* [A alteração entre as origens do pacote na caixa de diálogo não atualiza o código-fonte ativo](http://nuget.codeplex.com/workitem/344)
* [Remover associação de chave da janela do console do Gerenciador de pacotes](http://nuget.codeplex.com/workitem/339)
* [O pacote de instalação não é reconhecido como o nome de um cmdlet...](http://nuget.codeplex.com/workitem/338)
* [Instalando um pacote de um feed local as dependências em feeds normais não são resolvidas](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies deve ignorar as dependências que ainda estão em uso](http://nuget.codeplex.com/workitem/331)
* [Se o cancelamento da navegação de página, o usuário não poderá navegar para uma página diferente enquanto a solicitação de página original retorna](http://nuget.codeplex.com/workitem/325)
* [Investigue o desempenho do NuPack. Server para fornecer feeds com um grande número de pacotes.](http://nuget.codeplex.com/workitem/324)
* [Na segunda vez que eu filtro para um pacote, ele usa a origem do pacote "New", em vez da origem selecionada anteriormente.](http://nuget.codeplex.com/workitem/321)
* [A origem do pacote padrão deve ser selecionada ao selecionar a guia "online" na caixa de diálogo.](http://nuget.codeplex.com/workitem/320)
* [O pacote de lista deve mostrar os pacotes instalados por padrão](http://nuget.codeplex.com/workitem/309)
* [Referência de assembly HintPaths](http://nuget.codeplex.com/workitem/294)
* [Exceção ao abrir o console do Gerenciador de pacotes](http://nuget.codeplex.com/workitem/268)
* [O console IntelliSense baixa o feed inteiro](http://nuget.codeplex.com/workitem/259)
* [A origem do pacote ' default ' deve ser renomeada para ' active '](http://nuget.codeplex.com/workitem/258)
* [Interface do usuário de origens do pacote: pressionar OK deve adicionar a nova origem se os campos nome/fonte não estiverem vazios](http://nuget.codeplex.com/workitem/257)
* [A caixa de diálogo torna-se super lenta quando o número de pacotes instalados é grande](http://nuget.codeplex.com/workitem/243)
* [Dar suporte a redirecionamentos de associação para assemblies com nome forte](http://nuget.codeplex.com/workitem/238)
* [Adicionar referência de pacote... Interface do usuário para incluir a lista suspensa para a origem do pacote](http://nuget.codeplex.com/workitem/226)
* [O NuPack precisa dar suporte à transformação de configuração de forma independente do nome do arquivo de configuração](http://nuget.codeplex.com/workitem/224)
* [Permite que o BasePath seja substituído em NuPack.exe](http://nuget.codeplex.com/workitem/222)
* [Comportamento de fallback de origem do pacote](http://nuget.codeplex.com/workitem/204)
* [Falha na GUI](http://nuget.codeplex.com/workitem/201)
* [Caixa de diálogo adicionar opções de classificação para adicionar pacote](http://nuget.codeplex.com/workitem/179)
* [tecla de atalho para limpar o console do Gerenciador de pacotes](http://nuget.codeplex.com/workitem/174)
* [PowerConsole faz com que o console do NuPack falhe](http://nuget.codeplex.com/workitem/166)
* [A caixa de diálogo console e adicionar pacote deve definir o agente do usuário em solicitações](http://nuget.codeplex.com/workitem/141)
* [Defina o número de versão do VSIX e NuPack.exe na compilação.](http://nuget.codeplex.com/workitem/134)
* [Ocultar parâmetros comuns do PowerShell de-?](http://nuget.codeplex.com/workitem/118)
* [Adição-ajuda detalhada para comandos do console](http://nuget.codeplex.com/workitem/110)
* [A caixa de diálogo Adicionar pacote deve permitir a escolha da origem do pacote atual](http://nuget.codeplex.com/workitem/88)
* [Mover classes NuPack. Core para namespaces diferentes](http://nuget.codeplex.com/workitem/50)
* [Adicionar ajuda aos cmdlets](http://nuget.codeplex.com/workitem/23)
* [Verificar o hash do feed após o download do pacote](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

A seguir estão as alterações mais significativas feitas no CTP 2:

* O feed do pacote foi alternado do ATOM para um ponto de extremidade do serviço OData: se você atualizar para a versão CTP2 do NuGet, certifique-se de adicionar a seguinte URL como uma origem do pacote: `https://feed.nuget.org/ctp2/odata/v1/` .
* Renomeou o comando Add-Package para *install-Package*.
* O formato foi atualizado `.nuspec` . O `.nuspec` formato agora inclui o campo *iconUrl* para especificar um ícone de formato png de 32x32 que aparecerá na caixa de diálogo Adicionar pacote. Portanto, certifique-se de definir isso para distinguir seu pacote. O `.nuspec` formato também inclui o novo campo *projectUrl* que você pode usar para apontar para uma página da Web que fornece mais informações sobre o pacote.

Essa compilação não funcionará com `.nupkg` arquivos antigos. Se você obtiver exceções de referência nulas, estará usando um `.nupkg` arquivo antigo e precisará reconstruí-lo com a [ferramenta de linha de comando do NuGet](http://nuget.codeplex.com/releases/52017/download/165468)atualizada.

Veja a seguir uma lista de recursos e bugs que foram corrigidos para o NuGet CTP 2 (não inclui bugs para limpezas de código secundárias, etc.).

* [Erro ao desempacotar assemblies de pacote quando especificar TargetFramework para um assembly.](http://nuget.codeplex.com/workitem/10)
* [Tornar a janela do console do NuPack mais detectável](http://nuget.codeplex.com/workitem/14)
* [ILMerge a versão de nupack.exe](http://nuget.codeplex.com/workitem/19)
* [Melhor manipulação de erros/exceções](http://nuget.codeplex.com/workitem/24)
* [[Nupack. Core]: PackageManager deve tratar normalmente erros relacionados ao feed](http://nuget.codeplex.com/workitem/28)
* [Precisa de um novo ícone para o console](http://nuget.codeplex.com/workitem/29)
* [Localizar cadeias de caracteres na caixa de diálogo](http://nuget.codeplex.com/workitem/38)
* [Caches NuPack baixados. NuPack arquivos na memória](http://nuget.codeplex.com/workitem/40)
* [Console do NuPack: alterar o atalho padrão para exibir o console](http://nuget.codeplex.com/workitem/48)
* [ProjectSystem deve dar suporte a valores padrão para propriedades comuns](http://nuget.codeplex.com/workitem/49)
* [A execução de nupack.exe em uma pasta com apenas um arquivo nuspec deve usar o nuspec](http://nuget.codeplex.com/workitem/52)
* [O menu do projeto aparece mesmo quando nenhum projeto/solução é carregado](http://nuget.codeplex.com/workitem/54)
* [o Build. cmd falha em um clone limpo da base de código](http://nuget.codeplex.com/workitem/56)
* [Recurso de atualizações disponíveis](http://nuget.codeplex.com/workitem/57)
* [Caixa de diálogo: adicionar um pacote por meio da caixa de diálogo remove o prompt no console](http://nuget.codeplex.com/workitem/73)
* [A adição de um pacote clicando em ' instalar ' geralmente é lenta, sem nenhum comentário visual](http://nuget.codeplex.com/workitem/80)
* [Não é possível descobrir quais dos meus pacotes instalados têm atualizações.](http://nuget.codeplex.com/workitem/82)
* [Não é possível atualizar um pacote instalado na caixa de diálogo.](http://nuget.codeplex.com/workitem/83)
* [Não é possível desinstalar um pacote instalado na caixa de diálogo](http://nuget.codeplex.com/workitem/84)
* [&ldquo;Adicionar referência &hellip; &rdquo; de pacote aparece no menu de contexto das referências instaladas](http://nuget.codeplex.com/workitem/85)
* [Depois de atualizar um pacote do console do, ele mostra a versão antiga e a nova versão como instalada](http://nuget.codeplex.com/workitem/86)
* [A atividade no console do, ao usar a caixa de diálogo, desaparece após o uso](http://nuget.codeplex.com/workitem/87)
* [Limpar a análise da linha de comando no nupack.exe](http://nuget.codeplex.com/workitem/89)
* [Adicionar um nome amigável às origens do pacote](http://nuget.codeplex.com/workitem/98)
* [Update. nuspec para dar suporte à inclusão de ícones de pacote](http://nuget.codeplex.com/workitem/103)
* [A interface do usuário do feed não permite copiar a URL](http://nuget.codeplex.com/workitem/105)
* [Melhor manipulação de erros de remoção de pacote.](http://nuget.codeplex.com/workitem/107)
* [A digitação na janela do console depende do foco do cursor](http://nuget.codeplex.com/workitem/112)
* [Mensagens de erro parecem horrível](http://nuget.codeplex.com/workitem/116)
* [O desempenho de Remove-Package para um pacote que não está instalado é inválido](http://nuget.codeplex.com/workitem/117)
* [A remoção de um pacote falha quando não há nenhuma origem do pacote](http://nuget.codeplex.com/workitem/119)
* [Remove-Package falha quando a origem do pacote está indisponível](http://nuget.codeplex.com/workitem/120)
* [Adicione o título aos metadados do pacote e ao feed.](http://nuget.codeplex.com/workitem/125)
* [Adicione o parâmetro-source de volta ao Add-Package](http://nuget.codeplex.com/workitem/127)
* [O pacote de lista deve ter um parâmetro-source](http://nuget.codeplex.com/workitem/128)
* [Atualize o NuPack. Server para exigir que o agente do usuário do NuPack Baixe o pacote](http://nuget.codeplex.com/workitem/142)
* [A caixa de diálogo de aceitação da licença deve listar licenças para todas as dependências que exigem aceitação](http://nuget.codeplex.com/workitem/145)
* [Registrar um erro quando um pacote lançar no feed](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe não deve permitir um &lt; elemento licenseurl &gt; vazio](http://nuget.codeplex.com/workitem/152)
* [Renomear List-Package como Get-Package, Add-Package instalar-Package e Remove-Package para desinstalar-Package](http://nuget.codeplex.com/workitem/155)
* [Usando o item de menu Adicionar referência de pacote do navegador de soluções falha no Visual Studio](http://nuget.codeplex.com/workitem/158)
* [O rótulo "fontes de pacote disponíveis" está sem dois-pontos](http://nuget.codeplex.com/workitem/160)
* [Fazer maiúsculas e minúsculas no elemento XML de forma consistente, camel case](http://nuget.codeplex.com/workitem/161)
* [O manifesto do VSIX NuPack precisa ativar o ' admin '](http://nuget.codeplex.com/workitem/162)
* [Se você executar List-Package sem feeds, obterá um erro de referência nulo](http://nuget.codeplex.com/workitem/164)
* [nuget.exe: especificar caminho de destino](http://nuget.codeplex.com/workitem/171)
* [Erros do PowerShell ao abrir Gerenciamento de Pacotes console no WinXP](http://nuget.codeplex.com/workitem/175)
* [VS falha ao tentar carregar a lista de pacotes](http://nuget.codeplex.com/workitem/176)
* [permitir meta pacotes (sem arquivos, somente dependências)](http://nuget.codeplex.com/workitem/180)
* [Converter script do PowerShell para módulo do PowerShell 2,0](http://nuget.codeplex.com/workitem/181)
* [PathResolver deve descartar a parte do caminho que precede os caracteres curinga quando o destino é especificado](http://nuget.codeplex.com/workitem/183)
* [Sem dependências](http://nuget.codeplex.com/workitem/186)
* [Erro ao instalar o ELMAH](http://nuget.codeplex.com/workitem/192)
* [As transformações de configuração não funcionam corretamente com &lt; configSections&gt;](http://nuget.codeplex.com/workitem/194)
* [A variável ' $global:p rojectCache ' não pode ser recuperada porque não foi definida](http://nuget.codeplex.com/workitem/203)
* [Adicionar tarefa MSBuild para criar pacotes NuPack](http://nuget.codeplex.com/workitem/205)
* [o pacote de lista precisa dar suporte à pesquisa/filtragem](http://nuget.codeplex.com/workitem/206)
* [Sempre exibir um link para licença se o autor do pacote fornecer uma URL de licença](http://nuget.codeplex.com/workitem/208)
* [Exceção ocasional "acesso negado" com Remove-Package](http://nuget.codeplex.com/workitem/213)
* [Testes de unidade com falha: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [Permitir um conjunto de arquivos de fallback/padrão se uma versão de estrutura específico não puder ser encontrada](http://nuget.codeplex.com/workitem/223)
* [Adicionar referência de pacote... A interface do usuário não pode remover um pacote](http://nuget.codeplex.com/workitem/225)
* [Adicionar o pacote de falhas de referência de pacotes quando um ou mais projetos são descarregados](http://nuget.codeplex.com/workitem/228)
* [A transformação de configuração não parece funcionar no arquivo web.debug.config](http://nuget.codeplex.com/workitem/229)
* [init.ps1 não disparar no pacote personalizado](http://nuget.codeplex.com/workitem/237)
* [Ao adicionar caminhos à feedlist, o botão padrão é definido como OK, portanto, se eu pressionar ENTER, ele será fechado automaticamente](http://nuget.codeplex.com/workitem/240)
* [A tentativa de desinstalar uma dependência falhará VS. se for tentada 2 vezes em uma linha](http://nuget.codeplex.com/workitem/241)
* [Exibir a URL do projeto na caixa de diálogo Adicionar pacote](http://nuget.codeplex.com/workitem/253)
* [Padrão a caixa de diálogo de Add-Package para pacotes instalados](http://nuget.codeplex.com/workitem/254)
* [Alterar item de menu da caixa de diálogo Adicionar pacote.](http://nuget.codeplex.com/workitem/261)
* [Renomear namespaces e assemblies](http://nuget.codeplex.com/workitem/274)
* [Renomear o projeto NuPack para NuGet](http://nuget.codeplex.com/workitem/282)
* [Adicione o seguinte texto sob a lista de dependências](http://nuget.codeplex.com/workitem/288)
* [Alterar o texto de aceitação da licença na caixa de diálogo de aceitação da licença](http://nuget.codeplex.com/workitem/291)
* [Alterar o texto na caixa de diálogo de aceitação da licença acima da lista de pacotes](http://nuget.codeplex.com/workitem/292)
* [O OData não funciona com uma URL fwlink](http://nuget.codeplex.com/workitem/304)
* [Interface do usuário do Gerenciador de pacotes: em cache agressivo de contagem de pacotes usada para paginação](http://nuget.codeplex.com/workitem/317)
* [NuPack/NuGet- &gt; erro do console do Gerenciador de pacotes](http://nuget.codeplex.com/workitem/335)
* [Caixa de diálogo Adicionar pacote mostra a aceitação da licença para o pacote já instalado](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

Veja a seguir uma lista de recursos e bugs que foram corrigidos para o NuGet CTP 1.

* [A extensão do pacote deve ser renomeada para. nupack](http://nuget.codeplex.com/workitem/1)
* [Mover o arquivo de pacote para a pasta](http://nuget.codeplex.com/workitem/2)
* [Instalação de mesclagem &amp; adicionar comandos do PS](http://nuget.codeplex.com/workitem/3)
* [Criar aliases para Verb-Noun cmdlets](http://nuget.codeplex.com/workitem/4)
* [NuPack fica confuso ao alternar a solução no VS](http://nuget.codeplex.com/workitem/6)
* [Devemos ocultar a pasta de solução ' Packages ' por padrão](http://nuget.codeplex.com/workitem/11)
* [Adicione suporte para substituição de token em itens de conteúdo.](http://nuget.codeplex.com/workitem/12)
* [NuPack. UI deve usar a API do packager](http://nuget.codeplex.com/workitem/26)
* [[Nupack. Core]: PackageManager marca pacotes como instalados antes de instalá-los](http://nuget.codeplex.com/workitem/27)
* [A exclusão do projeto padrão da solução ainda mostra o projeto excluído como padrão](http://nuget.codeplex.com/workitem/30)
* [Falha no novo pacote com "não é possível adicionar parte ao URI especificado porque ele já está no pacote".](http://nuget.codeplex.com/workitem/32)
* [Remover cadeias de caracteres "NuPack" da GUI do Visual Studio](http://nuget.codeplex.com/workitem/35)
* [Adicionar o cabeçalho do Apache a um arquivo de COPYRIGHT.txt](http://nuget.codeplex.com/workitem/36)
* [Remover Update-PackageSource comando](http://nuget.codeplex.com/workitem/37)
* [Gerenciador de pacotes inutilizável ao carregar o perfil gera uma exceção](http://nuget.codeplex.com/workitem/39)
* [init.ps1, install.ps1 e uninstall.ps1 precisam receber estado adicional](http://nuget.codeplex.com/workitem/41)
* [Combinar pacotes de console e GUI em um pacote](http://nuget.codeplex.com/workitem/42)
* [A lógica de transformação XML não funciona se for aplicada a XML que não está na raiz](http://nuget.codeplex.com/workitem/43)
* [Caixa de diálogo Gerenciar configurações de fontes de pacote não atualizando o console do NuPack](http://nuget.codeplex.com/workitem/44)
* [Interface do usuário do console do NuPack: renomear a lista suspensa ' feed do pacote ' para ' origem do pacote '](http://nuget.codeplex.com/workitem/45)
* [Opções do console do NuPack: Renomear ' IU do repositório ' para ser consistente com o console do NuPack](http://nuget.codeplex.com/workitem/46)
* [O Add-Package falha em um site que foi aberto do IIS ou de uma URL](http://nuget.codeplex.com/workitem/53)
* [A origem do Gerenciador de pacotes não funciona com FwLink](http://nuget.codeplex.com/workitem/55)
* [Definir a origem do pacote padrão](http://nuget.codeplex.com/workitem/59)
* [Ao adicionar fontes de pacote em opção, quando apenas uma fonte é fornecida, suponha que é o padrão.](http://nuget.codeplex.com/workitem/60)
* [A interface do usuário da caixa de diálogo mostra pacotes "recentes" falsos](http://nuget.codeplex.com/workitem/62)
* [Opções: clicar em cancelar não cancela as alterações](http://nuget.codeplex.com/workitem/63)
* [A pesquisa de caixa de diálogo Adicionar referência de pacote deve diferenciar maiúsculas de minúsculas](http://nuget.codeplex.com/workitem/65)
* [Corrigir metadados da empresa em arquivos AssemblyInfo.cs](http://nuget.codeplex.com/workitem/67)
* [Número de versão do VSIX](http://nuget.codeplex.com/workitem/71)
* [Remove-Package: using-? exibe a ajuda duas vezes](http://nuget.codeplex.com/workitem/72)
* [Executar pacotes de instalação/desinstalação para pacotes de nível de projeto](http://nuget.codeplex.com/workitem/74)
* [O servidor não pode criar o feed quando um nupack falha na validação](http://nuget.codeplex.com/workitem/90)
* [É necessário substituir os ícones NuPack](http://nuget.codeplex.com/workitem/94)
* [O proxy http NTLM não se autentica no feed de pacote.](http://nuget.codeplex.com/workitem/96)
* [A caixa de diálogo nem sempre começa centralizada na janela VS](http://nuget.codeplex.com/workitem/100)
* [Muitos dos campos em um pacote detalhes não estão sendo populados na caixa de diálogo](http://nuget.codeplex.com/workitem/102)
* [A IU da caixa de diálogo não mostra os nomes dos autores](http://nuget.codeplex.com/workitem/108)
* [Por que versão para Remove-Package](http://nuget.codeplex.com/workitem/113)
* [Remover a guia recente na interface do usuário da caixa de diálogo](http://nuget.codeplex.com/workitem/115)
* [Falha do VS ao clicar com o botão direito do mouse na pasta da solução depois de abrir a IU da caixa de diálogo pelo menos](http://nuget.codeplex.com/workitem/126)
* [Alterar o parâmetro-local de List-Package para-instalado](http://nuget.codeplex.com/workitem/129)
* [Renomear packages.xml para NuPack.config](http://nuget.codeplex.com/workitem/132)
* [O console força o cursor até o fim da linha](http://nuget.codeplex.com/workitem/135)
* [O IntelliSense Remove-Package está danificado](http://nuget.codeplex.com/workitem/136)
* [Adicione o sinalizador RequireLicenseAcceptance a. nuspec e feed](http://nuget.codeplex.com/workitem/137)
* [Adicionar LicenseUrl ao formato. nuspec e ao feed de pacote](http://nuget.codeplex.com/workitem/138)
* [Clicar em instalar para o pacote que requer a aceitação deve mostrar a caixa de diálogo de aceitação](http://nuget.codeplex.com/workitem/139)
* [Adicionar texto de isenção de responsabilidade à caixa de diálogo Adicionar pacote](http://nuget.codeplex.com/workitem/140)
* [Adicionar um aviso de isenção de responsabilidade quando o console do pacote for executado pela primeira vez](http://nuget.codeplex.com/workitem/143)
* [Exibir o aviso de isenção de responsabilidade após instalar o pacote no console](http://nuget.codeplex.com/workitem/144)
* [Renomeie a extensão. nupack para. nupkg](http://nuget.codeplex.com/workitem/146)