---
title: Pacotes assinados
description: Requisitos de assinatura de pacote do NuGet.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 952256a24246543ecd4c37285cd001622aa2bc46
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426170"
---
# <a name="signed-packages"></a>Pacotes assinados

*4.6.0+ do NuGet e o Visual Studio 2017 versão 15.6 e posterior*

Pacotes do NuGet podem incluir uma assinatura digital que fornece proteção contra conteúdo violado. Essa assinatura é produzida a partir de um certificado X.509 que também adiciona provas de autenticidade à origem do pacote real.

Os pacotes assinados fornecem a validação de ponta a ponta mais forte. Há dois tipos diferentes de assinaturas do NuGet:
- **Criar assinatura**. Uma assinatura do autor garante que o pacote não foi modificado desde que o autor assinou o pacote, não importa de que o repositório ou o que o pacote é entregue de método de transporte. Além disso, pacotes assinados pelo autor fornecem um mecanismo de autenticação extra para o pipeline de publicação do nuget.org, porque o certificado de autenticação deve ser registrado antes do tempo. Para obter mais informações, consulte [registrar certificados](#signature-requirements-on-nugetorg).
- **Assinatura do repositório**. Assinaturas de repositório fornecem uma garantia de integridade para **todos os** pacotes em um repositório, independentemente de estarem autor assinada ou não, mesmo que esses pacotes sejam obtidos de um local diferente do repositório original em que estavam assinado.   

Para obter detalhes sobre como criar um pacote assinado do autor, consulte [assinatura de pacotes](../create-packages/Sign-a-package.md) e o [comando nuget a entrada](../tools/cli-ref-sign.md).

> [!Important]
> Atualmente, há suporte para a assinatura do pacote somente ao usar nuget.exe no Windows. Verificação de pacotes assinados tem suporte atualmente somente ao usar nuget.exe ou o Visual Studio no Windows.

## <a name="certificate-requirements"></a>Requisitos de certificado

Assinatura do pacote requer um código de assinatura de certificado, que é um tipo especial de certificado é válido para o `id-kp-codeSigning` finalidade [[RFC 5280 seção 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Além disso, o certificado deve ter um público comprimento da chave RSA de 2048 bits ou superior.

## <a name="timestamp-requirements"></a>Requisitos de carimbo de hora

Pacotes assinados devem incluir um carimbo de hora RFC 3161 para garantir a validade da assinatura além do período de validade do certificado de assinatura de pacote. O certificado usado para assinar o carimbo de hora deve ser válido para o `id-kp-timeStamping` finalidade [[RFC 5280 seção 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Além disso, o certificado deve ter um público comprimento da chave RSA de 2048 bits ou superior.

Detalhes técnicos adicionais podem ser encontrados na [especificações técnicas de assinatura de pacote](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Requisitos de assinatura em NuGet.org

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
  
  
## <a name="related-articles"></a>Artigos relacionados

- [Assinando pacotes NuGet](../create-packages/Sign-a-Package.md)
- [Gerenciar limites de confiança do pacote](../consume-packages/installing-signed-packages.md)
