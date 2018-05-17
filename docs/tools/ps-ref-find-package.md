---
title: Referência de PowerShell do NuGet Find-Package
description: Referência de comando do PowerShell de Find-Package no Console do Gerenciador de pacotes do NuGet no Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 0faf5c5cf9ae99105e3d76a4f5e37f164c4f4ff3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (Console do Gerenciador de Pacotes no Visual Studio)

*Versão 3.0 +; Este tópico descreve o comando dentro de [NuGet Package Manager Console](package-manager-console.md) no Visual Studio no Windows. Para o comando PowerShell Find-Package genérico, consulte o [referência do PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Obtém o conjunto de pacotes remotos com a ID ou palavras-chave especificada da origem do pacote.

## <a name="syntax"></a>Sintaxe

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --- | --- |
| ID &lt;palavras-chave&gt; | (Obrigatório) Palavras-chave a ser usado ao procurar a origem do pacote. Use - ExactMatch para retornar somente os pacotes cuja ID de pacote coincide com as palavras-chave. Se nenhuma palavra-chave for fornecido, `Find-Package` retorna uma lista dos pacotes 20 principais downloads ou o número especificada por - primeiro. Observe que - Id é opcional e não operacional. |
| Origem | O caminho de URL ou pasta para a origem do pacote a ser pesquisado. Caminhos de pasta local podem ser absoluto ou relativo para a pasta atual. Se omitido, `Find-Package` procura a origem de pacote selecionada atualmente. |
| Todasas versões | Exibe todas as versões disponíveis de cada pacote em vez de apenas a versão mais recente. |
| Primeiro | O número de pacotes a serem retornados desde o início da lista; o padrão é 20. |
| Skip | Omite o primeiro &lt;int&gt; pacotes na lista exibida.  |
| IncludePrerelease | Inclui pacotes pré-lançados nos resultados. |
| ExactMatch | Especificado para usar &lt;palavras-chave&gt; como uma ID de pacote diferencia maiusculas de minúsculas. |
| StartWith | Retorna pacotes cujo começa com a ID de pacote &lt;palavras-chave&gt;. |

Nenhum desses parâmetros aceitar caracteres curinga ou de entrada do pipeline.

## <a name="common-parameters"></a>Parâmetros comuns

`Find-Package` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, WarningAction, detalhado e WarningVariable.

## <a name="examples"></a>Exemplos

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```