---
title: Sincronização do NuGet – referência do PowerShell do pacote
description: Referência para o comando sync-Package do PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 12a3d5f32056539a75da9e17b15d67e72a8a42c2
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384897"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (Console do Gerenciador de Pacotes no Visual Studio)

*Versão 3.0 +; disponível somente dentro do [console do Gerenciador de pacotes](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows.*

Obtém a versão do pacote instalado do projeto especificado (ou padrão) e sincroniza a versão para o restante dos projetos na solução.

## <a name="syntax"></a>Sintaxe

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --- | --- |
| Id | Necessária O identificador do pacote a ser sincronizado. A opção-ID em si é opcional. |
| IgnoreDependencies | Instale somente este pacote e não suas dependências. |
| ProjectName | O projeto do qual sincronizar o pacote, padronizando para o projeto padrão. |
| Versão do | A versão do pacote a ser sincronizado, padronizando para a versão instalada no momento. |
| Source | O caminho da URL ou da pasta para a origem do pacote a ser pesquisado. Os caminhos de pasta local podem ser absolutos ou relativos à pasta atual. Se for omitido, `Sync-Package` pesquisará a origem do pacote selecionada no momento. |
| IncludePrerelease | Inclui pacotes de pré-lançamento na sincronização. |
| FileConflictAction | A ação a ser tomada quando for solicitado a substituir ou ignorar os arquivos existentes referenciados pelo projeto. Os valores possíveis são *overwrite, ignore, None, OverwriteAll*e *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | A versão dos pacotes de dependência a serem usados, que pode ser uma das seguintes:<br/><ul><li>*Mais baixo* (padrão): a versão mais baixa</li><li>*HighestPatch*: a versão com o menor principal, menor o mais baixo, patch mais alto</li><li>*HighestMinor*: a versão com o menor principal, o mais baixo, o patch mais alto</li><li>*Mais alto* (padrão para update-package sem parâmetros): a versão mais recente</li></ul>Você pode definir o valor padrão usando a configuração de [`dependencyVersion`](../nuget-config-file.md#config-section) no arquivo de `Nuget.Config`. |
| WhatIf | Mostra o que aconteceria ao executar o comando sem realmente executar a sincronização. |

Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.

## <a name="common-parameters"></a>Parâmetros comuns

o `Sync-Package` dá suporte aos seguintes [parâmetros comuns do PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Exemplos

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```
