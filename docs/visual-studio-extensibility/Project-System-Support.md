---
title: Suporte do NuGet para o sistema de projeto do Visual Studio
description: Integração do NuGet ao sistema de projeto do Visual Studio para tipos de projetos de terceiros.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: 9f1ddfd20835cc3a0f9af40a8b4e712c218b31bc
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901402"
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a>Suporte do NuGet para o sistema de projetos do Visual Studio

Para dar suporte a tipos de projeto de terceiros no Visual Studio, o NuGet 3.x e superior dá suporte a [CPS (Common Project System)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md) e o NuGet 3.2 e superior também dá suporte a sistemas de projeto não CPS.

Para integrar-se ao NuGet, um sistema de projeto deve anunciar seu próprio suporte para todos os recursos de projeto descritos neste tópico.

> [!Note]
> Não declare recursos que seu projeto efetivamente não contém visando habilitar pacotes para instalação no seu projeto. Muitos recursos do Visual Studio e outras extensões dependem de recursos de projeto, além do cliente do NuGet. Anunciar falsamente recursos do seu projeto pode levar esses componentes a funcionarem incorretamente e degradar a experiência dos usuários.

## <a name="advertise-project-capabilities"></a>Anunciar funcionalidades do projeto

O cliente do NuGet determina quais pacotes são compatíveis com o tipo de projeto com base nos [recursos do projeto](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), conforme descrito na tabela a seguir.

| Funcionalidade | Descrição |
| --- | --- |
| AssemblyReferences | Indica que o projeto é compatível com referências de assembly (diferentes de WinRTReferences). |
| DeclaredSourceItems | Indica que o projeto é um projeto típico do MSBuild (não DNX) em que ele declara itens de origem no próprio projeto. |
| UserSourceItems|Indica que o usuário tem permissão para adicionar arquivos arbitrários ao projeto dele. |

Para sistemas de projeto baseados em CPS, os detalhes de implementação para recursos de projeto descritos no restante desta seção já foram feitos para você. Consulte [declarando recursos em projetos do CPS](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a>Implementando VsProjectCapabilitiesPresenceChecker

A classe `VsProjectCapabilitiesPresenceChecker` precisa implementar a interface `IVsBooleanSymbolPresenceChecker`, que é definida da seguinte maneira:

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

Uma implementação de exemplo desta interface seria:

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

Lembre-se de adicionar/remover recursos do conjunto `ActualProjectCapabilities` com base no que o sistema de projeto realmente dá suporte. Consulte a [documentação de recursos de projeto](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) para ver descrições completas.

## <a name="responding-to-queries"></a>Respondendo a consultas

Um projeto declara essa funcionalidade dando suporte à propriedade `VSHPROPID_ProjectCapabilitiesChecker` por meio do `IVsHierarchy::GetProperty`. Ele deve retornar uma instância de `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, que é definida no assembly `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll`. Faça referência a esse assembly instalando [seu pacote do NuGet](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).

Por exemplo, você pode adicionar a instrução `case` a seguir à instrução `switch` do método `IVsHierarchy::GetProperty`:

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a>Suporte a DTE

O NuGet comanda o sistema do projeto para adicionar referências, itens de conteúdo e importações do MSBuild chamando [DTE](/dotnet/api/envdte.dte), que é a interface de automação do Visual Studio nível superior. O DTE é um conjunto de interfaces COM que você já pode implementar.

Se o tipo de projeto é baseado no CPS, o DTE é implementado para você.
