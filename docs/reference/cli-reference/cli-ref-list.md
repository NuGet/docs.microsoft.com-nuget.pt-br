---
title: Comando de lista da CLI do NuGet
description: Referência para o comando de lista de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 91886dbbdcdb24648289d6f6efbe1f87e4099fff
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623065"
---
# <a name="list-command-nuget-cli"></a>comando List (NuGet CLI)

**Aplica-se a:** consumo de pacote, &bullet; **versões com suporte para publicação:** todos

Exibe uma lista de pacotes de uma determinada origem. Se nenhuma fonte for especificada, todas as fontes definidas no arquivo de configuração global, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` , serão usadas. Se `NuGet.Config` não especificar nenhuma fonte, `list` o usará o feed padrão (NuGet.org).

## <a name="usage"></a>Uso

```cli
nuget list [search terms] [options]
```

onde os termos de pesquisa opcionais filtrarão a lista exibida. Os [termos de pesquisa](/nuget/consume-packages/finding-and-choosing-packages#search-syntax) são aplicados aos nomes de pacotes, marcas e descrições de pacote da mesma forma que quando estão usando-os no NuGet.org. 

## <a name="options"></a>Opções

- **`-AllVersions`**

  Listar todas as versões de um pacote. Por padrão, somente a versão mais recente do pacote é exibida.

- **`-ConfigFile`**

  O arquivo de configuração do NuGet a ser aplicado. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.

- **`-ForceEnglishOutput`**

  *(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.

- **`-?|-help`**

  Exibe informações de ajuda para o comando.

- **`-IncludeDelisted`**

  *(3,2 +)* Exibir pacotes não listados.

- **`-NonInteractive`**

  Suprime prompts de entrada ou confirmações do usuário.

- **`-PreRelease`**

  Inclui pacotes de pré-lançamento na lista.

- **`-Source`**

  Especifica uma lista de fontes de pacotes a serem pesquisadas.

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

Listar todos os pacotes de feeds configurados:
```
nuget list
```
Listar pacotes relacionados ao Azure com detalhes detalhados:
```
nuget list Azure -Verbosity detailed
```
Listar todas as versões de pacotes relacionados ao Azure de feeds configurados:
```
nuget list Azure -AllVersions
```
Listar todas as versões de pacotes relacionados ao JSON de origem/feed especificado:
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
Listar pacotes relacionados a JSON de várias fontes/feeds:
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```
