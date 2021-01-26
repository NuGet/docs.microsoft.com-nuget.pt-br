---
title: Relatar o modelo de URL de abuso, API do NuGet
description: O modelo de URL do relatório de abuso permite que os clientes exibam um link de abuso de relatório em sua interface do usuário.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b36058c9c841e2cca6eb61121ada8275f1525a8f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775232"
---
# <a name="report-abuse-url-template"></a>Relatar o modelo de URL de abuso

É possível que um cliente crie uma URL que possa ser usada pelo usuário para relatar abusos sobre um pacote específico. Isso é útil quando uma origem de pacote deseja habilitar todas as experiências do cliente (mesmo de terceiros) para delegar relatórios de abuso à origem do pacote.

O recurso usado para criar essa URL é o `ReportAbuseUriTemplate` recurso encontrado no [índice de serviço](service-index.md).

## <a name="versioning"></a>Controle de versão

Os seguintes `@type` valores são usados:

@type valor                       | Observações
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | A versão inicial
ReportAbuseUriTemplate/3.0.0-RC   | Alias de `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>Modelo do URL

A URL para a API a seguir é o valor da `@id` propriedade associada a um dos valores de recurso mencionados anteriormente `@type` .

## <a name="http-methods"></a>Métodos HTTP

Embora o cliente não se destine a fazer solicitações para a URL de abuso de relatório em nome do usuário, a página da Web deve dar suporte ao `GET` método para permitir que uma URL clicada seja aberta facilmente em um navegador da Web.

## <a name="construct-the-url"></a>Construir a URL

Dada uma ID de pacote e versão conhecidas, a implementação do cliente pode construir uma URL usada para acessar uma interface da Web. A implementação do cliente deve exibir essa URL construída (ou link clicável) para o usuário, permitindo que ele abra um navegador da Web para a URL e faça qualquer relatório de abuso necessário. A implementação do formulário de relatório de abuso é determinada pela implementação do servidor.

O valor de `@id` é uma cadeia de caracteres de URL que contém qualquer um dos seguintes tokens de espaço reservado:

### <a name="url-placeholders"></a>Espaços reservados de URL

Nome        | Type    | Necessária | Observações
----------- | ------- | -------- | -----
`{id}`      | string  | não       | A ID do pacote para relatar abuso
`{version}` | string  | não       | A versão do pacote para relatar abuso

Os `{id}` `{version}` valores e interpretados pela implementação do servidor devem diferenciar maiúsculas de minúsculas e não diferenciar se a versão for normalizada.

Por exemplo, o modelo de abuso de relatório do NuGet. org tem esta aparência:

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

Se a implementação do cliente precisar exibir um link para o formulário relatar abuso para NuGet. Versioning 4.3.0, ele produzirá a seguinte URL e a forneceria ao usuário:

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```
