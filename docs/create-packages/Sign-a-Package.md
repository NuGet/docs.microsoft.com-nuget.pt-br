---
title: Assinando pacotes NuGet
description: Explica como os pacotes assinados podem ser usados para habilitar a verificação de integridade de conteúdo.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: c598461831323ecfcc5da3877df71bd8d69557f6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551972"
---
# <a name="signing-nuget-packages"></a>Assinando pacotes NuGet

A assinatura de um pacote é um processo que verifica se o pacote não foi modificado depois de ser criado.

## <a name="prerequisites"></a>Pré-requisitos

1. O pacote (um arquivo `.nupkg`) a ser assinado. Veja [Criando um pacote](creating-a-package.md).

1. nuget.exe 4.6.0 ou posterior. Veja como [Instalar a CLI do NuGet](../install-nuget-client-tools.md#nugetexe-cli).

1. [Um certificado de autenticação de código](../reference/signed-packages-reference.md#get-a-code-signing-certificate).

## <a name="sign-a-package"></a>Assinar um pacote

Para assinar um pacote, use [nuget sign](../tools/cli-ref-sign.md):

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

Conforme descrito na referência do comando, você pode usar um certificado disponível no repositório de certificados ou usar um certificado de um arquivo.

### <a name="common-problems-when-signing-a-package"></a>Problemas comuns ao assinar um pacote

- O certificado é inválido para a assinatura de código. Você precisa garantir que o certificado especificado tenha o uso avançado de chave apropriado (EKU 1.3.6.1.5.5.7.3.3).
- O certificado não satisfaz aos requisitos básicos, como algoritmo de assinatura RSA SHA-256 ou chave pública de 2.048 bits ou superior.
- O certificado expirou ou foi revogado.
- O servidor de carimbo de data/hora não satisfaz aos requisitos de certificado.

> [!Note]
> Os pacotes assinados devem incluir um carimbo de data/hora para assegurar que a assinatura permaneça válida quando o certificado de autenticação expira. A operação de assinatura produz um [aviso NU3002](../reference/errors-and-warnings/NU3002.md) ao assinar sem um carimbo de data/hora.

## <a name="verify-a-signed-package"></a>Verificar um pacote assinado

Use [nuget verify](../tools/cli-ref-verify.md) para ver os detalhes da assinatura de um determinado pacote:

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a>Instalar um pacote assinado

Os pacotes assinados não exigem nenhuma ação específica para serem instalados. No entanto, se o conteúdo tiver sido modificado depois da assinatura, a instalação será bloqueada e um [erro NU3008](../reference/errors-and-warnings/NU3008.md) será gerado.

> [!Warning]
> Os pacotes assinados com certificados não confiáveis são considerados não assinados e instalados sem avisos ou erros, como qualquer outro pacote não assinado.

## <a name="see-also"></a>Consulte também

[Referência de pacotes assinados](../reference/Signed-Packages-Reference.md)
