---
title: "Referência do PowerShell do NuGet BindingRedirect adicionar | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 90f4dcb0-6e5a-4948-8ea9-62e0d061d95a
description: "Referência de comando do PowerShell Add-BindingRedirect no Console do Gerenciador de pacotes do NuGet no Visual Studio."
keywords: "Pacote de NuGet manager console, comandos do Powershell do NuGet, referência do Powershell do NuGet, adicionar BindingRedirect"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7bf8cdb938195f4747932b38ef0d5bb6c34b9137
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Adicionar-BindingRedirect (Console de Gerenciador de pacotes no Visual Studio)

*Disponível apenas dentro de [NuGet Package Manager Console](Package-Manager-Console.md) no Visual Studio no Windows.*

Examina todos os assemblies no caminho de saída para um projeto e adiciona redirecionamentos de associação para o arquivo de configuração do aplicativo ou da web, quando necessário. Esse comando é executado automaticamente quando a instalação de um pacote.

Para obter detalhes sobre associação redirecionamentos e por que eles são usados, consulte [Redirecting Assembly Versions](https://docs.microsoft.com/dotnet/framework/configure-apps/redirect-assembly-versions) na documentação do .NET.

## <a name="syntax"></a>Sintaxe

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --- | --- |
| ProjectName | (Obrigatório) O projeto ao qual adicionar redirecionamentos de associação. A opção - ProjectName em si é opcional. |

Nenhum desses parâmetros aceitar caracteres curinga ou de entrada do pipeline.

## <a name="common-parameters"></a>Parâmetros comuns

`Add-BindingRedirect`suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, WarningAction, detalhado e WarningVariable.

## <a name="examples"></a>Exemplos

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```