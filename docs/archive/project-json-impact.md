---
title: Impacto do project.json sobre autores de pacote do NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Detalhes sobre como a implementação do project.json no NuGet 3.x afeta autores de pacote, como recursos incompatíveis, conteúdo e formato do pacote."
keywords: "NuGet e project.json, impacto do project.json, considerações de criação de pacotes, recursos do project.json"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6104b4dac330869bc5724ffcf15cc0ac9ee26c1f
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="impact-of-projectjson-when-creating-packages"></a><span data-ttu-id="97599-104">Impacto do project.json durante a criação de pacotes</span><span class="sxs-lookup"><span data-stu-id="97599-104">Impact of project.json when creating packages</span></span>

> [!Important]
> <span data-ttu-id="97599-105">Este conteúdo foi preterido.</span><span class="sxs-lookup"><span data-stu-id="97599-105">This content is deprecated.</span></span> <span data-ttu-id="97599-106">Os projetos devem usar os formatos `packages.config` ou PackageReference.</span><span class="sxs-lookup"><span data-stu-id="97599-106">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="97599-107">O sistema `project.json` usado no NuGet 3 ou superior afeta os autores de pacote de várias maneiras, conforme descrito nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="97599-107">The `project.json` system used in NuGet 3+ affects package authors in several ways as described in the following sections.</span></span>

## <a name="changes-affecting-existing-packages-usage"></a><span data-ttu-id="97599-108">Alterações que afetam o uso de pacotes existentes</span><span class="sxs-lookup"><span data-stu-id="97599-108">Changes affecting existing packages usage</span></span>

<span data-ttu-id="97599-109">Pacotes do NuGet tradicionais são compatíveis com diversos recursos que não são refletidos no mundo transitivo.</span><span class="sxs-lookup"><span data-stu-id="97599-109">Traditional NuGet packages support a set of features that are not carried over to the transitive world.</span></span>

### <a name="install-and-uninstall-scripts-are-ignored"></a><span data-ttu-id="97599-110">Scripts de instalação e desinstalação são ignorados</span><span class="sxs-lookup"><span data-stu-id="97599-110">Install and uninstall scripts are ignored</span></span>

<span data-ttu-id="97599-111">O modelo de restauração transitiva, descrito em [Resolução de dependência](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference), não tem um conceito de “tempo de instalação do pacote”.</span><span class="sxs-lookup"><span data-stu-id="97599-111">The transitive restore model, described in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference), does not have a concept of "package install time".</span></span> <span data-ttu-id="97599-112">Um pacote existe ou não, porém não há nenhum processo consistente que ocorre quando um pacote é instalado.</span><span class="sxs-lookup"><span data-stu-id="97599-112">A package is either present or not present, but there is no consistent process that occurs when a package is installed.</span></span>

<span data-ttu-id="97599-113">Além disso, scripts de instalação são compatíveis apenas com o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="97599-113">Also, install scripts were supported only in Visual Studio.</span></span> <span data-ttu-id="97599-114">Outros IDEs precisavam simular a API de extensibilidade do Visual Studio para tentar ser compatíveis com tais scripts e não há compatibilidade em editores e ferramentas de linha de comando comuns.</span><span class="sxs-lookup"><span data-stu-id="97599-114">Other IDEs had to mock the Visual Studio extensibility API to attempt to support such scripts, and no support was available in common editors and command-line tools.</span></span>

### <a name="content-transforms-are-not-supported"></a><span data-ttu-id="97599-115">As transformações de conteúdo não são compatíveis</span><span class="sxs-lookup"><span data-stu-id="97599-115">Content transforms are not supported</span></span>

<span data-ttu-id="97599-116">Semelhante a scripts de instalação, as transformações são executadas na instalação do pacote e geralmente não são idempotentes.</span><span class="sxs-lookup"><span data-stu-id="97599-116">Similar to install scripts, transforms run on package install and are typically not idempotent.</span></span> <span data-ttu-id="97599-117">Como não há mais nenhum tempo de instalação, o XDT Transform e recursos semelhantes são incompatíveis e serão ignorados se esse tipo de pacote for usado em um cenário transitivo.</span><span class="sxs-lookup"><span data-stu-id="97599-117">Since there is no install time anymore, XDT Transform and similar features are not supported, and are ignored if such a package is used in a transitive scenario.</span></span>

### <a name="content"></a><span data-ttu-id="97599-118">Conteúdo</span><span class="sxs-lookup"><span data-stu-id="97599-118">Content</span></span>

