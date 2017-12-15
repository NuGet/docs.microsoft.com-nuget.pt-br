---
title: Comando update do NuGet CLI | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 61fde945-6983-46a5-8636-da0fada4e641
description: "Referência para o comando de atualização de nuget.exe"
keywords: "referência de atualização do NuGet, comando de pacote de atualização"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 654144e93a99a4a4f8d79c0db5660cfb7c6c308e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="update-command-nuget-cli"></a>comando de atualização (NuGet CLI)

**Aplica-se a:** pacote consumo &bullet; **versões com suporte:** todos

Atualiza todos os pacotes em um projeto (usando `packages.config`) para suas versões mais recentes disponíveis. É recomendável executar ['restore'](#restore) antes de executar o `update`. (Para atualizar um pacote individual, use [ `nuget install` ](cli-ref-install.md) sem especificar um número de versão, em que o NuGet caso instala a versão mais recente.)

Observação: `update` não funciona com a CLI em execução em Mono (Mac OSX ou Linux). O comando também funciona com projetos usando `project.json` ou PackageReference formatos de gerenciamento.

O `update` comando também atualiza as referências de assembly no arquivo de projeto, desde que as referências já existe. Se um pacote atualizado tem um assembly adicionado, uma nova referência é *não* adicionado. Novas dependências do pacote também não têm suas referências de assembly adicionadas. Para incluir essas operações como parte de uma atualização, atualize o pacote no Visual Studio usando a UI Package Manager ou o Package Manager Console.

Este comando também pode ser usado para atualizar o nuget.exe si mesmo usando o *-self* sinalizador.

## <a name="usage"></a>Uso

```
nuget update <configPath> [options]
```

onde `<configPath>` identifica em uma `packages.config` ou arquivo de solução que lista as dependências do projeto.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ConfigFile | *(2.5 +)*  NuGet o arquivo de configuração para aplicar. Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado. |
| FileConflictAction | *(2.5 +)*  Especifica a ação a ser tomada quando for solicitado a substituir ou ignorar os arquivos existentes, referenciados pelo projeto. Os valores são *substituir, ignorar, nenhum*. |
| ForceEnglishOutput | *(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Ajuda | Exibe informações de ajuda para o comando. |
| Id | Especifica uma lista de IDs para a atualização do pacote. |
| MSBuildPath | *(4.0 +)*  Especifica o caminho do MSBuild para usar com o comando tendo precedência sobre `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Especifica a versão do MSBuild a ser usado com este comando. Valores com suporte são 4, 12, 14, 15. Por padrão que o MSBuild em seu caminho é separado, caso contrário, o padrão é a versão mais recente instalada do MSBuild. |
| Não interativo | Suprime avisos para a entrada do usuário ou confirmações. |
| Versão de pré-lançamento | Permite a atualização para as versões de pré-lançamento. Este sinalizador não é necessário ao atualizar os pacotes de pré-lançamento que já estão instalados. |
| Caminho do repositório | Especifica a pasta local onde os pacotes estão instalados. |
| Safe | Especifica que apenas atualizações com a versão mais recente disponível dentro da mesma versão principal e secundária, o pacote instalado será instalado. |
| Self | *(1.4 +)*  Atualiza nuget.exe para a versão mais recente; todos os outros argumentos são ignorados. |
| Origem | Especifica a lista de fontes de pacote (como URLs) para usar as atualizações. Se omitido, o comando usa as fontes fornecidas nos arquivos de configuração, consulte [NuGet Configurando comportamento](../Consume-Packages/Configuring-NuGet-Behavior.md). |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas (2.5 +)*. |
| Versão | Quando usado com uma ID de pacote, especifica a versão do pacote para atualizar. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
