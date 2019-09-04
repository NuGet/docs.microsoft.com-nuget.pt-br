---
title: Pesquisar, API do NuGet
description: O serviço de pesquisa permite que os clientes consultem pacotes por palavra-chave e filtrem os resultados em determinados campos de pacote.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: be25e9bf72b9115de8ae55f6296195fed3152f10
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/03/2019
ms.locfileid: "70235117"
---
# <a name="search"></a>Pesquisar

É possível pesquisar pacotes disponíveis em uma origem de pacote usando a API v3. O recurso usado para pesquisa é o `SearchQueryService` recurso encontrado no [índice de serviço](service-index.md).

## <a name="versioning"></a>Controle de versão

Os seguintes `@type` valores são usados:

Valor @type                   | Observações
----------------------------- | -----
SearchQueryService            | A versão inicial
SearchQueryService/3.0.0-beta | Alias of `SearchQueryService`
SearchQueryService/3.0.0-rc   | Alias of `SearchQueryService`

## <a name="base-url"></a>URL Base

A URL base para a seguinte API é o valor da `@id` propriedade associada a um dos valores de recurso `@type` mencionados anteriormente. No documento a seguir, a URL `{@id}` base do espaço reservado será usada.

## <a name="http-methods"></a>Métodos HTTP

Todas as URLs encontradas no recurso de registro dão suporte aos `GET` métodos `HEAD`http e.

## <a name="search-for-packages"></a>Pesquisar pacotes

A API de pesquisa permite que um cliente consulte uma página de pacotes que correspondem a uma consulta de pesquisa especificada. A interpretação da consulta de pesquisa (por exemplo, a geração de tokens dos termos de pesquisa) é determinada pela implementação do servidor, mas a expectativa geral é que a consulta de pesquisa seja usada para corresponder IDs, títulos, descrições e marcas de pacote. Outros campos de metadados de pacote também podem ser considerados.

Um pacote não listado nunca deve aparecer nos resultados da pesquisa.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parâmetros de solicitação

Nome        | No     | Tipo    | Necessária | Observações
----------- | ------ | ------- | -------- | -----
q           | URL    | cadeia de caracteres  | no       | Os termos de pesquisa a serem usados para filtrar pacotes
skip        | URL    | inteiro | no       | O número de resultados a serem ignorados, para paginação
ter        | URL    | inteiro | no       | O número de resultados a serem retornados, para paginação
pré-lançamento  | URL    | boolean | no       | `true`ou `false` determinando se os [pacotes de pré-lançamento](../create-packages/prerelease-packages.md) devem ser incluídos
semVerLevel | URL    | cadeia de caracteres  | no       | Uma cadeia de versão do SemVer 1.0.0 

A consulta `q` de pesquisa é analisada de uma maneira que é definida pela implementação do servidor. o nuget.org dá suporte à filtragem básica em uma [variedade de campos](../consume-packages/finding-and-choosing-packages.md#search-syntax). Se não `q` for fornecido, todos os pacotes devem ser retornados, dentro dos limites impostos por Skip e Take. Isso habilita a guia "procurar" na experiência do NuGet Visual Studio.

O `skip` padrão do parâmetro é 0.

O `take` parâmetro deve ser um número inteiro maior que zero. A implementação do servidor pode impor um valor máximo.

Se `prerelease` não for fornecido, os pacotes de pré-lançamento serão excluídos.

O `semVerLevel` parâmetro de consulta é usado para aceitar [pacotes SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Se esse parâmetro de consulta for excluído, somente pacotes com versões compatíveis do SemVer 1.0.0 serão retornados (com as advertências de [controle de versão do NuGet padrão](../concepts/package-versioning.md) , como cadeias de caracteres de versão com 4 partes de inteiros).
Se `semVerLevel=2.0.0` for fornecido, os pacotes compatíveis SemVer 1.0.0 e SemVer 2.0.0 serão retornados. Consulte o [SemVer 2.0.0 support for NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obter mais informações.

### <a name="response"></a>Resposta

A resposta é um documento JSON que contém `take` resultados de pesquisa. Os resultados da pesquisa são agrupados por ID do pacote.

O objeto JSON raiz tem as seguintes propriedades:

Nome      | Tipo             | Necessária | Observações
--------- | ---------------- | -------- | -----
totalHits | inteiro          | sim      | O número total de correspondências, desconsiderando `skip` e`take`
Dados      | matriz de objetos | sim      | Os resultados da pesquisa correspondidos pela solicitação

### <a name="search-result"></a>Resultado da pesquisa

Cada item na `data` matriz é um objeto JSON composto por um grupo de versões de pacote que compartilham a mesma ID de pacote.
O objeto tem as seguintes propriedades:

Nome           | Tipo                       | Necessária | Observações
-------------- | -------------------------- | -------- | -----
id             | cadeia de caracteres                     | sim      | A ID do pacote correspondente
version        | cadeia de caracteres                     | sim      | A cadeia de caracteres de versão SemVer 2.0.0 completa do pacote (pode conter metadados de compilação)
descrição    | cadeia de caracteres                     | no       | 
versões       | matriz de objetos           | sim      | Todas as versões do pacote que correspondem ao `prerelease` parâmetro
authors        | String ou matriz de cadeias de caracteres | no       | 
iconUrl        | cadeia de caracteres                     | no       | 
licenseUrl     | cadeia de caracteres                     | no       | 
owners         | String ou matriz de cadeias de caracteres | no       | 
projectUrl     | cadeia de caracteres                     | no       | 
registro   | cadeia de caracteres                     | no       | A URL absoluta para o [índice de registro](registration-base-url-resource.md#registration-index) associado
resumo        | cadeia de caracteres                     | no       | 
marcações           | String ou matriz de cadeias de caracteres | no       | 
título          | cadeia de caracteres                     | no       | 
totalDownloads | inteiro                    | no       | Esse valor pode ser deduzido pela soma de downloads na `versions` matriz
verificar       | boolean                    | no       | Um booliano JSON que indica se o pacote é [verificado](../nuget-org/id-prefix-reservation.md)

No nuget.org, um pacote verificado é aquele que tem uma ID de pacote correspondente a um prefixo de ID reservado e pertence a um dos proprietários do prefixo reservado. Para obter mais informações, consulte a [documentação sobre reserva de prefixo de ID](../reference/id-prefix-reservation.md).

Os metadados contidos no objeto de resultado da pesquisa são extraídos da versão mais recente do pacote. Cada item na `versions` matriz é um objeto JSON com as seguintes propriedades:

Nome      | Tipo    | Necessária | Observações
--------- | ------- | -------- | -----
@id       | cadeia de caracteres  | sim      | A URL absoluta para a [folha de registro](registration-base-url-resource.md#registration-leaf) associada
version   | cadeia de caracteres  | sim      | A cadeia de caracteres de versão SemVer 2.0.0 completa do pacote (pode conter metadados de compilação)
downloads | inteiro | sim      | O número de downloads para esta versão de pacote específica

### <a name="sample-request"></a>Exemplo de solicitação

    GET https://azuresearch-usnc.nuget.org/query?q=NuGet.Versioning&prerelease=false&semVerLevel=2.0.0

### <a name="sample-response"></a>Exemplo de resposta

[!code-JSON [search-result.json](./_data/search-result.json)]
