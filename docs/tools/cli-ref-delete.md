---
title: Comando de exclusão de CLI do NuGet
description: Referência do comando delete nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3ea2dc3e87d0a626704fe5623d39eaf5bd3f3446
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426117"
---
# <a name="delete-command-nuget-cli"></a>Excluir comando (CLI do NuGet)

**Aplica-se a:** publicação de pacote &bullet; **versões com suporte:** todos os

Exclui ou retira da lista um pacote a partir de uma origem de pacote. Para nuget.org, o comando de exclusão [retira da lista o pacote](../nuget-org/policies/deleting-packages.md).

## <a name="usage"></a>Uso

```cli
nuget delete <packageID> <packageVersion> [options]
```

em que `<packageID>` e `<packageVersion>` identificar o pacote exato para excluir ou remover da lista. O comportamento exato depende do código-fonte. Para pastas locais, por exemplo, o pacote é excluído; para nuget.org, o pacote é removido da lista.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ApiKey | A chave de API para o repositório de destino. Se não estiver presente, aquele especificado no arquivo de configuração será usada. |
| ConfigFile | O arquivo de configuração do NuGet para aplicar. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.|
| ForceEnglishOutput | *(3.5 ou superior)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Help | Exibe informações de ajuda para o comando. |
| NonInteractive | Suprime a solicitações de entrada do usuário ou confirmações. |
| Source | Especifica a URL do servidor. A URL para o nuget.org é `https://api.nuget.org/v3/index.json`. Para feeds privados, substitua o nome de host, por exemplo, *%hostname%/api/v3*. |
| Verbosity | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
