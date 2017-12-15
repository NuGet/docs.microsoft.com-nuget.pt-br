---
title: "Notas de versão do NuGet 1.6 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ed433790-99bf-4b71-92a8-17314bd49867
description: "Notas de versão do NuGet 1.6 incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão 1.6 do NuGet, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7824d62cb73c54205175ec742cfc26d1ca3aa741
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
 # <a name="nuget-16-release-notes"></a>Notas de versão 1.6 do NuGet

[Notas de versão do NuGet 1.5](../release-notes/nuget-1.5.md) | [notas de versão 1.7 do NuGet](../release-notes/nuget-1.7.md)

1.6 NuGet foi lançado em 13 de dezembro de 2011.

## <a name="known-installation-issue"></a>Problema de instalação conhecidos
Se você estiver executando o VS 2010 SP1, você pode executar em um erro de instalação durante a tentativa de atualizar o NuGet se você tiver uma versão mais antiga.

A solução alternativa é simplesmente desinstalar NuGet e, em seguida, instalá-lo a partir da Galeria de extensão do VS.  Consulte [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) para obter mais informações.

Observação: Se o Visual Studio não permitirão que você desinstalar a extensão (o botão de desinstalação estiver desabilitado), em seguida, provavelmente você precisa reiniciar o Visual Studio usando "Executar como administrador".

## <a name="features"></a>Recursos

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>Suporte para controle de versão semântico e pacotes de pré-lançamento
NuGet 1.6 apresenta suporte para controle de versão semântico (SemVer). Para obter mais detalhes sobre como ele usa SemVer, leia o [documentação de controle de versão](../create-packages/prerelease-packages.md).

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>Usando o NuGet sem a verificação em pacotes (restauração do pacote)
1.6 NuGet agora tem suporte de primeira classe do fluxo de trabalho no qual NuGet pacotes não são adicionados ao controle de origem, mas em vez disso, são restaurados em tempo de compilação se ausente. Para obter mais detalhes, leia o [usando o NuGet sem confirmar pacotes ao controle de origem](../consume-packages/packages-and-source-control.md) tópico.

### <a name="item-templates-that-install-nuget-packages"></a>Modelos de item que instalam os pacotes NuGet
Aproveitando o trabalho para dar suporte ao pacote de NuGet pré-instalados para modelos de projeto do Visual Studio, o NuGet 1.6 também adiciona suporte para modelos de item do Visual Studio. Modelos de item podem ter associados a pacotes do NuGet que são instalados quando o modelo na chamada.

Para obter mais detalhes sobre como alterar um modelo de item do projeto para instalar os pacotes NuGet, leia o [pacotes em modelos do Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) tópico.

### <a name="support-for-disabling-package-sources"></a>Suporte para desabilitar origens do pacote
Quando várias fontes de pacote são configurados, NuGet aparecerá em cada uma para os pacotes durante a instalação de um pacote e suas dependências. Uma origem do pacote que está inativo por algum motivo severos lenta NuGet.

Antes de 1.6 NuGet, você pode remover a origem do pacote, mas, em seguida, você precisa se lembrar os detalhes para quando quiser adicioná-lo novamente.

1.6 NuGet permite desmarcar uma origem do pacote para desabilitá-lo, mas mantê-lo.

![Desabilitando um pacote](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Correções de Bug
1.6 NuGet tinha um total de 106 fixos de itens de trabalho. 95 deles foram classificados como bugs e 10 deles foram recursos.

Para obter uma lista completa de trabalho itens corrigidos no NuGet 1.6, por favor, exibição de [NuGet Issue Tracker para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
