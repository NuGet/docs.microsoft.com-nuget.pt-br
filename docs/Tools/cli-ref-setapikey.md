---
title: Comando do NuGet CLI setapikey | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referência para o comando de setapikey nuget.exe"
keywords: "NuGet setapikey referência, o comando setapikey"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ca6caddbf1404bcaa1ca068c9556f7cf0c651947
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="setapikey-command-nuget-cli"></a>comando setapikey (NuGet CLI)

**Aplica-se a:** consumo de pacote, a publicação &bullet; **versões com suporte:** todos

Salva uma chave de API para uma URL de servidor específico em `NuGet.Config` para que ele não precisa ser inserido para os comandos subsequentes.

## <a name="usage"></a>Uso

```cli
nuget setapikey <key> -Source <url> [options]
```

onde `<source>` identifica o servidor e `<key>` é a chave ou senha para salvar. Se `<source>` for omitido, nuget.org é assumido.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ConfigFile | O arquivo de configuração do NuGet para modificar. Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado. |
| ForceEnglishOutput | *(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Ajuda | Exibe informações de ajuda para o comando. |
| NonInteractive | Suprime avisos para a entrada do usuário ou confirmações. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
