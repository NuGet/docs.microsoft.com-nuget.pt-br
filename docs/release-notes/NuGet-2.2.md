---
title: Notas de versão 2.2 do NuGet
description: Notas de versão para 2.2 de NuGet, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a968ced3c58b7187a8bd9a8b14baa92f61f0140f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545986"
---
# <a name="nuget-22-release-notes"></a>Notas de versão 2.2 do NuGet

[Notas de versão do NuGet 2.1](../release-notes/nuget-2.1.md) | [notas de versão do NuGet 2.2.1](../release-notes/nuget-2.2.1.md)

NuGet 2.2 foi lançado em 12 de dezembro de 2012.

## <a name="visual-studio-quick-launch"></a>Início rápido do Visual Studio
Um dos novos recursos que foi adicionado no Visual Studio 2012 foi a [caixa de diálogo de início rápido](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box). 2.2 NuGet estende essa caixa de diálogo, permitindo que ele inicializar a caixa de diálogo do Gerenciador de pacote com os termos de pesquisa inseridos no início rápido. Por exemplo, inserir 'jquery' no início rápido agora inclui uma opção nos resultados para pesquisar pacotes do NuGet 'jquery' de correspondência.

![NuGet no início rápido do Visual Studio](./media/quick-launch.png)

Selecionar esta opção iniciará a standard NuGet pacote manager experiência de pesquisa para o termo 'jquery'.

![Caixa de diálogo de Gerenciador de pacotes NuGet previamente preenchido](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>Especifique a pasta inteira para o conteúdo do pacote
2.2 NuGet agora permite que você especifique uma pasta inteira na `<file>` elemento do `.nuspec` arquivo para incluir todo o conteúdo dessa pasta. Por exemplo, a seguir fará com que todos os scripts na pasta de scripts do pacote a ser adicionado à pasta contents\scripts quando o pacote é instalado em um projeto.

```xml
<file src="scripts\" target="content\scripts"/>
```

**Atualizar 6/24/16: pastas vazias na pasta "content" são ignoradas quando a instalação do pacote.**

## <a name="known-issues"></a>Problemas Conhecidos

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>Falha da instalação do pacote para projetos do F # ao usar o console do Gerenciador de pacotes
Ao tentar instalar um pacote do NuGet em um projeto do F # usando o console do Gerenciador de pacotes, será gerada uma InvalidOperationException. Estamos trabalhando ativamente com a equipe do F # para resolver o problema, mas por enquanto, a solução alternativa é instalar os pacotes NuGet em projetos do F # por meio da caixa de diálogo de Gerenciador de pacote do NuGet em vez do console. [Mais informações estão disponíveis no CodePlex](http://nuget.codeplex.com/workitem/2873).


## <a name="bug-fixes"></a>Correções de Bug
NuGet 2.2 inclui muitas correções de bugs. Para obter uma lista completa de trabalho itens corrigidos no NuGet 2.2, por favor, modo de exibição de [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
