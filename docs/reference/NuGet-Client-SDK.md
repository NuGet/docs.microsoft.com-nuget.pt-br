---
title: SDK do cliente NuGet
description: A API está em evolução e ainda não está documentada, mas exemplos estão disponíveis no blog de Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 873bde467a39653b818b49173d53bc983e99d1b9
ms.sourcegitcommit: f9645fc5f49c18978e12a292a3f832e162e069d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72924612"
---
# <a name="nuget-client-sdk"></a>SDK do cliente NuGet

O *SDK do cliente NuGet* refere-se a um grupo de pacotes NuGet centralizado em relação ao [NuGet. Commands](https://www.nuget.org/packages/NuGet.Commands), [NuGet. Packaging](https://www.nuget.org/packages/NuGet.Packaging)e [NuGet. Protocol](https://www.nuget.org/packages/NuGet.Protocol). Esses pacotes substituem a biblioteca [NuGet. Core](https://www.nuget.org/packages/NuGet.Core/) anterior.

> [!Note]
>  Para obter a documentação sobre o protocolo de servidor NuGet, consulte a [API do servidor NuGet](~/api/overview.md).

## <a name="source-code"></a>Código-fonte

O código-fonte é publicado no GitHub no projeto [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client).

## <a name="third-party-documentation"></a>Documentação de terceiros

Você pode encontrar exemplos e documentação para algumas das APIs na série de Blogs a seguir de Dave Glick, publicada 2016:

- [Explorando as bibliotecas do NuGet v3, parte 1: introdução e conceitos](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [Explorando as bibliotecas do NuGet v3, parte 2: pesquisando pacotes](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [Explorando as bibliotecas do NuGet v3, parte 3: Instalando pacotes](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Essas Postagens de blog foram escritas logo após a liberação da versão **3.4.3** dos pacotes do SDK do cliente NuGet.
> As versões mais recentes dos pacotes podem ser incompatíveis com as informações nas postagens do blog.

Martin Björkström fez uma postagem no blog de acompanhamento na série de Blogs de Dave Glick, onde ele introduz uma abordagem diferente sobre o uso do SDK do cliente do NuGet para a instalação de pacotes NuGet:

- [Revisitando as bibliotecas do NuGet v3](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
