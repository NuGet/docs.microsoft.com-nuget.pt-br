---
title: Notas de versão do NuGet 2.8.1
description: Notas de versão do NuGet 2.8.1 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4dcd8ab140026c39345f850ac00a7a5f26a0e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776770"
---
# <a name="nuget-281-release-notes"></a>Notas de versão do NuGet 2.8.1

Notas de versão do [NuGet 2,8](../release-notes/nuget-2.8.md)  |  [Notas de versão do NuGet 2.8.2](../release-notes/nuget-2.8.2.md)

O NuGet 2.8.1 foi lançado em 2 de abril de 2014.

## <a name="notable-features-in-the-release"></a>Recursos notáveis na versão

### <a name="support-for-windows-phone-81-projects"></a>Suporte para projetos Windows Phone 8,1
Esta versão agora dá suporte aos seguintes novos monikers da estrutura de destino que podem ser usados para direcionar Windows Phone projetos 8,1:

* WindowsPhone81/WP81 (para projetos Windows Phone baseados no Silverlight)
* WindowsPhoneApp81/WPA81 (para projetos de aplicativo Windows Phone baseados em WinRT)

### <a name="update-of-the-nuget-webmatrix-extension"></a>Atualização da extensão do WebMatrix do NuGet
Esta versão atualiza o cliente NuGet encontrado no WebMatrix para [NuGet. Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 e traz recursos de ti, como transformações de xdt. O mais importante é que a atualização do 2.6.1 Core permite que o cliente do WebMatrix instale pacotes NuGet que contêm versões mais recentes do `.nuspec` esquema, que inclui os pacotes NuGet do ASP.net.

Para obter mais informações sobre a atualização de extensão do WebMatrix, consulte as [notas de versão](../release-notes/nuget-2.6.1-for-WebMatrix.md)específicas.

### <a name="bug-fixes"></a>Correções de bugs
Além desses recursos, esta versão do NuGet inclui outras correções de bugs. Houve 16 problemas totais abordados na versão. Para obter uma lista completa dos itens de trabalho corrigidos no NuGet 2.8.1, consulte o [rastreador de problemas do NuGet para esta versão](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).

### <a name="reshipping-with-visual-studio-14-ctp"></a>Reentregando com o Visual Studio "14" CTP
No Visual Studio "14" CTP lançado em 3 de junho de 2014, o NuGet 2.8.1 é fornecido na caixa. Os recursos para os quais ele dá suporte permanecem em conta com outros VSIXs 2.8.1, como aquele para Visual Studio 2013.
