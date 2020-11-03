---
title: Referência do NuGet Get-Package PowerShell
description: Referência para Get-Package comando do PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 1576e3f20eba1ecdd099b1e7c23aef6b1a1a0a4f
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237225"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (console do Gerenciador de pacotes no Visual Studio)

*Este tópico descreve o comando no [console do Gerenciador de pacotes](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows. Para o comando genérico Get-Package do PowerShell, consulte a [referência do PackageManagement do PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*

Recupera a lista de pacotes instalados no repositório local, lista os pacotes disponíveis de uma origem de pacote quando usados com a opção-ListAvailable ou lista as atualizações disponíveis quando usadas com a opção-Update.

## <a name="syntax"></a>Syntax

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

Sem parâmetros, `Get-Package` exibe a lista de pacotes instalados no projeto padrão.

## <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --- | --- |
| Fonte | A URL ou o caminho da pasta do pacote. Os caminhos de pasta local podem ser absolutos ou relativos à pasta atual. Se omitido, `Get-Package` pesquisa a origem do pacote selecionada no momento. Quando usado com-ListAvailable, o padrão é nuget.org. |
| ListAvailable | Lista os pacotes disponíveis de uma origem de pacote, padronizando para nuget.org. Mostra um padrão de pacotes 50 a menos que-PageSize e/ou-First sejam especificados. |
| Atualizações | Lista os pacotes que têm uma atualização disponível na origem do pacote. |
| ProjectName | O projeto do qual obter os pacotes instalados. Se omitido, retorna projetos instalados para a solução inteira. |
| Filtrar | Uma cadeia de caracteres de filtro usada para restringir a lista de pacotes aplicando-o à ID, descrição e marcas do pacote. |
| Primeiro | O número de pacotes a serem retornados do início da lista. Se não for especificado, o padrão será 50. |
| Ignorar | Omite os primeiros &lt; pacotes int &gt; da lista exibida.  |
| AllVersions | Exibe todas as versões disponíveis de cada pacote, em vez de apenas a versão mais recente. |
| IncludePrerelease | Inclui pacotes de pré-lançamento nos resultados. |
| PageSize | *(3.0 +)* Quando usado com-ListAvailable (obrigatório), o número de pacotes a serem listados antes de dar um aviso para continuar. |

Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.

## <a name="common-parameters"></a>Parâmetros comuns

`Get-Package` o oferece suporte aos seguintes [parâmetros comuns do PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Exemplos

```ps
# Lists the packages installed in the current solution
Get-Package

# Lists the packages installed in a project
Get-Package -ProjectName MyProject

# Lists packages available in the current package source
Get-Package -ListAvailable

# Lists 30 packages at a time from the current source, and prompts to continue if more are available
Get-Package -ListAvailable -PageSize 30

# Lists packages with the Ninject keyword in the current source, up to 50
Get-Package -ListAvailable -Filter Ninject

# List all versions of packages matching the filter "jquery"
Get-Package -ListAvailable -Filter jquery -AllVersions

# Lists packages installed in the solution that have available updates
Get-Package -Updates

# Lists packages installed in a specific project that have available updates
Get-Package -Updates -ProjectName MyProject
```