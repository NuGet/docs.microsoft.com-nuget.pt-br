---
title: Enviar por push e excluir, API do NuGet
description: O serviço de publicação permite que os clientes publiquem novos pacotes e deslistem ou excluam pacotes existentes.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0a79266011433d5adc1341a8e250838988c84d13
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773925"
---
# <a name="push-and-delete"></a>Enviar por push e excluir

É possível enviar por push, excluir (ou deslistar, dependendo da implementação do servidor) e relistar os pacotes usando a API do NuGet v3. Essas operações são baseadas no `PackagePublish` recurso encontrado no [índice de serviço](service-index.md).

## <a name="versioning"></a>Controle de versão

O seguinte `@type` valor é usado:

@type valor          | Observações
-------------------- | -----
PackagePublish/2.0.0 | A versão inicial

## <a name="base-url"></a>URL base

A URL base para as APIs a seguir é o valor da `@id` Propriedade do `PackagePublish/2.0.0` recurso no [índice de serviço](service-index.md)da origem do pacote. Para a documentação abaixo, a URL do NuGet. org é usada. Considere `https://www.nuget.org/api/v2/package` como um espaço reservado para o `@id` valor encontrado no índice de serviço.

Observe que essa URL aponta para o mesmo local que o ponto de extremidade de push v2 herdado, pois o protocolo é o mesmo.

## <a name="http-methods"></a>Métodos HTTP

`PUT` `POST` `DELETE` Esse recurso oferece suporte aos métodos http e. Para quais métodos têm suporte em cada ponto de extremidade, consulte abaixo.

## <a name="push-a-package"></a>Enviar por push um pacote

> [!Note]
> o nuget.org tem [requisitos adicionais](NuGet-Protocols.md) para interagir com o ponto de extremidade de push.

o nuget.org dá suporte ao envio de novos pacotes usando a API a seguir. Se o pacote com a ID e a versão fornecidas já existir, o nuget.org rejeitará o envio por push. Outras origens de pacote podem dar suporte à substituição de um pacote existente.

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a>Parâmetros da solicitação

Nome           | Em     | Type   | Necessária | Observações
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Cabeçalho | string | sim      | Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`

A chave de API é uma cadeia de caracteres opaca proveniente da origem do pacote pelo usuário e configurada no cliente. Nenhum formato de cadeia de caracteres específico é obrigatório, mas o comprimento da chave de API não deve exceder um tamanho razoável para valores de cabeçalho HTTP.

### <a name="request-body"></a>Corpo da solicitação

O corpo da solicitação deve estar no seguinte formato:

#### <a name="multipart-form-data"></a>Dados de formulário com várias partes

O cabeçalho da solicitação `Content-Type` é `multipart/form-data` e o primeiro item no corpo da solicitação são os bytes brutos de. nupkg sendo enviados por push. Os itens subsequentes no corpo com diversas partes são ignorados. O nome do arquivo ou quaisquer outros cabeçalhos dos itens com diversas partes são ignorados.

### <a name="response"></a>Resposta

Código de status | Significado
----------- | -------
201, 202    | O pacote foi enviado por push com êxito
400         | O pacote fornecido é inválido
409         | Já existe um pacote com a ID e a versão fornecidas

Implementações de servidor variam no código de status de êxito retornado quando um pacote é enviado por push com êxito.

## <a name="delete-a-package"></a>Excluir um pacote

nuget.org interpreta a solicitação de exclusão de pacote como uma "deslista". Isso significa que o pacote ainda está disponível para os consumidores existentes do pacote, mas o pacote não aparece mais nos resultados da pesquisa ou na interface da Web. Para obter mais informações sobre essa prática, consulte a política de [pacotes excluídos](../nuget-org/policies/deleting-packages.md) . Outras implementações de servidor são livres para interpretar esse sinal como uma exclusão rígida, exclusão reversível ou deslistar. Por exemplo, o [NuGet. Server](https://www.nuget.org/packages/NuGet.Server) (uma implementação de servidor que dá suporte apenas à API v2 mais antiga) dá suporte ao tratamento dessa solicitação como uma exclusão incorreta ou um disco rígido com base em uma opção de configuração.

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>Parâmetros da solicitação

Nome           | Em     | Type   | Necessária | Observações
-------------- | ------ | ------ | -------- | -----
ID             | URL    | string | sim      | A ID do pacote a ser excluído
VERSION        | URL    | string | sim      | A versão do pacote a ser excluído
X-NuGet-ApiKey | Cabeçalho | string | sim      | Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Resposta

Código de status | Significado
----------- | -------
204         | O pacote foi excluído
404         | Nenhum pacote com o fornecido `ID` e `VERSION` existe

## <a name="relist-a-package"></a>Relistar um pacote

Se um pacote estiver deslistado, será possível tornar esse pacote mais uma vez visível nos resultados da pesquisa usando o ponto de extremidade "relistar". Esse ponto de extremidade tem a mesma forma que o [ponto de extremidade de exclusão (deslistar)](#delete-a-package) , mas usa o `POST` método http em vez do `DELETE` método.

Se o pacote já estiver listado, a solicitação ainda terá sucesso.

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>Parâmetros da solicitação

Nome           | Em     | Type   | Necessária | Observações
-------------- | ------ | ------ | -------- | -----
ID             | URL    | string | sim      | A ID do pacote a ser relistado
VERSION        | URL    | string | sim      | A versão do pacote a ser relistada
X-NuGet-ApiKey | Cabeçalho | string | sim      | Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Resposta

Código de status | Significado
----------- | -------
200         | O pacote agora está listado
404         | Nenhum pacote com o fornecido `ID` e `VERSION` existe
