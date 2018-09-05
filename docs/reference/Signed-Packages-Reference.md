---
title: Pacotes assinados
description: Requisitos de assinatura de pacote do NuGet.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c36db9486ad787f19430c75fc38a2e9dd8ba6e37
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550415"
---
# <a name="signed-packages"></a><span data-ttu-id="1d04f-103">Pacotes assinados</span><span class="sxs-lookup"><span data-stu-id="1d04f-103">Signed packages</span></span>

<span data-ttu-id="1d04f-104">*4.6.0+ do NuGet e o Visual Studio 2017 versão 15.6 e posterior*</span><span class="sxs-lookup"><span data-stu-id="1d04f-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="1d04f-105">Pacotes do NuGet podem incluir uma assinatura digital que fornece proteção contra conteúdo violado.</span><span class="sxs-lookup"><span data-stu-id="1d04f-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="1d04f-106">Essa assinatura é produzida a partir de um certificado X.509 que também adiciona provas de autenticidade à origem do pacote real.</span><span class="sxs-lookup"><span data-stu-id="1d04f-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="1d04f-107">Os pacotes assinados fornecem a validação de ponta a ponta mais forte.</span><span class="sxs-lookup"><span data-stu-id="1d04f-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="1d04f-108">Há dois tipos diferentes de assinaturas do NuGet:</span><span class="sxs-lookup"><span data-stu-id="1d04f-108">There are two different types of NuGet signatures:</span></span>
- <span data-ttu-id="1d04f-109">**Criar assinatura**.</span><span class="sxs-lookup"><span data-stu-id="1d04f-109">**Author Signature**.</span></span> <span data-ttu-id="1d04f-110">Uma assinatura do autor garante que o pacote não foi modificado desde que o autor assinou o pacote, não importa de que o repositório ou o que o pacote é entregue de método de transporte.</span><span class="sxs-lookup"><span data-stu-id="1d04f-110">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span> <span data-ttu-id="1d04f-111">Além disso, pacotes assinados pelo autor fornecem um mecanismo de autenticação extra para o pipeline de publicação do nuget.org, porque o certificado de autenticação deve ser registrado antes do tempo.</span><span class="sxs-lookup"><span data-stu-id="1d04f-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="1d04f-112">Para obter mais informações, consulte [registrar certificados](#register-certificate-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="1d04f-112">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>
- <span data-ttu-id="1d04f-113">**Assinatura do repositório**.</span><span class="sxs-lookup"><span data-stu-id="1d04f-113">**Repository Signature**.</span></span> <span data-ttu-id="1d04f-114">Assinaturas de repositório fornecem uma garantia de integridade para **todos os** pacotes em um repositório, independentemente de estarem autor assinada ou não, mesmo que esses pacotes sejam obtidos de um local diferente do repositório original em que estavam assinado.</span><span class="sxs-lookup"><span data-stu-id="1d04f-114">Repository signatures provide an integrity guarantee for **all** packages in a repository whether they are author signed or not, even if those packages are obtained from a different location than the original repository where they were signed.</span></span>   

