---
title: "Referência da Interface de linha de comando (CLI) do NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Índice de referência de linha de comando para o nuget.exe CLI"
keywords: "índice de referência de NuGet.exe, interface de linha de comando nuget.exe, nuget.exe CLI, comando nuget"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8b1ee17702f5a54a77dc2cd663e13729a9b4a39f
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-cli-reference"></a>Referência da CLI do NuGet

NuGet Interface de linha de comando (CLI), `nuget.exe`, fornece toda a extensão da funcionalidade do NuGet para instalar, criar, publicar e gerenciar pacotes sem fazer alterações nos arquivos de projeto.

Para usar qualquer comando, abra uma janela de comando ou bash shell, execute `nuget` seguido do comando e as opções apropriadas, como `nuget help pack` (para exibir a Ajuda sobre o comando de pacote).

Esta documentação reflete a versão mais recente do NuGet CLI. Para obter detalhes exatos para qualquer determinada versão que você está usando, execute `nuget help` para o comando desejado.

## <a name="installing-nugetexe"></a>Instalando o nuget.exe

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Tip]
> Para disponibilizar a CLI do NuGet no Console do Gerenciador de pacotes no Visual Studio, consulte [usando a CLI nuget.exe no console do](package-manager-console.md#using-the-nugetexe-cli-in-the-console).

## <a name="availability"></a>Disponibilidade

Consulte [recurso disponibilidade](../install-nuget-client-tools.md#feature-availability) para detalhes exatos.

- Todos os comandos estão disponíveis no Windows.
- Todos os comandos funcionam com nuget.exe em execução em Mono exceto onde indicado para `pack`, `restore`, e `update`.
- O `pack`, `restore`, `delete`, `locals`, e `push` comandos também estão disponíveis no Mac e Linux por meio do dotnet CLI.

## <a name="commands-and-applicability"></a>Comandos e aplicabilidade

Comandos disponíveis e aplicabilidade para criação de pacote, consumo de pacote, e/ou publicar um pacote para um host:

| Comandos comuns | Funções aplicáveis do | Versão do NuGet | Descrição |
| --- | --- | --- | --- |
| [pack](cli-ref-pack.md) | Criação | 2.7+ | Cria um pacote de NuGet de uma `.nuspec` ou arquivo de projeto. Ao executar em Mono, não há suporte a criação de um pacote de um arquivo de projeto. |
| [push](cli-ref-push.md) | Publicando | Todos | Publica um pacote para uma origem de pacote. |
| [config](cli-ref-config.md) | Todos | Todos | Obtém ou define os valores de configuração do NuGet. |
| [help ou ?](cli-ref-help.md) | Todos | Todos | Exibe a Ajuda informações ou ajuda para um comando. |
| [locals](cli-ref-locals.md) | Consumo | 3.3+ | Limpa ou lista de pacotes em vários caches ou a pasta pacotes global ou identifica essas pastas. |
| [restore](cli-ref-restore.md) | Consumo | 2.7+ | Restaura todos os pacotes referenciados pelo formato de referência de pacote em uso. Ao executar em Mono, não há suporte a restauração de pacotes usando o formato de PackageReference. |
| [setapikey](cli-ref-setapikey.md) | Publicação de consumo | Todos | Salva uma chave de API para uma origem do pacote fornecido quando essa origem de pacote exige uma chave de acesso. |
| [spec](cli-ref-spec.md) | Criação | Todos | Gera um `.nuspec` de arquivo, usando tokens se gerar o arquivo de um projeto do Visual Studio. |

| Comandos secundários | Funções aplicáveis do | Versão do NuGet | Descrição |
| --- | --- | --- | --- |
| [add](cli-ref-add.md) | Publicando | 3.3+ | Adiciona um pacote para uma origem de pacote de não-HTTP usando layout hierárquico. Para fontes HTTP, use *push*. |
| [delete](cli-ref-delete.md) | Publicando | Todos | Remove ou unlists um pacote de uma origem do pacote. |
| [init](cli-ref-init.md) | Criação | 3.3+ | Adiciona os pacotes de uma pasta para uma origem de pacote usando o layout hierárquico. |
| [install](cli-ref-install.md) | Consumo | Todos | Instala um pacote no atual projeto mas não modificar projetos ou fazer referência a arquivos. |
| [list](cli-ref-list.md) | Consumo, talvez a publicação | Todos | Exibe os pacotes de uma origem específica. |
| [mirror](cli-ref-mirror.md) | Publicando | 3.2 + preteridos no | Reflete um pacote e suas dependências de uma fonte para um repositório de destino. |
| [sources](cli-ref-sources.md) | Consumo, publicação | Todos | Gerencia as fontes de pacote nos arquivos de configuração. |
| [update](cli-ref-update.md) | Consumo | Todos | Atualiza os pacotes do projeto para as versões mais recentes disponíveis. Não tem suporte durante a execução em Mono. |

Comandos diferentes fazem uso de vários [variáveis de ambiente](cli-ref-environment-variables.md).

Comandos da CLI do NuGet por funções aplicáveis:

| Função | Comandos |
| --- | --- |
| Consumo | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` |
| Criação | `config`, `help`, `init`, `pack`, `spec` |
| Publicando | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

Por exemplo, os desenvolvedores preocupados apenas com pacotes, de consumo só precisam compreender para esse subconjunto de comandos do NuGet.

> [!Note]
> Os nomes de opções de comando diferenciam maiusculas de minúsculas. Opções que estão obsoletas não são incluídas nesta referência, como `NoPrompt` (substituído por `NonInteractive`) e `Verbose` (substituído por `Verbosity`).
