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
ms.openlocfilehash: 0197902e4dbc18893d68833fbcfe4263f185a594
ms.sourcegitcommit: e4b0ff4460865db6dc7bc9f20e9f644d98493011
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71307182"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="1820a-104">Criando pacotes de símbolos (.snupkg)</span><span class="sxs-lookup"><span data-stu-id="1820a-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="1820a-105">Os pacotes de símbolos permitem melhorar a experiência de depuração dos pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="1820a-105">Symbol packages allow you to improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1820a-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1820a-106">Prerequisites</span></span>

<span data-ttu-id="1820a-107">[NuGet.exe v4.9.0 ou superior](https://www.nuget.org/downloads) ou [dotnet.exe v2.2.0 ou acima](https://www.microsoft.com/net/download/dotnet-core/2.2), que implementam os [protocolos NuGet](../api/nuget-protocols.md) necessários.</span><span class="sxs-lookup"><span data-stu-id="1820a-107">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="1820a-108">Criar um pacote de símbolos</span><span class="sxs-lookup"><span data-stu-id="1820a-108">Creating a symbol package</span></span>

<span data-ttu-id="1820a-109">Se você estiver usando dotNet. exe ou MSBuild, precisará definir as `IncludeSymbols` Propriedades e `SymbolPackageFormat` para criar um arquivo. snupkg além do arquivo. nupkg.</span><span class="sxs-lookup"><span data-stu-id="1820a-109">If you're using dotnet.exe or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="1820a-110">Adicione as seguintes propriedades ao seu arquivo. csproj:</span><span class="sxs-lookup"><span data-stu-id="1820a-110">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols> 
      <SymbolPackageFormat>snupkg</SymbolPackageFormat> 
   </PropertyGroup>
   ```

* <span data-ttu-id="1820a-111">Ou especifique essas propriedades na linha de comando:</span><span class="sxs-lookup"><span data-stu-id="1820a-111">Or specify these properties on the command-line:</span></span>

     ```cli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="1820a-112">ou</span><span class="sxs-lookup"><span data-stu-id="1820a-112">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="1820a-113">Se estiver usando o NuGet.exe, use os seguintes comandos para criar um arquivo .snupkg além do arquivo .nupkg:</span><span class="sxs-lookup"><span data-stu-id="1820a-113">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="1820a-114">A propriedade [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) pode ter um destes dois valores: `symbols.nupkg` (o padrão) ou `snupkg`.</span><span class="sxs-lookup"><span data-stu-id="1820a-114">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="1820a-115">Se essa propriedade não for especificada, um pacote de símbolos herdado será criado.</span><span class="sxs-lookup"><span data-stu-id="1820a-115">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="1820a-116">O formato herdado `.symbols.nupkg` ainda é compatível, mas apenas por razões de compatibilidade (veja [Pacotes de símbolos herdados](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="1820a-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="1820a-117">O servidor de símbolos da NuGet.org aceita apenas o novo formato de pacote de símbolos – `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="1820a-117">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="1820a-118">Publicando um pacote de símbolos</span><span class="sxs-lookup"><span data-stu-id="1820a-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="1820a-119">Para sua conveniência, primeiro salve sua chave de API com o NuGet (veja [Publicar um pacote](../nuget-org/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="1820a-119">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="1820a-120">Depois de publicar o pacote principal para o nuget.org, envie por push o pacote de símbolos da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="1820a-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="1820a-121">Você também pode efetuar push nos pacotes primário e de símbolos simultaneamente usando o comando abaixo.</span><span class="sxs-lookup"><span data-stu-id="1820a-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="1820a-122">Ambos os arquivos .nupkg e .snupkg precisam estar presentes na pasta atual.</span><span class="sxs-lookup"><span data-stu-id="1820a-122">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="1820a-123">O NuGet publicará ambos os pacotes em nuget.org. O `MyPackage.nupkg` será publicado primeiro, seguido por `MyPackage.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="1820a-123">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="1820a-124">Se o pacote de símbolos não for publicado, verifique se você configurou a fonte de NuGet.org como `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="1820a-124">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="1820a-125">A publicação de pacote de símbolos tem compatibilidade apenas [na API do NuGet V3](../api/overview.md#versioning).</span><span class="sxs-lookup"><span data-stu-id="1820a-125">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="1820a-126">Servidor de símbolos de NuGet.org</span><span class="sxs-lookup"><span data-stu-id="1820a-126">NuGet.org symbol server</span></span>

<span data-ttu-id="1820a-127">O NuGet.org dá suporte a seu próprio repositório de servidor de símbolos e aceita apenas o novo formato de pacote de símbolos – `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="1820a-127">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="1820a-128">Os consumidores de pacote podem usar os símbolos publicados no servidor de símbolos nuget.org adicionando `https://symbols.nuget.org/download/symbols` às suas origens de símbolos no Visual Studio, o que permite intervir no código do pacote no depurador do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1820a-128">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="1820a-129">Consulte [Especificar símbolos (.pdb) e arquivos de origem no depurador do Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) para obter mais detalhes sobre esse processo.</span><span class="sxs-lookup"><span data-stu-id="1820a-129">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="1820a-130">Restrições de pacote de símbolos NuGet.org</span><span class="sxs-lookup"><span data-stu-id="1820a-130">NuGet.org symbol package constraints</span></span>

<span data-ttu-id="1820a-131">NuGet.org tem as seguintes restrições para pacotes de símbolo:</span><span class="sxs-lookup"><span data-stu-id="1820a-131">NuGet.org has the following constraints for symbol packages:</span></span>

- <span data-ttu-id="1820a-132">Somente as seguintes extensões de arquivo são permitidas em pacotes `.pdb`de `.nuspec`símbolos `.xml`: `.psmdcp`, `.rels`,,,,`.p7s`</span><span class="sxs-lookup"><span data-stu-id="1820a-132">Only the following file extensions are allowed in symbol packages: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span></span>
- <span data-ttu-id="1820a-133">Somente os [PDBs portáteis](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) gerenciados têm suporte no servidor de símbolos do NuGet. org.</span><span class="sxs-lookup"><span data-stu-id="1820a-133">Only managed [Portable PDBs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are supported on NuGet.org's symbol server.</span></span>
- <span data-ttu-id="1820a-134">O PDBs e suas DLLs. nupkg associadas precisam ser compilados com o compilador no Visual Studio versão 15,9 ou superior (consulte o [hash de criptografia PDB](https://github.com/dotnet/roslyn/issues/24429))</span><span class="sxs-lookup"><span data-stu-id="1820a-134">The PDBs and their associated .nupkg DLLs need to be built with the compiler in Visual Studio version 15.9 or above (see [PDB crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="1820a-135">Os pacotes de símbolo publicados no NuGet.org falharão na validação se essas restrições não forem atendidas.</span><span class="sxs-lookup"><span data-stu-id="1820a-135">Symbol packages published to NuGet.org will fail validation if these constraints aren't met.</span></span> 

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="1820a-136">Validação e indexação de pacote de símbolos</span><span class="sxs-lookup"><span data-stu-id="1820a-136">Symbol package validation and indexing</span></span>

<span data-ttu-id="1820a-137">Os pacotes de símbolos publicados no [NuGet.org](https://www.nuget.org/) passam por várias validações, incluindo a verificação de malware.</span><span class="sxs-lookup"><span data-stu-id="1820a-137">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, including malware scanning.</span></span> <span data-ttu-id="1820a-138">Se um pacote falhar em uma verificação de validação, a página de detalhes do pacote exibirá uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="1820a-138">If a package fails a validation check, its package details page will display an error message.</span></span> <span data-ttu-id="1820a-139">Além disso, os proprietários do pacote receberão um email com instruções sobre como corrigir os problemas identificados.</span><span class="sxs-lookup"><span data-stu-id="1820a-139">In addition, the package's owners will receive an email with instructions on how to fix the identified issues.</span></span>

<span data-ttu-id="1820a-140">Quando o pacote de símbolos tiver passado por todas as validações, os símbolos serão indexados pelos servidores de símbolos do NuGet. org.</span><span class="sxs-lookup"><span data-stu-id="1820a-140">When the symbol package has passed all validations, the symbols will be indexed by NuGet.org's symbol servers.</span></span> <span data-ttu-id="1820a-141">Depois de indexar, o símbolo estará disponível para consumo dos servidores de símbolos NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="1820a-141">Once indexed, the symbol will be available for consumption from the NuGet.org symbol servers.</span></span>

<span data-ttu-id="1820a-142">A validação e indexação do pacote geralmente leva menos de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="1820a-142">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="1820a-143">Se a publicação do pacote estiver demorando mais do que o esperado, visite [status.nuget.org](https://status.nuget.org/) para verificar se o NuGet.org está passando por alguma interrupção.</span><span class="sxs-lookup"><span data-stu-id="1820a-143">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="1820a-144">Se todos os sistemas estiverem operacionais e o pacote não tiver sido publicado com êxito dentro de uma hora, faça logon no nuget.org e entre em contato conosco usando o link Entre em contato com o suporte na página de detalhes do pacote.</span><span class="sxs-lookup"><span data-stu-id="1820a-144">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="1820a-145">Estrutura do pacote de símbolos</span><span class="sxs-lookup"><span data-stu-id="1820a-145">Symbol package structure</span></span>

<span data-ttu-id="1820a-146">O arquivo .nupkg seria exatamente o mesmo como está hoje, mas o arquivo .snupkg teria as seguintes características:</span><span class="sxs-lookup"><span data-stu-id="1820a-146">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="1820a-147">O .snupkg terá a mesma ID e versão que o .nupkg correspondente.</span><span class="sxs-lookup"><span data-stu-id="1820a-147">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="1820a-148">O .snupkg terá exatamente a mesma a estrutura de pasta que o nupkg para todos os arquivos DLL ou EXE, com a diferença que, em vez de DLLs/EXEs, seus PDBs correspondentes serão incluídos na mesma hierarquia de pastas.</span><span class="sxs-lookup"><span data-stu-id="1820a-148">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="1820a-149">Arquivos e pastas com extensões que não sejam PDB serão deixados de fora do snupkg.</span><span class="sxs-lookup"><span data-stu-id="1820a-149">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="1820a-150">O arquivo .nuspec no .snupkg também especificará um novo PackageType, conforme mostrado a seguir.</span><span class="sxs-lookup"><span data-stu-id="1820a-150">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="1820a-151">Isso deve ser o único PackageType especificado.</span><span class="sxs-lookup"><span data-stu-id="1820a-151">This should the only one PackageType specified.</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="1820a-152">Se um autor decide usar um nuspec personalizado para compilar seus nupkg e snupkg, o snupkg deve ter a mesma hierarquia de pastas e arquivos detalhados em 2).</span><span class="sxs-lookup"><span data-stu-id="1820a-152">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="1820a-153">O campo ```authors``` e ```owners``` será excluído do nuspec do snupkg.</span><span class="sxs-lookup"><span data-stu-id="1820a-153">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>
6) <span data-ttu-id="1820a-154">Não use o elemento ```<license>```.</span><span class="sxs-lookup"><span data-stu-id="1820a-154">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="1820a-155">Um .snupkg é coberto pela mesma licença que o .nupkg correspondente.</span><span class="sxs-lookup"><span data-stu-id="1820a-155">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="1820a-156">Consulte também</span><span class="sxs-lookup"><span data-stu-id="1820a-156">See Also</span></span>

<span data-ttu-id="1820a-157">Considere usar o link de origem para habilitar a depuração de código-fonte de assemblies .NET.</span><span class="sxs-lookup"><span data-stu-id="1820a-157">Consider using Source Link to enable source code debugging of .NET assemblies.</span></span> <span data-ttu-id="1820a-158">Para obter mais informações, consulte as [diretrizes de link de origem](/dotnet/standard/library-guidance/sourcelink).</span><span class="sxs-lookup"><span data-stu-id="1820a-158">For more information, please refer to the [Source Link guidance](/dotnet/standard/library-guidance/sourcelink).</span></span>

<span data-ttu-id="1820a-159">Para obter mais informações sobre pacotes de símbolos, consulte a [depuração do pacote NuGet &](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) a especificação de design de melhorias de símbolos.</span><span class="sxs-lookup"><span data-stu-id="1820a-159">For more information on symbol packages, please refer to the [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) design spec.</span></span>
