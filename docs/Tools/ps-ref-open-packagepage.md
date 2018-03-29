---
title: Referência do PowerShell do NuGet Open-PackagePage | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referência de comando do PowerShell PackagePage abrir no Console do Gerenciador de pacotes do NuGet no Visual Studio.
keywords: Pacote de NuGet manager console, comandos do Powershell do NuGet, referência do Powershell do NuGet, abrir PackagePage
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 5e0955e58daacf381666c676c8fcf22c698e9db6
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Abra-PackagePage (Console de Gerenciador de pacotes no Visual Studio)

*Preterido no 3.0 +; disponível apenas dentro de [NuGet Package Manager Console](package-manager-console.md) no Visual Studio no Windows.*

Inicia o navegador padrão com o projeto, a licença ou a URL para o pacote especificado abuso.

## <a name="syntax"></a>Sintaxe

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --- | --- |
| Id | A ID do pacote do pacote desejado. -Id switch é opcional. |
| Versão | A versão do pacote, o padrão para a versão mais recente. |
| Origem | A origem do pacote, o padrão para a fonte selecionada na fonte de lista suspensa. |
| Licença | Abre o navegador a URL de licença do pacote. Se - licença nem - ReportAbuse for especificado, o navegador abre a URL do projeto do pacote. |
| ReportAbuse | Abre o navegador a URL de abuso de relatório do pacote. Se - licença nem - ReportAbuse for especificado, o navegador abre a URL do projeto do pacote. |
| PassThru | Exibe a URL; Use com - WhatIf para suprimir a abrir o navegador. |

Nenhum desses parâmetros aceitar caracteres curinga ou de entrada do pipeline.

## <a name="common-parameters"></a>Parâmetros comuns

`Open-PackagePage` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, WarningAction, detalhado e WarningVariable.

## <a name="examples"></a>Exemplos

```ps
# Opens a browser with the Ninject package's project page
Open-PackagePage Ninject

# Opens a browser with the Ninject package's license page
Open-PackagePage Ninject -License

# Opens a browser with the Ninject package's report abuse page  
Open-PackagePage Ninject -ReportAbuse

# Assigns the license URL to the variable, $url, without launching the browser
$url = Open-PackagePage Ninject -License -PassThru -WhatIf
```