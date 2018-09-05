---
title: Assinaturas de repositório, a API do NuGet | Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: O recurso de assinaturas do repositório permite que os clientes origens de pacote em anunciar o seu repositório de recursos de assinatura.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 50f309b99d4bf59e14f3e29b6b0421d8c3e8aa5a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547975"
---
# <a name="repository-signatures"></a><span data-ttu-id="e8b32-103">Assinaturas de repositório</span><span class="sxs-lookup"><span data-stu-id="e8b32-103">Repository signatures</span></span>

<span data-ttu-id="e8b32-104">Se uma origem de pacote dá suporte a assinaturas de repositório de adição para pacotes publicados, é possível que um cliente para determinar os certificados de autenticação que são usados por origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="e8b32-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="e8b32-105">Esse recurso permite que os clientes detectar se um repositório assinado o pacote foi violado ou tem um certificado de autenticação inesperado.</span><span class="sxs-lookup"><span data-stu-id="e8b32-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="e8b32-106">O recurso usado para buscar informações de assinatura esse repositório é o `RepositorySignatures` recurso encontrado na [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="e8b32-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

> [!Note]
> <span data-ttu-id="e8b32-107">NuGet.org iniciará anunciando o `RepositorySignatures` recursos em um futuro próximo.</span><span class="sxs-lookup"><span data-stu-id="e8b32-107">NuGet.org will start announcing the `RepositorySignatures` resource in the near future.</span></span>

## <a name="versioning"></a><span data-ttu-id="e8b32-108">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="e8b32-108">Versioning</span></span>

<span data-ttu-id="e8b32-109">O seguinte `@type` valor é usado:</span><span class="sxs-lookup"><span data-stu-id="e8b32-109">The following `@type` value is used:</span></span>

<span data-ttu-id="e8b32-110">Valor @type</span><span class="sxs-lookup"><span data-stu-id="e8b32-110">@type value</span></span>                | <span data-ttu-id="e8b32-111">Observações</span><span class="sxs-lookup"><span data-stu-id="e8b32-111">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="e8b32-112">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="e8b32-112">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="e8b32-113">A versão inicial</span><span class="sxs-lookup"><span data-stu-id="e8b32-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="e8b32-114">URL Base</span><span class="sxs-lookup"><span data-stu-id="e8b32-114">Base URL</span></span>

<span data-ttu-id="e8b32-115">A URL de ponto de entrada para as seguintes APIs é o valor da `@id` propriedade associada ao recurso mencionados anteriormente `@type` valor.</span><span class="sxs-lookup"><span data-stu-id="e8b32-115">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="e8b32-116">Este tópico usa a URL de espaço reservado `{@id}`.</span><span class="sxs-lookup"><span data-stu-id="e8b32-116">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="e8b32-117">Observe que, ao contrário de outros recursos, o `{@id}` URL é necessária para ser atendida por HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e8b32-117">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="e8b32-118">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="e8b32-118">HTTP methods</span></span>

<span data-ttu-id="e8b32-119">Todas as URLs encontradas nos métodos de suporte apenas o HTTP de recurso de assinaturas de repositório `GET` e `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="e8b32-119">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="e8b32-120">Índice de assinaturas do repositório</span><span class="sxs-lookup"><span data-stu-id="e8b32-120">Repository signatures index</span></span>

<span data-ttu-id="e8b32-121">O índice de assinaturas do repositório contém duas informações:</span><span class="sxs-lookup"><span data-stu-id="e8b32-121">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="e8b32-122">Se deseja ou não todos os pacotes encontrados na origem são assinado por essa fonte de pacote do repositório.</span><span class="sxs-lookup"><span data-stu-id="e8b32-122">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="e8b32-123">A lista de certificados usada pela origem do pacote para assinar pacotes.</span><span class="sxs-lookup"><span data-stu-id="e8b32-123">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="e8b32-124">Na maioria dos casos, a lista de certificados só será acrescentada ao.</span><span class="sxs-lookup"><span data-stu-id="e8b32-124">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="e8b32-125">Novos certificados seriam adicionados à lista quando o certificado de autenticação anterior expirou e a origem do pacote precisa começar a usar um novo certificado de assinatura.</span><span class="sxs-lookup"><span data-stu-id="e8b32-125">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="e8b32-126">Se um certificado for removido da lista, o que significa que todas as assinaturas de pacote criadas com o certificado de autenticação removido devem não ser consideradas válidas pelo cliente.</span><span class="sxs-lookup"><span data-stu-id="e8b32-126">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="e8b32-127">Nesse caso, a assinatura do pacote (mas não necessariamente o pacote) é inválido.</span><span class="sxs-lookup"><span data-stu-id="e8b32-127">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="e8b32-128">Uma política de cliente pode permitir que a instalação do pacote como não assinados.</span><span class="sxs-lookup"><span data-stu-id="e8b32-128">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="e8b32-129">No caso de revogação de certificado (comprometimento da chave, por exemplo,), a origem do pacote é esperada para assinar novamente todos os pacotes assinados pelo certificado afetado.</span><span class="sxs-lookup"><span data-stu-id="e8b32-129">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="e8b32-130">Além disso, a origem do pacote deve remover o certificado afetado da lista de certificados de assinatura.</span><span class="sxs-lookup"><span data-stu-id="e8b32-130">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="e8b32-131">A seguinte solicitação de busca de índice de assinaturas do repositório.</span><span class="sxs-lookup"><span data-stu-id="e8b32-131">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="e8b32-132">O índice de assinatura do repositório é um documento JSON que contém um objeto com as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="e8b32-132">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="e8b32-133">Nome</span><span class="sxs-lookup"><span data-stu-id="e8b32-133">Name</span></span>                | <span data-ttu-id="e8b32-134">Tipo</span><span class="sxs-lookup"><span data-stu-id="e8b32-134">Type</span></span>             | <span data-ttu-id="e8b32-135">Necessária</span><span class="sxs-lookup"><span data-stu-id="e8b32-135">Required</span></span>
------------------- | ---------------- | --------
<span data-ttu-id="e8b32-136">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="e8b32-136">allRepositorySigned</span></span> | <span data-ttu-id="e8b32-137">boolean</span><span class="sxs-lookup"><span data-stu-id="e8b32-137">boolean</span></span>          | <span data-ttu-id="e8b32-138">sim</span><span class="sxs-lookup"><span data-stu-id="e8b32-138">yes</span></span>
<span data-ttu-id="e8b32-139">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="e8b32-139">signingCertificates</span></span> | <span data-ttu-id="e8b32-140">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="e8b32-140">array of objects</span></span> | <span data-ttu-id="e8b32-141">sim</span><span class="sxs-lookup"><span data-stu-id="e8b32-141">yes</span></span>

<span data-ttu-id="e8b32-142">O `allRepositorySigned` booliano é definido como false se a origem do pacote tem alguns pacotes que não têm a nenhuma assinatura do repositório.</span><span class="sxs-lookup"><span data-stu-id="e8b32-142">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="e8b32-143">Se o valor booliano é definido como true, todos os pacotes disponíveis na fonte de deve ter uma assinatura de repositório produzida por um dos certificados de autenticação mencionados no `signingCertificates`.</span><span class="sxs-lookup"><span data-stu-id="e8b32-143">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

<span data-ttu-id="e8b32-144">Deve haver um ou mais certificados de autenticação na `signingCertificates` matriz se o `allRepositorySigned` booliano é definido como true.</span><span class="sxs-lookup"><span data-stu-id="e8b32-144">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="e8b32-145">Se a matriz está vazia e `allRepositorySigned` é definido como true, todos os pacotes da origem devem ser considerados inválidos, embora uma política de cliente ainda pode permitir que o consumo de pacotes.</span><span class="sxs-lookup"><span data-stu-id="e8b32-145">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="e8b32-146">Cada elemento desta matriz é um objeto JSON com as propriedades a seguir.</span><span class="sxs-lookup"><span data-stu-id="e8b32-146">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="e8b32-147">Nome</span><span class="sxs-lookup"><span data-stu-id="e8b32-147">Name</span></span>         | <span data-ttu-id="e8b32-148">Tipo</span><span class="sxs-lookup"><span data-stu-id="e8b32-148">Type</span></span>   | <span data-ttu-id="e8b32-149">Necessária</span><span class="sxs-lookup"><span data-stu-id="e8b32-149">Required</span></span> | <span data-ttu-id="e8b32-150">Observações</span><span class="sxs-lookup"><span data-stu-id="e8b32-150">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="e8b32-151">contentUrl</span><span class="sxs-lookup"><span data-stu-id="e8b32-151">contentUrl</span></span>   | <span data-ttu-id="e8b32-152">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e8b32-152">string</span></span> | <span data-ttu-id="e8b32-153">sim</span><span class="sxs-lookup"><span data-stu-id="e8b32-153">yes</span></span>      | <span data-ttu-id="e8b32-154">URL absoluta para o certificado público codificado por DER</span><span class="sxs-lookup"><span data-stu-id="e8b32-154">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="e8b32-155">impressões digitais</span><span class="sxs-lookup"><span data-stu-id="e8b32-155">fingerprints</span></span> | <span data-ttu-id="e8b32-156">objeto</span><span class="sxs-lookup"><span data-stu-id="e8b32-156">object</span></span> | <span data-ttu-id="e8b32-157">sim</span><span class="sxs-lookup"><span data-stu-id="e8b32-157">yes</span></span>      |
<span data-ttu-id="e8b32-158">Assunto</span><span class="sxs-lookup"><span data-stu-id="e8b32-158">subject</span></span>      | <span data-ttu-id="e8b32-159">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e8b32-159">string</span></span> | <span data-ttu-id="e8b32-160">sim</span><span class="sxs-lookup"><span data-stu-id="e8b32-160">yes</span></span>      | <span data-ttu-id="e8b32-161">O nome diferenciado do assunto do certificado</span><span class="sxs-lookup"><span data-stu-id="e8b32-161">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="e8b32-162">emissor</span><span class="sxs-lookup"><span data-stu-id="e8b32-162">issuer</span></span>       | <span data-ttu-id="e8b32-163">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e8b32-163">string</span></span> | <span data-ttu-id="e8b32-164">sim</span><span class="sxs-lookup"><span data-stu-id="e8b32-164">yes</span></span>      | <span data-ttu-id="e8b32-165">O nome diferenciado do emissor do certificado</span><span class="sxs-lookup"><span data-stu-id="e8b32-165">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="e8b32-166">notBefore</span><span class="sxs-lookup"><span data-stu-id="e8b32-166">notBefore</span></span>    | <span data-ttu-id="e8b32-167">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e8b32-167">string</span></span> | <span data-ttu-id="e8b32-168">sim</span><span class="sxs-lookup"><span data-stu-id="e8b32-168">yes</span></span>      | <span data-ttu-id="e8b32-169">O carimbo de hora de início do período de validade do certificado</span><span class="sxs-lookup"><span data-stu-id="e8b32-169">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="e8b32-170">notAfter</span><span class="sxs-lookup"><span data-stu-id="e8b32-170">notAfter</span></span>     | <span data-ttu-id="e8b32-171">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e8b32-171">string</span></span> | <span data-ttu-id="e8b32-172">sim</span><span class="sxs-lookup"><span data-stu-id="e8b32-172">yes</span></span>      | <span data-ttu-id="e8b32-173">O carimbo de hora de término do período de validade do certificado</span><span class="sxs-lookup"><span data-stu-id="e8b32-173">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="e8b32-174">Observe que o `contentUrl` deve ser atendida por HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e8b32-174">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="e8b32-175">Essa URL não tem nenhum padrão de URL específico e deve ser descoberta dinamicamente usando esse documento de índice de assinaturas do repositório.</span><span class="sxs-lookup"><span data-stu-id="e8b32-175">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="e8b32-176">Todas as propriedades desse objeto (parte dos `contentUrl`) deve ser derivado do certificado encontrado em `contentUrl`.</span><span class="sxs-lookup"><span data-stu-id="e8b32-176">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="e8b32-177">Essas propriedades derivadas são fornecidas como uma conveniência para minimizar as viagens de ida e volta.</span><span class="sxs-lookup"><span data-stu-id="e8b32-177">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="e8b32-178">O `fingerprints` objeto tem as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="e8b32-178">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="e8b32-179">Nome</span><span class="sxs-lookup"><span data-stu-id="e8b32-179">Name</span></span>                   | <span data-ttu-id="e8b32-180">Tipo</span><span class="sxs-lookup"><span data-stu-id="e8b32-180">Type</span></span>   | <span data-ttu-id="e8b32-181">Necessária</span><span class="sxs-lookup"><span data-stu-id="e8b32-181">Required</span></span> | <span data-ttu-id="e8b32-182">Observações</span><span class="sxs-lookup"><span data-stu-id="e8b32-182">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="e8b32-183">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="e8b32-183">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="e8b32-184">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e8b32-184">string</span></span> | <span data-ttu-id="e8b32-185">sim</span><span class="sxs-lookup"><span data-stu-id="e8b32-185">yes</span></span>      | <span data-ttu-id="e8b32-186">A impressão digital de SHA-256</span><span class="sxs-lookup"><span data-stu-id="e8b32-186">The SHA-256 fingerprint</span></span>

<span data-ttu-id="e8b32-187">O nome da chave `2.16.840.1.101.3.4.2.1` é o OID do algoritmo de hash SHA-256.</span><span class="sxs-lookup"><span data-stu-id="e8b32-187">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="e8b32-188">Todos os valores de hash devem ser representações de cadeia de caracteres de letras minúsculas, com codificação hexadecimal do resumo do hash de.</span><span class="sxs-lookup"><span data-stu-id="e8b32-188">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="e8b32-189">Exemplo de solicitação</span><span class="sxs-lookup"><span data-stu-id="e8b32-189">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="e8b32-190">Resposta de exemplo</span><span class="sxs-lookup"><span data-stu-id="e8b32-190">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
