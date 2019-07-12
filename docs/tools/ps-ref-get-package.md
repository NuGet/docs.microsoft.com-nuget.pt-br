---
title: Referência do PowerShell Get-pacote do NuGet
description: Referência de comando do PowerShell Get-Package no Console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d0d25cb6e21f6d0d42389e08340b6f1e1baf8a64
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842511"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (Console do Gerenciador de Pacotes no Visual Studio)

*Este tópico descreve o comando dentro de [Package Manager Console](package-manager-console.md) no Visual Studio no Windows. Para o comando do PowerShell Get-Package genérico, consulte o [referência do PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Recupera a lista de pacotes instalados no repositório local, lista de pacotes disponíveis a partir de uma origem de pacote quando usado com a opção - ListAvailable ou lista de atualizações disponíveis quando usado com a opção - opção de atualização.

## <a name="syntax"></a>Sintaxe

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

Sem parâmetros, `Get-Package` exibe a lista de pacotes instalados no projeto padrão.

## <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --- | --- |
| Origem | O caminho de URL ou pasta para o pacote. Caminhos de pasta local podem ser absoluto ou relativo à pasta atual. Se omitido, `Get-Package` procura a origem do pacote selecionado no momento. Quando usado com - ListAvailable, assume como padrão para o nuget.org. |
| ListAvailable | Lista os pacotes disponíveis a partir de uma origem de pacote, padronizando para nuget.org. Mostra um padrão de 50 pacotes, a menos que - PageSize e/ou - primeiro é especificado. |
| Atualizações | Lista os pacotes que têm uma atualização disponível da origem do pacote. |
| ProjectName | O projeto do qual obter os pacotes instalados. Se omitido, retorna instalados projetos da solução inteira. |
| Filtro | Uma cadeia de caracteres de filtro usada para restringir a lista de pacotes aplicando-o para a ID do pacote, descrição e marcas. |
| First | O número de pacotes para retornar do início da lista. Se não for especificado, padrão é 50. |
| Skip | Omite o primeiro &lt;int&gt; pacotes na lista exibida.  |
| AllVersions | Exibe todas as versões disponíveis de cada pacote em vez de apenas a versão mais recente. |
| IncludePrerelease | Inclui pacotes pré-lançados nos resultados. |
| PageSize | *(3.0 ou superior)*  Quando usado com - ListAvailable (obrigatório), o número de pacotes para a lista antes de entregar um prompt para continuar. |

Nenhum desses parâmetros aceitam caracteres curinga ou de entrada do pipeline.

## <a name="common-parameters"></a>Parâmetros comuns

`Get-Package` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detalhado, WarningAction e WarningVariable.

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
