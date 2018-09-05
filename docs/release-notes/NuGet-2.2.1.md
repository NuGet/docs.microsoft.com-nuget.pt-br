---
title: Notas de versão do NuGet 2.2.1
description: Notas de versão do NuGet 2.2.1 incluindo conhecidos problemas, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: abbd3a9d9c51132477ceb236fed22cb63ccda209
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550692"
---
# <a name="nuget-221-release-notes"></a>Notas de versão do NuGet 2.2.1

[Notas de versão do NuGet 2.2](../release-notes/nuget-2.2.md) | [notas de versão do NuGet 2.5](../release-notes/nuget-2.5.md)

O NuGet 2.2.1 foi lançado em 15 de fevereiro de 2013.  O número de versão da extensão do VS é 2.2.40116.9051.

## <a name="localization-refresh"></a>Atualização de localização
Quando o NuGet é fornecida como parte do Visual Studio 2012, ele foi totalmente localizado em inglês + 13 outros idiomas.  Desde então, ter enviado o NuGet 2.1 e 2.2, mas a localização não tinha sido atualizada.  A versão do NuGet 2.2.1 atualiza nossa localização.

Interface do usuário do NuGet e o Console do PowerShell são localizados para os seguintes idiomas:

1. Chinês (simplificado)
1. Chinês (tradicional)
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

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Modelos do Visual Studio dão suporte a vários repositórios de pacote pré-instalados
Se você gerar modelos do Visual Studio, você pode usar o NuGet para [pré-instalar pacotes](../visual-studio-extensibility/visual-studio-templates.md) como parte do modelo.  Até agora, esse recurso tinha uma limitação que todos os pacotes necessários para provenientes da mesma origem.  Com o NuGet 2.2.1, no entanto, você pode ter pacotes instalados de vários repositórios (dentro do modelo, um VSIX ou uma pasta no disco definido no registro).

O cenário principal para esse recurso é modelos de projeto personalizados do ASP.NET.  Os modelos internos do ASP.NET usam pacotes pré-instalados, receberão pacotes do disco local.  Agora você pode criar um modelo de projeto personalizado do ASP.NET que usa os pacotes existentes instalados pelo ASP.NET mas adicionar pacotes do NuGet extras ao seu modelo.

## <a name="bug-fixes"></a>Correções de Bug
O NuGet 2.2.1 inclui algumas correções de bugs de destino. Para obter uma lista de trabalho itens corrigidos no NuGet 2.2.1, por favor, modo de exibição de [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).


## <a name="known-issues"></a>Problemas Conhecidos

Se você estiver estendendo modelos de projeto do ASP.NET, todos os repositórios de pacote pré-instalado devem usar o mesmo valor para o `isPreunzipped` atributo.
