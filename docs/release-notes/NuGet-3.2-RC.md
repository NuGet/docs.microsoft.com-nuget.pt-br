---
title: Notas de versão do NuGet 3.2 RC
description: Notas de versão do NuGet 3.2 RC incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: eafdedc3ad022a6794dbeb390de87d7f317e28f1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551492"
---
# <a name="nuget-32-rc-release-notes"></a>Notas de versão do NuGet 3.2 RC

[Notas de versão do NuGet 3.1.1](../release-notes/nuget-3.1.1.md) | [notas de versão do NuGet 3.2](../release-notes/nuget-3.2.md)

Versão Release candidate do NuGet 3.2 foi lançado a versão 2 de setembro de 2015 como uma coleção de melhorias e correções para o 3.1.1.  Além disso, essas são as primeiras versões que são publicadas pela primeira vez para o novo repositório dist.nuget.org.

## <a name="new-features"></a>Novos recursos

* Projetos que residem na mesma pasta agora podem ter diferentes `project.json` arquivos nessa pasta específica para cada projeto.  Para cada projeto, o nome do `project.json` arquivo `{ProjectName}.project.json` e NuGet corretamente referenciar e usar esse conteúdo para cada projeto de forma adequada.  Isso dá suporte a um novo recurso [1102](https://github.com/NuGet/Home/issues/1102)
* `NuGet.Config` agora dá suporte a um globalPackagesFolder como um caminho relativo - [1062](https://github.com/NuGet/Home/issues/1062)

## <a name="command-line-updates"></a>Atualizações de linha de comando

Isso é a primeira versão do cliente nuget.exe que dá suporte a servidores NuGet v3 e restauração de pacotes para projetos gerenciados com um `project.json` arquivo.

#### <a name="there-were-a-number-of-authenticated-feed-issues-that-were-addressed-in-this-release-to-improve-interactions-with-the-client"></a>Havia vários problemas de feed autenticados que foram resolvidos nesta versão para aprimorar as interações com o cliente.

* Instalar / interações de restauração apenas enviar as credenciais para a solicitação inicial para o feed autenticado - [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* Comando Push não resolve as credenciais da configuração - [1248](https://github.com/NuGet/Home/issues/1248)
* Agente do usuário e cabeçalhos agora são enviados aos repositórios do NuGet para ajudá-lo com o acompanhamento de estatísticas - [929](https://github.com/NuGet/Home/issues/929)

#### <a name="we-made-a-number-of-improvements-to-better-handle-network-failures-while-attempting-to-work-with-a-remote-nuget-repository"></a>Fizemos vários aprimoramentos para lidar melhor com falhas de rede ao tentar trabalhar com um repositório remoto do NuGet:

* Mensagens de erro quando não é possível conectar-se a feeds remotos - aprimoradas [1238](https://github.com/NuGet/Home/issues/1238)
* Corrigido o comando de restauração do NuGet para corretamente retorna 1 quando ocorre uma condição de erro - [1186](https://github.com/NuGet/Home/issues/1186)
* Agora, repetindo as conexões de rede cada 200 ms para um máximo de 5 tentativas no caso de falhas do HTTP 5xx - [1120](https://github.com/NuGet/Home/issues/1120)
* Manipulação de respostas de redirecionamento do servidor durante um comando push - melhorada [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` Agora é compatível com o nome de uma URL ou o repositório do NuGet. config como um argumento - [1046](https://github.com/NuGet/Home/issues/1046)
* Os pacotes ausentes que não foram localizados em um repositório durante uma restauração agora são relatados como erros, em vez de avisos [1038](https://github.com/NuGet/Home/issues/1038)
* Corrigido o tratamento de multipartwebrequest de \r\n para cenários de Unix/Linux - [776](https://github.com/NuGet/Home/issues/776)

#### <a name="there-are-a-number-of-fixes-to-issues-with-various-commands"></a>Há uma série de correções para problemas com vários comandos:

* Comando Push não faz mais um GET antes de um PUT em relação a uma origem de pacote - [1237](https://github.com/NuGet/Home/issues/1237)
* Comando list não repete os números de versão - [1185](https://github.com/NuGet/Home/issues/1185)
* Pacote com o argumento - build agora corretamente dá suporte a C# 6.0 - [1107](https://github.com/NuGet/Home/issues/1107)
* Problemas corrigidos tentando empacotar um projeto F # compilados com o Visual Studio 2015 - [1048](https://github.com/NuGet/Home/issues/1048)
* Restaurar agora não funciona quando já existem pacotes - [1040](https://github.com/NuGet/Home/issues/1040)
* Mensagens de erro aprimoradas quando `packages.config` o arquivo está malformado - [1034](https://github.com/NuGet/Home/issues/1034)
* Corrigido o comando de restauração com `-SolutionDirectory` alternar para trabalhar com caminhos relativos - [992](https://github.com/NuGet/Home/issues/992)
* Aprimorado o comando Updated para dar suporte à atualização de toda a solução - [924](https://github.com/NuGet/Home/issues/924)

Uma lista completa dos problemas abordados nesta versão pode ser encontrada no GitHub do NuGet [marco de linha de comando](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate).

## <a name="visual-studio-extension-updates"></a>Atualizações de extensão do Visual Studio

### <a name="new-features-in-visual-studio"></a>Novos recursos no Visual Studio

* Um novo item de menu de contexto foi adicionado ao Gerenciador de soluções, no nó da solução que permite que os pacotes a serem restaurados sem compilar a solução ([1274](https://github.com/NuGet/Home/issues/1274)).

![Novo 'Restaurar pacotes' Item de Menu de contexto](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Atualizações e correções no Visual Studio

#### <a name="the-fixes-for-authenticated-feeds-were-rolled-up-and-addressed-in-the-extension-as-well--the-following-authentication-items-were-also-addressed-in-the-extension"></a>As correções para feeds autenticados foram acumuladas e abordadas na extensão também.  Os itens de autenticação a seguir também foram tratados na extensão:

* Agora, tratar corretamente o NuGet v3 feeds autenticados corretamente, em vez de como v2 autenticados feeds - [1216](https://github.com/NuGet/Home/issues/1216)
* Corrigido solicitação de credenciais de autenticação em projetos que usam `project.json` e se comunicando com feeds do v2 - [1082](https://github.com/NuGet/Home/issues/1082)

#### <a name="network-connectivity-had-affected-the-user-interface-in-visual-studio-and-we-addressed-this-with-the-following-fixes"></a>Conectividade de rede tive afetado a interface do usuário no Visual Studio e resolvemos isso com as seguintes correções:

* Aprimorada a manutenção do cache local das versões do pacote – [1096](https://github.com/NuGet/Home/issues/1096)
* Alterado o comportamento de falha ao se conectar a um v3 feed a tentativa de não precisa mais tratá-la como um feed v2 ‑ [1253](https://github.com/NuGet/Home/issues/1253)
* Impedindo que falhas de instalação ao instalar um pacote com várias origens de pacote - [1183](https://github.com/NuGet/Home/issues/1183)

Melhoramos o tratamento de interações com operações de compilação:

* Agora, continue compilar projetos se restaurando pacotes para um único projeto falha - [1169](https://github.com/NuGet/Home/issues/1169)
* Instalar um pacote em um projeto que depende de outro projeto na solução força uma recompilação de solução - [981](https://github.com/NuGet/Home/issues/981)
* Corrigida a instalações de pacote com falha corretamente reverter as alterações a um projeto - [1265](https://github.com/NuGet/Home/issues/1265)
* Corrigida a remoção acidental do `developmentDependency` atributo em um pacote no `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* Chamadas para `install.ps1` agora tem apropriadas `$package.AssemblyReferences` objeto passado - [1245](https://github.com/NuGet/Home/issues/1245)
* Não impedindo que desinstala pacotes em projetos UWP, enquanto o projeto está em um estado inválido - [1128](https://github.com/NuGet/Home/issues/1128)
* Soluções que contêm uma mistura de `packages.config` e `project.json` projetos agora são compilados corretamente sem a necessidade de uma segunda operação - de build [1122](https://github.com/NuGet/Home/issues/1122)
* Localizando corretamente arquivos App. config, se estiverem vinculados ou localizados em uma pasta diferente - [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* Projetos da UWP agora podem instalar os pacotes não listados - [1109](https://github.com/NuGet/Home/issues/1109)
* Restauração de pacote agora é permitida enquanto uma solução não está em um estado salvo - [1081](https://github.com/NuGet/Home/issues/1081)


Administrando atualizações para configuração de arquivos que foram corrigidos:

* Não há mais a remoção de um arquivo de destino entregue de um pacote em compilações subsequentes de uma `project.json` projeto gerenciado - [1288](https://github.com/NuGet/Home/issues/1288)
* Não há mais modificando arquivos NuGet. config durante a compilação da solução ASP.NET 5 - [1201](https://github.com/NuGet/Home/issues/1201)
* Não é mais permitido alterar a restrição de versões durante a atualização do pacote - [1130](https://github.com/NuGet/Home/issues/1130)
* Bloquear arquivos agora permanecem bloqueados durante o build - [1127](https://github.com/NuGet/Home/issues/1127)
* Modificando `packages.config` e não reescrevê-lo durante as atualizações - [585](https://github.com/NuGet/Home/issues/585)


Interações com o controle de origem do TFS são aprimoradas:

* Falha não instala os pacotes que estão associados ao TFS - [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)
* Interface de usuário do NuGet corrigido para permitir a integração do TFS 2013 - [1071](https://github.com/NuGet/Home/issues/1071)
* Corrigidas referências a pacotes restaurados adequadamente que vêm de uma pasta de pacotes - [1004](https://github.com/NuGet/Home/issues/1004)

Por fim, também melhoramos a estes itens:

* Nível de detalhes de mensagens de log é reduzido para `project.json` projetos - gerenciados [1163](https://github.com/NuGet/Home/issues/1163)
* Agora exibir corretamente a versão instalada de um pacote na interface do usuário - [1061](https://github.com/NuGet/Home/issues/1061)


Uma lista completa dos problemas abordados para a extensão do Visual Studio pode ser encontrado no NuGet GitHub [etapa 3.2](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>Problemas Conhecidos

Continuamos a acompanhar os problemas em nossa lista de problemas do GitHub que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)