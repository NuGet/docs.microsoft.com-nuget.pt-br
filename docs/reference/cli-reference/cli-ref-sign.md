---
title: Comando de assinatura do NuGet CLI
description: Referência para o comando de assinatura de nuget.exe
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 84386f1752b98688f1fd34e453f5b72ae8afdd92
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622766"
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="a1c3c-103">comando Sign (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a1c3c-103">sign command (NuGet CLI)</span></span>

<span data-ttu-id="a1c3c-104">**Aplica-se a:** &bullet; **versões com suporte** para criação de pacote: 4.6 +</span><span class="sxs-lookup"><span data-stu-id="a1c3c-104">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="a1c3c-105">Assina todos os pacotes que correspondem ao primeiro argumento com um certificado.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-105">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="a1c3c-106">O certificado com a chave privada pode ser obtido de um arquivo ou de um certificado instalado em um repositório de certificados, fornecendo um nome de entidade ou uma impressão digital.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-106">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

> [!Note]
> <span data-ttu-id="a1c3c-107">A assinatura de pacote ainda não tem suporte no .NET Core, em mono ou em plataformas que não são do Windows.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-107">Package signing is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="a1c3c-108">Uso</span><span class="sxs-lookup"><span data-stu-id="a1c3c-108">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="a1c3c-109">onde `<package(s)>` é um ou mais `.nupkg` arquivos.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-109">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="a1c3c-110">Opções</span><span class="sxs-lookup"><span data-stu-id="a1c3c-110">Options</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="a1c3c-111">Especifica a impressão digital SHA-1 do certificado usado para pesquisar um repositório de certificados local para o certificado.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-111">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span>

- **`-CertificatePassword`**

  <span data-ttu-id="a1c3c-112">Especifica a senha do certificado, se necessário.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-112">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="a1c3c-113">Se um certificado for protegido por senha, mas nenhuma senha for fornecida, o comando solicitará uma senha em tempo de execução, a menos que a `-NonInteractive` opção seja passada.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-113">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the `-NonInteractive` option is passed.</span></span>

- **`-CertificatePath`**

  <span data-ttu-id="a1c3c-114">Especifica o caminho do arquivo para o certificado a ser usado na assinatura do pacote.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-114">Specifies the file path to the certificate to be used in signing the package.</span></span>

- **`-CertificateStoreLocation`**

  <span data-ttu-id="a1c3c-115">Especifica o nome do repositório de certificados X. 509 usado para pesquisar o certificado.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-115">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="a1c3c-116">O padrão é "CurrentUser", o repositório de certificados X. 509 usado pelo usuário atual.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-116">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="a1c3c-117">Essa opção deve ser usada ao especificar o certificado por meio de `-CertificateSubjectName` `-CertificateFingerprint` Opções ou.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-117">This option should be used when specifying the certificate via `-CertificateSubjectName` or `-CertificateFingerprint` options.</span></span>

- **`-CertificateStoreName`**

  <span data-ttu-id="a1c3c-118">Especifica o nome do repositório de certificados X. 509 a ser usado para pesquisar o certificado.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-118">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="a1c3c-119">O padrão é "My", o repositório de certificados X. 509 para certificados pessoais.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-119">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="a1c3c-120">Essa opção deve ser usada ao especificar o certificado por meio de `-CertificateSubjectName` `-CertificateFingerprint` Opções ou.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-120">This option should be used when specifying the certificate via `-CertificateSubjectName` or `-CertificateFingerprint` options.</span></span>

- **`-CertificateSubjectName`**

  <span data-ttu-id="a1c3c-121">Especifica o nome da entidade do certificado usado para pesquisar um repositório de certificados local para o certificado.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-121">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="a1c3c-122">A pesquisa é uma comparação de cadeias de caracteres que não diferencia maiúsculas de minúsculas usando o valor fornecido, que encontrará todos os certificados com o nome da entidade que contém essa cadeia de caracteres, independentemente de outros valores de entidade.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-122">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="a1c3c-123">O repositório de certificados pode ser especificado por `-CertificateStoreName` e `-CertificateStoreLocation` opções.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-123">The certificate store can be specified by `-CertificateStoreName` and `-CertificateStoreLocation` options.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="a1c3c-124">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a1c3c-125">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="a1c3c-126">Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-126">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-HashAlgorithm`**

  <span data-ttu-id="a1c3c-127">Algoritmo de hash a ser usado para assinar o pacote.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-127">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="a1c3c-128">O padrão é SHA256.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-128">Defaults to SHA256.</span></span> <span data-ttu-id="a1c3c-129">Os valores possíveis são SHA256, SHA384 e SHA512.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-129">Possible values are SHA256, SHA384, and SHA512.</span></span>

- **`-?|-help`**

  <span data-ttu-id="a1c3c-130">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-130">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="a1c3c-131">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-131">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="a1c3c-132">Especifica o diretório em que o pacote assinado deve ser salvo.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-132">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="a1c3c-133">Por padrão, o pacote original é substituído pelo pacote assinado.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-133">By default the original package is overwritten by the signed package.</span></span>

- **`-Overwrite`**

  <span data-ttu-id="a1c3c-134">Alterne para indicar se a assinatura atual deve ser substituída.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-134">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="a1c3c-135">Por padrão, o comando falhará se o pacote já tiver uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-135">By default the command will fail if the package already has a signature.</span></span>

- **`-Timestamper`**

  <span data-ttu-id="a1c3c-136">URL para um servidor de carimbo de data/hora RFC 3161.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-136">URL to an RFC 3161 timestamping server.</span></span>

- **`-TimestampHashAlgorithm`**

  <span data-ttu-id="a1c3c-137">Algoritmo de hash a ser usado pelo servidor de carimbo de data/hora RFC 3161.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-137">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="a1c3c-138">O padrão é SHA256.</span><span class="sxs-lookup"><span data-stu-id="a1c3c-138">Defaults to SHA256.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="a1c3c-139">Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="a1c3c-139">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="a1c3c-140">Exemplos</span><span class="sxs-lookup"><span data-stu-id="a1c3c-140">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath .\..\certificate.pfx -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -CertificateStoreLocation CurrentUser -CertificateStoreName My -CertificateSubjectName 'subject name' -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
