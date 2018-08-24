---
title: Visão geral da API do NuGet
description: A API do NuGet é um conjunto de pontos de extremidade HTTP que podem ser usados para baixar os pacotes, buscar metadados, publicar novos pacotes, etc.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0cb40a640a0bab63a63b3b690a34f1f8cbf7fcb8
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/21/2018
ms.locfileid: "42793186"
---
# <a name="nuget-api"></a>API do NuGet

A API do NuGet é um conjunto de pontos de extremidade HTTP que pode ser usado para baixar os pacotes, buscar metadados, publicar novos pacotes e executar a maioria das outras operações disponíveis em que os clientes do NuGet oficiais.

Essa API é usada pelo cliente do NuGet no Visual Studio, nuget.exe e a CLI do .NET para executar operações do NuGet, como [ `dotnet restore` ](/dotnet/articles/core/preview3/tools/dotnet-restore), pesquisa na IU do Visual Studio, e [ `nuget.exe push` ](../tools/cli-ref-push.md).

Observe que em alguns casos, nuget.org tem requisitos adicionais que não são impostos por outras fontes de pacote. Essas diferenças são documentadas pela [protocolos nuget.org](nuget-protocols.md).

Para uma enumeração simple e download de versões nuget.exe disponíveis, consulte o [tools.json](tools-json.md) ponto de extremidade.

## <a name="service-index"></a>Índice de serviço

O ponto de entrada para a API é um documento JSON em um local bem conhecido. Este documento é chamado de **índice de serviço**. O local do índice de serviço para nuget.org é `https://api.nuget.org/v3/index.json`.

Este documento JSON contém uma lista de *recursos* que fornecem uma funcionalidade diferente e atender a diferentes casos de uso.

Clientes que oferecem suporte a API devem aceitar um ou mais desses URL do serviço de índice como o meio de se conectar a fontes o respectivo pacote.

Para obter mais informações sobre o índice de serviço, consulte [sua referência de API](service-index.md).

## <a name="versioning"></a>Controle de versão

A API é a versão 3 do protocolo HTTP do NuGet. Às vezes, esse protocolo é conhecido como "a API V3". Esses documentos de referência fará referência a esta versão do protocolo simplesmente como "API".

O serviço de versão de esquema de índice é indicado pela `version` propriedade no índice de serviço. A API exige que a cadeia de caracteres de versão tem um número de versão principal `3`. Como o esquema de índice de serviço forem feitas alterações sem interrupções, versão secundária da cadeia de caracteres de versão será aumentado.

Os clientes mais antigos (como nuget.exe 2. x) não suportam a API V3 e só há suporte para a API V2 mais antigos, que não está documentada aqui.

A API do NuGet V3 é chamada assim porque é a sucessora da API V2, que era o protocolo OData-based implementado pela versão 2.x do cliente do NuGet oficial. A API V3 primeiro era compatível com a versão 3.0 do cliente do NuGet oficial e é ainda a versão mais recente principal protocolo com suporte pelo cliente do NuGet, 4.0 e no. 

As alterações do protocolo não significativas foram feitas para a API desde a primeira versão.

## <a name="resources-and-schema"></a>Recursos e esquema

O **índice de serviço** descreve uma variedade de recursos. O conjunto atual de recursos com suporte são os seguintes:

Nome do recurso                                                          | Necessária | Descrição
---------------------------------------------------------------------- | -------- | -----------
[`PackagePublish`](package-publish-resource.md)                        | sim      | Enviar por push e excluir (ou remover da lista) pacotes.
[`SearchQueryService`](search-query-service-resource.md)               | sim      | Filtrar e pesquisar pacotes pela palavra-chave.
[`RegistrationsBaseUrl`](registration-base-url-resource.md)            | sim      | Obter metadados de pacote.
[`PackageBaseAddress`](package-base-address-resource.md)               | sim      | Obter o conteúdo do pacote (. nupkg).
[`SearchAutocompleteService`](search-autocomplete-service-resource.md) | no       | Descubra os IDs de pacote e versões pela subcadeia de caracteres.
[`ReportAbuseUriTemplate`](report-abuse-resource.md)                   | no       | Construa uma URL para acessar uma página da web de "relatar abuso".
[`RepositorySignatures`](repository-signatures-resource.md)            | no       | Obter certificados usados na assinatura do repositório.
[`Catalog`](catalog-resource.md)                                       | no       | Registro completo de todos os eventos de pacote.

