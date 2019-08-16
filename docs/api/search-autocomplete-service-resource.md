---
title: Preenchimento automático, API do NuGet
description: O serviço de preenchimento automático de pesquisa dá suporte à descoberta interativa de IDs e versões de pacote.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1179ad649da560766f28c18ab6fa670fd8fa6d8b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488301"
---
# <a name="autocomplete"></a>Preenchimento Automático

É possível criar uma ID do pacote e uma experiência de preenchimento automático da versão usando a API v3. O recurso usado para fazer consultas de preenchimento automático é `SearchAutocompleteService` o recurso encontrado no [índice de serviço](service-index.md).

## <a name="versioning"></a>Controle de versão

Os seguintes `@type` valores são usados:

Valor @type                          | Observações
------------------------------------ | -----
SearchAutocompleteService            | A versão inicial
SearchAutocompleteService/3.0.0-beta | Alias of `SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | Alias of `SearchAutocompleteService`

## <a name="base-url"></a>URL Base

A URL base para as APIs a seguir é o valor da `@id` propriedade associada a um dos valores de recurso `@type` mencionados anteriormente. No documento a seguir, a URL `{@id}` base do espaço reservado será usada.

## <a name="http-methods"></a>Métodos HTTP

Todas as URLs encontradas no recurso de registro dão suporte aos `GET` métodos `HEAD`http e.

## <a name="search-for-package-ids"></a>Pesquisar por IDs de pacote

A primeira API de preenchimento automático dá suporte à pesquisa de parte de uma cadeia de caracteres de ID de pacote. Isso é ótimo quando você deseja fornecer um recurso typeahead de pacote em uma interface de usuário integrada com uma origem de pacote NuGet.

Um pacote com apenas versões não listadas não será exibido nos resultados.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parâmetros de solicitação

Nome        | No     | Tipo    | Necessária | Observações
----------- | ------ | ------- | -------- | -----
q           | URL    | cadeia de caracteres  | no       | A cadeia de caracteres para comparar com as IDs de pacote
skip        | URL    | inteiro | no       | O número de resultados a serem ignorados, para paginação
ter        | URL    | inteiro | no       | O número de resultados a serem retornados, para paginação
pré-lançamento  | URL    | boolean | no       | `true`ou `false` determinando se os [pacotes de pré-lançamento](../create-packages/prerelease-packages.md) devem ser incluídos
semVerLevel | URL    | cadeia de caracteres  | no       | Uma cadeia de versão do SemVer 1.0.0 

A consulta `q` de preenchimento automático é analisada de uma maneira que é definida pela implementação do servidor. o nuget.org dá suporte à consulta do prefixo dos tokens de ID do pacote, que são partes da ID produzida pela divisão do original por caracteres de letras e símbolos do Camel.

O `skip` padrão do parâmetro é 0.

O `take` parâmetro deve ser um número inteiro maior que zero. A implementação do servidor pode impor um valor máximo.

Se `prerelease` não for fornecido, os pacotes de pré-lançamento serão excluídos.

O `semVerLevel` parâmetro de consulta é usado para aceitar [pacotes SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Se esse parâmetro de consulta for excluído, somente as IDs de pacote com versões compatíveis do SemVer 1.0.0 serão retornadas (com as advertências de [versão padrão do NuGet](../concepts/package-versioning.md) , como cadeias de caracteres de versão com 4 partes de inteiros).
Se `semVerLevel=2.0.0` for fornecido, os pacotes compatíveis SemVer 1.0.0 e SemVer 2.0.0 serão retornados. Consulte o [SemVer 2.0.0 support for NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obter mais informações.

### <a name="response"></a>Resposta

A resposta é um documento JSON que contém `take` até resultados de preenchimento automático.

O objeto JSON raiz tem as seguintes propriedades:

Nome      | Tipo             | Necessária | Observações
--------- | ---------------- | -------- | -----
totalHits | inteiro          | sim      | O número total de correspondências, desconsiderando `skip` e`take`
Dados      | matriz de cadeias de caracteres | sim      | As IDs de pacote correspondentes à solicitação

### <a name="sample-request"></a>Exemplo de solicitação

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>Exemplo de resposta

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Enumerar versões de pacote

Depois que uma ID de pacote é descoberta usando a API anterior, um cliente pode usar a API de preenchimento automático para enumerar versões de pacote para uma ID de pacote fornecida.

Uma versão de pacote que não está listada não aparecerá nos resultados.

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parâmetros de solicitação

Nome        | No     | Tipo    | Necessária | Observações
----------- | ------ | ------- | -------- | -----
id          | URL    | cadeia de caracteres  | sim      | A ID do pacote para buscar versões para
pré-lançamento  | URL    | boolean | no       | `true`ou `false` determinando se os [pacotes de pré-lançamento](../create-packages/prerelease-packages.md) devem ser incluídos
semVerLevel | URL    | cadeia de caracteres  | no       | Uma cadeia de caracteres de versão SemVer 2.0.0 

Se `prerelease` não for fornecido, os pacotes de pré-lançamento serão excluídos.

O `semVerLevel` parâmetro de consulta é usado para aceitar pacotes SemVer 2.0.0. Se esse parâmetro de consulta for excluído, somente as versões do SemVer 1.0.0 serão retornadas. Se `semVerLevel=2.0.0` for fornecido, as versões SemVer 1.0.0 e SemVer 2.0.0 serão retornadas. Consulte o [SemVer 2.0.0 support for NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obter mais informações.

### <a name="response"></a>Resposta

A resposta é um documento JSON que contém todas as versões de pacote da ID de pacote fornecida, filtrando pelos parâmetros de consulta fornecidos.

O objeto JSON raiz tem a seguinte propriedade:

Nome      | Tipo             | Necessária | Observações
--------- | ---------------- | -------- | -----
Dados      | matriz de cadeias de caracteres | sim      | As versões de pacote correspondidas pela solicitação

As versões de pacote na `data` matriz podem conter metadados de compilação SemVer 2.0.0 ( `1.0.0+metadata`por exemplo,) `semVerLevel=2.0.0` se o for fornecido na cadeia de caracteres de consulta.

### <a name="sample-request"></a>Exemplo de solicitação

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>Exemplo de resposta

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
