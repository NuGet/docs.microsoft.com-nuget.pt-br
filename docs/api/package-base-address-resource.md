---
title: Conteúdo do pacote, API do NuGet
description: O endereço base do pacote é uma interface simple para buscar o pacote propriamente dito.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 740defc34077793b81fb35db73a2eee393ae3bac
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547148"
---
# <a name="package-content"></a>Conteúdo do pacote

É possível gerar uma URL para buscar o conteúdo de um pacote arbitrários (o arquivo. nupkg) usando a API V3. O recurso usado para buscar o conteúdo do pacote é o `PackageBaseAddress` recurso encontrado na [índice de serviço](service-index.md). Esse recurso também permite a descoberta de todas as versões de um pacote, listados ou não listado.

Esse recurso é conhecido como o o "pacote endereço básico" ou "contêiner simples".

## <a name="versioning"></a>Controle de versão

O seguinte `@type` valor é usado:

Valor @type              | Observações
------------------------ | -----
PackageBaseAddress/3.0.0 | A versão inicial

## <a name="base-url"></a>URL Base

A URL base para as APIs a seguir é o valor da `@id` propriedade associada ao recurso mencionados anteriormente `@type` valor. O seguinte documento, o espaço reservado de URL de base `{@id}` será usado.

## <a name="http-methods"></a>Métodos HTTP

Todas as URLs encontradas no suporte a recursos de registro os métodos HTTP `GET` e `HEAD`.

## <a name="enumerate-package-versions"></a>Enumerar as versões do pacote

Se o cliente sabe que uma ID de pacote e quer descobrir quais versões do pacote o pacote de origem tem disponível, o cliente pode construir uma URL previsível para enumerar todas as versões do pacote. Essa lista deve ser uma "listagem de diretório" para a API de conteúdo do pacote mencionada a seguir.

> [!Note]
> Esta lista contém ambas as versões de pacote listadas e removido da lista.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parâmetros de solicitação

Nome     | No     | Tipo    | Necessária | Observações
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | cadeia de caracteres  | sim      | A ID do pacote, em minúsculas

O `LOWER_ID` valor é a ID do pacote desejado em minúscula usando as regras implementadas pelo. Do NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.

### <a name="response"></a>Resposta

Se a origem do pacote não tiver nenhuma versão da ID do pacote fornecido, um código de 404 status será retornado.

Se a origem do pacote tem uma ou mais versões, um código de 200 status será retornado. O corpo da resposta é um objeto JSON com a seguinte propriedade:

Nome     | Tipo             | Necessária | Observações
-------- | ---------------- | -------- | -----
versões | matriz de cadeias de caracteres | sim      | O pacote IDs disponíveis

Cadeias de caracteres a `versions` matriz estão todos em minúscula, [normalizados cadeias de caracteres de versão NuGet](../reference/package-versioning.md#normalized-version-numbers). As cadeias de caracteres de versão contém os metadados de compilação de SemVer 2.0.0.

A intenção é que as cadeias de caracteres de versão encontradas nesta matriz podem ser usadas textual para o `LOWER_VERSION` tokens encontrados nos seguintes pontos de extremidade.

### <a name="sample-request"></a>Exemplo de solicitação

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>Baixar conteúdo do pacote (. nupkg)

Se o cliente sabe que uma ID de pacote e a versão e quiser baixar o conteúdo do pacote, precisará apenas construir a URL a seguir:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>Parâmetros de solicitação

Nome          | No     | Tipo   | Necessária | Observações
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | cadeia de caracteres | sim      | A ID do pacote, em minúsculas
LOWER_VERSION | URL    | cadeia de caracteres | sim      | A versão do pacote, normalizado e em minúscula

Ambos `LOWER_ID` e `LOWER_VERSION` em minúscula usando as regras implementadas pelo. Do NET [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)
método.

O `LOWER_VERSION` é a versão do pacote desejado normalizada usando a versão do NuGet [regras de normalização](../reference/package-versioning.md#normalized-version-numbers). Isso significa que os metadados compilação que é permitido pela especificação de SemVer 2.0.0 devem ser excluídos nesse caso.

### <a name="response-body"></a>Corpo da resposta

Se o pacote existe na origem do pacote, um código de 200 status será retornado. O corpo da resposta será o conteúdo do pacote.

Se o pacote não existe na origem do pacote, um código de 404 status será retornado.

### <a name="sample-request"></a>Exemplo de solicitação

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>Resposta de exemplo

O fluxo binário que é o. nupkg para newtonsoft. JSON 9.0.1.

## <a name="download-package-manifest-nuspec"></a>Baixe o manifesto do pacote (. NuSpec)

Se o cliente sabe que uma ID de pacote e a versão e quiser baixar o manifesto do pacote, precisará apenas construir a URL a seguir:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>Parâmetros de solicitação

Nome          | No     | Tipo    | Necessária | Observações
------------- | ------ | ------- | -------- | -----
LOWER_ID      | URL    | cadeia de caracteres  | sim      | A ID do pacote, em minúsculas
LOWER_VERSION | URL    | inteiro | sim      | A versão do pacote, normalizado e em minúscula

Ambos `LOWER_ID` e `LOWER_VERSION` em minúscula usando as regras implementadas pelo. Do NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.

O `LOWER_VERSION` é a versão do pacote desejado normalizada usando a versão do NuGet [regras de normalização](../reference/package-versioning.md#normalized-version-numbers). Isso significa que os metadados compilação que é permitido pela especificação de SemVer 2.0.0 devem ser excluídos nesse caso.

### <a name="response-body"></a>Corpo da resposta

Se o pacote existe na origem do pacote, um código de 200 status será retornado. O corpo da resposta será o manifesto de pacote, que é o. NuSpec contidos no. nupkg correspondente. O. NuSpec é um documento XML.

Se o pacote não existe na origem do pacote, um código de 404 status será retornado.

### <a name="sample-request"></a>Exemplo de solicitação

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>Resposta de exemplo

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
