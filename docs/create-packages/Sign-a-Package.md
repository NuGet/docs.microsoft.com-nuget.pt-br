---
title: Assinando pacotes NuGet
description: Explica como os pacotes assinados podem ser usados para habilitar a verificação de integridade de conteúdo.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 85a862852761b68db882abdc1ca0e84d83d95f07
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317634"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="df321-103">Assinando pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="df321-103">Signing NuGet Packages</span></span>

<span data-ttu-id="df321-104">Os pacotes assinados permitem verificações de integridade do conteúdo que oferecem proteção contra violação de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="df321-104">Signed packages allows for content integrity verification checks which provides protection against content tampering.</span></span> <span data-ttu-id="df321-105">A assinatura do pacote também serve como a única fonte de verdade sobre a origem real do pacote e reforça a autenticidade do pacote para o consumidor.</span><span class="sxs-lookup"><span data-stu-id="df321-105">The package signature also serves as the single source of truth about the actual origin of the package and bolsters package authenticity for the consumer.</span></span> <span data-ttu-id="df321-106">Este guia pressupõe que você já [criou um pacote](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="df321-106">This guide assumes you have already [created a package](creating-a-package.md).</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="df321-107">Obter um certificado de assinatura de código</span><span class="sxs-lookup"><span data-stu-id="df321-107">Get a code signing certificate</span></span>

<span data-ttu-id="df321-108">Certificados válidos podem ser obtidos de uma autoridade de certificação pública, como [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) etc. A lista completa de autoridades de certificação confiáveis para Windows pode ser obtida de [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="df321-108">Valid certificates may be obtained from a public certificate authority such as [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

<span data-ttu-id="df321-109">Você pode usar certificados emitidos por conta própria para fins de teste.</span><span class="sxs-lookup"><span data-stu-id="df321-109">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="df321-110">No entanto, os pacotes assinados com certificados emitidos por conta própria não são aceitos por NuGet.org. Saiba mais sobre a [criação de um certificado de teste](#create-a-test-certificate)</span><span class="sxs-lookup"><span data-stu-id="df321-110">However, packages signed using self-issued certificates are not accepted by NuGet.org. Learn more about [creating a test certificate](#create-a-test-certificate)</span></span>

## <a name="export-the-certificate-file"></a><span data-ttu-id="df321-111">Exportar o arquivo do certificado</span><span class="sxs-lookup"><span data-stu-id="df321-111">Export the certificate file</span></span>

* <span data-ttu-id="df321-112">Você pode exportar um certificado existente para um formato DER binário usando o Assistente de Exportação de Certificados.</span><span class="sxs-lookup"><span data-stu-id="df321-112">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

  ![Assistente de Exportação de Certificados](../reference/media/CertificateExportWizard.png)

* <span data-ttu-id="df321-114">Você também pode exportar o certificado usando o [comando Export-Certificate do PowerShell](/powershell/module/pkiclient/export-certificate).</span><span class="sxs-lookup"><span data-stu-id="df321-114">You can also export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate).</span></span>

## <a name="sign-the-package"></a><span data-ttu-id="df321-115">Assinar o pacote</span><span class="sxs-lookup"><span data-stu-id="df321-115">Sign the package</span></span>

> [!note]
> <span data-ttu-id="df321-116">Requer o nuget.exe 4.6.0 ou posterior</span><span class="sxs-lookup"><span data-stu-id="df321-116">Requires nuget.exe 4.6.0 or later</span></span>

<span data-ttu-id="df321-117">Assinar o pacote usando [nuget sign](../reference/cli-reference/cli-ref-sign.md):</span><span class="sxs-lookup"><span data-stu-id="df321-117">Sign the package using [nuget sign](../reference/cli-reference/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> <span data-ttu-id="df321-118">Geralmente, o provedor de certificado também fornece uma URL de servidor de carimbo de data/hora que pode ser usada para o argumento opcional `Timestamper` mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="df321-118">The certificate provider often also provides a timestamping server URL which you can use for the `Timestamper` optional argument show above.</span></span> <span data-ttu-id="df321-119">Consulte a documentação e/ou o suporte do seu provedor para essa URL de serviço.</span><span class="sxs-lookup"><span data-stu-id="df321-119">Consult with your provider's documentation and/or support for that service URL.</span></span>

* <span data-ttu-id="df321-120">Você pode usar um certificado disponível no repositório de certificados ou usar um certificado de um arquivo.</span><span class="sxs-lookup"><span data-stu-id="df321-120">You can use a certificate available in the certificate store or use a certificate from a file.</span></span> <span data-ttu-id="df321-121">Consulte a CLI de referência para [nuget sign](../reference/cli-reference/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="df321-121">See CLI reference for [nuget sign](../reference/cli-reference/cli-ref-sign.md).</span></span>
* <span data-ttu-id="df321-122">Os pacotes assinados devem incluir um carimbo de data/hora para assegurar que a assinatura permaneça válida quando o certificado de autenticação expira.</span><span class="sxs-lookup"><span data-stu-id="df321-122">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="df321-123">Caso contrário, a operação de entrada produzirá um [aviso](../reference/errors-and-warnings/NU3002.md).</span><span class="sxs-lookup"><span data-stu-id="df321-123">Else the sign operation will produce a [warning](../reference/errors-and-warnings/NU3002.md).</span></span>
* <span data-ttu-id="df321-124">Você pode usar [nuget verify](../reference/cli-reference/cli-ref-verify.md) para ver os detalhes da assinatura de um determinado pacote.</span><span class="sxs-lookup"><span data-stu-id="df321-124">You can see the signature details of a given package using [nuget verify](../reference/cli-reference/cli-ref-verify.md).</span></span>

## <a name="register-the-certificate-on-nugetorg"></a><span data-ttu-id="df321-125">Registrar o certificado em NuGet.org</span><span class="sxs-lookup"><span data-stu-id="df321-125">Register the certificate on NuGet.org</span></span>

<span data-ttu-id="df321-126">Para publicar um pacote assinado, você deverá primeiro registrar o certificado com NuGet.org. Você precisa do certificado como um arquivo `.cer` em um formato DER binário.</span><span class="sxs-lookup"><span data-stu-id="df321-126">To publish a signed package, you must first register the certificate with NuGet.org. You need the certificate as a `.cer` file in a binary DER format.</span></span>

1. <span data-ttu-id="df321-127">[Entre](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) em NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="df321-127">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>
1. <span data-ttu-id="df321-128">Vá para `Account settings` (ou `Manage Organization` **>** `Edit Organziation` se você gostaria de registrar o certificado com uma conta de organização).</span><span class="sxs-lookup"><span data-stu-id="df321-128">Go to `Account settings` (or `Manage Organization` **>** `Edit Organziation` if you would like to register the certificate with an Organization account).</span></span>
1. <span data-ttu-id="df321-129">Expanda a seção `Certificates` e selecione `Register new`.</span><span class="sxs-lookup"><span data-stu-id="df321-129">Expand the `Certificates` section and select `Register new`.</span></span>
1. <span data-ttu-id="df321-130">Procure e selecione o arquivo de certificado que foi exportado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="df321-130">Browse and select the certficate file that was exported earlier.</span></span>
  <span data-ttu-id="df321-131">![Certificados registrados](../reference/media/registered-certs.png)</span><span class="sxs-lookup"><span data-stu-id="df321-131">![Registered Certificates](../reference/media/registered-certs.png)</span></span>

<span data-ttu-id="df321-132">**Observação**</span><span class="sxs-lookup"><span data-stu-id="df321-132">**Note**</span></span>
* <span data-ttu-id="df321-133">Um usuário pode enviar vários certificados e o mesmo certificado pode ser registrado por vários usuários.</span><span class="sxs-lookup"><span data-stu-id="df321-133">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>
* <span data-ttu-id="df321-134">Depois que um usuário tem um certificado registrado, todos os envios de pacote futuros **precisam** ser assinados com um dos certificados.</span><span class="sxs-lookup"><span data-stu-id="df321-134">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span> <span data-ttu-id="df321-135">Veja [Gerenciar os requisitos de assinatura do seu pacote em NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span><span class="sxs-lookup"><span data-stu-id="df321-135">See [Manage signing requirements for your package on NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span></span>
* <span data-ttu-id="df321-136">Os usuários também podem remover um certificado registrado da conta.</span><span class="sxs-lookup"><span data-stu-id="df321-136">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="df321-137">Depois que um certificado é removido, o envio de novos pacotes assinados com esse certificado falhará.</span><span class="sxs-lookup"><span data-stu-id="df321-137">Once a certificate is removed, new packages signed with that certificate will fail at submission.</span></span> <span data-ttu-id="df321-138">Os pacotes existentes não serão afetados.</span><span class="sxs-lookup"><span data-stu-id="df321-138">Existing packages aren't affected.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="df321-139">Publicar o pacote</span><span class="sxs-lookup"><span data-stu-id="df321-139">Publish the package</span></span>

<span data-ttu-id="df321-140">Agora você está pronto para publicar o pacote em NuGet.org. Veja [Publicando pacotes](../nuget-org/Publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="df321-140">You are now ready to publish the package to NuGet.org. See [Publishing packages](../nuget-org/Publish-a-package.md).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="df321-141">Criar um certificado de teste</span><span class="sxs-lookup"><span data-stu-id="df321-141">Create a test certificate</span></span>

<span data-ttu-id="df321-142">Você pode usar certificados emitidos por conta própria para fins de teste.</span><span class="sxs-lookup"><span data-stu-id="df321-142">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="df321-143">Para criar um certificado emitido por conta própria, use o [comando New-SelfSignedCertificate do PowerShell](/powershell/module/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="df321-143">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate).</span></span>

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

<span data-ttu-id="df321-144">Este comando cria um certificado de teste disponível no repositório de certificados pessoal do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="df321-144">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="df321-145">Você pode abrir o repositório de certificados executando `certmgr.msc` para ver o certificado recém-criado.</span><span class="sxs-lookup"><span data-stu-id="df321-145">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="df321-146">O NuGet.org não aceita pacotes assinados com certificados emitidos por conta própria.</span><span class="sxs-lookup"><span data-stu-id="df321-146">NuGet.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a><span data-ttu-id="df321-147">Gerenciar os requisitos de assinatura do seu pacote em NuGet.org</span><span class="sxs-lookup"><span data-stu-id="df321-147">Manage signing requirements for your package on NuGet.org</span></span>
1. <span data-ttu-id="df321-148">[Entre](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) em NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="df321-148">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>

1. <span data-ttu-id="df321-149">Vá para `Manage Packages` 
   ![Configurar signatários do pacote](../reference/media/configure-package-signers.png)</span><span class="sxs-lookup"><span data-stu-id="df321-149">Go to `Manage Packages` 
![Configure package signers](../reference/media/configure-package-signers.png)</span></span>

* <span data-ttu-id="df321-150">Se for o único proprietário de um pacote, você será o signatário necessário, ou seja, poderá usar qualquer um dos certificados registrados para assinar e publicar seus pacotes em NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="df321-150">If you are the sole owner of a package, you are the required signer i.e. you can use any of the registered certificates to sign and publish your packages to NuGet.org.</span></span>

* <span data-ttu-id="df321-151">Se um pacote tem vários proprietários, por padrão, os certificados do proprietário "Qualquer" podem ser usados para assinar o pacote.</span><span class="sxs-lookup"><span data-stu-id="df321-151">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="df321-152">Como um coproprietário do pacote, você pode substituir "Qualquer" consigo mesmo ou com qualquer outro coproprietário para ser o signatário necessário.</span><span class="sxs-lookup"><span data-stu-id="df321-152">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="df321-153">Se você criar um proprietário que não tiver nenhum certificado registrado, os pacotes não assinados serão permitidos.</span><span class="sxs-lookup"><span data-stu-id="df321-153">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

* <span data-ttu-id="df321-154">Da mesma forma, se a opção "Qualquer" estiver selecionada para um pacote em que um proprietário tenha um certificado registrado e o outro proprietário não tenha nenhum certificado registrado, o NuGet.org aceitará um pacote assinado com uma assinatura registrada por um de seus proprietários ou então aceitará um pacote não assinado (porque um dos proprietários não tem nenhum certificado registrado).</span><span class="sxs-lookup"><span data-stu-id="df321-154">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then NuGet.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

## <a name="related-articles"></a><span data-ttu-id="df321-155">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="df321-155">Related articles</span></span>

- [<span data-ttu-id="df321-156">Gerenciar os limites de confiança do pacote</span><span class="sxs-lookup"><span data-stu-id="df321-156">Manage package trust boundaries</span></span>](../consume-packages/installing-signed-packages.md)
- [<span data-ttu-id="df321-157">Referência de pacotes assinados</span><span class="sxs-lookup"><span data-stu-id="df321-157">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
