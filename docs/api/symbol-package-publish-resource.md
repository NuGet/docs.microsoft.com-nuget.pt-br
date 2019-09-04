---
title: Pacotes de símbolo de push, API do NuGet | Microsoft Docs
author: cristinamanum
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: O serviço de publicação permite que os clientes publiquem novos pacotes de símbolo.
keywords: Pacote de símbolos de push da API do NuGet
ms.reviewer: karann
ms.openlocfilehash: 27e557bf15ce31152243a409eddc4112eeb6c38b
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/03/2019
ms.locfileid: "70235113"
---
# <a name="push-symbol-packages"></a>Pacotes de símbolo de push

É possível enviar por push os pacotes de símbolos ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) usando a API do NuGet v3.
Essas operações são baseadas `SymbolPackagePublish` no recurso encontrado no índice de [serviço](service-index.md).

## <a name="versioning"></a>Controle de versão

O seguinte `@type` valor é usado:

Valor @type                 | Observações
--------------------        | -----
SymbolPackagePublish/4.9.0  | A versão inicial

## <a name="base-url"></a>URL Base

A URL base para as APIs a seguir é o valor da `@id` propriedade `SymbolPackagePublish/4.9.0` do recurso no [índice de serviço](service-index.md)da origem do pacote. Para a documentação abaixo, a URL do NuGet. org é usada. Considere `https://www.nuget.org/api/v2/symbolpackage` como um espaço reservado para `@id` o valor encontrado no índice de serviço.

## <a name="http-methods"></a>Métodos HTTP

Este `PUT` recurso dá suporte ao método http. 

## <a name="push-a-symbol-package"></a>Enviar por push um pacote de símbolos

o nuget.org dá suporte ao envio de novo formato de pacotes de símbolo ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) usando a API a seguir. 

    PUT https://www.nuget.org/api/v2/symbolpackage

Pacotes de símbolos com a mesma ID e versão podem ser enviados várias vezes. Um pacote de símbolos será rejeitado nos casos a seguir.
- Não existe um pacote com a mesma ID e versão.
- Um pacote de símbolos com a mesma ID e versão foi enviado por push, mas ainda não foi publicado.
- O pacote de símbolos ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) é inválido (consulte [restrições de pacote de símbolo](../create-packages/Symbol-Packages-snupkg.md)).

### <a name="request-parameters"></a>Parâmetros de solicitação

Nome           | No     | Tipo   | Necessária | Observações
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Cabeçalho | cadeia de caracteres | sim      | Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`

A chave de API é uma cadeia de caracteres opaca proveniente da origem do pacote pelo usuário e configurada no cliente. Nenhum formato de cadeia de caracteres específico é obrigatório, mas o comprimento da chave de API não deve exceder um tamanho razoável para valores de cabeçalho HTTP.

### <a name="request-body"></a>Corpo da solicitação

O corpo da solicitação para o símbolo Push é o mesmo que com o corpo da solicitação de uma solicitação de push de pacote (consulte [push e Delete do pacote](package-publish-resource.md)). 

### <a name="response"></a>Resposta

Código de status | Significado
----------- | -------
201         | O pacote de símbolos foi enviado por push com êxito.
400         | O pacote de símbolos fornecido é inválido.
401         | O usuário não está autorizado a executar esta ação.
404         | Não existe um pacote correspondente com a ID e a versão fornecidas.
409         | Um pacote de símbolos com a ID e a versão fornecidas foi enviado por push, mas ainda não está disponível.
413         | O pacote é muito grande.

