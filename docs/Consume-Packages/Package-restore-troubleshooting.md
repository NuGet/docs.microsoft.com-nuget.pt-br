---
title: "Solução de problemas da restauração de pacote do NuGet no Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: b70326a0-5bfc-4b7c-881d-7a7d5ebeeed5
description: "Uma descrição de erros de restauração de NuGet comuns no Visual Studio e como solucioná-los."
keywords: "Restauração de pacote do NuGet, restaurando pacotes, solucionando problemas, solução de problemas"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c23a9ed2b7cffbf904018a089ccde000adaa517f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a><span data-ttu-id="cc8d9-104">Solução de problemas de erros de restauração de pacote no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cc8d9-104">Troubleshooting package restore errors in Visual Studio</span></span>

> [!Note]
> <span data-ttu-id="cc8d9-105">Esta página aborda os erros comuns ao restaurar pacotes no Visual Studio e as etapas para resolvê-los.</span><span class="sxs-lookup"><span data-stu-id="cc8d9-105">This page focuses on common errors when restoring packages in Visual Studio and steps to resolve them.</span></span> <span data-ttu-id="cc8d9-106">Para ver instruções sobre como restaurar pacotes, consulte [Restauração de pacote](../Consume-Packages/Package-Restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="cc8d9-106">For how-to restore packages, see [Package restore](../Consume-Packages/Package-Restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="cc8d9-107">Por padrão, compilar um projeto no Visual Studio automaticamente restaura os pacotes do NuGet referenciados no projeto.</span><span class="sxs-lookup"><span data-stu-id="cc8d9-107">By default, building a project in Visual Studio automatically restores NuGet packages referenced in the project.</span></span> <span data-ttu-id="cc8d9-108">No entanto, as compilações falharão se a restauração de pacote estiver desabilitada nas configurações **Ferramentas > Opções > Gerenciador de Pacotes do NuGet > Restauração de Pacote** e os pacotes necessários não estiverem disponíveis no seu computador.</span><span class="sxs-lookup"><span data-stu-id="cc8d9-108">However, builds will fail if package restore is disabled in the **Tools > Options > NuGet Package Manager > Package Restore** settings and the necessary packages are not available on your computer.</span></span> <span data-ttu-id="cc8d9-109">Nesses casos, você poderá receber os erros a seguir:</span><span class="sxs-lookup"><span data-stu-id="cc8d9-109">In these cases you may see the following errors:</span></span>

```
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

```
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name} 
```

<span data-ttu-id="cc8d9-110">Para habilitar a restauração de pacotes, abra **Ferramentas > Opções > Gerenciador de Pacote do NuGet** e selecione as opções para **Permitir que o NuGet baixe os pacotes ausentes** e **Verificar automaticamente se estão faltando pacotes durante o build no Visual Studio**:</span><span class="sxs-lookup"><span data-stu-id="cc8d9-110">To enable package restore, open **Tools > Options > NuGet Package Manager** and select the options for **Allow NuGet to download missing packages** and **Automatically check for missing packages during build in Visual Studio**:</span></span>

![habilitar a restauração de pacote do NuGet em Ferramenta/Opções](../Consume-Packages/media/restore-01-autorestoreoptions.png)

