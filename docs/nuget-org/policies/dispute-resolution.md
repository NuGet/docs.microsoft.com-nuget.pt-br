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
# <a name="resolving-disputes-over-nuget-package-names"></a><span data-ttu-id="39f2c-103">Solucionar controvérsias sobre nomes de pacote do NuGet</span><span class="sxs-lookup"><span data-stu-id="39f2c-103">Resolving disputes over NuGet package names</span></span>

<span data-ttu-id="39f2c-104">Este artigo fornece um processo de resolução recomendado para membros da comunidade solucionarem controvérsias com outros editores do NuGet.</span><span class="sxs-lookup"><span data-stu-id="39f2c-104">This article provides a recommended resolution process for community members to resolve disputes with other NuGet publishers.</span></span>

<span data-ttu-id="39f2c-105">Por exemplo, suponha que a Northwind Traders cria um sistema CRM para o qual eles fornecem drivers de cliente como um MSI que pode ser baixado do site.</span><span class="sxs-lookup"><span data-stu-id="39f2c-105">For example, suppose that Northwind Traders makes a CRM system for which they provide client drivers as a downloadable MSI from their website.</span></span> <span data-ttu-id="39f2c-106">Nancy, um desenvolvedor independente, quer facilitar o uso da biblioteca de cliente da Northwind e o transforma em um pacote do NuGet chamado `NorthwindTraders.Client`.</span><span class="sxs-lookup"><span data-stu-id="39f2c-106">Nancy, an independent developer, wants to make it easier to use Northwind's client library, and turns it into a NuGet package called `NorthwindTraders.Client`.</span></span> <span data-ttu-id="39f2c-107">Mais tarde, o Northwind deseja produzir um pacote do NuGet oficial próprio para sua biblioteca de cliente e, portanto, deseja contestar a propriedade da Nancy do nome do pacote.</span><span class="sxs-lookup"><span data-stu-id="39f2c-107">Later, Northwind wants to produce an official NuGet package of their own for their client library, and would thus like to dispute Nancy's ownership of the package name.</span></span>

<span data-ttu-id="39f2c-108">Nesse cenário, Nancy parece não estar agindo de má fé, mas sim apoiando as ferramentas e clientes da Northwind ao contribuir seu próprio tempo e código.</span><span class="sxs-lookup"><span data-stu-id="39f2c-108">In this scenario, Nancy does not appear to be acting with bad intentions, but is rather supporting Northwind's tools and customers by contributing her own time and code.</span></span> <span data-ttu-id="39f2c-109">Por outro lado, a Northwind é a proprietária legítima do nome Northwind.</span><span class="sxs-lookup"><span data-stu-id="39f2c-109">At the same time, Northwind is the legitimate owner of the Northwind name.</span></span>

<span data-ttu-id="39f2c-110">Seguindo o processo abaixo, a Northwind e a Nancy podem trabalhar juntas para alcançar uma resolução adequada, pois ambas estão interessadas em atender a comunidade de desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="39f2c-110">By following the process below, Northwind and Nancy can work together to a suitable resolution, because both are interested in serving the developer community.</span></span> <span data-ttu-id="39f2c-111">Normalmente não é necessário que a equipe do NuGet se envolva; a colaboração geralmente funciona melhor.</span><span class="sxs-lookup"><span data-stu-id="39f2c-111">It's typically not necessary for the NuGet team to become involved; collaboration usually works out best.</span></span>

## <a name="process"></a><span data-ttu-id="39f2c-112">Processo</span><span class="sxs-lookup"><span data-stu-id="39f2c-112">Process</span></span>

1. <span data-ttu-id="39f2c-113">Entre em contato com os proprietários do pacote ao qual se refere a controvérsia, usando o link **Entrar em contato com os proprietários** na página de detalhes do pacote.</span><span class="sxs-lookup"><span data-stu-id="39f2c-113">Contact the owners of the package you have the dispute with using the **Contact Owners** link on the package details page.</span></span> <span data-ttu-id="39f2c-114">Explique o problema de forma cordial e direta.</span><span class="sxs-lookup"><span data-stu-id="39f2c-114">Explain your issue in a kind and direct manner.</span></span>
2. <span data-ttu-id="39f2c-115">Envie uma cópia de sua mensagem para [support@nuget.org](mailto:support@nuget.org) que o NuGet e o .net Foundation estejam cientes de sua disputa.</span><span class="sxs-lookup"><span data-stu-id="39f2c-115">Send a copy of your message to [support@nuget.org](mailto:support@nuget.org) so that NuGet and the .NET Foundation are aware of your dispute.</span></span>
3. <span data-ttu-id="39f2c-116">Aguarde um máximo de 30 dias para uma resolução e, em seguida, notifique [support@nuget.org](mailto:support@nuget.org) novamente.</span><span class="sxs-lookup"><span data-stu-id="39f2c-116">Wait a maximum of 30 days for a resolution, then notify [support@nuget.org](mailto:support@nuget.org) again.</span></span> <span data-ttu-id="39f2c-117">A equipe de suporte do nuget.org será envolvida e tentará intermediar a controvérsia entre ambas as partes.</span><span class="sxs-lookup"><span data-stu-id="39f2c-117">The nuget.org support team will get involved and try to work through the dispute with both parties.</span></span>