Em geral, todos os dados não binários retornados por um recurso de API são serializados usando JSON. O esquema de resposta retornado por cada recurso no índice de serviço é definido individualmente para esse recurso. Para obter mais informações sobre cada recurso, consulte os tópicos listados acima.

> [!Note]
> Quando uma fonte não implementa `SearchAutocompleteService` qualquer comportamento de preenchimento automático deve ser desabilitado normalmente. Quando `ReportAbuseUriTemplate` não for implementado, o cai de cliente do NuGet oficial para do nuget.org relatar abuso URL (controladas pelo [NuGet/Home #4924](https://github.com/NuGet/Home/issues/4924)). Outros clientes podem optar por simplesmente mostra uma URL para relatar abuso para o usuário.

## <a name="timestamps"></a>Carimbos de hora

Todos os carimbos de hora retornados pela API são UTC ou caso contrário, são especificados usando [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) representação. 

## <a name="http-methods"></a>Métodos HTTP

Verbo   | Use
------ | -----------
OBTER    | Executa uma operação somente leitura, normalmente a recuperação de dados.
HOME   | Busca os cabeçalhos de resposta para o controle correspondente `GET` solicitação.
PUT    | Cria um recurso que não existe ou, se ela existir, atualizá-la. Alguns recursos podem não aceitar a atualização.
DELETE | Exclui ou retira da lista de um recurso.

## <a name="http-status-codes"></a>Códigos de status HTTP

Código | Descrição
---- | -----
200  | Caso de sucesso, e há um corpo de resposta.
201  | Êxito e o recurso foi criado.
202  | Caso de sucesso, a solicitação foi aceita, mas algum trabalho ainda pode estar incompleta e concluído assincronamente.
204  | Caso de sucesso, mas não há nenhum corpo de resposta.
301  | Um redirecionamento permanente.
302  | Um redirecionamento temporário.
400  | Os parâmetros na URL ou no corpo da solicitação não são válidos.
401  | As credenciais fornecidas são inválidas.
403  | A ação não é permitida considerando as credenciais fornecidas.
404  | O recurso solicitado não existe.
409  | A solicitação está em conflito com um recurso existente.
500  | O serviço encontrou um erro inesperado.
503  | O serviço está temporariamente indisponível.

Qualquer `GET` solicitação feita para um ponto de extremidade de API pode retornar um redirecionamento HTTP (301 ou 302). Os clientes devem simplesmente manipular esses redirecionamentos, observando os `Location` cabeçalho e emitindo um subsequentes `GET`. Documentação sobre pontos de extremidade específicos não irá chamar explicitamente onde redirecionamentos podem ser usada.

No caso de um código de status de nível 500, o cliente pode implementar um mecanismo de repetição razoável. O oficial NuGet cliente tenta novamente três vezes ao encontrar qualquer código de status de nível 500 ou erro de TCP/DNS.

## <a name="http-request-headers"></a>Cabeçalhos de solicitação HTTP

Nome                     | Descrição
------------------------ | -----------
X-NuGet-ApiKey           | Necessário para envio por push e delete, consulte [ `PackagePublish` recursos](package-publish-resource.md)
X-NuGet-Client-Version   | **Preterido** e substituído por `X-NuGet-Protocol-Version`
X-NuGet-Protocol-Version | Obrigatório em certos casos somente em nuget.org, consulte [protocolos nuget.org](NuGet-Protocols.md)
X-NuGet-Session-Id       | *Opcional*. NuGet clientes v4.7 + identificar solicitações HTTP que fazem parte da mesma sessão de cliente do NuGet. Para `PackageReference` operações de restauração existe é uma id de sessão único, para outros cenários, como preenchimento, automático e `packages.config` restauração, pode haver vários diferentes id de sessão devido a como o código é acrescentado.

## <a name="authentication"></a>Autenticação

Autenticação é deixada a cargo da implementação de origem do pacote para definir. Para nuget.org, somente o `PackagePublish` recurso requer a autenticação por meio de um cabeçalho de chave de API especial. Ver [ `PackagePublish` recurso](package-publish-resource.md) para obter detalhes.
