---
title: Enviar por push pacotes de símbolos, API do NuGet | Microsoft Docs
author:
- cristinamanum
- kraigb
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: O serviço de publicação permite que os clientes publicar novos pacotes de símbolo.
keywords: Pacote de símbolos de envio por push de API do NuGet
ms.reviewer: karann
ms.openlocfilehash: 514ab3683db81da5b2220b005b8b39f1fec8300d
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580409"
---
# <a name="push-symbol-packages"></a>Pacotes de símbolos por push

É possível aos pacotes de símbolos por push ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) usando a API do NuGet V3.
Essas operações são baseadas fora do `SymbolPackagePublish` recurso encontrado na [índice de serviço](service-index.md).

## <a name="versioning"></a>Controle de versão

O seguinte `@type` valor é usado:

Valor @type                 | Observações
--------------------        | -----
SymbolPackagePublish/4.9.0  | A versão inicial

## <a name="base-url"></a>URL Base

A URL base para as APIs a seguir é o valor da `@id` propriedade do `SymbolPackagePublish/4.9.0` recurso na origem do pacote [índice de serviço](service-index.md). Para obter a documentação abaixo, a URL do nuget.org é usado. Considere `https://www.nuget.org/api/v2/symbolpackage` como um espaço reservado para o `@id` valor encontrado no índice de serviço.

## <a name="http-methods"></a>Métodos HTTP

O `PUT` método HTTP tem suporte por esse recurso. 

## <a name="push-a-symbol-package"></a>Enviar por push a um pacote de símbolos

NuGet.org dá suporte ao novo formato enviar por push de pacotes de símbolo ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) usando a API a seguir. 

    PUT https://www.nuget.org/api/v2/symbolpackage

Pacotes de símbolo com a mesma ID e versão podem ser enviados várias vezes. Um pacote de símbolos será rejeitado nos seguintes casos.
- Não existe um pacote com o mesmo ID e versão.
- Um pacote de símbolos com a mesma ID e versão foi enviado por push, mas ainda não foi publicado.
- O pacote de símbolos ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) é inválido (consulte [restrições de pacote de símbolos](../create-packages/Symbol-Packages-snupkg.md)).

### <a name="request-parameters"></a>Parâmetros de solicitação

Nome           | No     | Tipo   | Necessária | Observações
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Cabeçalho | cadeia de caracteres | sim      | Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`

A chave de API é uma cadeia de caracteres opaca obtidos de origem do pacote pelo usuário e configurado no cliente. Nenhum formato de cadeia de caracteres específica é obrigatória, mas o comprimento da chave de API não deve exceder um tamanho razoável para valores de cabeçalho HTTP.

### <a name="request-body"></a>Corpo da solicitação

O corpo da solicitação para o envio por push do símbolo é o mesmo que com o corpo de solicitação de uma solicitação de envio do pacote (consulte [de pacote por push e excluir](package-publish-resource.md)). 

### <a name="response"></a>Resposta

Código de status | Significado
----------- | -------
201         | O pacote de símbolos foi enviado com êxito.
400         | O pacote de símbolos fornecido é inválido.
401         | O usuário não está autorizado para executar esta ação.
404         | Um pacote correspondente com a ID e a versão fornecida não existe.
409         | Um pacote de símbolos com a ID e a versão fornecida foi enviado por push, mas ele ainda não está disponível.
413         | O pacote é muito grande.

