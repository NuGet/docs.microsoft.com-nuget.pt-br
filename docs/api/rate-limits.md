---
title: Limites de taxa, API do NuGet
description: As APIs do NuGet terão limites de taxa impostos para evitar abusos.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 372304255bf8849693947b22539e012ccdd48966
ms.sourcegitcommit: 0a63956bf12aaf1b1b45e680bc8e90f97347988c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/13/2020
ms.locfileid: "83367928"
---
# <a name="rate-limits"></a>Limites de taxa

A API NuGet.org impõe a limitação de taxa para evitar abuso. As solicitações que excedem o limite de taxa retornam o seguinte erro: 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

Além da limitação de solicitação usando limites de taxa, algumas APIs também impõem cotas. As solicitações que excedem a cota retornam o seguinte erro:

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

As tabelas a seguir listam os limites de taxa para a API NuGet.org.

## <a name="package-search"></a>Pesquisa de pacote

> [!Note]
> É recomendável usar as APIs de [pesquisa v3](search-query-service-resource.md) do NuGet. org, pois a taxa não é limitada no momento. Para APIs de pesquisa v1 e v2, os seguintes limites se aplicam:

| API | Tipo de limite | Valor de limite | Caso de uso da API |
|:---|:---|:---|:---|
**Obter**`/api/v1/Packages` | IP | 1000/minuto | Consultar metadados do pacote NuGet via coleção de OData v1 `Packages` |
**Obter**`/api/v1/Search()` | IP | 3000/minuto | Pesquisar pacotes NuGet por meio do ponto de extremidade de pesquisa v1 | 
**Obter**`/api/v2/Packages` | IP | 20000/minuto | Consultar metadados do pacote NuGet por meio da coleção do OData v2 `Packages` | 
**Obter**`/api/v2/Packages/$count` | IP | 100/minuto | Consultar contagem de pacotes NuGet por meio da coleção de OData do v2 `Packages` | 

## <a name="package-push-and-unlist"></a>Enviar por push de pacote e não listar

| API | Tipo de limite | Valor de limite | Caso de uso da API | 
|:---|:---|:---|:--- |
**Put**`/api/v2/package` | Chave de API | 350/hora | Carregar um novo pacote NuGet (versão) por meio do ponto de extremidade de push v2 
**Excluir**`/api/v2/package/{id}/{version}` | Chave de API | 250/hora | Deslistar um pacote NuGet (versão) via ponto de extremidade v2 

## <a name="nugetorg-website-page-views"></a>exibições de página do site nuget.org

Se você estiver acessando as páginas da Web do nuget.org programaticamente, considere a investigação de nossas [APIs v3](overview.md)documentadas. Esses pontos de extremidade permitem um acesso mais simples aos metadados e ao conteúdo do pacote. A API v3 tem melhor disponibilidade e tem um desempenho maior do que acessar as páginas da Web da galeria do NuGet, que são projetadas para interação com o navegador da Web.

| API | Tipo de limite | Valor de limite | Caso de uso da API | 
|:---|:---|:---|:--- |
**Obter**`/package/{id}/{version}` | IP | 50/minuto | Página de detalhes do pacote de exibição (versão). 
