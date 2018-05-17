---
title: Comando de atualização de CLI do NuGet
description: Referência para o comando de atualização de nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: e6964d92436ce1bac9e6af85f6dae75fcf40378d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="update-command-nuget-cli"></a>Commando update (NuGet CLI)

**Aplica-se a:** pacote consumo &bullet; **versões com suporte:** todos

Atualiza todos os pacotes em um projeto (usando `packages.config`) para suas versões mais recentes disponíveis. É recomendável executar ['restore'](cli-ref-restore.md) antes de executar o `update`. (Para atualizar um pacote individual, use [ `nuget install` ](cli-ref-install.md) sem especificar um número de versão, em que o NuGet caso instala a versão mais recente.)

Observação: `update` não funciona com a CLI em execução em Mono (Mac OSX ou Linux) ou ao usar o formato de PackageReference.

O `update` comando também atualiza as referências de assembly no arquivo de projeto, desde que as referências já existe. Se um pacote atualizado tem um assembly adicionado, uma nova referência é *não* adicionado. Novas dependências do pacote também não têm suas referências de assembly adicionadas. Para incluir essas operações como parte de uma atualização, atualize o pacote no Visual Studio usando a UI Package Manager ou o Package Manager Console.

Este comando também pode ser usado para atualizar o nuget.exe si mesmo usando o *-self* sinalizador.

## <a name="usage"></a>Uso

```cli
nuget update <configPath> [options]
```

onde `<configPath>` identifica em uma `packages.config` ou arquivo de solução que lista as dependências do projeto.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ConfigFile | O arquivo de configuração do NuGet para aplicar. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.|
| FileConflictAction | Especifica a ação a ser tomada quando for solicitado a substituir ou ignorar os arquivos existentes, referenciados pelo projeto. Os valores são *substituir, ignorar, nenhum*. |
| ForceEnglishOutput | *(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Ajuda | Exibe informações de ajuda para o comando. |
| Id | Especifica uma lista de IDs para a atualização do pacote. |
| MSBuildPath | *(4.0 +)*  Especifica o caminho do MSBuild para usar com o comando tendo precedência sobre `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Especifica a versão do MSBuild a ser usado com este comando. Valores com suporte são 4, 12, 14, 15. Por padrão que o MSBuild em seu caminho é separado, caso contrário, o padrão é a versão mais recente instalada do MSBuild. |
| NonInteractive | Suprime avisos para a entrada do usuário ou confirmações. |
| Versão de pré-lançamento | Permite a atualização para as versões de pré-lançamento. Este sinalizador não é necessário ao atualizar os pacotes de pré-lançamento que já estão instalados. |
| Caminho do repositório | Especifica a pasta local onde os pacotes estão instalados. |
| Safe | Especifica que apenas atualizações com a versão mais recente disponível dentro da mesma versão principal e secundária, o pacote instalado será instalado. |
| Self | Atualiza o nuget.exe para a versão mais recente; todos os outros argumentos são ignorados. |
| Origem | Especifica a lista de fontes de pacote (como URLs) para usar as atualizações. Se omitido, o comando usa as fontes fornecidas nos arquivos de configuração, consulte [NuGet Configurando comportamento](../consume-packages/configuring-nuget-behavior.md). |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |
| Versão | Quando usado com uma ID de pacote, especifica a versão do pacote para atualizar. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
