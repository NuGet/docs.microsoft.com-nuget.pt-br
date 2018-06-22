---
title: Pacotes assinados
description: Requisitos de assinatura de pacote do NuGet.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 72fb1a87c13160c53f632d2ef87a12a4e9bc02a3
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/22/2018
ms.locfileid: "34449585"
---
# <a name="signed-packages"></a><span data-ttu-id="9b408-103">Pacotes assinados</span><span class="sxs-lookup"><span data-stu-id="9b408-103">Signed packages</span></span>

<span data-ttu-id="9b408-104">*NuGet 4.6.0+ e Visual Studio 2017 versão 15.6 e posterior*</span><span class="sxs-lookup"><span data-stu-id="9b408-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="9b408-105">Pacotes do NuGet podem incluir uma assinatura digital que fornece proteção contra conteúdo violada.</span><span class="sxs-lookup"><span data-stu-id="9b408-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="9b408-106">Esta assinatura é gerada de um certificado x. 509 que também adiciona provas autenticidade à origem do pacote real.</span><span class="sxs-lookup"><span data-stu-id="9b408-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="9b408-107">Pacotes assinados fornecem a validação de ponta a ponta mais forte.</span><span class="sxs-lookup"><span data-stu-id="9b408-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="9b408-108">Uma assinatura de autor garante que o pacote não foi modificado desde que o autor entrada o pacote, não importa qual repositório ou o que o pacote é entregue de método de transporte.</span><span class="sxs-lookup"><span data-stu-id="9b408-108">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span>

