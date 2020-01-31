---
title: Notas de versão do NuGet 3,3
description: Notas de versão do NuGet 3,3 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa8290c80cc500b59d1779bf76662c07382fd277
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813774"
---
# <a name="nuget-33-release-notes"></a>Notas de versão do NuGet 3,3

[Notas de versão do NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [NuGet 3,4-RC Release Notes](../release-notes/nuget-3.4-RC.md)

O NuGet 3,3 foi lançado em 30 de novembro de 2015 com um número significativo de atualizações de interface do usuário e recursos de linha de comando, bem como uma coleção de correções úteis para os clientes NuGet.

## <a name="new-features"></a>Novos recursos

* Provedores de credenciais foram introduzidos para permitir que os clientes de linha de comando do NuGet possam trabalhar sem problemas com um feed autenticado. [Instruções sobre como instalar o provedor de credenciais Visual Studio Team Services](../reference/extensibility/nuget-exe-credential-providers.md) e configurar os clientes do NuGet para usá-lo estão disponíveis em documentos do NuGet.

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

Nesta versão, apresentamos os comandos `add` e `init` para inicializar repositórios baseados em pasta, conforme descrito na [referência do NuGet. exe](../reference/nuget-exe-cli-reference.md). Os repositórios construídos e mantidos com essa estrutura de pastas fornecerão [benefícios de desempenho significativos](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) , conforme descrito em nosso blog.

## <a name="contentfiles"></a>ContentFiles

Agora há suporte para conteúdo em `project.json` projetos gerenciados por meio da nova pasta `contentFiles` e `.nuspec` notação de elemento `contentFiles`.  Esse conteúdo pode ser especificado mais diretamente pelo autor do pacote para interações com sistemas de projeto.  Mais informações sobre como configurar o contentFiles em um documento `.nuspec` podem ser encontradas na [referência de. nuspec](../reference/nuspec.md).

## <a name="nuget-locals-cache-management"></a>Gerenciamento de cache local do NuGet

A linha de comando do NuGet foi atualizada para incluir informações sobre como gerenciar os caches locais em uma estação de trabalho.  Mais informações sobre o comando locals estão disponíveis na [referência de linha de comando do NuGet](../reference/cli-reference/cli-ref-locals.md).

## <a name="fixed-issues"></a>Problemas corrigidos

**Problemas notáveis**

* Suporte de linha de comando do NuGet restaurado para restaurar pacotes com um arquivo de solução no mono- [1543](https://github.com/NuGet/Home/issues/1543)

A lista completa de problemas que foram resolvidos na versão 3,3 pode ser encontrada no GitHub na [etapa 3,3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).

A lista de problemas corrigidos na versão de linha de comando 3,3 é registrada na [etapa de linha de comando 3,3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).

## <a name="known-issues"></a>Problemas Conhecidos

Continuamos a acompanhar problemas em nossa lista de problemas do GitHub, que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)