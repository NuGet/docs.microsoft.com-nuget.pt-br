---
title: Referência do PowerShell NuGet Find-Package
description: Referência de comando do PowerShell de Find-Package no Console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: c6797e3778c7095a9abfc6cd87e2337313988c20
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550972"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (Console do Gerenciador de Pacotes no Visual Studio)

*Versão 3.0 ou superior; Este tópico descreve o comando dentro de [NuGet Package Manager Console](package-manager-console.md) no Visual Studio no Windows. Para o comando Find-Package PowerShell genérico, consulte o [referência do PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Obtém o conjunto de pacotes remotos com o ID ou palavras-chave especificada da origem do pacote.

## <a name="syntax"></a>Sintaxe

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --- | --- |
| ID &lt;palavras-chave&gt; | (Obrigatório) Palavras-chave a ser usado ao procurar a origem do pacote. Use - ExactMatch para retornar somente os pacotes cuja ID de pacote corresponde as palavras-chave. Se nenhuma palavra-chave é fornecidas, `Find-Package` retorna uma lista dos pacotes 20 principais downloads, ou o número especificada pelo - primeiro. Observe que - Id é opcional e não operacional. |
| Origem | O caminho de URL ou pasta para a origem do pacote a pesquisar. Caminhos de pasta local podem ser absoluto ou relativo à pasta atual. Se omitido, `Find-Package` procura a origem do pacote selecionado no momento. |
| AllVersions | Exibe todas as versões disponíveis de cada pacote em vez de apenas a versão mais recente. |
| Primeiro | O número de pacotes para retornar do início da lista; o padrão é 20. |
| Skip | Omite o primeiro &lt;int&gt; pacotes na lista exibida.  |
| IncludePrerelease | Inclui pacotes pré-lançados nos resultados. |
| ExactMatch | Especificado para usar &lt;palavras-chave&gt; como uma ID do pacote diferencia maiusculas de minúsculas. |
| StartWith | Retorna pacotes cujo começa com a ID de pacote &lt;palavras-chave&gt;. |

Nenhum desses parâmetros aceitam caracteres curinga ou de entrada do pipeline.

## <a name="common-parameters"></a>Parâmetros comuns

`Find-Package` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detalhado, WarningAction e WarningVariable.

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
