---
title: Referência do PowerShell aberta-PackagePage do NuGet
description: Referência de comando do PowerShell de PackagePage aberto no Console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 0325aa4ddd718a901dd6a09cdf86cae260e326ab
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547162"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (Console do Gerenciador de Pacotes no Visual Studio)

*Preterido no 3.0 ou superior; disponível somente dentro de [NuGet Package Manager Console](package-manager-console.md) no Visual Studio no Windows.*

Inicia o navegador padrão com o projeto, a licença ou a URL para relatar abuso para o pacote especificado.

## <a name="syntax"></a>Sintaxe

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --- | --- |
| Id | A ID do pacote do pacote desejado. -Id do comutador em si é opcional. |
| Versão | A versão do pacote, padronizando para a versão mais recente. |
| Origem | A origem do pacote, padronizando para a fonte selecionada na lista suspensa origem. |
| Licença | Abre o navegador a URL de licença do pacote. Se nem - licença nem - ReportAbuse for especificado, o navegador abre a URL do projeto do pacote. |
| ReportAbuse | Abre o navegador a URL para relatar abuso do pacote. Se nem - licença nem - ReportAbuse for especificado, o navegador abre a URL do projeto do pacote. |
| PassThru | Exibe a URL; Use com - WhatIf para suprimir abrindo o navegador. |

Nenhum desses parâmetros aceitam caracteres curinga ou de entrada do pipeline.

## <a name="common-parameters"></a>Parâmetros comuns

`Open-PackagePage` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detalhado, WarningAction e WarningVariable.

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