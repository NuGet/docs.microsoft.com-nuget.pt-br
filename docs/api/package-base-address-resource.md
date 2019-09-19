---
title: Conteúdo do pacote, API do NuGet
description: O endereço base do pacote é uma interface simples para buscar o pacote em si.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 7aea28d6224a89149aa33be035c82a45db3058f0
ms.sourcegitcommit: 1eda83ab537c86cc27316e7bc67f95a358766e63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/18/2019
ms.locfileid: "71094122"
---
# <a name="package-content"></a>Conteúdo do pacote

É possível gerar uma URL para buscar o conteúdo de um pacote arbitrário (o arquivo. nupkg) usando a API v3. O recurso usado para buscar o conteúdo do pacote é `PackageBaseAddress` o recurso encontrado no [índice de serviço](service-index.md). Esse recurso também habilita a descoberta de todas as versões de um pacote, listadas ou não listadas.

Esse recurso é comumente conhecido como "endereço base do pacote" ou como "contêiner simples".

## <a name="versioning"></a>Controle de versão

O seguinte `@type` valor é usado:

Valor @type              | Observações
------------------------ | -----
PackageBaseAddress/3.0.0 | A versão inicial

## <a name="base-url"></a>URL Base

A URL base para as APIs a seguir é o valor da `@id` propriedade associada ao valor de recurso `@type` mencionado anteriormente. No documento a seguir, a URL `{@id}` base do espaço reservado será usada.

## <a name="http-methods"></a>Métodos HTTP

Todas as URLs encontradas no recurso de registro dão suporte aos `GET` métodos `HEAD`http e.

## <a name="enumerate-package-versions"></a>Enumerar versões de pacote

Se o cliente souber uma ID de pacote e quiser descobrir quais versões de pacote a origem do pacote está disponível, o cliente poderá construir uma URL previsível para enumerar todas as versões do pacote. Esta lista deve ser uma "listagem de diretório" para a API de conteúdo do pacote mencionada abaixo.

> [!Note]
> Essa lista contém as versões de pacote listadas e não listadas.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parâmetros de solicitação

Nome     | No     | Tipo    | Necessária | Observações
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | cadeia de caracteres  | sim      | A ID do pacote, em letras minúsculas

O `LOWER_ID` valor é a ID de pacote desejada com letras minúsculas usando as regras implementadas pelo. [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Método net.

### <a name="response"></a>Resposta

Se a origem do pacote não tiver nenhuma versão da ID de pacote fornecida, um código de status 404 será retornado.

Se a origem do pacote tiver uma ou mais versões, um código de status 200 será retornado. O corpo da resposta é um objeto JSON com a seguinte propriedade:

Nome     | Tipo             | Necessária | Observações
-------- | ---------------- | -------- | -----
versões | Matriz de cadeias de caracteres | sim      | As versões disponíveis

As cadeias de `versions` caracteres na matriz são todas as [cadeias de caracteres de versão do NuGet normalizadas](../concepts/package-versioning.md#normalized-version-numbers)e em letras minúsculas. As cadeias de caracteres de versão não contêm nenhum metadado de compilação SemVer 2.0.0.

A intenção é que as cadeias de caracteres de versão encontradas nessa matriz possam ser usadas `LOWER_VERSION` em textual para os tokens encontrados nos pontos de extremidade a seguir.

### <a name="sample-request"></a>Exemplo de solicitação

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>Exemplo de resposta

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>Baixar conteúdo do pacote (. nupkg)

Se o cliente souber uma ID e uma versão do pacote e quiser baixar o conteúdo do pacote, ele só precisará construir a seguinte URL:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>Parâmetros de solicitação

Nome          | No     | Tipo   | Necessária | Observações
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | cadeia de caracteres | sim      | A ID do pacote, em minúsculas
LOWER_VERSION | URL    | cadeia de caracteres | sim      | A versão do pacote, normalizada e minúscula

Ambos `LOWER_ID` e `LOWER_VERSION` estão em letras minúsculas usando as regras implementadas pelo. Da rede[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)
método.

O `LOWER_VERSION` é a versão de pacote desejada normalizada usando [as regras de normalização](../concepts/package-versioning.md#normalized-version-numbers)de versão do NuGet. Isso significa que os metadados de compilação permitidos pela especificação SemVer 2.0.0 devem ser excluídos nesse caso.

### <a name="response-body"></a>Corpo da resposta

Se o pacote existir na origem do pacote, um código de status 200 será retornado. O corpo da resposta será o próprio conteúdo do pacote.

Se o pacote não existir na origem do pacote, um código de status 404 será retornado.

### <a name="sample-request"></a>Exemplo de solicitação

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>Exemplo de resposta

O fluxo binário que é o. nupkg para Newtonsoft. JSON 9.0.1.

## <a name="download-package-manifest-nuspec"></a>Baixar o manifesto do pacote (. nuspec)

Se o cliente souber uma ID e uma versão do pacote e quiser baixar o manifesto do pacote, ele só precisará construir a seguinte URL:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>Parâmetros de solicitação

Nome          | No     | Tipo   | Necessária | Observações
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | cadeia de caracteres | sim      | A ID do pacote, em minúsculas
LOWER_VERSION | URL    | cadeia de caracteres | sim      | A versão do pacote, normalizada e minúscula

Ambos `LOWER_ID` e `LOWER_VERSION` estão em letras minúsculas usando as regras implementadas pelo. [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Método net.

O `LOWER_VERSION` é a versão de pacote desejada normalizada usando [as regras de normalização](../concepts/package-versioning.md#normalized-version-numbers)de versão do NuGet. Isso significa que os metadados de compilação permitidos pela especificação SemVer 2.0.0 devem ser excluídos nesse caso.

### <a name="response-body"></a>Corpo da resposta

Se o pacote existir na origem do pacote, um código de status 200 será retornado. O corpo da resposta será o manifesto do pacote, que é o. nuspec contido no. nupkg correspondente. O. nuspec é um documento XML.

Se o pacote não existir na origem do pacote, um código de status 404 será retornado.

### <a name="sample-request"></a>Exemplo de solicitação

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>Exemplo de resposta

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
