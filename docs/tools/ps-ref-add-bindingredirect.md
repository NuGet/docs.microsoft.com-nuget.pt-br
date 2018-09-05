---
title: Referência do PowerShell BindingRedirect adicionar NuGet
description: Referência de comando do PowerShell Add-BindingRedirect no Console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: dec7db04c5cf239863b9c00e9f5bc0dde42c7e47
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551651"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect (Console do Gerenciador de Pacotes no Visual Studio)

*Disponível somente dentro de [NuGet Package Manager Console](package-manager-console.md) no Visual Studio no Windows.*

Examina todos os assemblies no caminho de saída para um projeto e adiciona redirecionamentos de ligação ao arquivo de configuração da web ou aplicativo, onde for necessário. Esse comando é executado automaticamente ao instalar um pacote.

Para obter detalhes sobre associação de redirecionamentos e por que eles são usados, consulte [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) na documentação do .NET.

## <a name="syntax"></a>Sintaxe

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --- | --- |
| ProjectName | (Obrigatório) O projeto ao qual adicionar redirecionamentos de associação. O comutador - ProjectName em si é opcional. |

Nenhum desses parâmetros aceitam caracteres curinga ou de entrada do pipeline.

## <a name="common-parameters"></a>Parâmetros comuns

`Add-BindingRedirect` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detalhado, WarningAction e WarningVariable.

## <a name="examples"></a>Exemplos

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```