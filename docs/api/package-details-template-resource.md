---
title: Modelo de URL de detalhes do pacote, API do NuGet
description: O modelo de URL de detalhes do pacote permite que os clientes exibam em sua interface do usuário um link da Web para mais detalhes do pacote
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 1b84c6e88a56216e5747d5bc602219af6695c305
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76812929"
---
# <a name="package-details-url-template"></a>Modelo de URL de detalhes do pacote

É possível que um cliente crie uma URL que possa ser usada pelo usuário para ver mais detalhes do pacote em seu navegador da Web. Isso é útil quando uma origem de pacote deseja mostrar informações adicionais sobre um pacote que talvez não caibam no escopo do que o aplicativo cliente NuGet mostra.

O recurso usado para criar essa URL é o `PackageDetailsUriTemplate` recurso encontrado no [índice de serviço](service-index.md).

## <a name="versioning"></a>{1&gt;Controle de versão&lt;1}

Os seguintes valores de `@type` são usados:

Valor @type                     | {1&gt;Observações&lt;1}
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | A versão inicial

## <a name="url-template"></a>Modelo de URL

A URL para a API a seguir é o valor da propriedade `@id` associada a um dos valores de `@type` de recursos mencionados anteriormente.

## <a name="http-methods"></a>Métodos HTTP

Embora o cliente não se destine a fazer solicitações para a URL de detalhes do pacote em nome do usuário, a página da Web deve dar suporte ao método `GET` para permitir que uma URL clicada seja aberta facilmente em um navegador da Web.

## <a name="construct-the-url"></a>Construir a URL

Dada uma ID de pacote e versão conhecidas, a implementação do cliente pode construir uma URL usada para acessar uma interface da Web. A implementação do cliente deve exibir essa URL construída (ou link clicável) para o usuário, permitindo que ele abra um navegador da Web para a URL e saiba mais sobre o pacote. O conteúdo da página de detalhes do pacote é determinado pela implementação do servidor.

A URL deve ser uma URL absoluta e o esquema (protocolo) deve ser HTTPS.

O valor do `@id` no índice de serviço é uma cadeia de caracteres de URL que contém qualquer um dos seguintes tokens de espaço reservado:

### <a name="url-placeholders"></a>Espaços reservados de URL

Name        | {1&gt;Tipo&lt;1}    | Necessário | {1&gt;Observações&lt;1}
----------- | ------- | -------- | -----
`{id}`      | cadeia de caracteres  | no       | A ID do pacote para obter detalhes
`{version}` | cadeia de caracteres  | no       | A versão do pacote para obter detalhes

O servidor deve aceitar `{id}` e `{version}` valores com maiúsculas e minúsculas. Além disso, o servidor não deve ser sensível a se a versão é [normalizada](../concepts/package-versioning.md#normalized-version-numbers). Em outras palavras, o servidor também deve aceitar versões não normalizadas.

Por exemplo, o modelo de detalhes do pacote NuGet. org tem esta aparência:

    https://www.nuget.org/packages/{id}/{version}

Se a implementação do cliente precisar exibir um link para os detalhes do pacote para NuGet. Versioning 4.3.0, ele produzirá a seguinte URL e a forneceria ao usuário:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
