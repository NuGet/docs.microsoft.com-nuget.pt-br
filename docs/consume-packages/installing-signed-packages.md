---
title: Instalar um pacote assinado do NuGet
description: Descreve o processo de instalação de pacotes do NuGet assinados e de definição das configurações de confiança de assinatura de pacotes.
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 11ffaee96b6f6a9260f38c534328b6631cd96abf
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977830"
---
# <a name="install-a-signed-package"></a><span data-ttu-id="318bc-103">Instalar um pacote assinado</span><span class="sxs-lookup"><span data-stu-id="318bc-103">Install a signed package</span></span>

<span data-ttu-id="318bc-104">Os pacotes assinados não exigem nenhuma ação específica para serem instalados. No entanto, se o conteúdo tiver sido modificado depois da assinatura, a instalação será bloqueada com o erro [NU3008](../reference/errors-and-warnings/NU3008.md).</span><span class="sxs-lookup"><span data-stu-id="318bc-104">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked with error [NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="318bc-105">Os pacotes assinados com certificados não confiáveis são considerados não assinados e instalados sem avisos ou erros, como qualquer outro pacote não assinado.</span><span class="sxs-lookup"><span data-stu-id="318bc-105">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="configure-package-signature-requirements"></a><span data-ttu-id="318bc-106">Configurar os requisitos de assinatura do pacote</span><span class="sxs-lookup"><span data-stu-id="318bc-106">Configure package signature requirements</span></span>

> [!Note]
> <span data-ttu-id="318bc-107">Requer o NuGet 4.9.0+ e o Visual Studio versão 15.9 e posterior no Windows</span><span class="sxs-lookup"><span data-stu-id="318bc-107">Requires NuGet 4.9.0+ and Visual Studio version 15.9 and later on Windows</span></span>

<span data-ttu-id="318bc-108">Você pode configurar o modo como os clientes do NuGet validam assinaturas de pacote, definindo o `signatureValidationMode` para `require` no arquivo [nuget.config](../reference/nuget-config-file) usando o comando [`nuget config`](../tools/cli-ref-config).</span><span class="sxs-lookup"><span data-stu-id="318bc-108">You can configure how NuGet clients validate package signatures by setting the `signatureValidationMode` to `require` in the [nuget.config](../reference/nuget-config-file) file using the [`nuget config`](../tools/cli-ref-config) command.</span></span>

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

<span data-ttu-id="318bc-109">Esse modo vai verificar se todos os pacotes são assinados por qualquer um dos certificados confiáveis no arquivo `nuget.config`.</span><span class="sxs-lookup"><span data-stu-id="318bc-109">This mode will verify that all packages are signed by any of the certificates trusted in the `nuget.config` file.</span></span> <span data-ttu-id="318bc-110">Esse arquivo permite que você especifique quais autores e/ou repositórios são confiáveis, com base na impressão digital do certificado.</span><span class="sxs-lookup"><span data-stu-id="318bc-110">This file allows you to specify which authors and/or repositories are trusted based on the certificate's fingerprint.</span></span>

### <a name="trust-package-author"></a><span data-ttu-id="318bc-111">Confiar no autor do pacote</span><span class="sxs-lookup"><span data-stu-id="318bc-111">Trust package author</span></span>

<span data-ttu-id="318bc-112">Para confiar em pacotes com base na assinatura do autor, use o comando [`trusted-signers`](..tools/cli-ref-trusted-signers) para definir a propriedade `author` no nuget.config.</span><span class="sxs-lookup"><span data-stu-id="318bc-112">To trust packages based on the author signature use the [`trusted-signers`](..tools/cli-ref-trusted-signers) command to set the `author` property in the nuget.config.</span></span>

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
><span data-ttu-id="318bc-113">Use o [comando verify](https://docs.microsoft.com/en-us/nuget/tools/cli-ref-verify) `nuget.exe` para obter o valor `SHA256` da impressão digital do certificado.</span><span class="sxs-lookup"><span data-stu-id="318bc-113">Use the `nuget.exe` [verify command](https://docs.microsoft.com/en-us/nuget/tools/cli-ref-verify) to get the `SHA256` value of the certificate's fingerprint.</span></span>


### <a name="trust-all-packages-from-a-repository"></a><span data-ttu-id="318bc-114">Confiar em todos os pacotes de um repositório</span><span class="sxs-lookup"><span data-stu-id="318bc-114">Trust all packages from a repository</span></span>

<span data-ttu-id="318bc-115">Para confiar em pacotes com base na assinatura do repositório, use o elemento `repository`:</span><span class="sxs-lookup"><span data-stu-id="318bc-115">To trust packages based on the repository signature use the `repository` element:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a><span data-ttu-id="318bc-116">Confiar nos proprietários do pacote</span><span class="sxs-lookup"><span data-stu-id="318bc-116">Trust Package Owners</span></span>

<span data-ttu-id="318bc-117">Assinaturas de repositório incluem metadados adicionais para determinar os proprietários do pacote no momento do envio.</span><span class="sxs-lookup"><span data-stu-id="318bc-117">Repository signatures include additional metadata to determine the owners of the package at the time of submission.</span></span> <span data-ttu-id="318bc-118">Você pode restringir os pacotes de um repositório com base em uma lista de proprietários:</span><span class="sxs-lookup"><span data-stu-id="318bc-118">You can restrict packages from a repository based on a list of owners:</span></span>

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

<span data-ttu-id="318bc-119">Se um pacote tiver vários proprietários e qualquer um desses proprietários estiver na lista de confiáveis, a instalação do pacote será bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="318bc-119">If a package has multiple owners, and any one of those owners is in the trusted list, the package installation will succeed.</span></span>

### <a name="untrusted-root-certificates"></a><span data-ttu-id="318bc-120">Certificados raiz não confiáveis</span><span class="sxs-lookup"><span data-stu-id="318bc-120">Untrusted Root certificates</span></span>

<span data-ttu-id="318bc-121">Em algumas situações, convém habilitar a verificação usando certificados não encadeados a uma raiz confiável no computador local.</span><span class="sxs-lookup"><span data-stu-id="318bc-121">In some situations you may want to enable verification using certificates that do not chain to a trusted root in the local machine.</span></span> <span data-ttu-id="318bc-122">Você pode usar o atributo `allowUntrustedRoot` para personalizar esse comportamento.</span><span class="sxs-lookup"><span data-stu-id="318bc-122">You can use the `allowUntrustedRoot` attribute to customize this behavior.</span></span>

### <a name="sync-repository-certificates"></a><span data-ttu-id="318bc-123">Sincronizar certificados do repositório</span><span class="sxs-lookup"><span data-stu-id="318bc-123">Sync repository certificates</span></span>

<span data-ttu-id="318bc-124">Os repositórios de pacote devem anunciar os certificados que eles usam em seu [índice de serviço](https://docs.microsoft.com/en-us/nuget/api/service-index).</span><span class="sxs-lookup"><span data-stu-id="318bc-124">Package repositories should announce the certificates they use in their [service index](https://docs.microsoft.com/en-us/nuget/api/service-index).</span></span> <span data-ttu-id="318bc-125">Eventualmente, o repositório atualizará esses certificados, por exemplo, quando o certificado expirar.</span><span class="sxs-lookup"><span data-stu-id="318bc-125">Eventually the repository will update these certificates, e.g. when the certificate expires.</span></span> <span data-ttu-id="318bc-126">Quando isso acontecer, os clientes com políticas específicas exigirão uma atualização à configuração a fim de incluir o certificado recém-adicionado.</span><span class="sxs-lookup"><span data-stu-id="318bc-126">When that happens, clients with specific policies will require an update to the configuration to include the newly added certificate.</span></span> <span data-ttu-id="318bc-127">Você pode atualizar facilmente os signatários confiáveis associados a um repositório usando o [comando trusted-signers sync](/nuget/tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-) `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="318bc-127">You can easily upgrade the trusted signers associated to a repository by using the `nuget.exe` [trusted-signers sync command](/nuget/tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-).</span></span>

### <a name="schema-reference"></a><span data-ttu-id="318bc-128">Referência de esquema</span><span class="sxs-lookup"><span data-stu-id="318bc-128">Schema reference</span></span>

<span data-ttu-id="318bc-129">A referência de esquema completa para as políticas do cliente pode ser encontrada na [referência do nuget.config](/nuget/reference/nuget-config-file#trustedsigners-section)</span><span class="sxs-lookup"><span data-stu-id="318bc-129">The complete schema reference for the client policies can be found in the [nuget.config reference](/nuget/reference/nuget-config-file#trustedsigners-section)</span></span>

## <a name="related-articles"></a><span data-ttu-id="318bc-130">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="318bc-130">Related articles</span></span>

- [<span data-ttu-id="318bc-131">Maneiras diferentes de instalar um pacote NuGet</span><span class="sxs-lookup"><span data-stu-id="318bc-131">Different ways to install a NuGet Package</span></span>](ways-to-install-a-package.md)
- [<span data-ttu-id="318bc-132">Assinando pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="318bc-132">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="318bc-133">Referência de pacotes assinados</span><span class="sxs-lookup"><span data-stu-id="318bc-133">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
