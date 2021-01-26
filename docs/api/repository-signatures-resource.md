---
title: Assinaturas de repositório, API do NuGet | Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: O recurso de assinaturas de repositório permite que as fontes de pacote de clientes anunciem seus recursos de assinatura de repositório.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: bfdbbb3a11de3be3f2258a3a289c0188740cdfce
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775327"
---
# <a name="repository-signatures"></a><span data-ttu-id="e33ca-103">Assinaturas de repositório</span><span class="sxs-lookup"><span data-stu-id="e33ca-103">Repository signatures</span></span>

<span data-ttu-id="e33ca-104">Se uma origem de pacote oferecer suporte à adição de assinaturas de repositório a pacotes publicados, é possível para um cliente determinar os certificados de autenticação que são usados pela origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="e33ca-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="e33ca-105">Esse recurso permite que os clientes detectem se um pacote assinado por um repositório foi adulterado ou tem um certificado de assinatura inesperado.</span><span class="sxs-lookup"><span data-stu-id="e33ca-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="e33ca-106">O recurso usado para buscar essas informações de assinatura de repositório é o `RepositorySignatures` recurso encontrado no [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="e33ca-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="e33ca-107">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="e33ca-107">Versioning</span></span>

<span data-ttu-id="e33ca-108">O seguinte `@type` valor é usado:</span><span class="sxs-lookup"><span data-stu-id="e33ca-108">The following `@type` value is used:</span></span>

<span data-ttu-id="e33ca-109">@type valor</span><span class="sxs-lookup"><span data-stu-id="e33ca-109">@type value</span></span>                | <span data-ttu-id="e33ca-110">Observações</span><span class="sxs-lookup"><span data-stu-id="e33ca-110">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="e33ca-111">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="e33ca-111">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="e33ca-112">A versão inicial</span><span class="sxs-lookup"><span data-stu-id="e33ca-112">The initial release</span></span>
<span data-ttu-id="e33ca-113">RepositorySignatures/4.9.0</span><span class="sxs-lookup"><span data-stu-id="e33ca-113">RepositorySignatures/4.9.0</span></span> | <span data-ttu-id="e33ca-114">Com suporte dos clientes NuGet v 4.9 +</span><span class="sxs-lookup"><span data-stu-id="e33ca-114">Supported by NuGet v4.9+ clients</span></span>
<span data-ttu-id="e33ca-115">RepositorySignatures/5.0.0</span><span class="sxs-lookup"><span data-stu-id="e33ca-115">RepositorySignatures/5.0.0</span></span> | <span data-ttu-id="e33ca-116">Permite habilitar o `allRepositorySigned` .</span><span class="sxs-lookup"><span data-stu-id="e33ca-116">Allows enabling `allRepositorySigned`.</span></span> <span data-ttu-id="e33ca-117">Compatível com clientes NuGet v 5.0 +</span><span class="sxs-lookup"><span data-stu-id="e33ca-117">Supported by NuGet v5.0+ clients</span></span>

## <a name="base-url"></a><span data-ttu-id="e33ca-118">URL base</span><span class="sxs-lookup"><span data-stu-id="e33ca-118">Base URL</span></span>

<span data-ttu-id="e33ca-119">A URL do ponto de entrada para as seguintes APIs é o valor da `@id` propriedade associada ao valor de recurso mencionado anteriormente `@type` .</span><span class="sxs-lookup"><span data-stu-id="e33ca-119">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="e33ca-120">Este tópico usa a URL do espaço reservado `{@id}` .</span><span class="sxs-lookup"><span data-stu-id="e33ca-120">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="e33ca-121">Observe que, ao contrário de outros recursos, `{@id}` é necessário que a URL seja servida via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e33ca-121">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="e33ca-122">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="e33ca-122">HTTP methods</span></span>

<span data-ttu-id="e33ca-123">Todas as URLs encontradas no recurso de assinaturas de repositório dão suporte apenas aos métodos HTTP `GET` e `HEAD` .</span><span class="sxs-lookup"><span data-stu-id="e33ca-123">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="e33ca-124">Índice de assinaturas de repositório</span><span class="sxs-lookup"><span data-stu-id="e33ca-124">Repository signatures index</span></span>

<span data-ttu-id="e33ca-125">O índice de assinaturas de repositório contém duas partes de informação:</span><span class="sxs-lookup"><span data-stu-id="e33ca-125">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="e33ca-126">Se todos os pacotes encontrados na origem são o repositório assinado por essa origem de pacote.</span><span class="sxs-lookup"><span data-stu-id="e33ca-126">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="e33ca-127">A lista de certificados usados pela origem do pacote para assinar pacotes.</span><span class="sxs-lookup"><span data-stu-id="e33ca-127">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="e33ca-128">Na maioria dos casos, a lista de certificados só será acrescentada a.</span><span class="sxs-lookup"><span data-stu-id="e33ca-128">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="e33ca-129">Novos certificados seriam adicionados à lista quando o certificado de autenticação anterior tiver expirado e a origem do pacote precisar começar a usar um novo certificado de autenticação.</span><span class="sxs-lookup"><span data-stu-id="e33ca-129">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="e33ca-130">Se um certificado for removido da lista, isso significa que todas as assinaturas de pacote criadas com o certificado de autenticação removido não devem mais ser consideradas válidas pelo cliente.</span><span class="sxs-lookup"><span data-stu-id="e33ca-130">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="e33ca-131">Nesse caso, a assinatura do pacote (mas não necessariamente o pacote) é inválida.</span><span class="sxs-lookup"><span data-stu-id="e33ca-131">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="e33ca-132">Uma política de cliente pode permitir a instalação do pacote como não assinado.</span><span class="sxs-lookup"><span data-stu-id="e33ca-132">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="e33ca-133">No caso de revogação de certificado (por exemplo, comprometimento de chave), espera-se que a origem do pacote assine novamente todos os pacotes assinados pelo certificado afetado.</span><span class="sxs-lookup"><span data-stu-id="e33ca-133">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="e33ca-134">Além disso, a origem do pacote deve remover o certificado afetado da lista de certificados de autenticação.</span><span class="sxs-lookup"><span data-stu-id="e33ca-134">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="e33ca-135">A solicitação a seguir busca o índice de assinaturas de repositório.</span><span class="sxs-lookup"><span data-stu-id="e33ca-135">The following request fetches the repository signatures index.</span></span>

```
GET {@id}
```

<span data-ttu-id="e33ca-136">O índice de assinatura de repositório é um documento JSON que contém um objeto com as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="e33ca-136">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="e33ca-137">Nome</span><span class="sxs-lookup"><span data-stu-id="e33ca-137">Name</span></span>                | <span data-ttu-id="e33ca-138">Type</span><span class="sxs-lookup"><span data-stu-id="e33ca-138">Type</span></span>             | <span data-ttu-id="e33ca-139">Necessária</span><span class="sxs-lookup"><span data-stu-id="e33ca-139">Required</span></span> | <span data-ttu-id="e33ca-140">Observações</span><span class="sxs-lookup"><span data-stu-id="e33ca-140">Notes</span></span>
------------------- | ---------------- | -------- | -----
<span data-ttu-id="e33ca-141">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="e33ca-141">allRepositorySigned</span></span> | <span data-ttu-id="e33ca-142">booleano</span><span class="sxs-lookup"><span data-stu-id="e33ca-142">boolean</span></span>          | <span data-ttu-id="e33ca-143">sim</span><span class="sxs-lookup"><span data-stu-id="e33ca-143">yes</span></span>      | <span data-ttu-id="e33ca-144">Deve estar `false` nos recursos 4.7.0 e 4.9.0</span><span class="sxs-lookup"><span data-stu-id="e33ca-144">Must be `false` on 4.7.0 and 4.9.0 resources</span></span>
<span data-ttu-id="e33ca-145">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="e33ca-145">signingCertificates</span></span> | <span data-ttu-id="e33ca-146">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="e33ca-146">array of objects</span></span> | <span data-ttu-id="e33ca-147">sim</span><span class="sxs-lookup"><span data-stu-id="e33ca-147">yes</span></span>      | 

<span data-ttu-id="e33ca-148">O `allRepositorySigned` booliano será definido como false se a origem do pacote tiver alguns pacotes que não têm nenhuma assinatura de repositório.</span><span class="sxs-lookup"><span data-stu-id="e33ca-148">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="e33ca-149">Se o booliano for definido como true, todos os pacotes disponíveis na origem deverão ter uma assinatura de repositório produzida por um dos certificados de autenticação mencionados em `signingCertificates` .</span><span class="sxs-lookup"><span data-stu-id="e33ca-149">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

> [!Warning]
> <span data-ttu-id="e33ca-150">O `allRepositorySigned` booliano deve ser falso nos recursos 4.7.0 e 4.9.0.</span><span class="sxs-lookup"><span data-stu-id="e33ca-150">The `allRepositorySigned` boolean must be false on the 4.7.0 and 4.9.0 resources.</span></span> <span data-ttu-id="e33ca-151">Os clientes do NuGet v 4.7, v 4.8 e v 4.9 não podem instalar pacotes de fontes que foram `allRepositorySigned` definidas como true.</span><span class="sxs-lookup"><span data-stu-id="e33ca-151">NuGet v4.7, v4.8, and v4.9 clients cannot install packages from sources that have `allRepositorySigned` set to true.</span></span>

<span data-ttu-id="e33ca-152">Deve haver um ou mais certificados de assinatura na `signingCertificates` matriz se o `allRepositorySigned` booliano estiver definido como true.</span><span class="sxs-lookup"><span data-stu-id="e33ca-152">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="e33ca-153">Se a matriz estiver vazia e `allRepositorySigned` for definida como true, todos os pacotes da origem deverão ser considerados inválidos, embora uma política de cliente ainda possa permitir o consumo de pacotes.</span><span class="sxs-lookup"><span data-stu-id="e33ca-153">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="e33ca-154">Cada elemento nessa matriz é um objeto JSON com as propriedades a seguir.</span><span class="sxs-lookup"><span data-stu-id="e33ca-154">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="e33ca-155">Nome</span><span class="sxs-lookup"><span data-stu-id="e33ca-155">Name</span></span>         | <span data-ttu-id="e33ca-156">Type</span><span class="sxs-lookup"><span data-stu-id="e33ca-156">Type</span></span>   | <span data-ttu-id="e33ca-157">Necessária</span><span class="sxs-lookup"><span data-stu-id="e33ca-157">Required</span></span> | <span data-ttu-id="e33ca-158">Observações</span><span class="sxs-lookup"><span data-stu-id="e33ca-158">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="e33ca-159">contentUrl</span><span class="sxs-lookup"><span data-stu-id="e33ca-159">contentUrl</span></span>   | <span data-ttu-id="e33ca-160">string</span><span class="sxs-lookup"><span data-stu-id="e33ca-160">string</span></span> | <span data-ttu-id="e33ca-161">sim</span><span class="sxs-lookup"><span data-stu-id="e33ca-161">yes</span></span>      | <span data-ttu-id="e33ca-162">URL absoluta para o certificado público codificado em DER</span><span class="sxs-lookup"><span data-stu-id="e33ca-162">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="e33ca-163">marcas</span><span class="sxs-lookup"><span data-stu-id="e33ca-163">fingerprints</span></span> | <span data-ttu-id="e33ca-164">objeto</span><span class="sxs-lookup"><span data-stu-id="e33ca-164">object</span></span> | <span data-ttu-id="e33ca-165">sim</span><span class="sxs-lookup"><span data-stu-id="e33ca-165">yes</span></span>      |
<span data-ttu-id="e33ca-166">subject</span><span class="sxs-lookup"><span data-stu-id="e33ca-166">subject</span></span>      | <span data-ttu-id="e33ca-167">string</span><span class="sxs-lookup"><span data-stu-id="e33ca-167">string</span></span> | <span data-ttu-id="e33ca-168">sim</span><span class="sxs-lookup"><span data-stu-id="e33ca-168">yes</span></span>      | <span data-ttu-id="e33ca-169">O nome distinto da entidade do certificado</span><span class="sxs-lookup"><span data-stu-id="e33ca-169">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="e33ca-170">emissor</span><span class="sxs-lookup"><span data-stu-id="e33ca-170">issuer</span></span>       | <span data-ttu-id="e33ca-171">string</span><span class="sxs-lookup"><span data-stu-id="e33ca-171">string</span></span> | <span data-ttu-id="e33ca-172">sim</span><span class="sxs-lookup"><span data-stu-id="e33ca-172">yes</span></span>      | <span data-ttu-id="e33ca-173">O nome distinto do emissor do certificado</span><span class="sxs-lookup"><span data-stu-id="e33ca-173">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="e33ca-174">notBefore</span><span class="sxs-lookup"><span data-stu-id="e33ca-174">notBefore</span></span>    | <span data-ttu-id="e33ca-175">string</span><span class="sxs-lookup"><span data-stu-id="e33ca-175">string</span></span> | <span data-ttu-id="e33ca-176">sim</span><span class="sxs-lookup"><span data-stu-id="e33ca-176">yes</span></span>      | <span data-ttu-id="e33ca-177">O carimbo de data/hora inicial do período de validade do certificado</span><span class="sxs-lookup"><span data-stu-id="e33ca-177">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="e33ca-178">notAfter</span><span class="sxs-lookup"><span data-stu-id="e33ca-178">notAfter</span></span>     | <span data-ttu-id="e33ca-179">string</span><span class="sxs-lookup"><span data-stu-id="e33ca-179">string</span></span> | <span data-ttu-id="e33ca-180">sim</span><span class="sxs-lookup"><span data-stu-id="e33ca-180">yes</span></span>      | <span data-ttu-id="e33ca-181">O carimbo de data/hora final do período de validade do certificado</span><span class="sxs-lookup"><span data-stu-id="e33ca-181">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="e33ca-182">Observe que o `contentUrl` é necessário para ser servido por HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e33ca-182">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="e33ca-183">Esta URL não tem um padrão de URL específico e deve ser descoberta dinamicamente usando este documento de índice de assinaturas de repositório.</span><span class="sxs-lookup"><span data-stu-id="e33ca-183">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="e33ca-184">Todas as propriedades neste objeto (além de `contentUrl` ) devem ser derivadas do certificado encontrado em `contentUrl` .</span><span class="sxs-lookup"><span data-stu-id="e33ca-184">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="e33ca-185">Essas propriedades que podem ser derivadas são fornecidas como uma conveniência para minimizar viagens de ida e volta.</span><span class="sxs-lookup"><span data-stu-id="e33ca-185">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="e33ca-186">O objeto `fingerprints` tem as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="e33ca-186">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="e33ca-187">Nome</span><span class="sxs-lookup"><span data-stu-id="e33ca-187">Name</span></span>                   | <span data-ttu-id="e33ca-188">Type</span><span class="sxs-lookup"><span data-stu-id="e33ca-188">Type</span></span>   | <span data-ttu-id="e33ca-189">Necessária</span><span class="sxs-lookup"><span data-stu-id="e33ca-189">Required</span></span> | <span data-ttu-id="e33ca-190">Observações</span><span class="sxs-lookup"><span data-stu-id="e33ca-190">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="e33ca-191">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="e33ca-191">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="e33ca-192">string</span><span class="sxs-lookup"><span data-stu-id="e33ca-192">string</span></span> | <span data-ttu-id="e33ca-193">sim</span><span class="sxs-lookup"><span data-stu-id="e33ca-193">yes</span></span>      | <span data-ttu-id="e33ca-194">A impressão digital SHA-256</span><span class="sxs-lookup"><span data-stu-id="e33ca-194">The SHA-256 fingerprint</span></span>

<span data-ttu-id="e33ca-195">O nome da chave `2.16.840.1.101.3.4.2.1` é o OID do algoritmo de hash SHA-256.</span><span class="sxs-lookup"><span data-stu-id="e33ca-195">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="e33ca-196">Todos os valores de hash devem ser letras minúsculas, de cadeia de caracteres codificadas em hexadecimal do Resumo de hash.</span><span class="sxs-lookup"><span data-stu-id="e33ca-196">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="e33ca-197">Solicitação de exemplo</span><span class="sxs-lookup"><span data-stu-id="e33ca-197">Sample request</span></span>

```
GET https://api.nuget.org/v3-index/repository-signatures/index.json
```

### <a name="sample-response"></a><span data-ttu-id="e33ca-198">Resposta de exemplo</span><span class="sxs-lookup"><span data-stu-id="e33ca-198">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
