---
title: Metadados, NuGet API do pacote | Microsoft Docs
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
description: A URL de base de registro do pacote permite buscar metadados sobre os pacotes.
keywords: "Metadados de pacote do NuGet API, o registro do NuGet API, API do NuGet não consta da lista de pacotes"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: c098d70d58011bad7f9829f0c95c87c1339dd362
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
---
# <a name="package-metadata"></a>Metadados de pacote

É possível buscar metadados sobre os pacotes disponíveis em uma origem de pacote usando a API do NuGet V3. Esses metadados podem ser obtidos usando o `RegistrationsBaseUrl` recurso encontrado na [índice de serviço](service-index.md).

A coleção dos documentos encontrado em `RegistrationsBaseUrl` são chamados de "Registro" ou "blobs de registro". O conjunto de documentos em um único `RegistrationsBaseUrl` é chamado de "hive de registro". Um hive do registro contém todos os metadados sobre cada pacote disponível em uma origem do pacote.

## <a name="versioning"></a>Controle de versão

O seguinte `@type` valores são usados:

Valor @type                     | Observações
------------------------------- | -----
RegistrationsBaseUrl            | A versão inicial
RegistrationsBaseUrl/3.0.0-beta | Alias de`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | Alias de`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Gzip respostas
RegistrationsBaseUrl/3.6.0      | Inclui pacotes SemVer 2.0.0

