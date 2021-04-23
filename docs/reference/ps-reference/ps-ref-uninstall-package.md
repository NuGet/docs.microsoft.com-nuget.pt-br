---
title: Referência do NuGet Uninstall-Package PowerShell
description: Referência para Uninstall-Package comando do PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 371e95c341efbce1c4a15facefc15cd51b266141
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901779"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (console do Gerenciador de pacotes no Visual Studio)

*Este tópico descreve o comando no [console do Gerenciador de pacotes](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows. Para o comando genérico Uninstall-Package do PowerShell, consulte a [referência do PackageManagement do PowerShell](/powershell/module/packagemanagement).*

Remove um pacote de um projeto, removendo opcionalmente suas dependências. Se outros pacotes dependem deste pacote, o comando irá falhar, a não ser que a opção –Force esteja especificada.

## <a name="syntax"></a>Sintaxe

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Se outros pacotes dependem deste pacote, o comando irá falhar, a não ser que a opção –Force esteja especificada.

## <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --- | --- |
| ID | Necessária O identificador do pacote a ser desinstalado. A opção-ID em si é opcional. |
| Versão | A versão do pacote a ser desinstalado, padronizando para a versão instalada no momento. |
| RemoveDependencies | Desinstale o pacote e suas dependências não utilizadas. Ou seja, se alguma dependência tiver outro pacote que dependa dele, ela será ignorada. |
| ProjectName | O projeto do qual o pacote será desinstalado, padronizando para o projeto padrão. |
| Force | Força a desinstalação de um pacote, mesmo que outros pacotes dependam dele. |
| WhatIf | Mostra o que aconteceria ao executar o comando sem realmente executar a desinstalação. |

Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.

## <a name="common-parameters"></a>Parâmetros comuns

`Uninstall-Package` o oferece suporte aos seguintes [parâmetros comuns do PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Exemplos

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```