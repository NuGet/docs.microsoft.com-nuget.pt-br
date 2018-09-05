---
title: Referência do PowerShell Get-projeto NuGet
description: Referência de comando do PowerShell de GetProject no Console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 849261711fafcadbab38bf6fe99340c4b79e1e21
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550431"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (Console do Gerenciador de Pacotes no Visual Studio)

*Disponível somente dentro de [NuGet Package Manager Console](package-manager-console.md) no Visual Studio no Windows.*

Exibe informações sobre o padrão ou o projeto especificado. `Get-Project` Especificamente, retorna um referentes ao objeto DTE (ambiente de ferramentas de desenvolvimento) do Visual Studio para o projeto.

## <a name="syntax"></a>Sintaxe

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --- | --- |
| Nome | Especifica o projeto a ser exibido, padronizando para o projeto padrão selecionado no Console do Gerenciador de pacotes. -Nome do comutador é opcional. |
| Todos | Exibe informações para todos os projetos na solução. a ordem dos projetos não é determinística. |

Nenhum desses parâmetros aceitam caracteres curinga ou de entrada do pipeline.

## <a name="common-parameters"></a>Parâmetros comuns

`Get-Project` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detalhado, WarningAction e WarningVariable.

## <a name="examples"></a>Exemplos

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```