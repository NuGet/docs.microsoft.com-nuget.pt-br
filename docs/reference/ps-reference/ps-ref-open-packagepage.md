---
title: Referência do NuGet Open-PackagePage PowerShell
description: Referência para Open-PackagePage comando do PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: ba90e09c017ec66d73c35a60025474bc77cf65a7
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238056"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (console do Gerenciador de pacotes no Visual Studio)

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
| ID | A ID do pacote desejado. A opção-ID em si é opcional. |
| Versão | A versão do pacote, padronizando para a versão mais recente. |
| Fonte | A origem do pacote, padronizando para a origem selecionada na lista suspensa origem. |
| Licença | Abre o navegador para a URL de licença do pacote. Se nem-License nem-ReportAbuse for especificado, o navegador abrirá a URL do projeto do pacote. |
| ReportAbuse | Abre o navegador para a URL de abuso de relatório do pacote. Se nem-License nem-ReportAbuse for especificado, o navegador abrirá a URL do projeto do pacote. |
| PassThru | Exibe a URL; Use com-WhatIf para suprimir a abertura do navegador. |

Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.

## <a name="common-parameters"></a>Parâmetros comuns

`Open-PackagePage` o oferece suporte aos seguintes [parâmetros comuns do PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

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