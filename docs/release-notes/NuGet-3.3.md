---
title: Notas de versão do NuGet 3,3
description: Notas de versão do NuGet 3,3 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cd3f8c9c4586c608d41e7b8bfc413acfc6aff497
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776512"
---
# <a name="nuget-33-release-notes"></a>Notas de versão do NuGet 3,3

Notas de versão do [NuGet 3.2.1](../release-notes/nuget-3.2.1.md)  |  [Notas de versão do NuGet 3,4-RC](../release-notes/nuget-3.4-RC.md)

O NuGet 3,3 foi lançado em 30 de novembro de 2015 com um número significativo de atualizações de interface do usuário e recursos de linha de comando, bem como uma coleção de correções úteis para os clientes NuGet.

## <a name="new-features"></a>Novos recursos

* Provedores de credenciais foram introduzidos para permitir que os clientes de linha de comando do NuGet possam trabalhar sem problemas com um feed autenticado. [Instruções sobre como instalar o provedor de credenciais Visual Studio Team Services ](../reference/extensibility/nuget-exe-credential-providers.md) e configurar os clientes do NuGet para usá-lo estão disponíveis em documentos do NuGet.

## <a name="new-user-interface-features"></a>Novos recursos da interface do usuário

* Guias de procurar, instalar e atualizar disponíveis separados
* Notificação de atualizações disponíveis indicando o número de pacotes com atualizações disponíveis
* Notificações de pacote na lista de pacotes para indicar se o pacote está instalado ou se tem uma atualização disponível
* Baixar a contagem e o autor adicionados à lista de pacotes
* Número de versão mais alto disponível e número de versão atualmente instalado na lista de pacotes
* Botões de ação para permitir instalação, atualização e desinstalação rápida na lista de pacotes
* Botões de ação mais claros no painel de detalhes do pacote
* Data de atualização do pacote no painel de detalhes do pacote
* Painel consolidar no modo de exibição de solução
* Grade classificável de projetos e números de versão instalados no modo de exibição de solução

## <a name="new-command-line-features"></a>Novos recursos de linha de comando

Nesta versão, apresentamos os `add` `init` comandos e para inicializar repositórios baseados em pasta, conforme descrito na [ referência denuget.exe](../reference/nuget-exe-cli-reference.md). Os repositórios construídos e mantidos com essa estrutura de pastas fornecerão [benefícios de desempenho significativos](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) , conforme descrito em nosso blog.

## <a name="contentfiles"></a>ContentFiles

Agora há suporte para conteúdo em `project.json` projetos gerenciados por meio da nova `contentFiles` notação de pasta e `.nuspec` `contentFiles` elemento.  Esse conteúdo pode ser especificado mais diretamente pelo autor do pacote para interações com sistemas de projeto.  Mais informações sobre como configurar o contentFiles em um `.nuspec` documento podem ser encontradas na [referência de. nuspec](../reference/nuspec.md).

## <a name="nuget-locals-cache-management"></a>Gerenciamento de cache local do NuGet

A linha de comando do NuGet foi atualizada para incluir informações sobre como gerenciar os caches locais em uma estação de trabalho.  Mais informações sobre o comando locals estão disponíveis na [referência de linha de comando do NuGet](../reference/cli-reference/cli-ref-locals.md).

## <a name="fixed-issues"></a>Problemas corrigidos

**Problemas notáveis**

* Suporte de linha de comando do NuGet restaurado para restaurar pacotes com um arquivo de solução no mono- [1543](https://github.com/NuGet/Home/issues/1543)

A lista completa de problemas que foram resolvidos na versão 3,3 pode ser encontrada no GitHub na [etapa 3,3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).

A lista de problemas corrigidos na versão de linha de comando 3,3 é registrada na [etapa 3,3 Command-Line](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).

## <a name="known-issues"></a>Problemas conhecidos

Continuamos a acompanhar problemas em nossa lista de problemas do GitHub, que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)