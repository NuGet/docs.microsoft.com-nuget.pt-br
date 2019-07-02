---
title: Recurso de catálogo, a API do NuGet V3
description: O catálogo é um índice de todos os pacotes criados e excluídos em nuget.org.
author: joelverhagen
ms.author: jver
ms.date: 10/30/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 8e4fb376e471a207333d241aeb414da7d5c3571e
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496530"
---
# <a name="catalog"></a>Catálogo

O **catálogo** é um recurso que registra todas as operações de pacote em uma fonte de pacote, como as criações e exclusões. O recurso de catálogo tem o `Catalog` digite o [índice de serviço](service-index.md). Você pode usar este recurso para [de consulta para todos os pacotes de publicados](../guides/api/query-for-all-published-packages.md).

> [!Note]
> Como o catálogo não é usado pelo cliente do NuGet oficial, nem todas as fontes de pacote implementam o catálogo.

> [!Note]
> Atualmente, o catálogo de nuget.org não está disponível na China. Para obter mais detalhes, consulte [NuGet/NuGetGallery #4949](https://github.com/NuGet/NuGetGallery/issues/4949).

## <a name="versioning"></a>Controle de versão

O seguinte `@type` valor é usado:

Valor @type   | Observações
------------- | -----
Catalog/3.0.0 | A versão inicial

## <a name="base-url"></a>URL Base

A URL de ponto de entrada para as seguintes APIs é o valor da `@id` propriedade associada ao recurso mencionados anteriormente `@type` valores. Este tópico usa a URL de espaço reservado `{@id}`.

## <a name="http-methods"></a>Métodos HTTP

Todas as URLs encontradas no suporte a recurso de catálogo apenas os métodos HTTP `GET` e `HEAD`.

## <a name="catalog-index"></a>Índice do catálogo

O índice do catálogo é um documento em um local conhecido que tem uma lista de itens de catálogo, ordenadas em ordem cronológica. É o ponto de entrada do recurso de catálogo.

O índice é composto de páginas de catálogo. Cada página de catálogo contém itens de catálogo. Cada item de catálogo representa um evento sobre um único pacote em um ponto no tempo. Um item de catálogo pode representar um pacote que foi criado, não listados, listado novamente ou excluídos da origem do pacote. Ao processar os itens de catálogo em ordem cronológica, o cliente pode criar uma exibição atualizada de todos os pacotes que existe na origem do pacote V3.

Em resumo, os blobs de catálogo tem a seguinte estrutura hierárquica:

- **Índice**: o ponto de entrada para o catálogo.
- **Página**: um agrupamento de itens de catálogo.
- **Folha**: um documento que representa um item de catálogo, que é um instantâneo do estado de um único pacote.

Cada objeto de catálogo tem uma propriedade chamada o `commitTimeStamp` que representa quando o item foi adicionado ao catálogo. Itens de catálogo são adicionados a uma página de catálogo em lotes chamado confirmações. Todos os itens de catálogo na mesma confirmação têm o mesmo carimbo de hora de confirmação (`commitTimeStamp`) e a ID de confirmação (`commitId`). Itens de catálogo colocados na mesma confirmação representam os eventos que ocorreram em torno do mesmo ponto no tempo em que a origem do pacote. Não há nenhuma ordem dentro de uma confirmação de catálogo.

Como cada versão e a ID do pacote é exclusivo, nunca haverá mais de um item de catálogo em uma confirmação. Isso garante que os itens de catálogo para um único pacote podem sempre ser inequivocamente ordenados em relação ao carimbo de hora de confirmação.

Não há nunca ser mais de uma confirmação no catálogo por `commitTimeStamp`. Em outras palavras, o `commitId` são redundantes com o `commitTimeStamp`.

Em contraste com o [recurso de metadados do pacote](registration-base-url-resource.md), que é indexada pela ID do pacote, o catálogo é indexada (e passível de consulta) somente pelo tempo.

Itens de catálogo sempre são adicionados ao catálogo em uma ordem cronológica, com aumento monotônico. Isso significa que se uma confirmação de catálogo for adicionada no horário X, em seguida, nenhuma confirmação catálogo será adicionada com um tempo menor ou igual a X.

A seguinte solicitação de busca o índice do catálogo.

    GET {@id}

O índice do catálogo é um documento JSON que contém um objeto com as seguintes propriedades:

Nome            | Tipo             | Necessária | Observações
--------------- | ---------------- | -------- | -----
commitId        | cadeia de caracteres           | sim      | Uma ID exclusiva associada com a confirmação mais recente
commitTimeStamp | cadeia de caracteres           | sim      | Um carimbo de hora da confirmação mais recente
count           | inteiro          | sim      | O número de páginas no índice
items           | matriz de objetos | sim      | Uma matriz de objetos, cada objeto que representa uma página

Cada elemento no `items` matriz é um objeto com alguns detalhes mínimos sobre cada página. Esses objetos de página não contêm as folhas de catálogo (itens). A ordem dos elementos nesta matriz não está definida. As páginas podem ser solicitadas pelo cliente na memória usando seus `commitTimeStamp` propriedade.

Conforme novas páginas são introduzidas, o `count` será incrementado e novos objetos aparecerão no `items` matriz.

Como os itens são adicionados no catálogo, o índice `commitId` será alterado e o `commitTimeStamp` aumentará. Essas duas propriedades são, essencialmente, um resumo sobre a página todos os `commitId` e `commitTimeStamp` os valores no `items` matriz.

### <a name="catalog-page-object-in-the-index"></a>Objeto de página no índice do catálogo

Os objetos de página do catálogo encontrados no índice do catálogo `items` propriedade têm as seguintes propriedades:

Nome            | Tipo    | Necessária | Observações
--------------- | ------- | -------- | -----
@id             | cadeia de caracteres  | sim      | A URL para buscar a página de catálogo
commitId        | cadeia de caracteres  | sim      | Uma ID exclusiva associada com a confirmação mais recente nesta página
commitTimeStamp | cadeia de caracteres  | sim      | Um carimbo de hora da confirmação mais recente nesta página
count           | inteiro | sim      | O número de itens na página de catálogo

Em contraste com o [recurso de metadados do pacote](registration-base-url-resource.md) que, em alguns casos, inlines deixa em um índice, folhas de catálogo nunca são embutidas em um índice e sempre devem ser buscadas por meio da página `@id` URL.

### <a name="sample-request"></a>Exemplo de solicitação

    GET https://api.nuget.org/v3/catalog0/index.json

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>Página de catálogo

A página de catálogo é uma coleção de itens de catálogo. É um documento buscado usando um do `@id` valores encontrados no índice do catálogo. A URL para uma página de catálogo não se destina a ser previsíveis e deve ser descoberta usando apenas o índice do catálogo.

Novos itens de catálogo são adicionados à página no índice de catálogo apenas com o maior carimbo de hora de confirmação ou para uma nova página. Depois que uma página com um carimbo de hora de confirmação maior é adicionada ao catálogo, as páginas anteriores nunca são adicionadas ou alteradas.

O documento de página de catálogo é um objeto JSON com as seguintes propriedades:

Nome            | Tipo             | Necessária | Observações
--------------- | ---------------- | -------- | -----
commitId        | cadeia de caracteres           | sim      | Uma ID exclusiva associada com a confirmação mais recente nesta página
commitTimeStamp | cadeia de caracteres           | sim      | Um carimbo de hora da confirmação mais recente nesta página
count           | inteiro          | sim      | O número de itens na página
items           | matriz de objetos | sim      | Os itens de catálogo nesta página
parent          | cadeia de caracteres           | sim      | Uma URL para o índice do catálogo

Cada elemento no `items` matriz é um objeto com alguns detalhes mínimos sobre o item de catálogo. Esses objetos de item não contêm todos os dados do item do catálogo. A ordem dos itens na página de `items` matriz não está definida. Itens podem ser solicitados pelo cliente na memória usando seus `commitTimeStamp` propriedade.

O número de itens de catálogo em uma página é definido pela implementação do servidor. Para nuget.org, há no máximo 550 itens em cada página, embora o número real pode ser menor para algumas páginas, dependendo do tamanho do próximo lote de confirmação no ponto no tempo.

Conforme novos itens são introduzidos, o `count` é objetos de item de catálogo novo e incrementado aparecem no `items` matriz.

Como os itens são adicionados à página, o `commitId` as alterações e o `commitTimeStamp` aumenta. Essas duas propriedades são, essencialmente, um resumo de todos os `commitId` e `commitTimeStamp` os valores no `items` matriz.

### <a name="catalog-item-object-in-a-page"></a>Objeto de item em uma página do catálogo

Os objetos de item de catálogo encontram na página de catálogo `items` propriedade têm as seguintes propriedades:

Nome            | Tipo    | Necessária | Observações
--------------- | ------- | -------- | -----
@id             | cadeia de caracteres  | sim      | A URL para buscar o item de catálogo
@type           | cadeia de caracteres  | sim      | O tipo de item de catálogo
commitId        | cadeia de caracteres  | sim      | A ID de confirmação associada a este item de catálogo
commitTimeStamp | cadeia de caracteres  | sim      | O carimbo de hora de confirmação deste item de catálogo
nuget:id        | cadeia de caracteres  | sim      | A ID do pacote que essa folha está relacionada ao
nuget:version   | cadeia de caracteres  | sim      | A versão do pacote que essa folha está relacionada ao

O `@type` valor deve ser um dos dois valores a seguir:

1. `nuget:PackageDetails`: isso corresponde à `PackageDetails` tipo no documento de folha de catálogo.
1. `nuget:PackageDelete`: isso corresponde à `PackageDelete` tipo no documento de folha de catálogo.

Para obter mais detalhes sobre significa que cada tipo, consulte o [tipo os itens correspondentes](#item-types) abaixo.

### <a name="sample-request"></a>Exemplo de solicitação

    GET https://api.nuget.org/v3/catalog0/page2926.json

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>Folha de catálogo

A folha de catálogo contém metadados sobre um ID de pacote específico e uma versão em algum momento no tempo. É um documento buscado usando o `@id` valor encontrado em uma página de catálogo. A URL para uma folha de catálogo não se destina a ser previsíveis e deve ser descoberta usando apenas uma página de catálogo.

O documento de folha de catálogo é um objeto JSON com as seguintes propriedades:

Nome                    | Tipo                       | Necessária | Observações
----------------------- | -------------------------- | -------- | -----
@type                   | cadeia de caracteres ou matriz de cadeias de caracteres | sim      | Os tipos de item de catálogo
catalog:commitId        | cadeia de caracteres                     | sim      | Uma ID de confirmação associada a este item de catálogo
catalog:commitTimeStamp | cadeia de caracteres                     | sim      | O carimbo de hora de confirmação deste item de catálogo
id                      | cadeia de caracteres                     | sim      | A ID do pacote de item de catálogo
Publicado               | cadeia de caracteres                     | sim      | A data de publicação do item de catálogo de pacote
version                 | cadeia de caracteres                     | sim      | A versão do pacote de item de catálogo

### <a name="item-types"></a>Tipos de item

O `@type` propriedade é uma cadeia de caracteres ou uma matriz de cadeias de caracteres. Para sua conveniência, se o `@type` valor é uma cadeia de caracteres, ele deve ser tratado como qualquer matriz de tamanho. Nem todos os valores possíveis para `@type` são documentados. No entanto, cada item de catálogo tem exatamente um dos dois valores de tipo de cadeia de caracteres seguintes:

1. `PackageDetails`: representa um instantâneo dos metadados do pacote
1. `PackageDelete`: representa um pacote que foi excluído

### <a name="package-details-catalog-items"></a>Itens de catálogo de detalhes do pacote

Itens com o tipo de catálogo `PackageDetails` contêm um instantâneo dos metadados de pacote para um pacote específico (combinação de ID e versão). Um item de catálogo de detalhes do pacote é produzido quando uma origem de pacote encontra qualquer um dos seguintes cenários:

1. É um pacote **enviados por push**.
1. É um pacote **listados**.
1. É um pacote **não listados**.
1. É um pacote **fluxo redirecionado**.

Refluxo de um pacote é um gesto administrativo que gera, essencialmente, um envio FALSO de um pacote existente sem alterações para o pacote propriamente dito. Em nuget.org, refluxo de um é usado depois de corrigir um bug em um dos trabalhos em segundo plano que consomem o catálogo.

Os clientes consumindo os itens de catálogo não devem tentar determinar qual desses cenários produzido o item de catálogo. Em vez disso, o cliente deve simplesmente atualizar qualquer exibição mantida ou o índice com os metadados contidos no item de catálogo. Além disso, os itens de catálogo duplicados ou redundantes devem ser manipuladas com elegância (forma idempotencial).

Itens de catálogo de detalhes do pacote têm as propriedades a seguir, além daqueles [incluídos em todas as folhas de catálogo](#catalog-leaf).

Nome                    | Tipo                       | Necessária | Observações
----------------------- | -------------------------- | -------- | -----
authors                 | cadeia de caracteres                     | no       |
Criado                 | cadeia de caracteres                     | no       | Um carimbo de hora de quando o pacote foi criado. Propriedade de fallback: `published`.
dependencyGroups        | matriz de objetos           | no       | As dependências do pacote, agrupados por estrutura de destino ([mesmo formato que o recurso de metadados do pacote](registration-base-url-resource.md#package-dependency-group))
Substituição             | objeto                     | no       | A substituição associada ao pacote ([mesmo formato que o recurso de metadados do pacote](registration-base-url-resource.md#package-deprecation))
descrição             | cadeia de caracteres                     | no       |
iconUrl                 | cadeia de caracteres                     | no       |
isPrerelease            | boolean                    | no       | Se é ou não a versão do pacote pré-lançamento. Podem ser detectados de `version`.
linguagem                | cadeia de caracteres                     | no       |
licenseUrl              | cadeia de caracteres                     | no       |
listados                  | boolean                    | no       | Se o pacote está listado
minClientVersion        | cadeia de caracteres                     | no       |
packageHash             | cadeia de caracteres                     | sim      | O hash do pacote, codificação usando [padrão na base 64](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | cadeia de caracteres                     | sim      |
packageSize             | inteiro                    | sim      | O tamanho da. nupkg de pacote em bytes
projectUrl              | cadeia de caracteres                     | no       |
releaseNotes            | cadeia de caracteres                     | no       |
requireLicenseAgreement | boolean                    | no       | Suponha que `false` se excluído
resumo                 | cadeia de caracteres                     | no       |
marcações                    | matriz de cadeias de caracteres           | no       |
título                   | cadeia de caracteres                     | no       |
verbatimVersion         | cadeia de caracteres                     | no       | A cadeia de caracteres de versão como ele originalmente encontra o. NuSpec

O pacote `version` propriedade é a cadeia de caracteres de versão completa após a normalização. Isso significa que os dados de criação de SemVer 2.0.0 podem ser incluídos aqui.

O `created` carimbo de hora é quando o pacote foi recebido pela origem do pacote, que normalmente é um breve período antes do carimbo de hora de confirmação do item do catálogo.

O `packageHashAlgorithm` é uma cadeia de caracteres definida pela implementação do servidor, que representa o algoritmo de hash usado para produzir o `packageHash`. NuGet.org sempre usado o `packageHashAlgorithm` valor de `SHA512`.

O `published` carimbo de hora é a hora quando o pacote pela última vez foi listado.

> [!Note]
> Em nuget.org, o `published` valor é definido como o ano de 1900 quando o pacote for removido da lista.

#### <a name="sample-request"></a>Exemplo de solicitação

GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

#### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>Itens de catálogo de exclusão do pacote

Itens com o tipo de catálogo `PackageDelete` contêm um conjunto mínimo de informações que indicam a clientes de catálogo que um pacote foi excluído da origem do pacote e não está mais disponível para qualquer operação de pacote (por exemplo, restauração).

> [!NOTE]
> É possível que um pacote a ser excluído e republicadas posteriormente usando a mesma ID de pacote e a versão. Em nuget.org, isso é um caso muito raro, pois ela divide a suposição oficial do cliente que uma ID do pacote e versão implicam um conteúdo de pacote específico. Para obter mais informações sobre a exclusão do pacote em nuget.org, consulte [nossa política](../nuget-org/policies/deleting-packages.md).

Itens de catálogo de exclusão do pacote não têm nenhuma propriedade adicional, além daqueles [incluídos em todas as folhas de catálogo](#catalog-leaf).

O `version` propriedade é a cadeia de caracteres de versão original encontrada no. de NuSpec do pacote.

O `published` propriedade é a hora quando o pacote foi excluído, que normalmente é como pouco tempo antes do carimbo de hora de confirmação do item do catálogo.

#### <a name="sample-request"></a>Exemplo de solicitação

GET https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json

#### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Cursor

### <a name="overview"></a>Visão geral

Esta seção descreve um conceito de cliente que, embora não necessariamente é exigido pelo protocolo, deve ser parte de qualquer implementação de cliente do catálogo prático.

Como o catálogo é uma estrutura de dados somente de acréscimo indexada por tempo, o cliente deve armazenar uma **cursor** localmente, que representa até que ponto no tempo que o cliente processou itens de catálogo. Observe que esse valor de cursor deve nunca ser gerado usando o relógio do computador do cliente. Em vez disso, o valor deve vir de um objeto de catálogo `commitTimestamp` valor.

Toda vez que o cliente deseja processar novos eventos na origem do pacote, ele precisa apenas consulta o catálogo de todos os itens de catálogo com um carimbo de hora de confirmação maior que o seu cursor armazenado. Depois que o cliente processa com êxito todos os novos itens de catálogo, ela registra o carimbo de hora de confirmação mais recente de itens de catálogo processado apenas como seu novo valor de cursor.

Usando essa abordagem, o cliente pode ser-se de nunca perder quaisquer eventos de pacote que ocorreram na origem do pacote.
Além disso, o cliente nunca deve reprocessar eventos antigos antes do carimbo de hora de confirmação gravada do cursor.

Esse conceito poderoso de cursores é usado para muitos dos trabalhos de plano de fundo do nuget.org e é usado para manter a própria API V3 atualizados. 

### <a name="initial-value"></a>Valor inicial

Quando o cliente do catálogo está sendo iniciado pela primeira vez (e, portanto, não tem nenhum valor de cursor), ele deve usar um valor cursor padrão. Do NET `System.DateTimeOffset.MinValue` ou uma noção tal análoga de carimbo de hora mínimo representável.

### <a name="iterating-over-catalog-items"></a>Iterar em itens de catálogo

Para consultar o próximo conjunto de itens de catálogo para processar, o cliente deve:

1. Busca o valor de cursor registrados de um armazenamento local.
1. Baixar e desserializar o índice do catálogo.
1. Localizar todas as páginas com um carimbo de hora de confirmação do catálogo *maior que* o cursor.
1. Declare uma lista vazia de itens de catálogo para processar.
1. Para cada página de catálogo correspondida na etapa 3:
   1. Baixe e desserializado a página de catálogo.
   1. Localizar todos os itens com um carimbo de hora de confirmação do catálogo *maior que* o cursor.
   1. Adicione todos os itens de catálogo correspondente à lista declarada na etapa 4.
1. Classificar a lista de itens de catálogo por carimbo de hora de confirmação.
1. Processe cada item de catálogo na sequência:
   1. Baixar e desserializar o item de catálogo.
   1. Responder de forma adequada para o tipo do item de catálogo.
   1. Processe o documento de item de catálogo de forma específicas do cliente.
1. Registre o carimbo de hora de confirmação do último item de catálogo como o novo valor de cursor.

Com esse algoritmo básico, a implementação do cliente pode criar uma exibição completa de todos os pacotes disponíveis na origem do pacote. O cliente só precisa executar esse algoritmo periodicamente para estar ciente de que as alterações mais recentes para a origem do pacote.

> [!Note]
> Este é o algoritmo que nuget.org usa para manter o [metadados de pacote](registration-base-url-resource.md), [conteúdo do pacote](package-base-address-resource.md), [pesquisa](search-query-service-resource.md) e [AutoCompletar](search-autocomplete-service-resource.md) recursos atualizados.

### <a name="dependent-cursors"></a>Cursores dependentes

Suponha que há dois clientes de catálogo que têm uma dependência inerente onde saída de um cliente depende de saída do cliente para outro. 

#### <a name="example"></a>Exemplo

Por exemplo, em nuget.org um pacote publicado recentemente não deve aparecer no recurso de pesquisa para que ele apareça no recurso de metadados do pacote. Isso ocorre porque a operação de "restauração" realizada pelo cliente do NuGet oficial usa o recurso de metadados do pacote. Se um cliente descobrir um pacote usando o serviço de pesquisa, eles poderão restaurar com êxito o pacote usando o recurso de metadados do pacote. Em outras palavras, o recurso de pesquisa depende do recurso de metadados de pacote. Cada recurso tem um trabalho de plano de fundo do cliente de catálogo atualizando esse recurso. Cada cliente tem sua própria cursor.

Já que ambos os recursos são criados fora do catálogo, o cursor do cliente catálogo que atualiza o recurso de pesquisa *não deve ultrapassar* o cursor do cliente do catálogo de metadados do pacote.

#### <a name="algorithm"></a>Algoritmo

Para implementar essa restrição, basta modificar o algoritmo acima para ser:

1. Busca o valor de cursor registrados de um armazenamento local.
1. Baixar e desserializar o índice do catálogo.
1. Localizar todas as páginas com um carimbo de hora de confirmação do catálogo *maior que* cursor **menor ou igual ao cursor da dependência.**
1. Declare uma lista vazia de itens de catálogo para processar.
1. Para cada página de catálogo correspondida na etapa 3:
   1. Baixe e desserializado a página de catálogo.
   1. Localizar todos os itens com um carimbo de hora de confirmação do catálogo *maior que* cursor **menor ou igual ao cursor da dependência.**
   1. Adicione todos os itens de catálogo correspondente à lista declarada na etapa 4.
1. Classificar a lista de itens de catálogo por carimbo de hora de confirmação.
1. Processe cada item de catálogo na sequência:
   1. Baixar e desserializar o item de catálogo.
   1. Responder de forma adequada para o tipo do item de catálogo.
   1. Processe o documento de item de catálogo de forma específicas do cliente.
1. Registre o carimbo de hora de confirmação do último item de catálogo como o novo valor de cursor.

Usando esse algoritmo modificado, você pode criar um sistema de clientes dependentes catálogo produzir todos os seus próprios índices específicos, artefatos, etc.
