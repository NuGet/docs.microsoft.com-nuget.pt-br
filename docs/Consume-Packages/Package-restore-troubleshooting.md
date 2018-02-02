---
title: "Solução de problemas da restauração de pacote do NuGet no Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Uma descrição de erros de restauração de NuGet comuns no Visual Studio e como solucioná-los."
keywords: "Restauração de pacote do NuGet, restaurando pacotes, solucionando problemas, solução de problemas"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c0993e2585452e3c64da28d14bb1bbe1bea27768
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2018
---
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a>Solução de problemas de erros de restauração de pacote no Visual Studio

> [!Note]
> Esta página aborda os erros comuns ao restaurar pacotes no Visual Studio e as etapas para resolvê-los. Para ver instruções sobre como restaurar pacotes, consulte [Restauração de pacote](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

Por padrão, compilar um projeto no Visual Studio automaticamente restaura os pacotes do NuGet referenciados no projeto. No entanto, as compilações falharão se a restauração de pacote estiver desabilitada nas configurações **Ferramentas > Opções > Gerenciador de Pacotes do NuGet > Restauração de Pacote** e os pacotes necessários não estiverem disponíveis no seu computador. Nesses casos, você poderá receber os erros a seguir:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name} 
```

Para habilitar a restauração de pacotes, abra **Ferramentas > Opções > Gerenciador de Pacote do NuGet** e selecione as opções para **Permitir que o NuGet baixe os pacotes ausentes** e **Verificar automaticamente se estão faltando pacotes durante o build no Visual Studio**:

![habilitar a restauração de pacote do NuGet em Ferramenta/Opções](../consume-packages/media/restore-01-autorestoreoptions.png)
