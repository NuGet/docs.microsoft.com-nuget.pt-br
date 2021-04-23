---
title: Referência do NuGet Find-Package PowerShell
description: Referência para Find-Package comando do PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 263835da64340a13737b32ab54ab057cb640a080
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901753"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (console do Gerenciador de pacotes no Visual Studio)

*Versão 3.0 +; Este tópico descreve o comando no [console do Gerenciador de pacotes](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows. Para o comando genérico Find-Package do PowerShell, consulte a [referência do PackageManagement do PowerShell](/powershell/module/packagemanagement).*

Obtém o conjunto de pacotes remotos com a ID ou palavras-chave especificadas da origem do pacote.

## <a name="syntax"></a>Sintaxe

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --- | --- |
| &lt;Palavras-chave de ID&gt; | Necessária Palavras-chave a serem usadas ao pesquisar a origem do pacote. Use-ExactMatch para retornar apenas os pacotes cuja ID de pacote corresponde às palavras-chave. Se nenhuma palavra-chave for fornecida, `Find-Package` o retornará uma lista dos 20 primeiros pacotes por downloads ou o número especificado por-primeiro. Observe que-ID é opcional e um não op. |
| Fonte | O caminho da URL ou da pasta para a origem do pacote a ser pesquisado. Os caminhos de pasta local podem ser absolutos ou relativos à pasta atual. Se omitido, `Find-Package` pesquisa a origem do pacote selecionada no momento. |
| AllVersions | Exibe todas as versões disponíveis de cada pacote, em vez de apenas a versão mais recente. |
| Primeiro | O número de pacotes a serem retornados do início da lista; o padrão é 20. |
| Ignorar | Omite os primeiros &lt; pacotes int &gt; da lista exibida.  |
| IncludePrerelease | Inclui pacotes de pré-lançamento nos resultados. |
| ExactMatch | Especificado para usar &lt; palavras-chave &gt; como uma ID de pacote que diferencia maiúsculas de minúsculas. |
| StartWith | Retorna os pacotes cuja ID de pacote começa com &lt; palavras-chave &gt; . |

Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.

## <a name="common-parameters"></a>Parâmetros comuns

`Find-Package` o oferece suporte aos seguintes [parâmetros comuns do PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

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