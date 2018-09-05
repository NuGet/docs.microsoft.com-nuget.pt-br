---
title: CLI do NuGet verifique se o comando
description: Referência para o nuget.exe Verifique se o comando
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 127f7a549c0a213f319c8820293646b302830436
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545207"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="a81d8-103">Commando verify (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a81d8-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="a81d8-104">**Aplica-se a:** consumo do pacote &bullet; **versões com suporte:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="a81d8-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="a81d8-105">Verifica um pacote.</span><span class="sxs-lookup"><span data-stu-id="a81d8-105">Verifies a package.</span></span>

<span data-ttu-id="a81d8-106">Verificação de pacotes assinados ainda não é suportada no .NET Core, em Mono, ou em plataformas não Windows.</span><span class="sxs-lookup"><span data-stu-id="a81d8-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="a81d8-107">Uso</span><span class="sxs-lookup"><span data-stu-id="a81d8-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="a81d8-108">em que `<package(s)>` é um ou mais `.nupkg` arquivos.</span><span class="sxs-lookup"><span data-stu-id="a81d8-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="a81d8-109">Verifique se o NuGet - todos</span><span class="sxs-lookup"><span data-stu-id="a81d8-109">nuget verify -All</span></span>

<span data-ttu-id="a81d8-110">Especifica que todas as verificações de possíveis devem ser executadas sobre o pacote (s).</span><span class="sxs-lookup"><span data-stu-id="a81d8-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="a81d8-111">Verifique se o NuGet - assinaturas</span><span class="sxs-lookup"><span data-stu-id="a81d8-111">nuget verify -Signatures</span></span>

<span data-ttu-id="a81d8-112">Especifica que a verificação de assinatura de pacote deve ser executada.</span><span class="sxs-lookup"><span data-stu-id="a81d8-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="a81d8-113">Opções para "verificar - assinaturas"</span><span class="sxs-lookup"><span data-stu-id="a81d8-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="a81d8-114">Opção</span><span class="sxs-lookup"><span data-stu-id="a81d8-114">Option</span></span> | <span data-ttu-id="a81d8-115">Descrição</span><span class="sxs-lookup"><span data-stu-id="a81d8-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a81d8-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="a81d8-116">CertificateFingerprint</span></span> | <span data-ttu-id="a81d8-117">Especifica um ou mais SHA-256 certificado impressões digitais de certificados (s) quais pacotes assinados devem ser assinados com.</span><span class="sxs-lookup"><span data-stu-id="a81d8-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="a81d8-118">Uma impressão digital de certificado SHA-256 é um hash SHA-256 do certificado.</span><span class="sxs-lookup"><span data-stu-id="a81d8-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="a81d8-119">Várias entradas devem ser separada de ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="a81d8-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="a81d8-120">Opções</span><span class="sxs-lookup"><span data-stu-id="a81d8-120">Options</span></span>

| <span data-ttu-id="a81d8-121">Opção</span><span class="sxs-lookup"><span data-stu-id="a81d8-121">Option</span></span> | <span data-ttu-id="a81d8-122">Descrição</span><span class="sxs-lookup"><span data-stu-id="a81d8-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a81d8-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a81d8-123">ConfigFile</span></span> | <span data-ttu-id="a81d8-124">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="a81d8-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a81d8-125">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="a81d8-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="a81d8-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a81d8-126">ForceEnglishOutput</span></span> | <span data-ttu-id="a81d8-127">Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="a81d8-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a81d8-128">Ajuda</span><span class="sxs-lookup"><span data-stu-id="a81d8-128">Help</span></span> | <span data-ttu-id="a81d8-129">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="a81d8-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="a81d8-130">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="a81d8-130">Verbosity</span></span> | <span data-ttu-id="a81d8-131">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="a81d8-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="a81d8-132">Exemplos</span><span class="sxs-lookup"><span data-stu-id="a81d8-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```