---
title: "Comando de configuração de CLI do NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referência para o comando de configuração de nuget.exe"
keywords: "referência de configuração NuGet, o comando de configuração"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 34d156a29207122bac3c21c3307cbe7373b5f031
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/20/2018
---
# <a name="config-command-nuget-cli"></a>comando de configuração (NuGet CLI)

**Aplica-se a:** todos os &bullet; **versões com suporte**: todos os

Obtém ou define os valores de configuração do NuGet. Para uso adicional, consulte [Configurando NuGet comportamento](../consume-packages/configuring-nuget-behavior.md). Para obter detalhes sobre nomes de chave permitidos, consulte o [referência do arquivo de configuração NuGet](../reference/nuget-config-file.md).

## <a name="usage"></a>Uso

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

onde `<name>` e `<value>` Especifica um par chave-valor a ser definido na configuração. Você pode especificar quantos pares conforme desejado. Para remover um valor, especifique o nome e o `=` sinal, mas nenhum valor.

Para nomes de chave permitidos, consulte o [referência do arquivo de configuração NuGet](../reference/nuget-config-file.md).

No NuGet 3.4 ou posterior, `<value>` pode usar [variáveis de ambiente](cli-ref-environment-variables.md).

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| AsPath | Retorna a configuração do valor como um caminho, ignorado quando `-Set` é usado. |
| ConfigFile | O arquivo de configuração do NuGet para modificar. Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado. |
| ForceEnglishOutput | *(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Ajuda | Exibe informações de ajuda para o comando. |
| NonInteractive | Suprime avisos para a entrada do usuário ou confirmações. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

### <a name="examples"></a>Exemplos

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
