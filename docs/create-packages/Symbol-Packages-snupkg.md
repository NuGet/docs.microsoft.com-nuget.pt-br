---
title: Como publicar pacotes de símbolos do NuGet usando o novo formato de pacote de símbolos '.snupkg' | Microsoft Docs
author: cristinamanu
ms.author: cristinamanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Como criar pacotes de símbolos do NuGet (snupkg).
keywords: Pacotes de símbolos do NuGet, depuração de pacote do NuGet, suporte à depuração de NuGet, símbolos de pacotes, convenções de símbolo de pacote do NuGet
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: c42032f1869f4be0af44ffa8fbd5ad522f73c459
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "80380412"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="74da2-104">Criando pacotes de símbolos (.snupkg)</span><span class="sxs-lookup"><span data-stu-id="74da2-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="74da2-105">Uma boa experiência de depuração depende da presença de símbolos de depuração, pois eles fornecem informações críticas, como a associação entre o compilado e o código fonte, nomes de variáveis locais, traços de pilha e muito mais.</span><span class="sxs-lookup"><span data-stu-id="74da2-105">A good debugging experience relies on the presence of debug symbols as they provide critical information like the association between the compiled and the source code, names of local variables, stack traces, and more.</span></span> <span data-ttu-id="74da2-106">Você pode usar pacotes de símbolos (.snupkg) para distribuir esses símbolos e melhorar a experiência de depuração de seus pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="74da2-106">You can use symbol packages (.snupkg) to distribute these symbols and improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74da2-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="74da2-107">Prerequisites</span></span>

