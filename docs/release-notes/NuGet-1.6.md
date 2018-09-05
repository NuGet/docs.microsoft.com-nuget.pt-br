---
title: Notas de versão 1.6 do NuGet
description: Notas da versão 1.6 do NuGet incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 351303ca3ae27a37c19e59d84dfc9b4629fe0ca5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549006"
---
 # <a name="nuget-16-release-notes"></a>Notas de versão 1.6 do NuGet

[Notas de versão do NuGet 1.5](../release-notes/nuget-1.5.md) | [notas de versão do NuGet 1.7](../release-notes/nuget-1.7.md)

O NuGet 1.6 foi lançada em 13 de dezembro de 2011.

## <a name="known-installation-issue"></a>Problema de instalação conhecidos
Se você estiver executando o VS 2010 SP1, você pode executar em um erro de instalação quando tentar atualizar o NuGet se você tiver uma versão mais antiga instalada.

A solução alternativa é simplesmente desinstalar o NuGet e, em seguida, instalá-lo da Galeria de extensão do VS.  Veja [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) para obter mais informações.

Observação: Se o Visual Studio não permitirão que você desinstale a extensão (o botão Desinstalar está desabilitado), em seguida, é provável que você precisa reiniciar o Visual Studio usando "Executar como administrador".

## <a name="features"></a>Recursos

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>Suporte para controle de versão semântico e pacotes de pré-lançamento
O NuGet 1.6 apresenta suporte para controle de versão semântico (SemVer). Para obter mais detalhes sobre como ele usa o SemVer, leia as [documentação do controle de versão](../create-packages/prerelease-packages.md).

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>Usando o NuGet sem fazer check-In de pacotes (restauração de pacote)
O NuGet 1.6 agora tem suporte de primeira classe para o fluxo de trabalho no qual NuGet pacotes não são adicionados ao controle de origem, mas em vez disso, são restaurados no momento da compilação se estiverem ausentes. Para obter mais detalhes, leia as [usando o NuGet sem confirmar pacotes no controle do código-fonte](../consume-packages/packages-and-source-control.md) tópico.

### <a name="item-templates-that-install-nuget-packages"></a>Modelos de item que instalar os pacotes NuGet
Criando o trabalho para dar suporte ao pacote do NuGet pré-instalado para modelos de projeto do Visual Studio, 1.6 do NuGet também adiciona suporte para modelos de item do Visual Studio. Modelos de item podem ter associadas a pacotes do NuGet que são instalados quando o modelo no invocado.

Para obter mais detalhes sobre como alterar um modelo de projeto/item para instalar pacotes do NuGet, leia as [pacotes em modelos do Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) tópico.

### <a name="support-for-disabling-package-sources"></a>Suporte para desabilitar origens de pacote
Quando várias origens de pacote são configuradas, NuGet examinará cada um para pacotes durante a instalação de um pacote e suas dependências. Uma origem de pacote que está inativo por algum motivo gravemente lenta NuGet.

Antes do NuGet 1.6, você pode remover a origem do pacote, mas, em seguida, você precisa se lembrar os detalhes para quando você quiser adicioná-lo de volta.

O NuGet 1.6 permite desmarcando uma origem de pacote para desabilitá-lo, mas mantê-lo.

![Desabilitando um pacote](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Correções de Bug
O NuGet 1.6 tinha um total de 106 fixos de itens de trabalho. 95 deles foram classificados como bugs e foram de 10 desses recursos.

Para obter uma lista completa de trabalho itens corrigidos no NuGet 1.6, por favor, modo de exibição de [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
