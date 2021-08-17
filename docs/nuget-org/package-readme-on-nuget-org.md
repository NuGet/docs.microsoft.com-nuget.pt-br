---
title: Leiame do pacote em NuGet.org
description: Explicação detalhada de como os arquivos leiame no NuGet.org são renderizados e o que fazer quando você se deite em problemas.
author: chgill-MSFT
ms.author: chgill
ms.date: 02/23/2021
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: ac0e89c1f5ef9eb19c29646bcc76bcb0b460c5cd
ms.sourcegitcommit: adb261dd4b2a8cd75447f7b5ea6a9e5a1a54d61d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2021
ms.locfileid: "122209937"
---
# <a name="package-readme-on-nugetorg"></a>Leiame do pacote em NuGet.org

[Inclua um arquivo leiame em seu pacote NuGet para](/nuget/reference/msbuild-targets#packagereadmefile) tornar os detalhes do pacote mais completos e mais informativos para seus usuários!

Esse é provavelmente um dos primeiros elementos que os usuários verão quando exibirem a página de detalhes do pacote em NuGet.org e é essencial para dar uma boa impressão!

> [!IMPORTANT]
> NuGet.org dá suporte apenas a arquivos leiame [em Markdown](https://daringfireball.net/projects/markdown/) e imagens de um conjunto limitado de domínios. Confira nossos [domínios permitidos para imagens](#allowed-domains-for-images-and-badges) e recursos [de Markdown](#supported-markdown-features) com suporte para garantir que seu leiame seja renderizar corretamente em NuGet.org.

## <a name="what-should-my-readme-include"></a>O que meu leiame deve incluir?

Considere incluir os seguintes itens em seu leiame:
* Uma introdução ao que seu pacote é e faz – quais problemas ele resolve?
* Como começar a usar seu pacote – há requisitos específicos?
* Links para documentação mais abrangente se não estão incluídos no leiame em si.
* Pelo menos alguns snippets de código/exemplos ou imagens de exemplo.
* Onde e como deixar comentários, como link para os problemas do projeto, Twitter, rastreador de bugs ou outra plataforma.
* Como contribuir, se aplicável.

Tenha em mente que os leiames de alta qualidade podem vir em uma ampla variedade de formatos, formas e tamanhos! Se você já tiver um pacote disponível em NuGet.org, é provável que você já tenha um ou outro arquivo de documentação em seu repositório que seria uma ótima adição à página de detalhes `readme.md` do NuGet.org.

## <a name="preview-your-readme"></a>Visualizar seu leiame

Para visualizar o arquivo leiame antes que ele seja ao vivo no NuGet.org, carregue seu pacote usando o portal da Web do pacote Upload em [NuGet.org](/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) e role para baixo até a seção "Arquivo Leiame" da versão prévia de metadados. Ele deverá ser semelhante a este:

![Versão prévia do arquivo Leiame](media\readme-upload-preview.PNG)

Considere a possibilidade de levar tempo [](#allowed-domains-for-images-and-badges) para revisar e visualizar seu arquivo leiame quanto à conformidade da imagem e à [formatação](#supported-markdown-features) com suporte para garantir que ele dê uma ótima primeira impressão aos usuários potenciais! Para corrigir erros no leiame do pacote depois que ele é publicado no NuGet.org, você precisará efetuar push de uma versão atualizada do pacote com a correção. Garantir que tudo tenha uma boa aparência com antecedência pode poupar sua cabeça no caminho.
## <a name="allowed-domains-for-images-and-badges"></a>Domínios permitidos para imagens e selos

Devido a questões de segurança e privacidade, NuGet.org restringe os domínios dos quais imagens e selos podem ser renderizados para hosts confiáveis. 

NuGet.org permite que todas as imagens, incluindo selos, dos seguintes domínios confiáveis sejam renderizadas:
* api.bintray.com
* api.codacy.com
* app.codacy.com
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
* cdn.jsdelivr.net
* ci.appveyor.com
* circleci.com
* codecov.io
* codefactor.io
* coveralls.io
* dev.azure.com
* github.com/.../workflows/.../badge.svg
* gitlab.com
* img.shields.io
* i.imgur.com
* isitmaintained.com
* opencollective.com
* raw.github.com
* raw.githubusercontent.com
* snyk.io
* sonarcloud.io
* user-images.githubusercontent.com

Se você acha que outro domínio deve ser adicionado à [](https://github.com/NuGet/NuGetGallery/issues) lista de permitir, fique à vontade para registrar um problema e ele será revisado por nossa equipe de engenharia quanto à privacidade e à conformidade com a segurança. Imagens com caminhos locais relativos e imagens hospedadas de domínios sem suporte não serão renderizadas e produzirão um aviso na visualização do arquivo leiame e na página de detalhes do pacote que só está visível para os proprietários do pacote.

## <a name="supported-markdown-features"></a>Recursos de Markdown com suporte
O [Markdown](https://daringfireball.net/projects/markdown/) é uma linguagem de marcação leve com sintaxe de formatação de texto sem formatação. NuGet.org é compatível com [Markdown em](https://commonmark.org/) conformidade com CommonMark por meio do mecanismo de análise [Markdig.](https://github.com/lunet-io/markdig)

NuGet.org atualmente dá suporte aos seguintes recursos do Markdown:
* [Cabeçalhos](https://spec.commonmark.org/0.29/#atx-headings)
* [Imagens](https://spec.commonmark.org/0.29/#images)
* [Ênfase extra](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmphasisExtraSpecs.md)
* [Listas](https://spec.commonmark.org/0.29/#lists)
* [Links](https://spec.commonmark.org/0.29/#links)
* [Citações em bloco](https://spec.commonmark.org/0.29/#block-quotes)
* [Escapes de invertida](https://spec.commonmark.org/0.29/#backslash-escapes)
* [Intervalos de código](https://spec.commonmark.org/0.29/#code-spans)
* [Listas de tarefas](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/TaskListSpecs.md)
* [Tabelas](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/PipeTableSpecs.md)
* [Emojis](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmojiSpecs.md)
* [Links automáticos](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

