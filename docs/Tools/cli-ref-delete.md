---
title: Comando do NuGet CLI delete | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: c213a07a-711d-47e0-9ee6-1d582e6cdb69
description: "Referência para o comando de exclusão de nuget.exe"
keywords: "NuGet excluir referência, excluir o comando de pacote"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 92af9dc356f3932347864976496e0ba1216496c9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="delete-command-nuget-cli"></a>Excluir um comando NuGet CLI)

**Aplica-se a:** pacote publicação &bullet; **versões com suporte:** todos

Exclui ou unlists um pacote de uma origem do pacote. Para nuget.org, o comando Excluir [unlists o pacote](../policies/Deleting-Packages.md).

## <a name="usage"></a>Uso

```
nuget delete <packageID> <packageVersion> [options]
```

onde `<packageID>` e `<packageVersion>` identificar o pacote exato para excluir ou remover da lista. O comportamento exato depende da fonte. Para pastas locais, por exemplo, o pacote foi excluído; para o pacote do nuget.org está na lista.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| apiKey | A chave de API para o repositório de destino. Se não estiverem presentes, especificada na *%AppData%\NuGet\NuGet.Config* é usado. |
| ConfigFile | *(2.5 +)*  NuGet o arquivo de configuração para aplicar. Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado. |
| ForceEnglishOutput | *(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Ajuda | Exibe informações de ajuda para o comando. |
| Não interativo | Suprime avisos para a entrada do usuário ou confirmações. |
| Origem | Especifica a URL do servidor. A URL para nuget.org é `https://api.nuget.org/v3/index.json`. Para feeds privados, substitua o nome de host, por exemplo, *%hostname%/api/v3*. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas (2.5 +)*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
