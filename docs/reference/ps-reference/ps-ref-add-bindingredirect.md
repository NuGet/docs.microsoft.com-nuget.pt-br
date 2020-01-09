---
title: Referência do PowerShell para Add-BindingRedirect do NuGet
description: Referência para o comando Add-BindingRedirect PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d3d156cf882229260e8cf55f8ece2804aec36dc9
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384978"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect (Console do Gerenciador de Pacotes no Visual Studio)

*Disponível somente dentro do [console do Gerenciador de pacotes](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows.*

Examina todos os assemblies no caminho de saída de um projeto e adiciona redirecionamentos de associação ao aplicativo ou ao arquivo de configuração da Web, quando necessário. Esse comando é executado automaticamente ao instalar um pacote.

Para obter detalhes sobre redirecionamentos de associação e por que eles são usados, consulte [Redirecionando versões de assembly](/dotnet/framework/configure-apps/redirect-assembly-versions) na documentação do .net.

## <a name="syntax"></a>Sintaxe

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --- | --- |
| ProjectName | Necessária O projeto ao qual adicionar redirecionamentos de associação. A opção-ProjectName em si é opcional. |

Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.

## <a name="common-parameters"></a>Parâmetros comuns

o `Add-BindingRedirect` dá suporte aos seguintes [parâmetros comuns do PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Exemplos

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```