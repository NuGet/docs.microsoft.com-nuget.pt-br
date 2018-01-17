---
title: Como criar um pacote do NuGet localizado | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 824c3f45-c6c2-4c82-9d6d-62a19bfdc4a4
description: "Detalhes sobre os dois modos de criar pacotes do NuGet localizados, incluindo todos os assemblies em um único pacote ou publicando assemblies separados."
keywords: "Localização de pacote do NuGet, assemblies satélite do NuGet, criação de pacotes localizados, convenções de localização do NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: aa48e77bd0e64cf45292687a2d4cada198ff5749
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="creating-localized-nuget-packages"></a><span data-ttu-id="02823-104">Criando pacotes do NuGet localizados</span><span class="sxs-lookup"><span data-stu-id="02823-104">Creating localized NuGet packages</span></span>

<span data-ttu-id="02823-105">Há duas maneiras de criar versões localizadas de uma biblioteca:</span><span class="sxs-lookup"><span data-stu-id="02823-105">There are two ways to create localized versions of a library:</span></span>

1. <span data-ttu-id="02823-106">Inclua todos os assemblies de recursos localizados em um único pacote.</span><span class="sxs-lookup"><span data-stu-id="02823-106">Include all localized resources assemblies in a single package.</span></span>
2. <span data-ttu-id="02823-107">Crie pacotes satélite localizados separados (NuGet 1.8 e posterior) seguindo um conjunto restrito de convenções.</span><span class="sxs-lookup"><span data-stu-id="02823-107">Create separate localized satellite packages (NuGet 1.8 and later), by following a strict set of conventions.</span></span>

<span data-ttu-id="02823-108">Ambos os métodos têm vantagens e desvantagens, conforme discutido nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="02823-108">Both methods have their advantages and disadvantages, as described in the following sections.</span></span>

## <a name="localized-resource-assemblies-in-a-single-package"></a><span data-ttu-id="02823-109">Assemblies de recursos localizados em um único pacote</span><span class="sxs-lookup"><span data-stu-id="02823-109">Localized resource assemblies in a single package</span></span>

<span data-ttu-id="02823-110">Incluir assemblies de recurso localizado em um único pacote geralmente é a abordagem mais simples.</span><span class="sxs-lookup"><span data-stu-id="02823-110">Including localized resource assemblies in a single package is typically the simplest approach.</span></span> <span data-ttu-id="02823-111">Para fazer isso, crie pastas dentro de `lib` para os idiomas compatíveis além do padrão do pacote (presumido como en-us).</span><span class="sxs-lookup"><span data-stu-id="02823-111">To do this, create folders within `lib` for supported language other than the package default (assumed to be en-us).</span></span> <span data-ttu-id="02823-112">Nessas pastas, você pode colocar assemblies de recursos e arquivos XML do IntelliSense localizados.</span><span class="sxs-lookup"><span data-stu-id="02823-112">In these folders you can place resource assemblies and localized IntelliSense XML files.</span></span>

<span data-ttu-id="02823-113">Por exemplo, a seguinte estrutura de pasta é compatível com alemão (de), italiano (it), japonês (ja), russo (ru), chinês (simplificado) (zh-Hans) e chinês (tradicional) (zh-Hant):</span><span class="sxs-lookup"><span data-stu-id="02823-113">For example, the following folder structure supports, German (de), Italian (it), Japanese (ja), Russian (ru), Chinese (Simplified) (zh-Hans), and Chinese (Traditional) (zh-Hant):</span></span>

    lib
    └───net40
        │   Contoso.Utilities.dll
        │   Contoso.Utilities.xml
        │
        ├───de
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───it
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ja
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ru
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───zh-Hans
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        └───zh-Hant
                Contoso.Utilities.resources.dll
                Contoso.Utilities.xml

<span data-ttu-id="02823-114">Você pode ver que os idiomas estão todos listados sob a pasta `net40` da estrutura de destino.</span><span class="sxs-lookup"><span data-stu-id="02823-114">You can see that the languages are all listed underneath the `net40` target framework folder.</span></span> <span data-ttu-id="02823-115">Se você oferecer [compatibilidade a diversas estruturas](../create-packages/supporting-multiple-target-frameworks.md), existirá uma pasta em `lib` para cada variedade.</span><span class="sxs-lookup"><span data-stu-id="02823-115">If you're [supporting multiple frameworks](../create-packages/supporting-multiple-target-frameworks.md), then you'll have a folder under `lib` for each variant.</span></span>

