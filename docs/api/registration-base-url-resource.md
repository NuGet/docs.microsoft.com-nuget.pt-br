---
title: Metadados do pacote, API do NuGet
description: A URL base de registro do pacote permite buscar metadados sobre pacotes.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 8d1ab4d1f3d75d93c30d94958fd9d1abf0742730
ms.sourcegitcommit: af059dc776cfdcbad20baab2919b5d6dc1e9022d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2021
ms.locfileid: "99990119"
---
# <a name="package-metadata"></a>Metadados de pacote

É possível buscar metadados sobre os pacotes disponíveis em uma origem de pacote usando a API do NuGet v3. Esses metadados podem ser buscados usando o `RegistrationsBaseUrl` recurso encontrado no [índice de serviço](service-index.md).

A coleção dos documentos encontrados em `RegistrationsBaseUrl` geralmente é chamada de "registros" ou "blobs de registro". O conjunto de documentos em um único `RegistrationsBaseUrl` é chamado de "hive de registro". Um hive de registro contém todos os metadados sobre cada pacote disponível em uma origem de pacote.

## <a name="versioning"></a>Controle de versão

Os seguintes `@type` valores são usados:

@type valor                     | Observações
------------------------------- | -----
RegistrationsBaseUrl            | A versão inicial
RegistrationsBaseUrl/3.0.0-beta | Alias de `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-RC   | Alias de `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Gzip respostas
RegistrationsBaseUrl/3.6.0      | Inclui pacotes SemVer 2.0.0

