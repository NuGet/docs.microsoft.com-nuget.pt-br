---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 4a40cc1f7d333e8d35a721f3eed2e6b9365faf7b
ms.sourcegitcommit: 8793f528a11bd8e8fb229cd12e9abba50d61e104
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2019
ms.locfileid: "58921553"
---
# <a name="licensesnugetorg"></a><span data-ttu-id="dce86-102">licenses.nuget.org</span><span class="sxs-lookup"><span data-stu-id="dce86-102">licenses.nuget.org</span></span>

## <a name="rationale"></a><span data-ttu-id="dce86-103">Racional</span><span class="sxs-lookup"><span data-stu-id="dce86-103">Rationale</span></span>

<span data-ttu-id="dce86-104">Com a introdução do [expressões de licença](nuspec.md#license), um requisito surgiu para ter um serviço confiável que deveria fornecer um texto de referência para os identificadores de licença individual, os identificadores de exceção ou expressões de licença.</span><span class="sxs-lookup"><span data-stu-id="dce86-104">With the introduction of the [license expressions](nuspec.md#license), a requirement emerged to have a reliable service that would provide a reference text for individual license identifiers, exception identifiers or license expressions.</span></span>
<span data-ttu-id="dce86-105">Um requisito adicional para esse serviço é ter um esquema de URL estável, que não é suscetível a vincular corrompidos, para que podemos pode usá-lo com segurança para fornecer compatibilidade com versões anteriores de clientes mais antigos.</span><span class="sxs-lookup"><span data-stu-id="dce86-105">An additional requirement for this service is to have a stable URL schema, that is not susceptible to link rot, so that we can safely use it to provide backwards compatibility for older clients.</span></span>

<span data-ttu-id="dce86-106">Licenses.NuGet.org atende a essa função.</span><span class="sxs-lookup"><span data-stu-id="dce86-106">Licenses.nuget.org fulfills that role.</span></span> <span data-ttu-id="dce86-107">NuGet.org usa para fornecer a referência de texto de licença para pacotes que especificam a licença usando uma expressão de licença.</span><span class="sxs-lookup"><span data-stu-id="dce86-107">Nuget.org uses it to provide the license text reference for packages that specify their license using a license expression.</span></span> `nuget pack` <span data-ttu-id="dce86-108">ou embalagem com os outros [ferramentas de cliente](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) defina o [ `licenseUrl` ](nuspec.md#licenseurl) elemento para apontar para licenses.nuget.org para proporcionar compatibilidade com clientes mais antigos que não dão suporte a `license` elemento.</span><span class="sxs-lookup"><span data-stu-id="dce86-108">or packing with other [client tools](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) set the [`licenseUrl`](nuspec.md#licenseurl) element to point to licenses.nuget.org to provide backwards compatibility with older clients that don't support the `license` element.</span></span>

## <a name="protocol"></a><span data-ttu-id="dce86-109">Protocolo</span><span class="sxs-lookup"><span data-stu-id="dce86-109">Protocol</span></span>

<span data-ttu-id="dce86-110">Nenhuma resposta legível por máquina licenses.NuGet.org se destina a ser exibido pelas pessoas em seus navegadores, é fornecida.</span><span class="sxs-lookup"><span data-stu-id="dce86-110">Licenses.nuget.org is intended to be viewed by people in their browsers, no machine-readable responses are provided.</span></span>
<span data-ttu-id="dce86-111">Protocolo HTTPS deve ser usado e as solicitações devem ser construídos em uma determinada maneira.</span><span class="sxs-lookup"><span data-stu-id="dce86-111">HTTPS protocol must be used and requests are expected to be constructed in a certain way.</span></span> <span data-ttu-id="dce86-112">Ele dá suporte apenas a `GET` solicitações.</span><span class="sxs-lookup"><span data-stu-id="dce86-112">It only supports `GET` requests.</span></span>
<span data-ttu-id="dce86-113">Ele aceita expressões de licença ou identificadores de exceção de licença como uma entrada de uma forma especificada abaixo.</span><span class="sxs-lookup"><span data-stu-id="dce86-113">It accepts license expressions or license exception identifiers as an input in a way specified below.</span></span> <span data-ttu-id="dce86-114">Observe que todos os elementos de expressões de licença diferenciam maiusculas de minúsculas e, portanto, todas as entradas para licenses.nuget.org diferencia maiusculas de minúsculas, bem.</span><span class="sxs-lookup"><span data-stu-id="dce86-114">Please note, that all elements of license expressions are case sensitive, and therefore all input to licenses.nuget.org is case sensitive as well.</span></span>

### <a name="license-expressions"></a><span data-ttu-id="dce86-115">Expressões de licença</span><span class="sxs-lookup"><span data-stu-id="dce86-115">License expressions</span></span>

#### <a name="request"></a><span data-ttu-id="dce86-116">Solicitação</span><span class="sxs-lookup"><span data-stu-id="dce86-116">Request</span></span>

<span data-ttu-id="dce86-117">Expressões de licença (incluindo os casos triviais quando a expressão consiste em uma única licença) precisam ser [codificado por URL](https://tools.ietf.org/html/rfc3986#section-2.1) e usado como um caminho na solicitação para licenses.nuget.org.</span><span class="sxs-lookup"><span data-stu-id="dce86-117">License expressions (including the trivial cases when expression consists of a single license) have to be [URL-encoded](https://tools.ietf.org/html/rfc3986#section-2.1) and used as a path in the request to licenses.nuget.org.</span></span>

| <span data-ttu-id="dce86-118">Expressão de licença</span><span class="sxs-lookup"><span data-stu-id="dce86-118">License expression</span></span> | <span data-ttu-id="dce86-119">URL a ser usada</span><span class="sxs-lookup"><span data-stu-id="dce86-119">URL to use</span></span> |
|:---|:---|
| <span data-ttu-id="dce86-120">MIT</span><span class="sxs-lookup"><span data-stu-id="dce86-120">MIT</span></span>                                                | <https://licenses.nuget.org/MIT> |
| <span data-ttu-id="dce86-121">(MIT)</span><span class="sxs-lookup"><span data-stu-id="dce86-121">(MIT)</span></span>                                              | <https://licenses.nuget.org/(MIT)> |
| <span data-ttu-id="dce86-122">(LGPL 2.0-somente com o Apache FLTK exceção OR-2.0 +)</span><span class="sxs-lookup"><span data-stu-id="dce86-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span></span> | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

<span data-ttu-id="dce86-123">O serviço oferece suporte somente a identificadores de licença e identificadores de exceção de licença são aceitos pelo nuget.org. Todas as expressões de licença que contêm os identificadores de licença sem suporte ou identificadores de exceção de licença ou que não estão em conformidade com a sintaxe de expressão de licença são consideradas inválidas.</span><span class="sxs-lookup"><span data-stu-id="dce86-123">The service supports only license identifiers and license exception identifiers that are accepted by nuget.org. All license expressions that contain unsupported license identifiers or license exception identifiers or that does not conform to license expression syntax are considered invalid.</span></span>

#### <a name="response"></a><span data-ttu-id="dce86-124">Resposta</span><span class="sxs-lookup"><span data-stu-id="dce86-124">Response</span></span>

<span data-ttu-id="dce86-125">Licenses.NuGet.org responde às solicitações que contêm expressões de licença válida com um código de status HTTP 200 e uma página da web que contém uma descrição da expressão de licença:</span><span class="sxs-lookup"><span data-stu-id="dce86-125">Licenses.nuget.org responds to requests containing valid license expressions with an HTTP 200 status code and a web page containing a description of the license expression:</span></span>

* <span data-ttu-id="dce86-126">Se for fornecido a expressão de licença contém um identificador de licença única que uma página da web é retornado que contém o texto de referência dessa licença;</span><span class="sxs-lookup"><span data-stu-id="dce86-126">if supplied license expression contains a single license identifier a web page is returned that contains that license reference text;</span></span>
* <span data-ttu-id="dce86-127">Se for fornecido expressão de licença é uma expressão de licença de composição, uma página da web é retornado que contém a expressão de licença com links para referências de exceção de licença ou licença individual.</span><span class="sxs-lookup"><span data-stu-id="dce86-127">if supplied license expression is a composite license expression, a web page is returned that contains the license expression with links to individual license or license exception references.</span></span>

<span data-ttu-id="dce86-128">Qualquer solicitação que contenha uma expressão de licença inválida resulta em uma resposta HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="dce86-128">Any requests that contain an invalid license expression result in an HTTP 404 response.</span></span>

### <a name="license-exceptions"></a><span data-ttu-id="dce86-129">Exceções de licença</span><span class="sxs-lookup"><span data-stu-id="dce86-129">License exceptions</span></span>

#### <a name="request"></a><span data-ttu-id="dce86-130">Solicitação</span><span class="sxs-lookup"><span data-stu-id="dce86-130">Request</span></span>

<span data-ttu-id="dce86-131">Identificadores de exceção de licença devem ser codificados de URL e é usada como um caminho na solicitação para licenses.nuget.org. Somente um identificador de exceção única licença pode ser fornecido em uma única solicitação.</span><span class="sxs-lookup"><span data-stu-id="dce86-131">License exception identifiers must be URL-encoded and used as a path in the request to licenses.nuget.org. Only a single license exception identifier can be supplied in a single request.</span></span> <span data-ttu-id="dce86-132">Não há caracteres adicionais além do identificador de exceção de licença podem estar presentes na parte do caminho da URL.</span><span class="sxs-lookup"><span data-stu-id="dce86-132">No additional characters besides license exception identifier may present in the path portion of the URL.</span></span>

| <span data-ttu-id="dce86-133">Identificador de exceção de licença</span><span class="sxs-lookup"><span data-stu-id="dce86-133">License exception identifier</span></span> | <span data-ttu-id="dce86-134">URL a ser usada</span><span class="sxs-lookup"><span data-stu-id="dce86-134">URL to use</span></span> |
|:---|:---|
|<span data-ttu-id="dce86-135">FLTK-exception</span><span class="sxs-lookup"><span data-stu-id="dce86-135">FLTK-exception</span></span>            | <https://licenses.nuget.org/FLTK-exception> |
|<span data-ttu-id="dce86-136">openvpn-openssl-exception</span><span class="sxs-lookup"><span data-stu-id="dce86-136">openvpn-openssl-exception</span></span> | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a><span data-ttu-id="dce86-137">Resposta</span><span class="sxs-lookup"><span data-stu-id="dce86-137">Response</span></span>

<span data-ttu-id="dce86-138">Licenses.NuGet.org responde a uma solicitação com um identificador de exceção de licenças conhecidos com uma resposta HTTP 200 e uma página da web que contém o texto de referência para a exceção de licença especificado.</span><span class="sxs-lookup"><span data-stu-id="dce86-138">Licenses.nuget.org responds to a request with a known license exception identifier with a HTTP 200 response and a web page containing the reference text for the specified license exception.</span></span>

<span data-ttu-id="dce86-139">Qualquer solicitação que contém um identificador de exceção sem suporte de licença resulta em uma resposta HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="dce86-139">Any request containing an unsupported license exception identifier results in an HTTP 404 response.</span></span>