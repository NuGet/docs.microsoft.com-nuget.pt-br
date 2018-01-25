---
title: "Referência do pacote do NuGet Sync PowerShell | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referência de comando do PowerShell do pacote de sincronização no Console do Gerenciador de pacotes do NuGet no Visual Studio."
keywords: "Console do Gerenciador, comandos do Powershell do NuGet, referência do Powershell do NuGet, sincronização do pacote do pacote NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 02233cd0532fab2338e65e0d58b9afc3e2dab6af
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Pacote de sincronização (Console de Gerenciador de pacotes no Visual Studio)

*Versão 3.0 +; disponível apenas dentro de [NuGet Package Manager Console](Package-Manager-Console.md) no Visual Studio no Windows.*

Obtém a versão do pacote instalado a partir de especificado (ou padrão) do projeto e sincroniza a versão para o restante dos projetos na solução.

## <a name="syntax"></a>Sintaxe

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --- | --- |
| Id | (Obrigatório) O identificador do pacote para sincronizar. -Id switch é opcional. |
| IgnoreDependencies | Instale apenas esse pacote e não suas dependências. |
| ProjectName | O projeto a ser sincronizados com o pacote, o padrão para o projeto padrão. |
| Versão | A versão do pacote para sincronizar, padronizando para a versão atualmente instalada. |
| Origem | O caminho de URL ou pasta para a origem do pacote a ser pesquisado. Caminhos de pasta local podem ser absoluto ou relativo para a pasta atual. Se omitido, `Sync-Package` procura a origem de pacote selecionada atualmente. |
| IncludePrerelease | Inclui pacotes pré-lançados a sincronização. |
| FileConflictAction | A ação a ser tomada quando for solicitado a substituir ou ignorar os arquivos existentes, referenciados pelo projeto. Os valores possíveis são *substituir, ignorar, None, OverwriteAll*, e *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | A versão dos pacotes de dependência a usar, que pode ser um dos seguintes:<br/><ul><li>*Menor* (padrão): a versão mais antiga</li><li>*HighestPatch*: a versão com o patch mais baixo principal, secundária menor, mais alto</li><li>*HighestMinor*: a versão com o menor principais, mais alto patch menor, mais alto</li><li>*Mais alto* (padrão para o pacote de atualização sem parâmetros): a versão mais recente</li></ul>Você pode definir o valor padrão usando o [ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section) definindo no `Nuget.Config` arquivo. |
| WhatIf | Mostra o que aconteceria quando a execução do comando sem realmente executar a sincronização. |

Nenhum desses parâmetros aceitar caracteres curinga ou de entrada do pipeline.

## <a name="common-parameters"></a>Parâmetros comuns

`Sync-Package`suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, WarningAction, detalhado e WarningVariable.

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
