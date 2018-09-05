---
title: Notas de versão 3.4 do NuGet
description: Notas de versão do NuGet 3.4, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 77c0117fc40031a327e8dcb0aac5cd4045239e97
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551185"
---
# <a name="nuget-34-release-notes"></a>Notas de versão 3.4 do NuGet

[Notas de versão do RC 3.4 do NuGet](../release-notes/nuget-3.4-RC.md) | [notas de versão do NuGet 3.4.1](../release-notes/nuget-3.4.1.md)

NuGet 3.4 foi lançado em 30 de março de 2016 como parte do Visual Studio 2015 atualização 2 e versão de visualização do Visual Studio 15 e foi criado com alguns princípios em mente:

* Suporte de plataforma cruzada
* Melhorias de desempenho
* Pequenos aperfeiçoamentos de interface do usuário

Os seguintes recursos foram adicionados anteriormente no RC e foram atualizados ou concluídos para a versão 3.4:

## <a name="new-features"></a>Novos recursos

* Os clientes do NuGet agora dão suporte a codificação de conteúdo gzip de repositórios
* Suporte para PDBs de pacotes em projetos xproj
* Suporte para iOS e ações de build do Android no elemento contentFiles
* Suporte para o netstandard e netstandardapp monikers de estrutura

## <a name="new-user-interface-features"></a>Novos recursos de Interface do usuário

* Melhorias de desempenho significativas, especialmente nas guias instalado, as atualizações e consolidar
* Origem de 'Todas as origens de pacote' agregada está disponível com a mesclagem de resultados de pesquisa apropriada
* Instalado e guias de atualizações agora estão classificadas em ordem alfabética
* Adicionado um botão de atualização que permite que uma pesquisa a ser atualizado
* Opções de Build mais recente na parte superior da lista de versão

## <a name="updates-and-improvements"></a>Atualizações e aprimoramentos

* Pacotes referenciados no `project.json` que têm um flutuante versão não será atualizada em cada compilação. Em vez disso, eles serão atualizados somente quando forçado a restaurar, limpar, recompilar ou modificar `project.json`.
* origens de repositório de NuGet.org não são forçadas em uma configuração de projeto quando você usa a interface do usuário de configuração do NuGet.
* Não há mais o NuGet restaura pacotes em projetos compartilhados nem grava um arquivo de bloqueio.
* Nós aprimoramos falha de rede e tente novamente o tratamento para servidores inacessíveis ou lento para responder.
* Comportamentos de teclado e mouse estão aprimorados na UI do Gerenciador de pacotes do Visual Studio.
* Agora, damos suporte a versão mais recente `project.json` esquema em DNX.

## <a name="breaking-changes"></a>Alterações significativas

* Números de versão do pacote agora são normalizados para o formato *principais*. *pequenas*. *patch*-*pré-lançamento* cada um dos principais, secundária e patch são tratados como inteiros e descartar quaisquer zeros à esquerda.  As informações de pré-lançamento são tratadas como uma cadeia de caracteres e nenhuma alteração será aplicada a ele. Esses números são usados em consultas, os clientes do NuGet e a pesquisa fornecidos pelo serviço do nuget.org.  Mais detalhes podem ser encontrados nos documentos do NuGet, sob [versões de pré-lançamento](../create-packages/prerelease-packages.md).

## <a name="known-issues"></a>Problemas Conhecidos

* **Problema:** usuários do Windows 10 v1511 poderão enfrentar problemas ou até mesmo uma falha do Visual Studio com o Powershell no Visual Studio nos seguintes cenários:
    * Instalar / desinstalar pacotes que tenham install.ps1 / scripts uninstall.ps1
    * Carregamento de projetos que têm um script init.ps1 causa (como o EntityFramework.)
    * Publicação de conteúdo da web

* **Solução alternativa:** Certifique-se de que a instalação do Windows 10 tem os patches mais recentes aplicados, expecially janeiro de 2016 (KB 3124263) ou uma atualização posterior.  Mais detalhes estão disponíveis em [problema do GitHub #1638](http://github.com/nuget/home/issues/1638)

* **Problema:** os redirecionamentos de protocolo do NuGet v2 foram interrompidos.
Os repositórios NuGet personalizados que redirecionam solicitações para um host alternativo não consideram a solicitação de redirecionamento.
* **Solução alternativa:** para contornar esse problema, configure o URI do repositório de pacote nas configurações para apontar para o local do servidor redirecionado.
Para obter mais informações, consulte [solicitação de recepção GitHub #387](https://github.com/NuGet/NuGet.Client/pull/387).

Continuamos a acompanhar os problemas em nossa lista de problemas do GitHub que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)