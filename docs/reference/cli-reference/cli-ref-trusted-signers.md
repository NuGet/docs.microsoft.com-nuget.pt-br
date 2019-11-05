---
title: Comando de assinantes confiáveis da CLI do NuGet
description: Referência para o comando de assinantes confiáveis do NuGet. exe
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 94c4c6524c1870898893b80be914477af5a14e8b
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610342"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="8db8d-103">comando de assinantes confiáveis (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8db8d-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="8db8d-104">**Aplica-se a: consumo de** pacote &bullet; **versões com suporte:** 4.9.1 +</span><span class="sxs-lookup"><span data-stu-id="8db8d-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="8db8d-105">Obtém ou define os assinantes confiáveis para a configuração do NuGet.</span><span class="sxs-lookup"><span data-stu-id="8db8d-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="8db8d-106">Para uso adicional, consulte [configurações comuns do NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="8db8d-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="8db8d-107">Para obter detalhes sobre como o esquema NuGet. config se parece, consulte a [referência do arquivo de configuração do NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="8db8d-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="8db8d-108">Uso</span><span class="sxs-lookup"><span data-stu-id="8db8d-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="8db8d-109">Se nenhuma das `list|add|remove|sync` for especificada, o comando usará como padrão `list`.</span><span class="sxs-lookup"><span data-stu-id="8db8d-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="8db8d-110">lista de assinantes confiáveis do NuGet</span><span class="sxs-lookup"><span data-stu-id="8db8d-110">nuget trusted-signers list</span></span>

<span data-ttu-id="8db8d-111">Lista todos os assinantes confiáveis na configuração.</span><span class="sxs-lookup"><span data-stu-id="8db8d-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="8db8d-112">Essa opção incluirá todos os certificados (com o algoritmo de impressão digital e de impressão digital) que cada signatário tem.</span><span class="sxs-lookup"><span data-stu-id="8db8d-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="8db8d-113">Se um certificado tiver um `[U]`anterior, isso significará que a entrada do certificado tem `allowUntrustedRoot` definido como `true`.</span><span class="sxs-lookup"><span data-stu-id="8db8d-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="8db8d-114">Veja abaixo um exemplo de saída deste comando:</span><span class="sxs-lookup"><span data-stu-id="8db8d-114">Below is an example output from this command:</span></span>

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

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="8db8d-115">NuGet confiável-os assinantes adicionam [opções]</span><span class="sxs-lookup"><span data-stu-id="8db8d-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="8db8d-116">Adiciona um signatário confiável com o nome fornecido para a configuração. Esta opção tem gestos diferentes para adicionar um autor ou um repositório confiável.</span><span class="sxs-lookup"><span data-stu-id="8db8d-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="8db8d-117">Opções para adicionar com base em um pacote</span><span class="sxs-lookup"><span data-stu-id="8db8d-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="8db8d-118">onde `<package(s)>` é um ou mais arquivos de `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="8db8d-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

| <span data-ttu-id="8db8d-119">Opção</span><span class="sxs-lookup"><span data-stu-id="8db8d-119">Option</span></span> | <span data-ttu-id="8db8d-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="8db8d-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8db8d-121">Autor</span><span class="sxs-lookup"><span data-stu-id="8db8d-121">Author</span></span> | <span data-ttu-id="8db8d-122">Especifica que a assinatura de autor dos pacotes deve ser confiável.</span><span class="sxs-lookup"><span data-stu-id="8db8d-122">Specifies that the author signature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="8db8d-123">Repositório</span><span class="sxs-lookup"><span data-stu-id="8db8d-123">Repository</span></span> | <span data-ttu-id="8db8d-124">Especifica que a assinatura do repositório ou a referenda dos pacotes devem ser confiáveis.</span><span class="sxs-lookup"><span data-stu-id="8db8d-124">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="8db8d-125">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="8db8d-125">AllowUntrustedRoot</span></span> | <span data-ttu-id="8db8d-126">Especifica se o certificado para o assinante confiável deve ter permissão para se encadear a uma raiz não confiável.</span><span class="sxs-lookup"><span data-stu-id="8db8d-126">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="8db8d-127">Proprietários</span><span class="sxs-lookup"><span data-stu-id="8db8d-127">Owners</span></span> | <span data-ttu-id="8db8d-128">Lista separada por ponto e vírgula de proprietários confiáveis para restringir ainda mais a confiança de um repositório.</span><span class="sxs-lookup"><span data-stu-id="8db8d-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="8db8d-129">Válido somente ao usar a opção `-Repository`.</span><span class="sxs-lookup"><span data-stu-id="8db8d-129">Only valid when using the `-Repository` option.</span></span> |

<span data-ttu-id="8db8d-130">Não há suporte para fornecer `-Author` e `-Repository` ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="8db8d-130">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="8db8d-131">Opções para adicionar com base em um índice de serviço</span><span class="sxs-lookup"><span data-stu-id="8db8d-131">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="8db8d-132">_Observação_: esta opção adicionará somente Repositórios confiáveis.</span><span class="sxs-lookup"><span data-stu-id="8db8d-132">_Note_: This option will only add trusted repositories.</span></span> 

| <span data-ttu-id="8db8d-133">Opção</span><span class="sxs-lookup"><span data-stu-id="8db8d-133">Option</span></span> | <span data-ttu-id="8db8d-134">Descrição</span><span class="sxs-lookup"><span data-stu-id="8db8d-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8db8d-135">Não index</span><span class="sxs-lookup"><span data-stu-id="8db8d-135">ServiceIndex</span></span> | <span data-ttu-id="8db8d-136">Especifica o índice de serviço V3 do repositório a ser confiável.</span><span class="sxs-lookup"><span data-stu-id="8db8d-136">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="8db8d-137">Este repositório tem que oferecer suporte ao recurso de assinaturas de repositório.</span><span class="sxs-lookup"><span data-stu-id="8db8d-137">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="8db8d-138">Se não for fornecido, o comando procurará uma origem de pacote com o mesmo `-Name` e obterá o índice de serviço a partir daí.</span><span class="sxs-lookup"><span data-stu-id="8db8d-138">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span> |
| <span data-ttu-id="8db8d-139">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="8db8d-139">AllowUntrustedRoot</span></span> | <span data-ttu-id="8db8d-140">Especifica se o certificado para o assinante confiável deve ter permissão para se encadear a uma raiz não confiável.</span><span class="sxs-lookup"><span data-stu-id="8db8d-140">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="8db8d-141">Proprietários</span><span class="sxs-lookup"><span data-stu-id="8db8d-141">Owners</span></span> | <span data-ttu-id="8db8d-142">Lista separada por ponto e vírgula de proprietários confiáveis para restringir ainda mais a confiança de um repositório.</span><span class="sxs-lookup"><span data-stu-id="8db8d-142">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> |

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="8db8d-143">Opções para adicionar com base nas informações do certificado</span><span class="sxs-lookup"><span data-stu-id="8db8d-143">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="8db8d-144">_Observação_: se um signatário confiável com o nome fornecido já existir, o item de certificado será adicionado a esse signatário.</span><span class="sxs-lookup"><span data-stu-id="8db8d-144">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="8db8d-145">Caso contrário, um autor confiável será criado com um item de certificado de informações de certificado fornecidas.</span><span class="sxs-lookup"><span data-stu-id="8db8d-145">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>

| <span data-ttu-id="8db8d-146">Opção</span><span class="sxs-lookup"><span data-stu-id="8db8d-146">Option</span></span> | <span data-ttu-id="8db8d-147">Descrição</span><span class="sxs-lookup"><span data-stu-id="8db8d-147">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8db8d-148">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="8db8d-148">CertificateFingerprint</span></span> | <span data-ttu-id="8db8d-149">Especifica um certificado de impressões digitais de um certificado com o qual os pacotes assinados devem ser assinados.</span><span class="sxs-lookup"><span data-stu-id="8db8d-149">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="8db8d-150">Uma impressão digital de certificado é um hash do certificado.</span><span class="sxs-lookup"><span data-stu-id="8db8d-150">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="8db8d-151">O algoritmo de hash usado para calcular esse hash deve ser especificado na opção `FingerprintAlgorithm`.</span><span class="sxs-lookup"><span data-stu-id="8db8d-151">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span> |
| <span data-ttu-id="8db8d-152">FingerprintAlgorithm</span><span class="sxs-lookup"><span data-stu-id="8db8d-152">FingerprintAlgorithm</span></span> | <span data-ttu-id="8db8d-153">Especifica o algoritmo de hash usado para calcular a impressão digital do certificado.</span><span class="sxs-lookup"><span data-stu-id="8db8d-153">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="8db8d-154">Assume o padrão de `SHA256`.</span><span class="sxs-lookup"><span data-stu-id="8db8d-154">Defaults to `SHA256`.</span></span> <span data-ttu-id="8db8d-155">Os valores com suporte são `SHA256`, `SHA384` e `SHA512`</span><span class="sxs-lookup"><span data-stu-id="8db8d-155">Values supported are `SHA256`, `SHA384` and `SHA512`</span></span> |
| <span data-ttu-id="8db8d-156">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="8db8d-156">AllowUntrustedRoot</span></span> | <span data-ttu-id="8db8d-157">Especifica se o certificado para o assinante confiável deve ter permissão para se encadear a uma raiz não confiável.</span><span class="sxs-lookup"><span data-stu-id="8db8d-157">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="8db8d-158">o NuGet Trusted-signers remove-Name \<Name\></span><span class="sxs-lookup"><span data-stu-id="8db8d-158">nuget trusted-signers remove -Name \<name\></span></span>

<span data-ttu-id="8db8d-159">Remove os assinantes confiáveis que correspondem ao nome fornecido.</span><span class="sxs-lookup"><span data-stu-id="8db8d-159">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="8db8d-160">NuGet confiável-os assinantes Sync-Name \<Name\></span><span class="sxs-lookup"><span data-stu-id="8db8d-160">nuget trusted-signers sync -Name \<name\></span></span>

<span data-ttu-id="8db8d-161">Solicita a lista mais recente de certificados usados em um repositório atualmente confiável para atualizar a lista de certificados existentes no Assinante confiável.</span><span class="sxs-lookup"><span data-stu-id="8db8d-161">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="8db8d-162">_Observação_: esse gesto excluirá a lista atual de certificados e os substituirá por uma lista atualizada do repositório.</span><span class="sxs-lookup"><span data-stu-id="8db8d-162">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="8db8d-163">Opções</span><span class="sxs-lookup"><span data-stu-id="8db8d-163">Options</span></span>

| <span data-ttu-id="8db8d-164">Opção</span><span class="sxs-lookup"><span data-stu-id="8db8d-164">Option</span></span> | <span data-ttu-id="8db8d-165">Descrição</span><span class="sxs-lookup"><span data-stu-id="8db8d-165">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8db8d-166">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8db8d-166">ConfigFile</span></span> | <span data-ttu-id="8db8d-167">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="8db8d-167">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8db8d-168">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="8db8d-168">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="8db8d-169">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8db8d-169">ForceEnglishOutput</span></span> | <span data-ttu-id="8db8d-170">Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="8db8d-170">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8db8d-171">Ajuda</span><span class="sxs-lookup"><span data-stu-id="8db8d-171">Help</span></span> | <span data-ttu-id="8db8d-172">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="8db8d-172">Displays help information for the command.</span></span> |
| <span data-ttu-id="8db8d-173">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="8db8d-173">Verbosity</span></span> | <span data-ttu-id="8db8d-174">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*.</span><span class="sxs-lookup"><span data-stu-id="8db8d-174">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="8db8d-175">Exemplos</span><span class="sxs-lookup"><span data-stu-id="8db8d-175">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
