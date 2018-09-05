---
title: SDK do cliente NuGet
description: A API está em constante evolução e ainda não está documentado, mas os exemplos estão disponíveis no blog de Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 8e612d9f86bcffc99870c5541aa6091e678db512
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547083"
---
# <a name="nuget-client-sdk"></a>SDK do cliente NuGet

> [!Note]
> Não deve ser confundido com o [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)

O *SDK do cliente do NuGet* refere-se a um grupo de bibliotecas .NET centralizadas em torno [NuGet](https://www.nuget.org/packages/NuGet.Client), [struktury](https://www.nuget.org/packages/NuGet.Packaging), e [é](https://www.nuget.org/packages/NuGet.Protocol). Esses pacotes substituem anterior [NuGet. Core](https://www.nuget.org/packages/NuGet.Core/) biblioteca.

Estamos trabalhando em ter uma área de superfície estável que podemos pode documentar em breve.

## <a name="source-code"></a>Código-fonte

O código-fonte é publicado no GitHub no projeto [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).

## <a name="third-party-documentation"></a>Documentação de terceiros

Você pode encontrar exemplos e documentação para algumas das APIs na seguinte série de blog por Dave Glick, publicados 2016:

- [Explorando as bibliotecas do NuGet v3, parte 1: Introdução e conceitos](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [Explorando as bibliotecas do NuGet v3, parte 2: procurar pacotes](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [Explorando as bibliotecas do NuGet v3, parte 3: instalando pacotes](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Essas postagens de blog foram escritas logo após o **3.4.3** versão do NuGet, pacotes de SDK do cliente foram lançados.
> Versões mais recentes dos pacotes podem ser incompatíveis com as informações de postagens de blog.
