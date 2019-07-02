---
title: Referência de pacote de atualização do NuGet do PowerShell
description: Referência de comando do PowerShell do pacote de atualização no Console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a5b5a11ee11d9e2cf6a90d56ac63b1f7bad750ea
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496485"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Update-Package (Console do Gerenciador de Pacotes no Visual Studio)

*Disponível somente dentro de [NuGet Package Manager Console](package-manager-console.md) no Visual Studio no Windows.*

Atualiza um pacote e suas dependências ou todos os pacotes em um projeto, para uma versão mais recente.

## <a name="syntax"></a>Sintaxe

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

No NuGet 2.8 ou superior, `Update-Package` pode ser usado para fazer o downgrade de um pacote existente em seu projeto. Por exemplo, se você tiver 5.1.0-rc1 ASPNET instalado, o comando a seguir seria fazer o downgrade para 5.0.0:

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parâmetros

|  Parâmetro | Descrição |
| --- | --- |
| Id | O identificador do pacote a atualizar. Se omitido, todos os pacotes de atualizações. -Id do comutador em si é opcional. |
| IgnoreDependencies | Ignora atualizando dependências do pacote. |
| ProjectName | O nome do projeto que contém os pacotes para atualizar, padronizando para todos os projetos. |
| Versão | A versão a ser usado para a atualização, padronizando para a versão mais recente. No NuGet 3.0 ou superior, o valor de versão deve ser um dos *menor, mais alto, HighestMinor*, ou *HighestPatch* (equivalente ao - Safe). |
| Safe | Restringe atualizações para versões somente com a mesma versão principal e secundária do pacote atualmente instalado. |
| Origem | O caminho de URL ou pasta para a origem do pacote a pesquisar. Caminhos de pasta local podem ser absoluto ou relativo à pasta atual. Se omitido, `Update-Package` procura a origem do pacote selecionado no momento. |
| IncludePrerelease | Inclui pacotes de pré-lançamento de atualizações. |
| Reinstalar | Pacotes de Resintalls usando suas versões atualmente instaladas. Confira [Reinstalando e atualizando pacotes](../consume-packages/reinstalling-and-updating-packages.md). |
| FileConflictAction | A ação a ser tomada quando for solicitado a substituir ou ignorar os arquivos existentes, referenciados pelo projeto. Os valores possíveis são *substituir, ignorar, None, OverwriteAll*, e *IgnoreAll* (3.0 ou superior). |
| DependencyVersion | A versão dos pacotes de dependência a ser usado, que pode ser um dos seguintes:<br/><ul><li>*Mais baixo* (padrão): a versão mais antiga</li><li>*HighestPatch*: a versão com o patch mais baixa principal, secundária menor, mais alto</li><li>*HighestMinor*: a versão com menor principais, o patch mais alto de pequena, mais alto</li><li>*Mais alto* (padrão para o pacote de atualização sem parâmetros): a versão mais recente</li></ul>Você pode definir o valor padrão usando o [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) definindo no `Nuget.Config` arquivo. |
| ToHighestPatch | equivalente ao - Safe. |
| ToHighestMinor | Restringe atualizações para apenas as versões com a mesma versão principal que o pacote atualmente instalado. |
| WhatIf | Mostra o que aconteceria ao executar o comando sem realmente executar a atualização. |

Nenhum desses parâmetros aceitam caracteres curinga ou de entrada do pipeline.

### <a name="common-parameters"></a>Parâmetros comuns

`Update-Package` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detalhado, WarningAction e WarningVariable.

### <a name="examples"></a>Exemplos

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```
