---
title: Como criar pacotes de símbolos do NuGet
description: Como criar pacotes do NuGet que contêm apenas os símbolos compatíveis com a depuração de outros pacotes do NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 97a533171d698792d66a78550dacfe8eaf29a440
ms.sourcegitcommit: fc0f8c950829ee5c96e3f3f32184bc727714cfdb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2019
ms.locfileid: "74253909"
---
# <a name="creating-symbol-packages-legacy"></a><span data-ttu-id="4003c-103">Criando pacotes de símbolos (herdado)</span><span class="sxs-lookup"><span data-stu-id="4003c-103">Creating symbol packages (legacy)</span></span>

> [!Important]
> <span data-ttu-id="4003c-104">O novo formato recomendado para pacotes de símbolos é .snupkg.</span><span class="sxs-lookup"><span data-stu-id="4003c-104">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="4003c-105">Veja [Criando pacotes de símbolos (.snupkg)](Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="4003c-105">See [Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md).</span></span> </br>
> <span data-ttu-id="4003c-106">.symbols.nupkg ainda é compatível, mas exclusivamente por razões de compatibilidade.</span><span class="sxs-lookup"><span data-stu-id="4003c-106">.symbols.nupkg is still supported but only for compatibility reasons.</span></span>

<span data-ttu-id="4003c-107">Além de compilar pacotes para nuget.org ou outras origens, o NuGet também dá suporte à criação de pacotes de símbolos associados e publica-os no repositório SymbolSource.</span><span class="sxs-lookup"><span data-stu-id="4003c-107">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages and publishing them to the SymbolSource repository.</span></span>

<span data-ttu-id="4003c-108">Os consumidores de pacote podem adicionar `https://nuget.smbsrc.net` às suas origens de símbolos no Visual Studio, o que permite intervir no código do pacote no depurador do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4003c-108">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="4003c-109">Consulte [Especificar símbolos (.pdb) e arquivos de origem no depurador do Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) para obter mais detalhes sobre esse processo.</span><span class="sxs-lookup"><span data-stu-id="4003c-109">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="4003c-110">Criar um pacote de símbolos</span><span class="sxs-lookup"><span data-stu-id="4003c-110">Creating a symbol package</span></span>

<span data-ttu-id="4003c-111">Para criar um pacote de símbolos, siga essas convenções:</span><span class="sxs-lookup"><span data-stu-id="4003c-111">To create a symbol package, follow these conventions:</span></span>

- <span data-ttu-id="4003c-112">Nomeie o pacote primário (com o seu código) `{identifier}.nupkg` e inclua todos os arquivos, exceto os arquivos `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="4003c-112">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="4003c-113">Nomeie o pacote de símbolos `{identifier}.symbols.nupkg` e inclua sua DLL de assembly, arquivos `.pdb`, arquivos XMLDOC, arquivos de origem (consulte as seções a seguir).</span><span class="sxs-lookup"><span data-stu-id="4003c-113">Name the symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="4003c-114">Você pode criar pacotes com a opção `-Symbols` de um arquivo `.nuspec` ou um arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="4003c-114">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="4003c-115">Observe que `pack` requer o Mono 4.4.2 no Mac OS X e não funciona em sistemas Linux.</span><span class="sxs-lookup"><span data-stu-id="4003c-115">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="4003c-116">Em um Mac, você também precisa converter os nomes de caminho do Windows no arquivo `.nuspec` em caminhos no estilo Unix.</span><span class="sxs-lookup"><span data-stu-id="4003c-116">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="4003c-117">Estrutura do pacote de símbolos</span><span class="sxs-lookup"><span data-stu-id="4003c-117">Symbol package structure</span></span>

<span data-ttu-id="4003c-118">Um pacote de símbolos pode ser direcionado a várias estruturas de destino da mesma maneira que um pacote de biblioteca, portanto, a estrutura da pasta `lib` deve ser exatamente a mesma que o pacote primário, incluindo somente arquivos `.pdb` junto com a DLL.</span><span class="sxs-lookup"><span data-stu-id="4003c-118">A symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="4003c-119">Por exemplo, um pacote de símbolos voltado para o .NET 4.0 e o Silverlight 4 teria este layout:</span><span class="sxs-lookup"><span data-stu-id="4003c-119">For example, a symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="4003c-120">Arquivos de origem são, então, colocados em uma pasta especial separada chamada `src`, que precisa seguir a estrutura relativa do repositório de origem.</span><span class="sxs-lookup"><span data-stu-id="4003c-120">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="4003c-121">Isso ocorre porque PDBs contêm caminhos absolutos para arquivos de origem usados para compilar a DLL correspondente e eles precisam ser encontrados durante o processo de publicação.</span><span class="sxs-lookup"><span data-stu-id="4003c-121">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="4003c-122">Um caminho base (prefixo de caminho comum) pode ser eliminado. Por exemplo, considere uma biblioteca criada com base nesses arquivos:</span><span class="sxs-lookup"><span data-stu-id="4003c-122">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

    C:\Projects
        \MyProject
            \Common
                \MyClass.cs
            \Full
                \Properties
                    \AssemblyInfo.cs
                \MyAssembly.csproj (producing \lib\net40\MyAssembly.dll)
            \Silverlight
                \Properties
                    \AssemblyInfo.cs
                \MySilverlightExtensions.cs
                \MyAssembly.csproj (producing \lib\sl4\MyAssembly.dll)

<span data-ttu-id="4003c-123">Além da pasta `lib`, um pacote de símbolos precisaria conter este layout:</span><span class="sxs-lookup"><span data-stu-id="4003c-123">Apart from the `lib` folder, a symbol package would need to contain this layout:</span></span>

    \src
        \Common
            \MyClass.cs
        \Full
            \Properties
                \AssemblyInfo.cs
        \Silverlight
            \Properties
                \AssemblyInfo.cs
            \MySilverlightExtensions.cs

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="4003c-124">Fazendo referência a arquivos no nuspec</span><span class="sxs-lookup"><span data-stu-id="4003c-124">Referring to files in the nuspec</span></span>

<span data-ttu-id="4003c-125">Um pacote de símbolos pode ser compilado por convenções, de uma estrutura de pasta conforme descrito na seção anterior ou especificando o conteúdo na seção `files` do manifesto.</span><span class="sxs-lookup"><span data-stu-id="4003c-125">A symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="4003c-126">Por exemplo, para compilar o pacote mostrado na seção anterior, use o seguinte no arquivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="4003c-126">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="4003c-127">Publicando um pacote de símbolos</span><span class="sxs-lookup"><span data-stu-id="4003c-127">Publishing a symbol package</span></span>

> [!Important]
> <span data-ttu-id="4003c-128">Para enviar pacotes para o nuget.org, você deve usar o [nuget.exe v4.9.1 ou posterior](https://www.nuget.org/downloads), que implementa os [protocolos NuGet](../api/nuget-protocols.md) necessários.</span><span class="sxs-lookup"><span data-stu-id="4003c-128">To push packages to nuget.org you must use [nuget.exe v4.9.1 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="4003c-129">Para sua conveniência, primeiro salve sua chave de API com o NuGet (consulte [publicar um pacote](../nuget-org/publish-a-package.md), que aplicará nuget.org e symbolsource.org, pois symbolsource.org verificará nuget.org para confirmar se você é o proprietário do pacote.</span><span class="sxs-lookup"><span data-stu-id="4003c-129">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="4003c-130">Depois de publicar o pacote principal no nuget.org, efetue push do pacote de símbolos como mostrado a seguir, que usará automaticamente symbolsource.org como o destino devido ao `.symbols` no nome de arquivo:</span><span class="sxs-lookup"><span data-stu-id="4003c-130">After publishing your primary package to nuget.org, push the symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="4003c-131">Para publicar em um repositório de símbolos diferente ou para efetuar push em um pacote de símbolos que não segue a convenção de nomenclatura, use a opção `-Source`:</span><span class="sxs-lookup"><span data-stu-id="4003c-131">To publish to a different symbol repository, or to push a symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="4003c-132">Você também pode efetuar push nos pacotes primário e de símbolos para ambos os repositórios ao mesmo tempo usando o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4003c-132">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="4003c-133">Com o NuGet. exe 4.5.0 ou superior, os pacotes de símbolos não são enviados automaticamente para symbolsource.org. Você precisaria enviar os pacotes de símbolos separadamente, conforme explicado nas etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="4003c-133">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the earlier steps.</span></span>
   
<span data-ttu-id="4003c-134">Nesse caso, o NuGet publicará `MyPackage.symbols.nupkg`, se presente, em https://nuget.smbsrc.net/ (a URL de push para symbolsource.org), depois de publicar o pacote principal em nuget.org.</span><span class="sxs-lookup"><span data-stu-id="4003c-134">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="4003c-135">Consulte também</span><span class="sxs-lookup"><span data-stu-id="4003c-135">See also</span></span>

<span data-ttu-id="4003c-136">[Mover para o novo mecanismo de SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="4003c-136">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
