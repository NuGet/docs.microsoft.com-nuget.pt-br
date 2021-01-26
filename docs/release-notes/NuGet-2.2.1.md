---
title: Notas de versão do NuGet 2.2.1
description: Notas de versão do NuGet 2.2.1 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6058fd596e32d38042aa75027640a5e5baca472
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776805"
---
# <a name="nuget-221-release-notes"></a>Notas de versão do NuGet 2.2.1

Notas de versão do [NuGet 2,2](../release-notes/nuget-2.2.md)  |  [Notas de versão do NuGet 2,5](../release-notes/nuget-2.5.md)

O NuGet 2.2.1 foi lançado em 15 de fevereiro de 2013.  O número de versão da extensão VS é 2.2.40116.9051.

## <a name="localization-refresh"></a>Atualização de localização
Quando o NuGet é fornecido como parte do Visual Studio 2012, ele foi totalmente localizado em inglês + 13 outras linguagens.  Desde então, o NuGet 2,1 e o 2,2 foram enviados, mas a localização não tinha sido atualizada.  A versão 2.2.1 do NuGet atualiza nossa localização.

A interface do usuário do NuGet e o console do PowerShell estão localizados nos seguintes idiomas:

1. Chinês (Simplificado)
1. Chinês (Tradicional)
1. Tcheco
1. Inglês
1. Francês
1. Alemão
1. Italiano
1. Japonês
1. Coreano
1. Polonês
1. Português (Brasil)
1. Russo
1. Espanhol
1. Turco

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Os modelos do Visual Studio dão suporte a vários repositórios de pacotes pré-instalados
Se você produzir modelos do Visual Studio, poderá usar o NuGet para [pré-instalar pacotes](../visual-studio-extensibility/visual-studio-templates.md) como parte do modelo.  Até agora, esse recurso tinha uma limitação de que todos os pacotes precisavam vir da mesma origem.  No entanto, com o NuGet 2.2.1, você pode ter pacotes instalados de vários repositórios (dentro do modelo, um VSIX ou uma pasta no disco definida no registro).

O cenário principal para esse recurso são os modelos de projeto ASP.NET personalizados.  Os modelos internos do ASP.NET usam pacotes pré-instalados, obtendo pacotes do disco local.  Agora você pode criar um modelo de projeto ASP.NET personalizado que usa os pacotes existentes instalados pelo ASP.NET, mas adicionar pacotes NuGet extras ao seu modelo.

## <a name="bug-fixes"></a>Correções de bugs
O NuGet 2.2.1 inclui algumas correções de bugs direcionadas. Para obter uma lista de itens de trabalho corrigidos no NuGet 2.2.1, consulte o [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).


## <a name="known-issues"></a>Problemas conhecidos

Se você estiver estendendo modelos de projeto ASP.NET, todos os repositórios de pacote pré-instalados deverão usar o mesmo valor para o `isPreunzipped` atributo.