<span data-ttu-id="02823-116">Com essas pastas em vigor, você poderá fazer referência a todos os arquivos em seu `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="02823-116">With these folders in place, you'll then reference all the files in your `.nuspec`:</span></span>

```xml
<?xml version="1.0"?>
<package>
    <metadata>...
    </metadata>
    <files>
    <file src="lib\**" target="lib" />
    </files>
</package>
```

<span data-ttu-id="02823-117">Um pacote de exemplo que usa essa abordagem é [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span><span class="sxs-lookup"><span data-stu-id="02823-117">One example package that uses this approach is [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span></span>

### <a name="advantages-and-disadvantages"></a><span data-ttu-id="02823-118">Vantagens e desvantagens</span><span class="sxs-lookup"><span data-stu-id="02823-118">Advantages and disadvantages</span></span>

<span data-ttu-id="02823-119">Agrupar todos os idiomas em um único pacote traz algumas desvantagens:</span><span class="sxs-lookup"><span data-stu-id="02823-119">Bundling all languages in a single package has a few disadvantages:</span></span>

1. <span data-ttu-id="02823-120">**Metadados compartilhados**: como um pacote do NuGet só pode conter um único arquivo `.nuspec`, é possível fornecer metadados para um único idioma.</span><span class="sxs-lookup"><span data-stu-id="02823-120">**Shared metadata**: Because a NuGet package can only contain a single `.nuspec` file, you can provide metadata for only a single language.</span></span> <span data-ttu-id="02823-121">Ou seja, o NuGet não apresenta suporte a metadados localizados.</span><span class="sxs-lookup"><span data-stu-id="02823-121">That is, NuGet does not present support localized metadata.</span></span>
2. <span data-ttu-id="02823-122">**Tamanho do pacote**: dependendo do número de idiomas compatíveis, a biblioteca pode ficar consideravelmente grande, o que atrasa a instalação e restauração do pacote.</span><span class="sxs-lookup"><span data-stu-id="02823-122">**Package size**: Depending on the number of languages you support, the library can become considerably large, which slows installing and restoring the package.</span></span>
3. <span data-ttu-id="02823-123">**Versões simultâneas**: agrupar arquivos localizados em um único pacote requer que você libere todos os ativos no pacote ao mesmo tempo, em vez de liberar cada localização separadamente.</span><span class="sxs-lookup"><span data-stu-id="02823-123">**Simultaneous releases**: Bundling localized files into a single package requires that you release all assets in that package simultaneously, rather than being able to release each localization separately.</span></span> <span data-ttu-id="02823-124">Além disso, qualquer atualização feita em uma localização requer uma nova versão do pacote inteiro.</span><span class="sxs-lookup"><span data-stu-id="02823-124">Furthermore, any update to any one localization requires a new version of the entire package.</span></span>

<span data-ttu-id="02823-125">No entanto, isso também traz alguns benefícios:</span><span class="sxs-lookup"><span data-stu-id="02823-125">However, it also has a few benefits:</span></span>

1. <span data-ttu-id="02823-126">**Simplicidade**: os consumidores do pacote obtém todos os idiomas compatíveis em uma única instalação, em vez de ter que instalar cada idioma separadamente.</span><span class="sxs-lookup"><span data-stu-id="02823-126">**Simplicity**: Consumers of the package get all supported languages in a single install, rather than having to install each language separately.</span></span> <span data-ttu-id="02823-127">Também é mais fácil de localizar um único pacote no nuget.org.</span><span class="sxs-lookup"><span data-stu-id="02823-127">A single package is also easier to find on nuget.org.</span></span>
2. <span data-ttu-id="02823-128">**Versões acopladas**: como todos os assemblies de recursos estão no mesmo pacote que o assembly principal, todos eles compartilham o mesmo número de versão e não correm o risco de serem desacopladas inadvertidamente.</span><span class="sxs-lookup"><span data-stu-id="02823-128">**Coupled versions**: Because all of the resource assemblies are in the same package as the primary assembly, they all share the same version number and don't run a risk of getting erroneously decoupled.</span></span>


## <a name="localized-satellite-packages"></a><span data-ttu-id="02823-129">Pacotes satélite localizados</span><span class="sxs-lookup"><span data-stu-id="02823-129">Localized satellite packages</span></span>

<span data-ttu-id="02823-130">Semelhante a como o .NET Framework dá suporte a assemblies satélite, esse método separa os recursos localizados e arquivos XML do IntelliSense em pacotes satélite.</span><span class="sxs-lookup"><span data-stu-id="02823-130">Similar to how .NET Framework supports satellite assemblies, this method separates localized resources and IntelliSense XML files into satellite packages.</span></span>

<span data-ttu-id="02823-131">Para fazer isso, o pacote principal usa a convenção de nomenclatura `{identifier}.{version}.nupkg` e contém o assembly para o idioma padrão (por exemplo, en-US).</span><span class="sxs-lookup"><span data-stu-id="02823-131">Do to this, your primary package uses the naming convention `{identifier}.{version}.nupkg` and contains the assembly for the default language (such as en-US).</span></span> <span data-ttu-id="02823-132">Por exemplo, `ContosoUtilities.1.0.0.nupkg` conteria a seguinte estrutura:</span><span class="sxs-lookup"><span data-stu-id="02823-132">For example, `ContosoUtilities.1.0.0.nupkg` would contain the following structure:</span></span>

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

<span data-ttu-id="02823-133">Dessa forma, um assembly satélite usa a convenção de nomenclatura `{identifier}.{language}.{version}.nupkg`, como `ContosoUtilities.de.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="02823-133">A satellite assembly then uses the naming convention `{identifier}.{language}.{version}.nupkg`, such as `ContosoUtilities.de.1.0.0.nupkg`.</span></span> <span data-ttu-id="02823-134">O identificador **precisa** corresponder exatamente ao pacote principal.</span><span class="sxs-lookup"><span data-stu-id="02823-134">The identifier **must** exactly match that of the primary package.</span></span>

