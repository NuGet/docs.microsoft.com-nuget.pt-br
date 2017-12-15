---
title: "Comando de instalação do NuGet CLI | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 59ac622f-837c-4545-bc93-a56330e02d71
description: "Referência para o comando de instalação de nuget.exe"
keywords: "NuGet instalar referência, o comando do pacote de instalação"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88c123a7f2a3d628713cefcc4b110fb0205093b4
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="install-command-nuget-cli"></a>instalar o comando (NuGet CLI)

**Aplica-se a:** pacote consumo &bullet; **versões com suporte:** todos

Baixa e instala um pacote em um projeto, o padrão para a pasta atual, usando fontes de pacote especificado.

> [!Tip]
> Para baixar um pacote diretamente fora do contexto de um projeto, visite a página do pacote no [nuget.org](https://www.nuget.org) e selecione o **baixar** link. 

Se nenhuma fonte for especificada, aqueles listados no arquivo de configuração global, `%APPDATA%\NuGet\NuGet.Config`, são usados. Consulte [Configurando NuGet comportamento](../consume-packages/configuring-nuget-behavior.md) para obter detalhes adicionais.

Se nenhum pacote específico é especificada, `install` instala todos os pacotes listados no projeto de `packages.config` arquivo, tornando-o como [ `restore` ](#restore). (O `install` comando não funciona com `project.json`.)

O `install` comando não modifica um arquivo de projeto ou `packages.config`; desse modo é semelhante a `restore` em que ele apenas adiciona os pacotes para o disco, mas não altera as dependências do projeto.

Para adicionar uma dependência, adicionar um projeto por meio do Gerenciador de pacote da interface do usuário ou o Console no Visual Studio ou modificar `packages.config` e, em seguida, execute um `install` ou `restore`. Para projetos que usam `project.json`, você pode modificar esse arquivo e, em seguida, executar `restore`.

## <a name="usage"></a>Uso

```
nuget install <packageID | configFilePath> [options]
```

onde `<packageID>` nomeia o pacote de instalação (usando a versão mais recente), ou `<configFilePath>` identifica o `packages.config` arquivo que lista os pacotes para instalar. Você pode indicar uma versão específica com o `-Version` opção.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ConfigFile | *(2.5 +)*  NuGet o arquivo de configuração para aplicar. Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado. |
| DisableParallelProcessing | Desativa a instalação de vários pacotes em paralelo. |
| ExcludeVersion | Instala o pacote para uma pasta chamada com apenas o nome do pacote e não o número de versão. |
| FallbackSource | *(3.2 +)*  Uma lista de fontes de pacote para usar como fallbacks caso o pacote não foi encontrado no primário ou a fonte padrão. |
| ForceEnglishOutput | *(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Framework | *(4.4 +)*  Usada para selecionar as dependências de estrutura de destino. O padrão é 'Any' se não for especificado. |
| Ajuda | Exibe informações de ajuda para o comando. |
| NoCache | Impede que o NuGet usando pacotes de caches de computador local. |
| Não interativo | Suprime avisos para a entrada do usuário ou confirmações. |
| OutputDirectory | Especifica a pasta na qual os pacotes são instalados. Se nenhuma pasta for especificada, a pasta atual será usada. |
| PackageSaveMode | Especifica os tipos de arquivos para salvar após a instalação do pacote: um dos `nuspec`, `nupkg`, ou `nuspec;nupkg`. |
| Versão de pré-lançamento | Permite que os pacotes de pré-lançamento ser instalado. Esse sinalizador não é necessário ao restaurar pacotes com `packages.config`. |
| RequireConsent | Verifica se a restauração de pacotes é habilitado antes de baixar e instalar os pacotes. Para obter detalhes, consulte [restauração do pacote](../consume-packages/package-restore.md). |
| SolutionDirectory | Especifica a pasta raiz da solução para a qual restaurar os pacotes. |
| Origem | Especifica a lista de fontes de pacote (como URLs) para usar. Se omitido, o comando usa as fontes fornecidas nos arquivos de configuração, consulte [NuGet Configurando comportamento](../Consume-Packages/Configuring-NuGet-Behavior.md). |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas (2.5 +)*. |
| Versão | Especifica a versão do pacote para instalar. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
