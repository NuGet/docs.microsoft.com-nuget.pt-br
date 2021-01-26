---
title: Referência do NuGet Register-TabExpansion PowerShell
description: Referência para Register-TabExpansion comando do PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 6ad0da0e84fc2e31499c06bde013d2a256987d9a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777455"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="624fb-103">Register-TabExpansion (console do Gerenciador de pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="624fb-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="624fb-104">*Disponível somente dentro do [console do Gerenciador de pacotes](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows.*</span><span class="sxs-lookup"><span data-stu-id="624fb-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="624fb-105">Registra uma expansão de tabulação para os parâmetros do comando especificado, de modo que, quando a guia é usada ao inserir um comando, os valores expandidos aparecem como opções disponíveis para o parâmetro em questão.</span><span class="sxs-lookup"><span data-stu-id="624fb-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="624fb-106">Todas as expansões anteriores para o comando são substituídas.</span><span class="sxs-lookup"><span data-stu-id="624fb-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="624fb-107">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="624fb-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="624fb-108">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="624fb-108">Parameters</span></span>

| <span data-ttu-id="624fb-109">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="624fb-109">Parameter</span></span> | <span data-ttu-id="624fb-110">Descrição</span><span class="sxs-lookup"><span data-stu-id="624fb-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="624fb-111">Nome</span><span class="sxs-lookup"><span data-stu-id="624fb-111">Name</span></span> | <span data-ttu-id="624fb-112">Necessária O comando para o qual registrar expansões.</span><span class="sxs-lookup"><span data-stu-id="624fb-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="624fb-113">A opção-Name em si é opcional.</span><span class="sxs-lookup"><span data-stu-id="624fb-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="624fb-114">Definição</span><span class="sxs-lookup"><span data-stu-id="624fb-114">Definition</span></span> | <span data-ttu-id="624fb-115">Necessária Um objeto que descreve o argumento na sintaxe `@{'<parameter>' = {'<value1>', '<value2>', ...}}` em que `<parameter>` é o nome do parâmetro a ser modificado e cada `<value>` um fornece uma expansão específica.</span><span class="sxs-lookup"><span data-stu-id="624fb-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="624fb-116">Aspas simples e duplas são aceitas.</span><span class="sxs-lookup"><span data-stu-id="624fb-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="624fb-117">Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.</span><span class="sxs-lookup"><span data-stu-id="624fb-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="624fb-118">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="624fb-118">Common Parameters</span></span>

<span data-ttu-id="624fb-119">`Register-TabExpansion` o oferece suporte aos seguintes [parâmetros comuns do PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="624fb-119">`Register-TabExpansion` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="624fb-120">Exemplos</span><span class="sxs-lookup"><span data-stu-id="624fb-120">Examples</span></span>

<span data-ttu-id="624fb-121">Considere uma solução que contenha três nomes de projectmanager, utilitários e SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="624fb-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="624fb-122">O desenvolvedor frequentemente usa o `Update-Package` comando em momentos diferentes com cada um desses projetos.</span><span class="sxs-lookup"><span data-stu-id="624fb-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="624fb-123">Ela descobre que é conveniente fazer com que o `Update-Package` comando forneça expansões de preenchimento automático para o `-ProjectName` argumento para que ela não precise digitar um nome de projeto a cada vez.</span><span class="sxs-lookup"><span data-stu-id="624fb-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="624fb-124">O comando a seguir, em seguida, registra esses três nomes de projeto como uma expansão para o `-ProjectName` parâmetro:</span><span class="sxs-lookup"><span data-stu-id="624fb-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="624fb-125">O desenvolvedor pode digitar `Update-Package -ProjectName ` , pressionar Tab e ver as expansões oferecidas como opções de preenchimento automático:</span><span class="sxs-lookup"><span data-stu-id="624fb-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Exemplo de uso de Register-TabExpansion](media/Register-TabExpansion-Example.png)