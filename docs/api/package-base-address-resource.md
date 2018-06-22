---
title: Conteúdo do pacote, o NuGet API
description: O endereço base do pacote é uma interface simples para buscar o pacote propriamente dito.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: a6ac40368f30d33f35d4ca0b6cc18ce4bd6efee5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819171"
---
# <a name="package-content"></a>Conteúdo do pacote

É possível gerar uma URL para buscar o conteúdo de um pacote arbitrário (o arquivo. nupkg) usando a API V3. O recurso usado para buscar o conteúdo do pacote é o `PackageBaseAddress` recurso encontrado na [índice de serviço](service-index.md). Esse recurso também permite a descoberta de todas as versões de um pacote, listados ou não listadas.

Este recurso é conhecido como um "pacote base endereço" ou "contêiner simples".

## <a name="versioning"></a>Controle de versão

O seguinte `@type` valor é usado:

Valor @type              | Observações
------------------------ | -----
PackageBaseAddress/3.0.0 | A versão inicial

## <a name="base-url"></a>URL Base

A URL base para as seguintes APIs é o valor da `@id` propriedade associada com o recurso mencionados acima `@type` valor. No documento a seguir, a URL base do espaço reservado `{@id}` será usado.

## <a name="http-methods"></a>Métodos HTTP

Todas as URLs encontradas no suporte a recurso de registro os métodos HTTP `GET` e `HEAD`.

## <a name="enumerate-package-versions"></a>Enumerar as versões do pacote

Se o cliente sabe uma ID de pacote e quer descobrir quais versões do pacote do pacote de origem tem disponível, o cliente pode construir uma URL previsível para enumerar todas as versões do pacote. Essa lista deve ser uma "listagem de diretório" para a API de conteúdo do pacote mencionada abaixo.

> [!Note]
> Essa lista contém as duas versões do pacote listados e não listados.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parâmetros de solicitação

Nome     | No     | Tipo    | Necessária | Observações
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | cadeia de caracteres  | sim      | A ID do pacote, letras minúsculas

O `LOWER_ID` valor é a ID do pacote desejado em minúscula usando as regras implementadas pelo. Do NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.

### <a name="response"></a>Resposta

Se a origem do pacote não tem nenhuma versão da ID do pacote fornecido, um código de 404 status será retornado.

Se a origem do pacote tem uma ou mais versões, um código de 200 status será retornado. O corpo da resposta é um objeto JSON com a seguinte propriedade:

Nome     | Tipo             | Necessária | Observações
-------- | ---------------- | -------- | -----
versões | Matriz de cadeias de caracteres | sim      | O pacote IDs disponíveis

As cadeias de caracteres no `versions` matriz estão todos em minúscula, [normalizado cadeias de caracteres de versão NuGet](../reference/package-versioning.md#normalized-version-numbers). As cadeias de caracteres de versão não contém metadados de compilação SemVer 2.0.0.

A intenção é que as cadeias de caracteres de versão encontradas nesta matriz podem ser usadas textualmente para o `LOWER_VERSION` tokens encontrado nos seguintes pontos de extremidade.

### <a name="sample-request"></a>Solicitação de amostra

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>Baixar o conteúdo do pacote (. nupkg)

Se o cliente sabe um ID de pacote e a versão e deseja baixar o conteúdo do pacote, eles só precisam construir a URL a seguir:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>Parâmetros de solicitação

Nome          | No     | Tipo   | Necessária | Observações
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | cadeia de caracteres | sim      | A ID do pacote, letras minúsculas
LOWER_VERSION | URL    | cadeia de caracteres | sim      | A versão do pacote, padronizado e minúscula

Ambos `LOWER_ID` e `LOWER_VERSION` em minúscula usando as regras implementadas pelo. Do NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.

O `LOWER_VERSION` é a versão do pacote desejado normalizado de acordo com a versão do NuGet [as regras de normalização](../reference/package-versioning.md#normalized-version-numbers). Isso significa que os metadados de compilação que é permitido pela especificação SemVer 2.0.0 devem ser excluídos nesse caso.

### <a name="response-body"></a>Corpo da resposta

Se o pacote existe na origem do pacote, um código de 200 status será retornado. O corpo da resposta será o conteúdo do pacote.

Se o pacote não existe na origem do pacote, um código de 404 status será retornado.

### <a name="sample-request"></a>Solicitação de amostra

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>Resposta de exemplo

O fluxo binário é nupkg para newtonsoft 9.0.1.

## <a name="download-package-manifest-nuspec"></a>Baixe o manifesto de pacote (. NuSpec)

Se o cliente sabe um ID de pacote e a versão e deseja baixar o manifesto de pacote, eles só precisam construir a URL a seguir:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>Parâmetros de solicitação

Nome          | No     | Tipo    | Necessária | Observações
------------- | ------ | ------- | -------- | -----
LOWER_ID      | URL    | cadeia de caracteres  | sim      | A ID do pacote, letras minúsculas
LOWER_VERSION | URL    | inteiro | sim      | A versão do pacote, padronizado e minúscula

Ambos `LOWER_ID` e `LOWER_VERSION` em minúscula usando as regras implementadas pelo. Do NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.

O `LOWER_VERSION` é a versão do pacote desejado normalizado de acordo com a versão do NuGet [as regras de normalização](../reference/package-versioning.md#normalized-version-numbers). Isso significa que os metadados de compilação que é permitido pela especificação SemVer 2.0.0 devem ser excluídos nesse caso.

### <a name="response-body"></a>Corpo da resposta

Se o pacote existe na origem do pacote, um código de 200 status será retornado. O corpo da resposta será o manifesto de pacote, que é o. NuSpec contidas o nupkg correspondente. A. NuSpec é um documento XML.

Se o pacote não existe na origem do pacote, um código de 404 status será retornado.

### <a name="sample-request"></a>Solicitação de amostra

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>Resposta de exemplo

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
