---
title: "Solução de controvérsias no nome do pacote NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "O processo para solucionar controvérsias entre publicadores de pacotes do NuGet relacionadas à identidade visual, marcas comerciais e outras situações de conflito."
keywords: "Controvérsias de pacote do NuGet, solução de controvérsias do NuGet, processo de solução de controvérsias"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 589fe4e7d2b05f3d589dcc70e78e7199d7e717c8
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
---
# <a name="resolving-disputes-over-nuget-package-names"></a>Solucionar controvérsias sobre nomes de pacote do NuGet

Este artigo fornece um processo de resolução recomendado para membros da comunidade solucionarem controvérsias com outros editores do NuGet.

Por exemplo, suponha que a Northwind Traders cria um sistema CRM para o qual eles fornecem drivers de cliente como um MSI que pode ser baixado do site. Nancy, um desenvolvedor independente, quer facilitar o uso da biblioteca de cliente da Northwind e o transforma em um pacote do NuGet chamado `NorthwindTraders.Client`. Mais tarde, o Northwind deseja produzir um pacote do NuGet oficial próprio para sua biblioteca de cliente e, portanto, deseja contestar a propriedade da Nancy do nome do pacote.

Nesse cenário, Nancy parece não estar agindo de má fé, mas sim apoiando as ferramentas e clientes da Northwind ao contribuir seu próprio tempo e código. Por outro lado, a Northwind é a proprietária legítima do nome Northwind.

Seguindo o processo abaixo, a Northwind e a Nancy podem trabalhar juntas para alcançar uma resolução adequada, pois ambas estão interessadas em atender a comunidade de desenvolvedores. Normalmente não é necessário que a equipe do NuGet se envolva; a colaboração geralmente funciona melhor. Na verdade, todas as controvérsias levada para a equipe do NuGet até hoje foram solucionadas sem a necessidade de julgamento direto por parte da equipe.

## <a name="process"></a>Processo

1. Entre em contato com os proprietários do pacote que você está contestando usando o link **Contatar os Proprietários** na página de detalhes do pacote. Explique seu problema de forma gentil e direta.
1. Envie uma cópia da sua mensagem para [support@nuget.org](mailto:support@nuget.org) para que o NuGet e a .NET Foundation estejam cientes da sua controvérsia.
1. Aguarde um máximo de 30 dias por uma solução e notifique [support@nuget.org](mailto:support@nuget.org) novamente. A equipe de suporte do nuget.org será envolvida e tentará intermediar a controvérsia entre ambas as partes.
