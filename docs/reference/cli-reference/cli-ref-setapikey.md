---
title: Comando setapikey da CLI do NuGet
description: Referência para o comando nuget.exe setapikey
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b84d4257c580f6e734c26ebfc589be27bea10c82
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622805"
---
# <a name="setapikey-command-nuget-cli"></a>comando setapikey (NuGet CLI)

**Aplica-se a:** consumo de pacote, &bullet; **versões com suporte para publicação:** todos

Salva uma chave de API para uma determinada URL de servidor no `NuGet.Config` para que ela não precise ser inserida para comandos subsequentes.

## <a name="usage"></a>Uso

```cli
nuget setapikey <key> -Source <url> [options]
```

onde o `<source>` identifica o servidor e `<key>` é a chave a ser salva. Se `<source>` for omitido, NuGet.org será assumido. 

> [!NOTE]
> A chave de API não é usada para autenticação com o feed particular. Consulte o [ `nuget sources` comando](../cli-reference/cli-ref-sources.md) para gerenciar as credenciais de autenticação com a origem.
> As chaves de API podem ser obtidas dos servidores NuGet individuais. Para criar e gerenciar APIKeys para nuget.org, consulte [adquirir-a-API-Key](../../nuget-org/scoped-api-keys.md#acquire-an-api-key)

## <a name="options"></a>Opções

- **`-ConfigFile`**

  O arquivo de configuração do NuGet a ser aplicado. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.

- **`-ForceEnglishOutput`**

  *(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.

- **`-?|-help`**

  Exibe informações de ajuda para o comando.

- **`-NonInteractive`**

  Suprime prompts de entrada ou confirmações do usuário.

- **`-src|-Source`**

  URL do servidor em que a chave de API é válida.

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
