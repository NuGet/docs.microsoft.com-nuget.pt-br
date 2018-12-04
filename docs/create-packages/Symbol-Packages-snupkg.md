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
ms.openlocfilehash: 48ca4b62e722988b3dfe69306565d7f159805962
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453449"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="4241b-104">Criando pacotes de símbolos (.snupkg)</span><span class="sxs-lookup"><span data-stu-id="4241b-104">Creating symbol packages (.snupkg)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4241b-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4241b-105">Prerequisites</span></span>

<span data-ttu-id="4241b-106">[NuGet.exe v4.9.0 ou superior](https://www.nuget.org/downloads) ou [dotnet.exe v2.2.0 ou acima](https://www.microsoft.com/net/download/dotnet-core/2.2), que implementam os [protocolos NuGet](../api/nuget-protocols.md) necessários.</span><span class="sxs-lookup"><span data-stu-id="4241b-106">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="4241b-107">Criar um pacote de símbolos</span><span class="sxs-lookup"><span data-stu-id="4241b-107">Creating a symbol package</span></span>

<span data-ttu-id="4241b-108">Um pacote de símbolos snupkg pode ser criado com base em um arquivo .nuspec ou de um arquivo .csproj.</span><span class="sxs-lookup"><span data-stu-id="4241b-108">A snupkg symbol package can be created from a .nuspec file or from a .csproj file.</span></span> <span data-ttu-id="4241b-109">NuGet.exe e dotnet.exe são ambos compatíveis.</span><span class="sxs-lookup"><span data-stu-id="4241b-109">NuGet.exe and dotnet.exe are both supported.</span></span> <span data-ttu-id="4241b-110">Quando as opções ```-Symbols -SymbolPackageFormat snupkg``` são usadas no comando do pacote nuget.exe, um arquivo .snupkg será criado, além do arquivo .nupkg.</span><span class="sxs-lookup"><span data-stu-id="4241b-110">When the options ```-Symbols -SymbolPackageFormat snupkg``` are used on the nuget.exe pack command a .snupkg file will be created in additon to the .nupkg file.</span></span>

<span data-ttu-id="4241b-111">Comandos de exemplo para criar arquivos .snupkg</span><span class="sxs-lookup"><span data-stu-id="4241b-111">Example commands to create .snupkg files</span></span>
```
dotnet pack MyPackage.csproj --include-symbols -p:SymbolPackageFormat=snupkg

nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg

msbuild -t:pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
```

<span data-ttu-id="4241b-112">`.snupkgs` não são produzidos por padrão.</span><span class="sxs-lookup"><span data-stu-id="4241b-112">`.snupkgs` are not produced by default.</span></span> <span data-ttu-id="4241b-113">Você deve passar a propriedade `SymbolPackageFormat` junto com `-Symbols` em caso de nuget.exe, `--include-symbols` em caso de dotnet.exe ou `-p:IncludeSymbols` em caso do msbuild.</span><span class="sxs-lookup"><span data-stu-id="4241b-113">You must pass the `SymbolPackageFormat` property along with `-Symbols` in case of nuget.exe, `--include-symbols` in case of dotnet.exe, or `-p:IncludeSymbols` in case of msbuild.</span></span>

<span data-ttu-id="4241b-114">A propriedade SymbolPackageFormat pode ter um dos dois valores: `symbols.nupkg` (o padrão) ou `snupkg`.</span><span class="sxs-lookup"><span data-stu-id="4241b-114">SymbolPackageFormat property can have one of the two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="4241b-115">Se o SymbolPackageFormat não for especificado, ele assumirá `symbols.nupkg` por padrão e um pacote de símbolos herdados será criado.</span><span class="sxs-lookup"><span data-stu-id="4241b-115">If the SymbolPackageFormat is not specified, it defaults to `symbols.nupkg` and a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="4241b-116">O formato herdado `.symbols.nupkg` ainda é compatível, mas apenas por razões de compatibilidade (veja [Pacotes de símbolos herdados](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="4241b-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="4241b-117">Servidor de símbolos de NuGet.org aceita apenas o novo formato de pacote de símbolos – `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="4241b-117">NuGet.org symbols server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="4241b-118">Publicando um pacote de símbolos</span><span class="sxs-lookup"><span data-stu-id="4241b-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="4241b-119">Para sua conveniência, primeiro salve sua chave de API com o NuGet (veja [Publicar um pacote](../create-packages/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="4241b-119">For convenience, first save your API key with NuGet (see [publish a package](../create-packages/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="4241b-120">Depois de publicar o pacote principal para o nuget.org, envie por push o pacote de símbolos da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="4241b-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="4241b-121">Você também pode efetuar push nos pacotes primário e de símbolos simultaneamente usando o comando abaixo.</span><span class="sxs-lookup"><span data-stu-id="4241b-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="4241b-122">Ambos os arquivos .nupkg e .snupkg precisam estar presentes na pasta atual.</span><span class="sxs-lookup"><span data-stu-id="4241b-122">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="4241b-123">O NuGet publicará ambos os pacotes em nuget.org. O `MyPackage.nupkg` será publicado primeiro, seguido por `MyPackage.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="4241b-123">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="4241b-124">Servidor de símbolos de NuGet.org</span><span class="sxs-lookup"><span data-stu-id="4241b-124">NuGet.org symbol server</span></span>

<span data-ttu-id="4241b-125">O NuGet.org dá suporte a seu próprio repositório de servidor de símbolos e aceita apenas o novo formato de pacote de símbolos – `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="4241b-125">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="4241b-126">Os consumidores de pacote podem usar os símbolos publicados no servidor de símbolos nuget.org adicionando `https://symbols.nuget.org/download/symbols` às suas origens de símbolos no Visual Studio, o que permite intervir no código do pacote no depurador do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4241b-126">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="4241b-127">Consulte [Especificar símbolos (.pdb) e arquivos de origem no depurador do Visual Studio](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) para obter mais detalhes sobre esse processo.</span><span class="sxs-lookup"><span data-stu-id="4241b-127">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="4241b-128">Restrições de pacote de símbolos do nuget.org</span><span class="sxs-lookup"><span data-stu-id="4241b-128">Nuget.org symbol package constraints</span></span>

<span data-ttu-id="4241b-129">Os pacotes de símbolos compatíveis com o nuget.org têm as restrições a seguir</span><span class="sxs-lookup"><span data-stu-id="4241b-129">The symbol packages supported on nuget.org have the following contraints</span></span>

- <span data-ttu-id="4241b-130">Somente as extensões de arquivo a seguir podem ser adicionadas a um pacote de símbolos.</span><span class="sxs-lookup"><span data-stu-id="4241b-130">Only the following file extensions are allowed to be added to a symbol package.</span></span> ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- <span data-ttu-id="4241b-131">Somente [Pdbs portáteis](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) gerenciados são compatíveis com o servidor de símbolos do nuget atualmente.</span><span class="sxs-lookup"><span data-stu-id="4241b-131">Only managed [Portable pdbs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are currently supported on nuget symbol server.</span></span>
- <span data-ttu-id="4241b-132">Os pdbs e dlls do nupkg associados precisam ser compilados com o compilador no Visual Studio versão 15.9 ou superior (veja [hash de criptografia de pdb](https://github.com/dotnet/roslyn/issues/24429))</span><span class="sxs-lookup"><span data-stu-id="4241b-132">The pdbs and associated nupkg dlls need to be built with the compiler in Visual Studio version 15.9 or above (see [pdb crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="4241b-133">A publicação de pacote de símbolos no nuget.org falhará se qualquer outro tipo de arquivo for incluído no .snupkg.</span><span class="sxs-lookup"><span data-stu-id="4241b-133">The symbol package publish on nuget.org will fail if any other file types are included in the .snupkg.</span></span>

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="4241b-134">Validação e indexação de pacote de símbolos</span><span class="sxs-lookup"><span data-stu-id="4241b-134">Symbol package validation and indexing</span></span>

<span data-ttu-id="4241b-135">Os pacotes de símbolos publicados em [NuGet.org](https://www.nuget.org/) passam por várias validações, tais como verificações de vírus.</span><span class="sxs-lookup"><span data-stu-id="4241b-135">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, such as virus checks.</span></span>

<span data-ttu-id="4241b-136">Quando o pacote tiver passado todas as verificações de validação, pode levar algum tempo para que os símbolos sejam indexados e estejam disponíveis para consumo nos servidores de símbolos do NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="4241b-136">When the package has passed all validation checks, it might take a while for the symbols to index and be available for consumption from the NuGet.org symbol servers.</span></span> <span data-ttu-id="4241b-137">Se a verificação de validação do pacote falhar, a página de detalhes do pacote para o .nupkg será atualizada para exibir o erro associado e você também receberá um email notificando-o sobre isso.</span><span class="sxs-lookup"><span data-stu-id="4241b-137">If the package fails a validation check, the package details page for the .nupkg will update to display the associated error and you will also receive an email notifying you about it.</span></span>

<span data-ttu-id="4241b-138">A validação e indexação do pacote geralmente leva menos de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="4241b-138">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="4241b-139">Se a publicação do pacote estiver demorando mais do que o esperado, visite [status.nuget.org](https://status.nuget.org/) para verificar se o nuget.org está passando por alguma interrupção.</span><span class="sxs-lookup"><span data-stu-id="4241b-139">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="4241b-140">Se todos os sistemas estiverem operacionais e o pacote não tiver sido publicado com êxito dentro de uma hora, faça logon no nuget.org e entre em contato conosco usando o link Entre em contato com o suporte na página de detalhes do pacote.</span><span class="sxs-lookup"><span data-stu-id="4241b-140">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="4241b-141">Estrutura do pacote de símbolos</span><span class="sxs-lookup"><span data-stu-id="4241b-141">Symbol package structure</span></span>

<span data-ttu-id="4241b-142">O arquivo .nupkg seria exatamente o mesmo como está hoje, mas o arquivo .snupkg teria as seguintes características:</span><span class="sxs-lookup"><span data-stu-id="4241b-142">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="4241b-143">O .snupkg terá a mesma ID e versão que o .nupkg correspondente.</span><span class="sxs-lookup"><span data-stu-id="4241b-143">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="4241b-144">O .snupkg terá exatamente a mesma a estrutura de pasta que o nupkg para todos os arquivos DLL ou EXE, com a diferença que, em vez de DLLs/EXEs, seus PDBs correspondentes serão incluídos na mesma hierarquia de pastas.</span><span class="sxs-lookup"><span data-stu-id="4241b-144">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="4241b-145">Arquivos e pastas com extensões que não sejam PDB serão deixados de fora do snupkg.</span><span class="sxs-lookup"><span data-stu-id="4241b-145">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="4241b-146">O arquivo .nuspec no .snupkg também especificará um novo PackageType, conforme mostrado a seguir.</span><span class="sxs-lookup"><span data-stu-id="4241b-146">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="4241b-147">Isso deve ser o único PackageType especificado.</span><span class="sxs-lookup"><span data-stu-id="4241b-147">This should the only one PackageType specified.</span></span> 
``` 
<packageTypes>
  <packageType name="SymbolsPackage"/>
</packageTypes>
```
4) <span data-ttu-id="4241b-148">Se um autor decide usar um nuspec personalizado para compilar seus nupkg e snupkg, o snupkg deve ter a mesma hierarquia de pastas e arquivos detalhados em 2).</span><span class="sxs-lookup"><span data-stu-id="4241b-148">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="4241b-149">O campo ```authors``` e ```owners``` será excluído do nuspec do snupkg.</span><span class="sxs-lookup"><span data-stu-id="4241b-149">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>

## <a name="see-also"></a><span data-ttu-id="4241b-150">Consulte também</span><span class="sxs-lookup"><span data-stu-id="4241b-150">See Also</span></span>

[<span data-ttu-id="4241b-151">NuGet-Package-Debugging-&-Symbols-Improvements</span><span class="sxs-lookup"><span data-stu-id="4241b-151">NuGet-Package-Debugging-&-Symbols-Improvements</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
