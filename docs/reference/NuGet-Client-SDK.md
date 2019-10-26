---
title: SDK do cliente NuGet
description: A API está em evolução e ainda não está documentada, mas exemplos estão disponíveis no blog de Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 873bde467a39653b818b49173d53bc983e99d1b9
ms.sourcegitcommit: f9645fc5f49c18978e12a292a3f832e162e069d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72924612"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="13334-103">SDK do cliente NuGet</span><span class="sxs-lookup"><span data-stu-id="13334-103">NuGet Client SDK</span></span>

<span data-ttu-id="13334-104">O *SDK do cliente NuGet* refere-se a um grupo de pacotes NuGet centralizado em relação ao [NuGet. Commands](https://www.nuget.org/packages/NuGet.Commands), [NuGet. Packaging](https://www.nuget.org/packages/NuGet.Packaging)e [NuGet. Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span><span class="sxs-lookup"><span data-stu-id="13334-104">The *NuGet Client SDK* refers to a group of NuGet packages centered around [NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands), [NuGet.Packaging](https://www.nuget.org/packages/NuGet.Packaging), and [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span></span> <span data-ttu-id="13334-105">Esses pacotes substituem a biblioteca [NuGet. Core](https://www.nuget.org/packages/NuGet.Core/) anterior.</span><span class="sxs-lookup"><span data-stu-id="13334-105">These packages replace the earlier [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) library.</span></span>

> [!Note]
>  <span data-ttu-id="13334-106">Para obter a documentação sobre o protocolo de servidor NuGet, consulte a [API do servidor NuGet](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="13334-106">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="source-code"></a><span data-ttu-id="13334-107">Código-fonte</span><span class="sxs-lookup"><span data-stu-id="13334-107">Source code</span></span>

<span data-ttu-id="13334-108">O código-fonte é publicado no GitHub no projeto [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client).</span><span class="sxs-lookup"><span data-stu-id="13334-108">The source code is published on GitHub in the project [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span></span>

## <a name="third-party-documentation"></a><span data-ttu-id="13334-109">Documentação de terceiros</span><span class="sxs-lookup"><span data-stu-id="13334-109">Third-party documentation</span></span>

<span data-ttu-id="13334-110">Você pode encontrar exemplos e documentação para algumas das APIs na série de Blogs a seguir de Dave Glick, publicada 2016:</span><span class="sxs-lookup"><span data-stu-id="13334-110">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="13334-111">Explorando as bibliotecas do NuGet v3, parte 1: introdução e conceitos</span><span class="sxs-lookup"><span data-stu-id="13334-111">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="13334-112">Explorando as bibliotecas do NuGet v3, parte 2: pesquisando pacotes</span><span class="sxs-lookup"><span data-stu-id="13334-112">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="13334-113">Explorando as bibliotecas do NuGet v3, parte 3: Instalando pacotes</span><span class="sxs-lookup"><span data-stu-id="13334-113">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="13334-114">Essas Postagens de blog foram escritas logo após a liberação da versão **3.4.3** dos pacotes do SDK do cliente NuGet.</span><span class="sxs-lookup"><span data-stu-id="13334-114">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="13334-115">As versões mais recentes dos pacotes podem ser incompatíveis com as informações nas postagens do blog.</span><span class="sxs-lookup"><span data-stu-id="13334-115">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="13334-116">Martin Björkström fez uma postagem no blog de acompanhamento na série de Blogs de Dave Glick, onde ele introduz uma abordagem diferente sobre o uso do SDK do cliente do NuGet para a instalação de pacotes NuGet:</span><span class="sxs-lookup"><span data-stu-id="13334-116">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK for installing NuGet packages:</span></span>

- [<span data-ttu-id="13334-117">Revisitando as bibliotecas do NuGet v3</span><span class="sxs-lookup"><span data-stu-id="13334-117">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
