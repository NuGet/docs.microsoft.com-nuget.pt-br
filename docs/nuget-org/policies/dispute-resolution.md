---
title: Solução de controvérsias de nome do pacote do NuGet
description: O processo para solucionar controvérsias entre publicadores de pacotes do NuGet relacionadas à identidade visual, marcas comerciais e outras situações de conflito.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: a2f1fed578f1635296892ab925219f0f27883c02
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "67426931"
---
# <a name="resolving-disputes-over-nuget-package-names"></a>Solucionar controvérsias sobre nomes de pacote do NuGet

Este artigo fornece um processo de resolução recomendado para membros da comunidade solucionarem controvérsias com outros editores do NuGet.

Por exemplo, suponha que a Northwind Traders cria um sistema CRM para o qual eles fornecem drivers de cliente como um MSI que pode ser baixado do site. Nancy, um desenvolvedor independente, quer facilitar o uso da biblioteca de cliente da Northwind e o transforma em um pacote do NuGet chamado `NorthwindTraders.Client`. Mais tarde, o Northwind deseja produzir um pacote do NuGet oficial próprio para sua biblioteca de cliente e, portanto, deseja contestar a propriedade da Nancy do nome do pacote.

Nesse cenário, Nancy parece não estar agindo de má fé, mas sim apoiando as ferramentas e clientes da Northwind ao contribuir seu próprio tempo e código. Por outro lado, a Northwind é a proprietária legítima do nome Northwind.

Seguindo o processo abaixo, a Northwind e a Nancy podem trabalhar juntas para alcançar uma resolução adequada, pois ambas estão interessadas em atender a comunidade de desenvolvedores. Normalmente não é necessário que a equipe do NuGet se envolva; a colaboração geralmente funciona melhor. Na verdade, todas as controvérsias levada para a equipe do NuGet até hoje foram solucionadas sem a necessidade de julgamento direto por parte da equipe.

## <a name="process"></a>Processo

1. Entre em contato com os proprietários do pacote ao qual se refere a controvérsia, usando o link **Entrar em contato com os proprietários** na página de detalhes do pacote. Explique o problema de forma cordial e direta.
2. Envie uma cópia de [support@nuget.org](mailto:support@nuget.org) sua mensagem para que a NuGet e a Fundação .NET estejam cientes de sua disputa.
3. Aguarde no máximo 30 dias [support@nuget.org](mailto:support@nuget.org) para uma resolução e notifique novamente. A equipe de suporte do nuget.org será envolvida e tentará intermediar a controvérsia entre ambas as partes.
