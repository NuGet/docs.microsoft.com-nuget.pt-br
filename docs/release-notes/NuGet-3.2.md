---
title: Notas de versão do NuGet 3,2
description: Notas de versão do NuGet 3,2 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 38a56b1572770b02ff09135a3b0290742ca80f41
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780308"
---
# <a name="nuget-32-release-notes"></a>Notas de versão do NuGet 3,2

Notas de versão do [NuGet 3,2-RC](../release-notes/nuget-3.2-RC.md)  |  [Notas de versão do NuGet 3.2.1](../release-notes/nuget-3.2.1.md)

O NuGet 3,2 foi lançado em 16 de setembro de 2015 como uma coleção de melhorias e correções para a versão 3.1.1 e está disponível tanto no [dist.NuGet.org](http://dist.nuget.org/index.html) quanto na [Galeria do Visual Studio](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2015).

## <a name="new-features"></a>Novos recursos

* Os projetos que residem na mesma pasta agora podem ter `project.json` arquivos diferentes na pasta específica para cada projeto.  Para cada projeto, nomeie o `project.json` arquivo `{ProjectName}.project.json` e o NuGet dará preferência a essa configuração para cada projeto adequadamente.  Só há suporte para isso com as ferramentas do Windows 10 v 1.1 instaladas-  [1102](https://github.com/NuGet/Home/issues/1102)
* Os clientes do NuGet dão suporte à especificação de uma variável de ambiente de NUGET_PACKAGES global para especificar o local da pasta de pacotes globais compartilhados usada em `project.json` projetos gerenciados com as ferramentas do Windows 10 v 1.1.

## <a name="command-line-updates"></a>Atualizações de linha de comando

Esta é a primeira versão do cliente de nuget.exe que dá suporte aos servidores NuGet v3 e restaurando pacotes para projetos gerenciados com um `project.json` arquivo.

Houve uma série de problemas de feed autenticados que foram resolvidos nesta versão para melhorar as interações com o cliente.

* As interações de instalar/restaurar só enviam credenciais para a solicitação inicial para o feed autenticado- [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* O comando Push não resolve as credenciais da configuração- [1248](https://github.com/NuGet/Home/issues/1248)
* O agente do usuário e os cabeçalhos agora são enviados aos repositórios do NuGet para ajudar com o acompanhamento de estatísticas- [929](https://github.com/NuGet/Home/issues/929)

Fizemos vários aprimoramentos para lidar melhor com falhas de rede ao tentar trabalhar com um repositório do NuGet remoto:

* Mensagens de erro aprimoradas quando não é possível conectar-se a feeds remotos- [1238](https://github.com/NuGet/Home/issues/1238)
* O comando NuGet Restore foi corrigido para retornar um 1 quando ocorre uma condição de erro- [1186](https://github.com/NuGet/Home/issues/1186)
* Agora, repetindo conexões de rede a cada 200 MS para um máximo de 5 tentativas no caso de falhas HTTP 5xx- [1120](https://github.com/NuGet/Home/issues/1120)
* Tratamento aprimorado de respostas de redirecionamento de servidor durante um comando Push- [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` Agora é compatível com o nome da URL ou do repositório de Nuget.Config como um argumento- [1046](https://github.com/NuGet/Home/issues/1046)
* Os pacotes ausentes que não estavam localizados em um repositório durante uma restauração agora são relatados como erros em vez de avisos [1038](https://github.com/NuGet/Home/issues/1038)
* Manipulação de multipartwebrequest corrigida de \r\n para cenários UNIX/Linux- [776](https://github.com/NuGet/Home/issues/776)

Há uma série de correções para problemas com vários comandos:

* O comando Push não faz mais um GET antes de um PUT em uma origem de pacote- [1237](https://github.com/NuGet/Home/issues/1237)
* O comando de lista não repete mais números de versão- [1185](https://github.com/NuGet/Home/issues/1185)
* Pacote com o argumento-Build agora é compatível corretamente com C# 6,0- [1107](https://github.com/NuGet/Home/issues/1107)
* Problemas corrigidos ao tentar empacotar um projeto F # criado com o Visual Studio 2015- [1048](https://github.com/NuGet/Home/issues/1048)
* Restaurar agora não Ops quando os pacotes já existem- [1040](https://github.com/NuGet/Home/issues/1040)
* Mensagens de erro aprimoradas quando o `packages.config` arquivo está malformado- [1034](https://github.com/NuGet/Home/issues/1034)
* Corrigido o comando de restauração com a opção-SolutionDirectory para trabalhar com caminhos relativos- [992](https://github.com/NuGet/Home/issues/992)
* Aperfeiçoado o comando atualizado para dar suporte à atualização em toda a solução- [924](https://github.com/NuGet/Home/issues/924)

Uma lista completa dos problemas abordados nesta versão pode ser encontrada na [etapa da linha de comando](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate)do GitHub do NuGet.

## <a name="visual-studio-extension-updates"></a>Atualizações de extensão do Visual Studio

### <a name="new-features-in-visual-studio"></a>Novos recursos no Visual Studio

* Um novo item de menu de contexto foi adicionado ao Gerenciador de Soluções no nó da solução que permite que os pacotes sejam restaurados sem compilar a solução ([1274](https://github.com/NuGet/Home/issues/1274)).

![Novo item de menu de contexto ' restaurar pacotes '](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Atualizações e correções no Visual Studio

As correções de feeds autenticados também foram acumuladas e abordadas na extensão.  Os seguintes itens de autenticação também foram abordados na extensão:

* Agora tratando corretamente os feeds autenticados do NuGet v3 corretamente, em vez de os feeds autenticados v2- [1216](https://github.com/NuGet/Home/issues/1216)
* Solicitação corrigida de credenciais de autenticação em projetos usando `project.json` e comunicando-se com feeds v2- [1082](https://github.com/NuGet/Home/issues/1082)

A conectividade de rede afetou a interface do usuário no Visual Studio e corrigimos isso com as seguintes correções:

* Melhoria da manutenção do cache local das versões do pacote- [1096](https://github.com/NuGet/Home/issues/1096)
* O comportamento de falha foi alterado ao se conectar a um feed V3 para não tentar mais tratá-lo como um feed v2- [1253](https://github.com/NuGet/Home/issues/1253)
* Impedindo falhas de instalação ao instalar um pacote com várias fontes de pacote- [1183](https://github.com/NuGet/Home/issues/1183)

Melhoramos o tratamento de interações com operações de compilação:

* Agora, continuar a criar projetos se a restauração de pacotes de um único projeto falhar- [1169](https://github.com/NuGet/Home/issues/1169)
* A instalação de um pacote em um projeto que é dependente de outro projeto na solução força uma recompilação da solução- [981](https://github.com/NuGet/Home/issues/981)
* Instalações corrigidas com falha são instaladas para reverter corretamente as alterações para um projeto- [1265](https://github.com/NuGet/Home/issues/1265)
* Correção acidental de remoção do `developmentDependency` atributo em um pacote em `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* As chamadas para `install.ps1` agora têm um `$package.AssemblyReferences` objeto apropriado passado- [1245](https://github.com/NuGet/Home/issues/1245)
* Não está mais impedindo desinstalações de pacotes em projetos UWP enquanto o projeto está em um estado inadequado- [1128](https://github.com/NuGet/Home/issues/1128)
* As soluções que contêm uma combinação de `packages.config` `project.json` projetos e agora são criadas corretamente sem a necessidade de uma segunda operação de compilação- [1122](https://github.com/NuGet/Home/issues/1122)
* Localizando app.config arquivos corretamente se eles estiverem vinculados ou localizados em uma pasta diferente- [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* Os projetos UWP agora podem instalar pacotes não listados- [1109](https://github.com/NuGet/Home/issues/1109)
* A restauração de pacote agora é permitida enquanto uma solução não está em um estado salvo- [1081](https://github.com/NuGet/Home/issues/1081)

A manipulação de atualizações para arquivos de configuração foi corrigida:

* Não remove mais um arquivo de destino fornecido de um pacote em compilações subsequentes de um `project.json` projeto gerenciado- [1288](https://github.com/NuGet/Home/issues/1288)
* Não está mais modificando arquivos de Nuget.Config durante o Build da solução ASP.NET 5- [1201](https://github.com/NuGet/Home/issues/1201)
* Não está mais alterando a restrição de versões permitidas durante a atualização do pacote- [1130](https://github.com/NuGet/Home/issues/1130)
* Arquivos de bloqueio agora permanecem bloqueados durante o Build- [1127](https://github.com/NuGet/Home/issues/1127)
* Agora modificando `packages.config` e não regravando-o durante as atualizações- [585](https://github.com/NuGet/Home/issues/585)

As interações com o controle de origem do TFS são aprimoradas:

* Não há mais instalações com falha para pacotes associados ao TFS- [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)
* Interface do usuário do NuGet corrigida para permitir integração do TFS 2013- [1071](https://github.com/NuGet/Home/issues/1071)
* Referências corrigidas a pacotes restaurados de forma adequada vêm de uma pasta de pacotes- [1004](https://github.com/NuGet/Home/issues/1004)

Por fim, também melhoramos estes itens:

* Detalhamento de mensagens de log reduzidas para `project.json` projetos gerenciados- [1163](https://github.com/NuGet/Home/issues/1163)
* Exibindo corretamente a versão instalada de um pacote na interface do usuário- [1061](https://github.com/NuGet/Home/issues/1061)
* Pacotes com intervalos de dependência especificados em seu nuspec agora têm versões de pré-lançamento dessas dependências instaladas para uma versão de pacote estável- [1304](https://github.com/NuGet/Home/issues/1304)

Uma lista completa de problemas abordados para a extensão do Visual Studio pode ser encontrada na etapa de conclusão do GitHub [3,2](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2) do NuGet

## <a name="known-issues"></a>Problemas conhecidos

Continuamos a acompanhar problemas em nossa lista de problemas do GitHub, que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)