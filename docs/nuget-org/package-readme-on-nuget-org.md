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
# <a name="package-readme-on-nugetorg"></a><span data-ttu-id="e5f47-103">Pacote Leiame em NuGet.org</span><span class="sxs-lookup"><span data-stu-id="e5f47-103">Package readme on NuGet.org</span></span>

<span data-ttu-id="e5f47-104">[Inclua um arquivo Leiame em seu pacote NuGet](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile) para tornar os detalhes do pacote mais sofisticados e mais informativos para seus usuários!</span><span class="sxs-lookup"><span data-stu-id="e5f47-104">[Include a readme file in your NuGet package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile) to make your package details richer and more informative for your users!</span></span>

<span data-ttu-id="e5f47-105">Esse é provavelmente um dos primeiros elementos que os usuários verão quando exibirem a página de detalhes do pacote no NuGet.org e é essencial para fazer uma boa impressão!</span><span class="sxs-lookup"><span data-stu-id="e5f47-105">This is likely one of the first elements users will see when they view your package details page on NuGet.org and is essential to making a good impression!</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e5f47-106">O NuGet.org só dá suporte a arquivos Leiame em [redução](https://daringfireball.net/projects/markdown/) e imagens de um conjunto limitado de domínios.</span><span class="sxs-lookup"><span data-stu-id="e5f47-106">NuGet.org only supports readme files in [Markdown](https://daringfireball.net/projects/markdown/) and images from a limited set of domains.</span></span> <span data-ttu-id="e5f47-107">Consulte nossos [domínios permitidos para imagens](#allowed-domains-for-images-and-badges) e [recursos de redução com suporte](#supported-markdown-features) para garantir que seu Leiame seja renderizado corretamente no NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="e5f47-107">See our [allowed domains for images](#allowed-domains-for-images-and-badges) and [supported Markdown features](#supported-markdown-features) to ensure your readme renders correctly on NuGet.org.</span></span>

## <a name="what-should-my-readme-include"></a><span data-ttu-id="e5f47-108">O que meu arquivo Leiame deve incluir?</span><span class="sxs-lookup"><span data-stu-id="e5f47-108">What should my readme include?</span></span>

<span data-ttu-id="e5f47-109">Considere incluir os seguintes itens em seu Leiame:</span><span class="sxs-lookup"><span data-stu-id="e5f47-109">Consider including the following items in your readme:</span></span>
* <span data-ttu-id="e5f47-110">Uma introdução ao que é seu pacote e faz-quais problemas ele resolve?</span><span class="sxs-lookup"><span data-stu-id="e5f47-110">An introduction to what your package is and does - what problems does it solve?</span></span>
* <span data-ttu-id="e5f47-111">Como começar a usar seu pacote – há requisitos específicos?</span><span class="sxs-lookup"><span data-stu-id="e5f47-111">How to get started with your package - are there any specific requirements?</span></span>
* <span data-ttu-id="e5f47-112">Links para uma documentação mais abrangente, se não estiverem incluídos no próprio Leiame.</span><span class="sxs-lookup"><span data-stu-id="e5f47-112">Links to more comprehensive documentation if not included in the readme itself.</span></span>
* <span data-ttu-id="e5f47-113">Pelo menos alguns trechos de código/amostras ou imagens de exemplo.</span><span class="sxs-lookup"><span data-stu-id="e5f47-113">At least a few code snippets/samples or example images.</span></span>
* <span data-ttu-id="e5f47-114">Onde e como deixar comentários, como link para os problemas do projeto, Twitter, Issue Tracker ou outra plataforma.</span><span class="sxs-lookup"><span data-stu-id="e5f47-114">Where and how to leave feedback such as link to the project issues, Twitter, bug tracker, or other platform.</span></span>
* <span data-ttu-id="e5f47-115">Como contribuir, se aplicável.</span><span class="sxs-lookup"><span data-stu-id="e5f47-115">How to contribute, if applicable.</span></span>

<span data-ttu-id="e5f47-116">Lembre-se de que os Leiame de alta qualidade podem surgir em uma grande variedade de formatos, formas e tamanhos!</span><span class="sxs-lookup"><span data-stu-id="e5f47-116">Keep in mind, high quality readmes can come in a wide variety of formats, shapes, and sizes!</span></span> <span data-ttu-id="e5f47-117">Se você já tiver um pacote disponível em NuGet.org, é provável que você já tenha um `readme.md` ou outro arquivo de documentação em seu repositório que seja um ótimo acréscimo à sua página de detalhes do NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="e5f47-117">If you already have a package available on NuGet.org, chances are that you already have a `readme.md` or other documentation file in your repository that would be a great addition to your NuGet.org details page.</span></span>

