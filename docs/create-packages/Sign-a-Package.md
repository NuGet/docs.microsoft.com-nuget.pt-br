---
title: Assinando pacotes NuGet
description: Explica como os pacotes assinados podem ser usados para habilitar a verificação de integridade de conteúdo.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: a469cbdd218a0e9c18950bb0d36faf4dbcb42a01
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="bec7a-103">Assinando pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="bec7a-103">Signing NuGet Packages</span></span>

<span data-ttu-id="bec7a-104">A assinatura de um pacote é um processo que verifica se o pacote não foi modificado depois de ser criado.</span><span class="sxs-lookup"><span data-stu-id="bec7a-104">Signing a package is a process that makes sure the package has not been modified since its creation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bec7a-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bec7a-105">Prerequisites</span></span>

1. <span data-ttu-id="bec7a-106">O pacote (um arquivo `.nupkg`) a ser assinado.</span><span class="sxs-lookup"><span data-stu-id="bec7a-106">The package (a `.nupkg` file) to sign.</span></span> <span data-ttu-id="bec7a-107">Veja [Criando um pacote](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="bec7a-107">See [Creating a package](creating-a-package.md).</span></span>

1. <span data-ttu-id="bec7a-108">nuget.exe 4.6.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="bec7a-108">nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="bec7a-109">Veja como [Instalar a CLI do NuGet](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="bec7a-109">See how to [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span>

1. <span data-ttu-id="bec7a-110">[Um certificado de autenticação de código](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span><span class="sxs-lookup"><span data-stu-id="bec7a-110">[A code signing certificate](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span></span>

> [!Warning]
> <span data-ttu-id="bec7a-111">No momento, o nuget.org não aceita pacotes assinados.</span><span class="sxs-lookup"><span data-stu-id="bec7a-111">nuget.org does not currently accept signed packages.</span></span> <span data-ttu-id="bec7a-112">Você pode assinar pacotes para publicá-los em feeds personalizados.</span><span class="sxs-lookup"><span data-stu-id="bec7a-112">You can sign packages for publishing to custom feeds.</span></span>

## <a name="sign-a-package"></a><span data-ttu-id="bec7a-113">Assinar um pacote</span><span class="sxs-lookup"><span data-stu-id="bec7a-113">Sign a package</span></span>

<span data-ttu-id="bec7a-114">Para assinar um pacote, use [nuget sign](../tools/cli-ref-sign.md):</span><span class="sxs-lookup"><span data-stu-id="bec7a-114">To sign a package, use [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

<span data-ttu-id="bec7a-115">Conforme descrito na referência do comando, você pode usar um certificado disponível no repositório de certificados ou usar um certificado de um arquivo.</span><span class="sxs-lookup"><span data-stu-id="bec7a-115">As described in the command reference, you can use a certificate available in the certificate store or use a certificate from a file.</span></span>

### <a name="common-problems-when-signing-a-package"></a><span data-ttu-id="bec7a-116">Problemas comuns ao assinar um pacote</span><span class="sxs-lookup"><span data-stu-id="bec7a-116">Common problems when signing a package</span></span>

- <span data-ttu-id="bec7a-117">O certificado é inválido para a assinatura de código.</span><span class="sxs-lookup"><span data-stu-id="bec7a-117">The certificate is not valid for code signing.</span></span> <span data-ttu-id="bec7a-118">Você precisa garantir que o certificado especificado tenha o uso avançado de chave apropriado (EKU 1.3.6.1.5.5.7.3.3).</span><span class="sxs-lookup"><span data-stu-id="bec7a-118">You must ensure the certificate specified has the appropriate extended key usage (EKU 1.3.6.1.5.5.7.3.3).</span></span>
- <span data-ttu-id="bec7a-119">O certificado não satisfaz aos requisitos básicos, como algoritmo de assinatura RSA SHA-256 ou chave pública de 2.048 bits ou superior.</span><span class="sxs-lookup"><span data-stu-id="bec7a-119">The certificate does not satisfy the basic requirements such as the RSA SHA-256 signature algorithm or a public key 2048 bits or greater.</span></span>
- <span data-ttu-id="bec7a-120">O certificado expirou ou foi revogado.</span><span class="sxs-lookup"><span data-stu-id="bec7a-120">The certificate has expired or has been revoked.</span></span>
- <span data-ttu-id="bec7a-121">O servidor de carimbo de data/hora não satisfaz aos requisitos de certificado.</span><span class="sxs-lookup"><span data-stu-id="bec7a-121">The timestamp server does not satisfy the certificate requirements.</span></span>

> [!Note]
> <span data-ttu-id="bec7a-122">Os pacotes assinados devem incluir um carimbo de data/hora para assegurar que a assinatura permaneça válida quando o certificado de autenticação expira.</span><span class="sxs-lookup"><span data-stu-id="bec7a-122">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="bec7a-123">A operação de assinatura produz um [aviso NU3002](../reference/Errors-and-Warnings.md#nu3002) ao assinar sem um carimbo de data/hora.</span><span class="sxs-lookup"><span data-stu-id="bec7a-123">The sign operation produce a [warning NU3002](../reference/Errors-and-Warnings.md#nu3002) when signing without a timestamp.</span></span>

## <a name="verify-a-signed-package"></a><span data-ttu-id="bec7a-124">Verificar um pacote assinado</span><span class="sxs-lookup"><span data-stu-id="bec7a-124">Verify a signed package</span></span>

<span data-ttu-id="bec7a-125">Use [nuget verify](../tools/cli-ref-verify.md) para ver os detalhes da assinatura de um determinado pacote:</span><span class="sxs-lookup"><span data-stu-id="bec7a-125">Use [nuget verify](../tools/cli-ref-verify.md) to see the signature details of a given package:</span></span>

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a><span data-ttu-id="bec7a-126">Instalar um pacote assinado</span><span class="sxs-lookup"><span data-stu-id="bec7a-126">Install a signed package</span></span>

<span data-ttu-id="bec7a-127">Os pacotes assinados não exigem nenhuma ação específica para serem instalados. No entanto, se o conteúdo tiver sido modificado depois da assinatura, a instalação será bloqueada e um [erro NU3008](../reference/Errors-and-Warnings.md#nu3008) será gerado.</span><span class="sxs-lookup"><span data-stu-id="bec7a-127">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation be blocked and produces a [error NU3008](../reference/Errors-and-Warnings.md#nu3008).</span></span>

> [!Warning]
> <span data-ttu-id="bec7a-128">Os pacotes assinados com certificados não confiáveis são considerados não assinados e instalados sem avisos ou erros, como qualquer outro pacote não assinado.</span><span class="sxs-lookup"><span data-stu-id="bec7a-128">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="see-also"></a><span data-ttu-id="bec7a-129">Consulte também</span><span class="sxs-lookup"><span data-stu-id="bec7a-129">See also</span></span>

[<span data-ttu-id="bec7a-130">Referência de pacotes assinados</span><span class="sxs-lookup"><span data-stu-id="bec7a-130">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
