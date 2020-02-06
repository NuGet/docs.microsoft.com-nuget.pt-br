---
title: Comando de instalação da CLI do NuGet
description: Referência para o comando de instalação NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6c49b2406462eae6ce45c65dfd8b3a9eb1077e73
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036936"
---
# <a name="install-command-nuget-cli"></a>Commando install (NuGet CLI)

**Aplica-se a: consumo de** pacote &bullet; **versões com suporte:** todos

Baixa e instala um pacote em um projeto, padronizando para a pasta atual, usando as origens do pacote especificado.

> [!Tip]
> Para baixar um pacote diretamente fora do contexto de um projeto, visite a página do pacote em [NuGet.org](https://www.nuget.org) e selecione o link de **Download** .

Se nenhuma fonte for especificada, as listadas no arquivo de configuração global, `%appdata%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), serão usadas. Consulte [configurações comuns do NuGet](../../consume-packages/configuring-nuget-behavior.md) para obter detalhes adicionais.

Se nenhum pacote específico for especificado, `install` instalará todos os pacotes listados no arquivo de `packages.config` do projeto, tornando-o semelhante a [`restore`](cli-ref-restore.md).

O comando `install` não modifica um arquivo de projeto ou `packages.config`; dessa forma, é semelhante a `restore`, pois só adiciona pacotes ao disco, mas não altera as dependências de um projeto.

Para adicionar uma dependência, adicione um pacote por meio da interface do usuário ou console do Gerenciador de pacotes no Visual Studio, ou modifique `packages.config` e execute `install` ou `restore`.

## <a name="usage"></a>Uso

```cli
nuget install <packageID | configFilePath> [options]
```

em que `<packageID>` nomeia o pacote a ser instalado (usando a versão mais recente) ou `<configFilePath>` identifica o arquivo de `packages.config` que lista os pacotes a serem instalados. Você pode indicar uma versão específica com a opção `-Version`.

## <a name="options"></a>Opções

| Opção | DESCRIÇÃO |
| --- | --- |
| ConfigFile | O arquivo de configuração do NuGet a ser aplicado. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) será usado.|
| DependencyVersion | *(4.4 +)* A versão dos pacotes de dependência a serem usados, que pode ser uma das seguintes:<br/><ul><li>*Mais baixo* (padrão): a versão mais baixa</li><li>*HighestPatch*: a versão com o menor principal, menor o mais baixo, patch mais alto</li><li>*HighestMinor*: a versão com o menor principal, o mais baixo, o patch mais alto</li><li>*Mais alto*: a versão mais recente</li><li>*Ignorar*: nenhum pacote de dependência será usado</li></ul> |
| DisableParallelProcessing | Desabilita a instalação de vários pacotes em paralelo. |
| ExcludeVersion | Instala o pacote em uma pasta chamada somente com o nome do pacote e não com o número de versão. |
| Fallback | *(3,2 +)* Uma lista de origens do pacote a ser usada como fallbacks caso o pacote não seja encontrado na fonte primária ou padrão. |
| ForceEnglishOutput | *(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês. |
| Framework | *(4.4 +)* Estrutura de destino usada para selecionar dependências. O padrão é ' any ' se não for especificado. |
| Ajuda | Exibe informações de ajuda para o comando. |
| NoCache | Impede que o NuGet use pacotes armazenados em cache. Consulte [Gerenciando os pacotes globais e as pastas de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Suprime prompts de entrada ou confirmações do usuário. |
| OutputDirectory | Especifica a pasta na qual os pacotes são instalados. Se nenhuma pasta for especificada, a pasta atual será usada. |
| PackageSaveMode | Especifica os tipos de arquivos a serem salvos após a instalação do pacote: uma das `nuspec`, `nupkg`ou `nuspec;nupkg`. |
| PreRelease | Permite que pacotes de pré-lançamento sejam instalados. Esse sinalizador não é necessário ao restaurar pacotes com `packages.config`. |
| RequireConsent | Verifica se a restauração de pacotes está habilitada antes de baixar e instalar os pacotes. Para obter detalhes, consulte [restauração de pacote](../../consume-packages/package-restore.md). |
| SolutionDirectory | Especifica a pasta raiz da solução para a qual os pacotes são restaurados. |
| Fonte | Especifica a lista de origens do pacote (como URLs) a serem usadas. Se omitido, o comando usará as fontes fornecidas em arquivos de configuração, consulte [configurações comuns do NuGet](../../consume-packages/configuring-nuget-behavior.md). |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*. |
| Versão | Especifica a versão do pacote a instalar. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
