---
title: Visão geral da hospedagem de seus próprios feeds do NuGet
description: Uma visão geral de aberturas para hospedar seus próprios feeds de pacote do NuGet ou galerias localmente ou remotamente.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 95750bc926c242c02112f68a5aebf43c5fdb9a46
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508290"
---
# <a name="hosting-your-own-nuget-feeds"></a>Hospedando seus próprios feeds do NuGet

Em vez de disponibilizar os pacotes publicamente, pode ser útil liberar pacotes apenas para um público limitado, como sua organização ou grupo de trabalho. Além disso, algumas empresas podem querer restringir quais bibliotecas de terceiros seus desenvolvedores podem usar, portanto, direcionando os desenvolvedores para obterem pacotes de uma origem limitado em vez do nuget.org.

Para todas as finalidades, o NuGet é compatível com a configuração de origens de pacotes privadas das seguintes maneiras:

- Feed local: pacotes são simplesmente colocados em um compartilhamento de arquivos de rede adequado, visto que o ideal seria usar `nuget init` e `nuget add` para criar uma estrutura hierárquica de pastas (NuGet 3.3 ou superior). Para obter detalhes, consulte [Feeds Local](../hosting-packages/local-feeds.md).
- NuGet.Server: os pacotes são disponibilizados por meio de um servidor HTTP local. Para ver mais detalhes, consulte [NuGet.Server](../hosting-packages/nuget-server.md).
- Galeria do NuGet: os pacotes são hospedados em um servidor de Internet usando o [Projeto da Galeria do NuGet](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com). A Galeria do NuGet fornece gerenciamento de usuários e recursos como uma interface do usuário extensiva da Web que permite pesquisar e explorar pacotes de dentro do navegador, semelhante ao nuget.org.

Também há vários outros produtos de hospedagem de NuGet compatíveis com feeds privados remotos, incluindo:

- [Gerenciamento de Pacotes do Visual Studio Team Services](https://www.visualstudio.com/docs/package/nuget/publish), que também está disponível no Team Foundation Server 2017 e posterior.
- [MyGet](http://myget.org)
- [ProGet](http://inedo.com/proget) da Inedo
- [NuGet Server](http://nugetserver.net/), um projeto da comunidade do Inedo
- [NuGet Server (Software Livre)](http://nuget-server.net), uma implementação de software livre semelhante ao NuGet Server da Inedo
- [LiGet](https://github.com/ai-traders/liget), uma implementação em código aberto do servidor NuGet V2 que é executado no kestrel no docker
- [BaGet](https://github.com/loic-sharma/BaGet), uma implementação de software livre do servidor NuGet V3 criada no ASP.NET Core
- [Artifactory](https://www.jfrog.com/artifactory/) da JFrog.
- [Nexus](http://www.sonatype.org/nexus/) da Sonatype.
- [TeamCity](https://www.jetbrains.com/teamcity/) da JetBrains.

Independentemente de como os pacotes são hospedados, acesse-os adicionando-os à lista de origens disponíveis em `NuGet.Config`. Isso pode ser feito no Visual Studio, conforme descrito em [Origens de Pacote](../tools/package-manager-ui.md#package-sources) ou na linha de comando usando [`nuget sources`](../tools/cli-ref-sources.md). O caminho para uma origem pode ser um nome de caminho de pasta local, um nome de rede ou uma URL.
