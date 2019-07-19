---
title: Referência da CLI (interface de linha de comando) do NuGet
description: Índice de referência de linha de comando para a CLI do NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: 52aa2c533a8b67ae10455888a34a7ac9767fd0e3
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327463"
---
# <a name="nuget-cli-reference"></a>Referência da CLI do NuGet

A CLI (interface de linha de comando) `nuget.exe`do NuGet, fornece a extensão completa da funcionalidade do NuGet para instalar, criar, publicar e gerenciar pacotes sem fazer alterações nos arquivos de projeto.

Para usar qualquer comando, abra uma janela de comando ou um shell bash e `nuget` , em seguida, execute o seguido pelo comando e `nuget help pack` as opções apropriadas, como (para exibir a ajuda no comando do pacote).

Esta documentação reflete a versão mais recente da CLI do NuGet. Para obter detalhes exatos de qualquer versão específica que você esteja usando `nuget help` , execute para o comando desejado.

Para saber como usar comandos básicos com a CLI do `nuget.exe`, confira [Instalar e usar pacotes usando a CLI do nuget.exe](../consume-packages/install-use-packages-nuget-cli.md).

## <a name="installing-nugetexe"></a>Instalando NuGet. exe

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> Para disponibilizar a CLI do NuGet no console do Gerenciador de pacotes no Visual Studio, consulte [usando a CLI do NuGet. exe no console](../consume-packages/install-use-packages-powershell.md#use-the-nugetexe-cli-in-the-console)do.

## <a name="availability"></a>Disponibilidade

Consulte [disponibilidade de recursos](../install-nuget-client-tools.md#feature-availability) para obter detalhes exatos.

- Todos os comandos estão disponíveis no Windows.
- Todos os comandos funcionam com NuGet. exe em execução no mono, exceto `pack`quando `restore`indicado para `update`, e.
- Os `pack`comandos `restore` ,,`locals`, e também`push` estão disponíveis no Mac e no Linux por meio da CLI dotnet. `delete`

## <a name="commands-and-applicability"></a>Comandos e aplicabilidade

Comandos disponíveis e aplicabilidade à criação de pacote, consumo de pacote e/ou publicação de um pacote em um host:

| Comandos comuns | Funções aplicáveis | Versão do NuGet | Descrição |
| --- | --- | --- | --- |
| [pack](cli-reference/cli-ref-pack.md) | Criação | 2.7+ | Cria um pacote NuGet a partir `.nuspec` de um arquivo de projeto do ou do. Quando executado em mono, não há suporte para a criação de um pacote a partir de um arquivo de projeto. |
| [push](cli-reference/cli-ref-push.md) | Publicando | Todos | Publica um pacote em uma origem de pacote. |
| [config](cli-reference/cli-ref-config.md) | Todos | Todos | Obtém ou define os valores de configuração do NuGet. |
| [help or ?](cli-reference/cli-ref-help.md) | Todos | Todos | Exibe informações de ajuda ou ajuda para um comando. |
| [locals](cli-reference/cli-ref-locals.md) | Consumo | 3.3+ | Lista os locais das pastas *global-Packages*, *http-cache*e *Temp* e limpa o conteúdo dessas pastas. |
| [restore](cli-reference/cli-ref-restore.md) | Consumo | 2.7+ | Restaura todos os pacotes referenciados pelo formato de gerenciamento de pacote em uso. Quando executado no mono, não há suporte para a restauração de pacotes usando o formato PackageReference. |
| [setapikey](cli-reference/cli-ref-setapikey.md) | Publicação, consumo | Todos | Salva uma chave de API para uma determinada origem do pacote quando a origem do pacote requer uma chave para o acesso. |
| [spec](cli-reference/cli-ref-spec.md) | Criação | Todos | Gera um `.nuspec` arquivo, usando tokens, se estiver gerando o arquivo de um projeto do Visual Studio. |

| Comandos secundários | Funções aplicáveis | Versão do NuGet | Descrição |
| --- | --- | --- | --- |
| [add](cli-reference/cli-ref-add.md) | Publicando | 3.3+ | Adiciona um pacote a uma origem de pacote não HTTP usando layout hierárquico. Para fontes HTTP, use *Push*. |
| [delete](cli-reference/cli-ref-delete.md) | Publicando | Todos | Remove ou deslista um pacote de uma origem de pacote. |
| [init](cli-reference/cli-ref-init.md) | Criação | 3.3+ | Adiciona pacotes de uma pasta a uma origem de pacote usando layout hierárquico. |
| [install](cli-reference/cli-ref-install.md) | Consumo | Todos | Instala um pacote no projeto atual, mas não modifica projetos ou arquivos de referência. |
| [list](cli-reference/cli-ref-list.md) | Consumo, talvez publicação | Todos | Exibe pacotes de uma determinada origem. |
| [mirror](cli-reference/cli-ref-mirror.md) | Publicando | Preterido em 3.2 + | Espelha um pacote e suas dependências de uma origem para um repositório de destino. |
| [sources](cli-reference/cli-ref-sources.md) | Consumo, publicação | Todos | Gerencia fontes de pacote em arquivos de configuração. |
| [update](cli-reference/cli-ref-update.md) | Consumo | Todos | Atualiza os pacotes de um projeto para as versões mais recentes disponíveis. Sem suporte durante a execução em mono. |

Comandos diferentes fazem uso de várias [variáveis de ambiente](cli-reference/cli-ref-environment-variables.md).

Comandos da CLI do NuGet por funções aplicáveis:

| Função | Comandos |
| --- | --- |
| Consumo | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` |
| Criação | `config`, `help`, `init`, `pack`, `spec` |
| Publicando | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

Os desenvolvedores preocupados apenas com pacotes de consumo, por exemplo, precisam apenas entender o subconjunto de comandos do NuGet.

> [!Note]
> Os nomes de opção de comando não diferenciam maiúsculas de minúsculas. As opções preteridas não são incluídas nessa referência `NoPrompt` , como (substituído por `NonInteractive`) e `Verbose` (substituído por `Verbosity`).
