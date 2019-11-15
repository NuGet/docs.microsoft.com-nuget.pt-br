---
title: Metadados do pacote, API do NuGet
description: A URL base de registro do pacote permite buscar metadados sobre pacotes.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: eb8d59e253f85fbbb8546a5f71856df842ce94d6
ms.sourcegitcommit: 60414a17af65237652c1de9926475a74856b91cc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096893"
---
# <a name="package-metadata"></a>Metadados de pacote

É possível buscar metadados sobre os pacotes disponíveis em uma origem de pacote usando a API do NuGet v3. Esses metadados podem ser buscados usando o recurso de `RegistrationsBaseUrl` encontrado no [índice de serviço](service-index.md).

A coleção dos documentos encontrados em `RegistrationsBaseUrl` geralmente é chamada de "registros" ou "blobs de registro". O conjunto de documentos em um único `RegistrationsBaseUrl` é chamado de "hive de registro". Um hive de registro contém todos os metadados sobre cada pacote disponível em uma origem de pacote.

## <a name="versioning"></a>Controle de versão

Os seguintes valores de `@type` são usados:

Valor @type                     | Anotações
------------------------------- | -----
RegistrationsBaseUrl            | A versão inicial
RegistrationsBaseUrl/3.0.0-beta | Alias de `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-RC   | Alias de `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Gzip respostas
RegistrationsBaseUrl/3.6.0      | Inclui pacotes SemVer 2.0.0

