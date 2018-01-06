---
title: "Notas de versão do NuGet 2.2 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 25389d8c-e7db-4920-ab5e-cff20cebee7e
description: "Notas de versão do NuGet 2.2 incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão 2.2 do NuGet, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 1f6080e01777431c4dfb2278db167bd3bc9a67ea
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-22-release-notes"></a>Notas de versão 2.2 do NuGet

[Notas de versão do NuGet 2.1](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 notas de versão](../release-notes/nuget-2.2.1.md)

NuGet 2.2 foi lançado em 12 de dezembro de 2012.

## <a name="visual-studio-quick-launch"></a>Início rápido do Visual Studio
Um dos novos recursos que foi adicionado no Visual Studio 2012 foi o [caixa de diálogo de início rápido](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box). 2.2 NuGet estende essa caixa de diálogo que lhe permite inicializar a caixa de diálogo de Gerenciador de pacote com os termos de pesquisa inseridos no início rápido. Por exemplo, inserir 'jquery' no início rápido agora inclui uma opção nos resultados para pesquisar pacotes do NuGet correspondência 'jquery'.

![NuGet em início rápido do Visual Studio](./media/quick-launch.png)

Esta opção iniciará a padrão NuGet pacote manager experiência de pesquisa para o termo 'jquery'.

![Caixa de diálogo preenchido previamente o NuGet Package Manager](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>Especifique a pasta inteira para o conteúdo do pacote
2.2 NuGet agora permite que você especifique uma pasta inteira no `<file>` elemento o `.nuspec` arquivo para incluir todo o conteúdo dessa pasta. Por exemplo, a seguir fará com que todos os scripts na pasta de scripts do pacote a ser adicionado à pasta contents\scripts quando o pacote for instalado em um projeto.

```xml
<file src="scripts\" target="content\scripts"/>
```

**Atualizar 24/6/16: pastas vazias na pasta "conteúdo" serão ignoradas durante a instalação do pacote.**

## <a name="known-issues"></a>Problemas Conhecidos

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>Falha da instalação do pacote para projetos F # ao usar o console do Gerenciador de pacote
Ao tentar instalar um pacote do NuGet para um projeto do F # usando o console do Gerenciador de pacote, um InvalidOperationException é gerado. Estamos trabalhando ativamente com a equipe do F # para resolver o problema, mas por enquanto, a solução alternativa é instalar os pacotes do NuGet em F # projetos por meio da caixa de diálogo de Gerenciador de pacote do NuGet em vez do console. [Mais informações estão disponíveis no CodePlex](http://nuget.codeplex.com/workitem/2873).


## <a name="bug-fixes"></a>Correções de Bug
NuGet 2.2 inclui muitas correções de bugs. Para obter uma lista completa de trabalho itens corrigidos no NuGet 2.2, por favor, exibição de [NuGet Issue Tracker para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
