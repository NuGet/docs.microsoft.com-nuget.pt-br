---
title: Referência do PowerShell find-package do NuGet
description: Referência para o comando find-package do PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4bb6d090b97dd55fc1be0625855aab27a0d181c4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327383"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (Console do Gerenciador de Pacotes no Visual Studio)

*Versão 3.0 +; Este tópico descreve o comando no [console do Gerenciador de pacotes](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows. Para o comando genérico find-package do PowerShell, consulte a [referência do PackageManagement do PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*

Obtém o conjunto de pacotes remotos com a ID ou palavras-chave especificadas da origem do pacote.

## <a name="syntax"></a>Sintaxe

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --- | --- |
| Palavras &lt;-chave de ID&gt; | Necessária Palavras-chave a serem usadas ao pesquisar a origem do pacote. Use-ExactMatch para retornar apenas os pacotes cuja ID de pacote corresponde às palavras-chave. Se nenhuma palavra-chave for fornecida, `Find-Package` o retornará uma lista dos 20 primeiros pacotes por downloads ou o número especificado por-primeiro. Observe que-ID é opcional e um não op. |
| Origem | O caminho da URL ou da pasta para a origem do pacote a ser pesquisado. Os caminhos de pasta local podem ser absolutos ou relativos à pasta atual. Se omitido `Find-Package` , pesquisa a origem do pacote selecionada no momento. |
| AllVersions | Exibe todas as versões disponíveis de cada pacote, em vez de apenas a versão mais recente. |
| First | O número de pacotes a serem retornados do início da lista; o padrão é 20. |
| Skip | Omite os primeiros &lt;pacotes int&gt; da lista exibida.  |
| IncludePrerelease | Inclui pacotes de pré-lançamento nos resultados. |
| ExactMatch | Especificado para usar &lt;&gt; palavras-chave como uma ID de pacote que diferencia maiúsculas de minúsculas. |
| StartWith | Retorna os pacotes cuja ID de pacote &lt;começa com&gt;palavras-chave. |

Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.

## <a name="common-parameters"></a>Parâmetros comuns

`Find-Package`o oferece suporte aos seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

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