<span data-ttu-id="9b408-109">Além disso, os pacotes assinados pelo autor fornecem um mecanismo de autenticação extra para o pipeline de publicação nuget.org porque o certificado de autenticação deve ser registrado antes do tempo.</span><span class="sxs-lookup"><span data-stu-id="9b408-109">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="9b408-110">Para obter mais informações, consulte [registrar certificados](#register-certificate-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="9b408-110">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>

<span data-ttu-id="9b408-111">Para obter detalhes sobre como criar um pacote assinado, consulte [assinatura pacotes](../create-packages/Sign-a-package.md) e [comando de entrada do nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="9b408-111">For details on creating a signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="9b408-112">Atualmente há suporte para a assinatura do pacote somente quando usar nuget.exe no Windows.</span><span class="sxs-lookup"><span data-stu-id="9b408-112">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="9b408-113">Verificação de pacotes assinados é suportada atualmente apenas ao usar o nuget.exe ou o Visual Studio no Windows.</span><span class="sxs-lookup"><span data-stu-id="9b408-113">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="9b408-114">Requisitos de certificado</span><span class="sxs-lookup"><span data-stu-id="9b408-114">Certificate requirements</span></span>

<span data-ttu-id="9b408-115">Assinatura do pacote requer um código de assinatura de certificado, que é um tipo especial de certificado é válido para o `id-kp-codeSigning` finalidade [[RFC 5280 seção 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="9b408-115">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="9b408-116">Além disso, o certificado deve ter um público comprimento da chave RSA de 2048 bits ou superior.</span><span class="sxs-lookup"><span data-stu-id="9b408-116">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="9b408-117">Obter um certificado de assinatura de código</span><span class="sxs-lookup"><span data-stu-id="9b408-117">Get a code signing certificate</span></span>

<span data-ttu-id="9b408-118">Certificados válidos podem ser obtidos em uma autoridade de certificação pública, como:</span><span class="sxs-lookup"><span data-stu-id="9b408-118">Valid certificates may be obtained from a public certificate authority like:</span></span>

- [<span data-ttu-id="9b408-119">Symantec</span><span class="sxs-lookup"><span data-stu-id="9b408-119">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="9b408-120">DigiCert</span><span class="sxs-lookup"><span data-stu-id="9b408-120">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="9b408-121">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="9b408-121">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="9b408-122">Entrada global</span><span class="sxs-lookup"><span data-stu-id="9b408-122">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="9b408-123">Comodo</span><span class="sxs-lookup"><span data-stu-id="9b408-123">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="9b408-124">Certum</span><span class="sxs-lookup"><span data-stu-id="9b408-124">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="9b408-125">A lista completa de autoridades de certificação confiada pelo Windows pode ser obtida [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="9b408-125">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="9b408-126">Criar um certificado de teste</span><span class="sxs-lookup"><span data-stu-id="9b408-126">Create a test certificate</span></span>

<span data-ttu-id="9b408-127">Você pode usar certificados emitidos por conta própria para fins de teste.</span><span class="sxs-lookup"><span data-stu-id="9b408-127">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="9b408-128">Para criar um certificado emitido por conta própria, use o [comando do PowerShell New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span><span class="sxs-lookup"><span data-stu-id="9b408-128">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

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

<span data-ttu-id="9b408-129">Este comando cria um certificado de teste disponível no repositório de certificados pessoais do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="9b408-129">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="9b408-130">Você pode abrir o repositório de certificados executando `certmgr.msc` para ver o certificado recém-criado.</span><span class="sxs-lookup"><span data-stu-id="9b408-130">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="9b408-131">NuGet.org não aceita pacotes assinados com certificados emitidos por conta própria.</span><span class="sxs-lookup"><span data-stu-id="9b408-131">nuget.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="9b408-132">Requisitos de carimbo de hora</span><span class="sxs-lookup"><span data-stu-id="9b408-132">Timestamp requirements</span></span>

<span data-ttu-id="9b408-133">Pacotes assinados devem incluir um carimbo de hora do RFC 3161 para garantir a validade da assinatura além do período de validade do certificado de assinatura de pacote.</span><span class="sxs-lookup"><span data-stu-id="9b408-133">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="9b408-134">O certificado usado para assinar o carimbo de hora deve ser válido para o `id-kp-timeStamping` finalidade [[RFC 5280 seção 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="9b408-134">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="9b408-135">Além disso, o certificado deve ter um público comprimento da chave RSA de 2048 bits ou superior.</span><span class="sxs-lookup"><span data-stu-id="9b408-135">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="9b408-136">Detalhes técnicos adicionais podem ser encontrados no [especificações técnicas de assinatura do pacote](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="9b408-136">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="9b408-137">Requisitos de assinatura em nuget.org</span><span class="sxs-lookup"><span data-stu-id="9b408-137">Signature requirements on nuget.org</span></span>

<span data-ttu-id="9b408-138">NuGet.org tem requisitos adicionais para aceitar um pacote assinado:</span><span class="sxs-lookup"><span data-stu-id="9b408-138">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="9b408-139">A assinatura principal deve ser uma assinatura do autor.</span><span class="sxs-lookup"><span data-stu-id="9b408-139">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="9b408-140">A assinatura principal deve ter um único carimbo válido.</span><span class="sxs-lookup"><span data-stu-id="9b408-140">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="9b408-141">Os certificados x. 509 para a assinatura do autor e sua assinatura de carimbo de hora:</span><span class="sxs-lookup"><span data-stu-id="9b408-141">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="9b408-142">Deve ter uma chave pública RSA de 2048 bits ou superior.</span><span class="sxs-lookup"><span data-stu-id="9b408-142">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="9b408-143">Deve estar dentro do período de validade por hora UTC atual em tempo de validação de pacote em nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9b408-143">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="9b408-144">Devem se encadear a uma autoridade raiz confiável que é confiável por padrão no Windows.</span><span class="sxs-lookup"><span data-stu-id="9b408-144">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="9b408-145">Pacotes assinados com certificados emitidos por conta própria são rejeitados.</span><span class="sxs-lookup"><span data-stu-id="9b408-145">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="9b408-146">Deve ser válido para sua finalidade:</span><span class="sxs-lookup"><span data-stu-id="9b408-146">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="9b408-147">O autor do certificado de assinatura deve ser válido para assinatura de código.</span><span class="sxs-lookup"><span data-stu-id="9b408-147">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="9b408-148">O certificado de carimbo de hora deve ser válido para o carimbo de hora.</span><span class="sxs-lookup"><span data-stu-id="9b408-148">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="9b408-149">Não deve ser revogado a hora da assinatura.</span><span class="sxs-lookup"><span data-stu-id="9b408-149">Must not be revoked at signing time.</span></span> <span data-ttu-id="9b408-150">(Isso poderá não ser knowable no momento do envio, portanto nuget.org verifica o status de revogação periodicamente novamente).</span><span class="sxs-lookup"><span data-stu-id="9b408-150">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>

## <a name="register-certificate-on-nugetorg"></a><span data-ttu-id="9b408-151">Registrar certificado em nuget.org</span><span class="sxs-lookup"><span data-stu-id="9b408-151">Register certificate on nuget.org</span></span>

<span data-ttu-id="9b408-152">Para enviar um pacote assinado, você deve primeiro registrar o certificado com nuget.org. É necessário o certificado como um `.cer` arquivo em formato binário DER.</span><span class="sxs-lookup"><span data-stu-id="9b408-152">To submit a signed package, you must first register the certificate with nuget.org. You need the certificate as a `.cer` file in a binary DER format.</span></span> <span data-ttu-id="9b408-153">Você pode exportar um certificado existente para um formato DER binário usando o Assistente para exportação de certificados.</span><span class="sxs-lookup"><span data-stu-id="9b408-153">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

![Assistente para exportação de certificados](media/CertificateExportWizard.png)

<span data-ttu-id="9b408-155">Usuários avançados podem exportar o certificado usando o [comando do PowerShell do certificado de exportação](/powershell/module/pkiclient/export-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="9b408-155">Advanced users can export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

<span data-ttu-id="9b408-156">Para registrar o certificado com nuget.org, vá para `Certificates` seção `Account settings` página (ou a página de configurações da organização) e selecione `Register new certificate`.</span><span class="sxs-lookup"><span data-stu-id="9b408-156">To register the certificate with nuget.org, go to `Certificates` section on `Account settings` page (or the Organization's settings page) and select `Register new certificate`.</span></span>

![Certificados registrados](media/registered-certs.png)

> [!Tip]
> <span data-ttu-id="9b408-158">Um usuário pode enviar que vários certificados e o mesmo certificado podem ser registrados por vários usuários.</span><span class="sxs-lookup"><span data-stu-id="9b408-158">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>

<span data-ttu-id="9b408-159">Depois que um usuário tem um certificado registrado, todos os envios de pacote futuras **deve** ser assinado com um dos certificados.</span><span class="sxs-lookup"><span data-stu-id="9b408-159">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span>

<span data-ttu-id="9b408-160">Os usuários também podem remover um certificado registrado da conta.</span><span class="sxs-lookup"><span data-stu-id="9b408-160">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="9b408-161">Depois que um certificado é removido, pacotes assinados com esse certificado falham no envio.</span><span class="sxs-lookup"><span data-stu-id="9b408-161">Once a certificate is removed, packages signed with that certificate fail at submission.</span></span> <span data-ttu-id="9b408-162">Os pacotes existentes não serão afetados.</span><span class="sxs-lookup"><span data-stu-id="9b408-162">Existing packages aren't affected.</span></span>

## <a name="configure-package-signing-requirements"></a><span data-ttu-id="9b408-163">Configurar requisitos de assinatura de pacote</span><span class="sxs-lookup"><span data-stu-id="9b408-163">Configure package signing requirements</span></span>

<span data-ttu-id="9b408-164">Se você for o único proprietário de um pacote, você é o signatário necessário.</span><span class="sxs-lookup"><span data-stu-id="9b408-164">If you are the sole owner of a package, you are the required signer.</span></span> <span data-ttu-id="9b408-165">Ou seja, você pode usar qualquer um dos certificados registrados para assinar seus pacotes e enviá-las a nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9b408-165">That is, you can use any of the registered certificates to sign your packages and submit to nuget.org.</span></span>

<span data-ttu-id="9b408-166">Se um pacote tem vários proprietários, por padrão, os certificados de "Qualquer" do proprietário podem ser usados para assinar o pacote.</span><span class="sxs-lookup"><span data-stu-id="9b408-166">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="9b408-167">Como coproprietário do pacote, você pode substituir "Qualquer" com o mesmo ou outro proprietário colegas para ser o signatário necessário.</span><span class="sxs-lookup"><span data-stu-id="9b408-167">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="9b408-168">Se você fizer um proprietário que não tem nenhum certificado registrado, serão permitidos pacotes não assinados.</span><span class="sxs-lookup"><span data-stu-id="9b408-168">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

<span data-ttu-id="9b408-169">Da mesma forma, se o padrão "Qualquer" opção está selecionada para um pacote em que um proprietário tem um certificado registrado e outro proprietário não tiver nenhum certificado registrado, então nuget.org aceita ou um pacote assinado com uma assinatura registrada por um de seus proprietários ou sem uma assinatura do pacote (porque um dos proprietários não tem nenhum certificado registrado).</span><span class="sxs-lookup"><span data-stu-id="9b408-169">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then nuget.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

![Configurar signatários de pacote](media/configure-package-signers.png)
