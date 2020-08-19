---
title: Comando de fontes da CLI do NuGet
description: Referência para o comando nuget.exe sources
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 73c9cea8200a1ab1937d25a9a611ae7f2a943dba
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622584"
---
# <a name="sources-command-nuget-cli"></a>comando Sources (NuGet CLI)

**Aplica-se a:** consumo de pacote, &bullet; **versões com suporte para publicação:** todos

Gerencia a lista de fontes localizadas no arquivo de configuração de escopo do usuário ou um arquivo de configuração especificado. O arquivo de configuração de escopo do usuário está localizado em `%appdata%\NuGet\NuGet.Config` (Windows) e `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).

Observe que a URL de origem para nuget.org é `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Uso

```cli
nuget sources <operation> -Name <name> -Source <source>
```

em que `<operation>` é uma *lista, adicionar, remover, habilitar, desabilitar* ou *Atualizar*, `<name>` é o nome da origem e `<source>` é a URL da origem. Você pode operar em apenas uma fonte de cada vez.

## <a name="options"></a>Opções

- **`-ConfigFile`**

  O arquivo de configuração do NuGet a ser aplicado. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.

- **`-ForceEnglishOutput`**

  *(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.

- **`-Format`**

  Aplica-se à `list` ação e pode ser `Detailed` (o padrão) ou `Short` .

- **`-?|-help`**

  Exibe informações de ajuda para o comando.

- **`-Name`**

  Nome da origem.

- **`-NonInteractive`**

  Suprime prompts de entrada ou confirmações do usuário.

- **`-Password`**

  Especifica a senha para autenticação com a origem.

- **`-src|-Source`**

  Caminho para a origem de pacote (s).

- **`-StorePasswordInClearText`**

  Indica armazenar a senha em texto não criptografado em vez do comportamento padrão de armazenamento de um formulário criptografado.

- **`-UserName`**

  Especifica o nome de usuário para autenticação com a origem.

- **`-ValidAuthenticationTypes`**

  Lista separada por vírgulas de tipos de autenticação válidos para esta fonte. Por padrão, todos os tipos de autenticação são válidos. Exemplo: `basic,negotiate`.

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .

> [!Note]
> Certifique-se de adicionar a senha de origem no mesmo contexto de usuário que o nuget.exe é usado posteriormente para acessar a origem do pacote. A senha será armazenada criptografada no arquivo de configuração e só poderá ser descriptografada no mesmo contexto de usuário que foi criptografada. Por exemplo, quando você usa um servidor de compilação para restaurar os pacotes NuGet, a senha deve ser criptografada com o mesmo usuário do Windows no qual a tarefa do servidor de compilação será executada.

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
