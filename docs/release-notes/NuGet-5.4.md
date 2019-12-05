---
title: Notas de versão do NuGet 5,4
description: Notas de versão do NuGet 5,4, incluindo novos recursos, correções de bugs e DCRs.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 69f78ba5483fcc92887624584663e8c496cfc497
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2019
ms.locfileid: "74828404"
---
# <a name="nuget-54-release-notes"></a><span data-ttu-id="d2f64-103">Notas de versão do NuGet 5,4</span><span class="sxs-lookup"><span data-stu-id="d2f64-103">NuGet 5.4 Release Notes</span></span>

<span data-ttu-id="d2f64-104">Veículos de distribuição do NuGet:</span><span class="sxs-lookup"><span data-stu-id="d2f64-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="d2f64-105">Versão do NuGet</span><span class="sxs-lookup"><span data-stu-id="d2f64-105">NuGet version</span></span> | <span data-ttu-id="d2f64-106">Disponível na versão do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d2f64-106">Available in Visual Studio version</span></span>| <span data-ttu-id="d2f64-107">Disponível em SDKs do .NET</span><span class="sxs-lookup"><span data-stu-id="d2f64-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="d2f64-108">**5.4.0**</span><span class="sxs-lookup"><span data-stu-id="d2f64-108">**5.4.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="d2f64-109">Visual Studio 2019 versão 16,4</span><span class="sxs-lookup"><span data-stu-id="d2f64-109">Visual Studio 2019 version 16.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="d2f64-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="d2f64-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="d2f64-111"><sup>1</sup> Instalado com o Visual Studio 2019 com carga de trabalho do .NET Core</span><span class="sxs-lookup"><span data-stu-id="d2f64-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-54"></a><span data-ttu-id="d2f64-112">Resumo: o que há de novo no 5,4</span><span class="sxs-lookup"><span data-stu-id="d2f64-112">Summary: What's New in 5.4</span></span>

* <span data-ttu-id="d2f64-113">Tempo de carregamento de solução mais rápido – a sobrecarga de execução do código NuGet durante o primeiro carregamento da solução foi reduzida por meio de um NGen parcial para reduzir [#6007](https://github.com/NuGet/Home/issues/6007) de custo JIT</span><span class="sxs-lookup"><span data-stu-id="d2f64-113">Faster solution load time - Overhead running NuGet code during first solution load has been reduced via partial-ngen to reduce JIT cost - [#6007](https://github.com/NuGet/Home/issues/6007)</span></span>

* <span data-ttu-id="d2f64-114">Nova função auxiliar – dada uma lista de IDs e versões de pacote, obtenha os pacotes de nível superior prováveis.</span><span class="sxs-lookup"><span data-stu-id="d2f64-114">New helper function - given a list of package ids and versions, get the likely top level packages.</span></span><span data-ttu-id="d2f64-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span><span class="sxs-lookup"><span data-stu-id="d2f64-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="d2f64-116">Problemas corrigidos nesta versão</span><span class="sxs-lookup"><span data-stu-id="d2f64-116">Issues fixed in this release</span></span>

<span data-ttu-id="d2f64-117">**•s**</span><span class="sxs-lookup"><span data-stu-id="d2f64-117">**Bugs**</span></span>

* <span data-ttu-id="d2f64-118">Plugin: a precisão do tempo de log está desativada no Linux/Mac- [#8747](https://github.com/NuGet/Home/issues/8747)</span><span class="sxs-lookup"><span data-stu-id="d2f64-118">Plugin: Logging time accuracy is off on linux/Mac - [#8747](https://github.com/NuGet/Home/issues/8747)</span></span>

* <span data-ttu-id="d2f64-119">A descartação de um plug-in pode, às vezes, lançar e falhar toda a operação.</span><span class="sxs-lookup"><span data-stu-id="d2f64-119">Disposing of a plugin can sometimes throw and fail the whole operation.</span></span><span data-ttu-id="d2f64-120"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span><span class="sxs-lookup"><span data-stu-id="d2f64-120"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span></span>

* <span data-ttu-id="d2f64-121">Parar de exibir duplicatas de versão na lista de versões permitidas e bloqueadas em PMUI- [#8679](https://github.com/NuGet/Home/issues/8679)</span><span class="sxs-lookup"><span data-stu-id="d2f64-121">Stop displaying version duplicates in allowed and blocked versions list in PMUI - [#8679](https://github.com/NuGet/Home/issues/8679)</span></span>

* <span data-ttu-id="d2f64-122">O arquivo de bloqueio não foi gerado corretamente-a ordenação de estrutura não deve afetar a restauração com o modo bloqueado- [#8645](https://github.com/NuGet/Home/issues/8645)</span><span class="sxs-lookup"><span data-stu-id="d2f64-122">Lock File not properly generated - framework ordering should not impact the restore with lockedmode - [#8645](https://github.com/NuGet/Home/issues/8645)</span></span>

* <span data-ttu-id="d2f64-123">A validação de lockfile falha para projetos com <RuntimeIdentifiers> definido no SDK 3.0.100- [#8639](https://github.com/NuGet/Home/issues/8639)</span><span class="sxs-lookup"><span data-stu-id="d2f64-123">LockFile validation fails for projects with <RuntimeIdentifiers> set in SDK 3.0.100 - [#8639](https://github.com/NuGet/Home/issues/8639)</span></span>

* <span data-ttu-id="d2f64-124">A validação de assinatura agora rejeitará corretamente as assinaturas com carimbos de data/hora que têm 2 valores na mesma OID- [#8629](https://github.com/NuGet/Home/issues/8629)</span><span class="sxs-lookup"><span data-stu-id="d2f64-124">Signing Validation will now properly reject signatures with timestamps which have 2 values under the same OID - [#8629](https://github.com/NuGet/Home/issues/8629)</span></span>

* <span data-ttu-id="d2f64-125">Atualizar a lista de licenças- [#8544](https://github.com/NuGet/Home/issues/8544)</span><span class="sxs-lookup"><span data-stu-id="d2f64-125">Update the license list - [#8544](https://github.com/NuGet/Home/issues/8544)</span></span>

<span data-ttu-id="d2f64-126">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="d2f64-126">**DCRs**</span></span>

* <span data-ttu-id="d2f64-127">Integração de arquivos de diagnóstico ao IFeedbackDiagnosticFileProvider- [#8535](https://github.com/NuGet/Home/issues/8535)</span><span class="sxs-lookup"><span data-stu-id="d2f64-127">Onboarding diagnostic files to IFeedbackDiagnosticFileProvider - [#8535](https://github.com/NuGet/Home/issues/8535)</span></span>

<span data-ttu-id="d2f64-128">**[Lista de todos os problemas corrigidos nesta versão-5,4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span><span class="sxs-lookup"><span data-stu-id="d2f64-128">**[List of all issues fixed in this release - 5.4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span></span>
