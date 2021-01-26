---
title: Notas de versão do NuGet 3,4
description: Notas de versão do NuGet 3,4 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 794b25e2d81d7a2c297a185bdb34a7cf68535723
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776417"
---
# <a name="nuget-34-release-notes"></a>Notas de versão do NuGet 3,4

Notas de versão do [NuGet 3,4-RC](../release-notes/nuget-3.4-RC.md)  |  [Notas de versão do NuGet 3.4.1](../release-notes/nuget-3.4.1.md)

O NuGet 3,4 foi lançado em 30 de março de 2016 como parte do Visual Studio 2015 atualização 2 e da versão de visualização do Visual Studio 15 e foi criado com algumas filosofias nas mentes:

* Suporte de plataforma cruzada
* Melhorias de desempenho
* Melhorias secundárias da interface do usuário

Os seguintes recursos foram adicionados anteriormente no RC e foram atualizados ou concluídos para a versão 3,4:

## <a name="new-features"></a>Novos recursos

* Os clientes NuGet agora dão suporte à codificação de conteúdo gzip de repositórios
* Suporte para PDBs de pacotes em projetos xproj
* Suporte para ações de compilação do iOS e Android no elemento contentFiles
* Suporte para os monikers do netstandard e do netstandardapp Framework

## <a name="new-user-interface-features"></a>Novos recursos da interface do usuário

* Melhorias significativas de desempenho, especialmente nas guias instalado, atualizações e consolidar
* A origem ' todas as fontes de pacote ' agregada está disponível com a mesclagem apropriada de resultados de pesquisa
* As guias instaladas e atualizadas agora são classificadas alfabeticamente
* Adicionado um botão Atualizar que permite que uma pesquisa seja atualizada
* Opções de Build mais recentes na parte superior da lista de versões

## <a name="updates-and-improvements"></a>Atualizações e aprimoramentos

* Os pacotes referenciados no `project.json` que têm uma versão flutuante não serão atualizados em cada compilação. Em vez disso, eles serão atualizados somente quando forçados a restaurar, limpar, recompilar ou modificar `project.json` .
* as fontes de repositório nuget.org não são mais forçadas para uma configuração de projeto quando você usa a interface do usuário de configuração do NuGet.
* O NuGet não restaura mais os pacotes em projetos compartilhados nem grava um arquivo de bloqueio.
* Melhoramos a falha de rede e a manipulação de tentativas para servidores inacessíveis ou lentos para responder.
* Os comportamentos de teclado e mouse são aprimorados na interface do usuário do Gerenciador de pacotes do Visual Studio.
* Agora, damos suporte ao `project.json` esquema mais recente em DNX.

## <a name="breaking-changes"></a>Alterações de quebra

* Os números de versão do pacote agora são normalizados para o formato *principal*. *secundária*. *patch* - do *pré-lançamento*   Cada um dos principais, os menores e os patches são tratados como inteiros e descartam qualquer zero à esquerda.  As informações de pré-lançamento são tratadas como uma cadeia de caracteres e nenhuma alteração é aplicada a ela. Esses números são usados em consultas pelos clientes do NuGet e pela pesquisa fornecida pelo serviço nuget.org.  Mais detalhes podem ser encontrados nos documentos do NuGet em [versões de pré-lançamento](../create-packages/prerelease-packages.md).

## <a name="known-issues"></a>Problemas conhecidos

* **Problema:** Os usuários do Windows 10 v1511 podem enfrentar problemas ou até mesmo uma falha do Visual Studio com o PowerShell no Visual Studio nos seguintes cenários:
    * Instalando/desinstalando pacotes que têm scripts de install.ps1/uninstall.ps1
    * Carregando projetos que têm um script de init.ps1 (como o EntityFramework)
    * Publicando conteúdo da Web

* **Solução alternativa:** Verifique se a instalação do Windows 10 tem os patches mais recentes aplicados, expecially o 2016 de Janeiro (KB 3124263) ou uma atualização posterior.  Mais detalhes estão disponíveis no [problema do GitHub #1638](http://github.com/nuget/home/issues/1638)

* **Problema:** os redirecionamentos de protocolo do NuGet v2 foram interrompidos.
Os repositórios NuGet personalizados que redirecionam solicitações para um host alternativo não consideram a solicitação de redirecionamento.
* **Solução alternativa:**  Para contornar esse problema, configure o URI do repositório de pacotes em configurações para apontar para o local do servidor Redirecionado.
Para obter mais informações, consulte [solicitação pull do GitHub #387](https://github.com/NuGet/NuGet.Client/pull/387).

Continuamos a acompanhar problemas em nossa lista de problemas do GitHub, que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)