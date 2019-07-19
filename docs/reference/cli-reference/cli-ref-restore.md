---
title: Comando de restauração da CLI do NuGet
description: Referência para o comando de restauração NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 82113d460f7f5ff467b0a0552cc49283de95de25
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327633"
---
# <a name="restore-command-nuget-cli"></a>comando Restore (NuGet CLI)

**Aplica-se a:** &bullet; **versões com suporte** de consumo de pacote: 2.7+

Baixa e instala todos os pacotes ausentes `packages` da pasta. Quando usado com o NuGet 4.0 + e o formato PackageReference, o `<project>.nuget.props` gera um arquivo, se necessário, `obj` na pasta. (O arquivo pode ser omitido do controle do código-fonte.)

No Mac OSX e no Linux com a CLI no mono, não há suporte para a restauração de pacotes com o PackageReference.

## <a name="usage"></a>Uso

```cli
nuget restore <projectPath> [options]
```

em `<projectPath>` que especifica o local de uma solução ou `packages.config` um arquivo. Consulte os [comentários](#remarks) abaixo para obter detalhes comportamentais.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ConfigFile | O arquivo de configuração do NuGet a ser aplicado. Se não for especificado `%AppData%\NuGet\NuGet.Config` , (Windows) `~/.nuget/NuGet/NuGet.Config` ou (Mac/Linux) será usado.|
| DirectDownload | *(4.0 +)* Baixa pacotes diretamente sem preencher os caches com binários ou metadados. |
| DisableParallelProcessing | Desabilita a restauração de vários pacotes em paralelo. |
| Fallback | *(3,2 +)* Uma lista de origens do pacote a ser usada como fallbacks caso o pacote não seja encontrado na fonte primária ou padrão. |
| ForceEnglishOutput | *(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês. |
| Help | Exibe informações de ajuda para o comando. |
| MSBuildPath | *(4.0 +)* Especifica o caminho do MSBuild a ser usado com o comando, tendo precedência sobre `-MSBuildVersion`. |
| MSBuildVersion | *(3,2 +)* Especifica a versão do MSBuild a ser usada com este comando. Os valores com suporte são 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Por padrão, o MSBuild em seu caminho é escolhido; caso contrário, ele usa a versão mais recente instalada do MSBuild. |
| NoCache | Impede que o NuGet use pacotes armazenados em cache. Consulte [Gerenciando os pacotes globais e as pastas de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Suprime prompts de entrada ou confirmações do usuário. |
| OutputDirectory | Especifica a pasta na qual os pacotes são instalados. Se nenhuma pasta for especificada, a pasta atual será usada. Necessário ao restaurar com um `packages.config` arquivo, `PackagesDirectory` a `SolutionDirectory` menos que ou seja usado.|
| PackageSaveMode | Especifica os tipos de arquivos a serem salvos após a instalação do pacote `nuspec`: `nupkg`um dos `nuspec;nupkg`, ou. |
| PackagesDirectory | Mesmo que `OutputDirectory`. Necessário ao restaurar com um `packages.config` arquivo, `OutputDirectory` a `SolutionDirectory` menos que ou seja usado. |
| Project2ProjectTimeOut | Tempo limite em segundos para resolver referências de projeto para projeto. |
| recursiva | *(4.0 +)* Restaura todos os projetos de referência para projetos UWP e .NET Core. Não se aplica a projetos que `packages.config`usam o. |
| RequireConsent | Verifica se a restauração de pacotes está habilitada antes de baixar e instalar os pacotes. Para obter detalhes, consulte [restauração de pacote](../../consume-packages/package-restore.md). |
| SolutionDirectory | Especifica a pasta da solução. Não é válido ao restaurar pacotes para uma solução. Necessário ao restaurar com um `packages.config` arquivo, `PackagesDirectory` a `OutputDirectory` menos que ou seja usado. |
| Origem | Especifica a lista de origens do pacote (como URLs) a serem usadas para a restauração. Se omitido, o comando usará as fontes fornecidas em arquivos de configuração, consulte Configurando o [comportamento do NuGet](../../consume-packages/configuring-nuget-behavior.md). |
| Verbosity | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="remarks"></a>Comentários

O comando Restore executa as seguintes etapas:

1. Determine o modo de operação do comando Restore.

   | tipo de arquivo projectPath | Comportamento |
   | --- | --- |
   | Solução (pasta) | O NuGet procura um `.sln` arquivo e usa-o, se for encontrado; caso contrário, retornará um erro. `(SolutionDir)\.nuget`é usado como a pasta inicial. |
   | `.sln`Grupo | Restaurar os pacotes identificados pela solução; retornará um erro se `-SolutionDirectory` for usado. `$(SolutionDir)\.nuget`é usado como a pasta inicial. |
   | `packages.config`ou arquivo de projeto | Restaure os pacotes listados no arquivo, resolvendo e instalando dependências. |
   | Outro tipo de arquivo | O arquivo deve ser um `.sln` arquivo como acima; se não for uma solução, o NuGet fornecerá um erro. |
   | (projectPath não especificado) | <ul><li>O NuGet procura arquivos de solução na pasta atual. Se um único arquivo for encontrado, ele será usado para restaurar pacotes; se várias soluções forem encontradas, o NuGet fornecerá um erro.</li><li>Se não houver arquivos de solução, o NuGet procurará `packages.config` por um e o usará para restaurar os pacotes.</li><li>Se nenhuma solução ou `packages.config` arquivo for encontrado, o NuGet fornecerá um erro.</ul> |

2. Determine a pasta pacotes usando a seguinte ordem de prioridade (o NuGet fornecerá um erro se nenhuma dessas pastas for encontrada):

    - A pasta especificada com `-PackagesDirectory`.
    - O `repositoryPath` valor em`Nuget.Config`
    - A pasta especificada com`-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Ao restaurar pacotes para uma solução, o NuGet faz o seguinte:
    - Carrega o arquivo de solução.
    - Restaura os `$(SolutionDir)\.nuget\packages.config` `packages` pacotes de nível de solução listados na pasta.
    - Restaure os `$(ProjectDir)\packages.config` `packages` pacotes listados na pasta. Para cada pacote especificado, restaure o pacote em paralelo, `-DisableParallelProcessing` a menos que seja especificado.

## <a name="examples"></a>Exemplos

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
