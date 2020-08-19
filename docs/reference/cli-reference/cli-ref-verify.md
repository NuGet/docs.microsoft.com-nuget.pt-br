---
title: Comando Verify da CLI do NuGet
description: Referência para o comando nuget.exe Verify
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 2c501753a16820c5d027441001561c6b637ccda9
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622597"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="2db68-103">comando VERIFY (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2db68-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="2db68-104">**Aplica-se a:** &bullet; **versões com suporte** do consumo do pacote: 4.6 +</span><span class="sxs-lookup"><span data-stu-id="2db68-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="2db68-105">Verifica um pacote.</span><span class="sxs-lookup"><span data-stu-id="2db68-105">Verifies a package.</span></span>

<span data-ttu-id="2db68-106">A verificação de pacotes assinados ainda não tem suporte no .NET Core, em mono ou em plataformas que não são do Windows.</span><span class="sxs-lookup"><span data-stu-id="2db68-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="2db68-107">Uso</span><span class="sxs-lookup"><span data-stu-id="2db68-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="2db68-108">onde `<package(s)>` é um ou mais `.nupkg` arquivos.</span><span class="sxs-lookup"><span data-stu-id="2db68-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="2db68-109">verificar NuGet-todos</span><span class="sxs-lookup"><span data-stu-id="2db68-109">nuget verify -All</span></span>

<span data-ttu-id="2db68-110">Especifica que todas as verificações possíveis devem ser executadas nos pacotes.</span><span class="sxs-lookup"><span data-stu-id="2db68-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="2db68-111">verificação de NuGet-assinaturas</span><span class="sxs-lookup"><span data-stu-id="2db68-111">nuget verify -Signatures</span></span>

<span data-ttu-id="2db68-112">Especifica que a verificação de assinatura do pacote deve ser executada.</span><span class="sxs-lookup"><span data-stu-id="2db68-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="2db68-113">Opções para "Verify-Signatures"</span><span class="sxs-lookup"><span data-stu-id="2db68-113">Options for "verify -Signatures"</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="2db68-114">Especifica uma ou mais impressões digitais do certificado SHA-256 de certificados com os quais os pacotes assinados devem ser assinados.</span><span class="sxs-lookup"><span data-stu-id="2db68-114">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="2db68-115">Uma impressão digital SHA-256 do certificado é um hash SHA-256 do certificado.</span><span class="sxs-lookup"><span data-stu-id="2db68-115">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="2db68-116">Várias entradas devem ser separadas por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="2db68-116">Multiple inputs should be semicolon separated.</span></span>

## <a name="options"></a><span data-ttu-id="2db68-117">Opções</span><span class="sxs-lookup"><span data-stu-id="2db68-117">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="2db68-118">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="2db68-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2db68-119">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="2db68-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="2db68-120">Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="2db68-120">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="2db68-121">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="2db68-121">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="2db68-122">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="2db68-122">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="2db68-123">Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="2db68-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="2db68-124">Exemplos</span><span class="sxs-lookup"><span data-stu-id="2db68-124">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```