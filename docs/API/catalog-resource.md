---
title: "Catálogo, a API do NuGet V3 | Microsoft Docs"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/30/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "O catálogo é um índice de todos os pacotes criados e excluídos em nuget.org."
keywords: "Catálogo de API do NuGet V3, log de transações nuget.org, replicar NuGet.org, clone NuGet.org, registro somente de acréscimo de NuGet.org"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: d1a24be68a60085a40361c374ffb34dc221f09c4
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
---
# <a name="catalog"></a>Catálogo

O **catálogo** é um recurso que registra todas as operações de pacote em uma origem do pacote, como as criações e exclusões. O recurso de catálogo tem o `Catalog` digite o [índice de serviço](service-index.md).

> [!Note]
> Como o catálogo não é usado pelo cliente do NuGet oficial, nem todas as fontes de pacote implementam o catálogo.

> [!Note]
> Atualmente, o catálogo nuget.org não está disponível na China. Para obter mais detalhes, consulte [NuGet/NuGetGallery #4949](https://github.com/NuGet/NuGetGallery/issues/4949).

## <a name="versioning"></a>Controle de versão

O seguinte `@type` valor é usado:

Valor @type   | Observações
------------- | -----
Catalog/3.0.0 | A versão inicial

## <a name="base-url"></a>URL Base

A URL de ponto de entrada para as seguintes APIs é o valor da `@id` propriedade associada com o recurso mencionados acima `@type` valores. Este tópico usa a URL de espaço reservado `{@id}`.

## <a name="http-methods"></a>Métodos HTTP

Todas as URLs encontradas no suporte a recurso de catálogo apenas os métodos HTTP `GET` e `HEAD`.

## <a name="catalog-index"></a>Índice do catálogo

O índice do catálogo é um documento em um local conhecido que tem uma lista de itens de catálogo, ordenados cronologically. É o ponto de entrada do recurso de catálogo.

O índice é composto de páginas de catálogo. Cada página de catálogo contém itens de catálogo. Cada item de catálogo representa um evento sobre um único pacote em um ponto no tempo. Um item de catálogo pode representar um pacote que foi criado, não listados, listado novamente ou excluído da origem do pacote. Processando os itens de catálogo em ordem cronológica, o cliente pode criar uma exibição atualizada de cada pacote que existe na origem do pacote V3.

Em resumo, blobs de catálogo têm a seguinte estrutura hierárquica:

- **Índice**: o ponto de entrada para o catálogo.
- **Página**: um agrupamento de itens de catálogo.
- **Folha**: um documento que representa um item de catálogo, que é um instantâneo do estado de um único pacote.

Cada objeto de catálogo tem uma propriedade chamada o `commitTimeStamp` que representa quando o item foi adicionado ao catálogo. Itens de catálogo são adicionados a uma página de catálogo em lotes chamado confirmações. Todos os itens de catálogo no mesmo confirmação têm o mesmo carimbo de hora de confirmação (`commitTimeStamp`) e a ID de confirmação (`commitId`). Itens de catálogo colocados no mesmo confirmação representam eventos que ocorreram em torno do mesmo ponto no tempo em que a origem do pacote. Não há nenhuma ordem dentro de uma confirmação de catálogo.

Como cada versão e a ID do pacote é exclusivo, nunca será mais de um item de catálogo em uma confirmação. Isso garante que os itens de catálogo para um único pacote podem sempre ser inequivocamente ordenados em relação ao carimbo de hora de confirmação.

Há nunca ser mais de uma confirmação para o catálogo por `commitTimeStamp`. Em outras palavras, o `commitId` são redundantes com o `commitTimeStamp`.

Em comparação com o [recursos de metadados do pacote](registration-base-url-resource.md), que é indexado por ID do pacote, o catálogo é indexado (e podem ser consultados) somente por vez.

Itens de catálogo sempre sejam adicionados ao catálogo em uma ordem cronológica, aumenta de forma monotônica. Isso significa que se uma confirmação de catálogo é adicionada em tempo de X, em seguida, nenhuma confirmação de catálogo será adicionada com um tempo menor ou igual a X.

A seguinte solicitação de busca o índice do catálogo.

    GET {@id}

O índice do catálogo é um documento JSON que contém um objeto com as seguintes propriedades:

Nome            | Tipo             | Necessária | Observações
--------------- | ---------------- | -------- | -----
commitId        | cadeia de caracteres           | sim      | Uma ID exclusiva associada a mais recente confirmação
commitTimeStamp | cadeia de caracteres           | sim      | Um carimbo de hora da confirmação mais recente
count           | inteiro          | sim      | O número de páginas no índice
Itens           | Matriz de objetos | sim      | Uma matriz de objetos, cada objeto que representa uma página

Cada elemento de `items` matriz é um objeto com alguns detalhes mínimos sobre cada página. Esses objetos de página não contêm as folhas de catálogo (itens). A ordem dos elementos nesta matriz não está definida. Páginas podem ser solicitadas pelo cliente na memória usando seus `commitTimeStamp` propriedade.

Conforme novas páginas são apresentadas, o `count` será incrementada e novos objetos aparecerão na `items` matriz.

Como os itens são adicionados ao catálogo, o índice `commitId` será alterado e o `commitTimeStamp` aumentará. Essas duas propriedades são essencialmente um resumo sobre todas as página `commitId` e `commitTimeStamp` valores no `items` matriz.

### <a name="catalog-page-object-in-the-index"></a>Objeto de página no índice do catálogo

Os objetos da página de catálogo encontrada no índice de catálogo `items` propriedade têm as seguintes propriedades:

Nome            | Tipo    | Necessária | Observações
--------------- | ------- | -------- | -----
@id             | cadeia de caracteres  | sim      | A URL para a página de busca de catálogo
commitId        | cadeia de caracteres  | sim      | Uma ID exclusiva associada a mais recente confirmação nesta página
commitTimeStamp | cadeia de caracteres  | sim      | Um carimbo de hora da confirmação mais recente nesta página
count           | inteiro | sim      | O número de itens na página de catálogo

Em comparação com o [recursos de metadados do pacote](registration-base-url-resource.md) que em alguns casos, linhas internas deixa no índice, catálogo deixa nunca é embutida no índice e sempre deve ser obtida por meio da página `@id` URL.

### <a name="sample-request"></a>Solicitação de amostra

    GET https://api.nuget.org/v3/catalog0/index.json

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>Página Catálogo

A página de catálogo é uma coleção de itens de catálogo. É um documento buscado usando um do `@id` valores encontrados no índice do catálogo. A URL para uma página de catálogo não se destina a ser previsíveis e deve ser detectada usando apenas o índice do catálogo.

Novos itens de catálogo são adicionados à página no índice de catálogo apenas com o carimbo de hora de confirmação mais alto ou para uma nova página. Depois que uma página com um carimbo de hora de confirmação maior é adicionada ao catálogo, páginas mais antigas nunca são adicionadas ou alteradas.

O documento de página de catálogo é um objeto JSON com as seguintes propriedades:

Nome            | Tipo             | Necessária | Observações
--------------- | ---------------- | -------- | -----
commitId        | cadeia de caracteres           | sim      | Uma ID exclusiva associada a mais recente confirmação nesta página
commitTimeStamp | cadeia de caracteres           | sim      | Um carimbo de hora da confirmação mais recente nesta página
count           | inteiro          | sim      | O número de itens na página
Itens           | Matriz de objetos | sim      | Os itens de catálogo nesta página
pai          | cadeia de caracteres           | sim      | Uma URL para o índice do catálogo

Cada elemento de `items` matriz é um objeto com alguns detalhes mínimo sobre o item de catálogo. Esses objetos de item não contêm todos os dados do item de catálogo. A ordem dos itens na página de `items` matriz não está definida. Itens podem ser solicitados pelo cliente na memória usando seus `commitTimeStamp` propriedade.

O número de itens de catálogo em uma página é definido pela implementação do servidor. Para nuget.org, há no máximo 550 itens em cada página, embora o número real pode ser menor para dependong algumas páginas no tamanho do próximo lote de confirmação no ponto no tempo.

Conforme novos itens são apresentados, o `count` é objetos de item de catálogo novo e incrementado aparecem na `items` matriz.

Quando itens são adicionados à página, o `commitId` alterações e o `commitTimeStamp` aumenta. Essas duas propriedades são essencialmente um resumo sobre todas `commitId` e `commitTimeStamp` valores no `items` matriz.

### <a name="catalog-item-object-in-a-page"></a>Objeto de item em uma página do catálogo

Os objetos de item de catálogo encontram na página de catálogo `items` propriedade têm as seguintes propriedades:

Nome            | Tipo    | Necessária | Observações
--------------- | ------- | -------- | -----
@id             | cadeia de caracteres  | sim      | A URL para buscar o item de catálogo
@type           | cadeia de caracteres  | sim      | O tipo do item de catálogo
commitId        | cadeia de caracteres  | sim      | A ID de confirmação associada a este item de catálogo
commitTimeStamp | cadeia de caracteres  | sim      | O carimbo de hora de confirmação desse item de catálogo
NuGet:ID        | cadeia de caracteres  | sim      | A ID do pacote que esta folha está relacionada ao
NuGet:Version   | cadeia de caracteres  | sim      | A versão do pacote que esta folha está relacionada ao

O `@type` valor deve ser um dos seguintes valores:

1. `nuget:PackageDetails`: isso corresponde à `PackageDetails` tipo do documento de folha de catálogo.
1. `nuget:PackageDelete`: isso corresponde do `PackageDelete` tipo do documento de folha de catálogo.

Para obter mais detalhes sobre significa que cada tipo, consulte o [correspondente itens tipo](#item-types) abaixo.

### <a name="sample-request"></a>Solicitação de amostra

    GET https://api.nuget.org/v3/catalog0/page2926.json

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>Folha de catálogo

A folha de catálogo contém metadados sobre um ID de pacote específico e a versão em algum ponto no tempo. É um documento obtido usando o `@id` valor encontrado em uma página de catálogo. A URL para uma folha de catálogo não se destina a ser predictedable e deve ser detectada usando apenas uma página de catálogo.

O documento de folha de catálogo é um objeto JSON com as seguintes propriedades:

Nome                    | Tipo                       | Necessária | Observações
----------------------- | -------------------------- | -------- | -----
@type                   | cadeia de caracteres ou matriz de cadeias de caracteres | sim      | Os tipos de item de catálogo
catalog:commitId        | cadeia de caracteres                     | sim      | Uma ID de confirmação associada a este item de catálogo
catalog:commitTimeStamp | cadeia de caracteres                     | sim      | O carimbo de hora de confirmação desse item de catálogo
id                      | cadeia de caracteres                     | sim      | A ID do pacote do item de catálogo
Publicado               | cadeia de caracteres                     | sim      | A data de publicação do item de catálogo de pacote
version                 | cadeia de caracteres                     | sim      | A versão do pacote do item de catálogo

### <a name="item-types"></a>Tipos de item

O `@type` propriedade é uma cadeia de caracteres ou uma matriz de cadeias de caracteres. Para sua conveniência, se o `@type` valor é uma cadeia de caracteres, ele deve ser tratado como qualquer matriz de tamanho. Nem todos os valores possíveis para `@type` são documentadas. No entanto, cada item de catálogo tem exatamente um dos dois valores de tipo de cadeia de caracteres seguintes:

1. `PackageDetails`: representa um instantâneo dos metadados do pacote
1. `PackageDelete`: representa um pacote que foi excluído

### <a name="package-details-catalog-items"></a>Itens de catálogo de detalhes do pacote

Itens com o tipo de catálogo `PackageDetails` contêm um instantâneo dos metadados de pacote para um pacote específico (combinação de ID e a versão). Um item de catálogo de detalhes do pacote é gerado quando uma origem de pacote encontra qualquer um dos seguintes cenários:

1. Um pacote é **enviada por push**.
1. Um pacote é **listados**.
1. Um pacote é **não listados**.
1. Um pacote é **fluxo redirecionado**.

Refluxo um pacote é um gesto administrativo que essencialmente gera um falso envio de um pacote existente sem alterações para o próprio pacote. Em nuget.org, um refluxo é usado depois de corrigir um bug em um dos trabalhos em segundo plano que consomem o catálogo.

Os clientes que consome os itens de catálogo não devem tentar determinar qual desses cenários produziu o item de catálogo. Em vez disso, o cliente deve simplesmente atualizar qualquer índice ou exibição mantida com os metadados contidos no item de catálogo. Além disso, os itens de catálogo duplicada ou redundante devem ser tratados normalmente (forma idempotencial).

Itens de catálogo de detalhes do pacote com as seguintes propriedades além daqueles [incluído em todas as folhas de catálogo](#catalog-leaf).

Nome                    | Tipo                       | Necessária | Observações
----------------------- | -------------------------- | -------- | -----
authors                 | cadeia de caracteres                     | no       |
Criado                 | cadeia de caracteres                     | sim      | Um carimbo de hora de quando o pacote foi criado
dependencyGroups        | Matriz de objetos           | no       | Mesmo formato que o [recursos de metadados do pacote](registration-base-url-resource.md#package-dependency-group)
descrição             | cadeia de caracteres                     | no       |
iconUrl                 | cadeia de caracteres                     | no       |
isPrerelease            | boolean                    | sim      | Se a versão do pacote é pré-lançamento
linguagem                | cadeia de caracteres                     | no       |
licenseUrl              | cadeia de caracteres                     | no       |
listados                  | boolean                    | no       | Se o pacote está listado
minClientVersion        | cadeia de caracteres                     | no       |
packageHash             | cadeia de caracteres                     | sim      | O hash do pacote, codificação usando [padrão na base 64](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | cadeia de caracteres                     | sim      |
packageSize             | inteiro                    | sim      | O tamanho de nupkg do pacote em bytes
projectUrl              | cadeia de caracteres                     | no       |
releaseNotes            | cadeia de caracteres                     | no       |
requireLicenseAgreement | boolean                    | no       | Suponha que `false` se excluído
resumo                 | cadeia de caracteres                     | no       |
marcações                    | Matriz de cadeias de caracteres           | no       |
título                   | cadeia de caracteres                     | no       |
verbatimVersion         | cadeia de caracteres                     | no       | A cadeia de caracteres de versão como ele é originalmente encontrada no. o NuSpec

O pacote `version` propriedade é a cadeia de caracteres de versão completo, normalizado. Isso significa que os dados de criação de SemVer 2.0.0 podem ser incluídos aqui.

O `created` carimbo de hora é quando o pacote foi recebido pela origem do pacote, que é normalmente um curto período de tempo antes de carimbo de hora de confirmação do item de catálogo.

O `packageHashAlgorithm` é uma cadeia de caracteres definidos por represeting de implementação do servidor, o algoritmo de hash usado para produzir o `packageHash`. NuGet.org usado sempre o `packageHashAlgorithm` valor `SHA512`.

O `published` carimbo de hora é o tempo quando o pacote última foi listado.

> [!Note]
> Em nuget.org, o `published` valor é definido para ano 1900 quando o pacote for removido da lista.

#### <a name="sample-request"></a>Solicitação de amostra

GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

#### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>Itens de catálogo de exclusão do pacote

Itens com o tipo de catálogo `PackageDelete` contêm um conjunto mínimo de informações indicando a clientes de catálogo que um pacote foi excluído da origem do pacote e não está mais disponível para qualquer operação de pacote (por exemplo, a restauração).

> [!Note]
> É possível que um pacote a ser excluído e republicadas posteriormente usando a mesma ID de pacote e versão. Em nuget.org, isso é um caso raro como quebras suposição oficial do cliente que uma ID de pacote e versão implicam o conteúdo de um pacote específico. Para obter mais informações sobre a exclusão do pacote nuget.org, consulte [nossa política de](../policies/deleting-packages.md).

Itens de catálogo de exclusão do pacote não têm nenhuma propriedade adicional além daqueles [incluído em todas as folhas de catálogo](#catalog-leaf).

O `version` propriedade é a cadeia de caracteres de versão original encontrada no. de NuSpec pacote.

O `published` propriedade é a hora em que o pacote foi excluído, que normalmente é como curto período de tempo antes de carimbo de hora de confirmação do item de catálogo.

#### <a name="sample-request"></a>Solicitação de amostra

GET https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json

#### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Cursor

### <a name="overview"></a>Visão geral

Esta seção descreve um conceito de cliente que, embora não necessariamente é exigido pelo protocolo, deve ser parte de qualquer implementação de cliente de catálogo prático.

Como o catálogo é uma estrutura de dados somente de acréscimo indexada por hora, o cliente deve armazenar um **cursor** localmente, o que representa até que ponto no tempo que o cliente tiver processado itens de catálogo. Observe que esse valor de cursor deve nunca ser gerado usando o relógio do computador do cliente. Em vez disso, o valor deve vir de um objeto de catálogo `commitTimestamp` valor.

Toda vez que o cliente deseja processar novos eventos de origem do pacote, ele precisa consulta o catálogo para todos os itens de catálogo com um carimbo de hora de confirmação maior que o cursor armazenado. Depois que o cliente processa com êxito todos os novos itens de catálogo, ele registra o carimbo de hora mais recente confirmação de itens de catálogo processados apenas como o novo valor de cursor.

Usando essa abordagem, o cliente poderá ter certeza nunca perder quaisquer eventos de pacote que ocorreram na origem do pacote.
Além disso, o cliente nunca precisa reprocessar eventos antigos antes do carimbo de hora de confirmação gravada do cursor.

Esse conceito avançado de cursores é usado para muitos dos trabalhos de plano de fundo nuget.org e é usado para manter a própria API V3 atualizados. 

### <a name="initial-value"></a>Valor inicial

Quando o cliente do catálogo está sendo iniciado pela primeira vez (e, portanto, não tem nenhum valor de cursor), ele deve usar um valor cursor padrão. Do NET `System.DateTimeOffset.MinValue` ou uma noção tal análoga do mínimo timestamp representável.

### <a name="iterating-over-catalog-items"></a>Iterando sobre itens de catálogo

Para consultar o próximo conjunto de itens de catálogo para processar, o cliente deve:

1. Busca o valor de cursor gravada de um repositório local.
1. Baixe e desserializar o índice do catálogo.
1. Localizar todas as páginas com um carimbo de hora de confirmação de catálogo *maior* o cursor.
1. Declare uma lista vazia de itens de catálogo para processar.
1. Para cada página de catálogo correspondida na etapa 3:
   1. Baixe e desserializado a página de catálogo.
   1. Localizar todos os itens com um carimbo de hora de confirmação de catálogo *maior* o cursor.
   1. Adicione todos os itens de catálogo correspondente à lista declarada na etapa 4.
1. Classificar a lista de itens do catálogo por carimbo de hora de confirmação.
1. Processe cada item de catálogo em sequência:
   1. Baixe e desserializar o item de catálogo.
   1. Reagir de forma adequada para o tipo do item de catálogo.
   1. Processe o documento de item de catálogo de maneira específicas do cliente.
1. Registre o carimbo de hora de confirmação do último item de catálogo como o novo valor de cursor.

Com esse algoritmo básico, a implementação do cliente pode criar uma exibição completa de todos os pacotes disponíveis na origem do pacote. O cliente só precisa executar este algoritmo periodicamente para estar ciente de que as alterações mais recentes para a origem do pacote.

> [!Note]
> Esse é o algoritmo que nuget.org usa para manter o [metadados do pacote](registration-base-url-resource.md), [conteúdo do pacote](package-base-address-resource.md), [pesquisa](search-query-service-resource.md) e [AutoCompletar](search-autocomplete-service-resource.md) recursos atualizados.

### <a name="dependent-cursors"></a>Cursores dependentes

Suponha que há dois clientes de catálogo que têm uma dependência inherant onde saída de um cliente depende de saída do cliente para outro. 

#### <a name="example"></a>Exemplo

Por exemplo, em nuget.org um pacote publicado recentemente não deve aparecer no recurso de pesquisa para que ele apareça no recurso de metadados de pacote. Isso ocorre porque a operação de "restore" executada pelo cliente do NuGet oficial usa o recurso de metadados do pacote. Se um cliente detecta um pacote usando o serviço de pesquisa, eles devem ser capazes de restaurar com êxito o pacote usando o recurso de metadados do pacote. Em outras palavras, o recurso de pesquisa depende do recurso de metadados do pacote. Cada recurso tem um trabalho de plano de fundo do cliente do catálogo atualizar esse recurso. Cada cliente tem seu próprio cursor.

Já que ambos os recursos são criados fora do catálogo, o cursor do cliente de catálogo que atualiza o recurso de pesquisa *não deve ultrapassar* o cursor do cliente do catálogo de metadados do pacote.

#### <a name="algorithm"></a>Algoritmo

Para implementar essa restrição, simples modificar o algoritmo acima para ser:

1. Busca o valor de cursor gravada de um repositório local.
1. Baixe e desserializar o índice do catálogo.
1. Localizar todas as páginas com um carimbo de hora de confirmação de catálogo *maior* o cursor **menor ou igual ao cursor da dependência.**
1. Declare uma lista vazia de itens de catálogo para processar.
1. Para cada página de catálogo correspondida na etapa 3:
   1. Baixe e desserializado a página de catálogo.
   1. Localizar todos os itens com um carimbo de hora de confirmação de catálogo *maior* o cursor **menor ou igual ao cursor da dependência.**
   1. Adicione todos os itens de catálogo correspondente à lista declarada na etapa 4.
1. Classificar a lista de itens do catálogo por carimbo de hora de confirmação.
1. Processe cada item de catálogo em sequência:
   1. Baixe e desserializar o item de catálogo.
   1. Reagir de forma adequada para o tipo do item de catálogo.
   1. Processe o documento de item de catálogo de maneira específicas do cliente.
1. Registre o carimbo de hora de confirmação do último item de catálogo como o novo valor de cursor.

Usando esse algoritmo modificado, você pode criar um sistema de clientes dependentes catálogo gera todos os seus próprios índices específicos, artefatos, etc.
