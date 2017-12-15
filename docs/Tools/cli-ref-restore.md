---
title: "Comando de restauração do NuGet CLI | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 6ee41020-e548-4e61-b8cd-c82b77ac6af7
description: "Referência do comando de restauração de nuget.exe"
keywords: "NuGet restaure referência, restaure o comando de pacotes"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b435a3c2ffe08e3c2f8fc6a4dacb06cf674e4fb9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="restore-command-nuget-cli"></a>comando de restauração (NuGet CLI)

**Aplica-se a:** pacote consumo &bullet; **versões com suporte:** 2.7 +

NuGet 2.7 +: Baixa e instala todos os pacotes ausentes no `packages` pasta.

NuGet 3.3 + com projetos usando o `project.json`: gera um `project.lock.json` arquivo e um `<project>.nuget.props` de arquivo, se necessário. (Os dois arquivos podem ser omitidos do controle de origem).

NuGet 4.0 e posteriores com o projeto no qual pacote de referências são incluídas no arquivo de projeto diretamente: gera um `<project>.nuget.props` de arquivos, se necessário, o `obj` pasta. (O arquivo pode ser omitido do controle de origem).

Mac OSX e Linux com a CLI em Mono, restaurando os pacotes não há suporte para o formato PackageReference.

## <a name="usage"></a>Uso

```
nuget restore <projectPath> [options]
```

onde `<projectPath>` Especifica o local de uma solução, uma `packages.config` arquivo, ou um `project.json` arquivo. Consulte [comentários](#remarks) abaixo para obter detalhes de comportamentos.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ConfigFile | O arquivo de configuração do NuGet para aplicar. Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado. |
| DirectDownload | *(4.0 +)*  Baixa pacotes diretamente sem populá caches com binários ou metadados. |
| DisableParallelProcessing | Desabilita a restauração de vários pacotes em paralelo. |
| FallbackSource | *(3.2 +)*  Uma lista de fontes de pacote para usar como fallbacks caso o pacote não foi encontrado no primário ou a fonte padrão. |
| ForceEnglishOutput | *(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Ajuda | Exibe informações de ajuda para o comando. |
| MSBuildPath | *(4.0 +)*  Especifica o caminho do MSBuild para usar com o comando tendo precedência sobre `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Especifica a versão do MSBuild a ser usado com este comando. Valores com suporte são 4, 12, 14, 15. Por padrão que o MSBuild em seu caminho é separado, caso contrário, o padrão é a versão mais recente instalada do MSBuild. |
| NoCache | Impede que o NuGet usando pacotes de caches de computador local. |
| Não interativo | Suprime avisos para a entrada do usuário ou confirmações. |
| OutputDirectory | Especifica a pasta na qual os pacotes são instalados. Se nenhuma pasta for especificada, a pasta atual será usada. |
| PackageSaveMode | Especifica os tipos de arquivos para salvar após a instalação do pacote: um dos `nuspec`, `nupkg`, ou `nuspec;nupkg`. |
| PackagesDirectory | Mesmo que `OutputDirectory`. |
| Project2ProjectTimeOut | Tempo limite em segundos para resolver referências de projeto ao projeto. |
| Recursiva | *(4.0 +)*  Restaura todos os projetos de referências para os projetos UWP e .NET Core. Não se aplicam a projetos usando `packages.config`. |
| RequireConsent | Verifica se a restauração de pacotes é habilitado antes de baixar e instalar os pacotes. Para obter detalhes, consulte [restauração do pacote](../consume-packages/package-restore.md). |
| SolutionDirectory | Especifica a pasta de solução. Não é válido ao restaurar pacotes para uma solução. |
| Origem | Especifica a lista de fontes de pacote (como URLs) para usar para a restauração. Se omitido, o comando usa as fontes fornecidas nos arquivos de configuração, consulte [NuGet Configurando comportamento](../Consume-Packages/Configuring-NuGet-Behavior.md). |
| Detalhamento |> especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas (2.5 +)*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="remarks"></a>Comentários

O comando restore executa as seguintes etapas:

1. Determine o modo de operação do comando restore.
    tipo de arquivo projectPath | Comportamento
    | --- | --- |
    Solução (pasta) | NuGet procura um `.sln` de arquivo e usa esse encontrado; caso contrário, retorna um erro. `(SolutionDir)\.nuget`é usado como a pasta inicial.
    `.sln`arquivo | Restaurar os pacotes identificados pela solução; gera um erro se `-SolutionDirectory` é usado. `$(SolutionDir)\.nuget`é usado como a pasta inicial.
    `packages.config`, `project.json`, ou arquivo de projeto | Restaure os pacotes listados no arquivo, resolvendo e instalando dependências.
    Outro tipo de arquivo | Arquivo é considerado um `.sln` arquivo acima; se não for uma solução, o NuGet fornece um erro.
    (projectPath não especificado) | -NuGet procura por arquivos de solução na pasta atual. Se for encontrado um único arquivo, que é usado para restaurar os pacotes; Se várias soluções forem encontradas, o NuGet apresentará um erro.
    |-Se não houver nenhum arquivo de solução, o NuGet procura um `packages.config` ou `project.json` e a usa para restaurar os pacotes.
    |-Se nenhum arquivo de solução, `packages.config`, ou `project.json` for encontrado, o NuGet apresentará um erro.

1. Determine a pasta de pacotes usando a seguinte ordem de prioridade (NuGet apresentará um erro se nenhuma dessas pastas são encontradas):

    - O `%userprofile%\.nuget\packages` valor em `project.json`.
    - A pasta especificada com `-PackagesDirectory`.
    - O `repositoryPath` vale em`Nuget.Config`
    - A pasta especificada com`-SolutionDirectory`
    - `$(SolutionDir)\packages`

1. Ao restaurar pacotes para uma solução, o NuGet faz o seguinte:
    - Carrega o arquivo de solução.
    - Restaura os pacotes de nível de solução listados na `$(SolutionDir)\.nuget\packages.config` para o `packages` pasta.
    - Restaurar os pacotes listados na `$(ProjectDir)\packages.config` para o `packages` pasta. Para cada pacote especificado, restaurar o pacote em paralelo, a menos que `-DisableParallelProcessing` for especificado.

## <a name="examples"></a>Exemplos

```
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
