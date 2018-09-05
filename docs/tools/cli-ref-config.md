---
title: Comando de configuração de CLI do NuGet
description: Referência do comando de configuração nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 376b69186ad22d4d94a1df51146b833a1f6f9bd9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546472"
---
# <a name="config-command-nuget-cli"></a>configuração de comando (CLI do NuGet)

**Aplica-se a:** todos os &bullet; **versões com suporte**: todos

Obtém ou define os valores de configuração do NuGet. Para uso adicional, consulte [Configurando o comportamento do NuGet](../consume-packages/configuring-nuget-behavior.md). Para obter detalhes sobre nomes de chave permitidos, consulte o [referência de arquivo de configuração do NuGet](../reference/nuget-config-file.md).

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
| Ajuda | Exibe informações de ajuda para o comando. |
| NonInteractive | Suprime a solicitações de entrada do usuário ou confirmações. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

### <a name="examples"></a>Exemplos

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
