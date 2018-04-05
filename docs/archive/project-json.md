---
title: Referência do arquivo project.json para NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/27/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Em alguns tipos de projeto, o project.json mantém a lista de pacotes do NuGet usados no projeto.
keywords: Project.json do NuGet, referências de pacote do NuGet, dependências do NuGet, project.lock.json
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 21542a219faa3d1fa0c32a838645d4471c5aa935
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="projectjson-reference"></a><span data-ttu-id="9b0f0-104">Referência do project.json</span><span class="sxs-lookup"><span data-stu-id="9b0f0-104">project.json reference</span></span>

<span data-ttu-id="9b0f0-105">*NuGet 3.x ou superior*</span><span class="sxs-lookup"><span data-stu-id="9b0f0-105">*NuGet 3.x+*</span></span>

<span data-ttu-id="9b0f0-106">O arquivo `project.json` mantém uma lista de pacotes usados em um projeto, conhecidos como um formato de gerenciamento de pacote.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-106">The `project.json` file maintains a list of packages used in a project, known as a package management format.</span></span> <span data-ttu-id="9b0f0-107">Ele substitui `packages.config`, mas é, por sua vez substituído por [PackageReference](../consume-packages/package-references-in-project-files.md) com o NuGet 4.0 e superior.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-107">It supersedes `packages.config` but is in turn superseded by [PackageReference](../consume-packages/package-references-in-project-files.md) with NuGet 4.0+.</span></span>

