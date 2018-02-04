---
title: Relatar abuso modelo de URL, o NuGet API | Microsoft Docs
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "O modelo de URL do relatório abuso permite que os clientes exibir um link para relatar abuso em sua interface do usuário."
keywords: "Relatar abuso da API do NuGet, reclamação do arquivo NuGet API, o modelo de URL de relatório NuGet.org"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: c12be294c71547fbce421c72aa091e0eee15aacd
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
---
# <a name="report-abuse-url-template"></a>Modelo de URL do relatório abuso

É possível que um cliente para criar uma URL que pode ser usada pelo usuário para relatar abuso sobre um pacote específico. Isso é útil quando uma origem de pacote que deseja habilitar todas as experiências de cliente (mesmo 3ª parte) delegar abuso relatórios para a origem do pacote.

O recurso usado para buscar o conteúdo do pacote é o `ReportAbuseUriTemplate` recurso encontrado na [índice de serviço](service-index.md).

## <a name="versioning"></a>Controle de versão

O seguinte `@type` valores são usados:

Valor @type                       | Observações
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | A versão inicial
ReportAbuseUriTemplate/3.0.0-rc   | Alias de`ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>Modelo de URL

A URL para a seguinte API é o valor de `@id` propriedade associada a um recurso mencionados acima `@type` valores.

## <a name="http-methods"></a>Métodos HTTP

Embora o cliente não se destina para fazer solicitações para a URL do relatório abuso em nome do usuário, a página da web deve oferecer suporte a `GET` método para permitir que uma URL clicada facilmente ser aberto em um navegador da web.

## <a name="construct-the-url"></a>Construir a URL

Devido a uma ID de pacote conhecidos e versão, a implementação do cliente pode construir uma URL usada para acessar uma interface da web. A implementação do cliente deve exibir essa URL construído (ou link clicável) para o usuário é avisado para abrir um navegador da web para a URL e fazer qualquer relatório abuso necessário. A implementação do formulário de relatório abuso é determinada pela implementação do servidor.

O valor de `@id` é uma cadeia de caracteres de URL que contém qualquer um dos seguintes tokens de espaço reservado:

### <a name="url-placeholders"></a>Espaços reservados de URL

Nome        | Tipo    | Necessária | Observações
----------- | ------- | -------- | -----
`{id}`      | cadeia de caracteres  | no       | A ID do pacote para relatar abuso para
`{version}` | cadeia de caracteres  | no       | A versão do pacote para relatar abuso para

O `{id}` e `{version}` valores interpretados pela implementação do servidor devem ser o caso que e não é afetado se a versão é normalizada.

Por exemplo, o modelo de abuso de relatório do nuget.org tem esta aparência:

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

Se a implementação do cliente precisa exibir um link para o formulário de abuso do relatório para NuGet.Versioning 4.3.0, ele seria produzir a URL a seguir e fornecê-la para o usuário:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
