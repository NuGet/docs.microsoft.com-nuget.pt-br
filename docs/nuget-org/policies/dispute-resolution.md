---
title: Solução de controvérsias de nome do pacote do NuGet
description: O processo para solucionar controvérsias entre publicadores de pacotes do NuGet relacionadas à identidade visual, marcas comerciais e outras situações de conflito.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: d9ed7de95a1f38ea2c288b28958519b1dff0e595
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775654"
---
# <a name="resolving-disputes-over-nuget-package-names"></a>Solucionar controvérsias sobre nomes de pacote do NuGet

Este artigo fornece um processo de resolução recomendado para membros da comunidade solucionarem controvérsias com outros editores do NuGet.

Por exemplo, suponha que a Northwind Traders cria um sistema CRM para o qual eles fornecem drivers de cliente como um MSI que pode ser baixado do site. Nancy, um desenvolvedor independente, quer facilitar o uso da biblioteca de cliente da Northwind e o transforma em um pacote do NuGet chamado `NorthwindTraders.Client`. Mais tarde, o Northwind deseja produzir um pacote do NuGet oficial próprio para sua biblioteca de cliente e, portanto, deseja contestar a propriedade da Nancy do nome do pacote.

Nesse cenário, Nancy parece não estar agindo de má fé, mas sim apoiando as ferramentas e clientes da Northwind ao contribuir seu próprio tempo e código. Por outro lado, a Northwind é a proprietária legítima do nome Northwind.

Seguindo o processo abaixo, a Northwind e a Nancy podem trabalhar juntas para alcançar uma resolução adequada, pois ambas estão interessadas em atender a comunidade de desenvolvedores. Normalmente não é necessário que a equipe do NuGet se envolva; a colaboração geralmente funciona melhor.

## <a name="process"></a>Processo

1. Entre em contato com os proprietários do pacote ao qual se refere a controvérsia, usando o link **Entrar em contato com os proprietários** na página de detalhes do pacote. Explique o problema de forma cordial e direta.
2. Envie uma cópia de sua mensagem para [support@nuget.org](mailto:support@nuget.org) que o NuGet e o .net Foundation estejam cientes de sua disputa.
3. Aguarde um máximo de 30 dias para uma resolução e, em seguida, notifique [support@nuget.org](mailto:support@nuget.org) novamente. A equipe de suporte do nuget.org será envolvida e tentará intermediar a controvérsia entre ambas as partes.