<span data-ttu-id="9b0f0-108">O arquivo [`project.lock.json`](#projectlockjson) (descrito abaixo) também é usado em projetos que empregam o `project.json`.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-108">The [`project.lock.json`](#projectlockjson) file (described below) is also used in projects employing `project.json`.</span></span>

<span data-ttu-id="9b0f0-109">`project.json` tem a seguinte estrutura básica, em que cada um dos quatro objetos de nível superior pode ter qualquer número de objetos filho:</span><span class="sxs-lookup"><span data-stu-id="9b0f0-109">`project.json` has the following basic structure, where each of the four top-level objects can have any number of child objects:</span></span>

```json
{
    "dependencies": {
        "PackageID" : "{version_constraint}"
    },
    "frameworks" : {
        "TxM" : {}
    },
    "runtimes" : {
        "RID": {}
    },
    "supports" : {
        "CompatibilityProfile" : {}
    }
}
```

## <a name="dependencies"></a><span data-ttu-id="9b0f0-110">Dependências</span><span class="sxs-lookup"><span data-stu-id="9b0f0-110">Dependencies</span></span>

<span data-ttu-id="9b0f0-111">Lista as dependências de pacote do NuGet do seu projeto no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="9b0f0-111">Lists the NuGet package dependencies of your project in the following form:</span></span>

```json
"PackageID" : "version_constraint"
```

<span data-ttu-id="9b0f0-112">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9b0f0-112">For example:</span></span>

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

<span data-ttu-id="9b0f0-113">É na seção `dependencies` que a caixa de diálogo do Gerenciador de Pacotes do NuGet adiciona as dependências de pacote ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-113">The `dependencies` section is where the NuGet Package Manager dialog adds package dependencies to your project.</span></span>

<span data-ttu-id="9b0f0-114">A id do pacote corresponde à id do pacote no nuget.org, que é a mesma usada no console do gerenciador de pacotes: `Install-Package Microsoft.NETCore`.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-114">The Package id corresponds to the id of the package on nuget.org , the same as the id used in the package manager console: `Install-Package Microsoft.NETCore`.</span></span>

<span data-ttu-id="9b0f0-115">Ao restaurar pacotes, a restrição de versão do `"5.0.0"` implica em `>= 5.0.0`.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-115">When restoring packages, the version constraint of `"5.0.0"` implies `>= 5.0.0`.</span></span> <span data-ttu-id="9b0f0-116">Ou seja, se 5.0.0 não estiver disponível no servidor, mas o 5.0.1 sim, o NuGet instala o 5.0.1 e avisa sobre o upgrade.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-116">That is, if 5.0.0 is not available on the server but 5.0.1 is, NuGet installs  5.0.1 and warns you about the upgrade.</span></span> <span data-ttu-id="9b0f0-117">Caso contrário, o NuGet escolhe a versão mais antiga possível no servidor correspondente à restrição.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-117">NuGet otherwise picks the lowest possible version on the server matching the constraint.</span></span>

<span data-ttu-id="9b0f0-118">Consulte [Resolução de dependência](../consume-packages/dependency-resolution.md) para obter mais detalhes sobre as regras de resolução.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-118">See [Dependency resolution](../consume-packages/dependency-resolution.md) for more details on resolution rules.</span></span>

### <a name="managing-dependency-assets"></a><span data-ttu-id="9b0f0-119">Gerenciamento de ativos de dependência</span><span class="sxs-lookup"><span data-stu-id="9b0f0-119">Managing dependency assets</span></span>

<span data-ttu-id="9b0f0-120">Quais ativos do fluxo de dependências para o projeto de nível superior é controlado pela especificação de um conjunto de marcas delimitado por vírgulas nas propriedades `include` e `exclude` da referência de dependência.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-120">Which assets from dependencies flow into the top-level project is controlled by specifying a comma-delimited set of tags in the `include` and `exclude` properties of the dependency reference.</span></span> <span data-ttu-id="9b0f0-121">As marcas são listadas na tabela abaixo:</span><span class="sxs-lookup"><span data-stu-id="9b0f0-121">The tags are listed the table below:</span></span>

| <span data-ttu-id="9b0f0-122">Marca Incluir/Excluir</span><span class="sxs-lookup"><span data-stu-id="9b0f0-122">Include/Exclude tag</span></span> | <span data-ttu-id="9b0f0-123">Pastas afetadas do destino</span><span class="sxs-lookup"><span data-stu-id="9b0f0-123">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="9b0f0-124">contentFiles</span><span class="sxs-lookup"><span data-stu-id="9b0f0-124">contentFiles</span></span> | <span data-ttu-id="9b0f0-125">Conteúdo</span><span class="sxs-lookup"><span data-stu-id="9b0f0-125">Content</span></span>  |
| <span data-ttu-id="9b0f0-126">tempo de execução</span><span class="sxs-lookup"><span data-stu-id="9b0f0-126">runtime</span></span> | <span data-ttu-id="9b0f0-127">Runtime, Resources e FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="9b0f0-127">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="9b0f0-128">compilar</span><span class="sxs-lookup"><span data-stu-id="9b0f0-128">compile</span></span> | <span data-ttu-id="9b0f0-129">lib</span><span class="sxs-lookup"><span data-stu-id="9b0f0-129">lib</span></span> |
| <span data-ttu-id="9b0f0-130">build</span><span class="sxs-lookup"><span data-stu-id="9b0f0-130">build</span></span> | <span data-ttu-id="9b0f0-131">build (objetos e destinos do MSBuild)</span><span class="sxs-lookup"><span data-stu-id="9b0f0-131">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="9b0f0-132">nativa</span><span class="sxs-lookup"><span data-stu-id="9b0f0-132">native</span></span> | <span data-ttu-id="9b0f0-133">nativa</span><span class="sxs-lookup"><span data-stu-id="9b0f0-133">native</span></span> |
| <span data-ttu-id="9b0f0-134">nenhum</span><span class="sxs-lookup"><span data-stu-id="9b0f0-134">none</span></span> | <span data-ttu-id="9b0f0-135">Nenhuma pasta</span><span class="sxs-lookup"><span data-stu-id="9b0f0-135">No folders</span></span> |
| <span data-ttu-id="9b0f0-136">all</span><span class="sxs-lookup"><span data-stu-id="9b0f0-136">all</span></span> | <span data-ttu-id="9b0f0-137">Todas as pastas</span><span class="sxs-lookup"><span data-stu-id="9b0f0-137">All folders</span></span> |

<span data-ttu-id="9b0f0-138">Marcas especificadas com `exclude` têm precedência sobre aquelas especificadas com `include`.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-138">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="9b0f0-139">Por exemplo, `include="runtime, compile" exclude="compile"` é o mesmo que `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-139">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span>

<span data-ttu-id="9b0f0-140">Por exemplo, para incluir as pastas `build` e `native` de uma dependência, use o seguinte:</span><span class="sxs-lookup"><span data-stu-id="9b0f0-140">For example, to include the `build` and `native` folders of a dependency, use the following:</span></span>

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "include": "build, native"
    }
  }
}
```

<span data-ttu-id="9b0f0-141">Para excluir as pastas `content` e `build` de uma dependência, use o seguinte:</span><span class="sxs-lookup"><span data-stu-id="9b0f0-141">To exclude the `content` and `build` folders of a dependency, use the following:</span></span>

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "exclude": "contentFiles, build"
    }
  }
}
```

