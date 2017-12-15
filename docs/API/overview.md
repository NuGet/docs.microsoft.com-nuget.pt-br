---
title: "Visão geral, o NuGet API | Microsoft Docs"
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
ms.assetid: 8c81f1ac-18c7-44d1-b2e3-584fe85dee6f
description: "A API do NuGet é um conjunto de pontos de extremidade HTTP que podem ser usados para baixar os pacotes, buscar metadados, publicar novos pacotes, etc."
keywords: "NuGet V3 API, API do NuGet V2, NuGet JSON, API de registro do NuGet, contêiner simples de API do NuGet, NuGet nupkg API, NuGet metadados API, API de pesquisa NuGet, NuGet push API, NuGe publicar API, NuGet excluir API, NuGet remover da lista de API, o protocolo do NuGet"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: a9515d90ad66d8840f575bba542f0cf887c41718
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-api"></a>API do NuGet

A API do NuGet é um conjunto de pontos de extremidade HTTP que pode ser usado para baixar os pacotes, buscar metadados, publicar novos pacotes e executar a maioria das outras operações disponíveis aos clientes do NuGet oficial.

Essa API é usada pelo cliente do NuGet no Visual Studio, nuget.exe e a CLI do .NET para executar operações de NuGet como [ `dotnet restore` ](https://docs.microsoft.com/dotnet/articles/core/preview3/tools/dotnet-restore), pesquisa na IU do Visual Studio, e [ `nuget.exe push` ](../tools/cli-ref-push.md).

Observe que em alguns casos, nuget.org tem requisitos adicionais que não são impostos por outras fontes de pacote. Essas diferenças são documentadas pelo [nuget.org protocolos](nuget-protocols.md).

## <a name="service-index"></a>Índice de serviço

O ponto de entrada para a API é um documento JSON em um local conhecido. Este documento é chamado de **índice de serviço**.
O local do índice do serviço nuget.org é `https://api.nuget.org/v3/index.json`.

Este documento JSON contém uma lista de *recursos* que forneçam funcionalidade diferente e atender a diferentes casos de uso.

Clientes que oferecem suporte a API devem aceitar um ou mais desses URL do serviço de índice como o meio de se conectar a fontes de pacote do respectivos.

Para obter mais informações sobre o índice de serviço, consulte [sua referência de API](service-index.md).

## <a name="versioning"></a>Controle de versão

A API é a versão 3 do protocolo HTTP do NuGet. Às vezes, esse protocolo é conhecido como "a API V3." Esses documentos de referência fará referência a esta versão do protocolo simplesmente como "a API".

O serviço de versão de esquema de índice é indicado pelo `version` propriedade no índice de serviço. A API exige que a cadeia de caracteres de versão tem um número de versão principal do `3`. Como as alterações recentes não são feitas para o esquema de índice de serviço, versão secundária da cadeia de caracteres de versão será aumentado.

Clientes mais antigos (como nuget.exe 2. x) não suportam a API V3 e oferecem suporte apenas a API V2 mais antigos, que não está documentado aqui.

A API do NuGet V3 é chamada assim porque é a sucessora da API V2, que era o protocolo baseado em OData implementado pela versão 2. x do cliente NuGet oficial. A API V3 primeiro era compatível com a versão 3.0 do cliente NuGet oficial e ainda a versão mais recente principal protocolo tem suporte pelo cliente do NuGet, 4.0 e no. 

Alterações de protocolo recentes não foram feitas para a API desde a primeira versão.

## <a name="resources-and-schema"></a>Recursos e esquema

O **índice de serviço** descreve uma variedade de recursos. O conjunto atual de recursos com suporte são os seguintes:

Nome do recurso                                                          | Necessária | Descrição
---------------------------------------------------------------------- | -------- | -----------
[`PackagePublish`](package-publish-resource.md)                        | sim      | Enviar por push e excluir ou remover da lista pacotes.
[`SearchQueryService`](search-query-service-resource.md)               | sim      | Filtrar e procurar pacotes pela palavra-chave.
[`RegistrationsBaseUrl`](registration-base-url-resource.md)            | sim      | Obter metadados de pacote.
[`PackageBaseAddress`](package-base-address-resource.md)               | sim      | Obter o conteúdo do pacote (. nupkg).
[`SearchAutocompleteService`](search-autocomplete-service-resource.md) | no       | Detecte IDs de pacote e de versões por subcadeia de caracteres.
[`ReportAbuseUriTemplate`](report-abuse-resource.md)                   | no       | Construa uma URL para acessar uma página da web de "relatar abuso".
[`Catalog`](catalog-resource.md)                                       | no       | Registro completo de todos os eventos de pacote.

Em geral, todos os dados não binários retornados por um recurso da API são serializados usando JSON. O esquema de resposta retornado por cada recurso no índice de serviço é definido individualmente para esse recurso. Para obter mais informações sobre cada recurso, consulte os tópicos listados acima.

> [!Note]
> Quando uma origem não implementa `SearchAutocompleteService` qualquer comportamento de preenchimento automático deve ser desabilitado normalmente. Quando `ReportAbuseUriTemplate` não é implementada, a cai de cliente NuGet oficial para do nuget.org relatar abuso URL (controladas por [NuGet/Home #4924](https://github.com/NuGet/Home/issues/4924)). Outros clientes podem optar por simplesmente não mostram uma URL do relatório abuso para o usuário.

## <a name="timestamps"></a>Carimbos de hora

Todos os carimbos de hora retornados pela API são UTC ou for especificados usando [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) representação. 

## <a name="http-methods"></a>Métodos HTTP

Verbo   | Use
------ | -----------
OBTER    | Executa uma operação somente leitura, normalmente a recuperação de dados.
HOME   | Busca os cabeçalhos de resposta para o correspondente `GET` solicitação.
PUT    | Cria um recurso que não existe ou, se ele existir, atualizá-la. Alguns recursos podem não aceitar a atualização.
DELETE | Exclui ou unlists um recurso.

## <a name="http-status-codes"></a>Códigos de status HTTP

Código | Descrição
---- | -----
200  | Caso de sucesso, e há um corpo de resposta.
201  | Êxito e o recurso foi criado.
202  | Caso de sucesso, a solicitação foi aceita, mas algum trabalho ainda pode estar incompleto e concluído assincronamente.
204  | Caso de sucesso, mas não há nenhum corpo de resposta.
301  | Um redirecionamento permanente.
302  | Um redirecionamento temporário.
400  | Os parâmetros na URL ou no corpo da solicitação não são válidos.
401  | As credenciais fornecidas são inválidas.
403  | A ação não é permitida fornecido as credenciais fornecidas.
404  | O recurso solicitado não existe.
409  | A solicitação está em conflito com um recurso existente.
500  | O serviço encontrou um erro inesperado.
503  | O serviço está temporariamente indisponível.

Qualquer `GET` solicitação feita para um ponto de extremidade de API pode retornar um redirecionamento HTTP (301 ou 302). Os clientes devem tratar normalmente tais redirecionamentos observando o `Location` cabeçalho e emitindo um subsequente `GET`. Documentação sobre pontos de extremidade específicos não explicitamente destacam onde redireciona pode ser usada.

No caso de um código de status de nível 500, o cliente pode implementar um mecanismo de repetição razoável. O oficial NuGet cliente tenta novamente três vezes ao encontrar qualquer código de status de nível 500 ou erro de TCP/DNS.

## <a name="http-request-headers"></a>Cabeçalhos de solicitação HTTP

Nome                     | Descrição
------------------------ | -----------
X-NuGet-ApiKey           | Obrigatório para envio e exclusão, consulte [ `PackagePublish` recursos](package-publish-resource.md)
Versão X-NuGet-cliente   | **Preterido** e substituído por`X-NuGet-Protocol-Version`
X-NuGet-versão de protocolo | Necessário em certos casos somente em nuget.org, consulte [nuget.org protocolos](NuGet-Protocols.md)

## <a name="authentication"></a>Autenticação

A autenticação é deixada até a implementação de origem do pacote para definir. Para nuget.org, somente o `PackagePublish` recurso requer a autenticação por meio de um cabeçalho de chave de API especial. Consulte [ `PackagePublish` recurso](package-publish-resource.md) para obter detalhes.