Isso representa três hives de registro distintos disponíveis para várias versões de cliente.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Esses registros não são compactados (o que significa que usam um `Content-Encoding: identity`implícito). Os pacotes SemVer 2.0.0 são **excluídos** deste Hive.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Esses registros são compactados usando `Content-Encoding: gzip`. Os pacotes SemVer 2.0.0 são **excluídos** deste Hive.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Esses registros são compactados usando `Content-Encoding: gzip`. Os pacotes SemVer 2.0.0 estão **incluídos** neste Hive.
Para obter mais informações sobre SemVer 2.0.0, consulte [suporte do SemVer 2.0.0 para NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>URL Base

A URL base para as seguintes APIs é o valor da propriedade `@id` associada ao recurso mencionado anteriormente `@type` valores. No documento a seguir, a URL base do espaço reservado `{@id}` será usada.

## <a name="http-methods"></a>Métodos HTTP

Todas as URLs encontradas no recurso de registro dão suporte aos métodos HTTP `GET` e `HEAD`.

## <a name="registration-index"></a>Índice de registro

Os grupos de recursos de registro armazenam metadados por ID de pacote. Não é possível obter dados sobre mais de uma ID de pacote por vez. Esse recurso não fornece nenhuma maneira de descobrir IDs de pacote. Em vez disso, supõe-se que o cliente já conheça a ID de pacote desejada. Os metadados disponíveis sobre cada versão do pacote variam de acordo com a implementação do servidor. Os blobs de registro de pacote têm a seguinte estrutura hierárquica:

- **Index**: o ponto de entrada para os metadados do pacote, compartilhados por todos os pacotes em uma origem com a mesma ID de pacote.
- **Página**: um agrupamento de versões de pacote. O número de versões de pacote em uma página é definido pela implementação do servidor.
- **Folha**: um documento específico para uma versão de pacote único.

A URL do índice de registro é previsível e pode ser determinada pelo cliente dada uma ID de pacote e o valor de `@id` do recurso de registro do índice de serviço. As URLs para as páginas de registro e as folhas são descobertas inspecionando o índice de registro.

### <a name="registration-pages-and-leaves"></a>Páginas de registro e folhas

Embora não seja estritamente necessário para uma implementação de servidor armazenar folhas de registro em documentos de página de registro separados, é uma prática recomendada conservar a memória do lado do cliente. Em vez de enlinhar todas as folhas de registro no índice ou armazenar imediatamente as folhas em documentos de página, é recomendável que a implementação do servidor defina uma heurística para escolher entre as duas abordagens com base no número de versões de pacote ou tamanho cumulativo de folhas de pacote.

O armazenamento de todas as versões do pacote (folhas) no índice de registro salva o número de solicitações HTTP necessárias para buscar metadados do pacote, mas significa que um documento maior deve ser baixado e mais memória do cliente deve ser alocada. Por outro lado, se a implementação do servidor armazenar imediatamente as folhas de registro em documentos de página separados, o cliente deverá executar mais solicitações HTTP para obter as informações necessárias.

A heurística que o nuget.org usa é a seguinte: se houver 128 ou mais versões de um pacote, quebre as folhas em páginas de tamanho 64. Se houver menos de 128 versões, embutidas todas as folhas no índice de registro. Observe que isso significa que os pacotes com 65 a 127 versões terão duas páginas no índice, mas as duas páginas serão embutidas.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parâmetros de solicitação

Name     | No     | Digite    | Necessária | Anotações
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | cadeia de caracteres  | sim      | A ID do pacote, em letras minúsculas

O valor `LOWER_ID` é a ID de pacote desejada com letras minúsculas usando as regras implementadas pelo. Método de [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) da rede.

### <a name="response"></a>Resposta

A resposta é um documento JSON que tem um objeto raiz com as seguintes propriedades:

Name  | Digite             | Necessária | Anotações
----- | ---------------- | -------- | -----
count | inteiro          | sim      | O número de páginas de registro no índice
los | matriz de objetos | sim      | A matriz de páginas de registro

Cada item na matriz de `items` do objeto de índice é um objeto JSON que representa uma página de registro.

#### <a name="registration-page-object"></a>Objeto da página de registro

O objeto de página de registro encontrado no índice de registro tem as seguintes propriedades:

Name   | Digite             | Necessária | Anotações
------ | ---------------- | -------- | -----
@id    | cadeia de caracteres           | sim      | A URL para a página de registro
count  | inteiro          | sim      | O número de folhas de registro na página
los  | matriz de objetos | no       | A matriz de folhas de registro e seus metadados associados
canto  | cadeia de caracteres           | sim      | A versão mais baixa do SemVer 2.0.0 na página (inclusiva)
primária | cadeia de caracteres           | no       | A URL para o índice de registro
canto superior  | cadeia de caracteres           | sim      | A versão mais alta do SemVer 2.0.0 na página (inclusiva)

Os limites `lower` e `upper` do objeto Page são úteis quando são necessários os metadados para uma versão de página específica.
Esses limites podem ser usados para buscar a única página de registro necessária. As cadeias de caracteres de versão aderem às [regras de versão do NuGet](../concepts/package-versioning.md). As cadeias de caracteres de versão são normalizadas e não incluem metadados de compilação. Assim como em todas as versões no ecossistema do NuGet, a comparação de cadeias de caracteres de versão é implementada usando [regras de precedência de versão do SemVer 2.0.0](https://semver.org/spec/v2.0.0.html#spec-item-11).

A propriedade `parent` só será exibida se o objeto da página de registro tiver a propriedade `items`.

Se a propriedade `items` não estiver presente no objeto de página de registro, a URL especificada na `@id` deverá ser usada para buscar metadados sobre versões de pacotes individuais. Às vezes, a matriz de `items` é excluída do objeto Page como uma otimização. Se o número de versões de uma única ID de pacote for muito grande, o documento de índice de registro será maciço e não poderá ser processado para um cliente que se preocupa apenas com uma versão específica ou um pequeno intervalo de versões.

Observe que, se a propriedade `items` estiver presente, a propriedade `@id` não precisará ser usada, já que todos os dados da página já estão embutidos na propriedade `items`.

Cada item na matriz de `items` do objeto Page é um objeto JSON que representa uma folha de registro e seus metadados associados.

#### <a name="registration-leaf-object-in-a-page"></a>Objeto folha de registro em uma página

O objeto folha de registro encontrado em uma página de registro tem as seguintes propriedades:

Name           | Digite   | Necessária | Anotações
-------------- | ------ | -------- | -----
@id            | cadeia de caracteres | sim      | A URL para a folha de registro
catalogEntry   | objeto | sim      | A entrada de catálogo que contém os metadados do pacote
packageContent | cadeia de caracteres | sim      | A URL para o conteúdo do pacote (. nupkg)

Cada objeto folha de registro representa os dados associados a uma única versão de pacote.

#### <a name="catalog-entry"></a>Entrada do catálogo

A propriedade `catalogEntry` no objeto folha de registro tem as seguintes propriedades:

Name                     | Digite                       | Necessária | Anotações
------------------------ | -------------------------- | -------- | -----
@id                      | cadeia de caracteres                     | sim      | A URL para o documento usado para produzir este objeto
authors                  | String ou matriz de cadeias de caracteres | no       | 
dependencyGroups         | matriz de objetos           | no       | As dependências do pacote, agrupadas por estrutura de destino
substituição              | objeto                     | no       | A reprovação associada ao pacote
descrição              | cadeia de caracteres                     | no       | 
iconUrl                  | cadeia de caracteres                     | no       | 
id                       | cadeia de caracteres                     | sim      | A ID do pacote
licenseUrl               | cadeia de caracteres                     | no       |
carteira de licença        | cadeia de caracteres                     | no       | 
listados                   | boolean                    | no       | Deve ser considerado como listado, se ausente
minClientVersion         | cadeia de caracteres                     | no       | 
projectUrl               | cadeia de caracteres                     | no       | 
Checked                | cadeia de caracteres                     | no       | Uma cadeia de caracteres que contém um carimbo de data/hora ISO 8601 de quando o pacote foi publicado
requireLicenseAcceptance | boolean                    | no       | 
resumo                  | cadeia de caracteres                     | no       | 
marcações                     | Cadeia de caracteres ou matriz de cadeia de caracteres  | no       | 
título                    | cadeia de caracteres                     | no       | 
version                  | cadeia de caracteres                     | sim      | A cadeia de caracteres de versão completa após a normalização

O pacote `version` propriedade é a cadeia de caracteres de versão completa após a normalização. Isso significa que os dados de compilação SemVer 2.0.0 podem ser incluídos aqui.

A propriedade `dependencyGroups` é uma matriz de objetos que representa as dependências do pacote, agrupadas por estrutura de destino. Se o pacote não tiver dependências, a propriedade `dependencyGroups` estiver ausente, uma matriz vazia ou a propriedade `dependencies` de todos os grupos estará vazia ou ausente.

O valor da propriedade `licenseExpression` está em conformidade com a [sintaxe de expressão de licença do NuGet](https://docs.microsoft.com/nuget/reference/nuspec#license).

> [!Note]
> Em nuget.org, o valor `published` é definido como ano 1900 quando o pacote é deslistado.

#### <a name="package-dependency-group"></a>Grupo de dependências do pacote

Cada objeto de grupo de dependências tem as seguintes propriedades:

Name            | Digite             | Necessária | Anotações
--------------- | ---------------- | -------- | -----
targetFramework | cadeia de caracteres           | no       | A estrutura de destino à qual essas dependências se aplicam
dependências    | matriz de objetos | no       |

A cadeia de caracteres de `targetFramework` usa o formato implementado pela biblioteca .NET NuGet do NuGet. [frameworks](https://www.nuget.org/packages/NuGet.Frameworks/). Se nenhum `targetFramework` for especificado, o grupo de dependências se aplicará a todas as estruturas de destino.

A propriedade `dependencies` é uma matriz de objetos, cada um representando uma dependência de pacote do pacote atual.

#### <a name="package-dependency"></a>Dependência do pacote

Cada dependência de pacote tem as seguintes propriedades:

Name         | Digite   | Necessária | Anotações
------------ | ------ | -------- | -----
id           | cadeia de caracteres | sim      | A ID da dependência do pacote
range        | objeto | no       | O [intervalo de versão](../concepts/package-versioning.md#version-ranges-and-wildcards) permitido da dependência
registro | cadeia de caracteres | no       | A URL para o índice de registro desta dependência

Se a propriedade `range` for excluída ou uma cadeia de caracteres vazia, o cliente deverá padrão para o intervalo de versão `(, )`. Ou seja, qualquer versão da dependência é permitida. O valor de `*` não é permitido para a propriedade `range`.

#### <a name="package-deprecation"></a>Substituição de pacote

Cada substituição de pacote tem as seguintes propriedades:

Name             | Digite             | Necessária | Anotações
---------------- | ---------------- | -------- | -----
motivos          | Matriz de cadeias de caracteres | sim      | Os motivos pelos quais o pacote foi preterido
mensagem          | cadeia de caracteres           | no       | Os detalhes adicionais sobre essa reprovação
alternatePackage | objeto           | no       | O pacote alternativo que deve ser usado em vez disso

A propriedade `reasons` deve conter pelo menos uma cadeia de caracteres e deve incluir apenas as cadeias da tabela a seguir:

Motivo       | Descrição             
------------ | -----------
Herdado       | O pacote não é mais mantido
CriticalBugs | O pacote tem bugs que o tornam inadequado para uso
Outros        | O pacote foi preterido devido a um motivo que não está nessa lista

Se a propriedade `reasons` contiver cadeias de caracteres que não sejam do conjunto conhecido, elas deverão ser ignoradas. As cadeias de caracteres não diferenciam maiúsculas de minúsculas, portanto `legacy` devem ser tratados da mesma forma que `Legacy`. Não há nenhuma restrição de ordenação na matriz, portanto, as cadeias de caracteres podem ser organizadas em qualquer ordem arbitrária. Além disso, se a propriedade contiver apenas cadeias de caracteres que não sejam do conjunto conhecido, ela deverá ser tratada como se ela contivesse apenas a "outra" cadeia de caracteres.

#### <a name="alternate-package"></a>Pacote alternativo

O objeto de pacote alternativo tem as seguintes propriedades:

Name         | Digite   | Necessária | Anotações
------------ | ------ | -------- | -----
id           | cadeia de caracteres | sim      | A ID do pacote alternativo
range        | objeto | no       | O [intervalo de versão](../concepts/package-versioning.md#version-ranges-and-wildcards)permitido ou `*` se qualquer versão for permitida
registro | cadeia de caracteres | no       | A URL para o índice de registro para este pacote alternativo

### <a name="sample-request"></a>Exemplo de solicitação

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>Exemplo de resposta

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

Nesse caso em particular, o índice de registro tem a página de registro embutida, portanto, nenhuma solicitação extra é necessária para buscar metadados sobre versões de pacotes individuais.

## <a name="registration-page"></a>Página de registro

A página de registro contém folhas de registro. A URL para buscar uma página de registro é determinada pela propriedade `@id` no [objeto de página de registro](#registration-page-object) mencionado acima. A URL não é destinada a ser previsível e sempre deve ser descoberta por meio do documento de índice.

> [!Warning]
> No nuget.org, a URL do documento da página de registro contém coincidentemente o limite inferior e superior da página. No entanto, essa suposição nunca deve ser feita por um cliente, já que as implementações de servidor são livres para alterar a forma da URL, desde que o documento de índice tenha um link válido.

Quando a matriz de `items` não for fornecida no índice de registro, uma solicitação HTTP GET do valor de `@id` retornará um documento JSON que tem um objeto como sua raiz. O objeto tem as seguintes propriedades:

Name   | Digite             | Necessária | Anotações
------ | ---------------- | -------- | -----
@id    | cadeia de caracteres           | sim      | A URL para a página de registro
count  | inteiro          | sim      | O número de folhas de registro na página
los  | matriz de objetos | sim      | A matriz de folhas de registro e seus metadados associados
canto  | cadeia de caracteres           | sim      | A versão mais baixa do SemVer 2.0.0 na página (inclusiva)
primária | cadeia de caracteres           | sim      | A URL para o índice de registro
canto superior  | cadeia de caracteres           | sim      | A versão mais alta do SemVer 2.0.0 na página (inclusiva)

A forma dos objetos folha do registro é a mesma do índice de registro [acima](#registration-leaf-object-in-a-page).

## <a name="sample-request"></a>Exemplo de solicitação

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>Exemplo de resposta

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Folha de registro

A folha de registro contém informações sobre uma ID e versão do pacote específico. Os metadados sobre a versão específica podem não estar disponíveis neste documento. Os metadados do pacote devem ser buscados no [índice de registro](#registration-index) ou na página de [registro](#registration-page) (que é descoberta usando o índice de registro).

A URL para buscar uma folha de registro é obtida da propriedade `@id` de um objeto folha de registro em um índice de registro ou em uma página de registro. Como no documento da página. a URL não é destinada a ser previsível e sempre deve ser descoberta por meio do objeto de página de registro.

> [!Warning]
> Em nuget.org, a URL para o documento folha de registro contém a versão do pacote. No entanto, essa suposição nunca deve ser feita por um cliente, já que as implementações de servidor são livres para alterar a forma da URL, desde que o documento pai tenha um link válido. 

A folha de registro é um documento JSON com um objeto raiz com as seguintes propriedades:

Name           | Digite    | Necessária | Anotações
-------------- | ------- | -------- | -----
@id            | cadeia de caracteres  | sim      | A URL para a folha de registro
catalogEntry   | cadeia de caracteres  | no       | A URL para a entrada do catálogo que produziu estas folhas
listados         | boolean | no       | Deve ser considerado como listado, se ausente
packageContent | cadeia de caracteres  | no       | A URL para o conteúdo do pacote (. nupkg)
Checked      | cadeia de caracteres  | no       | Uma cadeia de caracteres que contém um carimbo de data/hora ISO 8601 de quando o pacote foi publicado
registro   | cadeia de caracteres  | no       | A URL para o índice de registro

> [!Note]
> Em nuget.org, o valor `published` é definido como ano 1900 quando o pacote é deslistado.

### <a name="sample-request"></a>Exemplo de solicitação

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>Exemplo de resposta

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
