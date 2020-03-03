---
title: Definir um tipo de pacote NuGet
description: Descreve os tipos de pacotes para indicar o uso pretendido de um pacote.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 1d869f616ce0291cf1c0a17b7ff20fc61e6a3bd5
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230818"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="bfeed-103">Definir um tipo de pacote NuGet</span><span class="sxs-lookup"><span data-stu-id="bfeed-103">Set a NuGet package type</span></span>

<span data-ttu-id="bfeed-104">Com o NuGet 3.5 ou superior, os pacotes podem ser marcados com um *tipo de pacote* específico para indicar o uso pretendido.</span><span class="sxs-lookup"><span data-stu-id="bfeed-104">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="bfeed-105">Pacotes não marcados com um tipo, incluindo todos os pacotes criados com versões anteriores do NuGet, usam o tipo `Dependency` como padrão.</span><span class="sxs-lookup"><span data-stu-id="bfeed-105">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="bfeed-106">Pacotes do tipo `Dependency` adicionam ativos de tempo de build ou de execução a bibliotecas e aplicativos e podem ser instalados em qualquer tipo de projeto (supondo que eles sejam compatíveis).</span><span class="sxs-lookup"><span data-stu-id="bfeed-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="bfeed-107">Pacotes do tipo `DotnetTool` são extensões para a [CLI do .NET](/dotnet/articles/core/tools/index) e são invocados na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="bfeed-107">`DotnetTool` type packages are extensions to the [dotnet CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="bfeed-108">Esses pacotes podem ser instalados somente em projetos do .NET Core e não têm nenhum efeito sobre operações de restauração.</span><span class="sxs-lookup"><span data-stu-id="bfeed-108">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="bfeed-109">Mais detalhes sobre essas extensões por projeto estão disponíveis na documentação da [extensibilidade do .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility).</span><span class="sxs-lookup"><span data-stu-id="bfeed-109">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="bfeed-110">pacotes de tipo de `Template` fornecem [modelos personalizados](/dotnet/core/tools/custom-templates) que podem ser usados para criar arquivos ou projetos como um aplicativo, serviço, ferramenta ou biblioteca de classes.</span><span class="sxs-lookup"><span data-stu-id="bfeed-110">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

- <span data-ttu-id="bfeed-111">Pacotes de tipo personalizado usam um identificador de tipo arbitrário que está em conformidade com as mesmas regras de formato que as IDs de pacote.</span><span class="sxs-lookup"><span data-stu-id="bfeed-111">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="bfeed-112">Qualquer tipo diferente de `Dependency` e `DotnetTool`, no entanto, não é reconhecido pelo Gerenciador de Pacotes do NuGet no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bfeed-112">Any type other than `Dependency` and `DotnetTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="bfeed-113">Os tipos de pacote são definidos no arquivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="bfeed-113">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="bfeed-114">É melhor para compatibilidade com versões anteriores *não* definir explicitamente o tipo `Dependency` e, em vez disso, contar com o NuGet, supondo este tipo quando nenhum tipo é especificado.</span><span class="sxs-lookup"><span data-stu-id="bfeed-114">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="bfeed-115">`.nuspec`: indica o tipo de pacote em um nó `packageTypes\packageType` sob o elemento `<metadata>`:</span><span class="sxs-lookup"><span data-stu-id="bfeed-115">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
