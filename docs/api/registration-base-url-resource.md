---
title: Metadados de pacote, API do NuGet
description: A URL base do registro de pacote permite buscar metadados sobre pacotes.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 19a1f48164f65f1ff805e036e55abb110247aa72
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324858"
---
# <a name="package-metadata"></a>Metadados de pacote

É possível buscar os metadados sobre os pacotes disponíveis em uma origem de pacote usando a API do NuGet V3. Esses metadados podem ser buscados usando o `RegistrationsBaseUrl` recurso encontrado na [índice de serviço](service-index.md).

A coleção de documentos encontrados em `RegistrationsBaseUrl` muitas vezes são chamados de "registros" ou "blobs de registro". O conjunto de documentos em um único `RegistrationsBaseUrl` é conhecido como "hive de registro". Um hive do registro contém todos os metadados sobre cada pacote disponível em uma origem de pacote.

## <a name="versioning"></a>Controle de versão

O seguinte `@type` valores são usados:

Valor @type                     | Observações
------------------------------- | -----
RegistrationsBaseUrl            | A versão inicial
RegistrationsBaseUrl/3.0.0-beta | Alias of `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | Alias of `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Gzip respostas
RegistrationsBaseUrl/3.6.0      | Inclui pacotes de SemVer 2.0.0

