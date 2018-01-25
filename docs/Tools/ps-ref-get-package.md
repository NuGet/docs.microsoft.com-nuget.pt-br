---
title: "Referência do PowerShell Get-pacote de NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referência de comando do PowerShell Get-Package no Console do Gerenciador de pacotes do NuGet no Visual Studio."
keywords: "Pacote de NuGet manager console, comandos do Powershell do NuGet, referência do Powershell do NuGet, Get-Package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c38e0da2e98d2e5bf5b4fc165462e9abcfdd73c0
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (Console de Gerenciador de pacotes no Visual Studio)

*Este tópico descreve o comando dentro de [NuGet Package Manager Console](Package-Manager-Console.md) no Visual Studio no Windows. Para o comando do PowerShell Get-Package genérico, consulte o [referência do PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Recupera a lista de pacotes instalados no repositório local, lista de pacotes disponíveis a partir de uma origem de pacote quando usado com a opção - ListAvailable ou lista de atualizações disponíveis quando usado com a opção-Update.

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
| Origem | O caminho de URL ou pasta para o pacote. Caminhos de pasta local podem ser absoluto ou relativo para a pasta atual. Se omitido, `Get-Package` procura a origem de pacote selecionada atualmente. Quando usado com - ListAvailable, o padrão é nuget.org. |
| ListAvailable | Lista de pacotes disponíveis a partir de uma origem do pacote, padronizando para nuget.org. Mostra um padrão de 50 pacotes, a menos que - PageSize e/ou - primeiro é especificado. |
| Atualizações | Lista os pacotes que tenham uma atualização disponível da origem do pacote. |
| ProjectName | O projeto do qual obter os pacotes instalados. Se omitido, retorna instalados projetos da solução inteira. |
| Filtro | Uma cadeia de caracteres de filtro usada para restringir a lista de pacotes por aplicá-la para a ID do pacote, descrição e marcas. |
| Primeiro | O número de pacotes a serem retornados desde o início da lista. Se não for especificado, padrão é 50. |
| Skip | Omite o primeiro &lt;int&gt; pacotes na lista exibida.  |
| Todasas versões | Exibe todas as versões disponíveis de cada pacote em vez de apenas a versão mais recente. |
| IncludePrerelease | Inclui pacotes pré-lançados nos resultados. |
| PageSize | *(3.0 +)*  Quando usado com - ListAvailable (obrigatório), o número de pacotes para a lista antes de fazer uma solicitação para continuar. |

Nenhum desses parâmetros aceitar caracteres curinga ou de entrada do pipeline.

## <a name="common-parameters"></a>Parâmetros comuns

`Get-Package`suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, WarningAction, detalhado e WarningVariable.

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
