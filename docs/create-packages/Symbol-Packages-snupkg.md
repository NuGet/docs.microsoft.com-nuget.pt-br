---
title: Como publicar pacotes de símbolos do NuGet usando o novo formato de pacote de símbolos '.snupkg' | Microsoft Docs
author:
- cristinamanu
- kraigb
ms.author:
- cristinamanu
- kraigb
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
ms.openlocfilehash: 0d82cf8614b88247bc3a3ba3019c11bf1b5e2593
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426798"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="6b57c-104">Criando pacotes de símbolos (.snupkg)</span><span class="sxs-lookup"><span data-stu-id="6b57c-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="6b57c-105">Os pacotes de símbolos permitem melhorar a experiência de depuração dos pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="6b57c-105">Symbol packages allow you to improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b57c-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6b57c-106">Prerequisites</span></span>

<span data-ttu-id="6b57c-107">[NuGet.exe v4.9.0 ou superior](https://www.nuget.org/downloads) ou [dotnet.exe v2.2.0 ou acima](https://www.microsoft.com/net/download/dotnet-core/2.2), que implementam os [protocolos NuGet](../api/nuget-protocols.md) necessários.</span><span class="sxs-lookup"><span data-stu-id="6b57c-107">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="6b57c-108">Criar um pacote de símbolos</span><span class="sxs-lookup"><span data-stu-id="6b57c-108">Creating a symbol package</span></span>

<span data-ttu-id="6b57c-109">Você pode criar um pacote de símbolos snupkg usando o dotnet.exe, o NuGet.exe ou o MSBuild.</span><span class="sxs-lookup"><span data-stu-id="6b57c-109">You can create a snupkg symbol package using dotnet.exe, NuGet.exe, or MSBuild.</span></span> <span data-ttu-id="6b57c-110">Se estiver usando o NuGet.exe, use os seguintes comandos para criar um arquivo .snupkg além do arquivo .nupkg:</span><span class="sxs-lookup"><span data-stu-id="6b57c-110">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="6b57c-111">Se estiver usando o dotnet.exe ou o MSBuild, siga as seguintes etapas para criar um arquivo .snupkg além do arquivo .nupkg:</span><span class="sxs-lookup"><span data-stu-id="6b57c-111">If you're using dotnet.exe or MSBuild, use the following steps to create a .snupkg file in addition to the .nupkg file:</span></span>

1. <span data-ttu-id="6b57c-112">Adicione as seguintes propriedades ao arquivo .csproj:</span><span class="sxs-lookup"><span data-stu-id="6b57c-112">Add the following properties to your .csproj file:</span></span>

    ```xml
    <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
    </PropertyGroup>
    ```

1. <span data-ttu-id="6b57c-113">Empacote o projeto com `dotnet pack MyPackage.csproj` ou `msbuild -t:pack MyPackage.csproj`.</span><span class="sxs-lookup"><span data-stu-id="6b57c-113">Pack your project with `dotnet pack MyPackage.csproj` or `msbuild -t:pack MyPackage.csproj`.</span></span>

<span data-ttu-id="6b57c-114">A propriedade [`SymbolPackageFormat`](/dotnet/core/tools/csproj.md#symbolpackageformat) pode ter um destes dois valores: `symbols.nupkg` (o padrão) ou `snupkg`.</span><span class="sxs-lookup"><span data-stu-id="6b57c-114">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj.md#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="6b57c-115">Se a propriedade [`SymbolPackageFormat`](/dotnet/core/tools/csproj.md#symbolpackageformat) não for especificada, um pacote de símbolos herdados será criado.</span><span class="sxs-lookup"><span data-stu-id="6b57c-115">If the [`SymbolPackageFormat`](/dotnet/core/tools/csproj.md#symbolpackageformat) property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="6b57c-116">O formato herdado `.symbols.nupkg` ainda é compatível, mas apenas por razões de compatibilidade (veja [Pacotes de símbolos herdados](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="6b57c-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="6b57c-117">O servidor de símbolos da NuGet.org aceita apenas o novo formato de pacote de símbolos – `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="6b57c-117">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="6b57c-118">Publicando um pacote de símbolos</span><span class="sxs-lookup"><span data-stu-id="6b57c-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="6b57c-119">Para sua conveniência, primeiro salve sua chave de API com o NuGet (veja [Publicar um pacote](../nuget-org/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="6b57c-119">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="6b57c-120">Depois de publicar o pacote principal para o nuget.org, envie por push o pacote de símbolos da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="6b57c-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="6b57c-121">Você também pode efetuar push nos pacotes primário e de símbolos simultaneamente usando o comando abaixo.</span><span class="sxs-lookup"><span data-stu-id="6b57c-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="6b57c-122">Ambos os arquivos .nupkg e .snupkg precisam estar presentes na pasta atual.</span><span class="sxs-lookup"><span data-stu-id="6b57c-122">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="6b57c-123">O NuGet publicará ambos os pacotes em nuget.org. O `MyPackage.nupkg` será publicado primeiro, seguido por `MyPackage.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="6b57c-123">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="6b57c-124">Se o pacote de símbolos não for publicado, verifique se você configurou a fonte de NuGet.org como `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="6b57c-124">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="6b57c-125">A publicação de pacote de símbolos tem compatibilidade apenas [na API do NuGet V3](../api/overview.md#versioning).</span><span class="sxs-lookup"><span data-stu-id="6b57c-125">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="6b57c-126">Servidor de símbolos de NuGet.org</span><span class="sxs-lookup"><span data-stu-id="6b57c-126">NuGet.org symbol server</span></span>

<span data-ttu-id="6b57c-127">O NuGet.org dá suporte a seu próprio repositório de servidor de símbolos e aceita apenas o novo formato de pacote de símbolos – `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="6b57c-127">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="6b57c-128">Os consumidores de pacote podem usar os símbolos publicados no servidor de símbolos nuget.org adicionando `https://symbols.nuget.org/download/symbols` às suas origens de símbolos no Visual Studio, o que permite intervir no código do pacote no depurador do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6b57c-128">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="6b57c-129">Consulte [Especificar símbolos (.pdb) e arquivos de origem no depurador do Visual Studio](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) para obter mais detalhes sobre esse processo.</span><span class="sxs-lookup"><span data-stu-id="6b57c-129">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="6b57c-130">Restrições de pacote de símbolos do nuget.org</span><span class="sxs-lookup"><span data-stu-id="6b57c-130">Nuget.org symbol package constraints</span></span>

<span data-ttu-id="6b57c-131">Os pacotes de símbolos compatíveis com o nuget.org têm as restrições a seguir</span><span class="sxs-lookup"><span data-stu-id="6b57c-131">The symbol packages supported on nuget.org have the following contraints</span></span>

- <span data-ttu-id="6b57c-132">Somente as extensões de arquivo a seguir podem ser adicionadas a um pacote de símbolos.</span><span class="sxs-lookup"><span data-stu-id="6b57c-132">Only the following file extensions are allowed to be added to a symbol package.</span></span> ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- <span data-ttu-id="6b57c-133">Somente [Pdbs portáteis](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) gerenciados são compatíveis com o servidor de símbolos do nuget atualmente.</span><span class="sxs-lookup"><span data-stu-id="6b57c-133">Only managed [Portable pdbs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are currently supported on nuget symbol server.</span></span>
- <span data-ttu-id="6b57c-134">Os pdbs e dlls do nupkg associados precisam ser compilados com o compilador no Visual Studio versão 15.9 ou superior (veja [hash de criptografia de pdb](https://github.com/dotnet/roslyn/issues/24429))</span><span class="sxs-lookup"><span data-stu-id="6b57c-134">The pdbs and associated nupkg dlls need to be built with the compiler in Visual Studio version 15.9 or above (see [pdb crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="6b57c-135">A publicação de pacote de símbolos no nuget.org falhará se qualquer outro tipo de arquivo for incluído no .snupkg.</span><span class="sxs-lookup"><span data-stu-id="6b57c-135">The symbol package publish on nuget.org will fail if any other file types are included in the .snupkg.</span></span>

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="6b57c-136">Validação e indexação de pacote de símbolos</span><span class="sxs-lookup"><span data-stu-id="6b57c-136">Symbol package validation and indexing</span></span>

<span data-ttu-id="6b57c-137">Os pacotes de símbolos publicados em [NuGet.org](https://www.nuget.org/) passam por várias validações, tais como verificações de vírus.</span><span class="sxs-lookup"><span data-stu-id="6b57c-137">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, such as virus checks.</span></span>

<span data-ttu-id="6b57c-138">Quando o pacote tiver passado todas as verificações de validação, pode levar algum tempo para que os símbolos sejam indexados e estejam disponíveis para consumo nos servidores de símbolos do NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="6b57c-138">When the package has passed all validation checks, it might take a while for the symbols to index and be available for consumption from the NuGet.org symbol servers.</span></span> <span data-ttu-id="6b57c-139">Se a verificação de validação do pacote falhar, a página de detalhes do pacote para o .nupkg será atualizada para exibir o erro associado e você também receberá um email notificando-o sobre isso.</span><span class="sxs-lookup"><span data-stu-id="6b57c-139">If the package fails a validation check, the package details page for the .nupkg will update to display the associated error and you will also receive an email notifying you about it.</span></span>

<span data-ttu-id="6b57c-140">A validação e indexação do pacote geralmente leva menos de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="6b57c-140">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="6b57c-141">Se a publicação do pacote estiver demorando mais do que o esperado, visite [status.nuget.org](https://status.nuget.org/) para verificar se o nuget.org está passando por alguma interrupção.</span><span class="sxs-lookup"><span data-stu-id="6b57c-141">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="6b57c-142">Se todos os sistemas estiverem operacionais e o pacote não tiver sido publicado com êxito dentro de uma hora, faça logon no nuget.org e entre em contato conosco usando o link Entre em contato com o suporte na página de detalhes do pacote.</span><span class="sxs-lookup"><span data-stu-id="6b57c-142">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="6b57c-143">Estrutura do pacote de símbolos</span><span class="sxs-lookup"><span data-stu-id="6b57c-143">Symbol package structure</span></span>

<span data-ttu-id="6b57c-144">O arquivo .nupkg seria exatamente o mesmo como está hoje, mas o arquivo .snupkg teria as seguintes características:</span><span class="sxs-lookup"><span data-stu-id="6b57c-144">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="6b57c-145">O .snupkg terá a mesma ID e versão que o .nupkg correspondente.</span><span class="sxs-lookup"><span data-stu-id="6b57c-145">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="6b57c-146">O .snupkg terá exatamente a mesma a estrutura de pasta que o nupkg para todos os arquivos DLL ou EXE, com a diferença que, em vez de DLLs/EXEs, seus PDBs correspondentes serão incluídos na mesma hierarquia de pastas.</span><span class="sxs-lookup"><span data-stu-id="6b57c-146">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="6b57c-147">Arquivos e pastas com extensões que não sejam PDB serão deixados de fora do snupkg.</span><span class="sxs-lookup"><span data-stu-id="6b57c-147">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="6b57c-148">O arquivo .nuspec no .snupkg também especificará um novo PackageType, conforme mostrado a seguir.</span><span class="sxs-lookup"><span data-stu-id="6b57c-148">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="6b57c-149">Isso deve ser o único PackageType especificado.</span><span class="sxs-lookup"><span data-stu-id="6b57c-149">This should the only one PackageType specified.</span></span> 
``` 
<packageTypes>
  <packageType name="SymbolsPackage"/>
</packageTypes>
```
4) <span data-ttu-id="6b57c-150">Se um autor decide usar um nuspec personalizado para compilar seus nupkg e snupkg, o snupkg deve ter a mesma hierarquia de pastas e arquivos detalhados em 2).</span><span class="sxs-lookup"><span data-stu-id="6b57c-150">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="6b57c-151">O campo ```authors``` e ```owners``` será excluído do nuspec do snupkg.</span><span class="sxs-lookup"><span data-stu-id="6b57c-151">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>

## <a name="see-also"></a><span data-ttu-id="6b57c-152">Veja também</span><span class="sxs-lookup"><span data-stu-id="6b57c-152">See Also</span></span>

[<span data-ttu-id="6b57c-153">NuGet-Package-Debugging-&-Symbols-Improvements</span><span class="sxs-lookup"><span data-stu-id="6b57c-153">NuGet-Package-Debugging-&-Symbols-Improvements</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
