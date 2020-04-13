---
title: Configurando feeds locais do NuGet
description: Como criar um feed local para pacotes do NuGet usando pastas em sua rede local
author: karann-msft
ms.author: karann
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 42a5c30c058a9efb35338c1b484235b6ad111bd0
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "68317587"
---
# <a name="local-feeds"></a>Feeds locais

Feeds de pacote do NuGet locais são simplesmente estruturas de pasta hierárquicas em sua rede local (ou até mesmo seu próprio computador) em que os pacotes são colocados. Esses feeds podem ser usados como fontes de pacote com todas as outras operações do NuGet usando a CLI, a interface do usuário do Gerenciador de Pacotes e Console do Gerenciador de Pacotes.

Para habilitar a origem, adicione o nome do caminho (como `\\myserver\packages`) à lista de origens que usam a [Interface do usuário do Gerenciador de Pacotes](../consume-packages/install-use-packages-visual-studio.md#package-sources) ou o comando [`nuget sources`](../reference/cli-reference/cli-ref-sources.md).

> [!Note]
> Estruturas de pastas hierárquicas são compatíveis com o NuGet 3.3 ou superior. Versões mais antigas do NuGet usam apenas uma única pasta que contém pacotes, com a qual o desempenho é muito menor que a estrutura hierárquica.

## <a name="initializing-and-maintaining-hierarchical-folders"></a>Inicializando e mantendo pastas hierárquicas

A árvore hierárquica de pastas com controle de versão tem a seguinte estrutura geral:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

NuGet cria essa estrutura automaticamente [`nuget add`](../reference/cli-reference/cli-ref-add.md) quando você usa o comando para copiar um pacote para o feed:

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

O comando `nuget add` funciona com um pacote ao mesmo tempo, o que pode ser inconveniente ao configurar um feed com vários pacotes.

Nesses casos, use [`nuget init`](../reference/cli-reference/cli-ref-init.md) o comando para copiar todos os pacotes `nuget add` em uma pasta para o feed como se você fosse usado em cada um individualmente. Por exemplo, o comando a seguir copia todos os pacotes de `c:\packages` para uma árvore hierárquica em `\\myserver\packages`:

```cli
nuget init c:\packages \\myserver\packages
```

Assim como acontece com o comando `add`, `init` cria uma pasta para cada identificador de pacote, cada uma delas contendo uma pasta de número de versão, na qual está o pacote apropriado.
