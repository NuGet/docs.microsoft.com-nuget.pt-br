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
# <a name="repository-signatures"></a>Assinaturas de repositório

Se uma origem de pacote oferecer suporte à adição de assinaturas de repositório a pacotes publicados, é possível para um cliente determinar os certificados de autenticação que são usados pela origem do pacote. Esse recurso permite que os clientes detectem se um pacote assinado por um repositório foi adulterado ou tem um certificado de assinatura inesperado.

O recurso usado para buscar essas informações de assinatura de repositório é o `RepositorySignatures` recurso encontrado no [índice de serviço](service-index.md).

## <a name="versioning"></a>Controle de versão

O seguinte `@type` valor é usado:

@type valor                | Observações
-------------------------- | -----
RepositorySignatures/4.7.0 | A versão inicial
RepositorySignatures/4.9.0 | Com suporte dos clientes NuGet v 4.9 +
RepositorySignatures/5.0.0 | Permite habilitar o `allRepositorySigned` . Compatível com clientes NuGet v 5.0 +

## <a name="base-url"></a>URL base

A URL do ponto de entrada para as seguintes APIs é o valor da `@id` propriedade associada ao valor de recurso mencionado anteriormente `@type` . Este tópico usa a URL do espaço reservado `{@id}` .

Observe que, ao contrário de outros recursos, `{@id}` é necessário que a URL seja servida via HTTPS.

## <a name="http-methods"></a>Métodos HTTP

Todas as URLs encontradas no recurso de assinaturas de repositório dão suporte apenas aos métodos HTTP `GET` e `HEAD` .

## <a name="repository-signatures-index"></a>Índice de assinaturas de repositório

O índice de assinaturas de repositório contém duas partes de informação:

1. Se todos os pacotes encontrados na origem são o repositório assinado por essa origem de pacote.
1. A lista de certificados usados pela origem do pacote para assinar pacotes.

Na maioria dos casos, a lista de certificados só será acrescentada a. Novos certificados seriam adicionados à lista quando o certificado de autenticação anterior tiver expirado e a origem do pacote precisar começar a usar um novo certificado de autenticação. Se um certificado for removido da lista, isso significa que todas as assinaturas de pacote criadas com o certificado de autenticação removido não devem mais ser consideradas válidas pelo cliente. Nesse caso, a assinatura do pacote (mas não necessariamente o pacote) é inválida. Uma política de cliente pode permitir a instalação do pacote como não assinado.

No caso de revogação de certificado (por exemplo, comprometimento de chave), espera-se que a origem do pacote assine novamente todos os pacotes assinados pelo certificado afetado. Além disso, a origem do pacote deve remover o certificado afetado da lista de certificados de autenticação.

A solicitação a seguir busca o índice de assinaturas de repositório.

```
GET {@id}
```

O índice de assinatura de repositório é um documento JSON que contém um objeto com as seguintes propriedades:

Nome                | Type             | Necessária | Observações
------------------- | ---------------- | -------- | -----
allRepositorySigned | booleano          | sim      | Deve estar `false` nos recursos 4.7.0 e 4.9.0
signingCertificates | matriz de objetos | sim      | 

O `allRepositorySigned` booliano será definido como false se a origem do pacote tiver alguns pacotes que não têm nenhuma assinatura de repositório. Se o booliano for definido como true, todos os pacotes disponíveis na origem deverão ter uma assinatura de repositório produzida por um dos certificados de autenticação mencionados em `signingCertificates` .

> [!Warning]
> O `allRepositorySigned` booliano deve ser falso nos recursos 4.7.0 e 4.9.0. Os clientes do NuGet v 4.7, v 4.8 e v 4.9 não podem instalar pacotes de fontes que foram `allRepositorySigned` definidas como true.

Deve haver um ou mais certificados de assinatura na `signingCertificates` matriz se o `allRepositorySigned` booliano estiver definido como true. Se a matriz estiver vazia e `allRepositorySigned` for definida como true, todos os pacotes da origem deverão ser considerados inválidos, embora uma política de cliente ainda possa permitir o consumo de pacotes. Cada elemento nessa matriz é um objeto JSON com as propriedades a seguir.

Nome         | Type   | Necessária | Observações
------------ | ------ | -------- | -----
contentUrl   | string | sim      | URL absoluta para o certificado público codificado em DER
marcas | objeto | sim      |
subject      | string | sim      | O nome distinto da entidade do certificado
emissor       | string | sim      | O nome distinto do emissor do certificado
notBefore    | string | sim      | O carimbo de data/hora inicial do período de validade do certificado
notAfter     | string | sim      | O carimbo de data/hora final do período de validade do certificado

Observe que o `contentUrl` é necessário para ser servido por HTTPS. Esta URL não tem um padrão de URL específico e deve ser descoberta dinamicamente usando este documento de índice de assinaturas de repositório. 

Todas as propriedades neste objeto (além de `contentUrl` ) devem ser derivadas do certificado encontrado em `contentUrl` .
Essas propriedades que podem ser derivadas são fornecidas como uma conveniência para minimizar viagens de ida e volta.

O objeto `fingerprints` tem as seguintes propriedades:

Nome                   | Type   | Necessária | Observações
---------------------- | ------ | -------- | -----
2.16.840.1.101.3.4.2.1 | string | sim      | A impressão digital SHA-256

O nome da chave `2.16.840.1.101.3.4.2.1` é o OID do algoritmo de hash SHA-256.

Todos os valores de hash devem ser letras minúsculas, de cadeia de caracteres codificadas em hexadecimal do Resumo de hash.

### <a name="sample-request"></a>Solicitação de exemplo

```
GET https://api.nuget.org/v3-index/repository-signatures/index.json
```

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
