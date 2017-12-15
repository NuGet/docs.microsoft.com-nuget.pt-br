---
title: NuGet CLI adicionar comando | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 4f68a016-ad4e-41fc-b869-88910fc5121e
description: "Comando de adicionar a referência para o nuget.exe"
keywords: "NuGet adicionar referência, adicione o comando de pacote"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: bf9a6e51dfbf1716ba40273487b76ae04c18e948
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="add-command-nuget-cli"></a>Adicionar um comando NuGet CLI)

**Aplica-se a**: a publicação do pacote &bullet; **versões com suporte**: 3.3 +

Adiciona um pacote especificado para uma origem de pacote não HTTP (uma pasta ou caminho UNC) em um layout hierárquico, no qual as pastas são criadas para o número de ID e a versão do pacote. Por exemplo:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

Ao restaurar ou atualizar em relação a origem do pacote, o layout hierárquico fornece um desempenho significativamente melhor.

Para expandir todos os arquivos no pacote de origem do pacote de destino, use o `-Expand` alternar. Isso normalmente resulta em subpastas adicionais que aparecem no destino, como `tools` e `lib`.

## <a name="usage"></a>Uso

```
nuget add <packagePath> -Source <sourcePath> [options]
```

onde `<packagePath>` é o nome do caminho para o pacote a ser adicionado e `<sourcePath>` Especifica a origem de pacote com base em pasta à qual o pacote será adicionado. Não há suporte para fontes HTTP.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ConfigFile | O arquivo de configuração do NuGet para aplicar. Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado.| 
| Expandir | Adiciona todos os arquivos no pacote de origem do pacote. |
| ForceEnglishOutput | *(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Ajuda | Exibe informações de ajuda para o comando. |
| Não interativo | Suprime avisos para a entrada do usuário ou confirmações. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
