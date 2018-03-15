---
title: NuGet CLI Verifique se o comando | Microsoft Docs
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Comando verificar a referência para o nuget.exe"
keywords: "NuGet verificar a referência, verifique se o comando"
ms.reviewer:
- karann
- rmpablos
ms.openlocfilehash: 096c79670267d9b602dd6ad30640e832441c31c5
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/15/2018
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="f816b-104">Verifique se o comando (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f816b-104">verify command (NuGet CLI)</span></span>

<span data-ttu-id="f816b-105">**Aplica-se a:** pacote consumo &bullet; **versões com suporte:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="f816b-105">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="f816b-106">Verifica um pacote.</span><span class="sxs-lookup"><span data-stu-id="f816b-106">Verifies a package.</span></span>

## <a name="usage"></a><span data-ttu-id="f816b-107">Uso</span><span class="sxs-lookup"><span data-stu-id="f816b-107">Usage</span></span>

```cli
nuget verify <package(s)> [options]
```

<span data-ttu-id="f816b-108">onde `<package(s)>` é uma ou mais `.nupkg` arquivos.</span><span class="sxs-lookup"><span data-stu-id="f816b-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="f816b-109">Opções</span><span class="sxs-lookup"><span data-stu-id="f816b-109">Options</span></span>

| <span data-ttu-id="f816b-110">Opção</span><span class="sxs-lookup"><span data-stu-id="f816b-110">Option</span></span> | <span data-ttu-id="f816b-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="f816b-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f816b-112">Todos</span><span class="sxs-lookup"><span data-stu-id="f816b-112">All</span></span> | <span data-ttu-id="f816b-113">Especifica que todas as verificações de possíveis devem ser executadas no pacote (s).</span><span class="sxs-lookup"><span data-stu-id="f816b-113">Specifies that all verifications possible should be performed on the package(s).</span></span> |
| <span data-ttu-id="f816b-114">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="f816b-114">CertificateFingerprint</span></span> | <span data-ttu-id="f816b-115">Especifica um ou mais SHA-256 certificado impressões digitais de certificados (s) qual pacotes assinados devem ser assinados com.</span><span class="sxs-lookup"><span data-stu-id="f816b-115">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="f816b-116">Uma impressão digital de certificado SHA-256 é um hash SHA-256 do certificado.</span><span class="sxs-lookup"><span data-stu-id="f816b-116">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="f816b-117">Várias entradas devem ser separada por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="f816b-117">Multiple inputs should be semicolon separated.</span></span> |
| <span data-ttu-id="f816b-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f816b-118">ConfigFile</span></span> | <span data-ttu-id="f816b-119">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="f816b-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f816b-120">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="f816b-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f816b-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f816b-121">ForceEnglishOutput</span></span> | <span data-ttu-id="f816b-122">Força o nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="f816b-122">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f816b-123">Ajuda</span><span class="sxs-lookup"><span data-stu-id="f816b-123">Help</span></span> | <span data-ttu-id="f816b-124">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="f816b-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="f816b-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f816b-125">NonInteractive</span></span> | <span data-ttu-id="f816b-126">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="f816b-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f816b-127">Assinaturas</span><span class="sxs-lookup"><span data-stu-id="f816b-127">Signatures</span></span> | <span data-ttu-id="f816b-128">Especifica que a verificação de assinatura de pacote deve ser executada.</span><span class="sxs-lookup"><span data-stu-id="f816b-128">Specifies that package signature verification should be performed.</span></span> |
| <span data-ttu-id="f816b-129">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="f816b-129">Verbosity</span></span> | <span data-ttu-id="f816b-130">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="f816b-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="f816b-131">Exemplos</span><span class="sxs-lookup"><span data-stu-id="f816b-131">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```