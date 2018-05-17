---
title: Referência de PowerShell do NuGet Uninstall-Package
description: Referência de comando do PowerShell do pacote de desinstalação no Console do Gerenciador de pacotes do NuGet no Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5969526a12cb6e06f23f35a2481d0385bb9780ab
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Console do Gerenciador de Pacotes no Visual Studio)

*Este tópico descreve o comando dentro de [NuGet Package Manager Console](package-manager-console.md) no Visual Studio no Windows. Para o comando genérico do pacote de desinstalação do PowerShell, consulte o [referência do PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Remove um pacote de um projeto, opcionalmente, a remoção de suas dependências. Se outros pacotes dependerem deste pacote, o comando falhará, a menos que – Force opção é especificada.

## <a name="syntax"></a>Sintaxe

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Se outros pacotes dependerem deste pacote, o comando falhará, a menos que – Force opção é especificada.

## <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --- | --- |
| Id | (Obrigatório) O identificador do pacote a ser desinstalado. -Id switch é opcional. |
| Versão | A versão do pacote para desinstalar, padronizando para a versão atualmente instalada. |
| RemoveDependencies | Desinstale o pacote e suas dependências não usadas. Ou seja, se qualquer dependência tiver outro pacote que depende dele, ele é ignorado. |
| ProjectName | O projeto do qual deseja desinstalar o pacote, o padrão para o projeto padrão. |
| Force | Força um pacote a ser desinstalado, mesmo se outros pacotes dependem dele. |
| WhatIf | Mostra o que aconteceria quando a execução do comando sem realmente executar a desinstalação. |

Nenhum desses parâmetros aceitar caracteres curinga ou de entrada do pipeline.

## <a name="common-parameters"></a>Parâmetros comuns

`Uninstall-Package` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, WarningAction, detalhado e WarningVariable.

## <a name="examples"></a>Exemplos

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```