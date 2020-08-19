---
title: Comando Push da CLI do NuGet
description: Referência para o comando nuget.exe push
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d53a2e7f41219e68e59b195d1d5a9d1f62ad7c63
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622838"
---
# <a name="push-command-nuget-cli"></a>comando push (NuGet CLI)

**Aplica-se a:** &bullet; **versões com suporte** para publicação de pacotes: tudo; 4.1.0 + obrigatório para NuGet.org

> [!Important]
> Para enviar pacotes por push para o nuget.org, você deve usar nuget.exe v 4.1.0 +, que implementa os [protocolos do NuGet](../../api/nuget-protocols.md)necessários.

Envia por push um pacote para uma origem de pacote e o publica.

A configuração padrão do NuGet é obtida carregando `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) e, em seguida, carregando qualquer `Nuget.Config` `.nuget\Nuget.Config` arquivo ou iniciando da raiz da unidade e terminando no diretório atual (consulte [configurações comuns do NuGet](../../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Uso

```cli
nuget push <packagePath> [options]
```

onde `<packagePath>` o identifica o pacote a ser enviado por push para o servidor.

## <a name="options"></a>Opções

- **`-ApiKey`**

  A chave de API para o repositório de destino. Se não estiver presente, o especificado no arquivo de configuração será usado.

- **`-ConfigFile`**

  O arquivo de configuração do NuGet a ser aplicado. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.

- **`-DisableBuffering`**

  Desabilita o armazenamento em buffer ao enviar por push para um servidor HTTP (s) para diminuir os usos de memória. Cuidado: quando essa opção é usada, a autenticação integrada do Windows pode não funcionar.

- **`-ForceEnglishOutput`**

  *(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.

- **`-?|-help`**

  Exibe informações de ajuda para o comando.

- **`-NonInteractive`**

  Suprime prompts de entrada ou confirmações do usuário.

- **`-NoServiceEndpoint`**

  Não acrescenta `api/v2/packages` à URL de origem.

- **`-NoSymbols`**

  *(3,5 +)* Se existir um pacote de símbolos, ele não será enviado por push para um servidor de símbolos.

- **`-src|-Source`**

  Especifica a URL do servidor. O NuGet identifica uma origem UNC ou de pasta local e simplesmente copia o arquivo em vez de enviá-lo por push usando HTTP.  Além disso, começando com o NuGet 3.4.2, esse é um parâmetro obrigatório, a menos que o `NuGet.Config` arquivo especifique um valor *defaultpushe* (consulte [Configurando o comportamento do NuGet](../../consume-packages/configuring-nuget-behavior.md)).

- **`-SkipDuplicate`**

  *(5.1 +)* Se já existir um pacote e uma versão, pule-o e continue com o próximo pacote no envio por push, se houver.

- **`-SymbolSource`**

  *(3,5 +)* Especifica a URL do servidor de símbolos; nuget.smbsrc.net é usado ao enviar para nuget.org

- **`-SymbolApiKey`**

  *(3,5 +)* Especifica a chave de API para a URL especificada em `-SymbolSource` .

- **`-Timeout`**

  Especifica o tempo limite, em segundos, para envio por push para um servidor.  O padrão é 300 segundos (5 minutos).

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .


Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```
