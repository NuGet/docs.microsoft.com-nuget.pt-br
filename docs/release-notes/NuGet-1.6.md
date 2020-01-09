---
title: Notas de versão do NuGet 1,6
description: Notas de versão do NuGet 1,6 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2878d3809b2be4fb71f4e7b1a1e08e405ead44b9
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384131"
---
 # <a name="nuget-16-release-notes"></a>Notas de versão do NuGet 1,6

[Notas de versão do nuget 1,5](../release-notes/nuget-1.5.md) | [notas de versão do NuGet 1,7](../release-notes/nuget-1.7.md)

O NuGet 1,6 foi lançado em 13 de dezembro de 2011.

## <a name="known-installation-issue"></a>Problema de instalação conhecido
Se você estiver executando o VS 2010 SP1, poderá encontrar um erro de instalação ao tentar atualizar o NuGet se tiver uma versão mais antiga instalada.

A solução alternativa é simplesmente desinstalar o NuGet e, em seguida, instalá-lo a partir da Galeria de extensões do VS.  Consulte <https://support.microsoft.com/kb/2581019> para obter mais informações.

Observação: se o Visual Studio não permitir que você desinstale a extensão (o botão desinstalar está desabilitado), provavelmente, você precisará reiniciar o Visual Studio usando "executar como administrador".

## <a name="features"></a>Recursos

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>Suporte para versão semântica e pacotes de pré-lançamento
O NuGet 1,6 apresenta suporte para o controle de versão semântico (SemVer). Para obter mais detalhes sobre como ele usa o SemVer, leia a [documentação de controle de versão](../create-packages/prerelease-packages.md).

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>Usando o NuGet sem fazer check-in de pacotes (restauração de pacote)
O NuGet 1,6 agora tem suporte de primeira classe para o fluxo de trabalho no qual os pacotes NuGet não são adicionados ao controle do código-fonte, mas, em vez disso, são restaurados no momento da compilação, se ausente. Para obter mais detalhes, leia o tópico [usando o NuGet sem confirmar pacotes no controle do código-fonte](../consume-packages/packages-and-source-control.md) .

### <a name="item-templates-that-install-nuget-packages"></a>Modelos de item que instalam pacotes NuGet
Com base no trabalho para dar suporte ao pacote do NuGet pré-instalado para modelos de projeto do Visual Studio, o NuGet 1,6 também adiciona suporte para modelos de item do Visual Studio. Os modelos de item podem ter pacotes NuGet associados que são instalados quando o modelo é chamado.

Para obter mais detalhes sobre como alterar um modelo de projeto/item para instalar pacotes NuGet, leia o tópico [pacotes no Visual Studio modelos](../visual-studio-extensibility/visual-studio-templates.md) .

### <a name="support-for-disabling-package-sources"></a>Suporte para desabilitar as origens do pacote
Quando várias fontes de pacote são configuradas, o NuGet examinará cada uma para pacotes durante a instalação de um pacote e suas dependências. Uma origem de pacote que está inoperante por algum motivo pode retardar seriamente o NuGet.

Antes do NuGet 1,6, você pode remover a origem do pacote, mas, em seguida, você precisa se lembrar dos detalhes de quando deseja adicioná-lo novamente.

O NuGet 1,6 permite desmarcar uma origem de pacote para desabilitá-la, mas mantê-la.

![Desabilitando um pacote](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Correções de Bug
O NuGet 1,6 tinha um total de 106 itens de trabalho corrigidos. 95 daqueles foram classificados como bugs e 10 desses eram recursos.

Para obter uma lista completa de itens de trabalho corrigidos no NuGet 1,6, consulte o [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
