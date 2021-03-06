---
title: Pacotes assinados
description: Requisitos para a assinatura do pacote NuGet.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 85fdf7a41cc033d92bbd0326648142aec27a9970
ms.sourcegitcommit: 1462f9f42ae36b3c990762ad4f02e38ab799ad09
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2021
ms.locfileid: "107508794"
---
# <a name="signed-packages"></a>Pacotes assinados

*NuGet 4.6.0 + e Visual Studio 2017 versão 15,6 e posterior*

Os pacotes NuGet podem incluir uma assinatura digital que fornece proteção contra conteúdo adulterado. Essa assinatura é produzida de um certificado X. 509 que também adiciona provas de autenticidade à origem real do pacote.

Os pacotes assinados fornecem a validação de ponta a ponta mais forte. Há dois tipos diferentes de assinaturas do NuGet:
- **Assinatura de autor**. Uma assinatura de autor garante que o pacote não foi modificado desde que o autor assinou o pacote, independentemente de qual repositório ou qual método de transporte o pacote é entregue. Além disso, os pacotes assinados por autor fornecem um mecanismo de autenticação extra para o pipeline de publicação nuget.org porque o certificado de autenticação deve ser registrado antecipadamente. Para obter mais informações, consulte [registrar certificados](#signature-requirements-on-nugetorg).
- **Assinatura do repositório**. As assinaturas de repositório fornecem uma garantia de integridade para **todos os** pacotes em um repositório, independentemente de serem autor ou não assinados, mesmo que esses pacotes sejam obtidos de um local diferente do repositório original em que foram assinados.   

Para obter detalhes sobre como criar um pacote assinado por autor, consulte [pacotes de assinatura](../create-packages/Sign-a-package.md) e o comando de [sinal do NuGet](../reference/cli-reference/cli-ref-sign.md). Você pode verificar as assinaturas de pacotes usando os comandos [dotnet NuGet Verify](/dotnet/core/tools/dotnet-nuget-verify) ou [NuGet Verify](../reference/cli-reference/cli-ref-verify.md) .

> [!Important]
> Os pacotes de assinatura de autor só têm suporte do nuget.exe no Windows no momento. No entanto, todos os pacotes carregados em nuget.org são assinados automaticamente pelo repositório.

## <a name="certificate-requirements"></a>Requisitos de certificado

A assinatura de pacote requer um certificado de assinatura de código, que é um tipo especial de certificado válido para a `id-kp-codeSigning` finalidade [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Além disso, o certificado deve ter um comprimento de chave pública RSA de 2048 bits ou mais.

## <a name="timestamp-requirements"></a>Requisitos de carimbo de hora

Os pacotes assinados devem incluir um carimbo de data/hora RFC 3161 para garantir a validade da assinatura além do período de validade do certificado de assinatura do pacote. O certificado usado para assinar o carimbo de data/hora deve ser válido para a `id-kp-timeStamping` finalidade [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Além disso, o certificado deve ter um comprimento de chave pública RSA de 2048 bits ou mais.

Detalhes técnicos adicionais podem ser encontrados no GitHub ( [especificações técnicas](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) ) de assinatura do pacote.

## <a name="signature-requirements-on-nugetorg"></a>Requisitos de assinatura no NuGet.org

o nuget.org tem requisitos adicionais para aceitar um pacote assinado:

- A assinatura principal deve ser uma assinatura de autor.
- A assinatura principal deve ter um único carimbo de data/hora válido.
- Os certificados X. 509 para a assinatura de autor e sua assinatura de carimbo de data/hora:
  - Deve ter uma chave pública RSA de 2048 bits ou superior.
  - Deve estar dentro de seu período de validade por hora UTC atual no momento da validação do pacote em nuget.org.
  - Deve se encadear a uma autoridade raiz confiável que é confiável por padrão no Windows. Pacotes assinados com certificados emitidos por conta própria são rejeitados.
  - Deve ser válido para sua finalidade: 
    - O certificado de assinatura de autor deve ser válido para assinatura de código.
    - O certificado de carimbo de data/hora deve ser válido para carimbo de data/hora.
  - Não deve ser revogado no momento da assinatura. (Isso pode não ser knowable no momento do envio, portanto, o nuget.org periodicamente verifica novamente o status de revogação).
  
  
## <a name="related-articles"></a>Artigos relacionados

- [Assinando pacotes NuGet](../create-packages/Sign-a-Package.md)
- [Verificar pacotes assinados usando a CLI do dotnet](/dotnet/core/tools/dotnet-nuget-verify)
- [Verificar pacotes assinados usando o nuget.exe](../reference/cli-reference/cli-ref-verify.md)
- [Gerenciar os limites de confiança do pacote](../consume-packages/installing-signed-packages.md)
