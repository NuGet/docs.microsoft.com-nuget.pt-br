---
title: Comando de instalação da CLI do NuGet
description: Referência para o comando de instalação NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f39bcc67c5f659f05ef02f2579bcf07b4481bb27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327783"
---
# <a name="install-command-nuget-cli"></a>Commando install (NuGet CLI)

**Aplica-se a:** &bullet; **versões com suporte** do consumo do pacote: todas

Baixa e instala um pacote em um projeto, padronizando para a pasta atual, usando as origens do pacote especificado.

> [!Tip]
> Para baixar um pacote diretamente fora do contexto de um projeto, visite a página do pacote em [NuGet.org](https://www.nuget.org) e selecione o link de **Download** .

Se nenhuma fonte for especificada, as listadas no arquivo de configuração global `%appdata%\NuGet\NuGet.Config` , (Windows) `~/.nuget/NuGet/NuGet.Config` ou (Mac/Linux) serão usadas. Consulte [configurações comuns do NuGet](../../consume-packages/configuring-nuget-behavior.md) para obter detalhes adicionais.

Se nenhum pacote específico for especificado, `install` o instalará todos os pacotes listados no `packages.config` arquivo do projeto, tornando- [`restore`](cli-ref-restore.md)o semelhante a.

O `install` comando não modifica um arquivo de projeto ou `packages.config`; dessa forma, é semelhante a `restore` ele apenas adiciona pacotes ao disco, mas não altera as dependências de um projeto.

Para adicionar uma dependência, adicione um pacote por meio da interface do usuário ou console do Gerenciador de pacotes no Visual `packages.config` Studio, ou modifique `install` e `restore`execute o ou o.

## <a name="usage"></a>Uso

```cli
nuget install <packageID | configFilePath> [options]
```

onde `<packageID>` o nomeia o pacote a ser instalado (usando a versão mais recente `<configFilePath>` ) ou `packages.config` identifica o arquivo que lista os pacotes a serem instalados. Você pode indicar uma versão específica com a `-Version` opção.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ConfigFile | O arquivo de configuração do NuGet a ser aplicado. Se não for especificado `%AppData%\NuGet\NuGet.Config` , (Windows) `~/.nuget/NuGet/NuGet.Config` ou (Mac/Linux) será usado.|
| DependencyVersion | *(4.4 +)* A versão dos pacotes de dependência a serem usados, que pode ser uma das seguintes:<br/><ul><li>*Mais baixo* (padrão): a versão mais baixa</li><li>*HighestPatch*: a versão com o menor principal, menor o mais baixo, patch mais alto</li><li>*HighestMinor*: a versão com o menor principal, o mais baixo, o patch mais alto</li><li>*Mais alto*: a versão mais recente</li></ul> |
| DisableParallelProcessing | Desabilita a instalação de vários pacotes em paralelo. |
| ExcludeVersion | Instala o pacote em uma pasta chamada somente com o nome do pacote e não com o número de versão. |
| Fallback | *(3,2 +)* Uma lista de origens do pacote a ser usada como fallbacks caso o pacote não seja encontrado na fonte primária ou padrão. |
| ForceEnglishOutput | *(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês. |
| Framework | *(4.4 +)* Estrutura de destino usada para selecionar dependências. O padrão é ' any ' se não for especificado. |
| Ajuda | Exibe informações de ajuda para o comando. |
| NoCache | Impede que o NuGet use pacotes armazenados em cache. Consulte [Gerenciando os pacotes globais e as pastas de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Suprime prompts de entrada ou confirmações do usuário. |
| OutputDirectory | Especifica a pasta na qual os pacotes são instalados. Se nenhuma pasta for especificada, a pasta atual será usada. |
| PackageSaveMode | Especifica os tipos de arquivos a serem salvos após a instalação do pacote `nuspec`: `nupkg`um dos `nuspec;nupkg`, ou. |
| Pré-lançamento | Permite que pacotes de pré-lançamento sejam instalados. Esse sinalizador não é necessário ao restaurar pacotes com `packages.config`o. |
| RequireConsent | Verifica se a restauração de pacotes está habilitada antes de baixar e instalar os pacotes. Para obter detalhes, consulte [restauração de pacote](../../consume-packages/package-restore.md). |
| SolutionDirectory | Especifica a pasta raiz da solução para a qual os pacotes são restaurados. |
| Origem | Especifica a lista de origens do pacote (como URLs) a serem usadas. Se omitido, o comando usará as fontes fornecidas em arquivos de configuração, consulte [configurações comuns do NuGet](../../consume-packages/configuring-nuget-behavior.md). |
| Verbosity | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*. |
| Versão | Especifica a versão do pacote a ser instalado. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
