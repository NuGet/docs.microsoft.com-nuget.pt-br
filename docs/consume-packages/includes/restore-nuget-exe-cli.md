---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "68860570"
---
Use o comando [restore](../../reference/cli-reference/cli-ref-restore.md), que baixa e instala os pacotes ausentes da pasta *packages*.

Em projetos migrados para o PackageReference, use [msbuild -t:restore](../package-restore.md#restore-using-msbuild) para restaurar os pacotes.

`restore` apenas adiciona pacotes ao disco, mas não altera as dependências do projeto. Para restaurar as dependências do projeto, modifique `packages.config` e, em seguida, use o comando `restore`.

Assim como ocorre com outros comandos CLI do `nuget.exe`, primeiro abra uma linha de comando e alterne para o diretório que contém o arquivo de projeto.

Para restaurar um pacote usando `restore`:

```cli
nuget restore MySolution.sln
```