## <a name="frameworks"></a><span data-ttu-id="9b0f0-142">Estruturas</span><span class="sxs-lookup"><span data-stu-id="9b0f0-142">Frameworks</span></span>

<span data-ttu-id="9b0f0-143">Lista as estruturas em que o projeto é executado, como `net45`, `netcoreapp`, `netstandard`.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-143">Lists the frameworks that the project runs on, such as `net45`, `netcoreapp`, `netstandard`.</span></span>

```json
"frameworks": {
    "netcore50": {}
    }
 ```

<span data-ttu-id="9b0f0-144">Somente uma única entrada é permitida na seção `frameworks`.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-144">Only a single entry is allowed in the `frameworks` section.</span></span> <span data-ttu-id="9b0f0-145">(Uma exceção são os arquivos `project.json` para projetos do ASP.NET compilados com a cadeia de ferramentas DNX preterida, o que permite considerar vários destinos).</span><span class="sxs-lookup"><span data-stu-id="9b0f0-145">(An exception is `project.json` files for ASP.NET projects that are build with deprecated DNX tool chain, which allows for multiple targets.)</span></span>

## <a name="runtimes"></a><span data-ttu-id="9b0f0-146">Tempos de execução</span><span class="sxs-lookup"><span data-stu-id="9b0f0-146">Runtimes</span></span>

<span data-ttu-id="9b0f0-147">Lista os sistemas operacionais e arquiteturas nos quais seu aplicativo é executado, como `win10-arm`, `win8-x64`, `win8-x86`.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-147">Lists the operating systems and architectures that your app runs on, such as `win10-arm`, `win8-x64`, `win8-x86`.</span></span>

```json
"runtimes": {
    "win10-arm": { },
    "win10-arm-aot": { },
    "win10-x86": { },
    "win10-x86-aot": { },
    "win10-x64": { },
    "win10-x64-aot": { }
}
```

<span data-ttu-id="9b0f0-148">Um pacote que contém um PCL que pode ser executado em qualquer tempo de execução não precisa especificar um tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-148">A package containing a PCL that can run on any runtime doesn't need to specify a runtime.</span></span> <span data-ttu-id="9b0f0-149">Isso também deve ser verdadeiro para todas as dependências, caso contrário, você precisará especificar tempos de execução.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-149">This must also be true of any dependencies, otherwise you must specify runtimes.</span></span>


## <a name="supports"></a><span data-ttu-id="9b0f0-150">Suporte</span><span class="sxs-lookup"><span data-stu-id="9b0f0-150">Supports</span></span>

