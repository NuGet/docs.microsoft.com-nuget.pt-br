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
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a>Solução de problemas de erros de restauração de pacote no Visual Studio

> [!Note]
> Esta página aborda os erros comuns ao restaurar pacotes no Visual Studio e as etapas para resolvê-los. Para ver instruções sobre como restaurar pacotes, consulte [Restauração de pacote](../Consume-Packages/Package-Restore.md#enabling-and-disabling-package-restore).

Por padrão, compilar um projeto no Visual Studio automaticamente restaura os pacotes do NuGet referenciados no projeto. No entanto, as compilações falharão se a restauração de pacote estiver desabilitada nas configurações **Ferramentas > Opções > Gerenciador de Pacotes do NuGet > Restauração de Pacote** e os pacotes necessários não estiverem disponíveis no seu computador. Nesses casos, você poderá receber os erros a seguir:

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

Para habilitar a restauração de pacotes, abra **Ferramentas > Opções > Gerenciador de Pacote do NuGet** e selecione as opções para **Permitir que o NuGet baixe os pacotes ausentes** e **Verificar automaticamente se estão faltando pacotes durante o build no Visual Studio**:

![habilitar a restauração de pacote do NuGet em Ferramenta/Opções](../Consume-Packages/media/restore-01-autorestoreoptions.png)

