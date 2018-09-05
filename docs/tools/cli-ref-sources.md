---
title: CLI do NuGet fontes de comando
description: Referência para o nuget.exe fontes de comando
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7ef856f783c8e11cdb40edb0d1c1458730d87262
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548102"
---
# <a name="sources-command-nuget-cli"></a>Commando sources (NuGet CLI)

**Aplica-se a:** consumo de pacote, publicando &bullet; **versões com suporte:** todos os

Gerencia a lista de fontes, localizado no arquivo de configuração de escopo de usuário ou um arquivo de configuração especificado. O arquivo de configuração de escopo do usuário está localizado em `%appdata%\NuGet\NuGet.Config` (Windows) e `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).

Observe que a URL de origem para nuget.org é `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Uso

```cli
nuget sources <operation> -Name <name> -Source <source>
```

em que `<operation>` é uma das *listar, adicionar, remover, habilitar, desabilitar* ou *Update*, `<name>` é o nome da fonte, e `<source>` é a URL da fonte.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ConfigFile | O arquivo de configuração do NuGet para aplicar. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.|
| ForceEnglishOutput | *(3.5 ou superior)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Formatar | Aplica-se para o `list` ação e pode ser `Detailed` (o padrão) ou `Short`. |
| Ajuda | Exibe informações de ajuda para o comando. |
| NonInteractive | Suprime a solicitações de entrada do usuário ou confirmações. |
| Senha | Especifica a senha para autenticação com o código-fonte. |
| StorePasswordInClearText | Indica para armazenar a senha em texto não criptografado em vez do comportamento padrão de armazenar um formato criptografado. |
| UserName | Especifica o nome de usuário para autenticar com o código-fonte. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |

> [!Note]
> Certifique-se de adicionar a senha dos fontes no mesmo contexto de usuário como o nuget.exe é usado posteriormente para acessar a origem do pacote. A senha será armazenada criptografado no arquivo de configuração e só pode ser descriptografada no mesmo contexto de usuário porque ele foi criptografado. Por exemplo, quando você usar um servidor de compilação para restaurar pacotes do NuGet que a senha deve ser criptografada com o mesmo usuário do Windows sob a qual a tarefa do servidor de compilação será executado.

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
