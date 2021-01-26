---
title: Modelo de URL de detalhes do pacote, API do NuGet
description: O modelo de URL de detalhes do pacote permite que os clientes exibam em sua interface do usuário um link da Web para mais detalhes do pacote
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: aaeedea9750c11099b34e927bd8442656839d784
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773947"
---
# <a name="package-details-url-template"></a>Modelo de URL de detalhes do pacote

É possível que um cliente crie uma URL que possa ser usada pelo usuário para ver mais detalhes do pacote em seu navegador da Web. Isso é útil quando uma origem de pacote deseja mostrar informações adicionais sobre um pacote que talvez não caibam no escopo do que o aplicativo cliente NuGet mostra.

O recurso usado para criar essa URL é o `PackageDetailsUriTemplate` recurso encontrado no [índice de serviço](service-index.md).

## <a name="versioning"></a>Controle de versão

Os seguintes `@type` valores são usados:

@type valor                     | Observações
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | A versão inicial

## <a name="url-template"></a>Modelo do URL

A URL para a API a seguir é o valor da `@id` propriedade associada a um dos valores de recurso mencionados anteriormente `@type` .

## <a name="http-methods"></a>Métodos HTTP

Embora o cliente não se destine a fazer solicitações para a URL de detalhes do pacote em nome do usuário, a página da Web deve dar suporte ao `GET` método para permitir que uma URL clicada seja aberta facilmente em um navegador da Web.

## <a name="construct-the-url"></a>Construir a URL

Dada uma ID de pacote e versão conhecidas, a implementação do cliente pode construir uma URL usada para acessar uma interface da Web. A implementação do cliente deve exibir essa URL construída (ou link clicável) para o usuário, permitindo que ele abra um navegador da Web para a URL e saiba mais sobre o pacote. O conteúdo da página de detalhes do pacote é determinado pela implementação do servidor.

A URL deve ser uma URL absoluta e o esquema (protocolo) deve ser HTTPS.

O valor de `@id` no índice de serviço é uma cadeia de caracteres de URL que contém qualquer um dos seguintes tokens de espaço reservado:

### <a name="url-placeholders"></a>Espaços reservados de URL

Nome        | Type    | Necessária | Observações
----------- | ------- | -------- | -----
`{id}`      | string  | não       | A ID do pacote para obter detalhes
`{version}` | string  | não       | A versão do pacote para obter detalhes

O servidor deve aceitar `{id}` e `{version}` valores com maiúsculas e minúsculas. Além disso, o servidor não deve ser sensível a se a versão é [normalizada](../concepts/package-versioning.md#normalized-version-numbers). Em outras palavras, o servidor também deve aceitar versões não normalizadas.

Por exemplo, o modelo de detalhes do pacote NuGet. org tem esta aparência:

```http
https://www.nuget.org/packages/{id}/{version}
```

Se a implementação do cliente precisar exibir um link para os detalhes do pacote para NuGet. Versioning 4.3.0, ele produzirá a seguinte URL e a forneceria ao usuário:

```http
https://www.nuget.org/packages/NuGet.Versioning/4.3.0
```
