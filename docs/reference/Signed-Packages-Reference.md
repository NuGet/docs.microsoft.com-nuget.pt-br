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
# <a name="signed-packages"></a>Pacotes assinados

*NuGet 4.6.0+ e Visual Studio 2017 versão 15.6 e posterior*

Pacotes do NuGet podem incluir uma assinatura digital que fornece proteção contra conteúdo violada. Esta assinatura é gerada de um certificado x. 509 que também adiciona provas autenticidade à origem do pacote real.

Pacotes assinados fornecem a validação de ponta a ponta mais forte. Uma assinatura de autor garante que o pacote não foi modificado desde que o autor entrada o pacote, não importa qual repositório ou o que o pacote é entregue de método de transporte.

Além disso, os pacotes assinados pelo autor fornecem um mecanismo de autenticação extra para o pipeline de publicação nuget.org porque o certificado de autenticação deve ser registrado antes do tempo. Para obter mais informações, consulte [registrar certificados](#register-certificate-on-nugetorg).

Para obter detalhes sobre como criar um pacote assinado, consulte [assinatura pacotes](../create-packages/Sign-a-package.md) e [comando de entrada do nuget](../tools/cli-ref-sign.md).

> [!Important]
> Atualmente há suporte para a assinatura do pacote somente quando usar nuget.exe no Windows. Verificação de pacotes assinados é suportada atualmente apenas ao usar o nuget.exe ou o Visual Studio no Windows.

## <a name="certificate-requirements"></a>Requisitos de certificado

Assinatura do pacote requer um código de assinatura de certificado, que é um tipo especial de certificado é válido para o `id-kp-codeSigning` finalidade [[RFC 5280 seção 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Além disso, o certificado deve ter um público comprimento da chave RSA de 2048 bits ou superior.

## <a name="get-a-code-signing-certificate"></a>Obter um certificado de assinatura de código

Certificados válidos podem ser obtidos em uma autoridade de certificação pública, como:

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [Entrada global](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

A lista completa de autoridades de certificação confiada pelo Windows pode ser obtida [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).

## <a name="create-a-test-certificate"></a>Criar um certificado de teste

Você pode usar certificados emitidos por conta própria para fins de teste. Para criar um certificado emitido por conta própria, use o [comando do PowerShell New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate.md).

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

Este comando cria um certificado de teste disponível no repositório de certificados pessoais do usuário atual. Você pode abrir o repositório de certificados executando `certmgr.msc` para ver o certificado recém-criado.

> [!Warning]
> NuGet.org não aceita pacotes assinados com certificados emitidos por conta própria.

## <a name="timestamp-requirements"></a>Requisitos de carimbo de hora

Pacotes assinados devem incluir um carimbo de hora do RFC 3161 para garantir a validade da assinatura além do período de validade do certificado de assinatura de pacote. O certificado usado para assinar o carimbo de hora deve ser válido para o `id-kp-timeStamping` finalidade [[RFC 5280 seção 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Além disso, o certificado deve ter um público comprimento da chave RSA de 2048 bits ou superior.

Detalhes técnicos adicionais podem ser encontrados no [especificações técnicas de assinatura do pacote](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Requisitos de assinatura em nuget.org

NuGet.org tem requisitos adicionais para aceitar um pacote assinado:

- A assinatura principal deve ser uma assinatura do autor.
- A assinatura principal deve ter um único carimbo válido.
- Os certificados x. 509 para a assinatura do autor e sua assinatura de carimbo de hora:
  - Deve ter uma chave pública RSA de 2048 bits ou superior.
  - Deve estar dentro do período de validade por hora UTC atual em tempo de validação de pacote em nuget.org.
  - Devem se encadear a uma autoridade raiz confiável que é confiável por padrão no Windows. Pacotes assinados com certificados emitidos por conta própria são rejeitados.
  - Deve ser válido para sua finalidade: 
    - O autor do certificado de assinatura deve ser válido para assinatura de código.
    - O certificado de carimbo de hora deve ser válido para o carimbo de hora.
  - Não deve ser revogado a hora da assinatura. (Isso poderá não ser knowable no momento do envio, portanto nuget.org verifica o status de revogação periodicamente novamente).

## <a name="register-certificate-on-nugetorg"></a>Registrar certificado em nuget.org

Para enviar um pacote assinado, você deve primeiro registrar o certificado com nuget.org. É necessário o certificado como um `.cer` arquivo em formato binário DER. Você pode exportar um certificado existente para um formato DER binário usando o Assistente para exportação de certificados.

![Assistente para exportação de certificados](media/CertificateExportWizard.png)

Usuários avançados podem exportar o certificado usando o [comando do PowerShell do certificado de exportação](/powershell/module/pkiclient/export-certificate.md).

Para registrar o certificado com nuget.org, vá para `Certificates` seção `Account settings` página (ou a página de configurações da organização) e selecione `Register new certificate`.

![Certificados registrados](media/registered-certs.png)

> [!Tip]
> Um usuário pode enviar que vários certificados e o mesmo certificado podem ser registrados por vários usuários.

Depois que um usuário tem um certificado registrado, todos os envios de pacote futuras **deve** ser assinado com um dos certificados.

Os usuários também podem remover um certificado registrado da conta. Depois que um certificado é removido, pacotes assinados com esse certificado falham no envio. Os pacotes existentes não serão afetados.

## <a name="configure-package-signing-requirements"></a>Configurar requisitos de assinatura de pacote

Se você for o único proprietário de um pacote, você é o signatário necessário. Ou seja, você pode usar qualquer um dos certificados registrados para assinar seus pacotes e enviá-las a nuget.org.

Se um pacote tem vários proprietários, por padrão, os certificados de "Qualquer" do proprietário podem ser usados para assinar o pacote. Como coproprietário do pacote, você pode substituir "Qualquer" com o mesmo ou outro proprietário colegas para ser o signatário necessário. Se você fizer um proprietário que não tem nenhum certificado registrado, serão permitidos pacotes não assinados. 

Da mesma forma, se o padrão "Qualquer" opção está selecionada para um pacote em que um proprietário tem um certificado registrado e outro proprietário não tiver nenhum certificado registrado, então nuget.org aceita ou um pacote assinado com uma assinatura registrada por um de seus proprietários ou sem uma assinatura do pacote (porque um dos proprietários não tem nenhum certificado registrado).

![Configurar signatários de pacote](media/configure-package-signers.png)
