---
title: Criando pacotes de símbolo herdados (. Symbols. nupkg)
description: Como criar pacotes do NuGet que contêm apenas os símbolos compatíveis com a depuração de outros pacotes do NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 374e9ccfc01cd06508e76529765db3f849342222
ms.sourcegitcommit: 1799d4ac23c8aacee7498fdc72c40dd1646d267b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77476263"
---
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a><span data-ttu-id="88fa9-103">Criando pacotes de símbolo herdados (. Symbols. nupkg)</span><span class="sxs-lookup"><span data-stu-id="88fa9-103">Creating legacy symbol packages (.symbols.nupkg)</span></span>

> [!Important]
> <span data-ttu-id="88fa9-104">O novo formato recomendado para pacotes de símbolos é .snupkg.</span><span class="sxs-lookup"><span data-stu-id="88fa9-104">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="88fa9-105">Veja [Criando pacotes de símbolos (.snupkg)](Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="88fa9-105">See [Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md).</span></span> </br>
> <span data-ttu-id="88fa9-106">.symbols.nupkg ainda é compatível, mas exclusivamente por razões de compatibilidade.</span><span class="sxs-lookup"><span data-stu-id="88fa9-106">.symbols.nupkg is still supported but only for compatibility reasons.</span></span>

<span data-ttu-id="88fa9-107">Além de criar pacotes para nuget.org ou outras fontes, o NuGet também dá suporte à criação de pacotes de símbolo associados que podem ser publicados em servidores de símbolos.</span><span class="sxs-lookup"><span data-stu-id="88fa9-107">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages that can be published to symbol servers.</span></span> <span data-ttu-id="88fa9-108">O formato de pacote de símbolo herdado,. Symbols. nupkg, pode ser enviado por push para o repositório de simbolismo.</span><span class="sxs-lookup"><span data-stu-id="88fa9-108">The legacy symbol package format, .symbols.nupkg, can be pushed to the SymbolSource repository.</span></span>

<span data-ttu-id="88fa9-109">Os consumidores de pacote podem adicionar `https://nuget.smbsrc.net` às suas origens de símbolos no Visual Studio, o que permite intervir no código do pacote no depurador do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="88fa9-109">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="88fa9-110">Consulte [Especificar símbolos (.pdb) e arquivos de origem no depurador do Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) para obter mais detalhes sobre esse processo.</span><span class="sxs-lookup"><span data-stu-id="88fa9-110">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-legacy-symbol-package"></a><span data-ttu-id="88fa9-111">Criando um pacote de símbolos herdado</span><span class="sxs-lookup"><span data-stu-id="88fa9-111">Creating a legacy symbol package</span></span>

<span data-ttu-id="88fa9-112">Para criar um pacote de símbolos herdado, siga estas convenções:</span><span class="sxs-lookup"><span data-stu-id="88fa9-112">To create a legacy symbol package, follow these conventions:</span></span>

- <span data-ttu-id="88fa9-113">Nomeie o pacote primário (com o seu código) `{identifier}.nupkg` e inclua todos os arquivos, exceto os arquivos `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="88fa9-113">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="88fa9-114">Nomeie o pacote de símbolo herdado `{identifier}.symbols.nupkg` e inclua sua DLL de assembly, arquivos de `.pdb`, arquivos XMLDOC, arquivos de origem (consulte as seções a seguir).</span><span class="sxs-lookup"><span data-stu-id="88fa9-114">Name the legacy symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="88fa9-115">Você pode criar pacotes com a opção `-Symbols` de um arquivo `.nuspec` ou um arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="88fa9-115">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="88fa9-116">Observe que `pack` requer o Mono 4.4.2 no Mac OS X e não funciona em sistemas Linux.</span><span class="sxs-lookup"><span data-stu-id="88fa9-116">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="88fa9-117">Em um Mac, você também precisa converter os nomes de caminho do Windows no arquivo `.nuspec` em caminhos no estilo Unix.</span><span class="sxs-lookup"><span data-stu-id="88fa9-117">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="legacy-symbol-package-structure"></a><span data-ttu-id="88fa9-118">Estrutura de pacote de símbolo herdado</span><span class="sxs-lookup"><span data-stu-id="88fa9-118">Legacy symbol package structure</span></span>

<span data-ttu-id="88fa9-119">Um pacote de símbolos herdado pode ser direcionado a várias estruturas de destino da mesma forma que um pacote de biblioteca, de modo que a estrutura da pasta de `lib` deve ser exatamente a mesma que a do pacote primário, incluindo `.pdb` arquivos juntamente com a DLL.</span><span class="sxs-lookup"><span data-stu-id="88fa9-119">A legacy symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="88fa9-120">Por exemplo, um pacote de símbolos herdado que tem como alvo o .NET 4,0 e o Silverlight 4 teria esse layout:</span><span class="sxs-lookup"><span data-stu-id="88fa9-120">For example, a legacy symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="88fa9-121">Arquivos de origem são, então, colocados em uma pasta especial separada chamada `src`, que precisa seguir a estrutura relativa do repositório de origem.</span><span class="sxs-lookup"><span data-stu-id="88fa9-121">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="88fa9-122">Isso ocorre porque PDBs contêm caminhos absolutos para arquivos de origem usados para compilar a DLL correspondente e eles precisam ser encontrados durante o processo de publicação.</span><span class="sxs-lookup"><span data-stu-id="88fa9-122">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="88fa9-123">Um caminho base (prefixo de caminho comum) pode ser eliminado. Por exemplo, considere uma biblioteca criada com base nesses arquivos:</span><span class="sxs-lookup"><span data-stu-id="88fa9-123">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

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

<span data-ttu-id="88fa9-124">Além da pasta `lib`, um pacote de símbolos herdado precisaria conter esse layout:</span><span class="sxs-lookup"><span data-stu-id="88fa9-124">Apart from the `lib` folder, a legacy symbol package would need to contain this layout:</span></span>

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

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="88fa9-125">Fazendo referência a arquivos no nuspec</span><span class="sxs-lookup"><span data-stu-id="88fa9-125">Referring to files in the nuspec</span></span>

<span data-ttu-id="88fa9-126">Um pacote de símbolos herdado pode ser criado por convenções, de uma estrutura de pastas, conforme descrito na seção anterior, ou especificando seu conteúdo na seção `files` do manifesto.</span><span class="sxs-lookup"><span data-stu-id="88fa9-126">A legacy symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="88fa9-127">Por exemplo, para compilar o pacote mostrado na seção anterior, use o seguinte no arquivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="88fa9-127">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a><span data-ttu-id="88fa9-128">Publicando um pacote de símbolos herdado</span><span class="sxs-lookup"><span data-stu-id="88fa9-128">Publishing a legacy symbol package</span></span>

> [!Important]
> <span data-ttu-id="88fa9-129">Para enviar pacotes para o nuget.org, você deve usar o [nuget.exe v4.9.1 ou posterior](https://www.nuget.org/downloads), que implementa os [protocolos NuGet](../api/nuget-protocols.md) necessários.</span><span class="sxs-lookup"><span data-stu-id="88fa9-129">To push packages to nuget.org you must use [nuget.exe v4.9.1 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="88fa9-130">Para sua conveniência, primeiro salve sua chave de API com o NuGet (consulte [publicar um pacote](../nuget-org/publish-a-package.md), que aplicará nuget.org e symbolsource.org, pois symbolsource.org verificará nuget.org para confirmar se você é o proprietário do pacote.</span><span class="sxs-lookup"><span data-stu-id="88fa9-130">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="88fa9-131">Depois de publicar o pacote primário no nuget.org, envie por push o pacote de símbolos herdado da seguinte maneira, que usará automaticamente o symbolsource.org como o destino devido ao `.symbols` no nome do arquivo:</span><span class="sxs-lookup"><span data-stu-id="88fa9-131">After publishing your primary package to nuget.org, push the legacy symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="88fa9-132">Para publicar em um repositório de símbolos diferente ou enviar por push um pacote de símbolos herdado que não segue a Convenção de nomenclatura, use a opção `-Source`:</span><span class="sxs-lookup"><span data-stu-id="88fa9-132">To publish to a different symbol repository, or to push a legacy symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="88fa9-133">Você também pode efetuar push nos pacotes primário e de símbolos para ambos os repositórios ao mesmo tempo usando o seguinte:</span><span class="sxs-lookup"><span data-stu-id="88fa9-133">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="88fa9-134">Com o NuGet. exe 4.5.0 ou superior, os pacotes de símbolos não são enviados automaticamente para symbolsource.org. Você precisaria enviar os pacotes de símbolos separadamente, conforme explicado nas etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="88fa9-134">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the earlier steps.</span></span>
   
<span data-ttu-id="88fa9-135">Nesse caso, o NuGet publicará `MyPackage.symbols.nupkg`, se presente, em https://nuget.smbsrc.net/ (a URL de push para symbolsource.org), depois de publicar o pacote principal em nuget.org.</span><span class="sxs-lookup"><span data-stu-id="88fa9-135">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="88fa9-136">Confira também</span><span class="sxs-lookup"><span data-stu-id="88fa9-136">See also</span></span>

* <span data-ttu-id="88fa9-137">[Criando pacotes de símbolo (. snupkg)](Symbol-Packages-snupkg.md) -o novo formato recomendado para pacotes de símbolo</span><span class="sxs-lookup"><span data-stu-id="88fa9-137">[Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md) - The new recommended format for symbol packages</span></span>
* <span data-ttu-id="88fa9-138">[Mover para o novo mecanismo de SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="88fa9-138">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
