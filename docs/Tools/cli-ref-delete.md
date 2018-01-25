---
title: Comando do NuGet CLI delete | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referência para o comando de exclusão de nuget.exe"
keywords: "NuGet excluir referência, excluir o comando de pacote"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3890e33ab0fc425e1c2ee39631ade57ea9b92bc9
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="delete-command-nuget-cli"></a>Excluir um comando NuGet CLI)

**Aplica-se a:** pacote publicação &bullet; **versões com suporte:** todos

Exclui ou unlists um pacote de uma origem do pacote. Para nuget.org, o comando Excluir [unlists o pacote](../policies/Deleting-Packages.md).

## <a name="usage"></a>Uso

```cli
nuget delete <packageID> <packageVersion> [options]
```

onde `<packageID>` e `<packageVersion>` identificar o pacote exato para excluir ou remover da lista. O comportamento exato depende da fonte. Para pastas locais, por exemplo, o pacote foi excluído; para o pacote do nuget.org está na lista.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| apiKey | A chave de API para o repositório de destino. Se não estiverem presentes, especificada na *%AppData%\NuGet\NuGet.Config* é usado. |
| ConfigFile | O arquivo de configuração do NuGet para aplicar. Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado. |
| ForceEnglishOutput | *(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Ajuda | Exibe informações de ajuda para o comando. |
| NonInteractive | Suprime avisos para a entrada do usuário ou confirmações. |
| Origem | Especifica a URL do servidor. A URL para nuget.org é `https://api.nuget.org/v3/index.json`. Para feeds privados, substitua o nome de host, por exemplo, *%hostname%/api/v3*. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
