---
title: Comando Verify da CLI do NuGet
description: Referência para o comando nuget.exe Verify
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 7ce08f11195437e94bfe69883ff525e9ad3a73f0
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238134"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="11dbb-103">comando VERIFY (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="11dbb-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="11dbb-104">**Aplica-se a:** &bullet; **versões com suporte** do consumo do pacote: 4.6 +</span><span class="sxs-lookup"><span data-stu-id="11dbb-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="11dbb-105">Verifica um pacote.</span><span class="sxs-lookup"><span data-stu-id="11dbb-105">Verifies a package.</span></span>

<span data-ttu-id="11dbb-106">A verificação de pacotes assinados ainda não tem suporte no mono.</span><span class="sxs-lookup"><span data-stu-id="11dbb-106">Verification of signed packages is not yet supported under Mono.</span></span>

## <a name="usage"></a><span data-ttu-id="11dbb-107">Uso</span><span class="sxs-lookup"><span data-stu-id="11dbb-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="11dbb-108">onde `<package(s)>` é um ou mais `.nupkg` arquivos.</span><span class="sxs-lookup"><span data-stu-id="11dbb-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="11dbb-109">verificar NuGet-todos</span><span class="sxs-lookup"><span data-stu-id="11dbb-109">nuget verify -All</span></span>

<span data-ttu-id="11dbb-110">Especifica que todas as verificações possíveis devem ser executadas nos pacotes.</span><span class="sxs-lookup"><span data-stu-id="11dbb-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="11dbb-111">verificação de NuGet-assinaturas</span><span class="sxs-lookup"><span data-stu-id="11dbb-111">nuget verify -Signatures</span></span>

<span data-ttu-id="11dbb-112">Especifica que a verificação de assinatura do pacote deve ser executada.</span><span class="sxs-lookup"><span data-stu-id="11dbb-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="11dbb-113">Opções para "Verify-Signatures"</span><span class="sxs-lookup"><span data-stu-id="11dbb-113">Options for "verify -Signatures"</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="11dbb-114">Especifica uma ou mais impressões digitais do certificado SHA-256 de certificados com os quais os pacotes assinados devem ser assinados.</span><span class="sxs-lookup"><span data-stu-id="11dbb-114">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="11dbb-115">Uma impressão digital SHA-256 do certificado é um hash SHA-256 do certificado.</span><span class="sxs-lookup"><span data-stu-id="11dbb-115">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="11dbb-116">Várias entradas devem ser separadas por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="11dbb-116">Multiple inputs should be semicolon separated.</span></span>

## <a name="options"></a><span data-ttu-id="11dbb-117">Opções</span><span class="sxs-lookup"><span data-stu-id="11dbb-117">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="11dbb-118">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="11dbb-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="11dbb-119">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="11dbb-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="11dbb-120">Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="11dbb-120">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="11dbb-121">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="11dbb-121">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="11dbb-122">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="11dbb-122">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="11dbb-123">Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="11dbb-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="11dbb-124">Exemplos</span><span class="sxs-lookup"><span data-stu-id="11dbb-124">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```