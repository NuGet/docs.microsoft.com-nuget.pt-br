---
title: Comando de configuração de CLI do NuGet
description: Referência do comando de configuração nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: c0497c7b99a2de6bee37d6d0ead8b055578e60b7
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426072"
---
# <a name="config-command-nuget-cli"></a>configuração de comando (CLI do NuGet)

**Aplica-se a:** todos os &bullet; **versões com suporte**: todos

Obtém ou define os valores de configuração do NuGet. Para uso adicional, consulte [configurações de NuGet comuns](../consume-packages/configuring-nuget-behavior.md). Para obter detalhes sobre nomes de chave permitidos, consulte o [referência de arquivo de configuração do NuGet](../reference/nuget-config-file.md).

## <a name="usage"></a>Uso

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

em que `<name>` e `<value>` especificar um par chave-valor a ser definido na configuração. Você pode especificar quantos pares conforme desejado. Para remover um valor, especifique o nome e o `=` , mas nenhum valor de entrada.

Para nomes de chave permitidos, consulte o [referência de arquivo de configuração do NuGet](../reference/nuget-config-file.md).

No NuGet 3.4 ou superior `<value>` pode usar [variáveis de ambiente](cli-ref-environment-variables.md).

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| AsPath | Retorna a configuração de valor como um caminho, ignorados quando `-Set` é usado. |
| ConfigFile | O arquivo de configuração do NuGet para modificar. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.|
| ForceEnglishOutput | *(3.5 ou superior)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Help | Exibe informações de ajuda para o comando. |
| NonInteractive | Suprime a solicitações de entrada do usuário ou confirmações. |
| Verbosity | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

### <a name="examples"></a>Exemplos

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
