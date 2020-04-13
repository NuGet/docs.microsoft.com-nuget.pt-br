---
title: Gerenciar os limites de confiança do pacote
description: Descreve o processo de instalação de pacotes do NuGet assinados e de definição das configurações de confiança de assinatura de pacotes.
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 034b9dd9699af529e4d82d6ee5b1c42214673341
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428978"
---
# <a name="manage-package-trust-boundaries"></a>Gerenciar os limites de confiança do pacote

Os pacotes assinados não exigem nenhuma ação específica para serem instalados. No entanto, se o conteúdo tiver sido modificado depois da assinatura, a instalação será bloqueada com o erro [NU3008](../reference/errors-and-warnings/NU3008.md).

> [!Warning]
> Os pacotes assinados com certificados não confiáveis são considerados não assinados e instalados sem avisos ou erros, como qualquer outro pacote não assinado.

## <a name="configure-package-signature-requirements"></a>Configurar os requisitos de assinatura do pacote

> [!Note]
> Requer o NuGet 4.9.0+ e o Visual Studio versão 15.9 e posterior no Windows

Você pode configurar o modo como os clientes do NuGet validam assinaturas de pacote, definindo o `signatureValidationMode` para `require` no arquivo [nuget.config](../reference/nuget-config-file.md) usando o comando [`nuget config`](../reference/cli-reference/cli-ref-config.md).

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

Esse modo vai verificar se todos os pacotes são assinados por qualquer um dos certificados confiáveis no arquivo `nuget.config`. Esse arquivo permite que você especifique quais autores e/ou repositórios são confiáveis, com base na impressão digital do certificado.

### <a name="trust-package-author"></a>Confiar no autor do pacote

Para confiar em pacotes com [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) base na `author` assinatura do autor, use o comando para definir a propriedade no nuget.config.

```cmd
nuget.exe  trusted-signers Add -Name MyCompanyCert -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256
```

```xml
<trustedSigners>
  <author name="MyCompanyCert">
    <certificate fingerprint="CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
  </author>
</trustedSigners>
```

>[!TIP]
>Use o  [comando verify](../reference/cli-reference/cli-ref-verify.md)`nuget.exe` para obter o valor `SHA256` da impressão digital do certificado.


### <a name="trust-all-packages-from-a-repository"></a>Confiar em todos os pacotes de um repositório

Para confiar em pacotes com base na assinatura do repositório, use o elemento `repository`:

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a>Confiar nos proprietários do pacote

Assinaturas de repositório incluem metadados adicionais para determinar os proprietários do pacote no momento do envio. Você pode restringir os pacotes de um repositório com base em uma lista de proprietários:

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
      <owners>microsoft;nuget</owners>
  </repository>
</trustedSigners>
```

Se um pacote tiver vários proprietários e qualquer um desses proprietários estiver na lista de confiáveis, a instalação do pacote será bem-sucedida.

### <a name="untrusted-root-certificates"></a>Certificados raiz não confiáveis

Em algumas situações, convém habilitar a verificação usando certificados não encadeados a uma raiz confiável no computador local. Você pode usar o atributo `allowUntrustedRoot` para personalizar esse comportamento.

### <a name="sync-repository-certificates"></a>Sincronizar certificados do repositório

Os repositórios de pacote devem anunciar os certificados que eles usam em seu [índice de serviço](../api/service-index.md). Eventualmente, o repositório atualizará esses certificados, por exemplo, quando o certificado expirar. Quando isso acontecer, os clientes com políticas específicas exigirão uma atualização à configuração a fim de incluir o certificado recém-adicionado. Você pode atualizar facilmente os signatários confiáveis associados a um repositório usando o  [comando trusted-signers sync](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name)`nuget.exe`.

### <a name="schema-reference"></a>Referência de esquema

A referência de esquema completa para as políticas do cliente pode ser encontrada na [referência do nuget.config](../reference/nuget-config-file.md#trustedsigners-section)

## <a name="related-articles"></a>Artigos relacionados

- [Assinando pacotes NuGet](../create-packages/Sign-a-Package.md)
- [Referência de pacotes assinados](../reference/Signed-Packages-Reference.md)
