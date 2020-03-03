---
title: Comando setapikey da CLI do NuGet
description: Referência para o comando setapikey do NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e06cfb5b355dfae8104090db7babdecdf9e9fec1
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231221"
---
# <a name="setapikey-command-nuget-cli"></a>comando setapikey (NuGet CLI)

**Aplica-se a:** consumo de pacote, publicação &bullet; **versões com suporte:** todos

Salva uma chave de API para uma determinada URL de servidor em `NuGet.Config` para que ela não precise ser inserida para comandos subsequentes.

## <a name="usage"></a>Uso

```cli
nuget setapikey <key> -Source <url> [options]
```

onde `<source>` identifica o servidor e `<key>` é a chave a ser salva. Se `<source>` for omitido, nuget.org será assumido. 

> [!NOTE]
> A chave de API não é usada para autenticação com o feed particular. Consulte [`nuget sources` comando](../cli-reference/cli-ref-sources.md) para gerenciar credenciais para autenticação com a origem.
> As chaves de API podem ser obtidas dos servidores NuGet individuais. Para criar e gerenciar APIKeys para nuget.org, consulte [Publish-API-Key](../../quickstart/includes/publish-api-key.md)

## <a name="options"></a>Opções

| Opção | DESCRIÇÃO |
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
