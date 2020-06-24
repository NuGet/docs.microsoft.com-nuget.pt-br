---
title: Preenchimento automático, API do NuGet
description: O serviço de preenchimento automático de pesquisa dá suporte à descoberta interativa de IDs e versões de pacote.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: f574849bf99cd4da4eefd55c3dd5a0648042f0c1
ms.sourcegitcommit: 7e9c0630335ef9ec1e200e2ee9065f702e52a8ec
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85292287"
---
# <a name="autocomplete"></a>Preenchimento Automático

É possível criar uma ID do pacote e uma experiência de preenchimento automático da versão usando a API v3. O recurso usado para fazer consultas de preenchimento automático é o `SearchAutocompleteService` recurso encontrado no [índice de serviço](service-index.md).

## <a name="versioning"></a>Controle de versão

Os seguintes `@type` valores são usados:

@type valor                          | Observações
------------------------------------ | -----
SearchAutocompleteService            | A versão inicial
SearchAutocompleteService/3.0.0-beta | Alias de`SearchAutocompleteService`
SearchAutocompleteService/3.0.0-RC   | Alias de`SearchAutocompleteService`
SearchAutocompleteService/3.5.0      | Inclui suporte para `packageType` parâmetro de consulta

### <a name="searchautocompleteservice350"></a>SearchAutocompleteService/3.5.0
Esta versão apresenta suporte para o `packageType` parâmetro de consulta, permitindo a filtragem por tipos de pacote definidos pelo autor. Ele é totalmente compatível com consultas ao `SearchAutocompleteService` .

## <a name="base-url"></a>URL base

A URL base para as APIs a seguir é o valor da `@id` propriedade associada a um dos valores de recurso mencionados anteriormente `@type` . No documento a seguir, a URL base do espaço reservado `{@id}` será usada.

## <a name="http-methods"></a>Métodos HTTP

Todas as URLs encontradas no recurso de registro dão suporte aos métodos HTTP `GET` e `HEAD` .

## <a name="search-for-package-ids"></a>Pesquisar por IDs de pacote

A primeira API de preenchimento automático dá suporte à pesquisa de parte de uma cadeia de caracteres de ID de pacote. Isso é ótimo quando você deseja fornecer um recurso typeahead de pacote em uma interface de usuário integrada com uma origem de pacote NuGet.

Um pacote com apenas versões não listadas não será exibido nos resultados.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}

### <a name="request-parameters"></a>Parâmetros da solicitação

Nome        | Em     | Type    | Obrigatório | Observações
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | não       | A cadeia de caracteres para comparar com as IDs de pacote
skip        | URL    | inteiro | não       | O número de resultados a serem ignorados, para paginação
take        | URL    | inteiro | não       | O número de resultados a serem retornados, para paginação
prerelease  | URL    | booleano | não       | `true`ou `false` determinando se os [pacotes de pré-lançamento](../create-packages/prerelease-packages.md) devem ser incluídos
semVerLevel | URL    | string  | não       | Uma cadeia de versão do SemVer 1.0.0 
packageType | URL    | string  | não       | O tipo de pacote a ser usado para filtrar pacotes (adicionados em `SearchAutocompleteService/3.5.0` )

A consulta de preenchimento automático `q` é analisada de uma maneira que é definida pela implementação do servidor. o nuget.org dá suporte à consulta do prefixo dos tokens de ID do pacote, que são partes da ID produzida pela divisão do original por caracteres de letras e símbolos do Camel.

O `skip` padrão do parâmetro é 0.

O `take` parâmetro deve ser um número inteiro maior que zero. A implementação do servidor pode impor um valor máximo.

Se `prerelease` não for fornecido, os pacotes de pré-lançamento serão excluídos.

O `semVerLevel` parâmetro de consulta é usado para aceitar [pacotes SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Se esse parâmetro de consulta for excluído, somente as IDs de pacote com versões compatíveis do SemVer 1.0.0 serão retornadas (com as advertências de [versão padrão do NuGet](../concepts/package-versioning.md) , como cadeias de caracteres de versão com 4 partes de inteiros).
Se `semVerLevel=2.0.0` for fornecido, os pacotes compatíveis SemVer 1.0.0 e SemVer 2.0.0 serão retornados. Consulte o [SemVer 2.0.0 support for NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obter mais informações.

O `packageType` parâmetro é usado para filtrar ainda mais os resultados de preenchimento automático para apenas pacotes que têm pelo menos um tipo de pacote correspondente ao nome do tipo de pacote.
Se o tipo de pacote fornecido não for um tipo de pacote válido, conforme definido pelo [documento de tipo de pacote](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D), um resultado vazio será retornado.
Se o tipo de pacote fornecido estiver vazio, nenhum filtro será aplicado. Em outras palavras, não passar nenhum valor para o `packageType` parâmetro se comportará como se o parâmetro não fosse passado.

### <a name="response"></a>Resposta

A resposta é um documento JSON que contém até `take` resultados de preenchimento automático.

O objeto JSON raiz tem as seguintes propriedades:

Nome      | Type             | Obrigatório | Observações
--------- | ---------------- | -------- | -----
totalHits | inteiro          | sim      | O número total de correspondências, desconsiderando `skip` e`take`
data      | Matriz de cadeias de caracteres | sim      | As IDs de pacote correspondentes à solicitação

### <a name="sample-request"></a>Solicitação de exemplo

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Enumerar versões de pacote

Depois que uma ID de pacote é descoberta usando a API anterior, um cliente pode usar a API de preenchimento automático para enumerar versões de pacote para uma ID de pacote fornecida.

Uma versão de pacote que não está listada não aparecerá nos resultados.

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parâmetros da solicitação

Nome        | Em     | Type    | Obrigatório | Observações
----------- | ------ | ------- | -------- | -----
id          | URL    | string  | sim      | A ID do pacote para buscar versões para
prerelease  | URL    | booleano | não       | `true`ou `false` determinando se os [pacotes de pré-lançamento](../create-packages/prerelease-packages.md) devem ser incluídos
semVerLevel | URL    | string  | não       | Uma cadeia de caracteres de versão SemVer 2.0.0 

Se `prerelease` não for fornecido, os pacotes de pré-lançamento serão excluídos.

O `semVerLevel` parâmetro de consulta é usado para aceitar pacotes SemVer 2.0.0. Se esse parâmetro de consulta for excluído, somente as versões do SemVer 1.0.0 serão retornadas. Se `semVerLevel=2.0.0` for fornecido, as versões SemVer 1.0.0 e SemVer 2.0.0 serão retornadas. Consulte o [SemVer 2.0.0 support for NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obter mais informações.

### <a name="response"></a>Resposta

A resposta é um documento JSON que contém todas as versões de pacote da ID de pacote fornecida, filtrando pelos parâmetros de consulta fornecidos.

O objeto JSON raiz tem a seguinte propriedade:

Nome      | Type             | Obrigatório | Observações
--------- | ---------------- | -------- | -----
data      | Matriz de cadeias de caracteres | sim      | As versões de pacote correspondidas pela solicitação

As versões de pacote na `data` matriz podem conter metadados de compilação SemVer 2.0.0 (por exemplo, `1.0.0+metadata` ) se o `semVerLevel=2.0.0` for fornecido na cadeia de caracteres de consulta.

### <a name="sample-request"></a>Solicitação de exemplo

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