<span data-ttu-id="1d04f-115">Para obter detalhes sobre como criar um pacote assinado do autor, consulte [assinatura de pacotes](../create-packages/Sign-a-package.md) e o [comando nuget a entrada](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="1d04f-115">For details on creating an author signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="1d04f-116">Atualmente, há suporte para a assinatura do pacote somente ao usar nuget.exe no Windows.</span><span class="sxs-lookup"><span data-stu-id="1d04f-116">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="1d04f-117">Verificação de pacotes assinados tem suporte atualmente somente ao usar nuget.exe ou o Visual Studio no Windows.</span><span class="sxs-lookup"><span data-stu-id="1d04f-117">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="1d04f-118">Requisitos de certificado</span><span class="sxs-lookup"><span data-stu-id="1d04f-118">Certificate requirements</span></span>

<span data-ttu-id="1d04f-119">Assinatura do pacote requer um código de assinatura de certificado, que é um tipo especial de certificado é válido para o `id-kp-codeSigning` finalidade [[RFC 5280 seção 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="1d04f-119">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="1d04f-120">Além disso, o certificado deve ter um público comprimento da chave RSA de 2048 bits ou superior.</span><span class="sxs-lookup"><span data-stu-id="1d04f-120">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="1d04f-121">Obtenha um certificado de assinatura de código</span><span class="sxs-lookup"><span data-stu-id="1d04f-121">Get a code signing certificate</span></span>

<span data-ttu-id="1d04f-122">Certificados válidos podem ser obtidos de uma autoridade de certificação pública, como:</span><span class="sxs-lookup"><span data-stu-id="1d04f-122">Valid certificates may be obtained from a public certificate authority like:</span></span>

- [<span data-ttu-id="1d04f-123">Symantec</span><span class="sxs-lookup"><span data-stu-id="1d04f-123">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="1d04f-124">DigiCert</span><span class="sxs-lookup"><span data-stu-id="1d04f-124">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="1d04f-125">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="1d04f-125">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="1d04f-126">Entrada global</span><span class="sxs-lookup"><span data-stu-id="1d04f-126">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="1d04f-127">Comodo</span><span class="sxs-lookup"><span data-stu-id="1d04f-127">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="1d04f-128">Certum</span><span class="sxs-lookup"><span data-stu-id="1d04f-128">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="1d04f-129">A lista completa de autoridades de certificação confiável para Windows pode ser obtida [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="1d04f-129">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="1d04f-130">Criar um certificado de teste</span><span class="sxs-lookup"><span data-stu-id="1d04f-130">Create a test certificate</span></span>

<span data-ttu-id="1d04f-131">Você pode usar certificados emitidos por conta própria para fins de teste.</span><span class="sxs-lookup"><span data-stu-id="1d04f-131">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="1d04f-132">Para criar um certificado emitido por conta própria, use o [comando do PowerShell New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span><span class="sxs-lookup"><span data-stu-id="1d04f-132">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

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

<span data-ttu-id="1d04f-133">Este comando cria um certificado de teste disponível no repositório de certificados pessoais do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="1d04f-133">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="1d04f-134">Você pode abrir o repositório de certificados executando `certmgr.msc` para ver o certificado recém-criado.</span><span class="sxs-lookup"><span data-stu-id="1d04f-134">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="1d04f-135">NuGet.org não aceita pacotes assinados com certificados emitidos por conta própria.</span><span class="sxs-lookup"><span data-stu-id="1d04f-135">nuget.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="1d04f-136">Requisitos de carimbo de hora</span><span class="sxs-lookup"><span data-stu-id="1d04f-136">Timestamp requirements</span></span>

<span data-ttu-id="1d04f-137">Pacotes assinados devem incluir um carimbo de hora RFC 3161 para garantir a validade da assinatura além do período de validade do certificado de assinatura de pacote.</span><span class="sxs-lookup"><span data-stu-id="1d04f-137">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="1d04f-138">O certificado usado para assinar o carimbo de hora deve ser válido para o `id-kp-timeStamping` finalidade [[RFC 5280 seção 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="1d04f-138">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="1d04f-139">Além disso, o certificado deve ter um público comprimento da chave RSA de 2048 bits ou superior.</span><span class="sxs-lookup"><span data-stu-id="1d04f-139">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="1d04f-140">Detalhes técnicos adicionais podem ser encontrados na [especificações técnicas de assinatura de pacote](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="1d04f-140">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="1d04f-141">Requisitos de assinatura em nuget.org</span><span class="sxs-lookup"><span data-stu-id="1d04f-141">Signature requirements on nuget.org</span></span>

<span data-ttu-id="1d04f-142">NuGet.org tem requisitos adicionais para aceitar um pacote assinado:</span><span class="sxs-lookup"><span data-stu-id="1d04f-142">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="1d04f-143">A assinatura principal deve ser uma assinatura do autor.</span><span class="sxs-lookup"><span data-stu-id="1d04f-143">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="1d04f-144">A assinatura principal deve ter um único carimbo de hora válido.</span><span class="sxs-lookup"><span data-stu-id="1d04f-144">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="1d04f-145">Os certificados x. 509 para a assinatura do autor e sua assinatura do carimbo de hora:</span><span class="sxs-lookup"><span data-stu-id="1d04f-145">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="1d04f-146">Deve ter uma chave pública do RSA de 2048 bits ou superior.</span><span class="sxs-lookup"><span data-stu-id="1d04f-146">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="1d04f-147">Deve estar dentro do período de validade por hora UTC atual em tempo de validação de pacote em nuget.org.</span><span class="sxs-lookup"><span data-stu-id="1d04f-147">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="1d04f-148">Devem estar vinculados a uma autoridade raiz confiável que é confiável por padrão no Windows.</span><span class="sxs-lookup"><span data-stu-id="1d04f-148">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="1d04f-149">Pacotes assinados com certificados emitidos por conta própria serão rejeitados.</span><span class="sxs-lookup"><span data-stu-id="1d04f-149">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="1d04f-150">Deve ser válido para sua finalidade:</span><span class="sxs-lookup"><span data-stu-id="1d04f-150">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="1d04f-151">O autor do certificado de autenticação deve ser válido para assinatura de código.</span><span class="sxs-lookup"><span data-stu-id="1d04f-151">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="1d04f-152">O certificado de carimbo de hora deve ser válido para o carimbo de hora.</span><span class="sxs-lookup"><span data-stu-id="1d04f-152">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="1d04f-153">Não deve ser revogado a hora da assinatura.</span><span class="sxs-lookup"><span data-stu-id="1d04f-153">Must not be revoked at signing time.</span></span> <span data-ttu-id="1d04f-154">(Isso pode não estar knowable no momento do envio, portanto, o nuget.org periodicamente verifica novamente o status de revogação).</span><span class="sxs-lookup"><span data-stu-id="1d04f-154">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>

## <a name="register-certificate-on-nugetorg"></a><span data-ttu-id="1d04f-155">Registrar o certificado em nuget.org</span><span class="sxs-lookup"><span data-stu-id="1d04f-155">Register certificate on nuget.org</span></span>

<span data-ttu-id="1d04f-156">Para enviar um pacote assinado, você deve primeiro registrar o certificado com nuget.org. Você precisa do certificado como um `.cer` arquivo em um formato DER binário.</span><span class="sxs-lookup"><span data-stu-id="1d04f-156">To submit a signed package, you must first register the certificate with nuget.org. You need the certificate as a `.cer` file in a binary DER format.</span></span> <span data-ttu-id="1d04f-157">Você pode exportar um certificado existente para um formato DER binário usando o Assistente para exportação de certificados.</span><span class="sxs-lookup"><span data-stu-id="1d04f-157">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

![Assistente para exportação de certificados](media/CertificateExportWizard.png)

<span data-ttu-id="1d04f-159">Os usuários avançados podem exportar o certificado usando o [comando do PowerShell do certificado de exportação](/powershell/module/pkiclient/export-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="1d04f-159">Advanced users can export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

<span data-ttu-id="1d04f-160">Para registrar o certificado em nuget.org, vá para `Certificates` seção `Account settings` página (ou página de configurações da organização) e selecione `Register new certificate`.</span><span class="sxs-lookup"><span data-stu-id="1d04f-160">To register the certificate with nuget.org, go to `Certificates` section on `Account settings` page (or the Organization's settings page) and select `Register new certificate`.</span></span>

![Certificados registrados](media/registered-certs.png)

> [!Tip]
> <span data-ttu-id="1d04f-162">Um usuário pode enviar que vários certificados e o mesmo certificado podem ser registrados por vários usuários.</span><span class="sxs-lookup"><span data-stu-id="1d04f-162">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>

<span data-ttu-id="1d04f-163">Depois que um usuário tem um certificado registrado, todos os envios de futuras do pacote **deve** ser assinado com um dos certificados.</span><span class="sxs-lookup"><span data-stu-id="1d04f-163">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span>

<span data-ttu-id="1d04f-164">Os usuários também podem remover um certificado registrado da conta.</span><span class="sxs-lookup"><span data-stu-id="1d04f-164">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="1d04f-165">Depois que um certificado é removido, pacotes assinados com esse certificado falharem no envio.</span><span class="sxs-lookup"><span data-stu-id="1d04f-165">Once a certificate is removed, packages signed with that certificate fail at submission.</span></span> <span data-ttu-id="1d04f-166">Os pacotes existentes não serão afetados.</span><span class="sxs-lookup"><span data-stu-id="1d04f-166">Existing packages aren't affected.</span></span>

## <a name="configure-package-signing-requirements"></a><span data-ttu-id="1d04f-167">Configurar requisitos de assinatura de pacote</span><span class="sxs-lookup"><span data-stu-id="1d04f-167">Configure package signing requirements</span></span>

<span data-ttu-id="1d04f-168">Se você for o único proprietário de um pacote, você é o signatário necessário.</span><span class="sxs-lookup"><span data-stu-id="1d04f-168">If you are the sole owner of a package, you are the required signer.</span></span> <span data-ttu-id="1d04f-169">Ou seja, você pode usar qualquer um dos certificados registrados para assinar seus pacotes e enviar para o nuget.org.</span><span class="sxs-lookup"><span data-stu-id="1d04f-169">That is, you can use any of the registered certificates to sign your packages and submit to nuget.org.</span></span>

<span data-ttu-id="1d04f-170">Se um pacote tem vários proprietários, por padrão, os certificados de "Qualquer" do proprietário podem ser usados para assinar o pacote.</span><span class="sxs-lookup"><span data-stu-id="1d04f-170">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="1d04f-171">Como um coproprietário do pacote, você pode substituir "Qualquer" com por conta própria ou qualquer outro coproprietário para ser o signatário necessário.</span><span class="sxs-lookup"><span data-stu-id="1d04f-171">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="1d04f-172">Se você fizer um proprietário que não tem qualquer certificado registrado, serão permitidos pacotes não assinados.</span><span class="sxs-lookup"><span data-stu-id="1d04f-172">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

<span data-ttu-id="1d04f-173">Da mesma forma, se o padrão "Qualquer" opção estiver selecionada para um pacote em que um proprietário tem um certificado registrado e o outro proprietário não tiver nenhum certificado registrado, em seguida, nuget.org aceita qualquer um pacote assinado com uma assinatura registrada por um de seus proprietários ou sem uma assinatura do pacote (porque um dos proprietários não tem qualquer certificado registrado).</span><span class="sxs-lookup"><span data-stu-id="1d04f-173">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then nuget.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

![Configurar signatários de pacote](media/configure-package-signers.png)
