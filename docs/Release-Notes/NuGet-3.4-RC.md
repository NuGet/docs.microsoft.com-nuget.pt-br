---
title: "Notas de versão 3.4 RC NuGet | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de versão do NuGet 3.4 RC incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão RC do NuGet 3.4, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 749068683d6e2a3fd9dd29c69d9ff50137acdd46
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-34-rc-release-notes"></a>Notas de versão 3.4 RC do NuGet

[Notas de versão do NuGet 3.3](../release-notes/nuget-3.3.md) | [notas de versão do NuGet 3.4](../release-notes/nuget-3.4.md)

NuGet 3.4-RC foi lançado 3 de março de 2016, junto com o Visual Studio 2015 atualização 2 RC e foi criado com alguns princípios em mente:

* Suporte de plataforma cruzada
* Melhorias de desempenho
* Pequenos aperfeiçoamentos de interface do usuário

Os seguintes recursos estarão disponíveis neste RC, com mais planejada para a versão final 3.4.

## <a name="new-features"></a>Novos recursos

* Os clientes do NuGet agora suportam a codificação de conteúdo gzip dos repositórios
* Suporte para PDBs de pacotes em projetos xproj
* Suporte para iOS e Android criar ações no elemento contentFiles
* Suporte para os identificadores de netstandard e netstandardapp monikers framework

## <a name="new-user-interface-features"></a>Novos recursos de Interface do usuário

* Melhorias de desempenho significativas, especialmente nas guias instalados, atualizações e consolidar
* Instalado e guias de atualizações agora são classificados em ordem alfabética
* Adicionar um botão de atualização que permite que uma pesquisa a ser atualizado

## <a name="updates-and-improvements"></a>Atualizações e aprimoramentos

* Pacotes referenciados em `project.json` que têm um flutuante versão não será atualizado em cada compilação. Em vez disso, elas serão atualizadas somente quando forçada a restaurar, limpar, recriar ou modificar `project.json`.
* origens de repositório NuGet.org não são forçadas em uma configuração de projeto quando você usa a configuração do NuGet da interface do usuário.
* O NuGet não restaura pacotes em projetos compartilhados nem grava um arquivo de bloqueio.
* Nós já aprimorado falha de rede e tente novamente tratamento para servidores inacessíveis ou lento para responder.
* Comportamentos de teclado e mouse são aprimorados na UI do Gerenciador de pacote do Visual Studio.
* Agora temos suporte para a versão mais recente `project.json` esquema DNX.

## <a name="known-issues"></a>Problemas Conhecidos

Continuamos a rastrear problemas em nossa lista de problemas do GitHub que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)