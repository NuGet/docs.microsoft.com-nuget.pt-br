---
title: Notas de versão 3.2 do NuGet
description: Notas de versão do NuGet 3.2 incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 938104c50fee19ee398de49c786bbb4963ba1429
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-32-release-notes"></a>Notas de versão 3.2 do NuGet

[Notas de versão 3.2 RC NuGet](../release-notes/nuget-3.2-RC.md) | [notas de versão do NuGet 3.2.1](../release-notes/nuget-3.2.1.md)

3.2 NuGet foi lançado 16 de setembro de 2015 como uma coleção de melhorias e correções para o 3.1.1 e está disponível para ambos [dist.nuget.org](http://dist.nuget.org/index.html) e [Galeria do Visual Studio](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2015).

## <a name="new-features"></a>Novos recursos

* Os projetos que residem na mesma pasta agora podem ter diferentes `project.json` arquivos nessa pasta específica para cada projeto.  Para cada projeto, o nome de `project.json` arquivo `{ProjectName}.project.json` e NuGet dará preferência para que a configuração para cada projeto adequadamente.  Isso só é suportado com a versão 1.1 do Windows 10 ferramentas instaladas - [1102](https://github.com/NuGet/Home/issues/1102)
* Os clientes do NuGet suporte à especificação de uma variável de ambiente NUGET_PACKAGES global para especificar o local da pasta compartilhada pacotes global usado no `project.json` gerenciados projetos com a versão 1.1 do Windows 10 ferramentas.

## <a name="command-line-updates"></a>Atualizações de linha de comando

Essa é a primeira versão do cliente nuget.exe que oferece suporte a servidores NuGet v3 e restaurando pacotes para projetos gerenciados com um `project.json` arquivo.

Houve um número de problemas de feed autenticados que foram abordados nesta versão para aprimorar as interações com o cliente.

* Instalar / restauração interações só enviar as credenciais para a solicitação inicial para o feed autenticado - [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* Comando de envio não resolve as credenciais de configuração - [1248](https://github.com/NuGet/Home/issues/1248)
* Cabeçalhos e agente do usuário agora são enviados para os repositórios NuGet para ajudá-lo com o controle de estatísticas - [929](https://github.com/NuGet/Home/issues/929)

Fizemos vários aprimoramentos para lidar melhor com falhas de rede ao tentar trabalhar com um repositório remoto do NuGet:

* Melhor mensagens de erro quando não é possível conectar-se a feeds remotos - [1238](https://github.com/NuGet/Home/issues/1238)
* Corrigido o comando de restauração do NuGet corretamente retornar 1 quando ocorre uma condição de erro - [1186](https://github.com/NuGet/Home/issues/1186)
* Agora, repetindo as conexões de rede cada 200 ms para um máximo de 5 tentativas no caso de falhas do HTTP 5xx - [1120](https://github.com/NuGet/Home/issues/1120)
* Melhor tratamento de redirecionamento de respostas do servidor durante um comando push - [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` agora dá suporte a nome de URL ou no repositório do NuGet. config como um argumento - [1046](https://github.com/NuGet/Home/issues/1046)
* Os pacotes ausentes que não foram localizados em um repositório durante uma restauração agora são relatados como erros, em vez de avisos [1038](https://github.com/NuGet/Home/issues/1038)
* Corrigido o tratamento de multipartwebrequest de \r\n para cenários de Unix/Linux - [776](https://github.com/NuGet/Home/issues/776)

Há inúmeras correções para problemas com vários comandos:

* Comando de push não faz um GET antes de um PUT em relação a uma origem do pacote - [1237](https://github.com/NuGet/Home/issues/1237)
* Comando Listar não repete números de versão - [1185](https://github.com/NuGet/Home/issues/1185)
* Pacote com argumento-build agora corretamente suporta c# 6.0 - [1107](https://github.com/NuGet/Home/issues/1107)
* Problemas corrigidos tentando empacotar um projeto F # criados com o Visual Studio 2015 - [1048](https://github.com/NuGet/Home/issues/1048)
* Agora não-operações de restauração quando pacotes já existem - [1040](https://github.com/NuGet/Home/issues/1040)
* Mensagens de erro aprimorado quando `packages.config` arquivo está malformado - [1034](https://github.com/NuGet/Home/issues/1034)
* Corrigido o comando restore com a opção - SolutionDirectory para trabalhar com caminhos relativos - [992](https://github.com/NuGet/Home/issues/992)
* Aprimorado o comando atualizado para dar suporte a toda a solução de atualização - [924](https://github.com/NuGet/Home/issues/924)

Uma lista completa dos problemas abordados nesta versão pode ser encontrada no NuGet GitHub [etapa de linha de comando](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate).

## <a name="visual-studio-extension-updates"></a>Atualizações de extensão do Visual Studio

### <a name="new-features-in-visual-studio"></a>Novos recursos no Visual Studio

* Um novo item de menu de contexto foi adicionado ao Gerenciador de soluções, no nó de solução que permite que os pacotes a serem restaurados sem compilar a solução ([1274](https://github.com/NuGet/Home/issues/1274)).

![Item de Menu de contexto de 'Restaurar os pacotes' novo](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Atualizações e correções no Visual Studio

As correções para feeds autenticados foram acumuladas e a extensão também são abordadas.  Os itens de autenticação a seguir também foram resolvidos na extensão:

* Agora tratar corretamente NuGet v3 autenticadas feeds corretamente, em vez de como v2 autenticados feeds - [1216](https://github.com/NuGet/Home/issues/1216)
* Corrigido solicitação de credenciais de autenticação em projetos usando `project.json` e se comunicando com feeds v2 - [1082](https://github.com/NuGet/Home/issues/1082)

Conectividade de rede tinha afetado a interface do usuário no Visual Studio, e nós abordamos isso com as seguintes correções:

* A manutenção do cache local das versões do pacote - aperfeiçoada [1096](https://github.com/NuGet/Home/issues/1096)
* Alterar o comportamento de falha ao se conectar a um v3 feed para não tentar tratá-lo como um feed v2 - [1253](https://github.com/NuGet/Home/issues/1253)
* Impedindo que instala a falhas ao instalar um pacote com várias fontes de pacote - [1183](https://github.com/NuGet/Home/issues/1183)

Melhoramos o tratamento de interações com operações de compilação:

* Agora continuar compilar projetos se restaurando pacotes para um único projeto falha - [1169](https://github.com/NuGet/Home/issues/1169)
* Instalação de um pacote em um projeto que depende de outro projeto na solução força recompilar solução - [981](https://github.com/NuGet/Home/issues/981)
* Corrigido o pacote com falha instala corretamente reverter as alterações a um projeto - [1265](https://github.com/NuGet/Home/issues/1265)
* Corrigida a remoção acidental do `developmentDependency` atributo em um pacote no `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* Chamadas para `install.ps1` agora tem apropriadas `$package.AssemblyReferences` objeto passado - [1245](https://github.com/NuGet/Home/issues/1245)
* Não impedindo desinstala de pacotes em projetos UWP enquanto o projeto está em um estado inválido - [1128](https://github.com/NuGet/Home/issues/1128)
* Soluções que contém uma mistura de `packages.config` e `project.json` projetos agora sejam compilados corretamente sem a necessidade de um segundo criar operação - [1122](https://github.com/NuGet/Home/issues/1122)
* Localizando corretamente arquivos App. config se eles são vinculados ou localizados em uma pasta diferente - [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* Os projetos UWP agora podem instalar pacotes não listados - [1109](https://github.com/NuGet/Home/issues/1109)
* Restauração do pacote agora é permitida enquanto uma solução não está em um estado salvo - [1081](https://github.com/NuGet/Home/issues/1081)

Tratamento de atualizações para configuração de arquivos foram corrigidos:

* Não remover um arquivo de destino entregues a partir de um pacote em compilações subsequentes de um `project.json` projeto gerenciado - [1288](https://github.com/NuGet/Home/issues/1288)
* Não modificar arquivos de config durante a compilação de solução do ASP.NET 5 - [1201](https://github.com/NuGet/Home/issues/1201)
* Não é mais permitido alterar restrição de versões durante a atualização do pacote - [1130](https://github.com/NuGet/Home/issues/1130)
* Arquivos de bloqueio agora permanecem bloqueados durante a compilação - [1127](https://github.com/NuGet/Home/issues/1127)
* Modificando `packages.config` e não reescrevê-los durante atualizações - [585](https://github.com/NuGet/Home/issues/585)

Interações com controle de origem do TFS são aprimoradas:

* Falha não instala os pacotes que estão associados ao TFS - [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)
* Interface do usuário do NuGet corrigido para permitir a integração do TFS 2013 - [1071](https://github.com/NuGet/Home/issues/1071)
* Corrigido referências aos pacotes restaurados para corretamente vêm de uma pasta de pacotes - [1004](https://github.com/NuGet/Home/issues/1004)

Por fim, também melhoramos estes itens:

* Detalhes de mensagens de log é reduzido para `project.json` gerenciados projetos - [1163](https://github.com/NuGet/Home/issues/1163)
* Agora exibir corretamente a versão instalada de um pacote na interface do usuário - [1061](https://github.com/NuGet/Home/issues/1061)
* Pacotes com intervalos de dependência especificados em seu nuspec agora têm versões de pré-lançamento dessas dependências instalado para uma versão do pacote estável - [1304](https://github.com/NuGet/Home/issues/1304)

Uma lista completa dos problemas abordados para a extensão do Visual Studio pode ser encontrada no NuGet GitHub [etapa 3.2](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>Problemas Conhecidos

Continuamos a rastrear problemas em nossa lista de problemas do GitHub que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)