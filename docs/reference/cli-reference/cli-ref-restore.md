---
title: Comando de restauração da CLI do NuGet
description: Referência para o comando de restauração NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d1768a741e3f1c48e94d854fa7d365ebfa3513ea
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231143"
---
# <a name="restore-command-nuget-cli"></a>comando Restore (NuGet CLI)

**Aplica-se a: consumo de** pacote &bullet; **versões com suporte:** 2.7 +

Baixa e instala todos os pacotes ausentes na pasta `packages`. Quando usado com o NuGet 4.0 + e o formato PackageReference, o gera um arquivo de `<project>.nuget.props`, se necessário, na pasta `obj`. (O arquivo pode ser omitido do controle do código-fonte.)

No Mac OSX e no Linux com a CLI no mono, não há suporte para a restauração de pacotes com o PackageReference.

## <a name="usage"></a>Uso

```cli
nuget restore <projectPath> [options]
```

em que `<projectPath>` especifica o local de uma solução ou um arquivo de `packages.config`. Consulte os [comentários](#remarks) abaixo para obter detalhes comportamentais.

## <a name="options"></a>Opções

| Opção | DESCRIÇÃO |
| --- | --- |
| ConfigFile | O arquivo de configuração do NuGet a ser aplicado. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) será usado.|
| DirectDownload | *(4.0 +)* Baixa pacotes diretamente sem preencher os caches com binários ou metadados. |
| DisableParallelProcessing | Desabilita a restauração de vários pacotes em paralelo. |
| Fallback | *(3,2 +)* Uma lista de origens do pacote a ser usada como fallbacks caso o pacote não seja encontrado na fonte primária ou padrão. Use um ponto e vírgula para separar entradas de lista. |
| Force | Em projetos baseados em PackageReference, o forçará a resolução de todas as dependências, mesmo que a última restauração tenha sido bem-sucedida. A especificação desse sinalizador é semelhante à exclusão do arquivo de `project.assets.json`. Isso não ignora o cache http. |
| ForceEnglishOutput | *(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês. |
| ForceEvaluate | Força a restauração a reavaliar todas as dependências mesmo se um arquivo de bloqueio já existir. |
| Ajuda | Exibe informações de ajuda para o comando. |
| LockFilePath | Local de saída onde o arquivo de bloqueio do projeto é gravado. Por padrão, é ' PROJECT_ROOT \Packages.Lock.JSON '. |
| Bloqueadomode | Não permitir atualização do arquivo de bloqueio do projeto. |
| MSBuildPath | *(4.0 +)* Especifica o caminho do MSBuild a ser usado com o comando, tendo precedência sobre `-MSBuildVersion`. |
| MSBuildVersion | *(3,2 +)* Especifica a versão do MSBuild a ser usada com este comando. Os valores com suporte são 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Por padrão, o MSBuild em seu caminho é escolhido; caso contrário, ele usa a versão mais recente instalada do MSBuild. |
| NoCache | Impede que o NuGet use pacotes armazenados em cache. Consulte [Gerenciando os pacotes globais e as pastas de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Suprime prompts de entrada ou confirmações do usuário. |
| OutputDirectory | Especifica a pasta na qual os pacotes são instalados. Se nenhuma pasta for especificada, a pasta atual será usada. Necessário ao restaurar com um arquivo de `packages.config`, a menos que `PackagesDirectory` ou `SolutionDirectory` seja usado.|
| PackageSaveMode | Especifica os tipos de arquivos a serem salvos após a instalação do pacote: uma das `nuspec`, `nupkg`ou `nuspec;nupkg`. |
| PackagesDirectory | Igual a `OutputDirectory`. Necessário ao restaurar com um arquivo de `packages.config`, a menos que `OutputDirectory` ou `SolutionDirectory` seja usado. |
| Project2ProjectTimeOut | Tempo limite em segundos para resolver referências de projeto para projeto. |
| Recursiva | *(4.0 +)* Restaura todos os projetos de referência para projetos UWP e .NET Core. Não se aplica a projetos que usam `packages.config`. |
| RequireConsent | Verifica se a restauração de pacotes está habilitada antes de baixar e instalar os pacotes. Para obter detalhes, consulte [restauração de pacote](../../consume-packages/package-restore.md). |
| SolutionDirectory | Especifica a pasta da solução. Não é válido ao restaurar pacotes para uma solução. Necessário ao restaurar com um arquivo de `packages.config`, a menos que `PackagesDirectory` ou `OutputDirectory` seja usado. |
| Fonte | Especifica a lista de origens do pacote (como URLs) a serem usadas para a restauração. Se omitido, o comando usará as fontes fornecidas em arquivos de configuração, consulte [Configurando o comportamento do NuGet](../../consume-packages/configuring-nuget-behavior.md). Use um ponto e vírgula para separar entradas de lista. |
| UseLockFile | Habilita o arquivo de bloqueio do projeto a ser gerado e usado com a restauração. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="remarks"></a>Comentários

O comando Restore executa as seguintes etapas:

1. Determine o modo de operação do comando Restore.

   | tipo de arquivo projectPath | Comportamento |
   | --- | --- |
   | Solução (pasta) | O NuGet procura um arquivo de `.sln` e usa-o, se for encontrado; caso contrário, retornará um erro. `(SolutionDir)\.nuget` é usado como a pasta inicial. |
   | arquivo de `.sln` | Restaurar os pacotes identificados pela solução; retornará um erro se `-SolutionDirectory` for usado. `$(SolutionDir)\.nuget` é usado como a pasta inicial. |
   | `packages.config` ou arquivo de projeto | Restaure os pacotes listados no arquivo, resolvendo e instalando dependências. |
   | Outro tipo de arquivo | O arquivo é considerado um arquivo `.sln` como acima; Se não for uma solução, o NuGet fornecerá um erro. |
   | (projectPath não especificado) | <ul><li>O NuGet procura arquivos de solução na pasta atual. Se um único arquivo for encontrado, ele será usado para restaurar pacotes; se várias soluções forem encontradas, o NuGet fornecerá um erro.</li><li>Se não houver arquivos de solução, o NuGet procurará um `packages.config` e o usará para restaurar os pacotes.</li><li>Se nenhum arquivo de solução ou de `packages.config` for encontrado, o NuGet fornecerá um erro.</ul> |

2. Determine a pasta pacotes usando a seguinte ordem de prioridade (o NuGet fornecerá um erro se nenhuma dessas pastas for encontrada):

    - A pasta especificada com `-PackagesDirectory`.
    - O valor de `repositoryPath` em `Nuget.Config`
    - A pasta especificada com `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Ao restaurar pacotes para uma solução, o NuGet faz o seguinte:
    - Carrega o arquivo de solução.
    - Restaura os pacotes de nível de solução listados em `$(SolutionDir)\.nuget\packages.config` na pasta `packages`.
    - Restaure os pacotes listados em `$(ProjectDir)\packages.config` na pasta `packages`. Para cada pacote especificado, restaure o pacote em paralelo, a menos que `-DisableParallelProcessing` seja especificado.

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