<span data-ttu-id="02823-135">Como esse é um pacote separado, ele tem seu próprio arquivo `.nuspec` que contém metadados localizado.</span><span class="sxs-lookup"><span data-stu-id="02823-135">Because this is a separate package, it has its own `.nuspec` file that contains localized metadata.</span></span> <span data-ttu-id="02823-136">Lembre-se que o idioma no `.nuspec` **precisa** corresponder àquele usado no nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="02823-136">Be mindful that the language in the `.nuspec` **must** match the one used in the filename.</span></span>

<span data-ttu-id="02823-137">O assembly satélite também **precisa** declarar uma versão exata do pacote principal como uma dependência, usando a notação de versão [] \(consulte [Controle de versão do pacote](../reference/package-versioning.md)).</span><span class="sxs-lookup"><span data-stu-id="02823-137">The satellite assembly **must** also declare an exact version of the primary package as a dependency, using the [] version notation (see [Package versioning](../reference/package-versioning.md)).</span></span> <span data-ttu-id="02823-138">Por exemplo, `ContosoUtilities.de.1.0.0.nupkg` precisa declarar uma dependência em `ContosoUtilities.1.0.0.nupkg` usando a notação `[1.0.0]`.</span><span class="sxs-lookup"><span data-stu-id="02823-138">For example, `ContosoUtilities.de.1.0.0.nupkg` must declare a dependency on `ContosoUtilities.1.0.0.nupkg` using the `[1.0.0]` notation.</span></span> <span data-ttu-id="02823-139">O pacote satélite pode, obviamente, ter um número de versão diferente do pacote principal.</span><span class="sxs-lookup"><span data-stu-id="02823-139">The satellite package can, of course, have a different version number than the primary package.</span></span>

<span data-ttu-id="02823-140">A estrutura do pacote satélite deverá incluir o assembly do recurso e o arquivo XML do IntelliSense em uma subpasta que corresponde a `{language}` no nome de arquivo do pacote:</span><span class="sxs-lookup"><span data-stu-id="02823-140">The satellite package's structure must then include the resource assembly and XML IntelliSense file in a subfolder that matches `{language}` in the package filename:</span></span>

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

