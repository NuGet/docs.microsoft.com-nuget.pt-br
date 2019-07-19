---
title: Comando de assinantes confiáveis da CLI do NuGet
description: Referência para o comando de assinantes confiáveis do NuGet. exe
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 197f2eaeed1a4a11f0f3ed426534807a0136271e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327533"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="fb25e-103">comando de assinantes confiáveis (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="fb25e-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="fb25e-104">**Aplica-se a:** &bullet; **versões com suporte** de consumo de pacote: 4.9.1 +</span><span class="sxs-lookup"><span data-stu-id="fb25e-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="fb25e-105">Obtém ou define os assinantes confiáveis para a configuração do NuGet.</span><span class="sxs-lookup"><span data-stu-id="fb25e-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="fb25e-106">Para uso adicional, consulte [configurações comuns do NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="fb25e-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="fb25e-107">Para obter detalhes sobre como o esquema NuGet. config se parece, consulte a [referência do arquivo de configuração do NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="fb25e-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="fb25e-108">Uso</span><span class="sxs-lookup"><span data-stu-id="fb25e-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="fb25e-109">Se nenhum `list|add|remove|sync` for especificado, o comando usará como `list`padrão.</span><span class="sxs-lookup"><span data-stu-id="fb25e-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="fb25e-110">lista de assinantes confiáveis do NuGet</span><span class="sxs-lookup"><span data-stu-id="fb25e-110">nuget trusted-signers list</span></span>

<span data-ttu-id="fb25e-111">Lista todos os assinantes confiáveis na configuração.</span><span class="sxs-lookup"><span data-stu-id="fb25e-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="fb25e-112">Essa opção incluirá todos os certificados (com o algoritmo de impressão digital e de impressão digital) que cada signatário tem.</span><span class="sxs-lookup"><span data-stu-id="fb25e-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="fb25e-113">Se um certificado tiver um anterior `[U]`, isso significará que a entrada `allowUntrustedRoot` do certificado `true`foi definida como.</span><span class="sxs-lookup"><span data-stu-id="fb25e-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="fb25e-114">Veja abaixo um exemplo de saída deste comando:</span><span class="sxs-lookup"><span data-stu-id="fb25e-114">Below is an example output from this command:</span></span>

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="fb25e-115">NuGet confiável-os assinantes adicionam [opções]</span><span class="sxs-lookup"><span data-stu-id="fb25e-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="fb25e-116">Adiciona um signatário confiável com o nome fornecido para a configuração. Esta opção tem gestos diferentes para adicionar um autor ou um repositório confiável.</span><span class="sxs-lookup"><span data-stu-id="fb25e-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="fb25e-117">Opções para adicionar com base em um pacote</span><span class="sxs-lookup"><span data-stu-id="fb25e-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="fb25e-118">onde `<package(s)>` é um ou mais `.nupkg` arquivos.</span><span class="sxs-lookup"><span data-stu-id="fb25e-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

| <span data-ttu-id="fb25e-119">Opção</span><span class="sxs-lookup"><span data-stu-id="fb25e-119">Option</span></span> | <span data-ttu-id="fb25e-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="fb25e-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fb25e-121">Autor</span><span class="sxs-lookup"><span data-stu-id="fb25e-121">Author</span></span> | <span data-ttu-id="fb25e-122">Especifica que a assinatura de autor dos pacotes deve ser confiável.</span><span class="sxs-lookup"><span data-stu-id="fb25e-122">Specifies that the author signature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="fb25e-123">Repositório</span><span class="sxs-lookup"><span data-stu-id="fb25e-123">Repository</span></span> | <span data-ttu-id="fb25e-124">Especifica que a assinatura do repositório ou a referenda dos pacotes devem ser confiáveis.</span><span class="sxs-lookup"><span data-stu-id="fb25e-124">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="fb25e-125">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="fb25e-125">AllowUntrustedRoot</span></span> | <span data-ttu-id="fb25e-126">Especifica se o certificado para o assinante confiável deve ter permissão para se encadear a uma raiz não confiável.</span><span class="sxs-lookup"><span data-stu-id="fb25e-126">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="fb25e-127">Proprietários</span><span class="sxs-lookup"><span data-stu-id="fb25e-127">Owners</span></span> | <span data-ttu-id="fb25e-128">Lista separada por ponto e vírgula de proprietários confiáveis para restringir ainda mais a confiança de um repositório.</span><span class="sxs-lookup"><span data-stu-id="fb25e-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="fb25e-129">Válido somente ao usar a `-Repository` opção.</span><span class="sxs-lookup"><span data-stu-id="fb25e-129">Only valid when using the `-Repository` option.</span></span> |

<span data-ttu-id="fb25e-130">`-Author` Fornecer e `-Repository` ao mesmo tempo não é suportado.</span><span class="sxs-lookup"><span data-stu-id="fb25e-130">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="fb25e-131">Opções para adicionar com base em um índice de serviço</span><span class="sxs-lookup"><span data-stu-id="fb25e-131">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="fb25e-132">_Observação_: Esta opção adicionará somente Repositórios confiáveis.</span><span class="sxs-lookup"><span data-stu-id="fb25e-132">_Note_: This option will only add trusted repositories.</span></span> 

| <span data-ttu-id="fb25e-133">Opção</span><span class="sxs-lookup"><span data-stu-id="fb25e-133">Option</span></span> | <span data-ttu-id="fb25e-134">Descrição</span><span class="sxs-lookup"><span data-stu-id="fb25e-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fb25e-135">Não index</span><span class="sxs-lookup"><span data-stu-id="fb25e-135">ServiceIndex</span></span> | <span data-ttu-id="fb25e-136">Especifica o índice de serviço V3 do repositório a ser confiável.</span><span class="sxs-lookup"><span data-stu-id="fb25e-136">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="fb25e-137">Este repositório tem que oferecer suporte ao recurso de assinaturas de repositório.</span><span class="sxs-lookup"><span data-stu-id="fb25e-137">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="fb25e-138">Se não for fornecido, o comando procurará uma origem de pacote com o `-Name` mesmo e obterá o índice de serviço a partir daí.</span><span class="sxs-lookup"><span data-stu-id="fb25e-138">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span> |
| <span data-ttu-id="fb25e-139">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="fb25e-139">AllowUntrustedRoot</span></span> | <span data-ttu-id="fb25e-140">Especifica se o certificado para o assinante confiável deve ter permissão para se encadear a uma raiz não confiável.</span><span class="sxs-lookup"><span data-stu-id="fb25e-140">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="fb25e-141">Proprietários</span><span class="sxs-lookup"><span data-stu-id="fb25e-141">Owners</span></span> | <span data-ttu-id="fb25e-142">Lista separada por ponto e vírgula de proprietários confiáveis para restringir ainda mais a confiança de um repositório.</span><span class="sxs-lookup"><span data-stu-id="fb25e-142">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> |

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="fb25e-143">Opções para adicionar com base nas informações do certificado</span><span class="sxs-lookup"><span data-stu-id="fb25e-143">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="fb25e-144">_Observação_: Se um signatário confiável com o nome fornecido já existir, o item de certificado será adicionado a esse signatário.</span><span class="sxs-lookup"><span data-stu-id="fb25e-144">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="fb25e-145">Caso contrário, um autor confiável será criado com um item de certificado de informações de certificado fornecidas.</span><span class="sxs-lookup"><span data-stu-id="fb25e-145">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>

| <span data-ttu-id="fb25e-146">Opção</span><span class="sxs-lookup"><span data-stu-id="fb25e-146">Option</span></span> | <span data-ttu-id="fb25e-147">Descrição</span><span class="sxs-lookup"><span data-stu-id="fb25e-147">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fb25e-148">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="fb25e-148">CertificateFingerprint</span></span> | <span data-ttu-id="fb25e-149">Especifica um certificado de impressões digitais de um certificado com o qual os pacotes assinados devem ser assinados.</span><span class="sxs-lookup"><span data-stu-id="fb25e-149">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="fb25e-150">Uma impressão digital de certificado é um hash do certificado.</span><span class="sxs-lookup"><span data-stu-id="fb25e-150">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="fb25e-151">O algoritmo de hash usado para calcular esse hash deve ser especificado na `FingerprintAlgorithm` opção.</span><span class="sxs-lookup"><span data-stu-id="fb25e-151">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span> |
| <span data-ttu-id="fb25e-152">FingerprintAlgorithm</span><span class="sxs-lookup"><span data-stu-id="fb25e-152">FingerprintAlgorithm</span></span> | <span data-ttu-id="fb25e-153">Especifica o algoritmo de hash usado para calcular a impressão digital do certificado.</span><span class="sxs-lookup"><span data-stu-id="fb25e-153">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="fb25e-154">Assume o padrão de `SHA256`.</span><span class="sxs-lookup"><span data-stu-id="fb25e-154">Defaults to `SHA256`.</span></span> <span data-ttu-id="fb25e-155">Os valores com `SHA256`suporte `SHA384` são e`SHA512`</span><span class="sxs-lookup"><span data-stu-id="fb25e-155">Values supported are `SHA256`, `SHA384` and `SHA512`</span></span> |
| <span data-ttu-id="fb25e-156">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="fb25e-156">AllowUntrustedRoot</span></span> | <span data-ttu-id="fb25e-157">Especifica se o certificado para o assinante confiável deve ter permissão para se encadear a uma raiz não confiável.</span><span class="sxs-lookup"><span data-stu-id="fb25e-157">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="fb25e-158">NuGet confiável-os assinantes removem-Name<name></span><span class="sxs-lookup"><span data-stu-id="fb25e-158">nuget trusted-signers remove -Name <name></span></span>

<span data-ttu-id="fb25e-159">Remove os assinantes confiáveis que correspondem ao nome fornecido.</span><span class="sxs-lookup"><span data-stu-id="fb25e-159">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="fb25e-160">NuGet confiável-autenticadores Sync-Name<name></span><span class="sxs-lookup"><span data-stu-id="fb25e-160">nuget trusted-signers sync -Name <name></span></span>

<span data-ttu-id="fb25e-161">Solicita a lista mais recente de certificados usados em um repositório atualmente confiável para atualizar a lista de certificados existentes no Assinante confiável.</span><span class="sxs-lookup"><span data-stu-id="fb25e-161">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="fb25e-162">_Observação_: Esse gesto excluirá a lista atual de certificados e os substituirá por uma lista atualizada do repositório.</span><span class="sxs-lookup"><span data-stu-id="fb25e-162">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="fb25e-163">Opções</span><span class="sxs-lookup"><span data-stu-id="fb25e-163">Options</span></span>

| <span data-ttu-id="fb25e-164">Opção</span><span class="sxs-lookup"><span data-stu-id="fb25e-164">Option</span></span> | <span data-ttu-id="fb25e-165">Descrição</span><span class="sxs-lookup"><span data-stu-id="fb25e-165">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fb25e-166">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="fb25e-166">ConfigFile</span></span> | <span data-ttu-id="fb25e-167">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="fb25e-167">The NuGet configuration file to apply.</span></span> <span data-ttu-id="fb25e-168">Se não for especificado `%AppData%\NuGet\NuGet.Config` , (Windows) `~/.nuget/NuGet/NuGet.Config` ou (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="fb25e-168">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="fb25e-169">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="fb25e-169">ForceEnglishOutput</span></span> | <span data-ttu-id="fb25e-170">Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="fb25e-170">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="fb25e-171">Ajuda</span><span class="sxs-lookup"><span data-stu-id="fb25e-171">Help</span></span> | <span data-ttu-id="fb25e-172">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="fb25e-172">Displays help information for the command.</span></span> |
| <span data-ttu-id="fb25e-173">Verbosity</span><span class="sxs-lookup"><span data-stu-id="fb25e-173">Verbosity</span></span> | <span data-ttu-id="fb25e-174">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*.</span><span class="sxs-lookup"><span data-stu-id="fb25e-174">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="fb25e-175">Exemplos</span><span class="sxs-lookup"><span data-stu-id="fb25e-175">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
