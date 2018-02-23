---
title: NuGet CLI fontes comando | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referência para o nuget.exe fontes de comando"
keywords: "NuGet fontes de referência, fontes de comando"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 1e8204f5e1bf712f65d8efb14ca2a4bd802e3f90
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/20/2018
---
# <a name="sources-command-nuget-cli"></a>comando de fontes (NuGet CLI)

**Aplica-se a:** consumo de pacote, a publicação &bullet; **versões com suporte:** todos

Gerencia a lista de fontes localizado no arquivo de configuração de escopo de usuário ou um arquivo de configuração especificado. O arquivo de configuração de escopo do usuário está localizado em `%APPDATA%\NuGet\NuGet.Config` no Windows e em `~/.nuget/NuGet.Config` no Mac/Linux.


Observe que a URL de origem para nuget.org é `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Uso

```cli
nuget sources <operation> -Name <name> -Source <source>
```

onde `<operation>` é um dos *lista, adicionar, remover, habilitar, desabilitar,* ou *atualização*, `<name>` é o nome da fonte, e `<source>` é a URL da fonte.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ConfigFile | O arquivo de configuração do NuGet para aplicar. Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado. |
| ForceEnglishOutput | *(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Formatar | Aplica-se para o `list` ação e pode ser `Detailed` (o padrão) ou `Short`. |
| Ajuda | Exibe informações de ajuda para o comando. |
| NonInteractive | Suprime avisos para a entrada do usuário ou confirmações. |
| Senha | Especifica a senha para autenticar com o código-fonte. |
| StorePasswordInClearText | Indica para armazenar a senha em texto não criptografado em vez do comportamento padrão de armazenar um formato criptografado. |
| UserName | Especifica o nome de usuário para autenticar com o código-fonte. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |

> [!Note]
> Certifique-se de Adicionar senha as fontes no mesmo contexto de usuário, como o nuget.exe mais tarde é usada para acessar a origem do pacote. A senha será armazenada criptografado no arquivo de configuração e só pode ser descriptografada no mesmo contexto de usuário, como ele foi criptografado. Assim, por exemplo quando você usar um servidor de compilação para restaurar os pacotes do NuGet que a senha deve ser criptografada com o mesmo usuário do Windows sob a qual a tarefa do servidor de compilação será executado.

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