<span data-ttu-id="02823-141">**Observação**: a menos que subculturas específicos como `ja-JP` sejam necessárias, sempre use o identificador de idioma de nível superior, como `ja`.</span><span class="sxs-lookup"><span data-stu-id="02823-141">**Note**: unless specific subcultures such as `ja-JP` are necessary, always use the higher level language identifier, like `ja`.</span></span>

<span data-ttu-id="02823-142">Em um assembly satélite, o NuGet reconhecerá **somente** esses arquivos na pasta que corresponde ao `{language}` no nome de arquivo.</span><span class="sxs-lookup"><span data-stu-id="02823-142">In a satellite assembly, NuGet will recognize **only** those files in the folder that matches the `{language}` in the filename.</span></span> <span data-ttu-id="02823-143">Todos os outros são ignorados.</span><span class="sxs-lookup"><span data-stu-id="02823-143">All others are ignored.</span></span>

<span data-ttu-id="02823-144">Quando todas essas convenções são atendidas, o NuGet reconhecerá o pacote como um pacote de satélite e instalará os arquivos localizados na pasta `lib` do pacote principal, como se tivesse sido fornecidos empacotados.</span><span class="sxs-lookup"><span data-stu-id="02823-144">When all of these conventions are met, NuGet will recognize the package as a satellite package and install the localized files into the primary package's `lib` folder, as if they had been originally bundled.</span></span> <span data-ttu-id="02823-145">Desinstalar o pacote satélite removerá seus arquivos da mesma pasta.</span><span class="sxs-lookup"><span data-stu-id="02823-145">Uninstalling the satellite package will remove its files from that same folder.</span></span>

<span data-ttu-id="02823-146">Assemblies satélite adicionais são criados da mesma forma para cada idioma compatível.</span><span class="sxs-lookup"><span data-stu-id="02823-146">You would create additional satellite assemblies in the same way for each supported language.</span></span> <span data-ttu-id="02823-147">Por exemplo, examine o conjunto de pacotes do ASP.NET MVC:</span><span class="sxs-lookup"><span data-stu-id="02823-147">For an example, examine the set of ASP.NET MVC packages:</span></span>

