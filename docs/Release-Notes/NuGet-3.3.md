---
title: "Notas de versão do NuGet 3.3 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de versão do NuGet 3.3 incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão 3.3 do NuGet, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c83f87231497e14c36f1b8100b7bec720bb63b1c
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-33-release-notes"></a>Notas de versão 3.3 do NuGet

[Notas de versão do NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC notas](../release-notes/nuget-3.4-RC.md)

3.3 NuGet foi liberado 30 de novembro de 2015, com um número significativo de atualizações de interface do usuário e recursos de linha de comando, bem como um conjunto de correções úteis para os clientes do NuGet.

## <a name="new-features"></a>Novos recursos

* Foram introduzidos provedores de credenciais que permitem que os clientes de linha de comando do NuGet poder funcionar perfeitamente com um feed autenticado. [Provedor de credenciais de instruções sobre como instalar o Visual Studio Team Services ](../API/nuget-exe-Credential-Providers.md) e configurar o NuGet clientes para usá-lo estão disponíveis em documentos do NuGet.

## <a name="new-user-interface-features"></a>Novos recursos de Interface do usuário

* Guias separadas de procurar, instalar e atualizações disponíveis
* Atualizações de notificação disponível que indica o número de pacotes com atualizações disponíveis
* Notificações de pacote na lista de pacotes para indicar se o pacote está instalado, ou uma atualização disponível
* Baixar a contagem e adicionado à lista de pacotes de autor
* Maior número de versão disponíveis e o número de versão instalada atualmente na lista de pacotes
* Botões de ação para permitir a rápida instalar, atualizar e desinstalar da lista de pacotes
* Botões de ação mais claros no painel de detalhes do pacote
* Data de atualização de pacote no painel de detalhes do pacote
* Consolidar o painel no modo de exibição de solução
* Grade classificável de projetos e os números de versão instalada no modo de exibição de solução

## <a name="new-command-line-features"></a>Novos recursos de linha de comando

Nesta versão, apresentamos o `add` e `init` comandos para inicializar com base em pasta repositórios conforme descrito no [nuget.exe referência](../tools/nuget-exe-cli-reference.md). Estrutura de repositórios que são construídos e mantidos com esta pasta será [fornecer benefícios significativos de desempenho](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) conforme descrito em nosso blog.

## <a name="contentfiles"></a>ContentFiles

Agora há suporte para o conteúdo em `project.json` gerenciados projetos por meio do novo `contentFiles` pasta e `.nuspec` `contentFiles` notação de elemento.  Esse conteúdo pode ser especificado mais diretamente pelo autor do pacote para interações com sistemas de projeto.  Para obter mais informações sobre como configurar contentFiles em uma `.nuspec` documento pode ser encontrado na [. NuSpec referência](../schema/nuspec.md).

## <a name="nuget-locals-cache-management"></a>Gerenciamento de Cache do NuGet locais

O linha de comando do NuGet foi atualizado para incluir informações sobre como gerenciar os caches locais em uma estação de trabalho.  Para obter mais informações sobre o comando locais estão disponíveis na [referência de linha de comando do NuGet](../tools/cli-ref-locals.md).

## <a name="fixed-issues"></a>Problemas corrigidos

**Problemas importantes**

* Pacotes do NuGet restaurado suporte para a restauração com um arquivo de solução Mono - [1543](https://github.com/NuGet/Home/issues/1543)

A lista completa de problemas foram resolvidos na versão 3.3 pode ser encontrada no GitHub sob o [3.3 marco](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).

A lista de problemas corrigidos na versão de linha de comando 3.3 são registradas no [3.3 etapa de linha de comando](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).

## <a name="known-issues"></a>Problemas Conhecidos

Continuamos a rastrear problemas em nossa lista de problemas do GitHub que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)