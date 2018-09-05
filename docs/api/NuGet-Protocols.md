---
title: Protocolos NuGet.org
description: Os protocolos nuget.org em evolução para interagir com os clientes do NuGet.
author: anangaur
ms.author: anangaur
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d0add777040dbb8bcde6d8e385a4feab568e5cdd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547267"
---
# <a name="nugetorg-protocols"></a>protocolos NuGet.org

Para interagir com o nuget.org, os clientes precisam seguir determinados protocolos. Porque esses protocolos mantenham evoluindo, os clientes devem identificar a versão do protocolo usarem ao chamar APIs de nuget.org específico. Isso permite que o nuget.org introduzir alterações de forma incondicional para os clientes antigos.

> [!Note]
> As APIs documentadas nesta página são específicas para o nuget.org e não há nenhuma expectativa de outras implementações de servidor do NuGet introduzir essas APIs. 

Para obter informações sobre a API do NuGet amplamente implementada no ecossistema do NuGet, consulte o [visão geral da API](overview.md).

Este tópico lista os vários protocolos, como e quando eles vêm à existência.

## <a name="nuget-protocol-version-410"></a>Versão de protocolo do NuGet 4.1.0

A 4.1.0 especifica o protocolo de uso de chaves de escopo verificar para interagir com serviços diferentes do nuget.org, a fim de validar um pacote em uma conta do nuget.org. Observe que o `4.1.0` versão número é uma cadeia de caracteres opaca, mas coincidir com a primeira versão do cliente do NuGet oficial que suporte esse protocolo.

A validação garante que as chaves de API criados pelo usuário são usadas somente com nuget.org e essa verificação ou validação de um serviço de terceiros é tratada por meio de chaves de escopo verificar um único uso. Essas chaves de escopo verificar podem ser usados para validar que o pacote pertence a um usuário específico (conta) em nuget.org.

### <a name="client-requirement"></a>Requisito de cliente

Os clientes devem passar o cabeçalho a seguir ao fazer chamadas à API **push** pacotes para nuget.org:

    X-NuGet-Protocol-Version: 4.1.0

Observe que o `X-NuGet-Client-Version` cabeçalho tem semântica semelhantes, mas está reservado para ser usado apenas pelo cliente do NuGet oficial. Os clientes de terceiros devem usar o `X-NuGet-Protocol-Version` cabeçalho e o valor.

O **push** protocolo em si é descrito na documentação para o [ `PackagePublish` recurso](package-publish-resource.md).

Se um cliente interage com serviços externos e necessidades para validar se um pacote pertence a um usuário específico (conta), ele deve usar o protocolo a seguir e usar as teclas de Verifique se o escopo e não as chaves de API do nuget.org.

### <a name="api-to-request-a-verify-scope-key"></a>API para solicitar uma chave Verifique se o escopo

Essa API é usada para obter uma chave Verifique se o escopo para um autor de nuget.org validar um pacote pertencente a pessoa.

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a>Parâmetros de solicitação

Nome           | No     | Tipo   | Necessária | Observações
-------------- | ------ | ------ | -------- | -----
ID             | URL    | cadeia de caracteres | sim      | O identidier de pacote para o qual a tecla de escopo de verificação é solicitada
VERSION        | URL    | cadeia de caracteres | no       | A versão do pacote
X-NuGet-ApiKey | Cabeçalho | cadeia de caracteres | sim      | Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`

#### <a name="response"></a>Resposta

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>API para verificar se a tecla de escopo de verificação

Essa API é usada para validar uma chave de Verifique se o escopo para o pacote de propriedade pelo autor do nuget.org.

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a>Parâmetros de solicitação

Nome           | No     | Tipo   | Necessária | Observações
-------------  | ------ | ------ | -------- | -----
ID             | URL    | cadeia de caracteres | sim      | O identificador de pacote para o qual a tecla de escopo de verificação é solicitada
VERSION        | URL    | cadeia de caracteres | no       | A versão do pacote
X-NuGet-ApiKey | Cabeçalho | cadeia de caracteres | sim      | Por exemplo, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`

> [!Note]
> Essa chave de API do escopo de verificar expira em um dia ou na primeira utilização, o que ocorrer primeiro.

#### <a name="response"></a>Resposta

Código de status | Significado
----------- | -------
200         | A chave de API é válida
403         | A chave de API é inválida ou não autorizado a enviar por push contra o pacote
404         | O pacote referenciado pela `ID` e `VERSION` (opcional) não existe
