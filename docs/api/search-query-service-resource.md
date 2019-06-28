---
title: Pesquisa, a API do NuGet
description: O serviço de pesquisa permite que os clientes para consultar pacotes pela palavra-chave e para filtrar os resultados em determinados campos do pacote.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d462b289c39c2dd1418304dabcad47d0d4217f82
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426739"
---
# <a name="search"></a>Pesquisar

É possível pesquisar pacotes disponíveis em uma origem de pacote usando a API V3. É o recurso usado para pesquisar o `SearchQueryService` recurso encontrado na [índice de serviço](service-index.md).

## <a name="versioning"></a>Controle de versão

O seguinte `@type` valores são usados:

Valor @type                   | Observações
----------------------------- | -----
SearchQueryService            | A versão inicial
SearchQueryService/3.0.0-beta | Alias of `SearchQueryService`
SearchQueryService/3.0.0-rc   | Alias of `SearchQueryService`

## <a name="base-url"></a>URL Base

A URL base para a seguinte API é o valor da `@id` propriedade associada a um do recurso mencionados anteriormente `@type` valores. O seguinte documento, o espaço reservado de URL de base `{@id}` será usado.

## <a name="http-methods"></a>Métodos HTTP

Todas as URLs encontradas no suporte a recursos de registro os métodos HTTP `GET` e `HEAD`.

## <a name="search-for-packages"></a>Pesquisar pacotes

A API de pesquisa permite que um cliente consulta para uma página de pacotes que correspondem a uma consulta de pesquisa especificado. A interpretação da consulta de pesquisa (por exemplo, a geração de tokens de termos de pesquisa) é determinada pela implementação do servidor, mas a expectativa geral é que a consulta de pesquisa é usada para correspondência de IDs de pacote, títulos, descrições e marcas. Também podem ser considerados outros campos de metadados do pacote.

Um pacote não listado nunca deve aparecer nos resultados da pesquisa.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parâmetros de solicitação

Nome        | No     | Tipo    | Necessária | Observações
----------- | ------ | ------- | -------- | -----
q           | URL    | cadeia de caracteres  | no       | Termos de pesquisa usada para pacotes de filtro
skip        | URL    | inteiro | no       | O número de resultados a ignorar, para paginação
Take        | URL    | inteiro | no       | O número de resultados a serem retornados para a paginação
versão de pré-lançamento  | URL    | boolean | no       | `true` ou `false` determinar se é necessário incluir [pacotes de pré-lançamento](../create-packages/prerelease-packages.md)
semVerLevel | URL    | cadeia de caracteres  | no       | Uma cadeia de caracteres de versão 1.0.0 de SemVer 

A consulta de pesquisa `q` é analisado de uma maneira que é definida pela implementação do servidor. NuGet.org dá suporte à filtragem básica em um [variedade de campos](../consume-packages/finding-and-choosing-packages.md#search-syntax). Se nenhum `q` for fornecido, todos os pacotes devem ser devolvidos, dentro dos limites impostos pela skip e take. Isso permite que a guia "Procurar" na experiência do NuGet Visual Studio.

O `skip` parâmetro padrão é 0.

O `take` parâmetro deve ser um inteiro maior que zero. A implementação do servidor pode impor um valor máximo.

Se `prerelease` não for fornecido, pacotes de pré-lançamento são excluídos.

O `semVerLevel` parâmetro de consulta é usado para participar [SemVer 2.0.0 pacotes](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Se esse parâmetro de consulta é excluído, apenas pacotes com as versões compatíveis do SemVer 1.0.0 serão retornados (com o [padrão controle de versão do NuGet](../reference/package-versioning.md) advertências, como cadeias de caracteres de versão com partes de inteiro de 4).
Se `semVerLevel=2.0.0` for fornecido, SemVer 1.0.0 e pacotes de SemVer 2.0.0 compatíveis serão retornados. Consulte a [SemVer 2.0.0 suporte para nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obter mais informações.

### <a name="response"></a>Resposta

A resposta é o documento JSON que contém até `take` resultados da pesquisa. Os resultados da pesquisa são agrupados por ID do pacote.

O objeto JSON de raiz tem as seguintes propriedades:

Nome      | Tipo             | Necessária | Observações
--------- | ---------------- | -------- | -----
totalHits | inteiro          | sim      | O número total de correspondências, desconsiderando `skip` e `take`
Dados      | matriz de objetos | sim      | Os resultados da pesquisa correspondidos pela solicitação

### <a name="search-result"></a>Resultado da pesquisa

Cada item no `data` matriz é um objeto JSON composto de um grupo de versões do pacote compartilhando a mesma ID de pacote.
O objeto tem as seguintes propriedades:

Nome           | Tipo                       | Necessária | Observações
-------------- | -------------------------- | -------- | -----
id             | cadeia de caracteres                     | sim      | A ID do pacote correspondente
version        | cadeia de caracteres                     | sim      | A cadeia de caracteres de versão SemVer 2.0.0 completa do pacote (pode conter metadados de compilação)
descrição    | cadeia de caracteres                     | no       | 
versões       | matriz de objetos           | sim      | Todas as versões do pacote correspondente a `prerelease` parâmetro
authors        | cadeia de caracteres ou matriz de cadeias de caracteres | no       | 
iconUrl        | cadeia de caracteres                     | no       | 
licenseUrl     | cadeia de caracteres                     | no       | 
owners         | cadeia de caracteres ou matriz de cadeias de caracteres | no       | 
projectUrl     | cadeia de caracteres                     | no       | 
registro   | cadeia de caracteres                     | no       | A URL absoluta associados [índice do registro](registration-base-url-resource.md#registration-index)
resumo        | cadeia de caracteres                     | no       | 
marcações           | cadeia de caracteres ou matriz de cadeias de caracteres | no       | 
título          | cadeia de caracteres                     | no       | 
totalDownloads | inteiro                    | no       | Esse valor pode ser inferido pela soma de downloads no `versions` matriz
Verificado       | boolean                    | no       | Um valor de JSON booliano que indica se o pacote é [verificado](../nuget-org/id-prefix-reservation.md)

Em nuget.org, um pacote verificado é aquele que tem uma ID de pacote, um prefixo reservado da ID de correspondência e pertencentes a um dos proprietários do prefixo reservado. Para obter mais informações, consulte o [documentação sobre a reserva de prefixo de ID](../reference/id-prefix-reservation.md).

Os metadados contidos no objeto de resultado de pesquisa é obtido a versão mais recente do pacote. Cada item no `versions` matriz é um objeto JSON com as seguintes propriedades:

Nome      | Tipo    | Necessária | Observações
--------- | ------- | -------- | -----
@id       | cadeia de caracteres  | sim      | A URL absoluta associados [folha registro](registration-base-url-resource.md#registration-leaf)
version   | cadeia de caracteres  | sim      | A cadeia de caracteres de versão SemVer 2.0.0 completa do pacote (pode conter metadados de compilação)
downloads | inteiro | sim      | O número de downloads para esta versão do pacote específico

### <a name="sample-request"></a>Exemplo de solicitação

    GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [search-result.json](./_data/search-result.json)]
