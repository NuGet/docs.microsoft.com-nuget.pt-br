---
title: Comando de atualização da CLI do NuGet
description: Referência para o comando nuget.exe Update
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 5f244e4cf15ca7afa0e6318a8c20d464ff75bd8e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323642"
---
# <a name="update-command-nuget-cli"></a>comando Update (NuGet CLI)

**Aplica-se a:** &bullet; **versões com suporte** do consumo do pacote: todas

Atualiza todos os pacotes de um projeto (usando `packages.config`) para as últimas versões disponíveis. É recomendável executar [' Restore '](cli-ref-restore.md) antes de executar o `update` . (Para atualizar um pacote individual, use [`nuget install`](cli-ref-install.md) sem especificar um número de versão, caso em que o NuGet instala a versão mais recente.)

Observação: `update` o não funciona com a CLI em execução em mono (Mac OSX ou Linux) ou ao usar o formato PackageReference.

O `update` comando também atualiza referências de assembly no arquivo de projeto, desde que essas referências já existam. Se um pacote atualizado tiver um assembly adicionado, uma nova referência *não* será adicionada. Novas dependências de pacote também não têm suas referências de assembly adicionadas. Para incluir essas operações como parte de uma atualização, atualize o pacote no Visual Studio usando a interface do usuário do Gerenciador de pacotes ou o console do Gerenciador de pacotes.

Esse comando também pode ser usado para atualizar nuget.exe si mesmo usando o sinalizador *-Self* .

## <a name="usage"></a>Uso

```cli
nuget update <configPath> [options]
```

onde `<configPath>` o identifica um `packages.config` arquivo de solução ou que lista as dependências do projeto.

## <a name="options"></a>Opções

- **`-ConfigFile`**

  O arquivo de configuração do NuGet a ser aplicado. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  Especifica a versão dos pacotes de dependência a serem usados, que pode ser um dos seguintes:<br/><ul><li>*Mais baixo* (padrão): a versão mais baixa</li><li>*HighestPatch*: a versão com o menor principal, menor o mais baixo, patch mais alto</li><li>*HighestMinor*: a versão com o menor principal, o mais baixo, o patch mais alto</li><li>*Mais alto*: a versão mais recente</li><li>*Ignorar*: nenhum pacote de dependência será usado</li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  Especifica a ação padrão quando um arquivo de um pacote já existe no projeto de destino. Defina como `Overwrite` para sempre substituir arquivos. Defina como `Ignore` para ignorar arquivos.

  A `PromptUser` ação, o padrão, solicitará cada arquivo conflitante, a menos que `OverwriteAll` ou `IgnoreAll` seja fornecido, que será aplicado a todos os arquivos restantes.

- **`-ForceEnglishOutput`**

  *(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.

- **`-?|-help`**

  Exibe informações de ajuda para o comando.

- **`-Id`**

  Especifica uma lista de IDs de pacote a serem atualizadas.

- **`-MSBuildPath`**

  *(4.0 +)* Especifica o caminho do MSBuild a ser usado com o comando, tendo precedência sobre `-MSBuildVersion` .

- **`-MSBuildVersion`**

  *(3,2 +)* Especifica a versão do MSBuild a ser usada com este comando. Os valores com suporte são 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Por padrão, o MSBuild em seu caminho é escolhido; caso contrário, ele usa a versão mais recente instalada do MSBuild.

- **`-NonInteractive`**

  Suprime prompts de entrada ou confirmações do usuário.

- **`-PreRelease`**

  Permite atualizar para versões de pré-lançamento. Esse sinalizador não é necessário ao atualizar pacotes de pré-lançamento que já estão instalados.

- **`-RepositoryPath`**

  Especifica a pasta local onde os pacotes são instalados.

- **`-Safe`**

  Especifica que somente as atualizações com a versão mais recente disponível na mesma versão principal e secundária do pacote instalado serão instaladas.

- **`-Self`**

  Atualizações `nuget.exe` para a versão mais recente. `-Source` pode ser usado no entanto, todos os outros argumentos são ignorados. Se nenhuma fonte for fornecida, o verificará se há `nuget.org` atualizações, independentemente das `NuGet.Config` configurações.

- **`-Source`**

  Especifica a lista de origens do pacote (como URLs) a serem usadas para as atualizações. Se omitido, o comando usará as fontes fornecidas em arquivos de configuração, consulte [configurações comuns do NuGet](../../consume-packages/configuring-nuget-behavior.md).

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .

- **`-Version`**

  Quando usado com uma ID de pacote, especifica a versão do pacote a ser atualizada.

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
