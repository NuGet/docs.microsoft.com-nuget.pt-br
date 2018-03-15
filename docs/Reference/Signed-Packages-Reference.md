---
title: "Assinado pacotes referência | Microsoft Docs"
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Descrição do recurso de pacotes de entrada."
keywords: Entrada de pacote do NuGet, assinatura de certificado
ms.reviewer:
- ananguar
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9bf9885aaf42bedb681a5d916202fa8b26749a0c
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/15/2018
---
# <a name="signed-packages"></a>Pacotes assinados

*NuGet 4.6.0+ e Visual Studio 2017 versão 15.6 e posterior*

Pacotes do NuGet podem incluir uma assinatura digital que fornece proteção contra conteúdo violada. Esta assinatura é gerada de um certificado x. 509 que também adiciona provas autenticidade à origem do pacote real.

Pacotes assinados fornecem a validação de ponta a ponta mais forte. Uma assinatura de autor garante que o pacote não foi modificado desde que o autor entrada o pacote, não importa qual repositório ou o que o pacote é entregue de método de transporte.

Os consumidores que exigem um ambiente de bloqueio podem exigir pacotes assinados com um certificado de autor específico.

Além disso, os pacotes assinados pelo autor fornecem um mecanismo de autenticação extra para o pipeline de publicação nuget.org porque o certificado de autenticação deve ser registrado antes do tempo.

Para obter detalhes sobre como criar um pacote assinado, consulte [assinatura pacotes](../create-packages/Sign-a-package.md) e [comando de entrada do nuget](../tools/cli-ref-sign.md).

> [!Important]
> Atualmente, o NuGet.org não aceita pacotes assinados. Você pode assinar pacotes para publicar feeds personalizados.

## <a name="certificate-requirements"></a>Requisitos de certificado

Assinatura do pacote requer um código de assinatura de certificado, que é um tipo especial de certificado é válido para o `id-kp-codeSigning` finalidade [[RFC 5280 seção 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Além disso, o certificado deve ter um público comprimento da chave RSA de 2048 bits ou superior.

## <a name="get-a-code-signing-certificate"></a>Obter um certificado de assinatura de código

Certificados válidos podem ser obtidos em autoridades de certificação pública como:

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [Entrada global](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

A lista completa de autoridades de certificação confiada pelo Windows pode ser obtida [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).

## <a name="create-a-test-certificate"></a>Criar um certificado de teste

Você pode usar certificados emitidos por conta própria para fins de teste. Para criar um certificado emitido por conta própria, use o [New-SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) comando do PowerShell.

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

## <a name="timestamp-requirements"></a>Requisitos de carimbo de hora

Pacotes assinados devem incluir um carimbo de hora do RFC 3161 para garantir a validade da assinatura além do período de validade do certificado de assinatura de pacote. O certificado usado para assinar o carimbo de hora deve ser válido para o `id-kp-timeStamping` finalidade [[RFC 5280 seção 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Além disso, o certificado deve ter um público comprimento da chave RSA de 2048 bits ou superior.

Detalhes técnicos adicionais podem ser encontrados no [especificações técnicas de assinatura do pacote](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).
