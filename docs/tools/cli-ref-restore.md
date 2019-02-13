---
title: Comando de restauração da CLI do NuGet
description: Referência do comando de restauração nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: adf97196f50f2a55d6b8ceed93d53ff12b67657b
ms.sourcegitcommit: d5a35a097e6b461ae791d9f66b3a85d5219d7305
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56145625"
---
# <a name="restore-command-nuget-cli"></a>Restaurar comando (CLI do NuGet)

**Aplica-se a:** consumo do pacote &bullet; **versões com suporte:** 2.7+

Baixa e instala todos os pacotes ausentes do `packages` pasta. Quando usado com o NuGet 4.0 + e o formato PackageReference, gera uma `<project>.nuget.props` do arquivo, se necessário, o `obj` pasta. (O arquivo pode ser omitido do controle de origem).

No Mac OSX e Linux com a CLI no Mono, restaurando pacotes não é compatível com o PackageReference.

## <a name="usage"></a>Uso

```cli
nuget restore <projectPath> [options]
```

em que `<projectPath>` Especifica o local de uma solução ou um `packages.config` arquivo. Ver [comentários](#remarks) abaixo para obter detalhes de comportamentos.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ConfigFile | O arquivo de configuração do NuGet para aplicar. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.|
| DirectDownload | *(4.0 e posteriores)*  Baixa os pacotes diretamente sem populá caches com quaisquer binários ou de metadados. |
| DisableParallelProcessing | Desabilita a restauração de vários pacotes em paralelo. |
| FallbackSource | *(3.2 e superior)*  Uma lista de origens de pacote a ser usado como fallbacks no caso do pacote não for encontrado no primário ou a fonte padrão. |
| ForceEnglishOutput | *(3.5 ou superior)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Ajuda | Exibe informações de ajuda para o comando. |
| MSBuildPath | *(4.0 e posteriores)*  Especifica o caminho do MSBuild a usar com o comando, tendo precedência sobre `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 e superior)*  Especifica a versão do MSBuild a ser usado com este comando. Valores com suporte são 4, 12, 14, 15.1, 15.3, 15.4, 15,5, 15.6, 15.7, 15,8, 15,9. Por padrão que o MSBuild em seu caminho é escolhido, caso contrário, o padrão é a versão mais recente instalada do MSBuild. |
| NoCache | Impede que o NuGet usando pacotes armazenados em cache. Ver [gerenciar as pastas de cache e de pacotes globais](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Suprime a solicitações de entrada do usuário ou confirmações. |
| OutputDirectory | Especifica a pasta na qual os pacotes são instalados. Se nenhuma pasta for especificada, a pasta atual será usada. Necessário quando a restauração com um `packages.config` do arquivo, a menos que `PackagesDirectory` ou `SolutionDirectory` é usado.|
| PackageSaveMode | Especifica os tipos de arquivos a serem salvos após a instalação do pacote: um dos `nuspec`, `nupkg`, ou `nuspec;nupkg`. |
| PackagesDirectory | Mesmo que `OutputDirectory`. Necessário quando a restauração com um `packages.config` do arquivo, a menos que `OutputDirectory` ou `SolutionDirectory` é usado. |
| Project2ProjectTimeOut | Tempo limite em segundos para resolver referências de projeto a projeto. |
| Recursiva | *(4.0 e posteriores)*  Restaura todas as referências de projetos para projetos UWP e .NET Core. Não se aplica a projetos que usam `packages.config`. |
| RequireConsent | Verifica se a restauração de pacotes está habilitado antes de baixar e instalar os pacotes. Para obter detalhes, consulte [restauração de pacote](../consume-packages/package-restore.md). |
| SolutionDirectory | Especifica a pasta de solução. Não é válido ao restaurar pacotes para uma solução. Necessário quando a restauração com um `packages.config` do arquivo, a menos que `PackagesDirectory` ou `OutputDirectory` é usado. |
| Origem | Especifica a lista de origens de pacote (como URLs) para usar para a restauração. Se omitido, o comando usa as fontes fornecidas em arquivos de configuração, consulte [o comportamento do NuGet configurando](../consume-packages/configuring-nuget-behavior.md). |
| Detalhamento |> especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="remarks"></a>Comentários

O comando restore realiza as seguintes etapas:

1. Determine o modo de operação do comando restore.

   | tipo de arquivo projectPath | Comportamento |
   | --- | --- |
   | Solução (pasta) | O NuGet procurará um `.sln` arquivo e usa esse se encontrado; caso contrário, retorna um erro. `(SolutionDir)\.nuget` é usado como pasta inicial. |
   | `.sln` Arquivo | Restaurar pacotes identificados pela solução; gera um erro se `-SolutionDirectory` é usado. `$(SolutionDir)\.nuget` é usado como pasta inicial. |
   | `packages.config` ou o arquivo de projeto | Restaure os pacotes listados no arquivo, resolução e instalação de dependências. |
   | Outro tipo de arquivo | Arquivo é considerado um `.sln` arquivo acima; se ele não é uma solução, o NuGet fornece um erro. |
   | (projectPath não especificado) | <ul><li>O NuGet procura por arquivos de solução na pasta atual. Se for encontrado um único arquivo, que é usado para restaurar os pacotes; Se forem encontradas várias soluções, o NuGet apresentará um erro.</li><li>Se não houver nenhum arquivo de solução, o NuGet procurará um `packages.config` e usa isso para restaurar os pacotes.</li><li>Se nenhuma solução ou `packages.config` arquivo for encontrado, o NuGet apresentará um erro.</ul> |

2. Determine a pasta de pacotes usando a seguinte ordem de prioridade (NuGet apresentará um erro se nenhuma dessas pastas forem encontradas):

    - A pasta especificada com `-PackagesDirectory`.
    - O `repositoryPath` valor em `Nuget.Config`
    - A pasta especificada com `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Ao restaurar pacotes para uma solução, o NuGet faz o seguinte:
    - Carrega o arquivo de solução.
    - Restaura os pacotes de nível de solução listados na `$(SolutionDir)\.nuget\packages.config` para o `packages` pasta.
    - Restaurar os pacotes listados em `$(ProjectDir)\packages.config` para o `packages` pasta. Para cada pacote especificado, restaurar o pacote em paralelo, a menos que `-DisableParallelProcessing` for especificado.

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
