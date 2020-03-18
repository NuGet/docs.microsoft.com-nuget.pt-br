---
title: Visão geral da API do servidor NuGet
description: A API do servidor NuGet é um conjunto de pontos de extremidade HTTP que podem ser usados para baixar pacotes, buscar metadados, publicar novos pacotes, etc.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: aacf56a5dc5af9abf6f60d42bc7fd530a128d0d8
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428705"
---
# <a name="nuget-server-api"></a>API do servidor NuGet

A API do servidor NuGet é um conjunto de pontos de extremidade HTTP que podem ser usados para baixar pacotes, buscar metadados, publicar novos pacotes e executar a maioria das outras operações disponíveis nos clientes NuGet oficiais.

Essa API é usada pelo cliente NuGet no Visual Studio, NuGet. exe e a CLI do .NET para executar operações do NuGet, como [`dotnet restore`](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), Pesquisar na interface do usuário do Visual Studio e [`nuget.exe push`](../reference/cli-reference/cli-ref-push.md).

Observe que, em alguns casos, o nuget.org tem requisitos adicionais que não são impostos por outras origens de pacote. Essas diferenças são documentadas pelos [protocolos NuGet.org](nuget-protocols.md).

Para uma enumeração simples e o download de versões disponíveis do NuGet. exe, consulte o ponto de extremidade [Tools. JSON](tools-json.md) .

## <a name="service-index"></a>Índice de serviço

O ponto de entrada para a API é um documento JSON em um local bem conhecido. Este documento é chamado de **índice de serviço**. O local do índice de serviço para nuget.org é `https://api.nuget.org/v3/index.json`.

Este documento JSON contém uma lista de *recursos* que fornecem funcionalidade diferente e atendem a diferentes casos de uso.

Os clientes que oferecem suporte à API devem aceitar uma ou mais dessas URLs de índice de serviço como o meio de conexão com as respectivas origens de pacote.

Para obter mais informações sobre o índice de serviço, consulte [sua referência de API](service-index.md).

## <a name="versioning"></a>Controle de versão

A API é a versão 3 do protocolo HTTP do NuGet. Esse protocolo é, às vezes, chamado de "API v3". Esses documentos de referência irão se referir a essa versão do protocolo simplesmente como "a API".

A versão do esquema de índice de serviço é indicada pela propriedade `version` no índice de serviço. A API determina que a cadeia de caracteres de versão tem um número de versão principal de `3`. Como alterações não significativas são feitas no esquema de índice de serviço, a versão secundária da cadeia de caracteres de versão será aumentada.

Os clientes mais antigos (como NuGet. exe 2. x) não dão suporte à API v3 e só oferecem suporte à API v2 mais antiga, que não está documentada aqui.

A API do NuGet v3 é nomeada como tal porque é o sucessor da API v2, que era o protocolo baseado em OData implementado pela versão 2. x do cliente do NuGet oficial. A API v3 era suportada pela primeira vez pela versão 3,0 do cliente do NuGet oficial e ainda é a versão mais recente do protocolo principal com suporte do cliente NuGet, 4,0 e em. 

Alterações de protocolo não separáveis foram feitas na API desde que ela foi lançada pela primeira vez.

## <a name="resources-and-schema"></a>Recursos e esquema

O **índice de serviço** descreve uma variedade de recursos. O conjunto atual de recursos com suporte é o seguinte:

Nome do recurso                                                        | Obrigatório | Descrição
-------------------------------------------------------------------- | -------- | -----------
[Catálogo](catalog-resource.md)                                       | no       | Registro completo de todos os eventos de pacote.
[PackageBaseAddress](package-base-address-resource.md)               | sim      | Obter conteúdo do pacote (. nupkg).
[PackageDetailsUriTemplate](package-details-template-resource.md)    | no       | Construa uma URL para acessar uma página da Web detalhes do pacote.
[PackagePublish](package-publish-resource.md)                        | sim      | Enviar por push e excluir (ou deslistar) pacotes.
[RegistrationsBaseUrl](registration-base-url-resource.md)            | sim      | Obter metadados do pacote.
[ReportAbuseUriTemplate](report-abuse-resource.md)                   | no       | Construa uma URL para acessar uma página da Web de abuso de relatório.
[RepositorySignatures](repository-signatures-resource.md)            | no       | Obter certificados usados para assinatura de repositório.
[SearchAutocompleteService](search-autocomplete-service-resource.md) | no       | Descobrir IDs e versões de pacote por substring.
[SearchQueryService](search-query-service-resource.md)               | sim      | Filtre e pesquise pacotes por palavra-chave.
[SymbolPackagePublish](symbol-package-publish-resource.md)           | no       | Pacotes de símbolo de push.

Em geral, todos os dados não binários retornados por um recurso de API são serializados usando JSON. O esquema de resposta retornado por cada recurso no índice de serviço é definido individualmente para esse recurso. Para obter mais informações sobre cada recurso, consulte os tópicos listados acima.

No futuro, à medida que o protocolo evolui, novas propriedades podem ser adicionadas às respostas JSON. Para que o cliente seja à prova de obsolescência, a implementação não deve assumir que o esquema de resposta é final e não pode incluir dados adicionais. Todas as propriedades que a implementação não entende devem ser ignoradas.

