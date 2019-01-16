---
title: Comando de signatários confiáveis de CLI do NuGet
description: Referência do comando de signatários confiável nuget.exe
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: ee4ffaa7e250cdbf313476fd794a8d87c80b69f9
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324702"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="86e87-103">comando de signatários confiáveis (CLI do NuGet)</span><span class="sxs-lookup"><span data-stu-id="86e87-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="86e87-104">**Aplica-se a:** consumo do pacote &bullet; **versões com suporte:** 4.9.1+</span><span class="sxs-lookup"><span data-stu-id="86e87-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="86e87-105">Obtém ou define os signatários confiáveis na configuração do NuGet.</span><span class="sxs-lookup"><span data-stu-id="86e87-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="86e87-106">Para uso adicional, consulte [Configurando o comportamento do NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="86e87-106">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="86e87-107">Para obter detalhes sobre como o esquema do NuGet. config se parece, consulte o [referência de arquivo de configuração do NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="86e87-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="86e87-108">Uso</span><span class="sxs-lookup"><span data-stu-id="86e87-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="86e87-109">Se nenhuma das `list|add|remove|sync` for especificado, o comando padrão será `list`.</span><span class="sxs-lookup"><span data-stu-id="86e87-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="86e87-110">lista de signatários confiáveis do NuGet</span><span class="sxs-lookup"><span data-stu-id="86e87-110">nuget trusted-signers list</span></span>

<span data-ttu-id="86e87-111">Lista todos os signatários confiáveis na configuração.</span><span class="sxs-lookup"><span data-stu-id="86e87-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="86e87-112">Essa opção incluirá todos os certificados (com a impressão digital e o algoritmo de impressão digital) tem cada assinante.</span><span class="sxs-lookup"><span data-stu-id="86e87-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="86e87-113">Se um certificado tem precedidos `[U]`, isso significa que a entrada de certificado tiver `allowUntrustedRoot` definido como `true`.</span><span class="sxs-lookup"><span data-stu-id="86e87-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="86e87-114">Abaixo está um exemplo de saída deste comando:</span><span class="sxs-lookup"><span data-stu-id="86e87-114">Below is an example output from this command:</span></span>

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

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="86e87-115">NuGet signatários confiável add [Opções]</span><span class="sxs-lookup"><span data-stu-id="86e87-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="86e87-116">Adiciona um signatário confiável com o nome fornecido para o arquivo config. Essa opção tem diferentes gestos para adicionar um repositório ou autor confiável.</span><span class="sxs-lookup"><span data-stu-id="86e87-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="86e87-117">Opções para adicionar, com base em um pacote</span><span class="sxs-lookup"><span data-stu-id="86e87-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="86e87-118">em que `<package(s)>` é um ou mais `.nupkg` arquivos.</span><span class="sxs-lookup"><span data-stu-id="86e87-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

| <span data-ttu-id="86e87-119">Opção</span><span class="sxs-lookup"><span data-stu-id="86e87-119">Option</span></span> | <span data-ttu-id="86e87-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="86e87-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="86e87-121">Autor</span><span class="sxs-lookup"><span data-stu-id="86e87-121">Author</span></span> | <span data-ttu-id="86e87-122">Especifica que a assinatura do autor do pacote (s) deve ser confiável.</span><span class="sxs-lookup"><span data-stu-id="86e87-122">Specifies that the author signature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="86e87-123">Repositório</span><span class="sxs-lookup"><span data-stu-id="86e87-123">Repository</span></span> | <span data-ttu-id="86e87-124">Especifica que a assinatura de repositório ou a referenda do pacote (s) deve ser confiável.</span><span class="sxs-lookup"><span data-stu-id="86e87-124">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="86e87-125">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="86e87-125">AllowUntrustedRoot</span></span> | <span data-ttu-id="86e87-126">Especifica se o certificado do signatário confiável deve ter permissão de encadear para uma raiz não confiável.</span><span class="sxs-lookup"><span data-stu-id="86e87-126">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="86e87-127">Proprietários</span><span class="sxs-lookup"><span data-stu-id="86e87-127">Owners</span></span> | <span data-ttu-id="86e87-128">Lista de ponto e vírgula separada de proprietários confiáveis para restringir ainda mais a relação de confiança de um repositório.</span><span class="sxs-lookup"><span data-stu-id="86e87-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="86e87-129">Válido somente ao usar o `-Repository` opção.</span><span class="sxs-lookup"><span data-stu-id="86e87-129">Only valid when using the `-Repository` option.</span></span> |

<span data-ttu-id="86e87-130">Fornecendo `-Author` e `-Repository` ao mesmo tempo não tem suporte.</span><span class="sxs-lookup"><span data-stu-id="86e87-130">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="86e87-131">Opções para adicionar, com base em um índice de serviço</span><span class="sxs-lookup"><span data-stu-id="86e87-131">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="86e87-132">_Observação_: Essa opção só será adicionar repositórios confiáveis.</span><span class="sxs-lookup"><span data-stu-id="86e87-132">_Note_: This option will only add trusted repositories.</span></span> 

| <span data-ttu-id="86e87-133">Opção</span><span class="sxs-lookup"><span data-stu-id="86e87-133">Option</span></span> | <span data-ttu-id="86e87-134">Descrição</span><span class="sxs-lookup"><span data-stu-id="86e87-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="86e87-135">ServiceIndex</span><span class="sxs-lookup"><span data-stu-id="86e87-135">ServiceIndex</span></span> | <span data-ttu-id="86e87-136">Especifica o índice de serviço V3 do repositório para ser confiável.</span><span class="sxs-lookup"><span data-stu-id="86e87-136">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="86e87-137">Esse repositório tem que oferecer suporte o recursos de assinaturas do repositório.</span><span class="sxs-lookup"><span data-stu-id="86e87-137">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="86e87-138">Se não for fornecido, o comando irá procurar uma origem de pacote com o mesmo `-Name` e obter o índice de serviço a partir daí.</span><span class="sxs-lookup"><span data-stu-id="86e87-138">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span> |
| <span data-ttu-id="86e87-139">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="86e87-139">AllowUntrustedRoot</span></span> | <span data-ttu-id="86e87-140">Especifica se o certificado do signatário confiável deve ter permissão de encadear para uma raiz não confiável.</span><span class="sxs-lookup"><span data-stu-id="86e87-140">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="86e87-141">Proprietários</span><span class="sxs-lookup"><span data-stu-id="86e87-141">Owners</span></span> | <span data-ttu-id="86e87-142">Lista de ponto e vírgula separada de proprietários confiáveis para restringir ainda mais a relação de confiança de um repositório.</span><span class="sxs-lookup"><span data-stu-id="86e87-142">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> |

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="86e87-143">Opções para adicionar, com base nas informações de certificado</span><span class="sxs-lookup"><span data-stu-id="86e87-143">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="86e87-144">_Observação_: Se um signatário confiável com o nome fornecido já existir, o item de certificado será adicionado para esse assinante.</span><span class="sxs-lookup"><span data-stu-id="86e87-144">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="86e87-145">Caso contrário, um autor confiável será criado com um item de certificado de determinadas informações do certificado.</span><span class="sxs-lookup"><span data-stu-id="86e87-145">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>

| <span data-ttu-id="86e87-146">Opção</span><span class="sxs-lookup"><span data-stu-id="86e87-146">Option</span></span> | <span data-ttu-id="86e87-147">Descrição</span><span class="sxs-lookup"><span data-stu-id="86e87-147">Description</span></span> |
| --- | --- |
| <span data-ttu-id="86e87-148">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="86e87-148">CertificateFingerprint</span></span> | <span data-ttu-id="86e87-149">Especifica um certificado de impressões digitais de um certificado que pacotes assinados devem ser assinadas com.</span><span class="sxs-lookup"><span data-stu-id="86e87-149">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="86e87-150">Uma impressão digital do certificado é um hash do certificado.</span><span class="sxs-lookup"><span data-stu-id="86e87-150">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="86e87-151">Especifica o algoritmo de hash usado para calcular esse hash deve ser o `FingerprintAlgorithm` opção.</span><span class="sxs-lookup"><span data-stu-id="86e87-151">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span> |
| <span data-ttu-id="86e87-152">FingerprintAlgorithm</span><span class="sxs-lookup"><span data-stu-id="86e87-152">FingerprintAlgorithm</span></span> | <span data-ttu-id="86e87-153">Especifica o algoritmo de hash usado para calcular a impressão digital do certificado.</span><span class="sxs-lookup"><span data-stu-id="86e87-153">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="86e87-154">Assume o padrão de `SHA256`.</span><span class="sxs-lookup"><span data-stu-id="86e87-154">Defaults to `SHA256`.</span></span> <span data-ttu-id="86e87-155">Valores com suporte são `SHA256`, `SHA384` e `SHA512`</span><span class="sxs-lookup"><span data-stu-id="86e87-155">Values supported are `SHA256`, `SHA384` and `SHA512`</span></span> |
| <span data-ttu-id="86e87-156">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="86e87-156">AllowUntrustedRoot</span></span> | <span data-ttu-id="86e87-157">Especifica se o certificado do signatário confiável deve ter permissão de encadear para uma raiz não confiável.</span><span class="sxs-lookup"><span data-stu-id="86e87-157">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="86e87-158">Remova o NuGet signatários confiáveis - nome <name></span><span class="sxs-lookup"><span data-stu-id="86e87-158">nuget trusted-signers remove -Name <name></span></span>

<span data-ttu-id="86e87-159">Remove qualquer signatários confiáveis que correspondem ao nome fornecido.</span><span class="sxs-lookup"><span data-stu-id="86e87-159">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="86e87-160">NuGet signatários confiáveis de sincronização - nome <name></span><span class="sxs-lookup"><span data-stu-id="86e87-160">nuget trusted-signers sync -Name <name></span></span>

<span data-ttu-id="86e87-161">Solicita a lista mais recente de certificados usados em um repositório confiável no momento para atualizar a lista de certificados existentes em um signatário confiável.</span><span class="sxs-lookup"><span data-stu-id="86e87-161">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="86e87-162">_Observação_: Esse gesto excluirá a lista atual de certificados e substituí-los com uma lista atualizada do repositório.</span><span class="sxs-lookup"><span data-stu-id="86e87-162">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="86e87-163">Opções</span><span class="sxs-lookup"><span data-stu-id="86e87-163">Options</span></span>

| <span data-ttu-id="86e87-164">Opção</span><span class="sxs-lookup"><span data-stu-id="86e87-164">Option</span></span> | <span data-ttu-id="86e87-165">Descrição</span><span class="sxs-lookup"><span data-stu-id="86e87-165">Description</span></span> |
| --- | --- |
| <span data-ttu-id="86e87-166">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="86e87-166">ConfigFile</span></span> | <span data-ttu-id="86e87-167">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="86e87-167">The NuGet configuration file to apply.</span></span> <span data-ttu-id="86e87-168">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="86e87-168">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="86e87-169">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="86e87-169">ForceEnglishOutput</span></span> | <span data-ttu-id="86e87-170">Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="86e87-170">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="86e87-171">Ajuda</span><span class="sxs-lookup"><span data-stu-id="86e87-171">Help</span></span> | <span data-ttu-id="86e87-172">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="86e87-172">Displays help information for the command.</span></span> |
| <span data-ttu-id="86e87-173">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="86e87-173">Verbosity</span></span> | <span data-ttu-id="86e87-174">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="86e87-174">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="86e87-175">Exemplos</span><span class="sxs-lookup"><span data-stu-id="86e87-175">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
