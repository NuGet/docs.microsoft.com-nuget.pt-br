---
title: Comando de lista do NuGet CLI | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 728c8452-0457-4bb8-bfdc-de77fe1570bd
description: "Referência para o comando de lista de nuget.exe"
keywords: "referência de lista do NuGet, comando de pacotes de lista"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 62a7077e7adac1e4d8cf305fd6e66a6ce5ebfb76
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="list-command-nuget-cli"></a>comando Listar (NuGet CLI)

**Aplica-se a:** consumo de pacote, a publicação &bullet; **versões com suporte:** todos

Exibe uma lista de pacotes de uma origem específica. Se nenhuma fonte for especificada, todas as fontes definidas no arquivo de configuração global, `%AppData%\NuGet\NuGet.Config`, são usados. Se `NuGet.Config` não especifica nenhuma fonte, em seguida, `list` usa o feed padrão (nuget.org).

## <a name="usage"></a>Uso

```
nuget list [search terms] [options]
```

onde os termos de pesquisa opcional filtra a lista exibida. Termos de pesquisa são aplicados para os nomes dos pacotes, marcas e descrições do pacote.

## <a name="options"></a>Opções
| Opção | Descrição |
| --- | --- |
| Todasas versões | Lista todas as versões de um pacote. Por padrão, somente a versão mais recente do pacote é exibida. |
| ConfigFile | *(2.5 +)*  NuGet o arquivo de configuração para aplicar. Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado. |
| ForceEnglishOutput | *(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Ajuda | Exibe informações de ajuda para o comando. |
| IncludeDelisted | *(3.2 +)*  Exibir pacotes não listados. |
| Não interativo | Suprime avisos para a entrada do usuário ou confirmações. |
| Versão de pré-lançamento | Inclui pacotes pré-lançados na lista. |
| Origem | Especifica uma lista de fontes de pacotes para pesquisar. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas (2.5 +)*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```
nuget list

nuget list -Verbosity detailed -AllVersions
```