* <span data-ttu-id="02823-148">[Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (principal em inglês)</span><span class="sxs-lookup"><span data-stu-id="02823-148">[Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (English primary)</span></span>
* <span data-ttu-id="02823-149">[Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (alemão)</span><span class="sxs-lookup"><span data-stu-id="02823-149">[Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (German)</span></span>
* <span data-ttu-id="02823-150">[Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (japonês)</span><span class="sxs-lookup"><span data-stu-id="02823-150">[Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)</span></span>
* <span data-ttu-id="02823-151">[Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (chinês (simplificado))</span><span class="sxs-lookup"><span data-stu-id="02823-151">[Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))</span></span>
* <span data-ttu-id="02823-152">[Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (chinês (tradicional))</span><span class="sxs-lookup"><span data-stu-id="02823-152">[Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))</span></span>

### <a name="summary-of-required-conventions"></a><span data-ttu-id="02823-153">Resumo das convenções necessárias</span><span class="sxs-lookup"><span data-stu-id="02823-153">Summary of required conventions</span></span>

- <span data-ttu-id="02823-154">O pacote principal deve ser nomeado `{identifier}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="02823-154">Primary package must be named `{identifier}.{version}.nupkg`</span></span>
- <span data-ttu-id="02823-155">Um pacote satélite deve ser nomeado `{identifier}.{language}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="02823-155">A satellite package must be named `{identifier}.{language}.{version}.nupkg`</span></span>
- <span data-ttu-id="02823-156">Um `.nuspec` do pacote satélite precisa especificar o idioma para corresponder ao nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="02823-156">A satellite package's `.nuspec` must specify its language to match the filename.</span></span>
- <span data-ttu-id="02823-157">Um pacote satélite precisa declarar uma dependência em uma versão exata do primário usando a notação [] no seu arquivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="02823-157">A satellite package must declare a dependency on an exact version of the primary using the [] notation in its `.nuspec` file.</span></span> <span data-ttu-id="02823-158">Não há suporte para intervalos.</span><span class="sxs-lookup"><span data-stu-id="02823-158">Ranges are not supported.</span></span>
- <span data-ttu-id="02823-159">Um pacote satélite precisa colocar os arquivos na pasta `lib\[{framework}\]{language}` que corresponde exatamente ao `{language}` no nome de arquivo.</span><span class="sxs-lookup"><span data-stu-id="02823-159">A satellite package must place files in the `lib\[{framework}\]{language}` folder that exactly matches `{language}` in the filename.</span></span>

### <a name="advantages-and-disadvantages"></a><span data-ttu-id="02823-160">Vantagens e desvantagens</span><span class="sxs-lookup"><span data-stu-id="02823-160">Advantages and disadvantages</span></span>

<span data-ttu-id="02823-161">Usar pacotes satélite traz alguns benefícios:</span><span class="sxs-lookup"><span data-stu-id="02823-161">Using satellite packages has a few benefits:</span></span>

1. <span data-ttu-id="02823-162">**Tamanho do pacote**: a superfície geral do pacote principal é minimizada e os consumidores incorrem somente nos custos de cada idioma que desejam usar.</span><span class="sxs-lookup"><span data-stu-id="02823-162">**Package size**: The overall footprint of the primary package is minimized, and consumers only incur the costs of each language they want to use.</span></span>
2. <span data-ttu-id="02823-163">**Metadados separados**: cada pacote satélite tem seu próprio arquivo `.nuspec` e, portanto, seus próprios metadados localizado porque.</span><span class="sxs-lookup"><span data-stu-id="02823-163">**Separate metadata**: Each satellite package has its own `.nuspec` file and thus its own localized metadata because.</span></span> <span data-ttu-id="02823-164">Isso pode permitir que alguns consumidores localizem os pacotes mais facilmente pesquisando nuget.org com termos localizados.</span><span class="sxs-lookup"><span data-stu-id="02823-164">This can allow some consumers to find packages more easily by searching nuget.org with localized terms.</span></span>
3. <span data-ttu-id="02823-165">**Versões desacopladas**: assemblies satélite podem ser liberados ao longo do tempo, em vez de uma só vez, permitindo que você distribua seus esforços de localização.</span><span class="sxs-lookup"><span data-stu-id="02823-165">**Decoupled releases**: Satellite assemblies can be released over time, rather than all at once, allowing you to spread out your localization efforts.</span></span>

<span data-ttu-id="02823-166">No entanto, pacotes satélite trazem seu próprio conjunto de desvantagens:</span><span class="sxs-lookup"><span data-stu-id="02823-166">However, satellite packages have their own set of disadvantages:</span></span>

1. <span data-ttu-id="02823-167">**Desordem**: em vez de um único pacote, você tem muitos pacotes que podem levar a resultados da pesquisa desorganizados no nuget.org e uma longa lista de referências em um projeto do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="02823-167">**Clutter**: Instead of a single package, you have many packages that can lead to cluttered search results on nuget.org and a long list of references in a Visual Studio project.</span></span>
2. <span data-ttu-id="02823-168">**Convenções estritas**.</span><span class="sxs-lookup"><span data-stu-id="02823-168">**Strict conventions**.</span></span> <span data-ttu-id="02823-169">Pacotes satélite devem seguir as convenções com exatidão ou as versões localizadas não serão selecionadas corretamente.</span><span class="sxs-lookup"><span data-stu-id="02823-169">Satellite packages must follow the conventions exactly or the localized versions won't be picked up properly.</span></span>
3. <span data-ttu-id="02823-170">**Controle de versão**: cada pacote satélite precisa ter uma dependência de versão exata do pacote principal.</span><span class="sxs-lookup"><span data-stu-id="02823-170">**Versioning**: Each satellite package must have an exact version dependency on the primary package.</span></span> <span data-ttu-id="02823-171">Isso significa que a atualização do pacote principal pode requerer a atualização de todos os pacotes satélite, mesmo se os recursos não foram alterados.</span><span class="sxs-lookup"><span data-stu-id="02823-171">This means that updating the primary package may require updating all satellite packages as well, even if the resources didn't change.</span></span>