<span data-ttu-id="74da2-108">[nuget.exe v4.9.0 ou acima](https://www.nuget.org/downloads) ou [dotnet CLI v2.2.0 ou superior,](https://www.microsoft.com/net/download/dotnet-core/2.2)que implementam os [protocolos NuGet necessários](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="74da2-108">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet CLI v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="74da2-109">Criar um pacote de símbolos</span><span class="sxs-lookup"><span data-stu-id="74da2-109">Creating a symbol package</span></span>

<span data-ttu-id="74da2-110">Se você estiver usando o DOtnet CLI ou MSBuild, você precisa definir as `IncludeSymbols` propriedades e `SymbolPackageFormat` as propriedades para criar um arquivo .snupkg, além do arquivo .nupkg.</span><span class="sxs-lookup"><span data-stu-id="74da2-110">If you're using dotnet CLI or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="74da2-111">Adicione as seguintes propriedades ao seu arquivo .csproj:</span><span class="sxs-lookup"><span data-stu-id="74da2-111">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* <span data-ttu-id="74da2-112">Ou especifique essas propriedades na linha de comando:</span><span class="sxs-lookup"><span data-stu-id="74da2-112">Or specify these properties on the command-line:</span></span>

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="74da2-113">ou</span><span class="sxs-lookup"><span data-stu-id="74da2-113">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="74da2-114">Se estiver usando o NuGet.exe, use os seguintes comandos para criar um arquivo .snupkg além do arquivo .nupkg:</span><span class="sxs-lookup"><span data-stu-id="74da2-114">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="74da2-115">A [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) propriedade pode ter um `symbols.nupkg` dos dois `snupkg`valores: (o padrão) ou .</span><span class="sxs-lookup"><span data-stu-id="74da2-115">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="74da2-116">Se essa propriedade não for especificada, um pacote de símbolo legado será criado.</span><span class="sxs-lookup"><span data-stu-id="74da2-116">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="74da2-117">O formato herdado `.symbols.nupkg` ainda é compatível, mas apenas por razões de compatibilidade (veja [Pacotes de símbolos herdados](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="74da2-117">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="74da2-118">O servidor de símbolos da NuGet.org aceita apenas o novo formato de pacote de símbolos – `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="74da2-118">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="74da2-119">Publicando um pacote de símbolos</span><span class="sxs-lookup"><span data-stu-id="74da2-119">Publishing a symbol package</span></span>

1. <span data-ttu-id="74da2-120">Para sua conveniência, primeiro salve sua chave de API com o NuGet (veja [Publicar um pacote](../nuget-org/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="74da2-120">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="74da2-121">Depois de publicar o pacote principal para o nuget.org, envie por push o pacote de símbolos da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="74da2-121">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="74da2-122">Você também pode efetuar push nos pacotes primário e de símbolos simultaneamente usando o comando abaixo.</span><span class="sxs-lookup"><span data-stu-id="74da2-122">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="74da2-123">Ambos os arquivos .nupkg e .snupkg precisam estar presentes na pasta atual.</span><span class="sxs-lookup"><span data-stu-id="74da2-123">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="74da2-124">O NuGet publicará ambos os pacotes em nuget.org. O `MyPackage.nupkg` será publicado primeiro, seguido por `MyPackage.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="74da2-124">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="74da2-125">Se o pacote de símbolos não for publicado, verifique se você configurou a fonte de NuGet.org como `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="74da2-125">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="74da2-126">A publicação de pacote de símbolos tem compatibilidade apenas [na API do NuGet V3](../api/overview.md#versioning).</span><span class="sxs-lookup"><span data-stu-id="74da2-126">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="74da2-127">Servidor de símbolos de NuGet.org</span><span class="sxs-lookup"><span data-stu-id="74da2-127">NuGet.org symbol server</span></span>

<span data-ttu-id="74da2-128">O NuGet.org dá suporte a seu próprio repositório de servidor de símbolos e aceita apenas o novo formato de pacote de símbolos – `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="74da2-128">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="74da2-129">Os consumidores de pacote podem usar os símbolos publicados no servidor de símbolos nuget.org adicionando `https://symbols.nuget.org/download/symbols` às suas origens de símbolos no Visual Studio, o que permite intervir no código do pacote no depurador do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="74da2-129">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="74da2-130">Consulte [Especificar símbolos (.pdb) e arquivos de origem no depurador do Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) para obter mais detalhes sobre esse processo.</span><span class="sxs-lookup"><span data-stu-id="74da2-130">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="74da2-131">NuGet.org restrições do pacote de símbolos</span><span class="sxs-lookup"><span data-stu-id="74da2-131">NuGet.org symbol package constraints</span></span>

<span data-ttu-id="74da2-132">NuGet.org tem as seguintes restrições para pacotes de símbolos:</span><span class="sxs-lookup"><span data-stu-id="74da2-132">NuGet.org has the following constraints for symbol packages:</span></span>

- <span data-ttu-id="74da2-133">Somente as seguintes extensões de arquivo `.pdb` `.nuspec`são `.xml` `.psmdcp`permitidas em pacotes de símbolos: , , , , `.rels`,`.p7s`</span><span class="sxs-lookup"><span data-stu-id="74da2-133">Only the following file extensions are allowed in symbol packages: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span></span>
- <span data-ttu-id="74da2-134">Somente [PDBs portáteis gerenciados](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) são suportados no servidor de símbolos do NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="74da2-134">Only managed [Portable PDBs](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are supported on NuGet.org's symbol server.</span></span>
- <span data-ttu-id="74da2-135">Os PDBs e seus DLLs associados .nupkg precisam ser construídos com o compilador na versão 15.9 ou superior do Visual Studio (ver [hash cripto PDB](https://github.com/dotnet/roslyn/issues/24429))</span><span class="sxs-lookup"><span data-stu-id="74da2-135">The PDBs and their associated .nupkg DLLs need to be built with the compiler in Visual Studio version 15.9 or above (see [PDB crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="74da2-136">Os pacotes de símbolos publicados para NuGet.org falharão na validação se essas restrições não forem atendidas.</span><span class="sxs-lookup"><span data-stu-id="74da2-136">Symbol packages published to NuGet.org will fail validation if these constraints aren't met.</span></span> 

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="74da2-137">Validação e indexação de pacote de símbolos</span><span class="sxs-lookup"><span data-stu-id="74da2-137">Symbol package validation and indexing</span></span>

<span data-ttu-id="74da2-138">Pacotes de símbolos publicados para [NuGet.org](https://www.nuget.org/) passam por várias validações, incluindo a varredura de malware.</span><span class="sxs-lookup"><span data-stu-id="74da2-138">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, including malware scanning.</span></span> <span data-ttu-id="74da2-139">Se um pacote falhar uma verificação de validação, a página de detalhes do pacote exibirá uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="74da2-139">If a package fails a validation check, its package details page will display an error message.</span></span> <span data-ttu-id="74da2-140">Além disso, os proprietários do pacote receberão um e-mail com instruções sobre como corrigir os problemas identificados.</span><span class="sxs-lookup"><span data-stu-id="74da2-140">In addition, the package's owners will receive an email with instructions on how to fix the identified issues.</span></span>

<span data-ttu-id="74da2-141">Quando o pacote de símbolos tiver passado por todas as validações, os símbolos serão indexados pelos servidores símbolo sustais do NuGet.org e estarão disponíveis para consumo.</span><span class="sxs-lookup"><span data-stu-id="74da2-141">When the symbol package has passed all validations, the symbols will be indexed by NuGet.org's symbol servers and will be available for consumption.</span></span>

<span data-ttu-id="74da2-142">A validação e indexação do pacote geralmente leva menos de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="74da2-142">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="74da2-143">Se a publicação do pacote demorar mais do que o esperado, visite [status.nuget.org](https://status.nuget.org/) para verificar se NuGet.org está sofrendo interrupções.</span><span class="sxs-lookup"><span data-stu-id="74da2-143">If the package publishing takes longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="74da2-144">Se todos os sistemas estiverem operacionais e o pacote não tiver sido publicado com êxito dentro de uma hora, faça logon no nuget.org e entre em contato conosco usando o link Entre em contato com o suporte na página de detalhes do pacote.</span><span class="sxs-lookup"><span data-stu-id="74da2-144">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="74da2-145">Estrutura do pacote de símbolos</span><span class="sxs-lookup"><span data-stu-id="74da2-145">Symbol package structure</span></span>

<span data-ttu-id="74da2-146">O pacote de símbolos (.snupkg) tem as seguintes características:</span><span class="sxs-lookup"><span data-stu-id="74da2-146">The symbol package (.snupkg) has the following characteristics:</span></span>

1) <span data-ttu-id="74da2-147">O .snupkg tem o mesmo id e versão que seu pacote NuGet correspondente (.nupkg).</span><span class="sxs-lookup"><span data-stu-id="74da2-147">The .snupkg has the same id and version as its corresponding NuGet package (.nupkg).</span></span>
2) <span data-ttu-id="74da2-148">O .snupkg tem a mesma estrutura de pasta que seu .nupkg correspondente para quaisquer arquivos DLL ou EXE com a distinção de que, em vez de DLLs/EXEs, seus PDBs correspondentes serão incluídos na mesma hierarquia de pastas.</span><span class="sxs-lookup"><span data-stu-id="74da2-148">The .snupkg has the same folder structure as its corresponding .nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="74da2-149">Arquivos e pastas com extensões que não sejam PDB serão deixados de fora do snupkg.</span><span class="sxs-lookup"><span data-stu-id="74da2-149">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="74da2-150">O arquivo .nuspec do pacote `SymbolsPackage` símbolo tem o tipo de pacote:</span><span class="sxs-lookup"><span data-stu-id="74da2-150">The symbol package's .nuspec file has the `SymbolsPackage` package type:</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="74da2-151">Se um autor decide usar um nuspec personalizado para compilar seus nupkg e snupkg, o snupkg deve ter a mesma hierarquia de pastas e arquivos detalhados em 2).</span><span class="sxs-lookup"><span data-stu-id="74da2-151">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="74da2-152">Os seguintes campos serão excluídos da nuspec ```authors```do ```owners``` ```requireLicenseAcceptance```snupkg: , , , ```license type``` ```licenseUrl```e ```icon```.</span><span class="sxs-lookup"><span data-stu-id="74da2-152">The following fields will be excluded from the snupkg's nuspec: ```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl```, and  ```icon```.</span></span>
6) <span data-ttu-id="74da2-153">Não use o elemento ```<license>```.</span><span class="sxs-lookup"><span data-stu-id="74da2-153">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="74da2-154">Um .snupkg é coberto pela mesma licença que o .nupkg correspondente.</span><span class="sxs-lookup"><span data-stu-id="74da2-154">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="74da2-155">Confira também</span><span class="sxs-lookup"><span data-stu-id="74da2-155">See also</span></span>

<span data-ttu-id="74da2-156">Considere usar o Source Link para habilitar a depuração do código fonte dos conjuntos .NET.</span><span class="sxs-lookup"><span data-stu-id="74da2-156">Consider using Source Link to enable source code debugging of .NET assemblies.</span></span> <span data-ttu-id="74da2-157">Para obter mais informações, consulte a [orientação do Link de Origem](/dotnet/standard/library-guidance/sourcelink).</span><span class="sxs-lookup"><span data-stu-id="74da2-157">For more information, please refer to the [Source Link guidance](/dotnet/standard/library-guidance/sourcelink).</span></span>

<span data-ttu-id="74da2-158">Para obter mais informações sobre pacotes de símbolos, consulte a [especificação de design de depuração de & símbolos do pacote NuGet.](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)</span><span class="sxs-lookup"><span data-stu-id="74da2-158">For more information on symbol packages, please refer to the [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) design spec.</span></span>
