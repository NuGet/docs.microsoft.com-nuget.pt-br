---
title: Suporte do NuGet para o sistema de projeto do Visual Studio
description: Integração do NuGet ao sistema de projeto do Visual Studio para tipos de projetos de terceiros.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: 00a64d95c943e9e5cb3a279358a6495125a1bd87
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64495928"
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a><span data-ttu-id="72889-103">Suporte do NuGet para o sistema de projetos do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="72889-103">NuGet support for the Visual Studio project system</span></span>

<span data-ttu-id="72889-104">Para dar suporte a tipos de projeto de terceiros no Visual Studio, o NuGet 3.x e superior dá suporte a [CPS (Common Project System)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md) e o NuGet 3.2 e superior também dá suporte a sistemas de projeto não CPS.</span><span class="sxs-lookup"><span data-stu-id="72889-104">To support third-party project types in Visual Studio, NuGet 3.x+ supports the [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), and NuGet 3.2+ supports non-CPS project systems as well.</span></span>

<span data-ttu-id="72889-105">Para integrar-se ao NuGet, um sistema de projeto deve anunciar seu próprio suporte para todos os recursos de projeto descritos neste tópico.</span><span class="sxs-lookup"><span data-stu-id="72889-105">To integrate with NuGet, a project system must advertise its own support for all the project capabilities described in this topic.</span></span>

> [!Note]
> <span data-ttu-id="72889-106">Não declare recursos que seu projeto efetivamente não contém visando habilitar pacotes para instalação no seu projeto.</span><span class="sxs-lookup"><span data-stu-id="72889-106">Don't declare capabilities that your project does not actually have for the sake of enabling packages to install in your project.</span></span> <span data-ttu-id="72889-107">Muitos recursos do Visual Studio e outras extensões dependem de recursos de projeto, além do cliente do NuGet.</span><span class="sxs-lookup"><span data-stu-id="72889-107">Many features of Visual Studio and other extensions depend on project capabilities besides the NuGet client.</span></span> <span data-ttu-id="72889-108">Anunciar falsamente recursos do seu projeto pode levar esses componentes a funcionarem incorretamente e degradar a experiência dos usuários.</span><span class="sxs-lookup"><span data-stu-id="72889-108">Falsely advertising capabilities of your project can lead these components to malfunction and your users' experience to degrade.</span></span>

## <a name="advertise-project-capabilities"></a><span data-ttu-id="72889-109">Anunciar funcionalidades do projeto</span><span class="sxs-lookup"><span data-stu-id="72889-109">Advertise project capabilities</span></span>

