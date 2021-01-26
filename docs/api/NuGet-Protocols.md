---
title: Protocolos nuget.org
description: Os protocolos de nuget.org em evolução para interagir com clientes NuGet.
author: anangaur
ms.author: anangaur
ms.date: 01/21/2021
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: ea072484c896c4862e47b2c03a1b177f196b0aad
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773978"
---
# <a name="nugetorg-protocols"></a>Protocolos nuget.org

Para interagir com o nuget.org, os clientes precisam seguir determinados protocolos. Como esses protocolos continuam em evolução, os clientes devem identificar a versão do protocolo que usam ao chamar APIs nuget.org específicas. Isso permite que o nuget.org introduza alterações de forma não-significativa para os clientes antigos.

> [!Note]
> As APIs documentadas nesta página são específicas do nuget.org e não há nenhuma expectativa para que outras implementações do servidor NuGet introduzam essas APIs. 

Para obter informações sobre a API do NuGet implementada amplamente no ecossistema do NuGet, consulte a [visão geral da API](overview.md).

Este tópico lista vários protocolos como e quando eles chegam à existência.

## <a name="nuget-protocol-version-410"></a>Versão do protocolo NuGet 4.1.0

O protocolo 4.1.0 especifica o uso de chaves de escopo de verificação para interagir com serviços diferentes de nuget.org, para validar um pacote em uma conta nuget.org. Observe que o `4.1.0` número de versão é uma cadeia de caracteres opaca, mas que ocorre coincidir com a primeira versão do cliente do NuGet oficial que tem suporte para esse protocolo.

A validação garante que as chaves de API criadas pelo usuário sejam usadas somente com nuget.org, e que outra verificação ou validação de um serviço de terceiros seja manipulada por meio de uma única utilização de chaves de escopo de verificação. Essas chaves de escopo de verificação podem ser usadas para validar que o pacote pertence a um usuário específico (conta) em nuget.org.

### <a name="client-requirement"></a>Requisito do cliente

Os clientes são obrigados a passar o seguinte cabeçalho quando fazem chamadas à API para **enviar pacotes por push** para NuGet.org:

```
X-NuGet-Protocol-Version: 4.1.0
```

Observe que o `X-NuGet-Client-Version` cabeçalho tem semântica semelhante, mas é reservado para ser usado apenas pelo cliente oficial do NuGet. Clientes de terceiros devem usar o `X-NuGet-Protocol-Version` cabeçalho e o valor.

O próprio protocolo de **Push** é descrito na documentação do [ `PackagePublish` recurso](package-publish-resource.md).

Se um cliente interage com serviços externos e precisa validar se um pacote pertence a um usuário específico (conta), ele deve usar o seguinte protocolo e usar as chaves de escopo de verificação e não as chaves de API de nuget.org.

### <a name="api-to-request-a-verify-scope-key"></a>API para solicitar uma chave de verificação de escopo

Essa API é usada para obter uma chave de escopo de verificação para um autor de nuget.org para validar um pacote de propriedade dele.

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>Parâmetros da solicitação

Nome           | Em     | Type   | Necessária | Observações
-------------- | ------ | ------ | -------- | -----
ID             | URL    | string | sim      | O pacote identidier para o qual a chave de verificação de escopo é solicitada
VERSION        | URL    | string | não       | A versão do pacote
X-NuGet-ApiKey | Cabeçalho | string | sim      | Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`

#### <a name="response"></a>Resposta

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>API para verificar a chave de verificação de escopo

Essa API é usada para validar uma chave de escopo de verificação para o pacote de Propriedade do autor do nuget.org.

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>Parâmetros da solicitação

Nome           | Em     | Type   | Necessária | Observações
-------------  | ------ | ------ | -------- | -----
ID             | URL    | string | sim      | O identificador de pacote para o qual a chave de verificação de escopo é solicitada
VERSION        | URL    | string | não       | A versão do pacote
X-NuGet-ApiKey | Cabeçalho | string | sim      | Por exemplo, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`

> [!Note]
> Essa chave verificar API de escopo expira no horário de um dia ou no primeiro uso, o que ocorrer primeiro.

#### <a name="response"></a>Resposta

Código de status | Significado
----------- | -------
200         | A chave de API é válida
403         | A chave de API é inválida ou não está autorizada a enviar por push para o pacote
404         | O pacote referido por `ID` e `VERSION` (opcional) não existe
