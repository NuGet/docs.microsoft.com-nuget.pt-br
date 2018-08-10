---
title: Assinaturas de repositório, a API do NuGet | Microsoft Docs
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 3/2/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: O recurso de assinaturas do repositório permite que os clientes origens de pacote em anunciar o seu repositório de recursos de assinatura.
keywords: Assinaturas de repositório de API do NuGet, nuget.org certificados de assinatura, assinatura do pacote nuget.org
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 27c572a482fef791f19b3d32e816a41d8dc40b53
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020550"
---
# <a name="repository-signatures"></a><span data-ttu-id="748b5-104">Assinaturas de repositório</span><span class="sxs-lookup"><span data-stu-id="748b5-104">Repository signatures</span></span>

<span data-ttu-id="748b5-105">Se uma origem de pacote dá suporte a assinaturas de repositório de adição para pacotes publicados, é possível que um cliente para determinar os certificados de autenticação que são usados por origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="748b5-105">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="748b5-106">Esse recurso permite que os clientes detectar se um repositório assinado o pacote foi violado ou tem um certificado de autenticação inesperado.</span><span class="sxs-lookup"><span data-stu-id="748b5-106">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="748b5-107">O recurso usado para buscar informações de assinatura esse repositório é o `RepositorySignatures` recurso encontrado na [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="748b5-107">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

> [!Note]
> <span data-ttu-id="748b5-108">NuGet.org iniciará anunciando o `RepositorySignatures` recursos em um futuro próximo.</span><span class="sxs-lookup"><span data-stu-id="748b5-108">NuGet.org will start announcing the `RepositorySignatures` resource in the near future.</span></span>

## <a name="versioning"></a><span data-ttu-id="748b5-109">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="748b5-109">Versioning</span></span>

<span data-ttu-id="748b5-110">O seguinte `@type` valor é usado:</span><span class="sxs-lookup"><span data-stu-id="748b5-110">The following `@type` value is used:</span></span>

<span data-ttu-id="748b5-111">Valor @type</span><span class="sxs-lookup"><span data-stu-id="748b5-111">@type value</span></span>                | <span data-ttu-id="748b5-112">Observações</span><span class="sxs-lookup"><span data-stu-id="748b5-112">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="748b5-113">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="748b5-113">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="748b5-114">A versão inicial</span><span class="sxs-lookup"><span data-stu-id="748b5-114">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="748b5-115">URL Base</span><span class="sxs-lookup"><span data-stu-id="748b5-115">Base URL</span></span>

<span data-ttu-id="748b5-116">A URL de ponto de entrada para as seguintes APIs é o valor da `@id` propriedade associada ao recurso mencionados anteriormente `@type` valor.</span><span class="sxs-lookup"><span data-stu-id="748b5-116">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="748b5-117">Este tópico usa a URL de espaço reservado `{@id}`.</span><span class="sxs-lookup"><span data-stu-id="748b5-117">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="748b5-118">Observe que, ao contrário de outros recursos, o `{@id}` URL é necessária para ser atendida por HTTPS.</span><span class="sxs-lookup"><span data-stu-id="748b5-118">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="748b5-119">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="748b5-119">HTTP methods</span></span>

<span data-ttu-id="748b5-120">Todas as URLs encontradas nos métodos de suporte apenas o HTTP de recurso de assinaturas de repositório `GET` e `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="748b5-120">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="748b5-121">Índice de assinaturas do repositório</span><span class="sxs-lookup"><span data-stu-id="748b5-121">Repository signatures index</span></span>

<span data-ttu-id="748b5-122">O índice de assinaturas do repositório contém duas informações:</span><span class="sxs-lookup"><span data-stu-id="748b5-122">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="748b5-123">Se deseja ou não todos os pacotes encontrados na origem são assinado por essa fonte de pacote do repositório.</span><span class="sxs-lookup"><span data-stu-id="748b5-123">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="748b5-124">A lista de certificados usada pela origem do pacote para assinar pacotes.</span><span class="sxs-lookup"><span data-stu-id="748b5-124">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="748b5-125">Na maioria dos casos, a lista de certificados só será acrescentada ao.</span><span class="sxs-lookup"><span data-stu-id="748b5-125">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="748b5-126">Novos certificados seriam adicionados à lista quando o certificado de autenticação anterior expirou e a origem do pacote precisa começar a usar um novo certificado de assinatura.</span><span class="sxs-lookup"><span data-stu-id="748b5-126">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="748b5-127">Se um certificado for removido da lista, o que significa que todas as assinaturas de pacote criadas com o certificado de autenticação removido devem não ser consideradas válidas pelo cliente.</span><span class="sxs-lookup"><span data-stu-id="748b5-127">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="748b5-128">Nesse caso, a assinatura do pacote (mas não necessariamente o pacote) é inválido.</span><span class="sxs-lookup"><span data-stu-id="748b5-128">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="748b5-129">Uma política de cliente pode permitir que a instalação do pacote como não assinados.</span><span class="sxs-lookup"><span data-stu-id="748b5-129">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="748b5-130">No caso de revogação de certificado (comprometimento da chave, por exemplo,), espera-se que a origem do pacote desistir de todos os pacotes assinados pelo certificado afetado.</span><span class="sxs-lookup"><span data-stu-id="748b5-130">In the case of certificate revocation (e.g. key compromise), the package source is expected to resign all packages signed by the affected certificate.</span></span> <span data-ttu-id="748b5-131">Além disso, a origem do pacote deve remover o certificado afetado da lista de certificados de assinatura.</span><span class="sxs-lookup"><span data-stu-id="748b5-131">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="748b5-132">A seguinte solicitação de busca de índice de assinaturas do repositório.</span><span class="sxs-lookup"><span data-stu-id="748b5-132">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="748b5-133">O índice de assinatura do repositório é um documento JSON que contém um objeto com as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="748b5-133">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="748b5-134">Nome</span><span class="sxs-lookup"><span data-stu-id="748b5-134">Name</span></span>                | <span data-ttu-id="748b5-135">Tipo</span><span class="sxs-lookup"><span data-stu-id="748b5-135">Type</span></span>             | <span data-ttu-id="748b5-136">Necessária</span><span class="sxs-lookup"><span data-stu-id="748b5-136">Required</span></span>
------------------- | ---------------- | --------
<span data-ttu-id="748b5-137">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="748b5-137">allRepositorySigned</span></span> | <span data-ttu-id="748b5-138">boolean</span><span class="sxs-lookup"><span data-stu-id="748b5-138">boolean</span></span>          | <span data-ttu-id="748b5-139">sim</span><span class="sxs-lookup"><span data-stu-id="748b5-139">yes</span></span>
<span data-ttu-id="748b5-140">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="748b5-140">signingCertificates</span></span> | <span data-ttu-id="748b5-141">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="748b5-141">array of objects</span></span> | <span data-ttu-id="748b5-142">sim</span><span class="sxs-lookup"><span data-stu-id="748b5-142">yes</span></span>

<span data-ttu-id="748b5-143">O `allRepositorySigned` booliano é definido como false se a origem do pacote tem alguns pacotes que não têm a nenhuma assinatura do repositório.</span><span class="sxs-lookup"><span data-stu-id="748b5-143">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="748b5-144">Se o valor booliano é definido como true, todos os pacotes disponíveis na fonte de deve ter uma assinatura de repositório produzida por um dos certificados de autenticação mencionados no `signingCertificates`.</span><span class="sxs-lookup"><span data-stu-id="748b5-144">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

<span data-ttu-id="748b5-145">Deve haver um ou mais certificados de autenticação na `signingCertificates` matriz se o `allRepositorySigned` booliano é definido como true.</span><span class="sxs-lookup"><span data-stu-id="748b5-145">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="748b5-146">Se a matriz está vazia e `allRepositorySigned` é definido como true, todos os pacotes da origem devem ser considerados inválidos, embora uma política de cliente ainda pode permitir que o consumo de pacotes.</span><span class="sxs-lookup"><span data-stu-id="748b5-146">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="748b5-147">Cada elemento desta matriz é um objeto JSON com as propriedades a seguir.</span><span class="sxs-lookup"><span data-stu-id="748b5-147">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="748b5-148">Nome</span><span class="sxs-lookup"><span data-stu-id="748b5-148">Name</span></span>         | <span data-ttu-id="748b5-149">Tipo</span><span class="sxs-lookup"><span data-stu-id="748b5-149">Type</span></span>   | <span data-ttu-id="748b5-150">Necessária</span><span class="sxs-lookup"><span data-stu-id="748b5-150">Required</span></span> | <span data-ttu-id="748b5-151">Observações</span><span class="sxs-lookup"><span data-stu-id="748b5-151">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="748b5-152">contentUrl</span><span class="sxs-lookup"><span data-stu-id="748b5-152">contentUrl</span></span>   | <span data-ttu-id="748b5-153">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="748b5-153">string</span></span> | <span data-ttu-id="748b5-154">sim</span><span class="sxs-lookup"><span data-stu-id="748b5-154">yes</span></span>      | <span data-ttu-id="748b5-155">URL absoluta para o certificado público codificado por DER</span><span class="sxs-lookup"><span data-stu-id="748b5-155">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="748b5-156">impressões digitais</span><span class="sxs-lookup"><span data-stu-id="748b5-156">fingerprints</span></span> | <span data-ttu-id="748b5-157">objeto</span><span class="sxs-lookup"><span data-stu-id="748b5-157">object</span></span> | <span data-ttu-id="748b5-158">sim</span><span class="sxs-lookup"><span data-stu-id="748b5-158">yes</span></span>      |
<span data-ttu-id="748b5-159">Assunto</span><span class="sxs-lookup"><span data-stu-id="748b5-159">subject</span></span>      | <span data-ttu-id="748b5-160">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="748b5-160">string</span></span> | <span data-ttu-id="748b5-161">sim</span><span class="sxs-lookup"><span data-stu-id="748b5-161">yes</span></span>      | <span data-ttu-id="748b5-162">O nome diferenciado do assunto do certificado</span><span class="sxs-lookup"><span data-stu-id="748b5-162">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="748b5-163">emissor</span><span class="sxs-lookup"><span data-stu-id="748b5-163">issuer</span></span>       | <span data-ttu-id="748b5-164">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="748b5-164">string</span></span> | <span data-ttu-id="748b5-165">sim</span><span class="sxs-lookup"><span data-stu-id="748b5-165">yes</span></span>      | <span data-ttu-id="748b5-166">O nome diferenciado do emissor do certificado</span><span class="sxs-lookup"><span data-stu-id="748b5-166">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="748b5-167">notBefore</span><span class="sxs-lookup"><span data-stu-id="748b5-167">notBefore</span></span>    | <span data-ttu-id="748b5-168">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="748b5-168">string</span></span> | <span data-ttu-id="748b5-169">sim</span><span class="sxs-lookup"><span data-stu-id="748b5-169">yes</span></span>      | <span data-ttu-id="748b5-170">O carimbo de hora de início do período de validade do certificado</span><span class="sxs-lookup"><span data-stu-id="748b5-170">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="748b5-171">notAfter</span><span class="sxs-lookup"><span data-stu-id="748b5-171">notAfter</span></span>     | <span data-ttu-id="748b5-172">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="748b5-172">string</span></span> | <span data-ttu-id="748b5-173">sim</span><span class="sxs-lookup"><span data-stu-id="748b5-173">yes</span></span>      | <span data-ttu-id="748b5-174">O carimbo de hora de término do período de validade do certificado</span><span class="sxs-lookup"><span data-stu-id="748b5-174">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="748b5-175">Observe que o `contentUrl` deve ser atendida por HTTPS.</span><span class="sxs-lookup"><span data-stu-id="748b5-175">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="748b5-176">Essa URL não tem nenhum padrão de URL específico e deve ser descoberta dinamicamente usando esse documento de índice de assinaturas do repositório.</span><span class="sxs-lookup"><span data-stu-id="748b5-176">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="748b5-177">Todas as propriedades desse objeto (parte dos `contentUrl`) deve ser derivado do certificado encontrado em `contentUrl`.</span><span class="sxs-lookup"><span data-stu-id="748b5-177">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="748b5-178">Essas propriedades derivadas são fornecidas como uma conveniência para minimizar as viagens de ida e volta.</span><span class="sxs-lookup"><span data-stu-id="748b5-178">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="748b5-179">O `fingerprints` objeto tem as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="748b5-179">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="748b5-180">Nome</span><span class="sxs-lookup"><span data-stu-id="748b5-180">Name</span></span>                   | <span data-ttu-id="748b5-181">Tipo</span><span class="sxs-lookup"><span data-stu-id="748b5-181">Type</span></span>   | <span data-ttu-id="748b5-182">Necessária</span><span class="sxs-lookup"><span data-stu-id="748b5-182">Required</span></span> | <span data-ttu-id="748b5-183">Observações</span><span class="sxs-lookup"><span data-stu-id="748b5-183">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="748b5-184">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="748b5-184">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="748b5-185">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="748b5-185">string</span></span> | <span data-ttu-id="748b5-186">sim</span><span class="sxs-lookup"><span data-stu-id="748b5-186">yes</span></span>      | <span data-ttu-id="748b5-187">A impressão digital de SHA-256</span><span class="sxs-lookup"><span data-stu-id="748b5-187">The SHA-256 fingerprint</span></span>

<span data-ttu-id="748b5-188">O nome da chave `2.16.840.1.101.3.4.2.1` é o OID do algoritmo de hash SHA-256.</span><span class="sxs-lookup"><span data-stu-id="748b5-188">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="748b5-189">Todos os valores de hash devem ser representações de cadeia de caracteres de letras minúsculas, com codificação hexadecimal do resumo do hash de.</span><span class="sxs-lookup"><span data-stu-id="748b5-189">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="748b5-190">Exemplo de solicitação</span><span class="sxs-lookup"><span data-stu-id="748b5-190">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="748b5-191">Resposta de exemplo</span><span class="sxs-lookup"><span data-stu-id="748b5-191">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
