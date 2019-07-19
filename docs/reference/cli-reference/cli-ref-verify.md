---
title: Comando Verify da CLI do NuGet
description: Referência para o comando de verificação NuGet. exe
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9510f7323fe0cb860e0dbde51c1eda761846ee27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327493"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="b1129-103">Commando verify (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b1129-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="b1129-104">**Aplica-se a:** &bullet; **versões com suporte** de consumo de pacote: 4.6 +</span><span class="sxs-lookup"><span data-stu-id="b1129-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="b1129-105">Verifica um pacote.</span><span class="sxs-lookup"><span data-stu-id="b1129-105">Verifies a package.</span></span>

<span data-ttu-id="b1129-106">A verificação de pacotes assinados ainda não tem suporte no .NET Core, em mono ou em plataformas que não são do Windows.</span><span class="sxs-lookup"><span data-stu-id="b1129-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="b1129-107">Uso</span><span class="sxs-lookup"><span data-stu-id="b1129-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="b1129-108">onde `<package(s)>` é um ou mais `.nupkg` arquivos.</span><span class="sxs-lookup"><span data-stu-id="b1129-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="b1129-109">verificar NuGet-todos</span><span class="sxs-lookup"><span data-stu-id="b1129-109">nuget verify -All</span></span>

<span data-ttu-id="b1129-110">Especifica que todas as verificações possíveis devem ser executadas nos pacotes.</span><span class="sxs-lookup"><span data-stu-id="b1129-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="b1129-111">verificação de NuGet-assinaturas</span><span class="sxs-lookup"><span data-stu-id="b1129-111">nuget verify -Signatures</span></span>

<span data-ttu-id="b1129-112">Especifica que a verificação de assinatura do pacote deve ser executada.</span><span class="sxs-lookup"><span data-stu-id="b1129-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="b1129-113">Opções para "Verify-Signatures"</span><span class="sxs-lookup"><span data-stu-id="b1129-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="b1129-114">Opção</span><span class="sxs-lookup"><span data-stu-id="b1129-114">Option</span></span> | <span data-ttu-id="b1129-115">Descrição</span><span class="sxs-lookup"><span data-stu-id="b1129-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b1129-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="b1129-116">CertificateFingerprint</span></span> | <span data-ttu-id="b1129-117">Especifica uma ou mais impressões digitais do certificado SHA-256 de certificados com os quais os pacotes assinados devem ser assinados.</span><span class="sxs-lookup"><span data-stu-id="b1129-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="b1129-118">Uma impressão digital SHA-256 do certificado é um hash SHA-256 do certificado.</span><span class="sxs-lookup"><span data-stu-id="b1129-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="b1129-119">Várias entradas devem ser separadas por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="b1129-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="b1129-120">Opções</span><span class="sxs-lookup"><span data-stu-id="b1129-120">Options</span></span>

| <span data-ttu-id="b1129-121">Opção</span><span class="sxs-lookup"><span data-stu-id="b1129-121">Option</span></span> | <span data-ttu-id="b1129-122">Descrição</span><span class="sxs-lookup"><span data-stu-id="b1129-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b1129-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b1129-123">ConfigFile</span></span> | <span data-ttu-id="b1129-124">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="b1129-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b1129-125">Se não for especificado `%AppData%\NuGet\NuGet.Config` , (Windows) `~/.nuget/NuGet/NuGet.Config` ou (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="b1129-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b1129-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b1129-126">ForceEnglishOutput</span></span> | <span data-ttu-id="b1129-127">Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="b1129-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b1129-128">Ajuda</span><span class="sxs-lookup"><span data-stu-id="b1129-128">Help</span></span> | <span data-ttu-id="b1129-129">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="b1129-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="b1129-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="b1129-130">Verbosity</span></span> | <span data-ttu-id="b1129-131">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*.</span><span class="sxs-lookup"><span data-stu-id="b1129-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="b1129-132">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b1129-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```