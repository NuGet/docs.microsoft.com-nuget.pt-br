---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860570"
---
<span data-ttu-id="5ec28-101">Use o comando [restore](../../reference/cli-reference/cli-ref-restore.md), que baixa e instala os pacotes ausentes da pasta *packages*.</span><span class="sxs-lookup"><span data-stu-id="5ec28-101">Use the [restore](../../reference/cli-reference/cli-ref-restore.md) command, which downloads and installs any packages missing from the *packages* folder.</span></span>

<span data-ttu-id="5ec28-102">Em projetos migrados para o PackageReference, use [msbuild -t:restore](../package-restore.md#restore-using-msbuild) para restaurar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="5ec28-102">For projects migrated to PackageReference, use [msbuild -t:restore](../package-restore.md#restore-using-msbuild) to restore packages instead.</span></span>

<span data-ttu-id="5ec28-103">`restore` apenas adiciona pacotes ao disco, mas não altera as dependências do projeto.</span><span class="sxs-lookup"><span data-stu-id="5ec28-103">`restore` only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="5ec28-104">Para restaurar as dependências do projeto, modifique `packages.config` e, em seguida, use o comando `restore`.</span><span class="sxs-lookup"><span data-stu-id="5ec28-104">To restore project dependencies, modify `packages.config`, then use the `restore` command.</span></span>

<span data-ttu-id="5ec28-105">Assim como ocorre com outros comandos CLI do `nuget.exe`, primeiro abra uma linha de comando e alterne para o diretório que contém o arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="5ec28-105">As with the other `nuget.exe` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="5ec28-106">Para restaurar um pacote usando `restore`:</span><span class="sxs-lookup"><span data-stu-id="5ec28-106">To restore a package using `restore`:</span></span>

```cli
nuget restore MySolution.sln
```