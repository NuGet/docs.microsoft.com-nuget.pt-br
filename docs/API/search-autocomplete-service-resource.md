---
title: "Preenchimento automático, o NuGet API | Microsoft Docs"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "O serviço de preenchimento automático de pesquisa oferece suporte a versões e descoberta interativa de IDs de pacote."
keywords: "API de preenchimento automático do NuGet, NuGet pacote ID, ID de pacote de subcadeia de caracteres de pesquisa"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 7c984ca61799293d7832851b80cf3fefc4734288
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="autocomplete"></a>Preenchimento Automático

É possível criar um pacote ID e a versão AutoCompletar experiência usando a API V3. O recurso usado para fazer consultas de preenchimento automático é o `SearchAutocompleteService` recurso encontrado na [índice de serviço](service-index.md).

## <a name="versioning"></a>Controle de versão

O seguinte `@type` valores são usados:

Valor @type                          | Observações
------------------------------------ | -----
SearchAutocompleteService            | A versão inicial
SearchAutocompleteService/3.0.0-beta | Alias de`SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | Alias de`SearchAutocompleteService`

## <a name="base-url"></a>URL Base

A URL base para as seguintes APIs é o valor da `@id` propriedade associada a um recurso mencionados acima `@type` valores. No documento a seguir, a URL base do espaço reservado `{@id}` será usado.

## <a name="http-methods"></a>Métodos HTTP

Todas as URLs encontradas no suporte a recurso de registro os métodos HTTP `GET` e `HEAD`.

## <a name="search-for-package-ids"></a>Pesquise IDs de pacote

O preenchimento automático de primeira API dá suporte ao procurar por parte de uma cadeia de caracteres de ID do pacote. Isso é ótimo quando você deseja fornecer um recurso de typeahead do pacote em uma interface de usuário integrada com uma origem de pacote do NuGet.

Um pacote com apenas as versões não aparecerão nos resultados.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parâmetros de solicitação

Nome        | No     | Tipo    | Necessária | Observações
----------- | ------ | ------- | -------- | -----
q           | URL    | cadeia de caracteres  | no       | A cadeia de caracteres a ser comparada com IDs de pacote
skip        | URL    | inteiro | no       | O número de resultados a ignorar, de paginação
Take        | URL    | inteiro | no       | O número de resultados para retornar para a paginação
versão de pré-lançamento  | URL    | boolean | no       | `true`ou `false` determinar a inclusão [pacotes de pré-lançamento](../create-packages/prerelease-packages.md)
semVerLevel | URL    | cadeia de caracteres  | no       | Uma cadeia de caracteres de versão SemVer 1.0.0 

A consulta de preenchimento automático `q` é analisado em uma maneira que é definida pela implementação do servidor. NuGet.org oferece suporte a consultas para o prefixo de tokens de ID de pacote, que fazem parte da ID produzido pelo spliting original por caracteres mista de caso e o símbolo.

O `skip` parâmetro padrão é 0.

O `take` parâmetro deve ser um inteiro maior que zero. A implementação do servidor pode impor um valor máximo.

Se `prerelease` não for fornecido, os pacotes de pré-lançamento serão excluídos.

O `semVerLevel` parâmetro de consulta é usado para aceitar [SemVer 2.0.0 pacotes](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Se esse parâmetro de consulta é excluído, IDs de pacote somente com as versões compatíveis do SemVer 1.0.0 será retornado (com o [padrão controle de versão do NuGet](../reference/package-versioning.md) limitações, como cadeias de caracteres de versão com 4 partes de inteiro).
Se `semVerLevel=2.0.0` for fornecido, SemVer 1.0.0 e pacotes compatíveis SemVer 2.0.0 serão retornados. Consulte o [suporte SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obter mais informações.

### <a name="response"></a>Resposta

A resposta é documento JSON que contém até `take` resultados de preenchimento automático.

A raiz do objeto JSON tem as seguintes propriedades:

Nome      | Tipo             | Necessária | Observações
--------- | ---------------- | -------- | -----
totalHits | inteiro          | sim      | O número total de correspondências, desconsiderando `skip` e`take`
Dados      | Matriz de cadeias de caracteres | sim      | O pacote correspondem às IDs de solicitação

### <a name="sample-request"></a>Solicitação de amostra

GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Enumerar as versões do pacote

Depois que uma ID de pacote for descoberta usando a API anterior, um cliente pode usar o API de preenchimento automático para enumerar as versões do pacote para uma ID do pacote fornecido.

Uma versão do pacote que está na lista não aparecerão nos resultados.

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parâmetros de solicitação

Nome        | No     | Tipo    | Necessária | Observações
----------- | ------ | ------- | -------- | -----
id          | URL    | cadeia de caracteres  | sim      | A ID do pacote para buscar versões para
versão de pré-lançamento  | URL    | boolean | no       | `true`ou `false` determinar a inclusão [pacotes de pré-lançamento](../create-packages/prerelease-packages.md)
semVerLevel | URL    | cadeia de caracteres  | no       | Uma cadeia de caracteres de versão SemVer 2.0.0 

Se `prerelease` não for fornecido, os pacotes de pré-lançamento serão excluídos.

O `semVerLevel` parâmetro de consulta é usado para aceitar a SemVer 2.0.0 pacotes. Se esse parâmetro de consulta é excluído, apenas as versões SemVer 1.0.0 serão retornadas. Se `semVerLevel=2.0.0` for fornecido, SemVer 1.0.0 e SemVer 2.0.0 versões serão retornadas. Consulte o [suporte SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obter mais informações.

### <a name="response"></a>Resposta

A resposta é documento JSON que contém todas as versões do pacote da ID do pacote fornecido, filtrando os parâmetros de consulta.

A raiz do objeto JSON tem a seguinte propriedade:

Nome      | Tipo             | Necessária | Observações
--------- | ---------------- | -------- | -----
Dados      | Matriz de cadeias de caracteres | sim      | As versões do pacote correspondidas a solicitação

As versões do pacote no `data` matriz pode conter metadados de compilação SemVer 2.0.0 (por exemplo, `1.0.0+metadata`) se o `semVerLevel=2.0.0` foi fornecido na cadeia de caracteres de consulta.

### <a name="sample-request"></a>Solicitação de amostra

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
