---
title: Referência do PowerShell de sincronização-pacote do NuGet
description: Referência de comando do PowerShell de sincronização de pacote no Console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8119664b1bafe9238b12b1819cc46dc1ee7bdd00
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547988"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (Console do Gerenciador de Pacotes no Visual Studio)

*Versão 3.0 ou superior; disponível somente dentro de [NuGet Package Manager Console](package-manager-console.md) no Visual Studio no Windows.*

Obtém a versão do pacote instalado do especificado (ou padrão) do projeto e sincroniza a versão para o restante dos projetos na solução.

## <a name="syntax"></a>Sintaxe

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --- | --- |
| Id | (Obrigatório) O identificador do pacote para sincronizar. -Id do comutador em si é opcional. |
| IgnoreDependencies | Instale apenas esse pacote e não as suas dependências. |
| ProjectName | O projeto para sincronizar o pacote, padronizando para o projeto padrão. |
| Versão | A versão do pacote para sincronizar, padronizando para a versão atualmente instalada. |
| Origem | O caminho de URL ou pasta para a origem do pacote a pesquisar. Caminhos de pasta local podem ser absoluto ou relativo à pasta atual. Se omitido, `Sync-Package` procura a origem do pacote selecionado no momento. |
| IncludePrerelease | Inclui pacotes de pré-lançamento na sincronização. |
| FileConflictAction | A ação a ser tomada quando for solicitado a substituir ou ignorar os arquivos existentes, referenciados pelo projeto. Os valores possíveis são *substituir, ignorar, None, OverwriteAll*, e *(3.0 ou superior)* *IgnoreAll*. |
| DependencyVersion | A versão dos pacotes de dependência a ser usado, que pode ser um dos seguintes:<br/><ul><li>*Mais baixo* (padrão): a versão mais antiga</li><li>*HighestPatch*: a versão com o patch mais baixa principal, secundária menor, mais alto</li><li>*HighestMinor*: a versão com menor principais, o patch mais alto de pequena, mais alto</li><li>*Mais alto* (padrão para o pacote de atualização sem parâmetros): a versão mais recente</li></ul>Você pode definir o valor padrão usando o [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) definindo no `Nuget.Config` arquivo. |
| WhatIf | Mostra o que aconteceria ao executar o comando sem realmente executar a sincronização. |

Nenhum desses parâmetros aceitam caracteres curinga ou de entrada do pipeline.

## <a name="common-parameters"></a>Parâmetros comuns

`Sync-Package` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detalhado, WarningAction e WarningVariable.

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
