---
title: Comando de entrada do NuGet CLI | Microsoft Docs
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referência para o comando de sinal de nuget.exe
keywords: referência de entrada NuGet, comando de sinal
ms.reviewer:
- karann
- rmpablos
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 9c83e5abae0e70cdc62917861c1febfce4f792c7
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="570fa-104">comando de sinal (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="570fa-104">sign command (NuGet CLI)</span></span>

<span data-ttu-id="570fa-105">**Aplica-se a:** criação do pacote &bullet; **versões com suporte:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="570fa-105">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="570fa-106">Assina todos os pacotes que o primeiro argumento com um certificado de correspondência.</span><span class="sxs-lookup"><span data-stu-id="570fa-106">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="570fa-107">O certificado com a chave privada pode ser obtido de um arquivo ou de um certificado instalado em um repositório de certificados, fornecendo um nome de entidade ou uma impressão digital.</span><span class="sxs-lookup"><span data-stu-id="570fa-107">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

<span data-ttu-id="570fa-108">Assinatura do pacote ainda não é suportado em Mono ou em plataformas não Windows.</span><span class="sxs-lookup"><span data-stu-id="570fa-108">Package signing is not yet supported under Mono or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="570fa-109">Uso</span><span class="sxs-lookup"><span data-stu-id="570fa-109">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="570fa-110">onde `<package(s)>` é uma ou mais `.nupkg` arquivos.</span><span class="sxs-lookup"><span data-stu-id="570fa-110">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="570fa-111">Opções</span><span class="sxs-lookup"><span data-stu-id="570fa-111">Options</span></span>

| <span data-ttu-id="570fa-112">Opção</span><span class="sxs-lookup"><span data-stu-id="570fa-112">Option</span></span> | <span data-ttu-id="570fa-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="570fa-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="570fa-114">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="570fa-114">CertificateFingerprint</span></span> | <span data-ttu-id="570fa-115">Especifica a impressão digital de SHA-1 do certificado usado para pesquisar um repositório de certificados local para o certificado.</span><span class="sxs-lookup"><span data-stu-id="570fa-115">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span> |
| <span data-ttu-id="570fa-116">CertificatePassword</span><span class="sxs-lookup"><span data-stu-id="570fa-116">CertificatePassword</span></span> | <span data-ttu-id="570fa-117">Especifica a senha do certificado, se necessário.</span><span class="sxs-lookup"><span data-stu-id="570fa-117">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="570fa-118">Se um certificado é protegido por senha, mas nenhuma senha for fornecida, o comando solicitará uma senha em tempo de execução, a menos que o - opção interativa é passado.</span><span class="sxs-lookup"><span data-stu-id="570fa-118">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the -NonInteractive option is passed.</span></span> |
| <span data-ttu-id="570fa-119">CertificatePath</span><span class="sxs-lookup"><span data-stu-id="570fa-119">CertificatePath</span></span> | <span data-ttu-id="570fa-120">Especifica o caminho do arquivo para o certificado a ser usado na assinatura do pacote.</span><span class="sxs-lookup"><span data-stu-id="570fa-120">Specifies the file path to the certificate to be used in signing the package.</span></span> |
| <span data-ttu-id="570fa-121">CertificateStoreLocation</span><span class="sxs-lookup"><span data-stu-id="570fa-121">CertificateStoreLocation</span></span> | <span data-ttu-id="570fa-122">Especifica o nome do uso de repositório de certificado x. 509 para pesquisar o certificado.</span><span class="sxs-lookup"><span data-stu-id="570fa-122">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="570fa-123">O padrão é "CurrentUser", o repositório de certificados x. 509 usado pelo usuário atual.</span><span class="sxs-lookup"><span data-stu-id="570fa-123">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="570fa-124">Essa opção deve ser usada ao especificar o certificado usando as opções de CertificateSubjectName - ou - CertificateFingerprint.</span><span class="sxs-lookup"><span data-stu-id="570fa-124">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="570fa-125">CertificateStoreName</span><span class="sxs-lookup"><span data-stu-id="570fa-125">CertificateStoreName</span></span> | <span data-ttu-id="570fa-126">Especifica o nome do repositório de certificados x. 509 a ser usado para pesquisar o certificado.</span><span class="sxs-lookup"><span data-stu-id="570fa-126">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="570fa-127">O padrão é "My", o repositório de certificados x. 509 certificados pessoais.</span><span class="sxs-lookup"><span data-stu-id="570fa-127">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="570fa-128">Essa opção deve ser usada ao especificar o certificado usando as opções de CertificateSubjectName - ou - CertificateFingerprint.</span><span class="sxs-lookup"><span data-stu-id="570fa-128">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="570fa-129">CertificateSubjectName</span><span class="sxs-lookup"><span data-stu-id="570fa-129">CertificateSubjectName</span></span> | <span data-ttu-id="570fa-130">Especifica o nome da entidade do certificado usado para pesquisar um repositório de certificados local para o certificado.</span><span class="sxs-lookup"><span data-stu-id="570fa-130">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="570fa-131">A pesquisa é uma comparação de cadeia de caracteres de maiusculas e minúsculas usando o valor fornecido, o que encontrará todos os certificados com o nome da entidade que contém essa cadeia de caracteres, independentemente de outros valores de assunto.</span><span class="sxs-lookup"><span data-stu-id="570fa-131">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="570fa-132">O repositório de certificados pode ser especificado pelas opções CertificateStoreName - e - CertificateStoreLocation.</span><span class="sxs-lookup"><span data-stu-id="570fa-132">The certificate store can be specified by -CertificateStoreName and -CertificateStoreLocation options.</span></span> |
| <span data-ttu-id="570fa-133">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="570fa-133">ConfigFile</span></span> | <span data-ttu-id="570fa-134">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="570fa-134">The NuGet configuration file to apply.</span></span> <span data-ttu-id="570fa-135">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="570fa-135">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="570fa-136">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="570fa-136">ForceEnglishOutput</span></span> | <span data-ttu-id="570fa-137">Força o nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="570fa-137">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="570fa-138">HashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="570fa-138">HashAlgorithm</span></span> | <span data-ttu-id="570fa-139">Algoritmo de hash a ser usado para assinar o pacote.</span><span class="sxs-lookup"><span data-stu-id="570fa-139">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="570fa-140">O padrão é SHA256.</span><span class="sxs-lookup"><span data-stu-id="570fa-140">Defaults to SHA256.</span></span> |
| <span data-ttu-id="570fa-141">Ajuda</span><span class="sxs-lookup"><span data-stu-id="570fa-141">Help</span></span> | <span data-ttu-id="570fa-142">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="570fa-142">Displays help information for the command.</span></span> |
| <span data-ttu-id="570fa-143">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="570fa-143">NonInteractive</span></span> | <span data-ttu-id="570fa-144">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="570fa-144">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="570fa-145">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="570fa-145">OutputDirectory</span></span> | <span data-ttu-id="570fa-146">Especifica o diretório onde o pacote assinado deve ser salvo.</span><span class="sxs-lookup"><span data-stu-id="570fa-146">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="570fa-147">Por padrão, o pacote original é substituído pelo pacote assinado.</span><span class="sxs-lookup"><span data-stu-id="570fa-147">By default the original package is overwritten by the signed package.</span></span> |
| <span data-ttu-id="570fa-148">Substituir</span><span class="sxs-lookup"><span data-stu-id="570fa-148">Overwrite</span></span> | <span data-ttu-id="570fa-149">Opção para indicar se a assinatura atual deve ser substituída.</span><span class="sxs-lookup"><span data-stu-id="570fa-149">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="570fa-150">Por padrão o comando falhará se o pacote já tiver uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="570fa-150">By default the command will fail if the package already has a signature.</span></span> |
| <span data-ttu-id="570fa-151">Timestamper</span><span class="sxs-lookup"><span data-stu-id="570fa-151">Timestamper</span></span> | <span data-ttu-id="570fa-152">URL para um servidor de carimbo de hora do RFC 3161.</span><span class="sxs-lookup"><span data-stu-id="570fa-152">URL to an RFC 3161 timestamping server.</span></span> |
| <span data-ttu-id="570fa-153">TimestampHashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="570fa-153">TimestampHashAlgorithm</span></span> | <span data-ttu-id="570fa-154">Algoritmo de hash a ser usado pelo servidor de carimbo de hora do RFC 3161.</span><span class="sxs-lookup"><span data-stu-id="570fa-154">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="570fa-155">O padrão é SHA256.</span><span class="sxs-lookup"><span data-stu-id="570fa-155">Defaults to SHA256.</span></span> |
| <span data-ttu-id="570fa-156">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="570fa-156">Verbosity</span></span> | <span data-ttu-id="570fa-157">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="570fa-157">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="570fa-158">Exemplos</span><span class="sxs-lookup"><span data-stu-id="570fa-158">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```