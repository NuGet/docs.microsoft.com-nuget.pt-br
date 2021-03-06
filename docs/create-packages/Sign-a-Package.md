---
title: Assinando pacotes NuGet
description: Explica como os pacotes assinados podem ser usados para habilitar a verificação de integridade de conteúdo.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: c0622520a325000d5fcb8fb884cb509ee4b641f4
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901896"
---
# <a name="signing-nuget-packages"></a>Assinando pacotes NuGet

Os pacotes assinados permitem verificações de integridade do conteúdo que oferecem proteção contra violação de conteúdo. A assinatura do pacote também serve como a única fonte de verdade sobre a origem real do pacote e reforça a autenticidade do pacote para o consumidor. Este guia pressupõe que você já [criou um pacote](creating-a-package.md).

## <a name="get-a-code-signing-certificate"></a>Obter um certificado de assinatura de código

Certificados válidos podem ser obtidos de uma autoridade de certificação pública, como [DigiCert](https://www.digicert.com/code-signing/), [Sign global](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certal](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml)etc. A lista completa de autoridades de certificação confiável pelo Windows pode ser obtida do [http://aka.ms/trustcertpartners](/security/trusted-root/participants-list) .

Você pode usar certificados emitidos por conta própria para fins de teste. No entanto, os pacotes assinados usando certificados emitidos por conta própria não são aceitos pelo NuGet.org. Saiba mais sobre como [criar um certificado de teste](#create-a-test-certificate)

## <a name="export-the-certificate-file"></a>Exportar o arquivo do certificado

* Você pode exportar um certificado existente para um formato DER binário usando o Assistente de Exportação de Certificados.

  ![Assistente de Exportação de Certificados](../reference/media/CertificateExportWizard.png)

* Você também pode exportar o certificado usando o [comando Export-Certificate do PowerShell](/powershell/module/pkiclient/export-certificate).

## <a name="sign-the-package"></a>Assinar o pacote

> [!note]
> Requer nuget.exe 4.6.0 ou posterior. dotnet.exe suporte será lançado em breve- [#7939](https://github.com/NuGet/Home/issues/7939)

Assinar o pacote usando [nuget sign](../reference/cli-reference/cli-ref-sign.md):

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> Geralmente, o provedor de certificado também fornece uma URL de servidor de carimbo de data/hora que pode ser usada para o argumento opcional `Timestamper` mostrado acima. Consulte a documentação e/ou o suporte do seu provedor para essa URL de serviço.

* Você pode usar um certificado disponível no repositório de certificados ou usar um certificado de um arquivo. Consulte a CLI de referência para [nuget sign](../reference/cli-reference/cli-ref-sign.md).
* Os pacotes assinados devem incluir um carimbo de data/hora para assegurar que a assinatura permaneça válida quando o certificado de autenticação expira. Caso contrário, a operação de entrada produzirá um [aviso](../reference/errors-and-warnings/NU3002.md).
* Você pode usar [nuget verify](../reference/cli-reference/cli-ref-verify.md) para ver os detalhes da assinatura de um determinado pacote.

## <a name="register-the-certificate-on-nugetorg"></a>Registrar o certificado em NuGet.org

Para publicar um pacote assinado, você deve primeiro registrar o certificado com NuGet.org. Você precisa do certificado como um `.cer` arquivo em um formato der binário.

1. [Entre](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) em NuGet.org.
1. Vá para `Account settings` (ou `Manage Organization` **>** `Edit Organization` se você gostaria de registrar o certificado com uma conta de organização).
1. Expanda a seção `Certificates` e selecione `Register new`.
1. Procure e selecione o arquivo de certificado que foi exportado anteriormente.
  ![Certificados registrados](../reference/media/registered-certs.png)

**Observação**
* Um usuário pode enviar vários certificados e o mesmo certificado pode ser registrado por vários usuários.
* Depois que um usuário tem um certificado registrado, todos os envios de pacote futuros **precisam** ser assinados com um dos certificados. Veja [Gerenciar os requisitos de assinatura do seu pacote em NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)
* Os usuários também podem remover um certificado registrado da conta. Depois que um certificado é removido, o envio de novos pacotes assinados com esse certificado falhará. Os pacotes existentes não serão afetados.

## <a name="publish-the-package"></a>Publicar o pacote

Agora você está pronto para publicar o pacote no NuGet.org. Consulte [publicando pacotes](../nuget-org/Publish-a-package.md).

## <a name="create-a-test-certificate"></a>Criar um certificado de teste

Você pode usar certificados emitidos por conta própria para fins de teste. Para criar um certificado emitido por conta própria, use o [comando New-SelfSignedCertificate do PowerShell](/powershell/module/pkiclient/new-selfsignedcertificate).

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

- [Gerenciar os limites de confiança do pacote](../consume-packages/installing-signed-packages.md)
- [Referência de pacotes assinados](../reference/Signed-Packages-Reference.md)