Isso representa três hives de registro distintos disponíveis para várias versões de cliente.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Esses registros não são compactados (o que significa que usam um implícito `Content-Encoding: identity` ). Os pacotes SemVer 2.0.0 são **excluídos** deste Hive.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Esses registros são compactados usando o `Content-Encoding: gzip` . Os pacotes SemVer 2.0.0 são **excluídos** deste Hive.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Esses registros são compactados usando o `Content-Encoding: gzip` . Os pacotes SemVer 2.0.0 estão **incluídos** neste Hive.
Para obter mais informações sobre SemVer 2.0.0, consulte [suporte do SemVer 2.0.0 para NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>URL base

A URL base para as APIs a seguir é o valor da `@id` propriedade associada aos valores de recurso mencionados anteriormente `@type` . No documento a seguir, a URL base do espaço reservado `{@id}` será usada.

## <a name="http-methods"></a>Métodos HTTP

Todas as URLs encontradas no recurso de registro dão suporte aos métodos HTTP `GET` e `HEAD` .

## <a name="registration-index"></a>Índice de registro

Os grupos de recursos de registro armazenam metadados por ID de pacote. Não é possível obter dados sobre mais de uma ID de pacote por vez. Esse recurso não fornece nenhuma maneira de descobrir IDs de pacote. Em vez disso, supõe-se que o cliente já conheça a ID de pacote desejada. Os metadados disponíveis sobre cada versão do pacote variam de acordo com a implementação do servidor. Os blobs de registro de pacote têm a seguinte estrutura hierárquica:

- **Index**: o ponto de entrada para os metadados do pacote, compartilhados por todos os pacotes em uma origem com a mesma ID de pacote.
- **Página**: um agrupamento de versões de pacote. O número de versões de pacote em uma página é definido pela implementação do servidor.
- **Folha**: um documento específico para uma versão de pacote único.

A URL do índice de registro é previsível e pode ser determinada pelo cliente dado uma ID de pacote e o valor do recurso `@id` de registro do índice de serviço. As URLs para as páginas de registro e as folhas são descobertas inspecionando o índice de registro.

### <a name="registration-pages-and-leaves"></a>Páginas de registro e folhas

Embora não seja estritamente necessário para uma implementação de servidor armazenar folhas de registro em documentos de página de registro separados, é uma prática recomendada conservar a memória do lado do cliente. Em vez de incolocar todas as folhas de registro no índice ou armazenar imediatamente as folhas em documentos de página, é recomendável que a implementação do servidor defina alguma heurística para escolher entre as duas abordagens com base no número de versões de pacote ou tamanho cumulativo de folhas de pacote.

O armazenamento de todas as versões do pacote (folhas) no índice de registro salva o número de solicitações HTTP necessárias para buscar metadados do pacote, mas significa que um documento maior deve ser baixado e mais memória do cliente deve ser alocada. Por outro lado, se a implementação do servidor armazenar imediatamente as folhas de registro em documentos de página separados, o cliente deverá executar mais solicitações HTTP para obter as informações necessárias.

A heurística que o nuget.org usa é a seguinte: se houver 128 ou mais versões de um pacote, quebre as folhas em páginas de tamanho 64. Se houver menos de 128 versões, embutidas todas as folhas no índice de registro. Observe que isso significa que os pacotes com 65 a 127 versões terão duas páginas no índice, mas as duas páginas serão embutidas.

```
GET {@id}/{LOWER_ID}/index.json
```

### <a name="request-parameters"></a>Parâmetros da solicitação

Nome     | Em     | Tipo    | Obrigatório | Observações
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | sim      | A ID do pacote, em letras minúsculas

O `LOWER_ID` valor é a ID de pacote desejada com letras minúsculas usando as regras implementadas pelo. Método NET [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) .

### <a name="response"></a>Resposta

A resposta é um documento JSON que tem um objeto raiz com as seguintes propriedades:

Nome  | Tipo             | Obrigatório | Observações
----- | ---------------- | -------- | -----
count | Número inteiro          | sim      | O número de páginas de registro no índice
itens | matriz de objetos | sim      | A matriz de páginas de registro

Cada item na matriz do objeto de índice `items` é um objeto JSON que representa uma página de registro.

#### <a name="registration-page-object"></a>Objeto da página de registro

O objeto de página de registro encontrado no índice de registro tem as seguintes propriedades:

Nome   | Tipo             | Obrigatório | Observações
------ | ---------------- | -------- | -----
@id    | string           | sim      | A URL para a página de registro
count  | Número inteiro          | sim      | O número de folhas de registro na página
itens  | matriz de objetos | não       | A matriz de folhas de registro e seus metadados associados
lower  | string           | sim      | A versão mais baixa do SemVer 2.0.0 na página (inclusiva)
pai | string           | não       | A URL para o índice de registro
upper  | string           | sim      | A versão mais alta do SemVer 2.0.0 na página (inclusiva)

Os `lower` `upper` limites e do objeto Page são úteis quando são necessários os metadados para uma versão de página específica.
Esses limites podem ser usados para buscar a única página de registro necessária. As cadeias de caracteres de versão aderem às [regras de versão do NuGet](../concepts/package-versioning.md). As cadeias de caracteres de versão são normalizadas e não incluem metadados de compilação. Assim como em todas as versões no ecossistema do NuGet, a comparação de cadeias de caracteres de versão é implementada usando [regras de precedência de versão do SemVer 2.0.0](https://semver.org/spec/v2.0.0.html#spec-item-11).

A `parent` propriedade só será exibida se o objeto da página de registro tiver a `items` propriedade.

Se a `items` propriedade não estiver presente no objeto de página de registro, a URL especificada em `@id` deve ser usada para buscar metadados sobre versões de pacotes individuais. `items`Às vezes, a matriz é excluída do objeto Page como uma otimização. Se o número de versões de uma única ID de pacote for muito grande, o documento de índice de registro será maciço e não poderá ser processado para um cliente que se preocupa apenas com uma versão específica ou um pequeno intervalo de versões.

Observe que, se a `items` propriedade estiver presente, a `@id` propriedade não precisará ser usada, já que todos os dados da página já estão embutidos na `items` propriedade.

Cada item na matriz do objeto da página `items` é um objeto JSON que representa uma folha de registro e seus metadados associados.

#### <a name="registration-leaf-object-in-a-page"></a>Objeto folha de registro em uma página

O objeto folha de registro encontrado em uma página de registro tem as seguintes propriedades:

Nome           | Tipo   | Obrigatório | Observações
-------------- | ------ | -------- | -----
@id            | string | sim      | A URL para a folha de registro
catalogEntry   | object | sim      | A entrada de catálogo que contém os metadados do pacote
packageContent | string | sim      | A URL para o conteúdo do pacote (. nupkg)

Cada objeto folha de registro representa os dados associados a uma única versão de pacote.

#### <a name="catalog-entry"></a>Entrada do catálogo

A `catalogEntry` propriedade no objeto folha de registro tem as seguintes propriedades:

Nome                     | Tipo                       | Obrigatório | Observações
------------------------ | -------------------------- | -------- | -----
@id                      | string                     | sim      | A URL para o documento usado para produzir este objeto
authors                  | cadeia de caracteres ou matriz de cadeias de caracteres | não       | 
dependencyGroups         | matriz de objetos           | não       | As dependências do pacote, agrupadas por estrutura de destino
substituição              | object                     | não       | A reprovação associada ao pacote
descrição              | string                     | não       | 
iconUrl                  | string                     | não       | 
id                       | string                     | sim      | A ID do pacote
licenseUrl               | string                     | não       |
carteira de licença        | string                     | não       | 
listados                   | booleano                    | não       | Deve ser considerado como listado, se ausente
minClientVersion         | string                     | não       | 
projectUrl               | string                     | não       | 
published                | string                     | não       | Uma cadeia de caracteres que contém um carimbo de data/hora ISO 8601 de quando o pacote foi publicado
requireLicenseAcceptance | booleano                    | não       | 
resumo                  | string                     | não       | 
marcas                     | Cadeia de caracteres ou matriz de cadeia de caracteres  | não       | 
título                    | string                     | não       | 
version                  | string                     | sim      | A cadeia de caracteres de versão completa após a normalização
vulnerabilidades          | matriz de objetos           | não       | As vulnerabilidades de segurança do pacote

A propriedade de pacote `version` é a cadeia de caracteres de versão completa após a normalização. Isso significa que os dados de compilação SemVer 2.0.0 podem ser incluídos aqui.

A `dependencyGroups` propriedade é uma matriz de objetos que representa as dependências do pacote, agrupadas por estrutura de destino. Se o pacote não tiver dependências, a `dependencyGroups` Propriedade estará ausente, uma matriz vazia ou a `dependencies` propriedade de todos os grupos estará vazia ou ausente.

O valor da `licenseExpression` propriedade está em conformidade com a [sintaxe de expressão de licença do NuGet](../reference/nuspec.md#license).

> [!Note]
> Em nuget.org, o `published` valor é definido como ano 1900 quando o pacote é deslistado.

#### <a name="package-dependency-group"></a>Grupo de dependências do pacote

Cada objeto de grupo de dependências tem as seguintes propriedades:

Nome            | Tipo             | Obrigatório | Observações
--------------- | ---------------- | -------- | -----
targetFramework | string           | não       | A estrutura de destino à qual essas dependências se aplicam
dependencies    | matriz de objetos | não       |

A `targetFramework` cadeia de caracteres usa o formato implementado pela biblioteca .NET [NuGet do NuGet. frameworks](https://www.nuget.org/packages/NuGet.Frameworks/). Se não `targetFramework` for especificado, o grupo de dependências se aplicará a todas as estruturas de destino.

A `dependencies` propriedade é uma matriz de objetos, cada um representando uma dependência de pacote do pacote atual.

#### <a name="package-dependency"></a>Dependência do pacote

Cada dependência de pacote tem as seguintes propriedades:

Nome         | Tipo   | Obrigatório | Observações
------------ | ------ | -------- | -----
id           | string | sim      | A ID da dependência do pacote
range        | object | não       | O [intervalo de versão](../concepts/package-versioning.md#version-ranges) permitido da dependência
registro | string | não       | A URL para o índice de registro desta dependência

Se a `range` propriedade for excluída ou uma cadeia de caracteres vazia, o cliente deverá padronizar para o intervalo de versão `(, )` . Ou seja, qualquer versão da dependência é permitida. O valor de `*` não é permitido para a `range` propriedade.

#### <a name="package-deprecation"></a>Reprovação de pacote

Cada substituição de pacote tem as seguintes propriedades:

Nome             | Tipo             | Obrigatório | Observações
---------------- | ---------------- | -------- | -----
motivos          | Matriz de cadeias de caracteres | sim      | Os motivos pelos quais o pacote foi preterido
message          | string           | não       | Os detalhes adicionais sobre essa reprovação
alternatePackage | object           | não       | O pacote alternativo que deve ser usado em vez disso

A `reasons` propriedade deve conter pelo menos uma cadeia de caracteres e deve incluir apenas as cadeias da tabela a seguir:

Motivo       | Descrição             
------------ | -----------
Herdada       | O pacote não é mais mantido
CriticalBugs | O pacote tem bugs que o tornam inadequado para uso
Outro        | O pacote foi preterido devido a um motivo que não está nessa lista

Se a `reasons` Propriedade contiver cadeias de caracteres que não sejam do conjunto conhecido, elas deverão ser ignoradas. As cadeias de caracteres não diferenciam maiúsculas de minúsculas e, portanto, `legacy` devem ser tratadas da mesma forma que `Legacy` . Não há nenhuma restrição de ordenação na matriz, portanto, as cadeias de caracteres podem ser organizadas em qualquer ordem arbitrária. Além disso, se a propriedade contiver apenas cadeias de caracteres que não sejam do conjunto conhecido, ela deverá ser tratada como se ela contivesse apenas a "outra" cadeia de caracteres.

#### <a name="alternate-package"></a>Pacote alternativo

O objeto de pacote alternativo tem as seguintes propriedades:

Nome         | Tipo   | Obrigatório | Observações
------------ | ------ | -------- | -----
id           | string | sim      | A ID do pacote alternativo
range        | object | não       | O [intervalo de versão](../concepts/package-versioning.md#version-ranges)permitido ou `*` se qualquer versão for permitida

#### <a name="vulnerabilities"></a>Vulnerabilidades

Uma matriz de objetos de `vulnerability`. Cada vulnerabilidade tem as seguintes propriedades:

Nome         | Tipo   | Obrigatório | Observações
------------ | ------ | -------- | -----
advisoryUrl  | string | sim      | Local do comunicado de segurança para o pacote
severidade     | string | sim      | Severidade do comunicado: "0" = baixo, "1" = moderado, "2" = alto, "3" = crítico

### <a name="sample-request"></a>Solicitação de exemplo

```
GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json
```

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

Nesse caso em particular, o índice de registro tem a página de registro embutida, portanto, nenhuma solicitação extra é necessária para buscar metadados sobre versões de pacotes individuais.

## <a name="registration-page"></a>Página de registro

A página de registro contém folhas de registro. A URL para buscar uma página de registro é determinada pela `@id` propriedade no [objeto de página de registro](#registration-page-object) mencionado acima. A URL não é destinada a ser previsível e sempre deve ser descoberta por meio do documento de índice.

> [!Warning]
> No nuget.org, a URL do documento da página de registro contém coincidentemente o limite inferior e superior da página. No entanto, essa suposição nunca deve ser feita por um cliente, já que as implementações de servidor são livres para alterar a forma da URL, desde que o documento de índice tenha um link válido.

Quando a `items` matriz não for fornecida no índice de registro, uma solicitação HTTP Get do `@id` valor retornará um documento JSON que tem um objeto como sua raiz. O objeto tem as seguintes propriedades:

Nome   | Tipo             | Obrigatório | Observações
------ | ---------------- | -------- | -----
@id    | string           | sim      | A URL para a página de registro
count  | Número inteiro          | sim      | O número de folhas de registro na página
itens  | matriz de objetos | sim      | A matriz de folhas de registro e seus metadados associados
lower  | string           | sim      | A versão mais baixa do SemVer 2.0.0 na página (inclusiva)
pai | string           | sim      | A URL para o índice de registro
upper  | string           | sim      | A versão mais alta do SemVer 2.0.0 na página (inclusiva)

A forma dos objetos folha do registro é a mesma do índice de registro [acima](#registration-leaf-object-in-a-page).

## <a name="sample-request"></a>Solicitação de exemplo

```
GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json
```

## <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Folha de registro

A folha de registro contém informações sobre uma ID e versão do pacote específico. Os metadados sobre a versão específica podem não estar disponíveis neste documento. Os metadados do pacote devem ser buscados no [índice de registro](#registration-index) ou na página de [registro](#registration-page) (que é descoberta usando o índice de registro).

A URL para buscar uma folha de registro é obtida da `@id` propriedade de um objeto folha de registro em um índice de registro ou página de registro. Como no documento da página. a URL não é destinada a ser previsível e sempre deve ser descoberta por meio do objeto de página de registro.

> [!Warning]
> Em nuget.org, a URL para o documento folha de registro contém a versão do pacote. No entanto, essa suposição nunca deve ser feita por um cliente, já que as implementações de servidor são livres para alterar a forma da URL, desde que o documento pai tenha um link válido. 

A folha de registro é um documento JSON com um objeto raiz com as seguintes propriedades:

Nome           | Tipo    | Obrigatório | Observações
-------------- | ------- | -------- | -----
@id            | string  | sim      | A URL para a folha de registro
catalogEntry   | string  | não       | A URL para a entrada do catálogo que produziu estas folhas
listados         | booleano | não       | Deve ser considerado como listado, se ausente
packageContent | string  | não       | A URL para o conteúdo do pacote (. nupkg)
published      | string  | não       | Uma cadeia de caracteres que contém um carimbo de data/hora ISO 8601 de quando o pacote foi publicado
registro   | string  | não       | A URL para o índice de registro

> [!Note]
> Em nuget.org, o `published` valor é definido como ano 1900 quando o pacote é deslistado.

### <a name="sample-request"></a>Solicitação de exemplo

```
GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json
```

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
