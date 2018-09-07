---
title: Visão geral do ecossistema do NuGet
description: Recursos abrangentes no ecossistema do NuGet, incluindo fontes NuGet, projetos que não são do Microsoft NuGet, utilitários e materiais de treinamento.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 31243076f36f6ff274c4377c1773ea59dda8c834
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548138"
---
# <a name="an-overview-of-the-nuget-ecosystem"></a>Uma visão geral do ecossistema do NuGet

Desde seu lançamento em 2010, o NuGet apresentou uma grande oportunidade para melhorar e automatizar os diferentes aspectos dos processos de desenvolvimento.

Como o NuGet é um software livre segundo a abrangente [licença do Apache v2](http://choosealicense.com/licenses/apache/), outros projetos podem aproveitar o NuGet e as empresas podem incluir compatibilidade com ele em seus produtos. Para projetos de software livre ou desenvolvimento de aplicativos corporativos, o NuGet e outros aplicativos baseados no NuGet fornecem um ecossistema amplo de ferramentas para melhorar o processo de desenvolvimento de software.

Todos esses projetos são capazes de inovar devido a contribuições do desenvolvedor. Assim como você contribuir com o NuGet em si, contribua também com esses projetos relatando defeitos e novas ideias de recursos, fornecer comentários, escrevendo documentação e contribuindo com código sempre que possível.

## <a name="net-foundation-projects"></a>Projetos da .NET Foundation

O NuGet fornece um sistema de gerenciamento de pacotes de software livre gratuito para a plataforma de desenvolvimento da Microsoft. Ele consiste em algumas ferramentas de cliente, bem como o conjunto de serviços que compõem a [Galeria do NuGet oficial](http://www.nuget.org). Combinados, eles formam o projeto NuGet, que é controlado pelo [.NET Foundation](http://www.dotnetfoundation.org/).

A NuGet Organization contém vários repositórios no GitHub. O [https://github.com/Nuget/Home](https://github.com/Nuget/Home) fornece uma visão geral de todos os repositórios e onde encontrar os vários componentes do NuGet.

## <a name="microsoft-projects"></a>Projetos da Microsoft

A Microsoft contribuiu amplamente para o desenvolvimento do NuGet. Todas as contribuições feitas por funcionários da Microsoft também de software livre e foram doadas (incluindo os direitos autorais) para a .NET Foundation.

## <a name="non-microsoft-projects"></a>Projetos que não são da Microsoft

Muitos outros indivíduos e empresas contribuíram significativamente com o ecossistema do NuGet. Cada projeto listado aqui pode ter uma licença diferente dos componentes principais do NuGet, portanto confirme se os termos de licença são aceitáveis antes de usar:

- [AppVeyor CI](https://www.appveyor.com/)
- [Artifactory](https://www.jfrog.com/artifactory/)
- [BoxStarter](http://boxstarter.org/)
- [Chocolatey](https://chocolatey.org/)
- [CoApp](http://coapp.org/)
- [JetBrains ReSharper](https://resharper-plugins.jetbrains.com/)
- [JetBrains TeamCity](https://www.jetbrains.com/teamcity/)
- [Klondike](https://github.com/themotleyfool/Klondike)
- [MinimalNugetServer](https://github.com/TanukiSharp/MinimalNugetServer)
- [MyGet (ou NuGet como serviço)](http://www.myget.org/)
- [Explorador de Pacotes do NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [NuGet Server](http://nugetserver.net/)
- [OctopusDeploy](https://octopus.com/)
- [Paket](https://fsprojects.github.io/Paket/)
- [ProGet (Inedo)](http://inedo.com/proget)
- [scriptcs](http://scriptcs.net/)
- [SharpDevelop](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [Sonatype Nexus](http://www.sonatype.com/nexus-repository-sonatype)
- [SymbolSource](http://www.symbolsource.org/Public)
- [Xamarin e MonoDevelop](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a>Outros utilitários baseados no NuGet

Essas são ferramentas e utilitários compilados no NuGet:

- [Extensões do Glimpse](http://getglimpse.com/Packages) (os plug-ins são pacotes)
- [NuGetMustHaves.com](http://nugetmusthaves.com/)
- [Orchard](http://www.orchardproject.net/) (módulos CMS são buscados de um feed do NuGet v1 hospedado na Galeria do Orchard)
- [Implementação Java do NuGet Server](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- [NuGetLatest](https://twitter.com/NuGetLatest) (bot do Twitter que tuíta a publicação de novos pacotes)
- [DefinitelyTyped](http://definitelytyped.org/) (Tipo de TypeScript [Automático](https://github.com/DefinitelyTyped/NugetAutomation/) com [Definições publicadas no NuGet](http://www.nuget.org/packages?q=DefinitelyTyped))

## <a name="training-materials-and-references"></a>Referências e materiais de treinamento

Usar uma nova ferramenta ou tecnologia geralmente requer certa curva de aprendizado. Felizmente, o NuGet não requer nenhuma curva de aprendizado. Na verdade, qualquer pessoa pode [começar a consumir pacotes](../quickstart/use-a-package.md) rapidamente.

Dito isso, criar pacotes – e, especialmente, bons pacotes – juntamente com a adoção do NuGet nos processos de compilação e implantação automatizados, requer dedicar um pouco mais de tempo com os seguintes recursos:

- [Blog do NuGet](http://blog.nuget.org/)
- [Equipe do NuGet no Twitter, @nuget](http://twitter.com/nuget)
- Livros:
  - [Apress Pro NuGet](http://bit.ly/ProNuGet)
  - [NuGet 2 Essentials](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a>Documentação de pacotes individuais

O [NuDoq](http://nudoq.org) concede acesso direto, atualizações e documentação para pacotes do NuGet.

O NuDoq sonda regularmente o servidor da galeria nuget.org em busca das atualizações de pacote mais recentes, descompacta e processa os arquivos de documentação de biblioteca e atualiza o site.

## <a name="adding-your-project"></a>Adicionar seu projeto

Se você tiver um projeto do ecossistema do NuGet que seria uma adição valiosa para essa página, envie uma solicitação de pull com uma edição para esta página.
