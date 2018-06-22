---
title: Enviar por push e excluir a API do NuGet
description: O serviço de publicação permite que os clientes publicar novos pacotes e remover da lista ou excluir os pacotes existentes.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 911c8238624f806b1fbb5c7938d02b6bdfbd8614
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819475"
---
# <a name="push-and-delete"></a>Enviar por push e excluir

É possível enviar por push, excluir (ou remover da lista, dependendo da implementação de servidor) e relist pacotes usando a API do NuGet V3. Essas operações baseiam-se do `PackagePublish` recurso encontrado na [índice de serviço](service-index.md).

## <a name="versioning"></a>Controle de versão

O seguinte `@type` valor é usado:

Valor @type          | Observações
-------------------- | -----
PackagePublish/2.0.0 | A versão inicial

## <a name="base-url"></a>URL Base

A URL base para as seguintes APIs é o valor da `@id` propriedade o `PackagePublish/2.0.0` recursos na origem do pacote [índice de serviço](service-index.md). Para obter a documentação abaixo URL do nuget.org é usado. Considere `https://www.nuget.org/api/v2/package` como um espaço reservado para o `@id` valor encontrado no índice de serviço.

Observe que essa URL aponta para o mesmo local que o ponto de extremidade de envio por push herdado V2 como o protocolo é o mesmo.

## <a name="http-methods"></a>Métodos HTTP

O `PUT`, `POST` e `DELETE` métodos HTTP compatíveis com esse recurso. Para quais métodos têm suporte em cada ponto de extremidade, consulte abaixo.

## <a name="push-a-package"></a>Enviar um pacote

> [!Note]
> NuGet.org tem [requisitos adicionais](NuGet-Protocols.md) para interagir com o ponto de extremidade de envio por push.

NuGet.org dá suporte a envio novos pacotes usando a seguinte API. Se o pacote com a ID e a versão fornecida já existir, nuget.org rejeitará o envio por push. Outras fontes de pacote podem oferecer suporte a substituição de um pacote existente.

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a>Parâmetros de solicitação

Nome           | No     | Tipo   | Necessária | Observações
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Cabeçalho | cadeia de caracteres | sim      | Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`

A chave de API é uma cadeia de caracteres opaca obtidos de origem do pacote pelo usuário e configurado no cliente. Nenhum formato de cadeia de caracteres específica é obrigatória, mas o comprimento da chave de API não deve exceder um tamanho razoável para valores de cabeçalho HTTP.

### <a name="request-body"></a>Corpo da solicitação

O corpo da solicitação deve ser da seguinte forma:

#### <a name="multipart-form-data"></a>Dados de formulário de várias partes

O cabeçalho de solicitação `Content-Type` é `multipart/form-data` e o primeiro item no corpo da solicitação é os bytes brutos do nupkg sendo enviado. Itens subsequentes no corpo com diversas partes são ignorados. O nome do arquivo ou quaisquer outros cabeçalhos dos itens de várias partes são ignorados.

### <a name="response"></a>Resposta

Código de status | Significado
----------- | -------
201, 202    | O pacote foi enviado com êxito
400         | O pacote fornecido é inválido
409         | Já existe um pacote com a ID e a versão fornecida

Implementações de servidor variam de acordo o código de status de êxito retornado quando um pacote é enviado com êxito.

## <a name="delete-a-package"></a>Excluir um pacote

NuGet.org interpreta a solicitação de exclusão do pacote como um "remover da lista". Isso significa que o pacote ainda está disponível para os consumidores existentes do pacote, mas o pacote não aparece nos resultados da pesquisa ou na interface da web. Para obter mais informações sobre esta prática, consulte o [pacotes excluído](../policies/deleting-packages.md) política. Outras implementações do servidor estão livres para interpretar esse sinal como uma exclusão de disco rígida, exclusão reversível ou remover da lista. Por exemplo, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (uma implementação de servidor somente com suporte a mais antiga API V2) oferece suporte à manipulação esta solicitação como um unlist ou uma exclusão de disco rígida com base em uma opção de configuração.

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>Parâmetros de solicitação

Nome           | No     | Tipo   | Necessária | Observações
-------------- | ------ | ------ | -------- | -----
ID             | URL    | cadeia de caracteres | sim      | A ID do pacote a ser excluído
VERSION        | URL    | cadeia de caracteres | sim      | A versão do pacote a excluir
X-NuGet-ApiKey | Cabeçalho | cadeia de caracteres | sim      | Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Resposta

Código de status | Significado
----------- | -------
204         | O pacote foi excluído
404         | Nenhum pacote com fornecido `ID` e `VERSION` existe

## <a name="relist-a-package"></a>Relist um pacote

Se um pacote não esteja listado, é possível fazer com que o pacote novamente visível nos resultados da pesquisa usando o ponto de extremidade de "relist". Esse ponto de extremidade tem a mesma forma como o [excluir (remover da lista) ponto de extremidade](#delete-a-package) , mas usa o `POST` método HTTP em vez do `DELETE` método.

Se o pacote já está listado, a solicitação ainda será bem-sucedida.

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>Parâmetros de solicitação

Nome           | No     | Tipo   | Necessária | Observações
-------------- | ------ | ------ | -------- | -----
ID             | URL    | cadeia de caracteres | sim      | A ID do pacote para relist
VERSION        | URL    | cadeia de caracteres | sim      | A versão do pacote a ser relist
X-NuGet-ApiKey | Cabeçalho | cadeia de caracteres | sim      | Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Resposta

Código de status | Significado
----------- | -------
200         | O pacote agora está listado
404         | Nenhum pacote com fornecido `ID` e `VERSION` existe
