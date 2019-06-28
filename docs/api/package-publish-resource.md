---
title: Enviar por push e excluir, a API do NuGet
description: O serviço de publicação permite que os clientes publicar novos pacotes e remover da lista ou excluir os pacotes existentes.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 6e81055796e20186c5769d2ec39849e6c551ff87
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426716"
---
# <a name="push-and-delete"></a>Enviar por push e excluir

É possível enviar por push, excluir (ou remover da lista, dependendo da implementação de servidor) e relist pacotes usando a API do NuGet V3. Essas operações são baseadas fora do `PackagePublish` recurso encontrado na [índice de serviço](service-index.md).

## <a name="versioning"></a>Controle de versão

O seguinte `@type` valor é usado:

Valor @type          | Observações
-------------------- | -----
PackagePublish/2.0.0 | A versão inicial

## <a name="base-url"></a>URL Base

A URL base para as APIs a seguir é o valor da `@id` propriedade do `PackagePublish/2.0.0` recurso na origem do pacote [índice de serviço](service-index.md). Para obter a documentação abaixo, a URL do nuget.org é usado. Considere `https://www.nuget.org/api/v2/package` como um espaço reservado para o `@id` valor encontrado no índice de serviço.

Observe que essa URL aponta para o mesmo local que o ponto de extremidade de envio por push herdado V2, pois o protocolo é o mesmo.

## <a name="http-methods"></a>Métodos HTTP

O `PUT`, `POST` e `DELETE` métodos HTTP compatíveis com esse recurso. Para quais métodos são suportados em cada ponto de extremidade, consulte abaixo.

## <a name="push-a-package"></a>Enviar por push a um pacote

> [!Note]
> tem NuGet.org [requisitos adicionais](NuGet-Protocols.md) para interagir com o ponto de extremidade de envio por push.

NuGet.org dá suporte a enviar por push novos pacotes usando a API a seguir. Se o pacote com a ID e a versão fornecido já existir, o nuget.org rejeitará o envio por push. Outras fontes de pacote podem dar suporte a substituição de um pacote existente.

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a>Parâmetros de solicitação

Nome           | No     | Tipo   | Necessária | Observações
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Cabeçalho | cadeia de caracteres | sim      | Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`

A chave de API é uma cadeia de caracteres opaca obtidos de origem do pacote pelo usuário e configurado no cliente. Nenhum formato de cadeia de caracteres específica é obrigatória, mas o comprimento da chave de API não deve exceder um tamanho razoável para valores de cabeçalho HTTP.

### <a name="request-body"></a>Corpo da solicitação

O corpo da solicitação deve vir da seguinte forma:

#### <a name="multipart-form-data"></a>Dados de formulário de várias partes

O cabeçalho de solicitação `Content-Type` é `multipart/form-data` e o primeiro item no corpo da solicitação é os bytes brutos da. nupkg que está sendo enviado por push. Os itens subsequentes no corpo com diversas partes são ignorados. O nome do arquivo ou quaisquer outros cabeçalhos dos itens de várias partes são ignorados.

### <a name="response"></a>Resposta

Código de status | Significado
----------- | -------
201, 202    | O pacote foi enviado com êxito
400         | O pacote fornecido é inválido
409         | Já existe um pacote com a ID e a versão fornecida

Implementações de servidor variam de acordo o código de status de êxito retornado quando um pacote é enviado com êxito.

## <a name="delete-a-package"></a>Excluir um pacote

NuGet.org interpreta a solicitação de exclusão do pacote como um "remover da lista". Isso significa que o pacote ainda está disponível para os consumidores existentes do pacote, mas o pacote não aparece nos resultados da pesquisa ou na interface da web. Para obter mais informações sobre essa prática, consulte o [excluído pacotes](../nuget-org/policies/deleting-packages.md) política. Outras implementações de servidor são livres para interpretar esse sinal como uma exclusão de disco rígida, exclusão reversível ou remover da lista. Por exemplo, [NuGet. Server](https://www.nuget.org/packages/NuGet.Server) (uma implementação de servidor somente com suporte a mais antiga API V2) dá suporte a tratamento essa solicitação como um unlist ou uma exclusão de disco rígida com base em uma opção de configuração.

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>Parâmetros de solicitação

Nome           | No     | Tipo   | Necessária | Observações
-------------- | ------ | ------ | -------- | -----
ID             | URL    | cadeia de caracteres | sim      | A ID do pacote a ser excluído
VERSION        | URL    | cadeia de caracteres | sim      | A versão do pacote a ser excluído
X-NuGet-ApiKey | Cabeçalho | cadeia de caracteres | sim      | Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Resposta

Código de status | Significado
----------- | -------
204         | O pacote foi excluído
404         | Nenhum pacote fornecido `ID` e `VERSION` existe

## <a name="relist-a-package"></a>Relist um pacote

Se um pacote for removido da lista, é possível fazer com que o pacote novamente visível nos resultados da pesquisa usando o ponto de extremidade "relist". Esse ponto de extremidade tem a mesma forma que o [excluir (remover da lista) ponto de extremidade](#delete-a-package) , mas usa o `POST` método HTTP em vez do `DELETE` método.

Se o pacote já estiver listado, a solicitação ainda terá êxito.

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>Parâmetros de solicitação

Nome           | No     | Tipo   | Necessária | Observações
-------------- | ------ | ------ | -------- | -----
ID             | URL    | cadeia de caracteres | sim      | A ID do pacote para relist
VERSION        | URL    | cadeia de caracteres | sim      | A versão do pacote como relist
X-NuGet-ApiKey | Cabeçalho | cadeia de caracteres | sim      | Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Resposta

Código de status | Significado
----------- | -------
200         | O pacote agora está listado
404         | Nenhum pacote fornecido `ID` e `VERSION` existe
