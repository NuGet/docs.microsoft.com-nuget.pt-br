---
title: SDK do cliente NuGet
description: A API está em constante evolução e ainda não está documentado, mas os exemplos estão disponíveis no blog de Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 97ed3ec7d41d2847c0521af69373a1871eb585dd
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324676"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="f415f-103">SDK do cliente NuGet</span><span class="sxs-lookup"><span data-stu-id="f415f-103">NuGet Client SDK</span></span>

> [!Note]
> <span data-ttu-id="f415f-104">Não deve ser confundido com o [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)</span><span class="sxs-lookup"><span data-stu-id="f415f-104">Not to be confused with the [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)</span></span>

<span data-ttu-id="f415f-105">O *SDK do cliente do NuGet* refere-se a um grupo de bibliotecas .NET centralizadas em torno [NuGet](https://www.nuget.org/packages/NuGet.Client), [struktury](https://www.nuget.org/packages/NuGet.Packaging), e [é](https://www.nuget.org/packages/NuGet.Protocol).</span><span class="sxs-lookup"><span data-stu-id="f415f-105">The *NuGet Client SDK* refers to a group of .NET libraries centered around [NuGet.Client](https://www.nuget.org/packages/NuGet.Client), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), and [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span></span> <span data-ttu-id="f415f-106">Esses pacotes substituem anterior [NuGet. Core](https://www.nuget.org/packages/NuGet.Core/) biblioteca.</span><span class="sxs-lookup"><span data-stu-id="f415f-106">These packages replace the earlier [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) library.</span></span>

<span data-ttu-id="f415f-107">Estamos trabalhando em ter uma área de superfície estável que podemos pode documentar em breve.</span><span class="sxs-lookup"><span data-stu-id="f415f-107">We are working on having a stable surface area that we can document soon.</span></span>

## <a name="source-code"></a><span data-ttu-id="f415f-108">Código-fonte</span><span class="sxs-lookup"><span data-stu-id="f415f-108">Source code</span></span>

<span data-ttu-id="f415f-109">O código-fonte é publicado no GitHub no projeto [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span><span class="sxs-lookup"><span data-stu-id="f415f-109">The source code is published on GitHub in the project [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span></span>

## <a name="third-party-documentation"></a><span data-ttu-id="f415f-110">Documentação de terceiros</span><span class="sxs-lookup"><span data-stu-id="f415f-110">Third-party documentation</span></span>

<span data-ttu-id="f415f-111">Você pode encontrar exemplos e documentação para algumas das APIs na seguinte série de blog por Dave Glick, publicados 2016:</span><span class="sxs-lookup"><span data-stu-id="f415f-111">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="f415f-112">Explorando as bibliotecas do NuGet v3, parte 1: Introdução e conceitos</span><span class="sxs-lookup"><span data-stu-id="f415f-112">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="f415f-113">Explorando as bibliotecas do NuGet v3, parte 2: Procurar pacotes</span><span class="sxs-lookup"><span data-stu-id="f415f-113">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="f415f-114">Explorando as bibliotecas do NuGet v3, parte 3: Instalando pacotes</span><span class="sxs-lookup"><span data-stu-id="f415f-114">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="f415f-115">Essas postagens de blog foram escritas logo após o **3.4.3** versão do NuGet, pacotes de SDK do cliente foram lançados.</span><span class="sxs-lookup"><span data-stu-id="f415f-115">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="f415f-116">Versões mais recentes dos pacotes podem ser incompatíveis com as informações de postagens de blog.</span><span class="sxs-lookup"><span data-stu-id="f415f-116">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="f415f-117">Martin Björkström fez uma postagem de blog de acompanhamento para a série do blog de Dave Glick onde ele apresenta uma abordagem diferente sobre como usar o SDK do cliente do NuGet para instalar os pacotes do NuGet:</span><span class="sxs-lookup"><span data-stu-id="f415f-117">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK for installing NuGet packages:</span></span>

- [<span data-ttu-id="f415f-118">Revisitando as bibliotecas do NuGet v3</span><span class="sxs-lookup"><span data-stu-id="f415f-118">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
