---
title: Notas de versão 3.3 do NuGet
description: Notas de versão do NuGet 3.3, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5fb840ab6a1329611e9cf417724bcdcd75efe2df
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546641"
---
# <a name="nuget-33-release-notes"></a>Notas de versão 3.3 do NuGet

[Notas de versão do NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [notas de versão do RC 3.4 do NuGet](../release-notes/nuget-3.4-RC.md)

O NuGet 3.3 foi lançado o dia 30 de novembro de 2015, com um número significativo de atualizações de interface do usuário e recursos de linha de comando, bem como uma coleção de correções úteis para os clientes do NuGet.

## <a name="new-features"></a>Novos recursos

* Foram introduzidos os provedores de credenciais que permitem que os clientes de linha de comando do NuGet ser capaz de trabalhar perfeitamente com um feed autenticado. [Provedor de credenciais de instruções sobre como instalar o Visual Studio Team Services ](../api/nuget-exe-credential-providers.md) e configurar o NuGet para usá-lo, os clientes estão disponíveis no NuGet Docs.

## <a name="new-user-interface-features"></a>Novos recursos de Interface do usuário

* Guias separadas de procurar, instalado e as atualizações disponíveis
* Atualizações disponível selo que indica o número de pacotes com atualizações disponíveis
* Notificações de pacote na lista de pacotes para indicar se o pacote está instalado ou tem uma atualização disponível
* Baixe a contagem e autor adicionado à lista de pacotes
* Maior número de versão disponíveis e o número de versão instalada atualmente na lista de pacotes
* Botões de ação para permitir a instalação rápida, atualizar e desinstalar da lista de pacotes
* Botões de ação mais claros sobre o painel de detalhes do pacote
* Data de atualização de pacote no painel de detalhes do pacote
* Consolidar o painel no modo de exibição de solução
* Grade classificável de projetos e os números da versão instalada no modo de exibição de solução

## <a name="new-command-line-features"></a>Novos recursos de linha de comando

Nesta versão, apresentamos os `add` e `init` comandos para inicializar repositórios baseados em pastas, conforme descrito a [nuget.exe referência](../tools/nuget-exe-cli-reference.md). Estrutura de repositórios que são construídos e mantidos com nessa pasta serão [fornecer benefícios significativos de desempenho](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) conforme descrito em nosso blog.

## <a name="contentfiles"></a>contentFiles

Agora há suporte para o conteúdo no `project.json` projetos por meio do novo gerenciados `contentFiles` pasta e `.nuspec` `contentFiles` notação do elemento.  Esse conteúdo pode ser especificado mais diretamente pelo autor do pacote para interações com os sistemas de projeto.  Para obter mais informações sobre como configurar contentFiles em uma `.nuspec` documento pode ser encontrado na [. NuSpec referência](../reference/nuspec.md).

## <a name="nuget-locals-cache-management"></a>Gerenciamento de Cache do NuGet Locals

O linha de comando do NuGet foi atualizado para incluir informações sobre como gerenciar os caches locais em uma estação de trabalho.  Para obter mais informações sobre o comando locals estão disponíveis na [referência de linha de comando do NuGet](../tools/cli-ref-locals.md).

## <a name="fixed-issues"></a>Problemas corrigidos

**Problemas importantes**

* Suporte restaurado de linha de comando do NuGet para a restauração de pacotes com um arquivo de solução no Mono - [1543](https://github.com/NuGet/Home/issues/1543)

A lista completa de problemas que foram abordados na versão 3.3 pode ser encontrada no GitHub sob o [etapa 3.3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).

A lista de problemas corrigidos na versão de linha de comando 3.3 são registradas na [3.3 marco de linha de comando](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).

## <a name="known-issues"></a>Problemas Conhecidos

Continuamos a acompanhar os problemas em nossa lista de problemas do GitHub que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)