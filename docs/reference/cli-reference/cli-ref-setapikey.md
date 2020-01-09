---
title: Comando setapikey da CLI do NuGet
description: Referência para o comando setapikey do NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e2119953e6d07cd3571f156fa0b2665de49f963
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383963"
---
# <a name="setapikey-command-nuget-cli"></a>comando setapikey (NuGet CLI)

**Aplica-se a:** consumo de pacote, publicação &bullet; **versões com suporte:** todos

Salva uma chave de API para uma determinada URL de servidor em `NuGet.Config` para que ela não precise ser inserida para comandos subsequentes.

## <a name="usage"></a>Medição de

```cli
nuget setapikey <key> -Source <url> [options]
```

onde `<source>` identifica o servidor e `<key>` é a chave ou a senha a ser salva. Se `<source>` for omitido, nuget.org será assumido.

> [!NOTE]
> A chave de API não é usada para autenticação com o feed particular. Consulte [`nuget sources` comando](../cli-reference/cli-ref-sources.md) para gerenciar credenciais para autenticação com a origem.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ConfigFile | O arquivo de configuração do NuGet a ser aplicado. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) será usado.|
| ForceEnglishOutput | *(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês. |
| Ajuda | Exibe informações de ajuda para o comando. |
| NonInteractive | Suprime prompts de entrada ou confirmações do usuário. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
