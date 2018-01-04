---
title: "“Solução de controvérsias no nome do pacote do NuGet | Microsoft Docs”"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 6d664378-3f7b-426e-aef3-2254d745fe60
description: "O processo para solucionar controvérsias entre publicadores de pacotes do NuGet relacionadas à identidade visual, marcas comerciais e outras situações de conflito."
keywords: "Controvérsias de pacote do NuGet, solução de controvérsias do NuGet, processo de solução de controvérsias"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 32f5f766a49a2e4254a81978757d973fc5353db1
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="resolving-disputes-over-nuget-package-names"></a><span data-ttu-id="5c6a0-104">Solucionar controvérsias sobre nomes de pacote do NuGet</span><span class="sxs-lookup"><span data-stu-id="5c6a0-104">Resolving disputes over NuGet package names</span></span>

<span data-ttu-id="5c6a0-105">Este documento é um processo de resolução recomendado para membros da comunidade solucionarem controvérsias com outros editores do NuGet.</span><span class="sxs-lookup"><span data-stu-id="5c6a0-105">This document is a recommended resolution process for community members to resolve disputes with other NuGet publishers.</span></span>  

<span data-ttu-id="5c6a0-106">Por exemplo, suponha que a Northwind Traders cria um sistema CRM para o qual eles fornecem drivers de cliente como um MSI que pode ser baixado do site.</span><span class="sxs-lookup"><span data-stu-id="5c6a0-106">For example, suppose that Northwind Traders makes a CRM system for which they provide client drivers as a downloadable MSI from their website.</span></span> <span data-ttu-id="5c6a0-107">Nancy, um desenvolvedor independente, quer facilitar o uso da biblioteca de cliente da Northwind e o transforma em um pacote do NuGet chamado `NorthwindTraders.Client`.</span><span class="sxs-lookup"><span data-stu-id="5c6a0-107">Nancy, an independent developer, wants to make it easier to use Northwind's client library, and turns it into a NuGet package called `NorthwindTraders.Client`.</span></span> <span data-ttu-id="5c6a0-108">Mais tarde, o Northwind deseja produzir um pacote do NuGet oficial próprio para sua biblioteca de cliente e, portanto, deseja contestar a propriedade da Nancy do nome do pacote.</span><span class="sxs-lookup"><span data-stu-id="5c6a0-108">Later, Northwind wants to produce an official NuGet package of their own for their client library, and would thus like to dispute Nancy's ownership of the package name.</span></span>

<span data-ttu-id="5c6a0-109">Nesse cenário, Nancy parece não estar agindo de má fé, mas sim apoiando as ferramentas e clientes da Northwind ao contribuir seu próprio tempo e código.</span><span class="sxs-lookup"><span data-stu-id="5c6a0-109">In this scenario, Nancy does not appear to be acting with bad intentions, but is rather supporting Northwind's tools and customers by contributing her own time and code.</span></span> <span data-ttu-id="5c6a0-110">Por outro lado, a Northwind é a proprietária legítima do nome Northwind.</span><span class="sxs-lookup"><span data-stu-id="5c6a0-110">At the same time, Northwind is the legitimate owner of the Northwind name.</span></span>

<span data-ttu-id="5c6a0-111">Seguindo o processo abaixo, a Northwind e a Nancy podem trabalhar juntas para alcançar uma resolução adequada, pois ambas estão interessadas em atender a comunidade de desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="5c6a0-111">By following the process below, Northwind and Nancy can work together to a suitable resolution, because both are interested in serving the developer community.</span></span> <span data-ttu-id="5c6a0-112">Normalmente não é necessário que a equipe do NuGet se envolva; a colaboração geralmente funciona melhor.</span><span class="sxs-lookup"><span data-stu-id="5c6a0-112">It's typically not necessary for the NuGet team to become involved; collaboration usually works out best.</span></span> <span data-ttu-id="5c6a0-113">Na verdade, todas as controvérsias levada para a equipe do NuGet até hoje foram solucionadas sem a necessidade de julgamento direto por parte da equipe.</span><span class="sxs-lookup"><span data-stu-id="5c6a0-113">In fact, every dispute brought to the NuGet team's attention to date has been worked out without the team needing to pass judgment.</span></span>


## <a name="process"></a><span data-ttu-id="5c6a0-114">Processo</span><span class="sxs-lookup"><span data-stu-id="5c6a0-114">Process</span></span>

1. <span data-ttu-id="5c6a0-115">Entre em contato com os proprietários do pacote que você está contestando usando o link **Contatar os Proprietários** na página de detalhes do pacote.</span><span class="sxs-lookup"><span data-stu-id="5c6a0-115">Contact the owners of the package you have the dispute with using the **Contact Owners** link on the package details page.</span></span> <span data-ttu-id="5c6a0-116">Explique seu problema de forma gentil e direta.</span><span class="sxs-lookup"><span data-stu-id="5c6a0-116">Explain your issue in a kind and direct manner.</span></span>
2. <span data-ttu-id="5c6a0-117">Envie uma cópia da sua mensagem para [support@nuget.org](mailto:support@nuget.org) para que o NuGet e a .NET Foundation estejam cientes da sua controvérsia.</span><span class="sxs-lookup"><span data-stu-id="5c6a0-117">Send a copy of your message to [support@nuget.org](mailto:support@nuget.org) so that NuGet and the .NET Foundation are aware of your dispute.</span></span>
3. <span data-ttu-id="5c6a0-118">Aguarde um máximo de 30 dias por uma solução e após esse período notifique [support@nuget.org](mailto:support@nuget.org) novamente.</span><span class="sxs-lookup"><span data-stu-id="5c6a0-118">Wait a maximum of 30 days for a resolution, after which notify [support@nuget.org](mailto:support@nuget.org) again.</span></span> <span data-ttu-id="5c6a0-119">A equipe de suporte do nuget.org será envolvida e tentará intermediar a controvérsia entre ambas as partes.</span><span class="sxs-lookup"><span data-stu-id="5c6a0-119">The nuget.org support team will get involved and try to work through the dispute with both parties.</span></span>
