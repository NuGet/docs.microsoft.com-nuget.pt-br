---
title: Pesquisa de API do NuGet
description: O serviço de pesquisa permite que os clientes para consultar pacotes pela palavra-chave e os resultados do filtro em determinados campos de pacote.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 76600ee916305ee01ddfb675c83c184e980c5a42
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="search"></a>Pesquisar

É possível procurar pacotes disponíveis em uma origem de pacote usando a API V3. O recurso usado para pesquisar o `SearchQueryService` recurso encontrado na [índice de serviço](service-index.md).

## <a name="versioning"></a>Controle de versão

O seguinte `@type` valores são usados:

Valor @type                   | Observações
----------------------------- | -----
SearchQueryService            | A versão inicial
SearchQueryService/3.0.0-beta | Alias de `SearchQueryService`
SearchQueryService/3.0.0-rc   | Alias de `SearchQueryService`

## <a name="base-url"></a>URL Base

A URL base para a seguinte API é o valor da `@id` propriedade associada a um recurso mencionados acima `@type` valores. No documento a seguir, a URL base do espaço reservado `{@id}` será usado.

## <a name="http-methods"></a>Métodos HTTP

Todas as URLs encontradas no suporte a recurso de registro os métodos HTTP `GET` e `HEAD`.

## <a name="search-for-packages"></a>Procurar pacotes

A API de pesquisa permite que um cliente consulta para uma página de pacotes de correspondência de uma consulta de pesquisa especificado. A interpretação da consulta de pesquisa (por exemplo, a geração de tokens dos termos de pesquisa) é determinada pela implementação do servidor, mas a expectativa geral é que a consulta de pesquisa é usada para correspondência de marcas, títulos, descrições e IDs de pacote. Também podem ser considerados outros campos de metadados do pacote.

Um pacote não listado nunca deve aparecer nos resultados da pesquisa.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parâmetros de solicitação

Nome        | No     | Tipo    | Necessária | Observações
----------- | ------ | ------- | -------- | -----
q           | URL    | cadeia de caracteres  | no       | Termos de pesquisa usado para pacotes de filtro
skip        | URL    | inteiro | no       | O número de resultados a ignorar, de paginação
Take        | URL    | inteiro | no       | O número de resultados para retornar para a paginação
versão de pré-lançamento  | URL    | boolean | no       | `true` ou `false` determinar a inclusão [pacotes de pré-lançamento](../create-packages/prerelease-packages.md)
semVerLevel | URL    | cadeia de caracteres  | no       | Uma cadeia de caracteres de versão SemVer 1.0.0 

A consulta de pesquisa `q` é analisado em uma maneira que é definida pela implementação do servidor. NuGet.org oferece suporte à filtragem básica em um [vários campos](../consume-packages/finding-and-choosing-packages.md#search-syntax). Se nenhum `q` for fornecido, todos os pacotes devem ser retornados, dentro dos limites impostos pela skip e take. Isso permite que o guia de "Procurar" na experiência do NuGet Visual Studio.

O `skip` parâmetro padrão é 0.

O `take` parâmetro deve ser um inteiro maior que zero. A implementação do servidor pode impor um valor máximo.

Se `prerelease` não for fornecido, os pacotes de pré-lançamento serão excluídos.

O `semVerLevel` parâmetro de consulta é usado para aceitar [SemVer 2.0.0 pacotes](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Se esse parâmetro de consulta é excluído, apenas pacotes com versões compatíveis do SemVer 1.0.0 serão retornados (com o [padrão controle de versão do NuGet](../reference/package-versioning.md) limitações, como cadeias de caracteres de versão com 4 partes de inteiro).
Se `semVerLevel=2.0.0` for fornecido, SemVer 1.0.0 e pacotes compatíveis SemVer 2.0.0 serão retornados. Consulte o [suporte SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obter mais informações.

### <a name="response"></a>Resposta

A resposta é documento JSON que contém até `take` resultados da pesquisa. Resultados da pesquisa são agrupados por ID do pacote.

A raiz do objeto JSON tem as seguintes propriedades:

Nome      | Tipo             | Necessária | Observações
--------- | ---------------- | -------- | -----
totalHits | inteiro          | sim      | O número total de correspondências, desconsiderando `skip` e `take`
Dados      | Matriz de objetos | sim      | Os resultados da pesquisa correspondidos com a solicitação

### <a name="search-result"></a>resultado da pesquisa

Cada item de `data` matriz é um objeto JSON composto de um grupo de versões do pacote de compartilhar a mesma ID de pacote.
O objeto tem as seguintes propriedades:

Nome           | Tipo                       | Necessária | Observações
-------------- | -------------------------- | -------- | -----
id             | cadeia de caracteres                     | sim      | A ID do pacote correspondente
version        | cadeia de caracteres                     | sim      | A cadeia de caracteres de versão SemVer 2.0.0 completa do pacote (pode conter metadados de compilação)
descrição    | cadeia de caracteres                     | no       | 
versões       | Matriz de objetos           | sim      | Todas as versões da correspondência de pacote a `prerelease` parâmetro
authors        | cadeia de caracteres ou matriz de cadeias de caracteres | no       | 
iconUrl        | cadeia de caracteres                     | no       | 
licenseUrl     | cadeia de caracteres                     | no       | 
owners         | cadeia de caracteres ou matriz de cadeias de caracteres | no       | 
projectUrl     | cadeia de caracteres                     | no       | 
registro   | cadeia de caracteres                     | no       | A URL absoluta associados [índice de registro](registration-base-url-resource.md#registration-index)
resumo        | cadeia de caracteres                     | no       | 
marcações           | cadeia de caracteres ou matriz de cadeias de caracteres | no       | 
título          | cadeia de caracteres                     | no       | 
totalDownloads | inteiro                    | no       | Esse valor pode ser inferido pela soma de downloads de `versions` matriz
Verificado       | boolean                    | no       | Um valor de JSON booleano que indica se o pacote é [verificado](../reference/id-prefix-reservation.md)

Em nuget.org, um pacote verificado é uma que tenha uma ID do pacote correspondente a um prefixo de ID reservado e pertencentes a um dos proprietários do namespace reservado. Para obter mais informações, consulte o [documentação sobre reserva de prefixo de ID](../reference/id-prefix-reservation.md).

Os metadados contidos no objeto de resultado de pesquisa é obtido a versão mais recente do pacote. Cada item de `versions` matriz é um objeto JSON com as seguintes propriedades:

Nome      | Tipo    | Necessária | Observações
--------- | ------- | -------- | -----
@id       | cadeia de caracteres  | sim      | A URL absoluta associados [folha de registro](registration-base-url-resource.md#registration-leaf)
version   | cadeia de caracteres  | sim      | A cadeia de caracteres de versão SemVer 2.0.0 completa do pacote (pode conter metadados de compilação)
Downloads | inteiro | sim      | O número de downloads para esta versão do pacote específico

### <a name="sample-request"></a>Solicitação de amostra

    GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [search-result.json](./_data/search-result.json)]
