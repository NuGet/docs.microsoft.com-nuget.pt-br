---
title: Pesquisar, API do NuGet
description: O serviço de pesquisa permite que os clientes consultem pacotes por palavra-chave e filtrem os resultados em determinados campos de pacote.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: aed591ceba00f1820a573eacf312112db0a1c69e
ms.sourcegitcommit: 7e9c0630335ef9ec1e200e2ee9065f702e52a8ec
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85292262"
---
# <a name="search"></a>Search

É possível pesquisar pacotes disponíveis em uma origem de pacote usando a API v3. O recurso usado para pesquisa é o `SearchQueryService` recurso encontrado no [índice de serviço](service-index.md).

## <a name="versioning"></a>Controle de versão

Os seguintes `@type` valores são usados:

@type valor                   | Observações
----------------------------- | -----
SearchQueryService            | A versão inicial
SearchQueryService/3.0.0-beta | Alias de`SearchQueryService`
SearchQueryService/3.0.0-RC   | Alias de`SearchQueryService`
SearchQueryService/3.5.0      | Inclui suporte para `packageType` parâmetro de consulta

### <a name="searchqueryservice350"></a>SearchQueryService/3.5.0
Esta versão apresenta suporte para o `packageType` parâmetro de consulta e a `packageTypes` propriedade de resposta, permitindo a filtragem por tipos de pacote definidos pelo autor. Ele é totalmente compatível com consultas ao `SearchQueryService` .

## <a name="base-url"></a>URL base

A URL base para a seguinte API é o valor da `@id` propriedade associada a um dos valores de recurso mencionados anteriormente `@type` . No documento a seguir, a URL base do espaço reservado `{@id}` será usada.

## <a name="http-methods"></a>Métodos HTTP

Todas as URLs encontradas no recurso de registro dão suporte aos métodos HTTP `GET` e `HEAD` .

## <a name="search-for-packages"></a>Pesquisar pacotes

A API de pesquisa permite que um cliente consulte uma página de pacotes que correspondem a uma consulta de pesquisa especificada. A interpretação da consulta de pesquisa (por exemplo, a geração de tokens dos termos de pesquisa) é determinada pela implementação do servidor, mas a expectativa geral é que a consulta de pesquisa seja usada para corresponder IDs, títulos, descrições e marcas de pacote. Outros campos de metadados de pacote também podem ser considerados.

Um pacote não listado nunca deve aparecer nos resultados da pesquisa.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}

### <a name="request-parameters"></a>Parâmetros da solicitação

Nome        | Em     | Type    | Obrigatório | Observações
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | não       | Os termos de pesquisa a serem usados para filtrar pacotes
skip        | URL    | inteiro | não       | O número de resultados a serem ignorados, para paginação
take        | URL    | inteiro | não       | O número de resultados a serem retornados, para paginação
prerelease  | URL    | booleano | não       | `true`ou `false` determinando se os [pacotes de pré-lançamento](../create-packages/prerelease-packages.md) devem ser incluídos
semVerLevel | URL    | string  | não       | Uma cadeia de versão do SemVer 1.0.0 
packageType | URL    | string  | não       | O tipo de pacote a ser usado para filtrar pacotes (adicionados em `SearchQueryService/3.5.0` )

