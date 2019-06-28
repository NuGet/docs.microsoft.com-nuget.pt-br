---
title: Referência de Interface de linha de comando (CLI) do NuGet
description: Índice de referência de linha de comando para a CLI nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: a257dbbd9d56b5989e050ed4096d096cd1036184
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426016"
---
# <a name="nuget-cli-reference"></a>Referência da CLI do NuGet

A Interface de linha de comando (CLI do NuGet), `nuget.exe`, fornece toda a extensão da funcionalidade do NuGet para instalar, criar, publicar e gerenciar pacotes sem fazer nenhuma alteração aos arquivos de projeto.

Para usar qualquer comando, abra uma janela de comando ou shell bash, em seguida, execute `nuget` seguido do comando e as opções apropriadas, como `nuget help pack` (para exibir a Ajuda sobre o comando pack).

Esta documentação reflete a versão mais recente da CLI do NuGet. Para obter detalhes exatos para qualquer determinada versão que você está usando, execute `nuget help` para o comando desejado.

Para aprender a usar os comandos básicos com o `nuget.exe` CLI, consulte [instalar e usar pacotes usando a CLI nuget.exe](../consume-packages/install-use-packages-nuget-cli.md).

## <a name="installing-nugetexe"></a>Instalando nuget.exe

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> Para disponibilizar a CLI do NuGet dentro do Console do Gerenciador de pacotes no Visual Studio, consulte [usando a CLI nuget.exe no console do](package-manager-console.md#using-the-nugetexe-cli-in-the-console).

## <a name="availability"></a>Disponibilidade

Ver [disponibilidade de recursos](../install-nuget-client-tools.md#feature-availability) para ver os detalhes.

- Todos os comandos estão disponíveis no Windows.
- Todos os comandos funcionam com nuget.exe em execução em Mono, exceto onde indicado para `pack`, `restore`, e `update`.
- O `pack`, `restore`, `delete`, `locals`, e `push` comandos também estão disponíveis no Mac e Linux por meio da CLI do dotnet.

## <a name="commands-and-applicability"></a>Comandos e aplicabilidade

Comandos disponíveis e a aplicabilidade a criação do pacote, consumo de pacote e/ou publicar um pacote para um host:

| Comandos comuns | Funções aplicáveis do | Versão do NuGet | Descrição |
| --- | --- | --- | --- |
| [pack](cli-ref-pack.md) | Criação | 2.7+ | Cria um pacote NuGet de um `.nuspec` ou arquivo de projeto. Quando em execução no Mono, não há suporte criando um pacote em um arquivo de projeto. |
| [push](cli-ref-push.md) | Publicando | Todos | Publica um pacote para uma origem de pacote. |
| [config](cli-ref-config.md) | Todos | Todos | Obtém ou define os valores de configuração do NuGet. |
| [help or ?](cli-ref-help.md) | Todos | Todos | Exibe a Ajuda de informações ou ajuda para um comando. |
| [locals](cli-ref-locals.md) | Consumo | 3.3+ | Lista os locais do *global-packages*, *http-cache*, e *temp* limpa o conteúdo dessas pastas e pastas. |
| [restore](cli-ref-restore.md) | Consumo | 2.7+ | Restaura todos os pacotes referenciados pelo formato de gerenciamento de pacote em uso. Quando em execução no Mono, não há suporte a restauração de pacotes usando o formato PackageReference. |
| [setapikey](cli-ref-setapikey.md) | Publicação, consumo | Todos | Salva uma chave de API para uma fonte de pacote especificado quando essa origem do pacote requer uma chave de acesso. |
| [spec](cli-ref-spec.md) | Criação | Todos | Gera um `.nuspec` de arquivo, usando tokens se gerar o arquivo de um projeto do Visual Studio. |

| Comandos secundários | Funções aplicáveis do | Versão do NuGet | Descrição |
| --- | --- | --- | --- |
| [add](cli-ref-add.md) | Publicando | 3.3+ | Adiciona um pacote a uma fonte de pacote não HTTP usando o layout hierárquico. Para fontes HTTP, use *push*. |
| [delete](cli-ref-delete.md) | Publicando | Todos | Remove ou retira da lista um pacote a partir de uma origem de pacote. |
| [init](cli-ref-init.md) | Criação | 3.3+ | Adiciona os pacotes de uma pasta a uma fonte de pacote usando o layout hierárquico. |
| [install](cli-ref-install.md) | Consumo | Todos | Instala um pacote com o atual do projeto, mas não modifica os projetos ou fazer referência a arquivos. |
| [list](cli-ref-list.md) | Consumo, talvez de publicação | Todos | Exibe os pacotes de uma origem específica. |
| [mirror](cli-ref-mirror.md) | Publicando | Preterido no 3.2 e superior | Espelha um pacote e suas dependências de uma fonte para um repositório de destino. |
| [sources](cli-ref-sources.md) | Consumo, a publicação | Todos | Gerencia as origens de pacote em arquivos de configuração. |
| [update](cli-ref-update.md) | Consumo | Todos | Pacotes de um projeto é atualizado para versões mais recentes disponíveis. Não tem suporte durante a execução em Mono. |

Comandos diferentes de fazer uso de vários [variáveis de ambiente](cli-ref-environment-variables.md).

Comandos da CLI do NuGet por funções aplicáveis:

| Função | Comandos |
| --- | --- |
| Consumo | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` |
| Criação | `config`, `help`, `init`, `pack`, `spec` |
| Publicando | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

Os desenvolvedores preocupados apenas com o consumo de pacotes, por exemplo, só precisam compreender esse subconjunto de comandos do NuGet.

> [!Note]
> Nomes de opção de comando diferenciam maiusculas de minúsculas. As opções que foram preteridas não estão incluídas nesta referência, como `NoPrompt` (substituído por `NonInteractive`) e `Verbose` (substituído por `Verbosity`).