<span data-ttu-id="72889-110">O cliente do NuGet determina quais pacotes são compatíveis com o tipo de projeto com base nos [recursos do projeto](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), conforme descrito na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="72889-110">The NuGet client determines which packages are compatible with your project type based on the [project's capabilities](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), as described in the following table.</span></span>

| <span data-ttu-id="72889-111">Recurso</span><span class="sxs-lookup"><span data-stu-id="72889-111">Capability</span></span> | <span data-ttu-id="72889-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="72889-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="72889-113">AssemblyReferences</span><span class="sxs-lookup"><span data-stu-id="72889-113">AssemblyReferences</span></span> | <span data-ttu-id="72889-114">Indica que o projeto é compatível com referências de assembly (diferentes de WinRTReferences).</span><span class="sxs-lookup"><span data-stu-id="72889-114">Indicates that the project supports assembly references (distinct from WinRTReferences).</span></span> |
| <span data-ttu-id="72889-115">DeclaredSourceItems</span><span class="sxs-lookup"><span data-stu-id="72889-115">DeclaredSourceItems</span></span> | <span data-ttu-id="72889-116">Indica que o projeto é um projeto típico do MSBuild (não DNX) em que ele declara itens de origem no próprio projeto.</span><span class="sxs-lookup"><span data-stu-id="72889-116">Indicates that the project is a typical MSBuild project (not DNX) in that it declares source items in the project itself.</span></span> |
| <span data-ttu-id="72889-117">UserSourceItems</span><span class="sxs-lookup"><span data-stu-id="72889-117">UserSourceItems</span></span>|<span data-ttu-id="72889-118">Indica que o usuário tem permissão para adicionar arquivos arbitrários ao projeto dele.</span><span class="sxs-lookup"><span data-stu-id="72889-118">Indicates that the user is allowed to add arbitrary files to their project.</span></span> |

<span data-ttu-id="72889-119">Para sistemas de projeto baseados em CPS, os detalhes de implementação para recursos de projeto descritos no restante desta seção já foram feitos para você.</span><span class="sxs-lookup"><span data-stu-id="72889-119">For CPS-based project systems, the implementation details for project capabilities described in the rest of this section have been done for you.</span></span> <span data-ttu-id="72889-120">Consulte [declarando recursos em projetos do CPS](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span><span class="sxs-lookup"><span data-stu-id="72889-120">See [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span></span>

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a><span data-ttu-id="72889-121">Implementando VsProjectCapabilitiesPresenceChecker</span><span class="sxs-lookup"><span data-stu-id="72889-121">Implementing VsProjectCapabilitiesPresenceChecker</span></span>

<span data-ttu-id="72889-122">A classe `VsProjectCapabilitiesPresenceChecker` precisa implementar a interface `IVsBooleanSymbolPresenceChecker`, que é definida da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="72889-122">The `VsProjectCapabilitiesPresenceChecker` class must implement the `IVsBooleanSymbolPresenceChecker` interface, which is defined as follows:</span></span>

```cs
public interface IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// Checks whether the symbols defined may have changed since the last time
    /// this method was called.
    /// </summary>
    /// <param name="versionObject">
    /// The response version object assigned at the last call.
    /// May be null to get the initial version.
    /// At the conclusion of this method call, the reference may be changed so that on a subsequent call
    /// we know what version was last observed. The caller should treat this value as an opaque object,
    /// and should not assume any significance from whether the pointer changed or not.
    /// </param>
    /// <returns>
    /// <c>true</c> if the symbols defined may have changed since the last call to this method
    /// or if <paramref name="versionObject"/> was <c>null</c> upon entering this method.
    /// <c>false</c> if the responses would all be the same.
    /// </returns>
    bool HasChangedSince(ref object versionObject);

    /// <summary>
    /// Checks for the presence of a given symbol.
    /// </summary>
    /// <param name="symbol">The symbol to check for.</param>
    /// <returns><c>true</c> if the symbol is present; <c>false</c> otherwise.</returns>
    bool IsSymbolPresent(string symbol);
}
```

<span data-ttu-id="72889-123">Uma implementação de exemplo desta interface seria:</span><span class="sxs-lookup"><span data-stu-id="72889-123">A sample implementation of this interface would then be:</span></span>

```cs
class VsProjectCapabilitiesPresenceChecker : IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// The set of capabilities this project system actually has.
    /// This should be kept current, and honestly reflect what the project can do.
    /// </summary>
    private static readonly HashSet<string> ActualProjectCapabilities = new HashSet<string>(StringComparer.OrdinalIgnoreCase)
        {
            "AssemblyReferences",
            "DeclaredSourceItems",
            "UserSourceItems",
        };

    public bool HasChangedSince(ref object versionObject)
    {
        // If your project capabilities do not change over time while the project is open,
        // you may simply `return false;` from your `HasChangedSince` method.
        return false;
    }

    public bool IsSymbolPresent(string symbol)
    {
        return ActualProjectCapabilities.Contains(symbol);
    }
}
```

<span data-ttu-id="72889-124">Lembre-se de adicionar/remover recursos do conjunto `ActualProjectCapabilities` com base no que o sistema de projeto realmente dá suporte.</span><span class="sxs-lookup"><span data-stu-id="72889-124">Remember to add/remove capabilities from the `ActualProjectCapabilities` set based on what your project system actually supports.</span></span> <span data-ttu-id="72889-125">Consulte a [documentação de recursos de projeto](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) para ver descrições completas.</span><span class="sxs-lookup"><span data-stu-id="72889-125">See the [project capabilities documentation](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) for full descriptions.</span></span>

## <a name="responding-to-queries"></a><span data-ttu-id="72889-126">Respondendo a consultas</span><span class="sxs-lookup"><span data-stu-id="72889-126">Responding to queries</span></span>

<span data-ttu-id="72889-127">Um projeto declara essa funcionalidade dando suporte à propriedade `VSHPROPID_ProjectCapabilitiesChecker` por meio do `IVsHierarchy::GetProperty`.</span><span class="sxs-lookup"><span data-stu-id="72889-127">A project declares this capability by supporting the  `VSHPROPID_ProjectCapabilitiesChecker` property through the `IVsHierarchy::GetProperty`.</span></span> <span data-ttu-id="72889-128">Ele deve retornar uma instância de `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, que é definida no assembly `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll`.</span><span class="sxs-lookup"><span data-stu-id="72889-128">It should return an instance of `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, which is defined in the `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` assembly.</span></span> <span data-ttu-id="72889-129">Faça referência a esse assembly instalando [seu pacote do NuGet](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span><span class="sxs-lookup"><span data-stu-id="72889-129">Reference this assembly by installing [its NuGet package](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span></span>

<span data-ttu-id="72889-130">Por exemplo, você pode adicionar a instrução `case` a seguir à instrução `switch` do método `IVsHierarchy::GetProperty`:</span><span class="sxs-lookup"><span data-stu-id="72889-130">For example, you might add the following `case` statement to your `IVsHierarchy::GetProperty` method's `switch` statement:</span></span>

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a><span data-ttu-id="72889-131">Suporte a DTE</span><span class="sxs-lookup"><span data-stu-id="72889-131">DTE Support</span></span>

<span data-ttu-id="72889-132">O NuGet comanda o sistema do projeto para adicionar referências, itens de conteúdo e importações do MSBuild chamando [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), que é a interface de automação do Visual Studio nível superior.</span><span class="sxs-lookup"><span data-stu-id="72889-132">NuGet drives the project system to add references, content items, and MSBuild imports by calling into [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), which is the top-level Visual Studio automation interface.</span></span> <span data-ttu-id="72889-133">O DTE é um conjunto de interfaces COM que você já pode implementar.</span><span class="sxs-lookup"><span data-stu-id="72889-133">DTE is a set of COM interfaces that you may already implement.</span></span>

<span data-ttu-id="72889-134">Se o tipo de projeto é baseado no CPS, o DTE é implementado para você.</span><span class="sxs-lookup"><span data-stu-id="72889-134">If your project type is based on CPS, DTE is implemented for you.</span></span>