> [!Note]
> Quando uma origem não implementa `SearchAutocompleteService` qualquer comportamento de preenchimento automático deve ser desabilitado normalmente. Quando `ReportAbuseUriTemplate` não é implementado, o cliente do NuGet oficial volta para a URL de abuso de relatório do NuGet. org (acompanhado pelo [NuGet/Home # 4924](https://github.com/NuGet/Home/issues/4924)). Outros clientes podem optar por simplesmente não mostrar uma URL de abuso de relatório para o usuário.

### <a name="undocumented-resources-on-nugetorg"></a>Recursos não documentados no nuget.org

O índice de serviço v3 em nuget.org tem alguns recursos que não estão documentados acima. Há alguns motivos para não documentar um recurso.

Primeiro, não Documentamos os recursos usados como um detalhe de implementação de nuget.org. O `SearchGalleryQueryService` se enquadra nessa categoria. O [NuGetGallery](https://github.com/NuGet/NuGetGallery) usa esse recurso para delegar algumas consultas v2 (OData) ao nosso índice de pesquisa em vez de usar o banco de dados. Esse recurso foi introduzido por motivos de escalabilidade e não se destina ao uso externo.

Em segundo lugar, não Documentamos os recursos que nunca foram enviados em uma versão RTM do cliente oficial.
`PackageDisplayMetadataUriTemplate` e `PackageVersionDisplayMetadataUriTemplate` se enquadram nessa categoria.

Em terceiro lugar, não Documentamos os recursos que estão firmemente acoplados com o protocolo v2, que em si é intencionalmente não documentado. O recurso `LegacyGallery` se enquadra nessa categoria. Esse recurso permite que um índice de serviço v3 aponte para uma URL de origem v2 correspondente. Este recurso dá suporte à `nuget.exe list`.

Se um recurso não estiver documentado aqui, é *altamente* recomendável que você não faça uma dependência deles. Podemos remover ou alterar o comportamento desses recursos não documentados, o que pode interromper sua implementação de maneiras inesperadas.

## <a name="timestamps"></a>Carimbos de data/hora

Todos os carimbos de data/hora retornados pela API são UTC ou, de outra forma, são especificados usando a representação [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) . 

## <a name="http-methods"></a>Métodos HTTP

Verbo   | Use
------ | -----------
GET    | Executa uma operação somente leitura, normalmente recuperando dados.
HEAD   | Busca os cabeçalhos de resposta para a solicitação de `GET` correspondente.
PUT    | Cria um recurso que não existe ou, se existir, o atualiza. Alguns recursos podem não dar suporte à atualização.
DELETE | Exclui ou deslista um recurso.

## <a name="http-status-codes"></a>Códigos de status HTTP

Código | Descrição
---- | -----
200  | Êxito e há um corpo de resposta.
201  | Êxito e o recurso foi criado.
202  | Êxito, a solicitação foi aceita, mas algum trabalho ainda pode estar incompleto e concluído de forma assíncrona.
204  | Êxito, mas não há nenhum corpo de resposta.
301  | Um redirecionamento permanente.
302  | Um redirecionamento temporário.
400  | Os parâmetros na URL ou no corpo da solicitação não são válidos.
401  | As credenciais fornecidas são inválidas.
403  | A ação não é permitida dadas as credenciais fornecidas.
404  | O recurso solicitado não existe.
409  | A solicitação está em conflito com um recurso existente.
500  | O serviço encontrou um erro inesperado.
503  | O serviço está temporariamente indisponível.

Qualquer `GET` solicitação feita a um ponto de extremidade de API pode retornar um redirecionamento HTTP (301 ou 302). Os clientes devem lidar normalmente com esses redirecionamentos observando o cabeçalho `Location` e emitindo uma `GET`subsequente. A documentação referente a pontos de extremidade específicos não chamará explicitamente onde os redirecionamentos podem ser usados.

No caso de um código de status de nível 500, o cliente pode implementar um mecanismo de repetição razoável. O cliente do NuGet oficial tenta novamente três vezes ao encontrar qualquer código de status de nível 500 ou erro de TCP/DNS.

## <a name="http-request-headers"></a>Cabeçalhos de solicitação HTTP

{1&gt;Nome&lt;1}                     | Descrição
------------------------ | -----------
X-NuGet-ApiKey           | Necessário para envio por push e exclusão, consulte [`PackagePublish` recurso](package-publish-resource.md)
X-NuGet-Client-Version   | **Preterido** e substituído por `X-NuGet-Protocol-Version`
X-NuGet-Protocol-Version | Necessário em determinados casos apenas em nuget.org, consulte [protocolos NuGet.org](NuGet-Protocols.md)
X-NuGet-Session-Id       | *Opcional*. Clientes NuGet v 4.7 + identificam solicitações HTTP que fazem parte da mesma sessão de cliente NuGet.

O `X-NuGet-Session-Id` tem um único valor para todas as operações relacionadas a uma única restauração no `PackageReference`. Para outros cenários, como preenchimento automático e `packages.config` restauração, pode haver várias IDs de sessão diferentes devido ao modo como o código é fatorado.

## <a name="authentication"></a>Autenticação

A autenticação é mantida até a implementação da origem do pacote a ser definida. Para nuget.org, somente o recurso `PackagePublish` requer autenticação por meio de um cabeçalho de chave de API especial. Consulte [`PackagePublish` recurso](package-publish-resource.md) para obter detalhes.
