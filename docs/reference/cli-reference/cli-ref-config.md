---
title: Comando de configuração da CLI do NuGet
description: Referência para o comando de configuração nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7d0c1c51f40cba9a5b69f209ffbd995451bfeb9f
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622870"
---
# <a name="config-command-nuget-cli"></a>comando config (NuGet CLI)

**Aplica-se a:** todas as &bullet; **versões com suporte**: todas

Obtém ou define os valores de configuração do NuGet. Para uso adicional, consulte [configurações comuns do NuGet](../../consume-packages/configuring-nuget-behavior.md). Para obter detalhes sobre nomes de chave permitidos, consulte a [referência do arquivo de configuração do NuGet](../nuget-config-file.md).

## <a name="usage"></a>Uso

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

onde `<name>` e `<value>` especifique um par chave-valor a ser definido na configuração. Você pode especificar quantos pares desejar. Para remover um valor, especifique o nome e o `=` sinal, mas nenhum valor.

Para nomes de chave permitidos, consulte a [referência do arquivo de configuração do NuGet](../nuget-config-file.md).

No NuGet 3.4 +, o `<value>` pode usar [variáveis de ambiente](cli-ref-environment-variables.md).

## <a name="options"></a>Opções


- **`AsPath`**

  Retorna o valor de configuração como um caminho, ignorado quando `-Set` é usado.

- **`-ConfigFile`**

  O arquivo de configuração do NuGet a ser aplicado. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.

- **`-ForceEnglishOutput`**

  *(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.

- **`-?|-help`**

  Exibe informações de ajuda para o comando.

- **`-NonInteractive`**

  Suprime prompts de entrada ou confirmações do usuário.

- **`-Set`**

  Um em mais pares chave-valor a ser definido na configuração.

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

### <a name="examples"></a>Exemplos

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
