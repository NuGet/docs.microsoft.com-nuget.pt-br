---
title: Notas de versão do NuGet 1.0 e 1.1
description: Notas de versão 1.1 do NuGet incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a11248a96109c879946e7e28a50e7753b644f042
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-10-and-11-release-notes"></a>Notas de versão do NuGet 1.0 e 1.1

[Notas de versão 1.2 do NuGet](../release-notes/nuget-1.2.md)

NuGet 1.0 foi lançado em 13 de janeiro de 2011.  NuGet 1.1 foi lançada em 12 de fevereiro de 2011.

## <a name="overview"></a>Visão geral

Este documento contém as notas de versão para diversas versões do NuGet 1.0 agrupados de acordo com a versão de visualização principal.

NuGet inclui os seguintes componentes:

* *NuGet.Tools.vsix* * consiste em que:
  * **Adicionar caixa de diálogo de pacote de biblioteca** * caixa de diálogo dentro do Visual Studio usado para procurar e instalar pacotes.
  * **Package Manager Console** * console dentro do Visual Studio com base em Powershell.
* *Ferramenta de linha de comando do NuGet* * ferramenta usada para criar (e, eventualmente, publicar) pacotes.

O NuGet ferramentas de extensão do Visual Studio (*NuGet.Tools.vsix*) requer:

* Visual Studio 2010 ou Visual Web Developer 2010 Express.

Requer a ferramenta de linha de comando do NuGet:

* Versão do .NET framework 4

## <a name="installation"></a>Instalação

