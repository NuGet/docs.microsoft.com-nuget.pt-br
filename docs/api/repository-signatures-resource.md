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
ms.openlocfilehash: ea318446c41a0d85d3fbf959dd38c929a0d0e9a1
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/11/2019
ms.locfileid: "59509016"
---
# <a name="repository-signatures"></a>Assinaturas de repositório

Se uma origem de pacote dá suporte a assinaturas de repositório de adição para pacotes publicados, é possível que um cliente para determinar os certificados de autenticação que são usados por origem do pacote. Esse recurso permite que os clientes detectar se um repositório assinado o pacote foi violado ou tem um certificado de autenticação inesperado.

O recurso usado para buscar informações de assinatura esse repositório é o `RepositorySignatures` recurso encontrado na [índice de serviço](service-index.md).

## <a name="versioning"></a>Controle de versão

O seguinte `@type` valor é usado:

Valor @type                | Observações
-------------------------- | -----
RepositorySignatures/4.7.0 | A versão inicial
RepositorySignatures/4.9.0 | Os clientes do NuGet v4.9 + com suporte
RepositorySignatures/5.0.0 | Permite habilitar `allRepositorySigned`. Os clientes do NuGet v 5.0 + com suporte

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

Nome                | Tipo             | Necessária | Observações
------------------- | ---------------- | -------- | -----
allRepositorySigned | boolean          | sim      | Deve ser `false` nos recursos 4.7.0 e 4.9.0
signingCertificates | matriz de objetos | sim      | 

O `allRepositorySigned` booliano é definido como false se a origem do pacote tem alguns pacotes que não têm a nenhuma assinatura do repositório. Se o valor booliano é definido como true, todos os pacotes disponíveis na fonte de deve ter uma assinatura de repositório produzida por um dos certificados de autenticação mencionados no `signingCertificates`.

> [!Warning]
> O `allRepositorySigned` booliano deve ser falsa nos recursos 4.7.0 e 4.9.0. Clientes do NuGet v4.7, v 4.8 e v4.9 não é possível instalar pacotes de fontes que têm `allRepositorySigned` definido como true.

Deve haver um ou mais certificados de autenticação na `signingCertificates` matriz se o `allRepositorySigned` booliano é definido como true. Se a matriz está vazia e `allRepositorySigned` é definido como true, todos os pacotes da origem devem ser considerados inválidos, embora uma política de cliente ainda pode permitir que o consumo de pacotes. Cada elemento desta matriz é um objeto JSON com as propriedades a seguir.

Nome         | Tipo   | Necessária | Observações
------------ | ------ | -------- | -----
contentUrl   | cadeia de caracteres | sim      | URL absoluta para o certificado público codificado por DER
fingerprints | objeto | sim      |
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
