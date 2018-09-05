---
title: Notas de versão do NuGet 2.8.1
description: Notas de versão do NuGet 2.8.1 incluindo conhecidos problemas, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39fb7db00e18e32eef15adc11764a122c97ddfd5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545233"
---
# <a name="nuget-281-release-notes"></a>Notas de versão do NuGet 2.8.1

[Notas de versão do NuGet 2.8](../release-notes/nuget-2.8.md) | [notas de versão do NuGet 2.8.2](../release-notes/nuget-2.8.2.md)

O NuGet 2.8.1 foi lançado em 2 de abril de 2014.

## <a name="notable-features-in-the-release"></a>Recursos importantes da versão

### <a name="support-for-windows-phone-81-projects"></a>Suporte para projetos do Windows Phone 8.1
Esta versão agora dá suporte os monikers de estrutura de destino de novo seguir que podem ser usadas para projetos de destino Windows Phone 8.1:

* WindowsPhone81 / WP81 (para projetos baseados em Silverlight do Windows Phone)
* WindowsPhoneApp81 / WPA81 (para projetos do WinRT com base no aplicativo do Windows Phone)

### <a name="update-of-the-nuget-webmatrix-extension"></a>Atualização da extensão do WebMatrix NuGet
Esta versão atualiza o cliente do NuGet encontrado em WebMatrix para [NuGet. Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 e traz com recursos como transformações XDT. Mais importante, o 2.6.1 atualização core permite que o cliente do WebMatrix instalar os pacotes do NuGet que contêm as versões mais recentes do `.nuspec` esquema, que inclui os pacotes do NuGet do ASP.NET.

Para obter mais informações sobre a atualização de extensão do WebMatrix, vê-los específico [notas de versão](../release-notes/nuget-2.6.1-for-WebMatrix.md).

### <a name="bug-fixes"></a>Correções de Bug
Além desses recursos, esta versão do NuGet inclui outras correções de bug. Havia um total de 16 problemas abordados na versão. Para obter uma lista completa de trabalho itens corrigidos no NuGet 2.8.1, por favor, modo de exibição de [rastreador de problemas do NuGet para esta versão](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).

### <a name="reshipping-with-visual-studio-14-ctp"></a>São distribuídos com o Visual Studio "14" CTP
No CTP do Visual Studio "14" lançado em 3 de junho de 2014, o NuGet 2.8.1 é fornecido na caixa. Os recursos que ele dá suporte a permanecem no mesmo nível com outros 2.8.1 VSIXes como o existente para o Visual Studio 2013.
