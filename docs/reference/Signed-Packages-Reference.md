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
# <a name="signed-packages"></a>Pacotes assinados

*4.6.0+ do NuGet e o Visual Studio 2017 versão 15.6 e posterior*

Pacotes do NuGet podem incluir uma assinatura digital que fornece proteção contra conteúdo violado. Essa assinatura é produzida a partir de um certificado X.509 que também adiciona provas de autenticidade à origem do pacote real.

Os pacotes assinados fornecem a validação de ponta a ponta mais forte. Há dois tipos diferentes de assinaturas do NuGet:
- **Criar assinatura**. Uma assinatura do autor garante que o pacote não foi modificado desde que o autor assinou o pacote, não importa de que o repositório ou o que o pacote é entregue de método de transporte. Além disso, pacotes assinados pelo autor fornecem um mecanismo de autenticação extra para o pipeline de publicação do nuget.org, porque o certificado de autenticação deve ser registrado antes do tempo. Para obter mais informações, consulte [registrar certificados](#register-certificate-on-nugetorg).
- **Assinatura do repositório**. Assinaturas de repositório fornecem uma garantia de integridade para **todos os** pacotes em um repositório, independentemente de estarem autor assinada ou não, mesmo que esses pacotes sejam obtidos de um local diferente do repositório original em que estavam assinado.   

Para obter detalhes sobre como criar um pacote assinado do autor, consulte [assinatura de pacotes](../create-packages/Sign-a-package.md) e o [comando nuget a entrada](../tools/cli-ref-sign.md).

> [!Important]
> Atualmente, há suporte para a assinatura do pacote somente ao usar nuget.exe no Windows. Verificação de pacotes assinados tem suporte atualmente somente ao usar nuget.exe ou o Visual Studio no Windows.

## <a name="certificate-requirements"></a>Requisitos de certificado

Assinatura do pacote requer um código de assinatura de certificado, que é um tipo especial de certificado é válido para o `id-kp-codeSigning` finalidade [[RFC 5280 seção 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Além disso, o certificado deve ter um público comprimento da chave RSA de 2048 bits ou superior.

## <a name="get-a-code-signing-certificate"></a>Obtenha um certificado de assinatura de código

Certificados válidos podem ser obtidos de uma autoridade de certificação pública, como:

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [Entrada global](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

A lista completa de autoridades de certificação confiável para Windows pode ser obtida [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).

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

Pacotes assinados devem incluir um carimbo de hora RFC 3161 para garantir a validade da assinatura além do período de validade do certificado de assinatura de pacote. O certificado usado para assinar o carimbo de hora deve ser válido para o `id-kp-timeStamping` finalidade [[RFC 5280 seção 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Além disso, o certificado deve ter um público comprimento da chave RSA de 2048 bits ou superior.

Detalhes técnicos adicionais podem ser encontrados na [especificações técnicas de assinatura de pacote](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Requisitos de assinatura em nuget.org

NuGet.org tem requisitos adicionais para aceitar um pacote assinado:

- A assinatura principal deve ser uma assinatura do autor.
- A assinatura principal deve ter um único carimbo de hora válido.
- Os certificados x. 509 para a assinatura do autor e sua assinatura do carimbo de hora:
  - Deve ter uma chave pública do RSA de 2048 bits ou superior.
  - Deve estar dentro do período de validade por hora UTC atual em tempo de validação de pacote em nuget.org.
  - Devem estar vinculados a uma autoridade raiz confiável que é confiável por padrão no Windows. Pacotes assinados com certificados emitidos por conta própria serão rejeitados.
  - Deve ser válido para sua finalidade: 
    - O autor do certificado de autenticação deve ser válido para assinatura de código.
    - O certificado de carimbo de hora deve ser válido para o carimbo de hora.
  - Não deve ser revogado a hora da assinatura. (Isso pode não estar knowable no momento do envio, portanto, o nuget.org periodicamente verifica novamente o status de revogação).

## <a name="register-certificate-on-nugetorg"></a>Registrar o certificado em nuget.org

Para enviar um pacote assinado, você deve primeiro registrar o certificado com nuget.org. Você precisa do certificado como um `.cer` arquivo em um formato DER binário. Você pode exportar um certificado existente para um formato DER binário usando o Assistente para exportação de certificados.

![Assistente para exportação de certificados](media/CertificateExportWizard.png)

Os usuários avançados podem exportar o certificado usando o [comando do PowerShell do certificado de exportação](/powershell/module/pkiclient/export-certificate.md).

Para registrar o certificado em nuget.org, vá para `Certificates` seção `Account settings` página (ou página de configurações da organização) e selecione `Register new certificate`.

![Certificados registrados](media/registered-certs.png)

> [!Tip]
> Um usuário pode enviar que vários certificados e o mesmo certificado podem ser registrados por vários usuários.

Depois que um usuário tem um certificado registrado, todos os envios de futuras do pacote **deve** ser assinado com um dos certificados.

Os usuários também podem remover um certificado registrado da conta. Depois que um certificado é removido, pacotes assinados com esse certificado falharem no envio. Os pacotes existentes não serão afetados.

## <a name="configure-package-signing-requirements"></a>Configurar requisitos de assinatura de pacote

Se você for o único proprietário de um pacote, você é o signatário necessário. Ou seja, você pode usar qualquer um dos certificados registrados para assinar seus pacotes e enviar para o nuget.org.

Se um pacote tem vários proprietários, por padrão, os certificados de "Qualquer" do proprietário podem ser usados para assinar o pacote. Como um coproprietário do pacote, você pode substituir "Qualquer" com por conta própria ou qualquer outro coproprietário para ser o signatário necessário. Se você fizer um proprietário que não tem qualquer certificado registrado, serão permitidos pacotes não assinados. 

Da mesma forma, se o padrão "Qualquer" opção estiver selecionada para um pacote em que um proprietário tem um certificado registrado e o outro proprietário não tiver nenhum certificado registrado, em seguida, nuget.org aceita qualquer um pacote assinado com uma assinatura registrada por um de seus proprietários ou sem uma assinatura do pacote (porque um dos proprietários não tem qualquer certificado registrado).

![Configurar signatários de pacote](media/configure-package-signers.png)
