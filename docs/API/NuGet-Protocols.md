---
title: Protocolos de NuGet.org
description: Os protocolos nuget.org em evolução para interagir com os clientes do NuGet.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: cc6d52617ea8b69d5b18b831ddf8a1a85dd6798f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="nugetorg-protocols"></a>protocolos de NuGet.org

Para interagir com nuget.org, os clientes precisam seguir determinados protocolos. Como mantenham em evolução esses protocolos, clientes devem identificar a versão de protocolo usada ao chamar APIs do nuget.org específico. Isso permite nuget.org introduzir alterações de forma incondicional para os clientes antigos.

> [!Note]
> As APIs documentadas nesta página são específicas para nuget.org e não há nenhuma expectativa de outras implementações de servidor NuGet introduzir essas APIs. 

Para obter informações sobre a API do NuGet amplamente implementados em ecossistema do NuGet, consulte o [visão geral da API](overview.md).

Este tópico lista os vários protocolos como e quando eles surgem existência.

## <a name="nuget-protocol-version-410"></a>Versão de protocolo do NuGet 4.1.0

O 4.1.0 protocolo Especifica o uso de chaves de escopo verificar para interagir com os serviços que não sejam nuget.org, para validar um pacote em uma conta do nuget.org. Observe que o `4.1.0` versão número é uma cadeia de caracteres opaca mas acontece coincidir com a primeira versão do cliente NuGet oficial que suporte esse protocolo.

A validação garante que as chaves de API criada pelo usuário são usadas apenas com nuget.org, e essa verificação ou validação de um serviço de terceiros é tratada por meio de uma chave de escopo verificar uso uma única vez. Essas chaves de escopo verificar podem ser usados para validar que o pacote pertence a um determinado usuário (conta) em nuget.org.

### <a name="client-requirement"></a>Requisito de cliente

Os clientes precisam passar o seguinte cabeçalho quando fazem chamadas de API para **push** pacotes nuget.org:

    X-NuGet-Protocol-Version: 4.1.0

Observe que o `X-NuGet-Client-Version` cabeçalho possui uma semântica semelhante, mas é reservado para ser usado apenas pelo cliente do NuGet oficial. Os clientes de terceiros devem usar o `X-NuGet-Protocol-Version` cabeçalho e o valor.

O **push** próprio protocolo é descrito na documentação para o [ `PackagePublish` recurso](package-publish-resource.md).

Se um cliente interage com serviços externos e precisa validar se um pacote pertence a um determinado usuário (conta), ele deve usar o protocolo a seguir e use as teclas de escopo de verificar e não as chaves de API do nuget.org.

### <a name="api-to-request-a-verify-scope-key"></a>API para solicitar uma chave de escopo de verificar

Essa API é usada para obter uma chave Verifique se o escopo para um autor nuget.org validar um pacote pertencente a ele.

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a>Parâmetros de solicitação

Nome           | No     | Tipo   | Necessária | Observações
-------------- | ------ | ------ | -------- | -----
ID             | URL    | cadeia de caracteres | sim      | O identidier de pacote para o qual a chave de escopo de verificar é solicitada
VERSION        | URL    | cadeia de caracteres | no       | A versão do pacote
X-NuGet-ApiKey | Cabeçalho | cadeia de caracteres | sim      | Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`

#### <a name="response"></a>Resposta

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>API para verificar a chave de escopo de verificar

Essa API é usada para validar uma chave Verifique se o escopo para o pacote de propriedade pelo autor do nuget.org.

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a>Parâmetros de solicitação

Nome           | No     | Tipo   | Necessária | Observações
-------------  | ------ | ------ | -------- | -----
ID             | URL    | cadeia de caracteres | sim      | O identificador de pacote para o qual a chave de escopo de verificar é solicitada
VERSION        | URL    | cadeia de caracteres | no       | A versão do pacote
X-NuGet-ApiKey | Cabeçalho | cadeia de caracteres | sim      | Por exemplo, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`

> [!Note]
> Essa chave de API do escopo verificar expira em um dia ou no primeiro uso, o que ocorrer primeiro.

#### <a name="response"></a>Resposta

Código de status | Significado
----------- | -------
200         | A chave de API é válida
403         | A chave de API é inválida ou não autorizado a enviar por push contra o pacote
404         | O pacote referenciado por `ID` e `VERSION` (opcional) não existe
