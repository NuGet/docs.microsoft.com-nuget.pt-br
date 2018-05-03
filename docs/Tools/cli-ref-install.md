---
title: Comando de instalação do NuGet CLI
description: Referência para o comando de instalação de nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 615f2beca1eb288417f2345fcdf25e323942d300
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="install-command-nuget-cli"></a>instalar o comando (NuGet CLI)

**Aplica-se a:** pacote consumo &bullet; **versões com suporte:** todos

Baixa e instala um pacote em um projeto, o padrão para a pasta atual, usando fontes de pacote especificado.

> [!Tip]
> Para baixar um pacote diretamente fora do contexto de um projeto, visite a página do pacote no [nuget.org](https://www.nuget.org) e selecione o **baixar** link.

Se nenhuma fonte for especificada, aqueles listados no arquivo de configuração global, `%appdata%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac Linux), são usados. Consulte [NuGet Configurando comportamento](../consume-packages/configuring-nuget-behavior.md) para obter detalhes adicionais.

Se nenhum pacote específico é especificada, `install` instala todos os pacotes listados no projeto de `packages.config` arquivo, tornando-o como [ `restore` ](cli-ref-restore.md).

O `install` comando não modifica um arquivo de projeto ou `packages.config`; desse modo é semelhante a `restore` em que ele apenas adiciona os pacotes para o disco, mas não altera as dependências do projeto.

Para adicionar uma dependência, adicionar um projeto por meio do Gerenciador de pacote da interface do usuário ou o Console no Visual Studio ou modificar `packages.config` e, em seguida, execute um `install` ou `restore`.

## <a name="usage"></a>Uso

```cli
nuget install <packageID | configFilePath> [options]
```

onde `<packageID>` nomeia o pacote de instalação (usando a versão mais recente), ou `<configFilePath>` identifica o `packages.config` arquivo que lista os pacotes para instalar. Você pode indicar uma versão específica com o `-Version` opção.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ConfigFile | O arquivo de configuração do NuGet para aplicar. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.|
| DependencyVersion | *(4.4 +)*  Especifica uma versão específica, substituindo o comportamento de resolução de dependência padrão. |
| DisableParallelProcessing | Desativa a instalação de vários pacotes em paralelo. |
| ExcludeVersion | Instala o pacote para uma pasta chamada com apenas o nome do pacote e não o número de versão. |
| FallbackSource | *(3.2 +)*  Uma lista de fontes de pacote para usar como fallbacks caso o pacote não foi encontrado no primário ou a fonte padrão. |
| ForceEnglishOutput | *(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Framework | *(4.4 +)*  Usada para selecionar as dependências de estrutura de destino. O padrão é 'Any' se não for especificado. |
| Ajuda | Exibe informações de ajuda para o comando. |
| NoCache | Impede que o NuGet usando pacotes armazenados em cache. Consulte [Gerenciando os pacotes globais e as pastas do cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Suprime avisos para a entrada do usuário ou confirmações. |
| OutputDirectory | Especifica a pasta na qual os pacotes são instalados. Se nenhuma pasta for especificada, a pasta atual será usada. |
| PackageSaveMode | Especifica os tipos de arquivos para salvar após a instalação do pacote: um dos `nuspec`, `nupkg`, ou `nuspec;nupkg`. |
| Versão de pré-lançamento | Permite que os pacotes de pré-lançamento ser instalado. Esse sinalizador não é necessário ao restaurar pacotes com `packages.config`. |
| RequireConsent | Verifica se a restauração de pacotes é habilitado antes de baixar e instalar os pacotes. Para obter detalhes, consulte [restauração do pacote](../consume-packages/package-restore.md). |
| SolutionDirectory | Especifica a pasta raiz da solução para a qual restaurar os pacotes. |
| Origem | Especifica a lista de fontes de pacote (como URLs) para usar. Se omitido, o comando usa as fontes fornecidas nos arquivos de configuração, consulte [NuGet Configurando comportamento](../consume-packages/configuring-nuget-behavior.md). |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |
| Versão | Especifica a versão do pacote para instalar. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