Isso representa três hives do registro diferentes disponíveis para várias versões de cliente.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Esses registros não são compactados (que significa que eles usam um implícita `Content-Encoding: identity`). Pacotes de SemVer 2.0.0 estão **excluídos** dessa seção.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Esses registros são compactados usando `Content-Encoding: gzip`. Pacotes de SemVer 2.0.0 estão **excluídos** dessa seção.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Esses registros são compactados usando `Content-Encoding: gzip`. Pacotes de SemVer 2.0.0 estão **incluídos** no hive.
Para obter mais informações sobre SemVer 2.0.0, consulte [suporte SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>URL Base

A URL base para as seguintes APIs é o valor da `@id` propriedade associada com o recurso mencionados acima `@type` valores. No documento a seguir, a URL base do espaço reservado `{@id}` será usado.

## <a name="http-methods"></a>Métodos HTTP

Todas as URLs encontradas no suporte a recurso de registro os métodos HTTP `GET` e `HEAD`.

## <a name="registration-index"></a>Índice de registro

Os grupos de recursos de registro do pacote metadados por ID do pacote. Não é possível obter dados sobre mais de uma ID de pacote por vez. Este recurso não fornece nenhuma maneira de detectar IDs de pacote. Em vez disso, o cliente será considerado para já souber a ID do pacote desejado. Os metadados disponíveis sobre cada versão do pacote varia de acordo com a implementação do servidor. Os blobs de registro do pacote tem a seguinte estrutura hierárquica:

- **Índice**: o ponto de entrada para os metadados do pacote, compartilhado por todos os pacotes em uma fonte com a mesma ID de pacote.
- **Página**: um agrupamento de versões do pacote. O número de versões do pacote em uma página é definido pela implementação do servidor.
- **Folha**: um documento específico para uma versão do pacote único.

A URL do índice de registro é previsível e pode ser determinada pelo cliente recebe uma ID de pacote e o recurso de registro `@id` valor do índice de serviço. As URLs para as páginas de registro e as folhas são descobertas inspecionando o índice de registro.

### <a name="registration-pages-and-leaves"></a>Deixa e páginas de registro

Embora não seja estritamente, é necessário para uma implementação do servidor armazenar registro folhas em documentos de página de registro separados, é uma prática recomendada para conservar a memória do lado do cliente. Em vez de todos os inlining registro deixa o índice ou armazenar imediatamente deixa em documentos de página, é recomendável que a implementação do servidor define uma heurística para escolher entre as duas abordagens com base no número de versões do pacote ou deixa o tamanho cumulativo de pacote.

Armazenar todas as versões do pacote (deixa) na salva de índice de registro para o número de solicitações HTTP necessária para metadados de pacote de busca, mas significa que um documento maior deve ser baixado e mais memória do cliente deve ser alocada. Por outro lado, se a implementação do servidor armazena imediatamente deixa de registro em documentos de página separada, o cliente deve executar mais solicitações HTTP para obter as informações necessárias.

A heurística nuget.org usa é o seguinte: se houver 128 ou mais versões de um pacote, quebrar a deixa em páginas de tamanho 64. Se houver menos de 128 versões, embutido todos os deixa o índice de registro.

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
Itens | Matriz de objetos | sim      | A matriz de páginas de registro

Cada item no objeto de índice `items` matriz é um objeto JSON que representa uma página de registro.

#### <a name="registration-page-object"></a>Objeto de página de registro

O objeto de página de registro encontrado no índice de registro tem as seguintes propriedades:

Nome   | Tipo             | Necessária | Observações
------ | ---------------- | -------- | -----
@id    | cadeia de caracteres           | sim      | A URL para a página de registro
count  | inteiro          | sim      | O número de registro deixa na página
Itens  | Matriz de objetos | no       | A matriz de folhas de registro e seus metadados associados
Inferior  | cadeia de caracteres           | sim      | A versão mais antiga do SemVer 2.0.0 na página (inclusiva)
pai | cadeia de caracteres           | no       | A URL para o índice de registro
superior  | cadeia de caracteres           | sim      | A versão mais recente SemVer 2.0.0 na página (inclusiva)

O `lower` e `upper` dos limites do objeto de página são úteis quando os metadados para uma versão de uma página específica é necessária.
Esses limites podem ser usados para buscar a página de registro somente necessário. As cadeias de caracteres de versão aderem a [as regras de versão do NuGet](../reference/package-versioning.md). As cadeias de caracteres de versão são normalizadas e não incluem os metadados de compilação. Como com todas as versões no ecossistema do NuGet, comparação de cadeias de caracteres de versão é implementada usando [SemVer 2.0.0's as regras de precedência versão](http://semver.org/spec/v2.0.0.html#spec-item-11).

O `parent` propriedade só aparecerá se o objeto de página de registro tem o `items` propriedade.

Se o `items` propriedade não está presente no objeto de página de registro, a URL especificada no `@id` deve ser usado para buscar metadados sobre as versões de pacote individuais. O `items` matriz às vezes é excluída do objeto de página como uma otimização. Se o número de versões de uma único pacote ID for muito grande, o documento de índice de registro será grandes e desnecessário ao processo para um cliente que só se preocupa com uma versão específica ou um pequeno intervalo de versões.

Observe que, se o `items` propriedade estiver presente, o `@id` propriedade não precisa ser usada, desde que todos os dados de página já está embutido no `items` propriedade.

Cada item no objeto de página `items` matriz é um objeto JSON que representa uma folha de registro e ele tem metadados associados.

#### <a name="registration-leaf-object-in-a-page"></a>Objeto de folha de registro em uma página

O objeto de folha de registro encontrado em uma página de registro tem as seguintes propriedades:

Nome           | Tipo   | Necessária | Observações
-------------- | ------ | -------- | -----
@id            | cadeia de caracteres | sim      | A URL para a folha de registro
catalogEntry   | objeto | sim      | A entrada do catálogo que contém os metadados do pacote
packageContent | cadeia de caracteres | sim      | A URL para o conteúdo do pacote (. nupkg)

Cada objeto de folha de registro representa os dados associados com uma versão do pacote único.

#### <a name="catalog-entry"></a>Entrada de catálogo

O `catalogEntry` propriedade no objeto folha registro tem as seguintes propriedades:

Nome                     | Tipo                       | Necessária | Observações
------------------------ | -------------------------- | -------- | -----
@id                      | cadeia de caracteres                     | sim      | A URL usada para produzir esse objeto de documento
authors                  | cadeia de caracteres ou matriz de cadeias de caracteres | no       | 
dependencyGroups         | Matriz de objetos           | no       | A URL para o conteúdo do pacote (. nupkg)
descrição              | cadeia de caracteres                     | no       | 
iconUrl                  | cadeia de caracteres                     | no       | 
id                       | cadeia de caracteres                     | sim      | A ID do pacote
licenseUrl               | cadeia de caracteres                     | no       | 
listados                   | boolean                    | no       | Deve ser considerada como caso esteja ausente, listado
minClientVersion         | cadeia de caracteres                     | no       | 
projectUrl               | cadeia de caracteres                     | no       | 
Publicado                | cadeia de caracteres                     | no       | Uma cadeia de caracteres que contém um carimbo de hora ISO 8601 de quando o pacote foi publicado
requireLicenseAcceptance | boolean                    | no       | 
resumo                  | cadeia de caracteres                     | no       | 
marcações                     | cadeia de caracteres ou matriz de cadeia de caracteres  | no       | 
título                    | cadeia de caracteres                     | no       | 
version                  | cadeia de caracteres                     | sim      | A versão do pacote

O `dependencyGroups` propriedade é uma matriz de objetos que representam as dependências do pacote, agrupados por estrutura de destino. Se o pacote não tem dependências, o `dependencyGroups` propriedade está ausente, uma matriz em branco, ou o `dependencies` propriedade de todos os grupos está vazio ou ausente.

#### <a name="package-dependency-group"></a>Grupo de dependências do pacote

Cada objeto de dependência de grupo tem as seguintes propriedades:

Nome            | Tipo             | Necessária | Observações
--------------- | ---------------- | -------- | -----
targetFramework | cadeia de caracteres           | no       | A estrutura de destino que essas dependências são aplicáveis para
dependências    | Matriz de objetos | no       |

O `targetFramework` cadeia usa o formato implementado pela biblioteca do .NET do NuGet [NuGet.Frameworks](https://www.nuget.org/packages/NuGet.Frameworks/). Se nenhum `targetFramework` for especificado, o grupo de dependência se aplica a todas as estruturas de destino.

O `dependencies` propriedade é uma matriz de objetos, cada uma representando uma dependência de pacote do pacote atual.

#### <a name="package-dependency"></a>Dependência de pacote

A dependência de cada pacote tem as seguintes propriedades:

Nome         | Tipo   | Necessária | Observações
------------ | ------ | -------- | -----
id           | cadeia de caracteres | sim      | A ID da dependência do pacote
range        | objeto | no       | Permitidos [intervalo de versão](../reference/package-versioning.md#version-ranges-and-wildcards) da dependência
registro | cadeia de caracteres | no       | A URL para o índice de registro para essa dependência

Se o `range` propriedade for excluída ou uma cadeia de caracteres vazia, o cliente deve usar como padrão para o intervalo de versão `(, )`. Ou seja, qualquer versão da dependência é permitido.

### <a name="sample-request"></a>Solicitação de amostra

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

Nesse caso específico, o índice de registro tem a página de registro embutida forma nenhuma solicitação adicional é necessário para buscar metadados sobre as versões de pacote individuais.

## <a name="registration-page"></a>Página de registro

A página de registro contém deixa de registro. A URL para buscar uma página de registro é determinada pelo `@id` propriedade o [objeto da página de registro](#registration-page-object) mencionados acima.

Quando o `items` matriz não é fornecida no índice de registro, a solicitação de um HTTP GET do `@id` valor retornará um documento JSON que tem um objeto como sua raiz. O objeto tem as seguintes propriedades:

Nome   | Tipo             | Necessária | Observações
------ | ---------------- | -------- | -----
@id    | cadeia de caracteres           | sim      | A URL para a página de registro
count  | inteiro          | sim      | O número de registro deixa na página
Itens  | Matriz de objetos | sim      | A matriz de folhas de registro e seus metadados associados
Inferior  | cadeia de caracteres           | sim      | A versão mais antiga do SemVer 2.0.0 na página (inclusiva)
pai | cadeia de caracteres           | sim      | A URL para o índice de registro
superior  | cadeia de caracteres           | sim      | A versão mais recente SemVer 2.0.0 na página (inclusiva)

A forma dos objetos de folha de registro é o mesmo que o índice de registro [acima](#registration-leaf-object-in-a-page).

## <a name="sample-request"></a>Solicitação de amostra

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Folha de registro

A folha de registro contém informações sobre um pacote específico ID e a versão. Os metadados sobre a versão específica podem não estar disponível neste documento. Metadados de pacote devem ser buscados no [índice de registro](#registration-index) ou [página de registro](#registration-page) (que é descoberto usando o índice de registro).

A URL para buscar uma folha de registro é obtida do `@id` propriedade de um objeto de folha de registro em um índice de registro ou a página de registro.

A folha de registro é um documento JSON com um objeto de raiz com as seguintes propriedades:

Nome           | Tipo    | Necessária | Observações
-------------- | ------- | -------- | -----
@id            | cadeia de caracteres  | sim      | A URL para a folha de registro
catalogEntry   | cadeia de caracteres  | no       | A URL para a entrada do catálogo que produziu esses folha
listados         | boolean | no       | Deve ser considerada como caso esteja ausente, listado
packageContent | cadeia de caracteres  | no       | A URL para o conteúdo do pacote (. nupkg)
Publicado      | cadeia de caracteres  | no       | Uma cadeia de caracteres que contém um carimbo de hora ISO 8601 de quando o pacote foi publicado
registro   | cadeia de caracteres  | no       | A URL para o índice de registro

> [!Note]
> Em nuget.org, o `published` valor é definido para ano 1900 quando o pacote for removido da lista.

### <a name="sample-request"></a>Solicitação de amostra

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
