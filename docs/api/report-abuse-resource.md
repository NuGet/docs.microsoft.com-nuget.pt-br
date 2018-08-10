---
title: Relatar abuso de modelo de URL, API do NuGet
description: O modelo de URL de abuso de relatório permite que os clientes exibir um link para relatar abuso em sua interface do usuário.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b1fd65b12590a6c5eeb23d946eec6ca4a1c661bc
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020434"
---
# <a name="report-abuse-url-template"></a>Modelo de URL de abuso de relatório

É possível que um cliente para criar uma URL que pode ser usada pelo usuário para relatar abuso sobre um pacote específico. Isso é útil quando uma origem de pacote que deseja habilitar todas as experiências de cliente (mesmo 3ª parte) delegar a relatórios de abuso à origem do pacote.

O recurso usado para criar essa URL é o `ReportAbuseUriTemplate` recurso encontrado na [índice de serviço](service-index.md).

## <a name="versioning"></a>Controle de versão

O seguinte `@type` valores são usados:

Valor @type                       | Observações
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | A versão inicial
ReportAbuseUriTemplate/3.0.0-rc   | Alias de `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>Modelo de URL

A URL para a seguinte API é o valor da `@id` propriedade associada a um do recurso mencionados anteriormente `@type` valores.

## <a name="http-methods"></a>Métodos HTTP

Embora o cliente não se destina para fazer solicitações para a URL para relatar abuso em nome do usuário, a página da web deve oferecer suporte a `GET` método para permitir que uma URL clicada ser aberto facilmente em um navegador da web.

## <a name="construct-the-url"></a>Construir a URL

Dada uma ID do pacote conhecidos e versão, a implementação do cliente pode construir uma URL usada para acessar uma interface da web. A implementação do cliente deve exibir esse URL construída (ou um link clicável) para o usuário permitindo que ele abra um navegador da web para a URL e fazer com que qualquer relatório abuso necessárias. A implementação do formulário de relatórios de abuso é determinada pela implementação do servidor.

O valor da `@id` é uma cadeia de caracteres de URL que contém qualquer um dos seguintes tokens de espaço reservado:

### <a name="url-placeholders"></a>Espaços reservados de URL

Nome        | Tipo    | Necessária | Observações
----------- | ------- | -------- | -----
`{id}`      | cadeia de caracteres  | no       | A ID do pacote para relatar abuso de
`{version}` | cadeia de caracteres  | no       | A versão do pacote para relatar abuso de

O `{id}` e `{version}` valores interpretadas pela implementação do servidor devem ser diferencia maiusculas de minúsculas e não é afetado se a versão é normalizada.

Por exemplo, o modelo de abuso de relatório do nuget.org fica assim:

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

Se a implementação do cliente precisar exibir um link para o formulário de abuso de relatório para NuGet.Versioning 4.3.0, ele seria produzem a seguinte URL e fornecê-la ao usuário:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
