---
title: Referência do NuGet Update-Package PowerShell
description: Referência para Update-Package comando do PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: af918d11e8f976be962d52084c5eda4d53e382c6
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238030"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Update-Package (console do Gerenciador de pacotes no Visual Studio)

*Disponível somente no [console do Gerenciador de pacotes NuGet](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows.*

Atualiza um pacote e suas dependências, ou todos os pacotes em um projeto, para uma versão mais recente.

## <a name="syntax"></a>Syntax

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

No NuGet 2.8 +, `Update-Package` o pode ser usado para fazer downgrade de um pacote existente em seu projeto. Por exemplo, se você tiver o Microsoft. AspNet. MVC 5.1.0-RC1 instalado, o comando a seguir o desfazeria para 5.0.0:

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parâmetros

|  Parâmetro | Descrição |
| --- | --- |
| ID | O identificador do pacote a ser atualizado. Se omitido, atualiza todos os pacotes. A opção-ID em si é opcional. |
| IgnoreDependencies | Ignora a atualização das dependências do pacote. |
| ProjectName | O nome do projeto que contém os pacotes a serem atualizados, padronizando para todos os projetos. |
| Versão | A versão a ser usada para a atualização, padronizando para a versão mais recente. No NuGet 3.0 +, o valor da versão deve ser um dos *mais baixo, mais alto, HighestMinor* ou *HighestPatch* (equivalente a seguro). |
| Safe | Restringe atualizações para apenas versões com a mesma versão principal e secundária do pacote atualmente instalado. |
| Fonte | O caminho da URL ou da pasta para a origem do pacote a ser pesquisado. Os caminhos de pasta local podem ser absolutos ou relativos à pasta atual. Se omitido, `Update-Package` pesquisa a origem do pacote selecionada no momento. |
| IncludePrerelease | Inclui pacotes de pré-lançamento para atualizações. |
| Reinstalar | Pacotes Resintalls usando suas versões atualmente instaladas. Consulte [reinstalando e atualizando pacotes](../../consume-packages/reinstalling-and-updating-packages.md). |
| Fileconflitoaction | A ação a ser tomada quando for solicitado a substituir ou ignorar os arquivos existentes referenciados pelo projeto. Os valores possíveis são *overwrite, ignore, None, OverwriteAll* e *IgnoreAll* (3.0 +). |
| DependencyVersion | A versão dos pacotes de dependência a serem usados, que pode ser uma das seguintes:<br/><ul><li>*Mais baixo* (padrão): a versão mais baixa</li><li>*HighestPatch* : a versão com o menor principal, menor o mais baixo, patch mais alto</li><li>*HighestMinor* : a versão com o menor principal, o mais baixo, o patch mais alto</li><li>*Mais alto* (padrão para Update-Package sem parâmetros): a versão mais recente</li></ul>Você pode definir o valor padrão usando a [`dependencyVersion`](../nuget-config-file.md#config-section) configuração no `Nuget.Config` arquivo. |
| ToHighestPatch | equivalente a-Safe. |
| ToHighestMinor | Restringe atualizações para apenas versões com a mesma versão principal do pacote atualmente instalado. |
| WhatIf | Mostra o que aconteceria ao executar o comando sem realmente executar a atualização. |

Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.

### <a name="common-parameters"></a>Parâmetros comuns

`Update-Package` o oferece suporte aos seguintes [parâmetros comuns do PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

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
Update-Package Elmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package Elmah –reinstall -ignoreDependencies
```
