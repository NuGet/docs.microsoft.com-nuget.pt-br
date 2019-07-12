---
title: Referência do PowerShell NuGet Install-Package
description: Referência de comando do PowerShell de Install-Package no Console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 755c87bbc68d3b688c81e16edbc1faabdc9e0520
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842495"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (Console do Gerenciador de Pacotes no Visual Studio)

*Este tópico descreve o comando dentro de [Package Manager Console](package-manager-console.md) no Visual Studio no Windows. Para o comando do PowerShell Install-Package genérico, consulte o [referência do PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Instala um pacote e suas dependências em um projeto.

## <a name="syntax"></a>Sintaxe

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

No NuGet 2.8 ou superior, `Install-Package` pode fazer downgrade de um pacote existente em seu projeto. Por exemplo, se você tiver 5.1.0-rc1 ASPNET instalado, o comando a seguir seria fazer o downgrade para 5.0.0:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --- | --- |
| Id | (Obrigatório) O identificador do pacote a instalar. (*3.0 ou superior*) o identificador pode ser um caminho ou URL de um `packages.config` arquivo ou um `.nupkg` arquivo. -Id do comutador em si é opcional. |
| IgnoreDependencies | Instale apenas esse pacote e não as suas dependências. |
| ProjectName | O projeto no qual instalar o pacote, padronizando para o projeto padrão. |
| Origem | O caminho de URL ou pasta para a origem do pacote a pesquisar. Caminhos de pasta local podem ser absoluto ou relativo à pasta atual. Se omitido, `Install-Package` procura a origem do pacote selecionado no momento. |
| Versão | A versão do pacote a instalar, padronizando para a versão mais recente. |
| IncludePrerelease | Considera os pacotes de pré-lançamento para a instalação. Se omitido, apenas os pacotes estáveis são considerados. |
| FileConflictAction | A ação a ser tomada quando for solicitado a substituir ou ignorar os arquivos existentes, referenciados pelo projeto. Os valores possíveis são *substituir, ignorar, None, OverwriteAll*, e *(3.0 ou superior)* *IgnoreAll*. |
| DependencyVersion | A versão dos pacotes de dependência a ser usado, que pode ser um dos seguintes:<br/><ul><li>*Mais baixo* (padrão): a versão mais antiga</li><li>*HighestPatch*: a versão com o patch mais baixa principal, secundária menor, mais alto</li><li>*HighestMinor*: a versão com menor principais, o patch mais alto de pequena, mais alto</li><li>*Mais alto* (padrão para o pacote de atualização sem parâmetros): a versão mais recente</li></ul>Você pode definir o valor padrão usando o [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) definindo no `Nuget.Config` arquivo. |
| WhatIf | Mostra o que aconteceria ao executar o comando sem realmente executar a instalação. |

Nenhum desses parâmetros aceitam caracteres curinga ou de entrada do pipeline.

## <a name="common-parameters"></a>Parâmetros comuns

`Install-Package` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detalhado, WarningAction e WarningVariable.

## <a name="examples"></a>Exemplos

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
