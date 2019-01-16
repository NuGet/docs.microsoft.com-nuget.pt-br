---
title: Preenchimento automático, API do NuGet
description: O serviço de preenchimento automático de pesquisa dá suporte a versões e descoberta interativa de IDs de pacote.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2d2b20c1ea439ec0a3225cf983d9a4d2eedb0333
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324754"
---
# <a name="autocomplete"></a>Preenchimento Automático

É possível criar um pacote ID e a versão AutoCompletar experiência usando a API V3. O recurso usado para fazer consultas de preenchimento automático é o `SearchAutocompleteService` recurso encontrado na [índice de serviço](service-index.md).

## <a name="versioning"></a>Controle de versão

O seguinte `@type` valores são usados:

Valor @type                          | Observações
------------------------------------ | -----
SearchAutocompleteService            | A versão inicial
SearchAutocompleteService/3.0.0-beta | Alias of `SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | Alias of `SearchAutocompleteService`

## <a name="base-url"></a>URL Base

A URL base para as APIs a seguir é o valor da `@id` propriedade associada a um do recurso mencionados anteriormente `@type` valores. O seguinte documento, o espaço reservado de URL de base `{@id}` será usado.

## <a name="http-methods"></a>Métodos HTTP

Todas as URLs encontradas no suporte a recursos de registro os métodos HTTP `GET` e `HEAD`.

## <a name="search-for-package-ids"></a>Procure as IDs de pacote

O preenchimento automático de primeira API dá suporte a procurar por parte de uma cadeia de caracteres de ID do pacote. Isso é ótimo quando você deseja fornecer um recurso de digitação antecipada de pacote em uma interface de usuário integrada com uma origem de pacote do NuGet.

Um pacote com apenas as versões não listados não aparecerão nos resultados.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parâmetros de solicitação

Nome        | No     | Tipo    | Necessária | Observações
----------- | ------ | ------- | -------- | -----
q           | URL    | cadeia de caracteres  | no       | A cadeia de caracteres a ser comparada com as IDs de pacote
skip        | URL    | inteiro | no       | O número de resultados a ignorar, para paginação
Take        | URL    | inteiro | no       | O número de resultados a serem retornados para a paginação
versão de pré-lançamento  | URL    | boolean | no       | `true` ou `false` determinar se é necessário incluir [pacotes de pré-lançamento](../create-packages/prerelease-packages.md)
semVerLevel | URL    | cadeia de caracteres  | no       | Uma cadeia de caracteres de versão 1.0.0 de SemVer 

A consulta de preenchimento automático `q` é analisado de uma maneira que é definida pela implementação do servidor. NuGet.org dá suporte à consulta para o prefixo de tokens de ID de pacote, que são partes da ID produzido pelo dividindo original pela concatenação com caracteres de símbolo e caso.

O `skip` parâmetro padrão é 0.

O `take` parâmetro deve ser um inteiro maior que zero. A implementação do servidor pode impor um valor máximo.

Se `prerelease` não for fornecido, pacotes de pré-lançamento são excluídos.

O `semVerLevel` parâmetro de consulta é usado para participar [SemVer 2.0.0 pacotes](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Se esse parâmetro de consulta é excluído, as IDs de pacote somente com as versões compatíveis do SemVer 1.0.0 serão retornada (com o [padrão controle de versão do NuGet](../reference/package-versioning.md) advertências, como cadeias de caracteres de versão com partes de inteiro de 4).
Se `semVerLevel=2.0.0` for fornecido, SemVer 1.0.0 e pacotes de SemVer 2.0.0 compatíveis serão retornados. Consulte a [SemVer 2.0.0 suporte para nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obter mais informações.

### <a name="response"></a>Resposta

A resposta é o documento JSON que contém até `take` resultados de preenchimento automático.

O objeto JSON de raiz tem as seguintes propriedades:

Nome      | Tipo             | Necessária | Observações
--------- | ---------------- | -------- | -----
totalHits | inteiro          | sim      | O número total de correspondências, desconsiderando `skip` e `take`
Dados      | matriz de cadeias de caracteres | sim      | O pacote IDs correspondidos pela solicitação

### <a name="sample-request"></a>Exemplo de solicitação

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Enumerar as versões do pacote

Quando uma ID de pacote for descoberta usando a API anterior, um cliente pode usar a API de preenchimento automático para enumerar as versões do pacote para uma ID do pacote fornecido.

Uma versão do pacote é removido da lista não aparecerão nos resultados.

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parâmetros de solicitação

Nome        | No     | Tipo    | Necessária | Observações
----------- | ------ | ------- | -------- | -----
id          | URL    | cadeia de caracteres  | sim      | A ID do pacote para buscar as versões para
versão de pré-lançamento  | URL    | boolean | no       | `true` ou `false` determinar se é necessário incluir [pacotes de pré-lançamento](../create-packages/prerelease-packages.md)
semVerLevel | URL    | cadeia de caracteres  | no       | Uma cadeia de caracteres de versão de SemVer 2.0.0 

Se `prerelease` não for fornecido, pacotes de pré-lançamento são excluídos.

O `semVerLevel` parâmetro de consulta é usado para participar de pacotes de SemVer 2.0.0. Se esse parâmetro de consulta é excluído, somente as versões de SemVer 1.0.0 serão retornadas. Se `semVerLevel=2.0.0` for fornecido, as versões de SemVer 2.0.0 e SemVer 1.0.0 serão retornadas. Consulte a [SemVer 2.0.0 suporte para nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obter mais informações.

### <a name="response"></a>Resposta

A resposta é um documento JSON que contém todas as versões de pacote da ID do pacote fornecido, filtrando por parâmetros de consulta fornecidos.

O objeto JSON de raiz tem a seguinte propriedade:

Nome      | Tipo             | Necessária | Observações
--------- | ---------------- | -------- | -----
Dados      | matriz de cadeias de caracteres | sim      | As versões do pacote correspondidas pela solicitação

As versões do pacote a `data` matriz pode conter metadados de compilação de SemVer 2.0.0 (por exemplo, `1.0.0+metadata`) se o `semVerLevel=2.0.0` foi fornecido na cadeia de caracteres de consulta.

### <a name="sample-request"></a>Exemplo de solicitação

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
