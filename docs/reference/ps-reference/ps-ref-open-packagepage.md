---
title: Referência do PowerShell open-PackagePage do NuGet
description: Referência para o comando Open-PackagePage do PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 39199ebfc37756ed40158a1c07afca7709067350
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384422"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (Console do Gerenciador de Pacotes no Visual Studio)

*Preterido em 3.0 +; disponível somente dentro do [console do Gerenciador de pacotes](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows.*

Inicia o navegador padrão com o projeto, a licença ou a URL de abuso de relatório para o pacote especificado.

## <a name="syntax"></a>Sintaxe

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --- | --- |
| Id | A ID do pacote desejado. A opção-ID em si é opcional. |
| Versão do | A versão do pacote, padronizando para a versão mais recente. |
| Source | A origem do pacote, padronizando para a origem selecionada na lista suspensa origem. |
| Licença | Abre o navegador para a URL de licença do pacote. Se nem-License nem-ReportAbuse for especificado, o navegador abrirá a URL do projeto do pacote. |
| ReportAbuse | Abre o navegador para a URL de abuso de relatório do pacote. Se nem-License nem-ReportAbuse for especificado, o navegador abrirá a URL do projeto do pacote. |
| PassThru | Exibe a URL; Use com-WhatIf para suprimir a abertura do navegador. |

Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.

## <a name="common-parameters"></a>Parâmetros comuns

o `Open-PackagePage` dá suporte aos seguintes [parâmetros comuns do PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

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