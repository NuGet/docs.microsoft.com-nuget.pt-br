---
title: Notas de versão do NuGet 2,2
description: Notas de versão do NuGet 2,2 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cc81d0ff53a5e8ac8b632a08c3cfe0b8b59c9bd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780433"
---
# <a name="nuget-22-release-notes"></a>Notas de versão do NuGet 2,2

Notas de versão do [NuGet 2,1](../release-notes/nuget-2.1.md)  |  [Notas de versão do NuGet 2.2.1](../release-notes/nuget-2.2.1.md)

O NuGet 2,2 foi lançado em 12 de dezembro de 2012.

## <a name="visual-studio-quick-launch"></a>Início rápido do Visual Studio
Um dos novos recursos que foi adicionado no Visual Studio 2012 foi a [caixa de diálogo início rápido](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box). O NuGet 2,2 estende essa caixa de diálogo, permitindo que ela inicialize a caixa de diálogo do Gerenciador de pacotes com os termos de pesquisa inseridos no início rápido. Por exemplo, inserir "jQuery" no início rápido agora inclui uma opção nos resultados para pesquisar os pacotes NuGet que correspondem a "jQuery".

![Início rápido do NuGet no Visual Studio](./media/quick-launch.png)

A seleção dessa opção iniciará a experiência de pesquisa padrão do Gerenciador de pacotes do NuGet para o termo ' jQuery '.

![Caixa de diálogo do Gerenciador de pacotes do NuGet preenchida previamente](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>Especificar a pasta inteira para o conteúdo do pacote
O NuGet 2,2 agora permite que você especifique uma pasta inteira no `<file>` elemento do `.nuspec` arquivo para incluir todo o conteúdo dessa pasta. Por exemplo, o seguinte fará com que todos os scripts na pasta de scripts do pacote sejam adicionados à pasta contents\scripts quando o pacote for instalado em um projeto.

```xml
<file src="scripts\" target="content\scripts"/>
```

**Atualização 6/24/16: as pastas vazias na pasta "conteúdo" são ignoradas durante a instalação do pacote.**

## <a name="known-issues"></a>Problemas conhecidos

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>Falha na instalação do pacote para projetos F # ao usar o console do Gerenciador de pacotes
Ao tentar instalar um pacote NuGet em um projeto F # usando o console do Gerenciador de pacotes, um InvalidOperationException é gerado. Estamos trabalhando ativamente com a equipe do F # para resolver o problema, mas enquanto isso, a solução alternativa é instalar pacotes NuGet em projetos F # por meio da caixa de diálogo Gerenciador de pacotes do NuGet, em vez do console. [Mais informações estão disponíveis no CodePlex](http://nuget.codeplex.com/workitem/2873).


## <a name="bug-fixes"></a>Correções de bugs
O NuGet 2,2 inclui muitas correções de bugs. Para obter uma lista completa de itens de trabalho corrigidos no NuGet 2,2, consulte o [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
