---
title: "Referência do PowerShell do NuGet Register-TabExpansion | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 8314ec69-ee8c-4933-84ef-e6d8a412d268
description: "Referência de comando do PowerShell do registro TabExpansion no Console do Gerenciador de pacotes do NuGet no Visual Studio."
keywords: "Console do Gerenciador, comandos do Powershell do NuGet, referência do Powershell do NuGet, TabExpansion de registro do pacote NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 498b8638c81b800e5f20f7604b36e6af76da0283
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="8f4ec-104">Register-TabExpansion (Console de Gerenciador de pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="8f4ec-104">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="8f4ec-105">*Disponível apenas dentro de [NuGet Package Manager Console](Package-Manager-Console.md) no Visual Studio no Windows.*</span><span class="sxs-lookup"><span data-stu-id="8f4ec-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="8f4ec-106">Registra uma expansão de guia para os parâmetros do comando especificado, que quando a guia é usada ao inserir um comando, os valores expandidos aparecem como opções disponíveis para o parâmetro em questão.</span><span class="sxs-lookup"><span data-stu-id="8f4ec-106">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="8f4ec-107">Qualquer expansões anteriores para o comando são substituídos.</span><span class="sxs-lookup"><span data-stu-id="8f4ec-107">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="8f4ec-108">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="8f4ec-108">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="8f4ec-109">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="8f4ec-109">Parameters</span></span>

| <span data-ttu-id="8f4ec-110">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="8f4ec-110">Parameter</span></span> | <span data-ttu-id="8f4ec-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="8f4ec-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8f4ec-112">Nome</span><span class="sxs-lookup"><span data-stu-id="8f4ec-112">Name</span></span> | <span data-ttu-id="8f4ec-113">(Obrigatório) O comando para o qual registrar expansões.</span><span class="sxs-lookup"><span data-stu-id="8f4ec-113">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="8f4ec-114">-Nome do comutador em si é opcional.</span><span class="sxs-lookup"><span data-stu-id="8f4ec-114">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="8f4ec-115">Definição</span><span class="sxs-lookup"><span data-stu-id="8f4ec-115">Definition</span></span> | <span data-ttu-id="8f4ec-116">(Obrigatório) Um objeto que descreve o argumento na sintaxe `@{'<parameter>' = {'<value1>', '<value2>', ...}}` onde `<parameter>` é o nome do parâmetro para modificar e cada `<value>` fornece uma expansão específica.</span><span class="sxs-lookup"><span data-stu-id="8f4ec-116">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="8f4ec-117">Aspas simples e duplas são aceitas.</span><span class="sxs-lookup"><span data-stu-id="8f4ec-117">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="8f4ec-118">Nenhum desses parâmetros aceitar caracteres curinga ou de entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="8f4ec-118">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="8f4ec-119">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="8f4ec-119">Common Parameters</span></span>

<span data-ttu-id="8f4ec-120">`Register-TabExpansion`suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, WarningAction, detalhado e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="8f4ec-120">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="8f4ec-121">Exemplos</span><span class="sxs-lookup"><span data-stu-id="8f4ec-121">Examples</span></span>

<span data-ttu-id="8f4ec-122">Considere uma solução que contém três nomes de projetos EventManager, utilitários e SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="8f4ec-122">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="8f4ec-123">O desenvolvedor usa com frequência o `Update-Package` comando em momentos diferentes com cada um desses projetos.</span><span class="sxs-lookup"><span data-stu-id="8f4ec-123">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="8f4ec-124">Ela localiza conveniente ter o `Update-Package` comando fornecem expansões de preenchimento automático para o `-ProjectName` argumento para que ela não precisa digitar um nome de projeto cada vez.</span><span class="sxs-lookup"><span data-stu-id="8f4ec-124">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="8f4ec-125">O comando a seguir, em seguida, registra esses nomes de três projeto como uma expansão para o `-ProjectName` parâmetro:</span><span class="sxs-lookup"><span data-stu-id="8f4ec-125">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="8f4ec-126">O desenvolvedor pode, em seguida, digite `Update-Package -ProjectName `, pressione a tecla Tab e ver as expansões oferecidas como opções de conclusão automática:</span><span class="sxs-lookup"><span data-stu-id="8f4ec-126">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Exemplo de como usar o registro TabExpansion](media/Register-TabExpansion-Example.png)
