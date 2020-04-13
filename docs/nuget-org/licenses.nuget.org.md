---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 717cf8c47335c620410be71300b07de82799e1d3
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427111"
---
# <a name="licensesnugetorg"></a><span data-ttu-id="79c52-102">licenses.nuget.org</span><span class="sxs-lookup"><span data-stu-id="79c52-102">licenses.nuget.org</span></span>

## <a name="rationale"></a><span data-ttu-id="79c52-103">Fundamento</span><span class="sxs-lookup"><span data-stu-id="79c52-103">Rationale</span></span>

<span data-ttu-id="79c52-104">Com a introdução das [expressões de licença](../reference/nuspec.md#license), surgiu um requisito de ter um serviço confiável que fornecerá um texto de referência para identificadores de licença individuais, identificadores de exceção ou expressões de licença.</span><span class="sxs-lookup"><span data-stu-id="79c52-104">With the introduction of the [license expressions](../reference/nuspec.md#license), a requirement emerged to have a reliable service that would provide a reference text for individual license identifiers, exception identifiers or license expressions.</span></span>
<span data-ttu-id="79c52-105">Um requisito adicional desse serviço é ter um esquema de URL estável, que não seja suscetível a links desfeitos, de modo que possamos usá-lo com segurança para fornecer compatibilidade com versões anteriores a clientes mais antigos.</span><span class="sxs-lookup"><span data-stu-id="79c52-105">An additional requirement for this service is to have a stable URL schema, that is not susceptible to link rot, so that we can safely use it to provide backwards compatibility for older clients.</span></span>

<span data-ttu-id="79c52-106">Licenses.nuget.org cumpre essa função.</span><span class="sxs-lookup"><span data-stu-id="79c52-106">Licenses.nuget.org fulfills that role.</span></span> <span data-ttu-id="79c52-107">O nuget.org usa-o para fornecer a referência de texto de licença para pacotes que especificam sua licença usando uma expressão de licença.</span><span class="sxs-lookup"><span data-stu-id="79c52-107">Nuget.org uses it to provide the license text reference for packages that specify their license using a license expression.</span></span> <span data-ttu-id="79c52-108">`nuget pack` ou o empacotamento com outras [ferramentas de cliente](../install-nuget-client-tools.md) define o elemento [`licenseUrl`](../reference/nuspec.md#licenseurl) para que ele aponte para licenses.nuget.org visando fornecer compatibilidade com clientes mais antigos que não dão suporte ao elemento `license`.</span><span class="sxs-lookup"><span data-stu-id="79c52-108">`nuget pack` or packing with other [client tools](../install-nuget-client-tools.md) set the [`licenseUrl`](../reference/nuspec.md#licenseurl) element to point to licenses.nuget.org to provide backwards compatibility with older clients that don't support the `license` element.</span></span>

## <a name="protocol"></a><span data-ttu-id="79c52-109">Protocolo</span><span class="sxs-lookup"><span data-stu-id="79c52-109">Protocol</span></span>

<span data-ttu-id="79c52-110">Licenses.nuget.org destina-se a ser exibido por pessoas em seus navegadores; nenhuma resposta legível por computador é fornecida.</span><span class="sxs-lookup"><span data-stu-id="79c52-110">Licenses.nuget.org is intended to be viewed by people in their browsers, no machine-readable responses are provided.</span></span>
<span data-ttu-id="79c52-111">O protocolo HTTPS precisa ser usado, e as solicitações devem ser construídas de uma maneira específica.</span><span class="sxs-lookup"><span data-stu-id="79c52-111">HTTPS protocol must be used and requests are expected to be constructed in a certain way.</span></span> <span data-ttu-id="79c52-112">Ele só dá suporte a solicitações `GET`.</span><span class="sxs-lookup"><span data-stu-id="79c52-112">It only supports `GET` requests.</span></span>
<span data-ttu-id="79c52-113">Aceita expressões de licença ou identificadores de exceção de licença como entrada de uma forma especificada abaixo.</span><span class="sxs-lookup"><span data-stu-id="79c52-113">It accepts license expressions or license exception identifiers as an input in a way specified below.</span></span> <span data-ttu-id="79c52-114">Observe que todos os elementos de expressões de licença diferenciam maiúsculas de minúsculas e, portanto, toda entrada para licenses.nuget.org também diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="79c52-114">Please note, that all elements of license expressions are case sensitive, and therefore all input to licenses.nuget.org is case sensitive as well.</span></span>

### <a name="license-expressions"></a><span data-ttu-id="79c52-115">Expressões de licença</span><span class="sxs-lookup"><span data-stu-id="79c52-115">License expressions</span></span>

#### <a name="request"></a><span data-ttu-id="79c52-116">Solicitação</span><span class="sxs-lookup"><span data-stu-id="79c52-116">Request</span></span>

<span data-ttu-id="79c52-117">As expressões de licença (incluindo os casos triviais em que a expressão consiste em uma única licença) devem ser [codificadas em URL](https://tools.ietf.org/html/rfc3986#section-2.1) e usadas como um caminho na solicitação para licenses.nuget.org.</span><span class="sxs-lookup"><span data-stu-id="79c52-117">License expressions (including the trivial cases when expression consists of a single license) have to be [URL-encoded](https://tools.ietf.org/html/rfc3986#section-2.1) and used as a path in the request to licenses.nuget.org.</span></span>

| <span data-ttu-id="79c52-118">Expressão de licença</span><span class="sxs-lookup"><span data-stu-id="79c52-118">License expression</span></span> | <span data-ttu-id="79c52-119">URL a ser usada</span><span class="sxs-lookup"><span data-stu-id="79c52-119">URL to use</span></span> |
|:---|:---|
| <span data-ttu-id="79c52-120">MIT</span><span class="sxs-lookup"><span data-stu-id="79c52-120">MIT</span></span>                                                | <https://licenses.nuget.org/MIT> |
| <span data-ttu-id="79c52-121">(MIT)</span><span class="sxs-lookup"><span data-stu-id="79c52-121">(MIT)</span></span>                                              | <https://licenses.nuget.org/(MIT)> |
| <span data-ttu-id="79c52-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span><span class="sxs-lookup"><span data-stu-id="79c52-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span></span> | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

<span data-ttu-id="79c52-123">O serviço suporta apenas identificadores de licença e identificadores de exceção de licença que são aceitos por nuget.org. Todas as expressões de licença que contenham identificadores de licença não suportados ou identificadores de exceção de licença ou que não estejam em conformidade com a sintaxe de expressão da licença são consideradas inválidas.</span><span class="sxs-lookup"><span data-stu-id="79c52-123">The service supports only license identifiers and license exception identifiers that are accepted by nuget.org. All license expressions that contain unsupported license identifiers or license exception identifiers or that does not conform to license expression syntax are considered invalid.</span></span>

#### <a name="response"></a><span data-ttu-id="79c52-124">Resposta</span><span class="sxs-lookup"><span data-stu-id="79c52-124">Response</span></span>

<span data-ttu-id="79c52-125">Licenses.nuget.org responde às solicitações que contêm expressões de licença válidas com um código de status HTTP 200 e uma página da Web que contém uma descrição da expressão de licença:</span><span class="sxs-lookup"><span data-stu-id="79c52-125">Licenses.nuget.org responds to requests containing valid license expressions with an HTTP 200 status code and a web page containing a description of the license expression:</span></span>

* <span data-ttu-id="79c52-126">se a expressão de licença fornecida contiver um único identificador de licença, será retornada uma página da Web que contém o texto de referência dessa licença;</span><span class="sxs-lookup"><span data-stu-id="79c52-126">if supplied license expression contains a single license identifier a web page is returned that contains that license reference text;</span></span>
* <span data-ttu-id="79c52-127">se a expressão de licença fornecida for uma expressão de licença composta, será retornada uma página da Web que contém a expressão de licença com links para referências de exceção de licença ou licença individual.</span><span class="sxs-lookup"><span data-stu-id="79c52-127">if supplied license expression is a composite license expression, a web page is returned that contains the license expression with links to individual license or license exception references.</span></span>

<span data-ttu-id="79c52-128">Qualquer solicitação que contenha uma expressão de licença inválida resulta em uma resposta HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="79c52-128">Any requests that contain an invalid license expression result in an HTTP 404 response.</span></span>

### <a name="license-exceptions"></a><span data-ttu-id="79c52-129">Exceções de licença</span><span class="sxs-lookup"><span data-stu-id="79c52-129">License exceptions</span></span>

#### <a name="request"></a><span data-ttu-id="79c52-130">Solicitação</span><span class="sxs-lookup"><span data-stu-id="79c52-130">Request</span></span>

<span data-ttu-id="79c52-131">Os identificadores de exceção de licença devem ser codificados por URL e usados como um caminho na solicitação para licenses.nuget.org. Apenas um único identificador de exceção de licença pode ser fornecido em uma única solicitação.</span><span class="sxs-lookup"><span data-stu-id="79c52-131">License exception identifiers must be URL-encoded and used as a path in the request to licenses.nuget.org. Only a single license exception identifier can be supplied in a single request.</span></span> <span data-ttu-id="79c52-132">Nenhum caractere adicional além do identificador de exceção de licença pode estar presente na parte do caminho da URL.</span><span class="sxs-lookup"><span data-stu-id="79c52-132">No additional characters besides license exception identifier may present in the path portion of the URL.</span></span>

| <span data-ttu-id="79c52-133">Identificador de exceção de licença</span><span class="sxs-lookup"><span data-stu-id="79c52-133">License exception identifier</span></span> | <span data-ttu-id="79c52-134">URL a ser usada</span><span class="sxs-lookup"><span data-stu-id="79c52-134">URL to use</span></span> |
|:---|:---|
|<span data-ttu-id="79c52-135">FLTK-exception</span><span class="sxs-lookup"><span data-stu-id="79c52-135">FLTK-exception</span></span>            | <https://licenses.nuget.org/FLTK-exception> |
|<span data-ttu-id="79c52-136">openvpn-openssl-exception</span><span class="sxs-lookup"><span data-stu-id="79c52-136">openvpn-openssl-exception</span></span> | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a><span data-ttu-id="79c52-137">Resposta</span><span class="sxs-lookup"><span data-stu-id="79c52-137">Response</span></span>

<span data-ttu-id="79c52-138">Licenses.nuget.org responde a uma solicitação com um identificador de exceção de licença conhecido contendo uma resposta HTTP 200 e uma página da Web que contém o texto de referência para a exceção de licença especificada.</span><span class="sxs-lookup"><span data-stu-id="79c52-138">Licenses.nuget.org responds to a request with a known license exception identifier with a HTTP 200 response and a web page containing the reference text for the specified license exception.</span></span>

<span data-ttu-id="79c52-139">Qualquer solicitação que contenha um identificador de exceção de licença sem suporte resulta em uma resposta HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="79c52-139">Any request containing an unsupported license exception identifier results in an HTTP 404 response.</span></span>