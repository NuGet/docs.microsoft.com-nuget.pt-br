---
title: Referência do NuGet Install-Package PowerShell
description: Referência para Install-Package comando do PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: ad551b8701cfc2061f7721fb050ed9b5a4fede32
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901688"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (console do Gerenciador de pacotes no Visual Studio)

*Este tópico descreve o comando no [console do Gerenciador de pacotes](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows. Para o comando genérico Install-Package do PowerShell, consulte a [referência do PackageManagement do PowerShell](/powershell/module/packagemanagement).*

Instala um pacote e suas dependências em um projeto.

## <a name="syntax"></a>Sintaxe

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

No NuGet 2.8 +, `Install-Package` o pode fazer o downgrade de um pacote existente em seu projeto. Por exemplo, se você tiver o Microsoft. AspNet. MVC 5.1.0-RC1 instalado, o comando a seguir o desfazeria para 5.0.0:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --- | --- |
| ID | Necessária O identificador do pacote a ser instalado. (*3.0 +*) O identificador pode ser um caminho ou uma URL de um `packages.config` arquivo ou `.nupkg` arquivo. A opção-ID em si é opcional. |
| IgnoreDependencies | Instale somente este pacote e não suas dependências. |
| ProjectName | O projeto no qual instalar o pacote, padronizando para o projeto padrão. |
| Fonte | O caminho da URL ou da pasta para a origem do pacote a ser pesquisado. Os caminhos de pasta local podem ser absolutos ou relativos à pasta atual. Se omitido, `Install-Package` pesquisa a origem do pacote selecionada no momento. |
| Versão | A versão do pacote a ser instalada, padronizando para a versão mais recente. |
| IncludePrerelease | Considera os pacotes de pré-lançamento para a instalação. Se omitido, apenas os pacotes estáveis são considerados. |
| Fileconflitoaction | A ação a ser tomada quando for solicitado a substituir ou ignorar os arquivos existentes referenciados pelo projeto. Os valores possíveis são *overwrite, ignore, None, OverwriteAll* e *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | A versão dos pacotes de dependência a serem usados, que pode ser uma das seguintes:<br/><ul><li>*Mais baixo* (padrão): a versão mais baixa</li><li>*HighestPatch*: a versão com o menor principal, menor o mais baixo, patch mais alto</li><li>*HighestMinor*: a versão com o menor principal, o mais baixo, o patch mais alto</li><li>*Mais alto* (padrão para Update-Package sem parâmetros): a versão mais recente</li></ul>Você pode definir o valor padrão usando a [`dependencyVersion`](../nuget-config-file.md#config-section) configuração no `Nuget.Config` arquivo. |
| WhatIf | Mostra o que aconteceria ao executar o comando sem realmente executar a instalação. |

Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.

## <a name="common-parameters"></a>Parâmetros comuns

`Install-Package` o oferece suporte aos seguintes [parâmetros comuns do PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Exemplos

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
# Note: the URL must end with "packages.config"
Install-Package https://raw.githubusercontent.com/linked-data-dotnet/json-ld.net/master/.nuget/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-Package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
# Note: the URL must end with ".nupkg"
Install-Package https://globalcdn.nuget.org/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```