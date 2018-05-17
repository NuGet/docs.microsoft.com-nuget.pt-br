---
title: Referência do PowerShell Get-projeto NuGet
description: Referência de comando do GetProject PowerShell no Console do Gerenciador de pacotes do NuGet no Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a7b66cbf36095e31b5929596300018239749cb15
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (Console do Gerenciador de Pacotes no Visual Studio)

*Disponível apenas dentro de [NuGet Package Manager Console](package-manager-console.md) no Visual Studio no Windows.*

Exibe informações sobre o padrão ou o projeto especificado. `Get-Project` Especificamente, retorna um referente ao objeto DTE (ambiente de ferramentas de desenvolvimento) do Visual Studio para o projeto.

## <a name="syntax"></a>Sintaxe

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --- | --- |
| Nome | Especifica o projeto a ser exibido, padronizando para o projeto padrão selecionado no Console do Gerenciador de pacotes. -Nome do comutador é opcional. |
| Todos | Exibe as informações de todos os projetos na solução. a ordem dos projetos não é determinística. |

Nenhum desses parâmetros aceitar caracteres curinga ou de entrada do pipeline.

## <a name="common-parameters"></a>Parâmetros comuns

`Get-Project` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, WarningAction, detalhado e WarningVariable.

## <a name="examples"></a>Exemplos

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```