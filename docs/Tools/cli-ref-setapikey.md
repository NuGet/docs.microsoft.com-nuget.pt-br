---
title: Comando do NuGet CLI setapikey | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a64c0462-973d-4100-ba3f-8902a2b127f7
description: "Referência para o comando de setapikey nuget.exe"
keywords: "NuGet setapikey referência, o comando setapikey"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a07c35b8bdd57157391e391e04a90204342b1d5c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
## <a name="setapikey-command-nuget-cli"></a>comando setapikey (NuGet CLI)

**Aplica-se a:** consumo de pacote, a publicação &bullet; **versões com suporte:** todos

Salva uma chave de API para uma URL de servidor específico em `NuGet.Config` para que ele não precisa ser inserido para os comandos subsequentes.

## <a name="usage"></a>Uso

```
nuget setapikey <key> -Source <url> [options]
```

onde `<source>` identifica o servidor e `<key>` é a chave ou senha para salvar. Se `<source>` for omitido, nuget.org é assumido.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ConfigFile | *(2.5 +)*  NuGet o arquivo de configuração para modificar. Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado. |
| ForceEnglishOutput | *(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Ajuda | Exibe informações de ajuda para o comando. |
| Não interativo | Suprime avisos para a entrada do usuário ou confirmações. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas (2.5 +)*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
