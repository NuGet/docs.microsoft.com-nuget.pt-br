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
ms.openlocfilehash: 32dd2ee19261488a2b1b92724095a11ced69ae68
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/21/2018
ms.locfileid: "42793201"
---
# <a name="repository-signatures"></a>Assinaturas de repositório

Se uma origem de pacote dá suporte a assinaturas de repositório de adição para pacotes publicados, é possível que um cliente para determinar os certificados de autenticação que são usados por origem do pacote. Esse recurso permite que os clientes detectar se um repositório assinado o pacote foi violado ou tem um certificado de autenticação inesperado.

O recurso usado para buscar informações de assinatura esse repositório é o `RepositorySignatures` recurso encontrado na [índice de serviço](service-index.md).

> [!Note]
> NuGet.org iniciará anunciando o `RepositorySignatures` recursos em um futuro próximo.

## <a name="versioning"></a>Controle de versão

O seguinte `@type` valor é usado:

Valor @type                | Observações
-------------------------- | -----
RepositorySignatures/4.7.0 | A versão inicial

## <a name="base-url"></a>URL Base

A URL de ponto de entrada para as seguintes APIs é o valor da `@id` propriedade associada ao recurso mencionados anteriormente `@type` valor. Este tópico usa a URL de espaço reservado `{@id}`.

Observe que, ao contrário de outros recursos, o `{@id}` URL é necessária para ser atendida por HTTPS.

## <a name="http-methods"></a>Métodos HTTP

Todas as URLs encontradas nos métodos de suporte apenas o HTTP de recurso de assinaturas de repositório `GET` e `HEAD`.

## <a name="repository-signatures-index"></a>Índice de assinaturas do repositório

O índice de assinaturas do repositório contém duas informações:

1. Se deseja ou não todos os pacotes encontrados na origem são assinado por essa fonte de pacote do repositório.
1. A lista de certificados usada pela origem do pacote para assinar pacotes.

Na maioria dos casos, a lista de certificados só será acrescentada ao. Novos certificados seriam adicionados à lista quando o certificado de autenticação anterior expirou e a origem do pacote precisa começar a usar um novo certificado de assinatura. Se um certificado for removido da lista, o que significa que todas as assinaturas de pacote criadas com o certificado de autenticação removido devem não ser consideradas válidas pelo cliente. Nesse caso, a assinatura do pacote (mas não necessariamente o pacote) é inválido. Uma política de cliente pode permitir que a instalação do pacote como não assinados.

No caso de revogação de certificado (comprometimento da chave, por exemplo,), a origem do pacote é esperada para assinar novamente todos os pacotes assinados pelo certificado afetado. Além disso, a origem do pacote deve remover o certificado afetado da lista de certificados de assinatura.

A seguinte solicitação de busca de índice de assinaturas do repositório.

    GET {@id}

O índice de assinatura do repositório é um documento JSON que contém um objeto com as seguintes propriedades:

Nome                | Tipo             | Necessária
------------------- | ---------------- | --------
allRepositorySigned | boolean          | sim
signingCertificates | matriz de objetos | sim

O `allRepositorySigned` booliano é definido como false se a origem do pacote tem alguns pacotes que não têm a nenhuma assinatura do repositório. Se o valor booliano é definido como true, todos os pacotes disponíveis na fonte de deve ter uma assinatura de repositório produzida por um dos certificados de autenticação mencionados no `signingCertificates`.

Deve haver um ou mais certificados de autenticação na `signingCertificates` matriz se o `allRepositorySigned` booliano é definido como true. Se a matriz está vazia e `allRepositorySigned` é definido como true, todos os pacotes da origem devem ser considerados inválidos, embora uma política de cliente ainda pode permitir que o consumo de pacotes. Cada elemento desta matriz é um objeto JSON com as propriedades a seguir.

Nome         | Tipo   | Necessária | Observações
------------ | ------ | -------- | -----
contentUrl   | cadeia de caracteres | sim      | URL absoluta para o certificado público codificado por DER
impressões digitais | objeto | sim      |
Assunto      | cadeia de caracteres | sim      | O nome diferenciado do assunto do certificado
emissor       | cadeia de caracteres | sim      | O nome diferenciado do emissor do certificado
notBefore    | cadeia de caracteres | sim      | O carimbo de hora de início do período de validade do certificado
notAfter     | cadeia de caracteres | sim      | O carimbo de hora de término do período de validade do certificado

Observe que o `contentUrl` deve ser atendida por HTTPS. Essa URL não tem nenhum padrão de URL específico e deve ser descoberta dinamicamente usando esse documento de índice de assinaturas do repositório. 

Todas as propriedades desse objeto (parte dos `contentUrl`) deve ser derivado do certificado encontrado em `contentUrl`.
Essas propriedades derivadas são fornecidas como uma conveniência para minimizar as viagens de ida e volta.

O `fingerprints` objeto tem as seguintes propriedades:

Nome                   | Tipo   | Necessária | Observações
---------------------- | ------ | -------- | -----
2.16.840.1.101.3.4.2.1 | cadeia de caracteres | sim      | A impressão digital de SHA-256

O nome da chave `2.16.840.1.101.3.4.2.1` é o OID do algoritmo de hash SHA-256.

Todos os valores de hash devem ser representações de cadeia de caracteres de letras minúsculas, com codificação hexadecimal do resumo do hash de.

### <a name="sample-request"></a>Exemplo de solicitação

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
