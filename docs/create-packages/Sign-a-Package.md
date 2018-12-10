---
title: Assinando pacotes NuGet
description: Explica como os pacotes assinados podem ser usados para habilitar a verificação de integridade de conteúdo.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: e8955f9d46bab235c8755d5654814a4291d542d6
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977557"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="4292f-103">Assinando pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="4292f-103">Signing NuGet Packages</span></span>

<span data-ttu-id="4292f-104">Os pacotes assinados permitem verificações de integridade do conteúdo que oferecem proteção contra violação de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="4292f-104">Signed packages allows for content integrity verification checks which provides protection against content tampering.</span></span> <span data-ttu-id="4292f-105">A assinatura do pacote também serve como a única fonte de verdade sobre a origem real do pacote e reforça a autenticidade do pacote para o consumidor.</span><span class="sxs-lookup"><span data-stu-id="4292f-105">The package signature also serves as the single source of truth about the actual origin of the package and bolsters package authenticity for the consumer.</span></span> <span data-ttu-id="4292f-106">Este guia pressupõe que você já [criou um pacote](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="4292f-106">This guide assumes you have already [created a package](creating-a-package.md).</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="4292f-107">Obter um certificado de assinatura de código</span><span class="sxs-lookup"><span data-stu-id="4292f-107">Get a code signing certificate</span></span>

<span data-ttu-id="4292f-108">Certificados válidos podem ser obtidos de uma autoridade de certificação pública, como [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) etc. A lista completa de autoridades de certificação confiáveis para Windows pode ser obtida de [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="4292f-108">Valid certificates may be obtained from a public certificate authority such as [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

<span data-ttu-id="4292f-109">Você pode usar certificados emitidos por conta própria para fins de teste.</span><span class="sxs-lookup"><span data-stu-id="4292f-109">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="4292f-110">No entanto, os pacotes assinados com certificados emitidos por conta própria não são aceitos por NuGet.org. Saiba mais sobre a [criação de um certificado de teste](#create-a-test-certificate)</span><span class="sxs-lookup"><span data-stu-id="4292f-110">However, packages signed using self-issued certificates are not accepted by NuGet.org. Learn more about [creating a test certificate](#create-a-test-certificate)</span></span>

## <a name="export-the-certificate-file"></a><span data-ttu-id="4292f-111">Exportar o arquivo do certificado</span><span class="sxs-lookup"><span data-stu-id="4292f-111">Export the certificate file</span></span>

* <span data-ttu-id="4292f-112">Você pode exportar um certificado existente para um formato DER binário usando o Assistente de Exportação de Certificados.</span><span class="sxs-lookup"><span data-stu-id="4292f-112">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

  ![Assistente de Exportação de Certificados](../reference/media/CertificateExportWizard.png)

* <span data-ttu-id="4292f-114">Você também pode exportar o certificado usando o [comando Export-Certificate do PowerShell](/powershell/module/pkiclient/export-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="4292f-114">You can also export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

## <a name="sign-the-package"></a><span data-ttu-id="4292f-115">Assinar o pacote</span><span class="sxs-lookup"><span data-stu-id="4292f-115">Sign the package</span></span>

> [!note]
> <span data-ttu-id="4292f-116">Requer o nuget.exe 4.6.0 ou posterior</span><span class="sxs-lookup"><span data-stu-id="4292f-116">Requires nuget.exe 4.6.0 or later</span></span>

<span data-ttu-id="4292f-117">Assinar o pacote usando [nuget sign](../tools/cli-ref-sign.md):</span><span class="sxs-lookup"><span data-stu-id="4292f-117">Sign the package using [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateFilePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

* <span data-ttu-id="4292f-118">Você pode usar um certificado disponível no repositório de certificados ou usar um certificado de um arquivo.</span><span class="sxs-lookup"><span data-stu-id="4292f-118">You can use a certificate available in the certificate store or use a certificate from a file.</span></span> <span data-ttu-id="4292f-119">Consulte a CLI de referência para [nuget sign](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="4292f-119">See CLI reference for [nuget sign](../tools/cli-ref-sign.md).</span></span>
* <span data-ttu-id="4292f-120">Os pacotes assinados devem incluir um carimbo de data/hora para assegurar que a assinatura permaneça válida quando o certificado de autenticação expira.</span><span class="sxs-lookup"><span data-stu-id="4292f-120">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="4292f-121">Caso contrário, a operação de entrada produzirá um [aviso](../reference/errors-and-warnings/NU3002.md).</span><span class="sxs-lookup"><span data-stu-id="4292f-121">Else the sign operation will produce a [warning](../reference/errors-and-warnings/NU3002.md).</span></span>
* <span data-ttu-id="4292f-122">Você pode usar [nuget verify](../tools/cli-ref-verify.md) para ver os detalhes da assinatura de um determinado pacote.</span><span class="sxs-lookup"><span data-stu-id="4292f-122">You can see the signature details of a given package using [nuget verify](../tools/cli-ref-verify.md).</span></span>

## <a name="register-the-certificate-on-nugetorg"></a><span data-ttu-id="4292f-123">Registrar o certificado em NuGet.org</span><span class="sxs-lookup"><span data-stu-id="4292f-123">Register the certificate on NuGet.org</span></span>

<span data-ttu-id="4292f-124">Para publicar um pacote assinado, você deverá primeiro registrar o certificado com NuGet.org. Você precisa do certificado como um arquivo `.cer` em um formato DER binário.</span><span class="sxs-lookup"><span data-stu-id="4292f-124">To publish a signed package, you must first register the certificate with NuGet.org. You need the certificate as a `.cer` file in a binary DER format.</span></span>

1. <span data-ttu-id="4292f-125">[Entre](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) em NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="4292f-125">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>
1. <span data-ttu-id="4292f-126">Vá para `Account settings` (ou `Manage Organization` **>** `Edit Organziation` se você gostaria de registrar o certificado com uma conta de organização).</span><span class="sxs-lookup"><span data-stu-id="4292f-126">Go to `Account settings` (or `Manage Organization` **>** `Edit Organziation` if you would like to register the certificate with an Organization account).</span></span>
1. <span data-ttu-id="4292f-127">Expanda a seção `Certificates` e selecione `Register new`.</span><span class="sxs-lookup"><span data-stu-id="4292f-127">Expand the `Certificates` section and select `Register new`.</span></span>
1. <span data-ttu-id="4292f-128">Procure e selecione o arquivo de certificado que foi exportado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4292f-128">Browse and select the certficate file that was exported earlier.</span></span>
  <span data-ttu-id="4292f-129">![Certificados registrados](../reference/media/registered-certs.png)</span><span class="sxs-lookup"><span data-stu-id="4292f-129">![Registered Certificates](../reference/media/registered-certs.png)</span></span>

<span data-ttu-id="4292f-130">**Observação**</span><span class="sxs-lookup"><span data-stu-id="4292f-130">**Note**</span></span>
* <span data-ttu-id="4292f-131">Um usuário pode enviar vários certificados e o mesmo certificado pode ser registrado por vários usuários.</span><span class="sxs-lookup"><span data-stu-id="4292f-131">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>
* <span data-ttu-id="4292f-132">Depois que um usuário tem um certificado registrado, todos os envios de pacote futuros **precisam** ser assinados com um dos certificados.</span><span class="sxs-lookup"><span data-stu-id="4292f-132">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span> <span data-ttu-id="4292f-133">Veja [Gerenciar os requisitos de assinatura do seu pacote em NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span><span class="sxs-lookup"><span data-stu-id="4292f-133">See [Manage signing requirements for your package on NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span></span>
* <span data-ttu-id="4292f-134">Os usuários também podem remover um certificado registrado da conta.</span><span class="sxs-lookup"><span data-stu-id="4292f-134">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="4292f-135">Depois que um certificado é removido, o envio de novos pacotes assinados com esse certificado falhará.</span><span class="sxs-lookup"><span data-stu-id="4292f-135">Once a certificate is removed, new packages signed with that certificate will fail at submission.</span></span> <span data-ttu-id="4292f-136">Os pacotes existentes não serão afetados.</span><span class="sxs-lookup"><span data-stu-id="4292f-136">Existing packages aren't affected.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="4292f-137">Publicar o pacote</span><span class="sxs-lookup"><span data-stu-id="4292f-137">Publish the package</span></span>

<span data-ttu-id="4292f-138">Agora você está pronto para publicar o pacote em NuGet.org. Veja [Publicando pacotes](Publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="4292f-138">You are now ready to publish the package to NuGet.org. See [Publishing packages](Publish-a-package.md).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="4292f-139">Criar um certificado de teste</span><span class="sxs-lookup"><span data-stu-id="4292f-139">Create a test certificate</span></span>

<span data-ttu-id="4292f-140">Você pode usar certificados emitidos por conta própria para fins de teste.</span><span class="sxs-lookup"><span data-stu-id="4292f-140">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="4292f-141">Para criar um certificado emitido por conta própria, use o [comando New-SelfSignedCertificate do PowerShell](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span><span class="sxs-lookup"><span data-stu-id="4292f-141">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

```ps
New-SelfSignedCertificate -Subject "CN=NuGet Test Developer, OU=Use for testing purposes ONLY" `
                          -FriendlyName "NuGetTestDeveloper" `
                          -Type CodeSigning `
                          -KeyUsage DigitalSignature `
                          -KeyLength 2048 `
                          -KeyAlgorithm RSA `
                          -HashAlgorithm SHA256 `
                          -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
                          -CertStoreLocation "Cert:\CurrentUser\My" 
```

<span data-ttu-id="4292f-142">Este comando cria um certificado de teste disponível no repositório de certificados pessoal do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="4292f-142">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="4292f-143">Você pode abrir o repositório de certificados executando `certmgr.msc` para ver o certificado recém-criado.</span><span class="sxs-lookup"><span data-stu-id="4292f-143">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="4292f-144">O NuGet.org não aceita pacotes assinados com certificados emitidos por conta própria.</span><span class="sxs-lookup"><span data-stu-id="4292f-144">NuGet.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a><span data-ttu-id="4292f-145">Gerenciar os requisitos de assinatura do seu pacote em NuGet.org</span><span class="sxs-lookup"><span data-stu-id="4292f-145">Manage signing requirements for your package on NuGet.org</span></span>
1. <span data-ttu-id="4292f-146">[Entre](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) em NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="4292f-146">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>

1. <span data-ttu-id="4292f-147">Vá para `Manage Packages` 
   ![Configurar signatários do pacote](../reference/media/configure-package-signers.png)</span><span class="sxs-lookup"><span data-stu-id="4292f-147">Go to `Manage Packages` 
![Configure package signers](../reference/media/configure-package-signers.png)</span></span>

* <span data-ttu-id="4292f-148">Se for o único proprietário de um pacote, você será o signatário necessário, ou seja, poderá usar qualquer um dos certificados registrados para assinar e publicar seus pacotes em NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="4292f-148">If you are the sole owner of a package, you are the required signer i.e. you can use any of the registered certificates to sign and publish your packages to NuGet.org.</span></span>

* <span data-ttu-id="4292f-149">Se um pacote tem vários proprietários, por padrão, os certificados do proprietário "Qualquer" podem ser usados para assinar o pacote.</span><span class="sxs-lookup"><span data-stu-id="4292f-149">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="4292f-150">Como um coproprietário do pacote, você pode substituir "Qualquer" consigo mesmo ou com qualquer outro coproprietário para ser o signatário necessário.</span><span class="sxs-lookup"><span data-stu-id="4292f-150">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="4292f-151">Se você criar um proprietário que não tiver nenhum certificado registrado, os pacotes não assinados serão permitidos.</span><span class="sxs-lookup"><span data-stu-id="4292f-151">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

* <span data-ttu-id="4292f-152">Da mesma forma, se a opção "Qualquer" estiver selecionada para um pacote em que um proprietário tenha um certificado registrado e o outro proprietário não tenha nenhum certificado registrado, o NuGet.org aceitará um pacote assinado com uma assinatura registrada por um de seus proprietários ou então aceitará um pacote não assinado (porque um dos proprietários não tem nenhum certificado registrado).</span><span class="sxs-lookup"><span data-stu-id="4292f-152">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then NuGet.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

## <a name="related-articles"></a><span data-ttu-id="4292f-153">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="4292f-153">Related articles</span></span>

- [<span data-ttu-id="4292f-154">Instalando pacotes assinados</span><span class="sxs-lookup"><span data-stu-id="4292f-154">Installing signed packages</span></span>](../consume-packages/installing-signed-packages.md)
- [<span data-ttu-id="4292f-155">Referência de pacotes assinados</span><span class="sxs-lookup"><span data-stu-id="4292f-155">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