<span data-ttu-id="97599-119">Pacotes do NuGet tradicionais fornecem arquivos de conteúdo como código-fonte e arquivos de configuração.</span><span class="sxs-lookup"><span data-stu-id="97599-119">Traditional NuGet packages are shipping content files such as source code and configuration files.</span></span> <span data-ttu-id="97599-120">Geralmente, eles são usados em dois cenários:</span><span class="sxs-lookup"><span data-stu-id="97599-120">There are used typically in two scenarios:</span></span>

1. <span data-ttu-id="97599-121">Arquivos iniciais são colocados no projeto para que o usuário possa editá-los mais tarde.</span><span class="sxs-lookup"><span data-stu-id="97599-121">Initial files dropped into the project so the user can edit them at a later time.</span></span> <span data-ttu-id="97599-122">O exemplo comum são os arquivos de configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="97599-122">The common example is default configuration files.</span></span>

1. <span data-ttu-id="97599-123">Arquivos de conteúdo usados como complementos para os assemblies instalados no projeto.</span><span class="sxs-lookup"><span data-stu-id="97599-123">Content files used as companions to the assemblies installed in the project.</span></span> <span data-ttu-id="97599-124">Este exemplo seria uma imagem de logotipo usada por um assembly.</span><span class="sxs-lookup"><span data-stu-id="97599-124">The example here would be a logo image used by an assembly.</span></span>

<span data-ttu-id="97599-125">Não há compatibilidade para o conteúdo pelos mesmos motivos dos scripts e transformações, porém já estamos desenvolvendo a compatibilidade para o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="97599-125">Support for content is currently disabled for similar reasons for scripts and transforms, but we are in the process of designing support for content.</span></span>

<span data-ttu-id="97599-126">Arquivos de conteúdo ainda podem ser transportados dentro de pacotes e são ignorados no momento, porém o usuário final ainda pode copiá-los para o ponto certo.</span><span class="sxs-lookup"><span data-stu-id="97599-126">Content files can still be carried inside the packages, and are ignored currently, however the end user can still copy them into the right spot.</span></span>

<span data-ttu-id="97599-127">Veja uma da propostas para recuperar arquivos de conteúdo e acompanhar seu andamento aqui: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span><span class="sxs-lookup"><span data-stu-id="97599-127">You can see one of the proposals for bringing back content files, and follow its progress, here: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span></span>

## <a name="impact-for-package-authors"></a><span data-ttu-id="97599-128">Impacto para os autores de pacote</span><span class="sxs-lookup"><span data-stu-id="97599-128">Impact for package authors</span></span>

<span data-ttu-id="97599-129">Pacotes que usam os recursos acima precisariam usar um mecanismo diferente.</span><span class="sxs-lookup"><span data-stu-id="97599-129">Packages using the above features would have to use a different mechanism.</span></span> <span data-ttu-id="97599-130">O mecanismo normalmente mais útil para isso seria os destinos/objetos do MSBuild que continuam a ter compatibilidade total.</span><span class="sxs-lookup"><span data-stu-id="97599-130">The most commonly useful mechanism for this would be the MSBuild targets/props that continues to get fully supported.</span></span> <span data-ttu-id="97599-131">O sistema de build pode optar por escolher outras convenções no pacote.</span><span class="sxs-lookup"><span data-stu-id="97599-131">The build system can choose to pick up other conventions in the package.</span></span> <span data-ttu-id="97599-132">É assim que os destinos do MSBuild são compatíveis, bem como os analisadores de Roslyn.</span><span class="sxs-lookup"><span data-stu-id="97599-132">This is how MSBuild targets are supported as well as Roslyn analyzers.</span></span> <span data-ttu-id="97599-133">É possível criar pacotes compatíveis com destinos e analisadores para cenários de `packages.config` e `project.json`.</span><span class="sxs-lookup"><span data-stu-id="97599-133">It is possible to build packages that supports targets and analyzers for `packages.config` and `project.json` scenarios.</span></span>

<span data-ttu-id="97599-134">Pacotes que tentam modificar o projeto para facilitar a inicialização normalmente funcionam em uma variedade muito limitada de cenários e devem fornecer um arquivo leiame ou orientação sobre como usar o pacote.</span><span class="sxs-lookup"><span data-stu-id="97599-134">Packages that attempt to modify the project to ease startup typically work in a very limited set of scenarios, and should instead provide a readme, or guidance on how to use the package.</span></span>

