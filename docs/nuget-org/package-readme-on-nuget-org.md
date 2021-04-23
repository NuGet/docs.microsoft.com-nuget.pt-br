---
title: Pacote Leiame em NuGet.org
description: Uma explicação detalhada de como os arquivos Leiame em NuGet.org são renderizados e o que fazer quando você encontrar problemas.
author: chgill-MSFT
ms.author: chgill
ms.date: 02/23/2021
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: a5d68329128c9e9d047fe10e08ce41f1ae0895b4
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107902240"
---
# <a name="package-readme-on-nugetorg"></a>Pacote Leiame em NuGet.org

[Inclua um arquivo Leiame em seu pacote NuGet](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile) para tornar os detalhes do pacote mais sofisticados e mais informativos para seus usuários!

Esse é provavelmente um dos primeiros elementos que os usuários verão quando exibirem a página de detalhes do pacote no NuGet.org e é essencial para fazer uma boa impressão!

> [!IMPORTANT]
> O NuGet.org só dá suporte a arquivos Leiame em [redução](https://daringfireball.net/projects/markdown/) e imagens de um conjunto limitado de domínios. Consulte nossos [domínios permitidos para imagens](#allowed-domains-for-images-and-badges) e [recursos de redução com suporte](#supported-markdown-features) para garantir que seu Leiame seja renderizado corretamente no NuGet.org.

## <a name="what-should-my-readme-include"></a>O que meu arquivo Leiame deve incluir?

Considere incluir os seguintes itens em seu Leiame:
* Uma introdução ao que é seu pacote e faz-quais problemas ele resolve?
* Como começar a usar seu pacote – há requisitos específicos?
* Links para uma documentação mais abrangente, se não estiverem incluídos no próprio Leiame.
* Pelo menos alguns trechos de código/amostras ou imagens de exemplo.
* Onde e como deixar comentários, como link para os problemas do projeto, Twitter, Issue Tracker ou outra plataforma.
* Como contribuir, se aplicável.

Lembre-se de que os Leiame de alta qualidade podem surgir em uma grande variedade de formatos, formas e tamanhos! Se você já tiver um pacote disponível em NuGet.org, é provável que você já tenha um `readme.md` ou outro arquivo de documentação em seu repositório que seja um ótimo acréscimo à sua página de detalhes do NuGet.org.

## <a name="preview-your-readme"></a>Visualizar seu Leiame

Para visualizar o arquivo Leiame antes que ele esteja ativo no NuGet.org, carregue o pacote usando o [portal da Web carregar pacote no NuGet.org](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) e role para baixo até a seção "arquivo Leiame" da visualização de metadados. Ele deverá ser semelhante a este:

![Visualização do arquivo Leiame](media\readme-upload-preview.PNG)

Considere a possibilidade de revisar e visualizar seu arquivo Leiame quanto à [compatibilidade de imagens](#allowed-domains-for-images-and-badges) e à [formatação com suporte](#supported-markdown-features) para garantir que ela proporcione uma ótima primeira impressão a usuários potenciais! Para corrigir erros no Leiame do pacote quando ele for publicado no NuGet.org, você precisará enviar por push uma versão atualizada do pacote com a correção. Verificar se tudo parece bom com antecedência pode poupar dor de cabeça.
## <a name="allowed-domains-for-images-and-badges"></a>Domínios permitidos para imagens e notificações

Devido a questões de segurança e privacidade, o NuGet.org restringe os domínios dos quais as imagens e as notificações podem ser renderizadas para hosts confiáveis. 

NuGet.org permite que todas as imagens, incluindo notificações, dos seguintes domínios confiáveis sejam renderizadas:
* api.bintray.com
* api.codacy.com
* api.codeclimate.com
* api.dependabot.com
* api.travis-ci.com
* api.travis-ci.org
* app.fossa.io
* badge.fury.io
* badgen.net
* badges.gitter.im
* bettercodehub.com
* buildstats.info
* camo.githubusercontent.com
* ci.appveyor.com
* circleci.com
* codecov.io
* codefactor.io
* coveralls.io
* dev.azure.com
* github.com/.../workflows/.../badge.svg
* gitlab.com
* img.shields.io
* isitmaintained.com
* opencollective.com
* raw.github.com
* raw.githubusercontent.com
* snyk.io
* sonarcloud.io
* user-images.githubusercontent.com

Se você sentir que outro domínio deve ser adicionado à lista de permissões, fique à vontade para [arquivar um problema](https://github.com/NuGet/NuGetGallery/issues) e ele será revisado por nossa equipe de engenharia para privacidade e conformidade de segurança. Imagens com caminhos e imagens locais relativas de domínios sem suporte não serão renderizadas e produzirão um aviso na página de detalhes do pacote e visualização do arquivo Leiame que é visível apenas para os proprietários do pacote.

## <a name="supported-markdown-features"></a>Recursos de redução com suporte
O [Markdown](https://daringfireball.net/projects/markdown/) é uma linguagem de marcação leve com sintaxe de formatação de texto sem formatação. Os NuGet.org Readmes dão suporte à redução de conformidade com [CommonMark](https://commonmark.org/) por meio do mecanismo de análise de [Markdig](https://github.com/lunet-io/markdig) .

Atualmente, o NuGet.org dá suporte aos seguintes recursos de redução:
* [Cabeçalhos](https://spec.commonmark.org/0.29/#atx-headings)
* [Imagens](https://spec.commonmark.org/0.29/#images)
* [Ênfase extra](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmphasisExtraSpecs.md)
* [Listas](https://spec.commonmark.org/0.29/#lists)
* [Links](https://spec.commonmark.org/0.29/#links)
* [Citações em bloco](https://spec.commonmark.org/0.29/#block-quotes)
* [Escapes de barra invertida](https://spec.commonmark.org/0.29/#backslash-escapes)
* [Trechos de código](https://spec.commonmark.org/0.29/#code-spans)
* [Listas de tarefas](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/TaskListSpecs.md)
* [Tabelas](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/PipeTableSpecs.md)
* [Emojis](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmojiSpecs.md)
* [Links automáticos](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

