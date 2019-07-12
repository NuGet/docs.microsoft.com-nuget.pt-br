---
title: Referência do PowerShell NuGet Register-TabExpansion
description: Referência do comando Register-TabExpansion PowerShell no Console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8adb80af85e2e32fa8c35e5272cf90ff0c0ddcbb
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842490"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="54092-103">Registre-se-TabExpansion (Package Manager Console no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="54092-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="54092-104">*Disponível somente dentro de [Package Manager Console](package-manager-console.md) no Visual Studio no Windows.*</span><span class="sxs-lookup"><span data-stu-id="54092-104">*Available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="54092-105">Registra uma expansão da tabulação para os parâmetros do comando especificado, de modo que quando a guia é usada ao inserir um comando, os valores expandidos aparecem como opções disponíveis para o parâmetro em questão.</span><span class="sxs-lookup"><span data-stu-id="54092-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="54092-106">Qualquer expansões anteriores para o comando são substituídos.</span><span class="sxs-lookup"><span data-stu-id="54092-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="54092-107">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="54092-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="54092-108">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="54092-108">Parameters</span></span>

| <span data-ttu-id="54092-109">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="54092-109">Parameter</span></span> | <span data-ttu-id="54092-110">Descrição</span><span class="sxs-lookup"><span data-stu-id="54092-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="54092-111">Nome</span><span class="sxs-lookup"><span data-stu-id="54092-111">Name</span></span> | <span data-ttu-id="54092-112">(Obrigatório) O comando para o qual registrar expansões.</span><span class="sxs-lookup"><span data-stu-id="54092-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="54092-113">-Nome do comutador em si é opcional.</span><span class="sxs-lookup"><span data-stu-id="54092-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="54092-114">Definição</span><span class="sxs-lookup"><span data-stu-id="54092-114">Definition</span></span> | <span data-ttu-id="54092-115">(Obrigatório) Um objeto que descreve o argumento na sintaxe `@{'<parameter>' = {'<value1>', '<value2>', ...}}` onde `<parameter>` é o nome do parâmetro para modificar e cada `<value>` fornece uma expansão específica.</span><span class="sxs-lookup"><span data-stu-id="54092-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="54092-116">Aspas simples e duplas são aceitos.</span><span class="sxs-lookup"><span data-stu-id="54092-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="54092-117">Nenhum desses parâmetros aceitam caracteres curinga ou de entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="54092-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="54092-118">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="54092-118">Common Parameters</span></span>

<span data-ttu-id="54092-119">`Register-TabExpansion` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detalhado, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="54092-119">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="54092-120">Exemplos</span><span class="sxs-lookup"><span data-stu-id="54092-120">Examples</span></span>

<span data-ttu-id="54092-121">Considere uma solução que contém três nomes de projetos EventManager, utilitários e SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="54092-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="54092-122">O desenvolvedor usa com frequência o `Update-Package` comando em momentos diferentes com cada um desses projetos.</span><span class="sxs-lookup"><span data-stu-id="54092-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="54092-123">Ela localiza conveniente fazer com que o `Update-Package` comando fornecer expansões de preenchimento automático para o `-ProjectName` argumento para que ela não precisa digitar um nome de projeto cada vez.</span><span class="sxs-lookup"><span data-stu-id="54092-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="54092-124">O comando a seguir, em seguida, registra esses nomes de três projetos como uma expansão para o `-ProjectName` parâmetro:</span><span class="sxs-lookup"><span data-stu-id="54092-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="54092-125">O desenvolvedor pode, em seguida, digite `Update-Package -ProjectName `, pressione a tecla Tab e veja as expansões oferecidas como opções de preenchimento automático:</span><span class="sxs-lookup"><span data-stu-id="54092-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Exemplo de como usar o registro TabExpansion](media/Register-TabExpansion-Example.png)
