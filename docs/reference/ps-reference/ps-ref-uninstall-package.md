---
title: Desinstalação do NuGet-referência do PowerShell do pacote
description: Referência para o comando Uninstall-Package do PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5c963588d28cab42e5fb6a43b31a17e26e49d0d2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327273"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Console do Gerenciador de Pacotes no Visual Studio)

*Este tópico descreve o comando no [console do Gerenciador de pacotes](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows. Para o comando genérico do PowerShell Uninstall-Package, consulte a [referência do PackageManagement do PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*

Remove um pacote de um projeto, removendo opcionalmente suas dependências. Se outros pacotes dependerem desse pacote, o comando falhará, a menos que a opção – Force seja especificada.

## <a name="syntax"></a>Sintaxe

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Se outros pacotes dependerem desse pacote, o comando falhará, a menos que a opção – Force seja especificada.

## <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --- | --- |
| Id | Necessária O identificador do pacote a ser desinstalado. A opção-ID em si é opcional. |
| Versão | A versão do pacote a ser desinstalado, padronizando para a versão instalada no momento. |
| RemoveDependencies | Desinstale o pacote e suas dependências não utilizadas. Ou seja, se alguma dependência tiver outro pacote que dependa dele, ela será ignorada. |
| ProjectName | O projeto do qual o pacote será desinstalado, padronizando para o projeto padrão. |
| Aplicação | Força a desinstalação de um pacote, mesmo que outros pacotes dependam dele. |
| WhatIf | Mostra o que aconteceria ao executar o comando sem realmente executar a desinstalação. |

Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.

## <a name="common-parameters"></a>Parâmetros comuns

`Uninstall-Package`o oferece suporte aos seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Exemplos

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
