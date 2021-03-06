---
title: Comando de exclusão da CLI do NuGet
description: Referência para o comando nuget.exe Delete
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 96c75366ae69b34f5cd1f55feb53087b5d0ea324
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775952"
---
# <a name="delete-command-nuget-cli"></a>comando Delete (NuGet CLI)

**Aplica-se a:** &bullet; **versões com suporte** para publicação de pacotes: todas

Exclui ou deslista um pacote de uma origem de pacote. Para nuget.org, o comando delete [deslista o pacote](../../nuget-org/policies/deleting-packages.md).

## <a name="usage"></a>Uso

```cli
nuget delete <packageID> <packageVersion> [options]
```

onde `<packageID>` e `<packageVersion>` identificar o pacote exato a ser excluído ou deslistado. O comportamento exato depende da origem. Para pastas locais, por exemplo, o pacote é excluído; para nuget.org, o pacote é não listado.

## <a name="options"></a>Opções

- **`-ApiKey`**

  A chave de API para o repositório de destino. Se não estiver presente, o especificado no arquivo de configuração será usado.

- **`-ConfigFile`**

  O arquivo de configuração do NuGet a ser aplicado. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.

- **`-ForceEnglishOutput`**

  *(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.

- **`-?|-help`**

  Exibe informações de ajuda para o comando.

- **`-NonInteractive`**

  Suprime prompts de entrada ou confirmações do usuário.

 - **`-np|-NoPrompt`**

   Não avisar ao excluir.

 - **`-NoServiceEndpoint`** Não acrescenta "API/v2/packages" à URL de origem.

- **`-src|-Source`**

  Especifica a URL do servidor. A URL para nuget.org é `https://api.nuget.org/v3/index.json` . Para feeds particulares, substitua o nome do host, por exemplo, *% hostname%/API/v3*.

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