<span data-ttu-id="97599-135">A maioria dos pacotes existentes não deve precisar usar o formato de pacote descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="97599-135">Most existing packages should not need to use the package format described below.</span></span>

<span data-ttu-id="97599-136">O formato habilita conteúdo nativo como um cenário de primeira classe.</span><span class="sxs-lookup"><span data-stu-id="97599-136">The format enables native content as a first class scenario.</span></span> <span data-ttu-id="97599-137">Isso significa que assemblies gerenciados dependem de implementações próximas a hardware para enviar fornecer implementações binárias juntamente com os assemblies gerenciados, dependendo da plataforma de destino.</span><span class="sxs-lookup"><span data-stu-id="97599-137">This means that managed assemblies depending on close to hardware implementations to ship binary implementations alongside the managed assemblies based on the target platform.</span></span> <span data-ttu-id="97599-138">O pacote System.IO.Compression, por exemplo, utiliza essa tecnologia.</span><span class="sxs-lookup"><span data-stu-id="97599-138">For example System.IO.Compression package is utilizing this technology.</span></span> [<span data-ttu-id="97599-139">https://www.nuget.org/packages/System.IO.Compression</span><span class="sxs-lookup"><span data-stu-id="97599-139">https://www.nuget.org/packages/System.IO.Compression</span></span>](https://www.nuget.org/packages/System.IO.Compression)

<span data-ttu-id="97599-140">Resumindo, se a funcionalidade acima não é absolutamente necessária, recomendamos continuar usando o formato de pacote existente, visto que o formato descrito aqui é compatível somente com o NuGet 3.x ou superior.</span><span class="sxs-lookup"><span data-stu-id="97599-140">In summary if the functionality above is not absolutely necessary, we recommend sticking with the existing package format, as the format described here is supported only by NuGet 3.x+.</span></span>

<span data-ttu-id="97599-141">Seria possível compilar pacotes para funcionar com ambos os cenários `packages.config` e `project.json` por meio de correções, no entanto, geralmente é mais simples apenas estruturar os pacotes de forma tradicional, sem os recursos preteridos mencionados acima.</span><span class="sxs-lookup"><span data-stu-id="97599-141">It would be possible to build packages to work for both `packages.config` and `project.json` scenarios through shimming, however it's often simpler to just structure the packages the traditional way, without the deprecated features mentioned above.</span></span>

## <a name="3x-package-format"></a><span data-ttu-id="97599-142">Formato de pacote do 3.x</span><span class="sxs-lookup"><span data-stu-id="97599-142">3.x package format</span></span>

<span data-ttu-id="97599-143">O formato de pacote 3.x permite usar vários recursos adicionais além do NuGet 2.x:</span><span class="sxs-lookup"><span data-stu-id="97599-143">The 3.x package format allows for several additional features beyond NuGet 2.x:</span></span>

1. <span data-ttu-id="97599-144">A definição de um assembly de referência usado para compilação e um conjunto de assemblies de implementação usados para o tempo de execução em diferentes plataformas/dispositivos.</span><span class="sxs-lookup"><span data-stu-id="97599-144">Defining a reference assembly used for compilation and a set of implementation assemblies used for runtime on different platforms/devices.</span></span> <span data-ttu-id="97599-145">Isso permite aproveitar APIs específicas da plataforma e fornecer uma área de superfície comum para seus clientes.</span><span class="sxs-lookup"><span data-stu-id="97599-145">Which allows you to take advantage of platform specific APIs while providing a common surface area for your consumers.</span></span> <span data-ttu-id="97599-146">Especificamente, isso facilita a criação de bibliotecas portáteis intermediárias.</span><span class="sxs-lookup"><span data-stu-id="97599-146">Specifically this makes writing intermediate portable libraries easier.</span></span>

1. <span data-ttu-id="97599-147">Permite que os pacotes circulem entre as plataformas como, por exemplo, sistemas operacionais ou arquiteturas de CPU.</span><span class="sxs-lookup"><span data-stu-id="97599-147">Allows packages to pivot on platforms e.g. operating systems or CPU architecture.</span></span>

1. <span data-ttu-id="97599-148">Possibilita a separação de implementações específicas de plataforma para pacotes complementares.</span><span class="sxs-lookup"><span data-stu-id="97599-148">Allows for separation of platform specific implementations to companion packages.</span></span>

1. <span data-ttu-id="97599-149">Dependências de suporte nativo como cidadão de primeira classe.</span><span class="sxs-lookup"><span data-stu-id="97599-149">Support Native dependencies as a first class citizen.</span></span>