---
title: Referência do PowerShell Get-Project do NuGet
description: Referência para o comando GetProject PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 3343952535c2d3c822f5cac24cb30c8f5bfa5be3
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384614"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (Console do Gerenciador de Pacotes no Visual Studio)

*Disponível somente dentro do [console do Gerenciador de pacotes](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows.*

Exibe informações sobre o projeto padrão ou especificado. `Get-Project` retorna especificamente um referent para o objeto DTE (ambiente de ferramentas de desenvolvimento) do Visual Studio para o projeto.

## <a name="syntax"></a>Sintaxe

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --- | --- |
| Name | Especifica o projeto a ser exibido, padronizando para o projeto padrão selecionado no console do Gerenciador de pacotes. A opção-Name é opcional. |
| {1&gt;Todos&lt;1} | Exibe informações para cada projeto na solução; a ordem dos projetos não é determinística. |

Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.

## <a name="common-parameters"></a>Parâmetros comuns

o `Get-Project` dá suporte aos seguintes [parâmetros comuns do PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Exemplos

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```