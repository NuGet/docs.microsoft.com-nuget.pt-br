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
# <a name="signing-nuget-packages"></a>Assinando pacotes NuGet

Os pacotes assinados permitem verificações de integridade do conteúdo que oferecem proteção contra violação de conteúdo. A assinatura do pacote também serve como a única fonte de verdade sobre a origem real do pacote e reforça a autenticidade do pacote para o consumidor. Este guia pressupõe que você já [criou um pacote](creating-a-package.md).

## <a name="get-a-code-signing-certificate"></a>Obter um certificado de assinatura de código

Certificados válidos podem ser obtidos de uma autoridade de certificação pública, como [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) etc. A lista completa de autoridades de certificação confiáveis para Windows pode ser obtida de [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).

Você pode usar certificados emitidos por conta própria para fins de teste. No entanto, os pacotes assinados com certificados emitidos por conta própria não são aceitos por NuGet.org. Saiba mais sobre a [criação de um certificado de teste](#create-a-test-certificate)

## <a name="export-the-certificate-file"></a>Exportar o arquivo do certificado

* Você pode exportar um certificado existente para um formato DER binário usando o Assistente de Exportação de Certificados.

  ![Assistente de Exportação de Certificados](../reference/media/CertificateExportWizard.png)

* Você também pode exportar o certificado usando o [comando Export-Certificate do PowerShell](/powershell/module/pkiclient/export-certificate.md).

## <a name="sign-the-package"></a>Assinar o pacote

> [!note]
> Requer o nuget.exe 4.6.0 ou posterior

Assinar o pacote usando [nuget sign](../tools/cli-ref-sign.md):

```cli
nuget sign MyPackage.nupkg -CertificateFilePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

* Você pode usar um certificado disponível no repositório de certificados ou usar um certificado de um arquivo. Consulte a CLI de referência para [nuget sign](../tools/cli-ref-sign.md).
* Os pacotes assinados devem incluir um carimbo de data/hora para assegurar que a assinatura permaneça válida quando o certificado de autenticação expira. Caso contrário, a operação de entrada produzirá um [aviso](../reference/errors-and-warnings/NU3002.md).
* Você pode usar [nuget verify](../tools/cli-ref-verify.md) para ver os detalhes da assinatura de um determinado pacote.

## <a name="register-the-certificate-on-nugetorg"></a>Registrar o certificado em NuGet.org

Para publicar um pacote assinado, você deverá primeiro registrar o certificado com NuGet.org. Você precisa do certificado como um arquivo `.cer` em um formato DER binário.

1. [Entre](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) em NuGet.org.
1. Vá para `Account settings` (ou `Manage Organization` **>** `Edit Organziation` se você gostaria de registrar o certificado com uma conta de organização).
1. Expanda a seção `Certificates` e selecione `Register new`.
1. Procure e selecione o arquivo de certificado que foi exportado anteriormente.
  ![Certificados registrados](../reference/media/registered-certs.png)

**Observação**
* Um usuário pode enviar vários certificados e o mesmo certificado pode ser registrado por vários usuários.
* Depois que um usuário tem um certificado registrado, todos os envios de pacote futuros **precisam** ser assinados com um dos certificados. Veja [Gerenciar os requisitos de assinatura do seu pacote em NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)
* Os usuários também podem remover um certificado registrado da conta. Depois que um certificado é removido, o envio de novos pacotes assinados com esse certificado falhará. Os pacotes existentes não serão afetados.

## <a name="publish-the-package"></a>Publicar o pacote

Agora você está pronto para publicar o pacote em NuGet.org. Veja [Publicando pacotes](Publish-a-package.md).

## <a name="create-a-test-certificate"></a>Criar um certificado de teste

Você pode usar certificados emitidos por conta própria para fins de teste. Para criar um certificado emitido por conta própria, use o [comando New-SelfSignedCertificate do PowerShell](/powershell/module/pkiclient/new-selfsignedcertificate.md).

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

Este comando cria um certificado de teste disponível no repositório de certificados pessoal do usuário atual. Você pode abrir o repositório de certificados executando `certmgr.msc` para ver o certificado recém-criado.

> [!Warning]
> O NuGet.org não aceita pacotes assinados com certificados emitidos por conta própria.

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a>Gerenciar os requisitos de assinatura do seu pacote em NuGet.org
1. [Entre](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) em NuGet.org.

1. Vá para `Manage Packages` 
   ![Configurar signatários do pacote](../reference/media/configure-package-signers.png)

* Se for o único proprietário de um pacote, você será o signatário necessário, ou seja, poderá usar qualquer um dos certificados registrados para assinar e publicar seus pacotes em NuGet.org.

* Se um pacote tem vários proprietários, por padrão, os certificados do proprietário "Qualquer" podem ser usados para assinar o pacote. Como um coproprietário do pacote, você pode substituir "Qualquer" consigo mesmo ou com qualquer outro coproprietário para ser o signatário necessário. Se você criar um proprietário que não tiver nenhum certificado registrado, os pacotes não assinados serão permitidos. 

* Da mesma forma, se a opção "Qualquer" estiver selecionada para um pacote em que um proprietário tenha um certificado registrado e o outro proprietário não tenha nenhum certificado registrado, o NuGet.org aceitará um pacote assinado com uma assinatura registrada por um de seus proprietários ou então aceitará um pacote não assinado (porque um dos proprietários não tem nenhum certificado registrado).

## <a name="related-articles"></a>Artigos relacionados

- [Instalando pacotes assinados](../consume-packages/installing-signed-packages.md)
- [Referência de pacotes assinados](../reference/Signed-Packages-Reference.md)