<span data-ttu-id="9b0f0-151">Define um conjunto de verificações para as dependências de pacote.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-151">Defines a set of checks for package dependencies.</span></span> <span data-ttu-id="9b0f0-152">Você pode definir onde você espera que o PCL ou aplicativo seja executado.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-152">You can define where you expect the PCL or app to run.</span></span> <span data-ttu-id="9b0f0-153">As definições não são restritivas, visto que seu código pode ser capaz de ser executado em outro lugar.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-153">The definitions are not restrictive, as your code may be able to run elsewhere.</span></span> <span data-ttu-id="9b0f0-154">Porém, especificar essas verificações faz o NuGet verificar se todas as dependências são atendidas nos TxMs listados.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-154">But specifying these checks makes NuGet check that all dependencies are satisfied on the listed TxMs.</span></span> <span data-ttu-id="9b0f0-155">Exemplos de valores para isso problema são: `net46.app`, `uwp.10.0.app`, etc.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-155">Examples of the values for this are: `net46.app`, `uwp.10.0.app`, etc.</span></span>

<span data-ttu-id="9b0f0-156">Esta seção deve ser populada automaticamente quando você seleciona uma entrada na caixa de diálogo de destinos da Biblioteca de Classes Portátil.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-156">This section should be populated automatically when you select an entry in the Portable Class Library targets dialog.</span></span>

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a><span data-ttu-id="9b0f0-157">Importações</span><span class="sxs-lookup"><span data-stu-id="9b0f0-157">Imports</span></span>

<span data-ttu-id="9b0f0-158">Importações foram desenvolvidas para permitir que os pacotes que usam o `dotnet` TxM operem com pacotes que não declaram um dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-158">Imports are designed to allow packages that use the `dotnet` TxM to operate with packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="9b0f0-159">Se seu projeto usa o `dotnet` TxM, todos os pacotes dos quais você depende também precisam ter um `project.json` TxM, a menos que você adicione o seguinte ao seu `dotnet` para permitir que plataformas não `dotnet` sejam compatíveis com o `dotnet`:</span><span class="sxs-lookup"><span data-stu-id="9b0f0-159">If your project is using the `dotnet` TxM then all the packages you depend on must also have a `dotnet` TxM, unless you add the following to your `project.json` to allow non `dotnet` platforms to be compatible with `dotnet`:</span></span>

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

<span data-ttu-id="9b0f0-160">Se você estiver usando o `dotnet` TxM, o sistema do projeto PCL adiciona a instrução `imports` apropriada com base nos destinos compatíveis.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-160">If you are using the `dotnet` TxM then the PCL project system adds the appropriate `imports` statement based on the supported targets.</span></span>

## <a name="differences-from-portable-apps-and-web-projects"></a><span data-ttu-id="9b0f0-161">Diferenças entre aplicativos portáteis e projetos Web</span><span class="sxs-lookup"><span data-stu-id="9b0f0-161">Differences from portable apps and web projects</span></span>

<span data-ttu-id="9b0f0-162">O arquivo `project.json` usado pelo NuGet é um subconjunto do que é encontrado em projetos do ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-162">The `project.json` file used by NuGet is a subset of that found in ASP.NET Core projects.</span></span> <span data-ttu-id="9b0f0-163">No ASP.NET Core, o `project.json` é usado para metadados do projeto, informações de compilação e dependências.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-163">In ASP.NET Core `project.json` is used for project metadata, compilation information, and dependencies.</span></span> <span data-ttu-id="9b0f0-164">Quando usado em outros sistemas de projeto, essas três coisas são divididas em arquivos separados e o `project.json` contém menos informações.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-164">When used in other project systems, those three things are split into separate files and `project.json` contains less information.</span></span> <span data-ttu-id="9b0f0-165">As diferenças notáveis incluem:</span><span class="sxs-lookup"><span data-stu-id="9b0f0-165">Notable differences include:</span></span>

- <span data-ttu-id="9b0f0-166">Pode haver somente uma estrutura na seção `frameworks`.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-166">There can only be one framework in the `frameworks` section.</span></span>

