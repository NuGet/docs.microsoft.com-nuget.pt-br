---
title: Comando de fontes da CLI do NuGet
description: Referência para o comando de origens do NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327593"
---
# <a name="sources-command-nuget-cli"></a>Commando sources (NuGet CLI)

**Aplica-se a:** consumo de &bullet; pacote, **versões com suporte para publicação:** todos

Gerencia a lista de fontes localizadas no arquivo de configuração de escopo do usuário ou um arquivo de configuração especificado. O arquivo de configuração de escopo do usuário `%appdata%\NuGet\NuGet.Config` está localizado em ( `~/.nuget/NuGet/NuGet.Config` Windows) e (Mac/Linux).

Observe que a URL de origem para nuget.org é `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Uso

```cli
nuget sources <operation> -Name <name> -Source <source>
```

em `<operation>` que é uma *lista, adicionar, remover, habilitar, desabilitar* ou *Atualizar*, `<name>` é o nome da origem e `<source>` é a URL da origem. Você pode operar em apenas uma fonte de cada vez.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ConfigFile | O arquivo de configuração do NuGet a ser aplicado. Se não for especificado `%AppData%\NuGet\NuGet.Config` , (Windows) `~/.nuget/NuGet/NuGet.Config` ou (Mac/Linux) será usado.|
| ForceEnglishOutput | *(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês. |
| Formatar | Aplica-se `list` à ação e pode `Detailed` ser (o padrão) `Short`ou. |
| Ajuda | Exibe informações de ajuda para o comando. |
| NonInteractive | Suprime prompts de entrada ou confirmações do usuário. |
| Senha | Especifica a senha para autenticação com a origem. |
| StorePasswordInClearText | Indica armazenar a senha em texto não criptografado em vez do comportamento padrão de armazenamento de um formulário criptografado. |
| UserName | Especifica o nome de usuário para autenticação com a origem. |
| Verbosity | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*. |

> [!Note]
> Certifique-se de adicionar a senha de origem no mesmo contexto de usuário que o NuGet. exe é usado posteriormente para acessar a origem do pacote. A senha será armazenada criptografada no arquivo de configuração e só poderá ser descriptografada no mesmo contexto de usuário que foi criptografada. Por exemplo, quando você usa um servidor de compilação para restaurar os pacotes NuGet, a senha deve ser criptografada com o mesmo usuário do Windows no qual a tarefa do servidor de compilação será executada.

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
