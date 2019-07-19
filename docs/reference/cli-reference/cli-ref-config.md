---
title: Comando de configuração da CLI do NuGet
description: Referência para o comando de configuração NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 51c4c9937483e7f8a57356515c06a60c0f9e6f62
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327843"
---
# <a name="config-command-nuget-cli"></a>comando config (NuGet CLI)

**Aplica-se a:** todas &bullet; as **versões com suporte**: todas

Obtém ou define os valores de configuração do NuGet. Para uso adicional, consulte [configurações comuns do NuGet](../../consume-packages/configuring-nuget-behavior.md). Para obter detalhes sobre nomes de chave permitidos, consulte a [referência do arquivo de configuração do NuGet](../nuget-config-file.md).

## <a name="usage"></a>Uso

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

onde `<name>` e`<value>` especifique um par chave-valor a ser definido na configuração. Você pode especificar quantos pares desejar. Para remover um valor, especifique o nome e o `=` sinal, mas nenhum valor.

Para nomes de chave permitidos, consulte a [referência do arquivo de configuração do NuGet](../nuget-config-file.md).

No NuGet 3.4 +, `<value>` o pode usar [variáveis de ambiente](cli-ref-environment-variables.md).

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| AsPath | Retorna o valor de configuração como um caminho, ignorado `-Set` quando é usado. |
| ConfigFile | O arquivo de configuração do NuGet a ser modificado. Se não for especificado `%AppData%\NuGet\NuGet.Config` , (Windows) `~/.nuget/NuGet/NuGet.Config` ou (Mac/Linux) será usado.|
| ForceEnglishOutput | *(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês. |
| Help | Exibe informações de ajuda para o comando. |
| NonInteractive | Suprime prompts de entrada ou confirmações do usuário. |
| Verbosity | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

### <a name="examples"></a>Exemplos

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
