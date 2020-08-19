---
title: Comando Add da CLI do NuGet
description: Referência para o nuget.exe Adicionar comando
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 89d268946243e8eae07e482db48e809a15260c38
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622896"
---
# <a name="add-command-nuget-cli"></a>Adicionar comando (NuGet CLI)

**Aplica-se a**: &bullet; **versões com suporte**para publicação de pacotes: 3.3 +

Adiciona um pacote especificado a uma origem de pacote não HTTP (uma pasta ou caminho UNC) em um layout hierárquico, onde as pastas são criadas para a ID do pacote e o número de versão. Por exemplo:

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      ├─<packageID>.<version>.nupkg.sha512
      └─<packageID>.nuspec
```

Ao restaurar ou atualizar na origem do pacote, o layout hierárquico fornece um desempenho significativamente melhor.

Para expandir todos os arquivos no pacote para a origem do pacote de destino, use a `-Expand` opção. Isso normalmente resulta em subpastas adicionais que aparecem no destino, como `tools` e `lib` .

## <a name="usage"></a>Uso

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

em que `<packagePath>` é o nome do caminho para o pacote a ser adicionado e `<sourcePath>` especifica a origem do pacote baseado em pasta à qual o pacote será adicionado. Não há suporte para fontes HTTP.

## <a name="options"></a>Opções

- **`-ConfigFile`**

  O arquivo de configuração do NuGet a ser aplicado. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.

- **`-Expand`**

  Adiciona todos os arquivos no pacote à origem do pacote.

- **`-ForceEnglishOutput`**

  *(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.
Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.

- **`-?|-help`**

  Exibe informações de ajuda para o comando.

- **`-NonInteractive`**

  Suprime prompts de entrada ou confirmações do usuário.

- **`-src|-Source`**

   Especifica a origem do pacote, que é uma pasta ou compartilhamento UNC, ao qual o nupkg será adicionado. Não há suporte para fontes http.

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
