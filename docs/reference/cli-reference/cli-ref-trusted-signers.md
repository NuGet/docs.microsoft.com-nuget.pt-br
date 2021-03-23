---
title: Comando de assinantes confiáveis da CLI do NuGet
description: Referência para o nuget.exe comando de assinantes confiáveis
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9dd3fe3786c824c4a0a1cb252aa50cfc4458a483
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859415"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="b1be4-103">comando de assinantes confiáveis (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b1be4-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="b1be4-104">**Aplica-se a:** &bullet; **versões com suporte** de consumo de pacote: 4.9.1 +</span><span class="sxs-lookup"><span data-stu-id="b1be4-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="b1be4-105">Obtém ou define os assinantes confiáveis para a configuração do NuGet.</span><span class="sxs-lookup"><span data-stu-id="b1be4-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="b1be4-106">Para uso adicional, consulte [configurações comuns do NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="b1be4-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="b1be4-107">Para obter detalhes sobre como o esquema de nuget.config se parece, consulte a [referência do arquivo de configuração do NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="b1be4-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="b1be4-108">Uso</span><span class="sxs-lookup"><span data-stu-id="b1be4-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="b1be4-109">Se nenhum `list|add|remove|sync` for especificado, o comando usará como padrão `list` .</span><span class="sxs-lookup"><span data-stu-id="b1be4-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="b1be4-110">lista de assinantes confiáveis do NuGet</span><span class="sxs-lookup"><span data-stu-id="b1be4-110">nuget trusted-signers list</span></span>

<span data-ttu-id="b1be4-111">Lista todos os assinantes confiáveis na configuração.</span><span class="sxs-lookup"><span data-stu-id="b1be4-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="b1be4-112">Essa opção incluirá todos os certificados (com o algoritmo de impressão digital e de impressão digital) que cada signatário tem.</span><span class="sxs-lookup"><span data-stu-id="b1be4-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="b1be4-113">Se um certificado tiver um anterior `[U]` , isso significará que a entrada do certificado foi `allowUntrustedRoot` definida como `true` .</span><span class="sxs-lookup"><span data-stu-id="b1be4-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="b1be4-114">Veja abaixo um exemplo de saída deste comando:</span><span class="sxs-lookup"><span data-stu-id="b1be4-114">Below is an example output from this command:</span></span>

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D
        SHA256 - 5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="b1be4-115">NuGet confiável-os assinantes adicionam [opções]</span><span class="sxs-lookup"><span data-stu-id="b1be4-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="b1be4-116">Adiciona um signatário confiável com o nome fornecido para a configuração. Esta opção tem gestos diferentes para adicionar um autor ou um repositório confiável.</span><span class="sxs-lookup"><span data-stu-id="b1be4-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="b1be4-117">Opções para adicionar com base em um pacote</span><span class="sxs-lookup"><span data-stu-id="b1be4-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="b1be4-118">onde `<package(s)>` é um ou mais `.nupkg` arquivos.</span><span class="sxs-lookup"><span data-stu-id="b1be4-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

- **`-Author`**

  <span data-ttu-id="b1be4-119">Especifica que a assinatura de autor dos pacotes deve ser confiável.</span><span class="sxs-lookup"><span data-stu-id="b1be4-119">Specifies that the author signature of the package(s) should be trusted.</span></span>

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="b1be4-120">Especifica se o certificado para o assinante confiável deve ter permissão para se encadear a uma raiz não confiável.</span><span class="sxs-lookup"><span data-stu-id="b1be4-120">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="b1be4-121">Lista separada por ponto e vírgula de proprietários confiáveis para restringir ainda mais a confiança de um repositório.</span><span class="sxs-lookup"><span data-stu-id="b1be4-121">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="b1be4-122">Válido somente ao usar a `-Repository` opção.</span><span class="sxs-lookup"><span data-stu-id="b1be4-122">Only valid when using the `-Repository` option.</span></span>

- **`-Repository`**

  <span data-ttu-id="b1be4-123">Especifica que a assinatura do repositório ou a referenda dos pacotes devem ser confiáveis.</span><span class="sxs-lookup"><span data-stu-id="b1be4-123">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span>

<span data-ttu-id="b1be4-124">Fornecer `-Author` e `-Repository` ao mesmo tempo não é suportado.</span><span class="sxs-lookup"><span data-stu-id="b1be4-124">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="b1be4-125">Opções para adicionar com base em um índice de serviço</span><span class="sxs-lookup"><span data-stu-id="b1be4-125">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="b1be4-126">_Observação_: esta opção adicionará somente Repositórios confiáveis.</span><span class="sxs-lookup"><span data-stu-id="b1be4-126">_Note_: This option will only add trusted repositories.</span></span> 

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="b1be4-127">Especifica se o certificado para o assinante confiável deve ter permissão para se encadear a uma raiz não confiável.</span><span class="sxs-lookup"><span data-stu-id="b1be4-127">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="b1be4-128">Lista separada por ponto e vírgula de proprietários confiáveis para restringir ainda mais a confiança de um repositório.</span><span class="sxs-lookup"><span data-stu-id="b1be4-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span>

- **`-ServiceIndex`**

  <span data-ttu-id="b1be4-129">Especifica o índice de serviço V3 do repositório a ser confiável.</span><span class="sxs-lookup"><span data-stu-id="b1be4-129">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="b1be4-130">Este repositório tem que oferecer suporte ao recurso de assinaturas de repositório.</span><span class="sxs-lookup"><span data-stu-id="b1be4-130">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="b1be4-131">Se não for fornecido, o comando procurará uma origem de pacote com o mesmo `-Name` e obterá o índice de serviço a partir daí.</span><span class="sxs-lookup"><span data-stu-id="b1be4-131">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span>

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="b1be4-132">Opções para adicionar com base nas informações do certificado</span><span class="sxs-lookup"><span data-stu-id="b1be4-132">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="b1be4-133">_Observação_: se um signatário confiável com o nome fornecido já existir, o item de certificado será adicionado a esse signatário.</span><span class="sxs-lookup"><span data-stu-id="b1be4-133">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="b1be4-134">Caso contrário, um autor confiável será criado com um item de certificado de informações de certificado fornecidas.</span><span class="sxs-lookup"><span data-stu-id="b1be4-134">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>


- **`-AllowUntrustedRoot`**

  <span data-ttu-id="b1be4-135">Especifica se o certificado para o assinante confiável deve ter permissão para se encadear a uma raiz não confiável.</span><span class="sxs-lookup"><span data-stu-id="b1be4-135">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="b1be4-136">Especifica um certificado de impressões digitais de um certificado com o qual os pacotes assinados devem ser assinados.</span><span class="sxs-lookup"><span data-stu-id="b1be4-136">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="b1be4-137">Uma impressão digital de certificado é um hash do certificado.</span><span class="sxs-lookup"><span data-stu-id="b1be4-137">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="b1be4-138">O algoritmo de hash usado para calcular esse hash deve ser especificado na `FingerprintAlgorithm` opção.</span><span class="sxs-lookup"><span data-stu-id="b1be4-138">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span>

- **`-FingerprintAlgorithm`**

  <span data-ttu-id="b1be4-139">Especifica o algoritmo de hash usado para calcular a impressão digital do certificado.</span><span class="sxs-lookup"><span data-stu-id="b1be4-139">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="b1be4-140">Assume o padrão de `SHA256`.</span><span class="sxs-lookup"><span data-stu-id="b1be4-140">Defaults to `SHA256`.</span></span> <span data-ttu-id="b1be4-141">Os valores com suporte são `SHA256` `SHA384` e `SHA512` .</span><span class="sxs-lookup"><span data-stu-id="b1be4-141">Values supported are `SHA256`, `SHA384` and `SHA512`.</span></span>

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="b1be4-142">NuGet confiável-os assinantes removem-Name \<name\></span><span class="sxs-lookup"><span data-stu-id="b1be4-142">nuget trusted-signers remove -Name \<name\></span></span>

<span data-ttu-id="b1be4-143">Remove os assinantes confiáveis que correspondem ao nome fornecido.</span><span class="sxs-lookup"><span data-stu-id="b1be4-143">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="b1be4-144">NuGet confiável-autenticadores Sync-Name \<name\></span><span class="sxs-lookup"><span data-stu-id="b1be4-144">nuget trusted-signers sync -Name \<name\></span></span>

<span data-ttu-id="b1be4-145">Solicita a lista mais recente de certificados usados em um repositório atualmente confiável para atualizar a lista de certificados existentes no Assinante confiável.</span><span class="sxs-lookup"><span data-stu-id="b1be4-145">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="b1be4-146">_Observação_: esse gesto excluirá a lista atual de certificados e os substituirá por uma lista atualizada do repositório.</span><span class="sxs-lookup"><span data-stu-id="b1be4-146">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="b1be4-147">Opções</span><span class="sxs-lookup"><span data-stu-id="b1be4-147">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="b1be4-148">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="b1be4-148">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b1be4-149">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="b1be4-149">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="b1be4-150">Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="b1be4-150">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="b1be4-151">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="b1be4-151">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="b1be4-152">Nome do signatário confiável.</span><span class="sxs-lookup"><span data-stu-id="b1be4-152">Name of the trusted signer.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="b1be4-153">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="b1be4-153">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="b1be4-154">Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="b1be4-154">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


## <a name="examples"></a><span data-ttu-id="b1be4-155">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b1be4-155">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget trusted-signers Remove -Name TrustedRepo

nuget trusted-signers Sync -Name TrustedRepo
```