Use essa [versão mais recente](http://nuget.codeplex.com/releases/view/52018):

* Desinstale a compilação mais antiga. Você precisa executar VS como administrador para fazer isso.
* Remova todos os feeds existentes que você tem.
* Adicionar um novo feed apontando para [ http://go.microsoft.com/fwlink/?LinkId=206669 ](http://go.microsoft.com/fwlink/?LinkId=206669).

## <a name="nuget-11"></a>NuGet 1.1

A lista de problemas corrigidos nesta versão [podem ser encontradas aqui](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>NuGet 1.0 RTM

Um problema foi corrigido para RTM desde o RC.

* [Problema 474: Removendo pacotes afeta todos os projetos na solução](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>Versão Release Candidate

A seguir estão as alterações feitas nesta versão Release Candidate desde o CTP 2. Visite o Issue Tracker para ver a lista completa de bugs.

* [Atualizar o pacote do Console não atualiza as dependências.](http://nuget.codeplex.com/workitem/443)
* [Adicionando pacote capta bin não referência (CTP1) do pacote](http://nuget.codeplex.com/workitem/442)
* [Um pacote de atualização deixa referências quebradas](http://nuget.codeplex.com/workitem/440)
* [Get-Package-atualizações falhar na caixa de diálogo, ou quando a fonte de agregação 'Todos' está selecionada no console do](http://nuget.codeplex.com/workitem/439)
* [Obtendo erros de verificação do pacote](http://nuget.codeplex.com/workitem/426)
* [Avisar os usuários quando um pacote não pode ser instalado na caixa de diálogo Adicionar pacote](http://nuget.codeplex.com/workitem/425)
* [Get-Package-atualiza lança ao atualizar um grande número de pacotes](http://nuget.codeplex.com/workitem/424)
* [Melhorar o tratamento de erros quando arquivos nuspec são criados incorretamente](http://nuget.codeplex.com/workitem/423)
* [Pacote do NuGet ignora os arquivos especificados](http://nuget.codeplex.com/workitem/422)
* [Removendo a origem do segundo ao último pacote e, em seguida, clicando em "Mover para baixo" falhas VS](http://nuget.codeplex.com/workitem/418)
* [Remover a referência de assembly durante a instalação de pacotes](http://nuget.codeplex.com/workitem/413)
* [Ao abrir a caixa de diálogo Configurações de InvalidOperationException](http://nuget.codeplex.com/workitem/411)
* [Chave de acesso para a origem do pacote no Console do Gerenciador de pacotes não funciona](http://nuget.codeplex.com/workitem/410)
* [Chaves de acesso de caixa de diálogo de configurações do NuGet VS focalizar campos incorretos](http://nuget.codeplex.com/workitem/409)
* [Intellisense de ID de pacote não deve consultar muitos itens](http://nuget.codeplex.com/workitem/404)
* [Falha ao adicionar o pacote para o projeto com um caractere de ponto no nome do projeto](http://nuget.codeplex.com/workitem/403)
* [Problema com os arquivos especificados em nuspec](http://nuget.codeplex.com/workitem/400)
* [Feed oficial correto deve se registrar ao usar a compilação mais recente](http://nuget.codeplex.com/workitem/399)
* [As marcas devem usar espaços em vez de #](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata não tem algumas informações úteis](http://nuget.codeplex.com/workitem/388)
* [Adicionar Link para relatar abuso para a caixa de diálogo](http://nuget.codeplex.com/workitem/386)
* [Usando App_Data para descompactar quebras de pacotes no Visual Studio](http://nuget.codeplex.com/workitem/380)
* [Implementar marcas](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder permite que um pacote vazio a ser criado sem dependências](http://nuget.codeplex.com/workitem/373)
* [Adicionar campo proprietários do pacote](http://nuget.codeplex.com/workitem/365)
* [Atualizar o manifesto do VSIX para dizer o NuGet Package Manager, em vez de ferramentas do VSIX](http://nuget.codeplex.com/workitem/364)
* [Comando Get-Package gera erro quando a fonte todos está selecionada](http://nuget.codeplex.com/workitem/359)
* [Permitir a ordenação de origens do pacote na caixa de diálogo Opções](http://nuget.codeplex.com/workitem/356)
* [Pacote de atualização não remove a versão mais antiga](http://nuget.codeplex.com/workitem/352)
* [Especificação do intervalo de versão de implementação para dependências](http://nuget.codeplex.com/workitem/347)
* [Visual Studio Falha ao clicar em "Adicionar novo pacote"](http://nuget.codeplex.com/workitem/346)
* [Exibir Downloads e classificações na caixa de diálogo Adicionar de pacote](http://nuget.codeplex.com/workitem/345)
* [Alterando entre origens do pacote na caixa de diálogo não atualiza a fonte ativa](http://nuget.codeplex.com/workitem/344)
* [Remover a chave de associação para a janela de Console do Gerenciador de pacotes](http://nuget.codeplex.com/workitem/339)
* [Pacote de instalação não é reconhecido como o nome de um cmdlet...](http://nuget.codeplex.com/workitem/338)
* [Instalação de um pacote de um local em que as dependências de feed em feeds regulares não são resolvidos](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies deve ignorar dependências que ainda estão em uso](http://nuget.codeplex.com/workitem/331)
* [Se cancelar a navegação de página, o usuário não pode navegar para uma página diferente enquanto a solicitação de página original retorna](http://nuget.codeplex.com/workitem/325)
* [Investigar o desempenho de NuPack.Server para atender a feeds com grande número de pacotes.](http://nuget.codeplex.com/workitem/324)
* [Na segunda vez que filtrar para um pacote, ele usa a origem do pacote de "Novo", em vez da fonte selecionada anteriormente.](http://nuget.codeplex.com/workitem/321)
* [Origem do pacote padrão deve ser selecionada quando selecionando a guia "Online" na caixa de diálogo.](http://nuget.codeplex.com/workitem/320)
* [Pacote de lista deve mostrar pacotes instalados por padrão](http://nuget.codeplex.com/workitem/309)
* [HintPaths de referência de assembly](http://nuget.codeplex.com/workitem/294)
* [Exceção ao abrir o Console do Gerenciador de pacotes](http://nuget.codeplex.com/workitem/268)
* [Console intellisense downloads feed inteiro](http://nuget.codeplex.com/workitem/259)
* [Origem do pacote 'Default' deve ser renomeada para 'Active'](http://nuget.codeplex.com/workitem/258)
* [Pacote de fontes da interface do usuário: pressionar Okey deve adicionar a nova fonte se campos de fonte do nome não vazio](http://nuget.codeplex.com/workitem/257)
* [Caixa de diálogo fica muito lenta quando o número de pacotes instalados é grande](http://nuget.codeplex.com/workitem/243)
* [Suporte a redirecionamentos de associação para conjuntos de alta segurança](http://nuget.codeplex.com/workitem/238)
* [Adicione referência de pacote... Interface do usuário para incluir drop para baixo para a origem do pacote](http://nuget.codeplex.com/workitem/226)
* [NuPack precisa oferecer suporte à transformação de configuração agnostically do nome do arquivo de configuração](http://nuget.codeplex.com/workitem/224)
* [Permite BasePath ser substituído em NuPack.exe](http://nuget.codeplex.com/workitem/222)
* [Comportamento de Fallback de origem do pacote](http://nuget.codeplex.com/workitem/204)
* [Falha na interface gráfica do usuário](http://nuget.codeplex.com/workitem/201)
* [Adicionar opções à caixa de diálogo Adicionar pacote de classificação](http://nuget.codeplex.com/workitem/179)
* [tecla de atalho para limpar o Package Manager Console](http://nuget.codeplex.com/workitem/174)
* [PowerConsole faz com que o Console de NuPack falha](http://nuget.codeplex.com/workitem/166)
* [Console e a caixa de diálogo Adicionar pacote devem definir o agente do usuário em solicitações](http://nuget.codeplex.com/workitem/141)
* [Definir o número de versão do VSIX e NuPack.exe no build.](http://nuget.codeplex.com/workitem/134)
* [Ocultar os parâmetros comuns do PowerShell de-?](http://nuget.codeplex.com/workitem/118)
* [Adicione - a ajuda detalhada para comandos do console](http://nuget.codeplex.com/workitem/110)
* [Adicionar caixa de diálogo pacote deve permitir a escolha de origem do pacote atual](http://nuget.codeplex.com/workitem/88)
* [Mover NuPack.Core classes em namespaces diferentes](http://nuget.codeplex.com/workitem/50)
* [Adicionar ajuda para cmdlets](http://nuget.codeplex.com/workitem/23)
* [Verifique se o hash do feed após o download do pacote](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

Estas são as alterações mais significativas feitas no CTP 2:

* Alternado o pacote de feed do ATOM para um ponto de extremidade do serviço OData: se você atualizar para a versão CTP2 do NuGet, certifique-se de adicionar a URL a seguir como uma origem de pacote: `https://feed.nuget.org/ctp2/odata/v1/`.
* Renomear o comando Add-Package para *Install-Package*.
* Atualizado o `.nuspec` formato. O `.nuspec` formato agora inclui o *iconUrl* campo para especificar um ícone de png de 32 x 32 que será exibido na caixa de diálogo Adicionar pacote. Portanto certifique-se de que para distinguir o pacote. O `.nuspec` formato também inclui o novo *projectUrl* campo que você pode usar para apontar para uma página da web que fornece mais informações sobre o pacote.

Esta compilação não funciona com o antigo `.nupkg` arquivos. Se você receber exceções de referência nula, você está usando o antigo `.nupkg` de arquivo e precisará recriá-lo com a atualização [ferramenta de linha de comando do NuGet](http://nuget.codeplex.com/releases/52017/download/165468).

A seguir está uma lista de recursos e os bugs que foram corrigidos para NuGet CTP 2 (não inclui bugs de limpezas de código secundária etc.).

* [Assemblies descompactação do pacote de erro quando especificar TargetFramework para um assembly.](http://nuget.codeplex.com/workitem/10)
* [Verifique a janela do NuPack Console mais detectáveis](http://nuget.codeplex.com/workitem/14)
* [A versão de nupack.exe de ILMerge](http://nuget.codeplex.com/workitem/19)
* [Melhor tratamento de erro/exceção](http://nuget.codeplex.com/workitem/24)
* [[Nupack.Core]: PackageManager normalmente deve tratar erros relacionados ao feed](http://nuget.codeplex.com/workitem/28)
* [Precisa de um novo ícone para o console](http://nuget.codeplex.com/workitem/29)
* [Localizar cadeias de caracteres na caixa de diálogo](http://nuget.codeplex.com/workitem/38)
* [Caches NuPack baixado arquivos .nupack na memória](http://nuget.codeplex.com/workitem/40)
* [NuPack Console: Alterar o atalho padrão para a exibição do console](http://nuget.codeplex.com/workitem/48)
* [ProjectSystem deve dar suporte a valores padrão para as propriedades comuns](http://nuget.codeplex.com/workitem/49)
* [Execução de nupack.exe em uma pasta com apenas um arquivo nuspec deve usar esse nuspec](http://nuget.codeplex.com/workitem/52)
* [Menu projeto exibida mesmo quando nenhum projeto/solução for carregada](http://nuget.codeplex.com/workitem/54)
* [Build.cmd falha em um clone exato da Base de código](http://nuget.codeplex.com/workitem/56)
* [Recurso de atualizações disponível](http://nuget.codeplex.com/workitem/57)
* [Caixa de diálogo: Adicionando um pacote por meio da caixa de diálogo Remove o prompt no console do](http://nuget.codeplex.com/workitem/73)
* [Adicionando um pacote clicando em "Instalar" geralmente é lento, não há indicação visual](http://nuget.codeplex.com/workitem/80)
* [Não há nenhuma maneira de descobrir quais dos meus pacotes instalados têm atualizações.](http://nuget.codeplex.com/workitem/82)
* [Não há nenhuma maneira de atualizar um pacote instalado na caixa de diálogo.](http://nuget.codeplex.com/workitem/83)
* [Não é possível desinstalar um pacote instalado na caixa de diálogo](http://nuget.codeplex.com/workitem/84)
* [&ldquo;Adicionar referência de pacotes&hellip; &rdquo; aparece no menu de contexto de referências instalados](http://nuget.codeplex.com/workitem/85)
* [Depois de atualizar um pacote no console do, ele mostra a versão antiga e a nova versão como instalado](http://nuget.codeplex.com/workitem/86)
* [A atividade no console, ao usar a caixa de diálogo desaparecerá depois de uso](http://nuget.codeplex.com/workitem/87)
* [Linha de comando de limpeza nupack.exe de análise](http://nuget.codeplex.com/workitem/89)
* [Adicionar um nome amigável para fontes de pacote](http://nuget.codeplex.com/workitem/98)
* [Atualizar. NuSpec para dar suporte a incluindo ícones de pacote](http://nuget.codeplex.com/workitem/103)
* [Feed de interface do usuário não permite copiar a URL](http://nuget.codeplex.com/workitem/105)
* [Melhor tratamento de erros de pacote a remover.](http://nuget.codeplex.com/workitem/107)
* [Digitando na janela de Console depende de foco de cursor](http://nuget.codeplex.com/workitem/112)
* [Mensagens de erro procure terrível](http://nuget.codeplex.com/workitem/116)
* [O desempenho de Remove-pacote de um pacote que não está instalado está incorreto](http://nuget.codeplex.com/workitem/117)
* [Falha na remoção de um pacote quando não houver nenhum origens do pacote](http://nuget.codeplex.com/workitem/119)
* [Remover pacote falha quando a origem do pacote não está disponível](http://nuget.codeplex.com/workitem/120)
* [Adicione um título para os metadados do pacote e o feed.](http://nuget.codeplex.com/workitem/125)
* [Adicionar-parâmetro de origem do pacote a adicionar](http://nuget.codeplex.com/workitem/127)
* [Lista de pacote deve ter um - parâmetro de origem](http://nuget.codeplex.com/workitem/128)
* [Atualizar NuPack.Server para exigir NuPack usuário para baixar o pacote do agente](http://nuget.codeplex.com/workitem/142)
* [Caixa de diálogo de consentimento de licença deve listar licenças para todas as dependências que exigem aceitação](http://nuget.codeplex.com/workitem/145)
* [Registrar um erro quando um pacote gera no feed](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe não deve permitir vazio &lt;licenseurl&gt; elemento](http://nuget.codeplex.com/workitem/152)
* [Renomeie o pacote da lista para Get-pacote, adicione-pacote de instalação e remoção pacote para desinstalar o pacote](http://nuget.codeplex.com/workitem/155)
* [Usando o item de menu Adicionar referência de pacote do navegador de solução de falhas de Visual Studio](http://nuget.codeplex.com/workitem/158)
* [Rótulo "origens do pacote disponíveis" está faltando um vírgula](http://nuget.codeplex.com/workitem/160)
* [Tornar. NuSpec xml elemento maiusculas e minúsculas consistentemente concatenação com maiusculas e minúsculas](http://nuget.codeplex.com/workitem/161)
* [Manifesto de NuPack VSIX precisa ativar o bit 'admin'](http://nuget.codeplex.com/workitem/162)
* [Se você executar o pacote de lista com nenhum feed, você receber o erro de referência nula](http://nuget.codeplex.com/workitem/164)
* [NuGet.exe: especifique o caminho de destino](http://nuget.codeplex.com/workitem/171)
* [Erros de PowerShell abrindo o Console de gerenciamento de pacote no WinXP](http://nuget.codeplex.com/workitem/175)
* [Falhas de VS ao tentar carregar a lista de pacotes](http://nuget.codeplex.com/workitem/176)
* [permita que os pacotes do meta (nenhum arquivo, apenas dependências)](http://nuget.codeplex.com/workitem/180)
* [Converter o Script do Powershell para o módulo do Powershell 2.0](http://nuget.codeplex.com/workitem/181)
* [PathResolver deve descartar os caracteres curinga do caminho parte anterior quando o destino for especificado](http://nuget.codeplex.com/workitem/183)
* [Sem dependências](http://nuget.codeplex.com/workitem/186)
* [Erro ao instalar o Elmah](http://nuget.codeplex.com/workitem/192)
* [Transformações de config não funcionam corretamente com &lt;configsections&gt;](http://nuget.codeplex.com/workitem/194)
* [A variável ' $global: projectCache' não pode ser recuperado porque não foi definido](http://nuget.codeplex.com/workitem/203)
* [Adicionar tarefa MSBuild para criar pacotes de NuPack](http://nuget.codeplex.com/workitem/205)
* [lista de pacote precisa dar suporte a pesquisa/filtragem](http://nuget.codeplex.com/workitem/206)
* [Sempre exibir um link para a licença se o autor do pacote fornece uma URL de licença](http://nuget.codeplex.com/workitem/208)
* [Exceção de "Acesso negado" ocasional com Remove-Package](http://nuget.codeplex.com/workitem/213)
* [Testes de unidade com falha: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [Permitir para um conjunto de fallback/padrão de arquivos se uma versão do framework específico não pode ser encontrada](http://nuget.codeplex.com/workitem/223)
* [Adicione referência de pacote... Interface do usuário não é possível remover um pacote](http://nuget.codeplex.com/workitem/225)
* [Adicionar referência de pacote falhar studio quando um ou mais projetos é descarregado](http://nuget.codeplex.com/workitem/228)
* [Transformação de configuração não parece funcionar no arquivo web.debug.config](http://nuget.codeplex.com/workitem/229)
* [Init.ps1 não são acionados no pacote personalizado](http://nuget.codeplex.com/workitem/237)
* [Ao adicionar caminhos para a lista de feeds, o botão padrão está definido como Okey, para que se pressionar ENTER fechá-lo automaticamente](http://nuget.codeplex.com/workitem/240)
* [Tentativa de desinstalar uma dependência falhará VS se tentou 2 vezes em uma linha](http://nuget.codeplex.com/workitem/241)
* [Exibir a URL do projeto na caixa de diálogo Adicionar pacote](http://nuget.codeplex.com/workitem/253)
* [A caixa de diálogo Adicionar pacote instalado pacotes de padrão](http://nuget.codeplex.com/workitem/254)
* [Item de menu da caixa de diálogo Adicionar pacote de alteração.](http://nuget.codeplex.com/workitem/261)
* [Renomear namespaces e assemblies](http://nuget.codeplex.com/workitem/274)
* [Renomear o projeto NuPack ao NuGet](http://nuget.codeplex.com/workitem/282)
* [Adicione o seguinte texto na lista de dependências](http://nuget.codeplex.com/workitem/288)
* [Alterar o texto de aceitação de licença na caixa de diálogo de aceitação de licença](http://nuget.codeplex.com/workitem/291)
* [Alterar o texto na caixa de diálogo de consentimento de licença acima da lista de pacotes](http://nuget.codeplex.com/workitem/292)
* [OData não funciona com uma URL fwlink](http://nuget.codeplex.com/workitem/304)
* [Gerenciador de pacote UI: em cache agressivo de contagem de pacote usada para paginação](http://nuget.codeplex.com/workitem/317)
* [NuPack / NuGet -&gt; erro Package Manager Console](http://nuget.codeplex.com/workitem/335)
* [Adicionar que caixa de diálogo pacote mostra a licença de aceitação para já instalado empacotados](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

A seguir está uma lista de recursos e os bugs que foram corrigidos para NuGet CTP 1.

* [Extensão do pacote deve ser renomeado para .nupack](http://nuget.codeplex.com/workitem/1)
* [Mover o arquivo de pacote na pasta](http://nuget.codeplex.com/workitem/2)
* [Instalação de mesclagem &amp; comandos Adicionar PS](http://nuget.codeplex.com/workitem/3)
* [Criar aliases para cmdlets verbo-substantivo.](http://nuget.codeplex.com/workitem/4)
* [NuPack obtém confusos quando a troca de solução no VS](http://nuget.codeplex.com/workitem/6)
* [Podemos deve ocultar a pasta de solução 'packages' por padrão](http://nuget.codeplex.com/workitem/11)
* [Adicione suporte para a substituição de token em itens de conteúdo.](http://nuget.codeplex.com/workitem/12)
* [NuPack.UI devem usar a API PackageSource](http://nuget.codeplex.com/workitem/26)
* [[Nupack.Core]: PackageManager marca pacotes como instalado antes de instalá-los](http://nuget.codeplex.com/workitem/27)
* [Excluindo projeto padrão de solução ainda mostrará o projeto excluído como padrão](http://nuget.codeplex.com/workitem/30)
* [Novo pacote falha com "Não é possível adicionar parte do URI especificado porque ele já está no pacote."](http://nuget.codeplex.com/workitem/32)
* [Remover cadeias de caracteres "NuPack" de GUI do Visual Studio](http://nuget.codeplex.com/workitem/35)
* [Adicionar cabeçalho de Apache para COPYRIGHT.txt um arquivo](http://nuget.codeplex.com/workitem/36)
* [Remova o comando Update-PackageSource](http://nuget.codeplex.com/workitem/37)
* [Inutilizável ao carregar o perfil do Gerenciador de pacote gera uma exceção](http://nuget.codeplex.com/workitem/39)
* [Init.ps1, install.ps1 e uninstall.ps1 precisam receber estado adicionais](http://nuget.codeplex.com/workitem/41)
* [Combinar o Console e pacotes de interface gráfica do usuário em um pacote](http://nuget.codeplex.com/workitem/42)
* [Lógica de transformação de XML não funciona se aplicado ao XML que não está na raiz](http://nuget.codeplex.com/workitem/43)
* [Gerenciar o diálogo de configurações de fontes de pacote não atualizar o console de NuPack](http://nuget.codeplex.com/workitem/44)
* [NuPack Console da interface do usuário: Renomear lista suspensa de 'Pacote feed' origem do pacote](http://nuget.codeplex.com/workitem/45)
* [Opções do Console do NuPack: Renomear 'Repositório da interface do usuário' para ser consistente com o Console de NuPack](http://nuget.codeplex.com/workitem/46)
* [Adicionar o pacote falha em relação a um site que foi aberto do IIS ou uma URL](http://nuget.codeplex.com/workitem/53)
* [Origem do Gerenciador de pacotes não funciona com FwLink](http://nuget.codeplex.com/workitem/55)
* [Defina a origem de pacote padrão](http://nuget.codeplex.com/workitem/59)
* [Ao adicionar fontes de pacote na opção, somente uma fonte for fornecido, suponha que é o padrão.](http://nuget.codeplex.com/workitem/60)
* [A interface de usuário da caixa de diálogo mostra pacotes "recentes" falsos](http://nuget.codeplex.com/workitem/62)
* [Opções: Clicar em Cancelar não cancelar as alterações](http://nuget.codeplex.com/workitem/63)
* [Adicionar que pacote de referência de caixa de diálogo pesquisa deve diferenciar maiusculas e minúsculas](http://nuget.codeplex.com/workitem/65)
* [Corrija os metadados de empresa nos arquivos AssemblyInfo.cs](http://nuget.codeplex.com/workitem/67)
* [Número de versão do VSIX](http://nuget.codeplex.com/workitem/71)
* [Pacote de remover: Usando o-? Exibe a Ajuda duas vezes](http://nuget.codeplex.com/workitem/72)
* [Executar pacotes de instalação/desinstalação para pacotes de nível de projeto](http://nuget.codeplex.com/workitem/74)
* [Não é possível criar o feed quando uma nupack Falha na validação do servidor](http://nuget.codeplex.com/workitem/90)
* [Preciso substituir NuPack ícones](http://nuget.codeplex.com/workitem/94)
* [Proxy de http NTLM não autentica para o pacote de feed.](http://nuget.codeplex.com/workitem/96)
* [A caixa de diálogo sempre não começa centralizada na janela do VS](http://nuget.codeplex.com/workitem/100)
* [Muitos dos campos em um detalhes de pacotes não estão sendo preenchidos na caixa de diálogo](http://nuget.codeplex.com/workitem/102)
* [Caixa de diálogo da interface do usuário não mostra os nomes dos autores](http://nuget.codeplex.com/workitem/108)
* [Por que - versão para remover pacote](http://nuget.codeplex.com/workitem/113)
* [Remover a guia recente da interface do usuário do diálogo](http://nuget.codeplex.com/workitem/115)
* [Falha do VS quando direito clique na pasta de solução depois de abrir a caixa de diálogo da interface do usuário pelo menos um.](http://nuget.codeplex.com/workitem/126)
* [Altere o parâmetro - Local do pacote de lista - instalado](http://nuget.codeplex.com/workitem/129)
* [Renomeie packages.xml para NuPack.config](http://nuget.codeplex.com/workitem/132)
* [Console força o cursor até o fim da linha](http://nuget.codeplex.com/workitem/135)
* [Remover pacote intellisense foi interrompido](http://nuget.codeplex.com/workitem/136)
* [Adicionar sinalizador RequireLicenseAcceptance. NuSpec e alimentação](http://nuget.codeplex.com/workitem/137)
* [Adicionar Feed LicenseUrl. NuSpec formato e pacote](http://nuget.codeplex.com/workitem/138)
* [Clicar em instalar para o pacote que requer aceitação deve mostrar a caixa de diálogo de aceitação](http://nuget.codeplex.com/workitem/139)
* [Adicionar texto de aviso para a caixa de diálogo Adicionar pacote](http://nuget.codeplex.com/workitem/140)
* [Adicionar que isenção quando o pacote de Console é executado na primeira vez](http://nuget.codeplex.com/workitem/143)
* [Exibir aviso de isenção depois de instalar o pacote no Console do](http://nuget.codeplex.com/workitem/144)
* [Renomeie a extensão .nupack para nupkg](http://nuget.codeplex.com/workitem/146)