A consulta de pesquisa `q` é analisada de uma maneira que é definida pela implementação do servidor. o nuget.org dá suporte à filtragem básica em uma [variedade de campos](../consume-packages/finding-and-choosing-packages.md#search-syntax). Se não `q` for fornecido, todos os pacotes devem ser retornados, dentro dos limites impostos por Skip e Take. Isso habilita a guia "procurar" na experiência do NuGet Visual Studio.

O `skip` padrão do parâmetro é 0.

O `take` parâmetro deve ser um número inteiro maior que zero. A implementação do servidor pode impor um valor máximo.

Se `prerelease` não for fornecido, os pacotes de pré-lançamento serão excluídos.

O `semVerLevel` parâmetro de consulta é usado para aceitar [pacotes SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Se esse parâmetro de consulta for excluído, somente pacotes com versões compatíveis do SemVer 1.0.0 serão retornados (com as advertências de [controle de versão do NuGet padrão](../concepts/package-versioning.md) , como cadeias de caracteres de versão com 4 partes de inteiros).
Se `semVerLevel=2.0.0` for fornecido, os pacotes compatíveis SemVer 1.0.0 e SemVer 2.0.0 serão retornados. Consulte o [SemVer 2.0.0 support for NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obter mais informações.

O `packageType` parâmetro é usado para filtrar ainda mais os resultados da pesquisa para apenas os pacotes que têm pelo menos um tipo de pacote correspondente ao nome do tipo de pacote.
Se o tipo de pacote fornecido não for um tipo de pacote válido, conforme definido pelo [documento de tipo de pacote](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D), um resultado vazio será retornado.
Se o tipo de pacote fornecido estiver vazio, nenhum filtro será aplicado. Em outras palavras, não passar nenhum valor para o parâmetro PackageType se comportará como se o parâmetro não fosse passado.

### <a name="response"></a>Resposta

A resposta é um documento JSON que contém `take` resultados de pesquisa. Os resultados da pesquisa são agrupados por ID do pacote.

O objeto JSON raiz tem as seguintes propriedades:

Nome      | Type             | Obrigatório | Observações
--------- | ---------------- | -------- | -----
totalHits | inteiro          | sim      | O número total de correspondências, desconsiderando `skip` e`take`
data      | matriz de objetos | sim      | Os resultados da pesquisa correspondidos pela solicitação

### <a name="search-result"></a>Resultado da pesquisa

Cada item na `data` matriz é um objeto JSON composto por um grupo de versões de pacote que compartilham a mesma ID de pacote.
O objeto tem as seguintes propriedades:

Nome           | Type                       | Obrigatório | Observações
-------------- | -------------------------- | -------- | -----
id             | string                     | sim      | A ID do pacote correspondente
version        | string                     | sim      | A cadeia de caracteres de versão SemVer 2.0.0 completa do pacote (pode conter metadados de compilação)
descrição    | string                     | não       | 
versões       | matriz de objetos           | sim      | Todas as versões do pacote que correspondem ao `prerelease` parâmetro
authors        | cadeia de caracteres ou matriz de cadeias de caracteres | não       | 
iconUrl        | string                     | não       | 
licenseUrl     | string                     | não       | 
owners         | cadeia de caracteres ou matriz de cadeias de caracteres | não       | 
projectUrl     | string                     | não       | 
registro   | string                     | não       | A URL absoluta para o [índice de registro](registration-base-url-resource.md#registration-index) associado
resumo        | string                     | não       | 
marcas           | cadeia de caracteres ou matriz de cadeias de caracteres | não       | 
título          | string                     | não       | 
totalDownloads | inteiro                    | não       | Esse valor pode ser deduzido pela soma de downloads na `versions` matriz
verificar       | booleano                    | não       | Um booliano JSON que indica se o pacote é [verificado](../nuget-org/id-prefix-reservation.md)
packageTypes   | matriz de objetos           | sim      | Os tipos de pacote definidos pelo autor do pacote (adicionado em `SearchQueryService/3.5.0` )

No nuget.org, um pacote verificado é aquele que tem uma ID de pacote correspondente a um prefixo de ID reservado e pertence a um dos proprietários do prefixo reservado. Para obter mais informações, consulte a [documentação sobre reserva de prefixo de ID](../reference/id-prefix-reservation.md).

Os metadados contidos no objeto de resultado da pesquisa são extraídos da versão mais recente do pacote. Cada item na `versions` matriz é um objeto JSON com as seguintes propriedades:

Nome      | Type    | Obrigatório | Observações
--------- | ------- | -------- | -----
@id       | string  | sim      | A URL absoluta para a [folha de registro](registration-base-url-resource.md#registration-leaf) associada
version   | string  | sim      | A cadeia de caracteres de versão SemVer 2.0.0 completa do pacote (pode conter metadados de compilação)
downloads | inteiro | sim      | O número de downloads para esta versão de pacote específica

A `packageTypes` matriz sempre consistirá em pelo menos um (1) item. O tipo de pacote para uma determinada ID de pacote é considerado como sendo os tipos de pacote definidos pela versão mais recente do pacote em relação aos outros parâmetros de pesquisa. Cada item na `packageTypes` matriz é um objeto JSON com as seguintes propriedades:

Nome      | Type    | Obrigatório | Observações
--------- | ------- | -------- | -----
name      | string  | sim      | O nome do tipo de pacote.

### <a name="sample-request"></a>Solicitação de exemplo

    GET https://azuresearch-usnc.nuget.org/query?q=NuGet.Versioning&prerelease=false&semVerLevel=2.0.0

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [search-result.json](./_data/search-result.json)]