## <a name="preview-your-readme"></a><span data-ttu-id="e5f47-118">Visualizar seu Leiame</span><span class="sxs-lookup"><span data-stu-id="e5f47-118">Preview your readme</span></span>

<span data-ttu-id="e5f47-119">Para visualizar o arquivo Leiame antes que ele esteja ativo no NuGet.org, carregue o pacote usando o [portal da Web carregar pacote no NuGet.org](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) e role para baixo até a seção "arquivo Leiame" da visualização de metadados.</span><span class="sxs-lookup"><span data-stu-id="e5f47-119">To preview your readme file before it's live on NuGet.org, upload your package using the [Upload Package web portal on NuGet.org](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) and scroll down to the "Readme File" section of the metadata preview.</span></span> <span data-ttu-id="e5f47-120">Ele deverá ser semelhante a este:</span><span class="sxs-lookup"><span data-stu-id="e5f47-120">It should look something like this:</span></span>

![Visualização do arquivo Leiame](media\readme-upload-preview.PNG)

<span data-ttu-id="e5f47-122">Considere a possibilidade de revisar e visualizar seu arquivo Leiame quanto à [compatibilidade de imagens](#allowed-domains-for-images-and-badges) e à [formatação com suporte](#supported-markdown-features) para garantir que ela proporcione uma ótima primeira impressão a usuários potenciais!</span><span class="sxs-lookup"><span data-stu-id="e5f47-122">Consider taking time to review and preview your readme file for [image compliance](#allowed-domains-for-images-and-badges) and [supported formatting](#supported-markdown-features) to make sure it gives a great first impression to potential users!</span></span> <span data-ttu-id="e5f47-123">Para corrigir erros no Leiame do pacote quando ele for publicado no NuGet.org, você precisará enviar por push uma versão atualizada do pacote com a correção.</span><span class="sxs-lookup"><span data-stu-id="e5f47-123">To correct mistakes on your package readme once it's published to NuGet.org, you will need to push an updated package version with the fix.</span></span> <span data-ttu-id="e5f47-124">Verificar se tudo parece bom com antecedência pode poupar dor de cabeça.</span><span class="sxs-lookup"><span data-stu-id="e5f47-124">Making sure everything looks good in advance may save you headache down the road.</span></span>
## <a name="allowed-domains-for-images-and-badges"></a><span data-ttu-id="e5f47-125">Domínios permitidos para imagens e notificações</span><span class="sxs-lookup"><span data-stu-id="e5f47-125">Allowed domains for images and badges</span></span>

<span data-ttu-id="e5f47-126">Devido a questões de segurança e privacidade, o NuGet.org restringe os domínios dos quais as imagens e as notificações podem ser renderizadas para hosts confiáveis.</span><span class="sxs-lookup"><span data-stu-id="e5f47-126">Due to security and privacy concerns, NuGet.org restricts the domains from which images and badges can be rendered to trusted hosts.</span></span> 

<span data-ttu-id="e5f47-127">NuGet.org permite que todas as imagens, incluindo notificações, dos seguintes domínios confiáveis sejam renderizadas:</span><span class="sxs-lookup"><span data-stu-id="e5f47-127">NuGet.org allows all images, including badges, from the following trusted domains to be rendered:</span></span>
* <span data-ttu-id="e5f47-128">api.bintray.com</span><span class="sxs-lookup"><span data-stu-id="e5f47-128">api.bintray.com</span></span>
* <span data-ttu-id="e5f47-129">api.codacy.com</span><span class="sxs-lookup"><span data-stu-id="e5f47-129">api.codacy.com</span></span>
* <span data-ttu-id="e5f47-130">api.codeclimate.com</span><span class="sxs-lookup"><span data-stu-id="e5f47-130">api.codeclimate.com</span></span>
* <span data-ttu-id="e5f47-131">api.dependabot.com</span><span class="sxs-lookup"><span data-stu-id="e5f47-131">api.dependabot.com</span></span>
* <span data-ttu-id="e5f47-132">api.travis-ci.com</span><span class="sxs-lookup"><span data-stu-id="e5f47-132">api.travis-ci.com</span></span>
* <span data-ttu-id="e5f47-133">api.travis-ci.org</span><span class="sxs-lookup"><span data-stu-id="e5f47-133">api.travis-ci.org</span></span>
* <span data-ttu-id="e5f47-134">app.fossa.io</span><span class="sxs-lookup"><span data-stu-id="e5f47-134">app.fossa.io</span></span>
* <span data-ttu-id="e5f47-135">badge.fury.io</span><span class="sxs-lookup"><span data-stu-id="e5f47-135">badge.fury.io</span></span>
* <span data-ttu-id="e5f47-136">badgen.net</span><span class="sxs-lookup"><span data-stu-id="e5f47-136">badgen.net</span></span>
* <span data-ttu-id="e5f47-137">badges.gitter.im</span><span class="sxs-lookup"><span data-stu-id="e5f47-137">badges.gitter.im</span></span>
* <span data-ttu-id="e5f47-138">bettercodehub.com</span><span class="sxs-lookup"><span data-stu-id="e5f47-138">bettercodehub.com</span></span>
* <span data-ttu-id="e5f47-139">buildstats.info</span><span class="sxs-lookup"><span data-stu-id="e5f47-139">buildstats.info</span></span>
* <span data-ttu-id="e5f47-140">camo.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="e5f47-140">camo.githubusercontent.com</span></span>
* <span data-ttu-id="e5f47-141">ci.appveyor.com</span><span class="sxs-lookup"><span data-stu-id="e5f47-141">ci.appveyor.com</span></span>
* <span data-ttu-id="e5f47-142">circleci.com</span><span class="sxs-lookup"><span data-stu-id="e5f47-142">circleci.com</span></span>
* <span data-ttu-id="e5f47-143">codecov.io</span><span class="sxs-lookup"><span data-stu-id="e5f47-143">codecov.io</span></span>
* <span data-ttu-id="e5f47-144">codefactor.io</span><span class="sxs-lookup"><span data-stu-id="e5f47-144">codefactor.io</span></span>
* <span data-ttu-id="e5f47-145">coveralls.io</span><span class="sxs-lookup"><span data-stu-id="e5f47-145">coveralls.io</span></span>
* <span data-ttu-id="e5f47-146">dev.azure.com</span><span class="sxs-lookup"><span data-stu-id="e5f47-146">dev.azure.com</span></span>
* <span data-ttu-id="e5f47-147">github.com/.../workflows/.../badge.svg</span><span class="sxs-lookup"><span data-stu-id="e5f47-147">github.com/.../workflows/.../badge.svg</span></span>
* <span data-ttu-id="e5f47-148">gitlab.com</span><span class="sxs-lookup"><span data-stu-id="e5f47-148">gitlab.com</span></span>
* <span data-ttu-id="e5f47-149">img.shields.io</span><span class="sxs-lookup"><span data-stu-id="e5f47-149">img.shields.io</span></span>
* <span data-ttu-id="e5f47-150">isitmaintained.com</span><span class="sxs-lookup"><span data-stu-id="e5f47-150">isitmaintained.com</span></span>
* <span data-ttu-id="e5f47-151">opencollective.com</span><span class="sxs-lookup"><span data-stu-id="e5f47-151">opencollective.com</span></span>
* <span data-ttu-id="e5f47-152">raw.github.com</span><span class="sxs-lookup"><span data-stu-id="e5f47-152">raw.github.com</span></span>
* <span data-ttu-id="e5f47-153">raw.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="e5f47-153">raw.githubusercontent.com</span></span>
* <span data-ttu-id="e5f47-154">snyk.io</span><span class="sxs-lookup"><span data-stu-id="e5f47-154">snyk.io</span></span>
* <span data-ttu-id="e5f47-155">sonarcloud.io</span><span class="sxs-lookup"><span data-stu-id="e5f47-155">sonarcloud.io</span></span>
* <span data-ttu-id="e5f47-156">user-images.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="e5f47-156">user-images.githubusercontent.com</span></span>

<span data-ttu-id="e5f47-157">Se você sentir que outro domínio deve ser adicionado à lista de permissões, fique à vontade para [arquivar um problema](https://github.com/NuGet/NuGetGallery/issues) e ele será revisado por nossa equipe de engenharia para privacidade e conformidade de segurança.</span><span class="sxs-lookup"><span data-stu-id="e5f47-157">If you feel that another domain should be added to the allow-list, please feel free to [file an issue](https://github.com/NuGet/NuGetGallery/issues) and it will be reviewed by our engineering team for privacy and security compliance.</span></span> <span data-ttu-id="e5f47-158">Imagens com caminhos e imagens locais relativas de domínios sem suporte não serão renderizadas e produzirão um aviso na página de detalhes do pacote e visualização do arquivo Leiame que é visível apenas para os proprietários do pacote.</span><span class="sxs-lookup"><span data-stu-id="e5f47-158">Images with relative local paths and images hosted from unsupported domains will not be rendered and will produce a warning on the readme file preview and package details page that is only visible to the package owners.</span></span>

## <a name="supported-markdown-features"></a><span data-ttu-id="e5f47-159">Recursos de redução com suporte</span><span class="sxs-lookup"><span data-stu-id="e5f47-159">Supported Markdown features</span></span>
<span data-ttu-id="e5f47-160">O [Markdown](https://daringfireball.net/projects/markdown/) é uma linguagem de marcação leve com sintaxe de formatação de texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="e5f47-160">[Markdown](https://daringfireball.net/projects/markdown/) is a lightweight markup language with plain text formatting syntax.</span></span> <span data-ttu-id="e5f47-161">Os NuGet.org Readmes dão suporte à redução de conformidade com [CommonMark](https://commonmark.org/) por meio do mecanismo de análise de [Markdig](https://github.com/lunet-io/markdig) .</span><span class="sxs-lookup"><span data-stu-id="e5f47-161">NuGet.org readmes support [CommonMark](https://commonmark.org/) compliant Markdown through the [Markdig](https://github.com/lunet-io/markdig) parsing engine.</span></span>

<span data-ttu-id="e5f47-162">Atualmente, o NuGet.org dá suporte aos seguintes recursos de redução:</span><span class="sxs-lookup"><span data-stu-id="e5f47-162">NuGet.org currently supports the following Markdown features:</span></span>
* [<span data-ttu-id="e5f47-163">Cabeçalhos</span><span class="sxs-lookup"><span data-stu-id="e5f47-163">Headers</span></span>](https://spec.commonmark.org/0.29/#atx-headings)
* [<span data-ttu-id="e5f47-164">Imagens</span><span class="sxs-lookup"><span data-stu-id="e5f47-164">Images</span></span>](https://spec.commonmark.org/0.29/#images)
* [<span data-ttu-id="e5f47-165">Ênfase extra</span><span class="sxs-lookup"><span data-stu-id="e5f47-165">Extra emphasis</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmphasisExtraSpecs.md)
* [<span data-ttu-id="e5f47-166">Listas</span><span class="sxs-lookup"><span data-stu-id="e5f47-166">Lists</span></span>](https://spec.commonmark.org/0.29/#lists)
* [<span data-ttu-id="e5f47-167">Links</span><span class="sxs-lookup"><span data-stu-id="e5f47-167">Links</span></span>](https://spec.commonmark.org/0.29/#links)
* [<span data-ttu-id="e5f47-168">Citações em bloco</span><span class="sxs-lookup"><span data-stu-id="e5f47-168">Block quotes</span></span>](https://spec.commonmark.org/0.29/#block-quotes)
* [<span data-ttu-id="e5f47-169">Escapes de barra invertida</span><span class="sxs-lookup"><span data-stu-id="e5f47-169">Backslash escapes</span></span>](https://spec.commonmark.org/0.29/#backslash-escapes)
* [<span data-ttu-id="e5f47-170">Trechos de código</span><span class="sxs-lookup"><span data-stu-id="e5f47-170">Code spans</span></span>](https://spec.commonmark.org/0.29/#code-spans)
* [<span data-ttu-id="e5f47-171">Listas de tarefas</span><span class="sxs-lookup"><span data-stu-id="e5f47-171">Task lists</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/TaskListSpecs.md)
* [<span data-ttu-id="e5f47-172">Tabelas</span><span class="sxs-lookup"><span data-stu-id="e5f47-172">Tables</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/PipeTableSpecs.md)
* [<span data-ttu-id="e5f47-173">Emojis</span><span class="sxs-lookup"><span data-stu-id="e5f47-173">Emojis</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmojiSpecs.md)
* [<span data-ttu-id="e5f47-174">Links automáticos</span><span class="sxs-lookup"><span data-stu-id="e5f47-174">Auto-links</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

