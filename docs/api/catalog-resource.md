---
title: Recurso de catálogo, API NuGet v3
description: O catálogo é um índice de todos os pacotes criados e excluídos em nuget.org.
author: joelverhagen
ms.author: jver
ms.date: 10/30/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 11485f583d6993919f6bb8acabcc87d9e4261975
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774150"
---
# <a name="catalog"></a>Catálogo

O **Catálogo** é um recurso que registra todas as operações de pacote em uma origem de pacote, como criações e exclusões. O recurso de catálogo tem o `Catalog` tipo no [índice de serviço](service-index.md). Você pode usar esse recurso para [consultar todos os pacotes publicados](../guides/api/query-for-all-published-packages.md).

> [!Note]
> Como o catálogo não é usado pelo cliente do NuGet oficial, nem todas as origens do pacote implementam o catálogo.

> [!Note]
> Atualmente, o catálogo nuget.org não está disponível na China. Para obter mais detalhes, consulte [NuGet/NuGetGallery # 4949](https://github.com/NuGet/NuGetGallery/issues/4949).

## <a name="versioning"></a>Controle de versão

O seguinte `@type` valor é usado:

@type valor   | Observações
------------- | -----
Catálogo/3.0.0 | A versão inicial

## <a name="base-url"></a>URL base

A URL do ponto de entrada para as seguintes APIs é o valor da `@id` propriedade associada aos valores de recursos mencionados anteriormente `@type` . Este tópico usa a URL do espaço reservado `{@id}` .

## <a name="http-methods"></a>Métodos HTTP

Todas as URLs encontradas no recurso de catálogo dão suporte apenas aos métodos HTTP `GET` e `HEAD` .

## <a name="catalog-index"></a>Índice do catálogo

O índice de catálogo é um documento em um local conhecido que tem uma lista de itens de catálogo, ordenada cronologicamente. É o ponto de entrada do recurso de catálogo.

O índice é composto de páginas de catálogo. Cada página do catálogo contém itens de catálogo. Cada item de catálogo representa um evento sobre um único pacote em um ponto no tempo. Um item de catálogo pode representar um pacote que foi criado, não listado, relistado ou excluído da origem do pacote. Ao processar os itens de catálogo em ordem cronológica, o cliente pode criar uma exibição atualizada de cada pacote existente na origem do pacote v3.

Em suma, os blobs de catálogo têm a seguinte estrutura hierárquica:

- **Índice**: o ponto de entrada para o catálogo.
- **Página**: um agrupamento de itens de catálogo.
- **Folha**: um documento que representa um item de catálogo, que é um instantâneo do estado de um único pacote.

Cada objeto de catálogo tem uma propriedade chamada `commitTimeStamp` representando quando o item foi adicionado ao catálogo. Os itens de catálogo são adicionados a uma página de catálogo em lotes chamados confirmações. Todos os itens de catálogo na mesma confirmação têm o mesmo carimbo de data/hora de confirmação ( `commitTimeStamp` ) e ID de confirmação ( `commitId` ). Os itens de catálogo colocados na mesma confirmação representam os eventos que ocorreram em vez do mesmo ponto no tempo na origem do pacote. Não há nenhuma ordenação dentro de uma confirmação de catálogo.

Como cada ID de pacote e versão é exclusiva, nunca haverá mais de um item de catálogo em uma confirmação. Isso garante que os itens de catálogo para um único pacote sempre possam ser ordenados sem ambigüidade em relação ao carimbo de data/hora de confirmação.

Nunca há mais de uma confirmação para o catálogo por `commitTimeStamp` . Em outras palavras, o `commitId` é redundante com o `commitTimeStamp` .

Ao contrário do [recurso de metadados do pacote](registration-base-url-resource.md), que é indexado pela ID do pacote, o catálogo é indexado (e passível de consulta) somente por tempo.

Os itens de catálogo são sempre adicionados ao catálogo em uma ordem cronológica crescente de forma monotônico. Isso significa que, se uma confirmação de catálogo for adicionada no momento X, nenhuma confirmação de catálogo será adicionada com um tempo menor ou igual a X.

A solicitação a seguir busca o índice do catálogo.

```
GET {@id}
```

O índice de catálogo é um documento JSON que contém um objeto com as seguintes propriedades:

Nome            | Type             | Necessária | Observações
--------------- | ---------------- | -------- | -----
commitId        | string           | sim      | Uma ID exclusiva associada à confirmação mais recente
commitTimeStamp | string           | sim      | Um carimbo de data/hora da confirmação mais recente
count           | Número inteiro          | sim      | O número de páginas no índice
itens           | matriz de objetos | sim      | Uma matriz de objetos, cada objeto que representa uma página

Cada elemento na `items` matriz é um objeto com alguns detalhes mínimos sobre cada página. Esses objetos de página não contêm as folhas de catálogo (itens). A ordem dos elementos nesta matriz não está definida. As páginas podem ser ordenadas pelo cliente na memória usando sua `commitTimeStamp` propriedade.

À medida que novas páginas são introduzidas, os `count` objetos serão incrementados e novos serão exibidos na `items` matriz.

À medida que os itens são adicionados ao catálogo, o índice `commitId` será alterado e o `commitTimeStamp` aumento será aumentado. Essas duas propriedades são essencialmente um resumo em todos os `commitId` `commitTimeStamp` valores de página e na `items` matriz.

### <a name="catalog-page-object-in-the-index"></a>Objeto de página de catálogo no índice

Os objetos de página de catálogo encontrados na Propriedade do índice de catálogo `items` têm as seguintes propriedades:

Nome            | Type    | Necessária | Observações
--------------- | ------- | -------- | -----
@id             | string  | sim      | A URL para buscar a página do catálogo
commitId        | string  | sim      | Uma ID exclusiva associada à confirmação mais recente nesta página
commitTimeStamp | string  | sim      | Um carimbo de data/hora da confirmação mais recente nesta página
count           | Número inteiro | sim      | O número de itens na página do catálogo

Ao contrário do [recurso de metadados do pacote](registration-base-url-resource.md) , que, em alguns casos, deixa de lado no índice, as folhas de catálogo nunca são embutidas no índice e sempre devem ser buscadas usando a URL da página `@id` .

### <a name="sample-request"></a>Solicitação de exemplo

```
GET https://api.nuget.org/v3/catalog0/index.json
```

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>Página do catálogo

A página catálogo é uma coleção de itens de catálogo. É um documento buscado usando um dos `@id` valores encontrados no índice do catálogo. A URL para uma página de catálogo não se destina a ser previsível e deve ser descoberta usando apenas o índice de catálogo.

Novos itens de catálogo são adicionados à página no índice de catálogo somente com o carimbo de data/hora de confirmação mais alto ou em uma nova página. Quando uma página com um carimbo de data/hora de confirmação maior é adicionada ao catálogo, as páginas mais antigas nunca são adicionadas ou alteradas.

O documento de página de catálogo é um objeto JSON com as seguintes propriedades:

Nome            | Type             | Necessária | Observações
--------------- | ---------------- | -------- | -----
commitId        | string           | sim      | Uma ID exclusiva associada à confirmação mais recente nesta página
commitTimeStamp | string           | sim      | Um carimbo de data/hora da confirmação mais recente nesta página
count           | Número inteiro          | sim      | O número de itens na página
itens           | matriz de objetos | sim      | Os itens de catálogo nesta página
pai          | string           | sim      | Uma URL para o índice do catálogo

Cada elemento na `items` matriz é um objeto com alguns detalhes mínimos sobre o item de catálogo. Esses objetos de item não contêm todos os dados do item do catálogo. A ordem dos itens na matriz da página `items` não está definida. Os itens podem ser ordenados pelo cliente na memória usando sua `commitTimeStamp` propriedade.

O número de itens de catálogo em uma página é definido pela implementação do servidor. Para nuget.org, há no máximo 550 itens em cada página, embora o número real possa ser menor para algumas páginas, dependendo do tamanho do próximo lote de confirmação no momento.

À medida que novos itens são introduzidos, os `count` objetos de item de catálogo são incrementados e novos aparecem na `items` matriz.

À medida que os itens são adicionados à página, as `commitId` alterações e as `commitTimeStamp` aumentam. Essas duas propriedades são essencialmente um resumo sobre todos `commitId` os `commitTimeStamp` valores e na `items` matriz.

### <a name="catalog-item-object-in-a-page"></a>Objeto de item de catálogo em uma página

Os objetos de item de catálogo encontrados na propriedade da página do catálogo `items` têm as seguintes propriedades:

Nome            | Type    | Necessária | Observações
--------------- | ------- | -------- | -----
@id             | string  | sim      | A URL para buscar o item de catálogo
@type           | string  | sim      | O tipo do item de catálogo
commitId        | string  | sim      | A ID de confirmação associada a este item de catálogo
commitTimeStamp | string  | sim      | O carimbo de data/hora de confirmação deste item de catálogo
NuGet: ID        | string  | sim      | A ID do pacote à qual esta folha está relacionada
NuGet: versão   | string  | sim      | A versão do pacote à qual esta folha está relacionada

O `@type` valor será um dos dois valores a seguir:

1. `nuget:PackageDetails`: isso corresponde ao `PackageDetails` tipo no documento folha do catálogo.
1. `nuget:PackageDelete`: isso corresponde ao `PackageDelete` tipo no documento folha do catálogo.

Para obter mais detalhes sobre o que cada tipo significa, consulte o [tipo de itens correspondentes](#item-types) abaixo.

### <a name="sample-request"></a>Solicitação de exemplo

```
GET https://api.nuget.org/v3/catalog0/page2926.json
```

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>Folha do catálogo

A folha catálogo contém metadados sobre uma ID e versão de pacote específicos em algum momento. É um documento buscado usando o `@id` valor encontrado em uma página de catálogo. A URL para uma folha de catálogo não se destina a ser previsível e deve ser descoberta usando apenas uma página de catálogo.

O documento folha do catálogo é um objeto JSON com as seguintes propriedades:

Nome                    | Type                       | Necessária | Observações
----------------------- | -------------------------- | -------- | -----
@type                   | cadeia de caracteres ou matriz de cadeias de caracteres | sim      | Os tipos do item de catálogo
Catálogo: ConfirmID        | string                     | sim      | Uma ID de confirmação associada a este item de catálogo
Catálogo: commitTimeStamp | string                     | sim      | O carimbo de data/hora de confirmação deste item de catálogo
id                      | string                     | sim      | A ID do pacote do item de catálogo
published               | string                     | sim      | A data de publicação do item de catálogo do pacote
version                 | string                     | sim      | A versão do pacote do item de catálogo

### <a name="item-types"></a>Tipos de item

A `@type` propriedade é uma cadeia de caracteres ou uma matriz de cadeias. Para sua conveniência, se o `@type` valor for uma cadeia de caracteres, ele deverá ser tratado como qualquer matriz do tamanho um. Nem todos os valores possíveis para `@type` estão documentados. No entanto, cada item de catálogo tem exatamente um dos dois valores de tipo de cadeia de caracteres a seguir:

1. `PackageDetails`: representa um instantâneo dos metadados do pacote
1. `PackageDelete`: representa um pacote que foi excluído

### <a name="package-details-catalog-items"></a>Itens do catálogo detalhes do pacote

Itens de catálogo com o tipo `PackageDetails` contêm um instantâneo dos metadados do pacote para um pacote específico (combinação de ID e versão). Um item de catálogo detalhes do pacote é produzido quando uma origem do pacote encontra qualquer um dos seguintes cenários:

1. Um pacote é **enviado por push**.
1. Um pacote é **listado**.
1. Um pacote não está **listado**.
1. Um pacote é **refluído**.

Um refluxo de pacote é um gesto administrativo que basicamente gera um envio falso de um pacote existente sem alterações no pacote em si. No nuget.org, um refluxo é usado após a correção de um bug em um dos trabalhos em segundo plano que consomem o catálogo.

Os clientes que consomem os itens de catálogo não devem tentar determinar quais desses cenários produziram o item de catálogo. Em vez disso, o cliente deve simplesmente atualizar qualquer exibição ou índice mantido com os metadados contidos no item de catálogo. Além disso, itens de catálogo duplicados ou redundantes devem ser manipulados normalmente (forma idempotencial).

Os itens do catálogo detalhes do pacote têm as seguintes propriedades além das [incluídas em todas as folhas de catálogo](#catalog-leaf).

Nome                    | Type                       | Necessária | Observações
----------------------- | -------------------------- | -------- | -----
authors                 | string                     | não       |
criado                 | string                     | não       | Um carimbo de data/hora de quando o pacote foi criado pela primeira vez. Propriedade de fallback: `published` .
dependencyGroups        | matriz de objetos           | não       | As dependências do pacote, agrupadas por estrutura de destino ([mesmo formato que o recurso de metadados do pacote](registration-base-url-resource.md#package-dependency-group))
substituição             | objeto                     | não       | A reprovação associada ao pacote ([mesmo formato que o recurso de metadados do pacote](registration-base-url-resource.md#package-deprecation))
descrição             | string                     | não       |
iconUrl                 | string                     | não       |
isPrerelease            | booleano                    | não       | Se a versão do pacote é de pré-lançamento ou não. Pode ser detectado de `version` .
Linguagem                | string                     | não       |
licenseUrl              | string                     | não       |
listados                  | booleano                    | não       | Se o pacote está ou não listado
minClientVersion        | string                     | não       |
packageHash             | string                     | sim      | O hash do pacote, codificação usando a [base padrão 64](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | string                     | sim      |
packageSize             | Número inteiro                    | sim      | O tamanho do pacote. nupkg em bytes
packageTypes            | matriz de objetos           | não       | Os tipos de pacote especificados pelo autor.
projectUrl              | string                     | não       |
releaseNotes            | string                     | não       |
requireLicenseAgreement | booleano                    | não       | Assumir `false` se excluído
resumo                 | string                     | não       |
marcas                    | Matriz de cadeias de caracteres           | não       |
título                   | string                     | não       |
verbatimVersion         | string                     | não       | A cadeia de caracteres da versão como foi encontrada originalmente no. nuspec

A propriedade de pacote `version` é a cadeia de caracteres de versão completa após a normalização. Isso significa que os dados de compilação SemVer 2.0.0 podem ser incluídos aqui.

O `created` carimbo de data/hora é quando o pacote foi recebido pela primeira vez pela origem do pacote, que normalmente é um pouco tempo antes do carimbo de data/hora de confirmação do item do catálogo.

O `packageHashAlgorithm` é uma cadeia de caracteres definida pela implementação do servidor que representa o algoritmo de hash usado para produzir o `packageHash` . nuget.org sempre usou o `packageHashAlgorithm` valor de `SHA512` .

A `packageTypes` propriedade só estará presente se um tipo de pacote tiver sido especificado pelo autor. Se estiver presente, ele sempre terá pelo menos uma (1) entrada. Cada item na `packageTypes` matriz é um objeto JSON com as seguintes propriedades:

Nome      | Type    | Necessária | Observações
--------- | ------- | -------- | -----
name      | string  | sim      | O nome do tipo de pacote.
version    | string  | não       | A versão do tipo de pacote. Presente somente se o autor especificou explicitamente uma versão no nuspec.

O `published` carimbo de data/hora é o horário em que o pacote foi listado pela última vez.

> [!Note]
> Em nuget.org, o `published` valor é definido como o ano 1900 quando o pacote é deslistado.

#### <a name="sample-request"></a>Solicitação de exemplo

```
GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json
```

#### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>Excluir itens do catálogo de pacotes

Os itens de catálogo com o tipo `PackageDelete` contêm um conjunto mínimo de informações que indicam para os clientes de catálogo que um pacote foi excluído da origem do pacote e não está mais disponível para qualquer operação de pacote (como a restauração).

> [!NOTE]
> É possível que um pacote seja excluído e posteriormente publicado novamente usando a mesma ID e versão do pacote. No nuget.org, esse é um caso muito raro, pois ele interrompe a suposição do cliente oficial de que uma ID e a versão do pacote sugerem um conteúdo de pacote específico. Para obter mais informações sobre a exclusão de pacotes no nuget.org, consulte [nossa política](../nuget-org/policies/deleting-packages.md).

Os itens de catálogo de exclusão de pacote não têm propriedades adicionais além das [incluídas em todas as folhas de catálogo](#catalog-leaf).

A `version` propriedade é a cadeia de caracteres de versão original encontrada no pacote. nuspec.

A `published` propriedade é a hora em que o pacote foi excluído, que normalmente é tão curto quanto o carimbo de data/hora de confirmação do item de catálogo.

#### <a name="sample-request"></a>Solicitação de exemplo

```
GET https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json
```

#### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Cursor

### <a name="overview"></a>Visão geral

Esta seção descreve um conceito de cliente que, embora não seja necessariamente obrigatório pelo protocolo, deve fazer parte de qualquer implementação de cliente de catálogo prática.

Como o catálogo é uma estrutura de dados somente de acréscimo indexada por tempo, o cliente deve armazenar um **cursor** localmente, representando até que ponto no tempo o cliente processou os itens de catálogo. Observe que esse valor de cursor nunca deve ser gerado usando o relógio do computador do cliente. Em vez disso, o valor deve vir do valor de um objeto de catálogo `commitTimestamp` .

Sempre que o cliente deseja processar novos eventos na origem do pacote, ele precisa apenas consultar o catálogo em busca de todos os itens de catálogo com um carimbo de data/hora de confirmação maior do que o cursor armazenado. Depois que o cliente processa com êxito todos os novos itens de catálogo, ele registra o carimbo de data/hora de confirmação mais recente dos itens de catálogo apenas processados como seu novo valor de cursor.

Usando essa abordagem, o cliente pode ter certeza de que nunca perderá nenhum evento de pacote que ocorreu na origem do pacote.
Além disso, o cliente nunca precisa reprocessar eventos antigos antes do carimbo de data/hora de confirmação registrado do cursor.

Esse conceito poderoso de cursores é usado para muitos trabalhos em segundo plano do nuget.org e é usado para manter a própria API v3 atualizada. 

### <a name="initial-value"></a>Valor inicial

Quando o cliente do catálogo está iniciando pela primeira vez (e, portanto, não tem nenhum valor de cursor), ele deve usar um valor de cursor padrão de. NET `System.DateTimeOffset.MinValue` ou alguma noção análoga de carimbo de data/hora mínimo reapresentável.

### <a name="iterating-over-catalog-items"></a>Iterando em itens de catálogo

Para consultar o próximo conjunto de itens de catálogo a ser processado, o cliente deve:

1. Busque o valor de cursor gravado de um repositório local.
1. Baixar e desserializar o índice do catálogo.
1. Localiza todas as páginas do catálogo com um carimbo de data/hora de confirmação *maior que* o cursor.
1. Declare uma lista vazia de itens de catálogo a serem processados.
1. Para cada página do catálogo correspondente na etapa 3:
   1. Baixar e desserializar a página do catálogo.
   1. Localiza todos os itens de catálogo com um carimbo de data/hora de confirmação *maior que* o cursor.
   1. Adicione todos os itens de catálogo correspondentes à lista declarada na etapa 4.
1. Classifique a lista de itens de catálogo por confirmação de carimbo de data/hora.
1. Processar cada item de catálogo em sequência:
   1. Baixar e desserializar o item de catálogo.
   1. Reagir adequadamente ao tipo do item de catálogo.
   1. Processar o documento de item de catálogo de maneira específica do cliente.
1. Registre o carimbo de data/hora de confirmação do último item do catálogo como o novo valor de cursor.

Com esse algoritmo básico, a implementação do cliente pode criar uma exibição completa de todos os pacotes disponíveis na origem do pacote. O cliente precisa apenas executar esse algoritmo periodicamente para sempre estar ciente das alterações mais recentes na origem do pacote.

> [!Note]
> Esse é o algoritmo que o nuget.org usa para manter [os metadados do pacote](registration-base-url-resource.md), o conteúdo do [pacote](package-base-address-resource.md), a [pesquisa](search-query-service-resource.md) e os recursos de [preenchimento automático](search-autocomplete-service-resource.md) atualizados.

### <a name="dependent-cursors"></a>Cursores dependentes

Suponha que haja dois clientes de catálogo que têm uma dependência inerente em que a saída de um cliente depende da saída de outro cliente. 

#### <a name="example"></a>Exemplo

Por exemplo, em nuget.org, um pacote recentemente publicado não deve aparecer no recurso de pesquisa antes de aparecer no recurso de metadados do pacote. Isso ocorre porque a operação de "restauração" executada pelo cliente do NuGet oficial usa o recurso de metadados do pacote. Se um cliente descobre um pacote usando o serviço de pesquisa, ele deve ser capaz de restaurar com êxito esse pacote usando o recurso de metadados do pacote. Em outras palavras, o recurso de pesquisa depende do recurso de metadados do pacote. Cada recurso tem um trabalho em segundo plano do cliente de catálogo atualizando esse recurso. Cada cliente tem seu próprio cursor.

Como os dois recursos são criados fora do catálogo, o cursor do cliente do catálogo que atualiza o recurso de pesquisa *não deve ir além* do cursor do cliente do catálogo de metadados do pacote.

#### <a name="algorithm"></a>Algoritmo

Para implementar essa restrição, basta modificar o algoritmo acima para ser:

1. Busque o valor de cursor gravado de um repositório local.
1. Baixar e desserializar o índice do catálogo.
1. Localiza todas as páginas do catálogo com um carimbo de data/hora de confirmação *maior que* o cursor **menor ou igual ao cursor da dependência.**
1. Declare uma lista vazia de itens de catálogo a serem processados.
1. Para cada página do catálogo correspondente na etapa 3:
   1. Baixar e desserializar a página do catálogo.
   1. Localiza todos os itens de catálogo com um carimbo de data/hora de confirmação *maior que* o cursor **menor ou igual ao cursor da dependência.**
   1. Adicione todos os itens de catálogo correspondentes à lista declarada na etapa 4.
1. Classifique a lista de itens de catálogo por confirmação de carimbo de data/hora.
1. Processar cada item de catálogo em sequência:
   1. Baixar e desserializar o item de catálogo.
   1. Reagir adequadamente ao tipo do item de catálogo.
   1. Processar o documento de item de catálogo de maneira específica do cliente.
1. Registre o carimbo de data/hora de confirmação do último item do catálogo como o novo valor de cursor.

Usando esse algoritmo modificado, você pode criar um sistema de clientes de catálogo dependentes, todos produzindo seus próprios índices específicos, artefatos, etc.
