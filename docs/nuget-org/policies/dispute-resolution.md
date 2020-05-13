---
title: Solução de controvérsias de nome do pacote do NuGet
description: O processo para solucionar controvérsias entre publicadores de pacotes do NuGet relacionadas à identidade visual, marcas comerciais e outras situações de conflito.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 7e725d8114cde3de189dc3a648bc5a6c0b0e785b
ms.sourcegitcommit: 0a63956bf12aaf1b1b45e680bc8e90f97347988c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/13/2020
ms.locfileid: "83367941"
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