- <span data-ttu-id="9b0f0-167">O arquivo não pode conter dependências, opções de compilação, etc. que são vistos nos arquivos `project.json` de DNX.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-167">The file cannot contain dependencies, compilation options, etc. that you see in DNX `project.json` files.</span></span> <span data-ttu-id="9b0f0-168">Considerando que pode haver apenas uma única estrutura, não faz sentido inserir dependências específicas de estrutura.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-168">Given that there can only be a single framework it doesn't make sense to enter framework-specific dependencies.</span></span>

- <span data-ttu-id="9b0f0-169">O build é tratada pelo MSBuild, por isso as opções de build, definições do pré-processador, etc. fazem parte do arquivo de projeto do MSBuild e não de `project.json`.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-169">Compilation is handled by MSBuild so compilation options, preprocessor defines, etc. are all part of the MSBuild project file and not `project.json`.</span></span>

<span data-ttu-id="9b0f0-170">No NuGet 3 ou superior, não é esperado que os desenvolvedores editem o `project.json` manualmente, visto que a interface do usuário do Gerenciador de Pacotes no Visual Studio manipula o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-170">In NuGet 3+, developers are not expected to manually edit the `project.json`, as the Package Manager UI in Visual Studio manipulates the content.</span></span> <span data-ttu-id="9b0f0-171">Dito isso, você certamente pode editar o arquivo, mas será preciso compilar o projeto para iniciar uma restauração de pacote ou invocar a restauração de outra maneira.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-171">That said, you can certainly edit the file, but you must build the project to start a package restore or invoke restore in another way.</span></span> <span data-ttu-id="9b0f0-172">Consulte [Restauração de pacote](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="9b0f0-172">See [Package restore](../consume-packages/package-restore.md).</span></span>


## <a name="projectlockjson"></a><span data-ttu-id="9b0f0-173">project.lock.json</span><span class="sxs-lookup"><span data-stu-id="9b0f0-173">project.lock.json</span></span>

<span data-ttu-id="9b0f0-174">O arquivo `project.lock.json` é gerado no processo de restauração de pacotes do NuGet em projetos que usam `project.json`.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-174">The `project.lock.json` file is generated in the process of restoring the NuGet packages in projects that use `project.json`.</span></span> <span data-ttu-id="9b0f0-175">Ele contém um instantâneo de todas as informações geradas à medida que o NuGet percorre o grafo de pacotes e inclui a versão, conteúdo e as dependências de todos os pacotes em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-175">It holds a snapshot of all the information that is generated as NuGet walks the graph of packages and includes the version, contents, and dependencies of all the packages in your project.</span></span> <span data-ttu-id="9b0f0-176">O sistema de build usa isso para escolher os pacotes de uma localização global que são relevantes ao compilar o projeto em vez de depender de uma pasta de pacotes local no projeto em si.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-176">The build system uses this to choose packages from a global location that are relevant when building the project instead of depending on a local packages folder in the project itself.</span></span> <span data-ttu-id="9b0f0-177">Isso resulta em desempenho mais rápido de build porque é necessário ler somente `project.lock.json` em vez de muitos arquivos `.nuspec` separados.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-177">This results in faster build performance because it's necessary to read only `project.lock.json` instead of many separate `.nuspec` files.</span></span>

<span data-ttu-id="9b0f0-178">`project.lock.json` é gerado automaticamente na restauração do pacote, por isso ele pode ser omitido do controle do código-fonte adicionando-o aos arquivos `.gitignore` e `.tfignore` (consulte [Pacotes e controle do código-fonte](../consume-packages/packages-and-source-control.md).</span><span class="sxs-lookup"><span data-stu-id="9b0f0-178">`project.lock.json` is automatically generated on package restore, so it can be omitted from source control by adding it to `.gitignore` and `.tfignore` files (see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> <span data-ttu-id="9b0f0-179">No entanto, se você incluí-lo no controle do código-fonte, o histórico de alterações mostrará as alterações em dependências resolvidas ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="9b0f0-179">However, if you include it in source control, the change history shows changes in dependencies resolved over time.</span></span>
