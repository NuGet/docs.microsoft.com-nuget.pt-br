---
title: Configurando feeds locais do NuGet
description: Como criar um feed local para pacotes do NuGet usando pastas em sua rede local
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 5d86657bdf26452d027593b953168e28694acf82
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818679"
---
# <a name="local-feeds"></a>Feeds locais

Feeds de pacote do NuGet locais são simplesmente estruturas de pasta hierárquicas em sua rede local (ou até mesmo seu próprio computador) em que os pacotes são colocados. Esses feeds podem ser usados como fontes de pacote com todas as outras operações do NuGet usando a CLI, a interface do usuário do Gerenciador de Pacotes e Console do Gerenciador de Pacotes.

Para habilitar a origem, adicione o nome do caminho (como `\\myserver\packages`) à lista de origens que usam a [Interface do usuário do Gerenciador de Pacotes](../tools/package-manager-ui.md#package-sources) ou o comando [`nuget sources`](../tools/cli-ref-sources.md).

> [!Note]
> Estruturas de pastas hierárquicas são compatíveis com o NuGet 3.3 ou superior. Versões mais antigas do NuGet usam apenas uma única pasta que contém pacotes, com a qual o desempenho é muito menor que a estrutura hierárquica.

## <a name="initializing-and-maintaining-hierarchical-folders"></a>Inicializando e mantendo pastas hierárquicas

A árvore hierárquica de pastas com controle de versão tem a seguinte estrutura geral:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

O NuGet cria essa estrutura automaticamente quando você usa o comando [`nuget add`](../tools/cli-ref-add.md) para copiar um pacote para o feed:

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

O comando `nuget add` funciona com um pacote ao mesmo tempo, o que pode ser inconveniente ao configurar um feed com vários pacotes.

Nesses casos, use o comando [`nuget init`](../tools/cli-ref-init.md) para copiar todos os pacotes em uma pasta para o feed como se você tivesse executado `nuget add` em cada um deles individualmente. Por exemplo, o comando a seguir copia todos os pacotes de `c:\packages` para uma árvore hierárquica em `\\myserver\packages`:

```cli
nuget init c:\packages \\myserver\packages
```

Assim como acontece com o comando `add`, `init` cria uma pasta para cada identificador de pacote, cada uma delas contendo uma pasta de número de versão, na qual está o pacote apropriado.
