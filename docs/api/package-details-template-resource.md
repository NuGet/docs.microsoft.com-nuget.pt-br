---
title: Modelo de URL de detalhes do pacote, API do NuGet
description: O modelo de URL de detalhes do pacote permite que os clientes exibir em sua interface do usuário que um link da web para obter mais detalhes do pacote
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c01fd35c5d96c44279c9d0254f89d8b1b9fe59d8
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638066"
---
# <a name="package-details-url-template"></a>Modelo de URL de detalhes do pacote

É possível que um cliente para criar uma URL que pode ser usada pelo usuário para ver mais detalhes do pacote em seu navegador da web. Isso é útil quando uma origem de pacote que deseja mostrar informações adicionais sobre um pacote que não se encaixam dentro do escopo do que mostra o aplicativo de cliente do NuGet.

O recurso usado para criar essa URL é o `PackageDetailsUriTemplate` recurso encontrado na [índice de serviço](service-index.md).

## <a name="versioning"></a>Controle de versão

O seguinte `@type` valores são usados:

Valor @type                     | Observações
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | A versão inicial

## <a name="url-template"></a>Modelo de URL

A URL para a seguinte API é o valor da `@id` propriedade associada a um do recurso mencionados anteriormente `@type` valores.

## <a name="http-methods"></a>Métodos HTTP

Embora o cliente não se destina para fazer solicitações para a URL de detalhes do pacote em nome do usuário, a página da web deve oferecer suporte a `GET` método para permitir que uma URL clicada ser aberto facilmente em um navegador da web.

## <a name="construct-the-url"></a>Construir a URL

Dada uma ID do pacote conhecidos e versão, a implementação do cliente pode construir uma URL usada para acessar uma interface da web. A implementação do cliente deve exibir esse URL construída (ou um link clicável) para o usuário, permitindo que eles para abrir um navegador da web para a URL e para saber mais sobre o pacote. O conteúdo da página de detalhes do pacote é determinado pela implementação do servidor.

A URL deve ser uma URL absoluta e o esquema (protocol) deve ser HTTPS.

O valor da `@id` no serviço de índice é uma cadeia de caracteres de URL que contém qualquer um dos seguintes tokens de espaço reservado:

### <a name="url-placeholders"></a>Espaços reservados de URL

Nome        | Tipo    | Necessária | Observações
----------- | ------- | -------- | -----
`{id}`      | cadeia de caracteres  | no       | Para obter detalhes para a ID do pacote
`{version}` | cadeia de caracteres  | no       | Para obter detalhes para a versão do pacote

O servidor deve aceitar `{id}` e `{version}` valores com qualquer uso de maiusculas e minúsculas. Além disso, o servidor não deve ser sensível a se a versão está [normalizado](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers). Em outras palavras, o servidor deve aceitar também aceitam versões não normalizado.

Por exemplo, o modelo de detalhes do pacote do nuget.org fica assim:

    https://www.nuget.org/packages/{id}/{version}

Se a implementação do cliente precisar exibir um link para os detalhes do pacote para NuGet.Versioning 4.3.0, ele seria produzem a seguinte URL e fornecê-la ao usuário:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