Isso representa três hives do registro distintos disponíveis para várias versões de cliente.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Esses registros não são compactados (que significa que eles usam um implícitas `Content-Encoding: identity`). São pacotes de SemVer 2.0.0 **excluídos** neste hive.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Esses registros são compactados usando `Content-Encoding: gzip`. São pacotes de SemVer 2.0.0 **excluídos** neste hive.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Esses registros são compactados usando `Content-Encoding: gzip`. São pacotes de SemVer 2.0.0 **incluídos** no hive.
Para obter mais informações sobre SemVer 2.0.0, consulte [SemVer 2.0.0 suporte para nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>URL Base

A URL base para as APIs a seguir é o valor da `@id` propriedade associada ao recurso mencionados anteriormente `@type` valores. O seguinte documento, o espaço reservado de URL de base `{@id}` será usado.

## <a name="http-methods"></a>Métodos HTTP

Todas as URLs encontradas no suporte a recursos de registro os métodos HTTP `GET` e `HEAD`.

## <a name="registration-index"></a>Índice de registro

Os grupos de recursos de registro do pacote metadados por ID do pacote. Não é possível obter dados sobre mais de uma ID de pacote por vez. Esse recurso não fornece nenhuma maneira de descobrir as IDs de pacote. Em vez disso, o cliente é considerado já sabe a ID do pacote desejado. Os metadados disponíveis sobre cada versão do pacote varia de acordo com a implementação do servidor. Os blobs de registro do pacote tem a seguinte estrutura hierárquica:

- **Índice**: o ponto de entrada para os metadados do pacote, compartilhados por todos os pacotes em uma fonte com a mesma ID de pacote.
- **Página**: um agrupamento de versões do pacote. O número de versões de pacote em uma página é definido pela implementação do servidor.
- **Folha**: um documento específico para uma versão do pacote único.

A URL do índice de registro é previsível e pode ser determinada pelo cliente recebe uma ID de pacote e o recurso de registro `@id` valor do índice de serviço. As URLs para as páginas de registro e as folhas são descobertas inspecionando o índice do registro.

### <a name="registration-pages-and-leaves"></a>Folhas e páginas de registro

Embora ele não seja estritamente necessário para uma implementação de servidor armazenar registro binárias em documentos de página de registro separados, é uma prática recomendada para conservar memória do lado do cliente. Em vez de alinhamento de todos os registro deixa no índice ou imediatamente armazenando deixa em documentos de página, é recomendável que a implementação do servidor define uma heurística para escolher entre as duas abordagens com base no número de versões do pacote ou deixa o tamanho cumulativo do pacote.

Armazenar todas as versões de pacote (deixa) no salva de índice do registro no número de solicitações HTTP necessária para buscar metadados de pacote, mas significa que deve ser baixado um documento maior e mais memória do cliente deve ser alocada. Por outro lado, se a implementação do servidor armazena imediatamente o registro deixa em documentos de página separada, o cliente deve executar mais solicitações HTTP para obter as informações necessárias.

A heurística que usa nuget.org é da seguinte maneira: se houver versões de 128 ou mais de um pacote, dividir as folhas em páginas de tamanho 64. Se houver menos de 128 versões, embutido todos os deixa em um índice de registro.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parâmetros de solicitação

Nome     | No     | Tipo    | Necessária | Observações
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | cadeia de caracteres  | sim      | A ID do pacote, em minúscula

O `LOWER_ID` valor é a ID do pacote desejado em minúscula usando as regras implementadas pelo. Do NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.

### <a name="response"></a>Resposta

A resposta é um documento JSON que tem um objeto raiz com as seguintes propriedades:

Nome  | Tipo             | Necessária | Observações
----- | ---------------- | -------- | -----
count | inteiro          | sim      | O número de páginas de registro no índice
Itens | matriz de objetos | sim      | A matriz das páginas de registro

Cada item no objeto de índice `items` matriz é um objeto JSON que representa uma página de registro.

#### <a name="registration-page-object"></a>Objeto de página de registro

O objeto de página de registro encontrado no índice de registro tem as seguintes propriedades:

Nome   | Tipo             | Necessária | Observações
------ | ---------------- | -------- | -----
@id    | cadeia de caracteres           | sim      | A URL para a página de registro
count  | inteiro          | sim      | O número de registro deixa na página
Itens  | matriz de objetos | no       | A matriz de folhas de registro e seus metadados associados
inferior  | cadeia de caracteres           | sim      | A versão mais antiga do SemVer 2.0.0 na página (inclusiva)
parent | cadeia de caracteres           | no       | A URL para o índice do registro
superior  | cadeia de caracteres           | sim      | A versão mais recente do SemVer 2.0.0 na página (inclusiva)

O `lower` e `upper` dos limites do objeto page são úteis quando os metadados para uma versão de página específica é necessária.
Esses limites podem ser usados para buscar a página de registro somente necessário. As cadeias de caracteres de versão seguem [regras de versão do NuGet](../reference/package-versioning.md). As cadeias de caracteres de versão são normalizadas e não incluem metadados de compilação. Como com todas as versões no ecossistema do NuGet, comparação de cadeias de caracteres de versão é implementada usando [regras de precedência de versão de SemVer 2.0.0's](http://semver.org/spec/v2.0.0.html#spec-item-11).

O `parent` propriedade só será exibida se o objeto de página de registro tem o `items` propriedade.

Se o `items` propriedade não está presente no objeto de página de registro, a URL especificada no `@id` deve ser usado para buscar metadados sobre as versões de pacote individuais. O `items` matriz, às vezes, é excluída do objeto de página como uma otimização. Se o número de versões de uma ID de pacote único é muito grande, o documento de índice do registro será grande e inútil ao processo para um cliente que só se preocupa sobre uma versão específica ou um pequeno intervalo de versões.

Observe que, se o `items` propriedade estiver presente, o `@id` propriedade não precisa ser usada, pois todos os dados da página já está embutido no `items` propriedade.

Cada item no objeto de página `items` matriz é um objeto JSON que representa uma folha de registro e ele tem os metadados associados.

#### <a name="registration-leaf-object-in-a-page"></a>Objeto de folha de registro em uma página

O objeto de folha de registro encontrado em uma página de registro tem as seguintes propriedades:

Nome           | Tipo   | Necessária | Observações
-------------- | ------ | -------- | -----
@id            | cadeia de caracteres | sim      | A URL para a folha de registro
catalogEntry   | objeto | sim      | A entrada de catálogo que contém os metadados do pacote
packageContent | cadeia de caracteres | sim      | A URL para o conteúdo do pacote (. nupkg)

Cada objeto de folha de registro representa dados associados a uma versão do pacote único.

#### <a name="catalog-entry"></a>Entrada de catálogo

O `catalogEntry` propriedade no objeto folha registro tem as seguintes propriedades:

Nome                     | Tipo                       | Necessária | Observações
------------------------ | -------------------------- | -------- | -----
@id                      | cadeia de caracteres                     | sim      | A URL a ser usado para produzir esse objeto de documento
authors                  | cadeia de caracteres ou matriz de cadeias de caracteres | no       | 
dependencyGroups         | matriz de objetos           | no       | As dependências do pacote, agrupados por estrutura de destino
descrição              | cadeia de caracteres                     | no       | 
iconUrl                  | cadeia de caracteres                     | no       | 
id                       | cadeia de caracteres                     | sim      | A ID do pacote
licenseUrl               | cadeia de caracteres                     | no       |
licenseExpression        | cadeia de caracteres                     | no       | 
listados                   | boolean                    | no       | Deve ser considerado como caso esteja ausente, listado
minClientVersion         | cadeia de caracteres                     | no       | 
projectUrl               | cadeia de caracteres                     | no       | 
Publicado                | cadeia de caracteres                     | no       | Uma cadeia de caracteres que contém um carimbo de hora ISO 8601 de quando o pacote foi publicado
requireLicenseAcceptance | boolean                    | no       | 
resumo                  | cadeia de caracteres                     | no       | 
marcações                     | cadeia de caracteres ou uma matriz de cadeia de caracteres  | no       | 
título                    | cadeia de caracteres                     | no       | 
version                  | cadeia de caracteres                     | sim      | A cadeia de caracteres de versão completa após a normalização

O pacote `version` propriedade é a cadeia de caracteres de versão completa após a normalização. Isso significa que os dados de criação de SemVer 2.0.0 podem ser incluídos aqui.

O `dependencyGroups` propriedade é uma matriz de objetos que representam as dependências do pacote, agrupados por estrutura de destino. Se o pacote não tem dependências, o `dependencyGroups` propriedade estiver ausente, uma matriz vazia, ou o `dependencies` propriedade de todos os grupos está vazio ou ausente.

O valor da `licenseExpression` obedece a propriedade [sintaxe de expressão de licença do NuGet](https://docs.microsoft.com/en-us/nuget/reference/nuspec#license).

#### <a name="package-dependency-group"></a>Grupo de dependência de pacote

Cada objeto de dependência de grupo tem as seguintes propriedades:

Nome            | Tipo             | Necessária | Observações
--------------- | ---------------- | -------- | -----
targetFramework | cadeia de caracteres           | no       | A estrutura de destino que essas dependências são aplicáveis para
dependências    | matriz de objetos | no       |

O `targetFramework` cadeia de caracteres usa o formato implementado pela biblioteca do .NET do NuGet [NuGet.Frameworks](https://www.nuget.org/packages/NuGet.Frameworks/). Se nenhum `targetFramework` for especificado, o grupo de dependência se aplica a todas as estruturas de destino.

O `dependencies` propriedade é uma matriz de objetos, cada um representando uma dependência de pacote do pacote atual.

#### <a name="package-dependency"></a>Dependência de pacote

Cada dependência de pacote tem as seguintes propriedades:

Nome         | Tipo   | Necessária | Observações
------------ | ------ | -------- | -----
id           | cadeia de caracteres | sim      | A ID da dependência de pacote
range        | objeto | no       | O permitidos [intervalo de versão](../reference/package-versioning.md#version-ranges-and-wildcards) da dependência
registro | cadeia de caracteres | no       | A URL para o índice do registro para essa dependência

Se o `range` propriedade for excluída ou uma cadeia de caracteres vazia, o cliente deve usar como padrão para o intervalo de versão `(, )`. Ou seja, qualquer versão da dependência é permitida.

### <a name="sample-request"></a>Exemplo de solicitação

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

Nesse caso específico, o índice do registro tem a página de registro embutida, portanto, não há solicitações extras são necessárias para buscar metadados sobre as versões do pacote individual.

## <a name="registration-page"></a>Página de registro

A página de registro contém folhas de registro. A URL para buscar uma página de registro é determinada pelo `@id` propriedade no [objeto de página de registro](#registration-page-object) mencionado acima.

Quando o `items` matriz não for fornecida no índice de registro, uma solicitação HTTP GET do `@id` valor retornará um documento JSON que tem um objeto como sua raiz. O objeto tem as seguintes propriedades:

Nome   | Tipo             | Necessária | Observações
------ | ---------------- | -------- | -----
@id    | cadeia de caracteres           | sim      | A URL para a página de registro
count  | inteiro          | sim      | O número de registro deixa na página
Itens  | matriz de objetos | sim      | A matriz de folhas de registro e seus metadados associados
inferior  | cadeia de caracteres           | sim      | A versão mais antiga do SemVer 2.0.0 na página (inclusiva)
parent | cadeia de caracteres           | sim      | A URL para o índice do registro
superior  | cadeia de caracteres           | sim      | A versão mais recente do SemVer 2.0.0 na página (inclusiva)

A forma dos objetos de folha de registro é o mesmo o índice do registro [acima](#registration-leaf-object-in-a-page).

## <a name="sample-request"></a>Exemplo de solicitação

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Folha de registro

A folha de registro contém informações sobre um pacote específico ID e versão. Os metadados sobre a versão específica podem não estar disponíveis neste documento. Metadados de pacote devem ser buscados na [índice de registro](#registration-index) ou o [página de registro](#registration-page) (que é descoberto usando o índice do registro).

A URL para buscar uma folha de registro é obtida a `@id` propriedade de um objeto de folha de registro em um índice de registro ou a página de registro.

A folha de registro é um documento JSON com um objeto raiz com as seguintes propriedades:

Nome           | Tipo    | Necessária | Observações
-------------- | ------- | -------- | -----
@id            | cadeia de caracteres  | sim      | A URL para a folha de registro
catalogEntry   | cadeia de caracteres  | no       | A URL para a entrada de catálogo que produziu esses folha
listados         | boolean | no       | Deve ser considerado como caso esteja ausente, listado
packageContent | cadeia de caracteres  | no       | A URL para o conteúdo do pacote (. nupkg)
Publicado      | cadeia de caracteres  | no       | Uma cadeia de caracteres que contém um carimbo de hora ISO 8601 de quando o pacote foi publicado
registro   | cadeia de caracteres  | no       | A URL para o índice do registro

> [!Note]
> Em nuget.org, o `published` valor é definido como ano 1900 quando o pacote for removido da lista.

### <a name="sample-request"></a>Exemplo de solicitação

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
