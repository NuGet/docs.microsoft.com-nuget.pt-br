---
title: nuget.config File Reference
description: Referência do arquivo NuGet.Config incluindo as seções config, bindingRedirects, packageRestore, solution e packageSource.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: 2eceb6e94a353cb29b83aea114c6cea2acbac266
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426153"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="d5603-103">referência do NuGet. config</span><span class="sxs-lookup"><span data-stu-id="d5603-103">nuget.config reference</span></span>

<span data-ttu-id="d5603-104">O comportamento do NuGet é controlado pelas configurações em diferentes `NuGet.Config` arquivos conforme descrito em [configurações de NuGet comuns](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="d5603-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="d5603-105">`nuget.config` é um arquivo XML que contém um nó `<configuration>` de nível superior, o qual contém os elementos da seção descritos neste tópico.</span><span class="sxs-lookup"><span data-stu-id="d5603-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="d5603-106">Cada seção contém zero ou mais itens.</span><span class="sxs-lookup"><span data-stu-id="d5603-106">Each section contains zero or more items.</span></span> <span data-ttu-id="d5603-107">Consulte o [arquivo de configuração de exemplos](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="d5603-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="d5603-108">Nomes de configuração não diferenciam maiúsculas de minúsculas e podem usar valores [variáveis de ambiente](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="d5603-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="d5603-109">Neste tópico:</span><span class="sxs-lookup"><span data-stu-id="d5603-109">In this topic:</span></span>

- [<span data-ttu-id="d5603-110">seção de configuração</span><span class="sxs-lookup"><span data-stu-id="d5603-110">config section</span></span>](#config-section)
- [<span data-ttu-id="d5603-111">Seção bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="d5603-111">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="d5603-112">Seção packageRestore</span><span class="sxs-lookup"><span data-stu-id="d5603-112">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="d5603-113">solution section</span><span class="sxs-lookup"><span data-stu-id="d5603-113">solution section</span></span>](#solution-section)
- <span data-ttu-id="d5603-114">[Seções de origem de pacote](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="d5603-114">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="d5603-115">packageSources</span><span class="sxs-lookup"><span data-stu-id="d5603-115">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="d5603-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="d5603-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="d5603-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="d5603-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="d5603-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="d5603-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="d5603-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="d5603-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="d5603-120">seção trustedSigners</span><span class="sxs-lookup"><span data-stu-id="d5603-120">trustedSigners section</span></span>](#trustedsigners-section)
- [<span data-ttu-id="d5603-121">Usando variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="d5603-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="d5603-122">Exemplo de arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="d5603-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="d5603-123">seção de configuração</span><span class="sxs-lookup"><span data-stu-id="d5603-123">config section</span></span>

<span data-ttu-id="d5603-124">Contém diversas definições de configurações, que podem ser definidas usando o comando [`nuget config`](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="d5603-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="d5603-125">`dependencyVersion` e `repositoryPath` se aplicam somente a projetos usando `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="d5603-125">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="d5603-126">`globalPackagesFolder` aplica-se somente a projetos usando o formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="d5603-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="d5603-127">Chave</span><span class="sxs-lookup"><span data-stu-id="d5603-127">Key</span></span> | <span data-ttu-id="d5603-128">Valor</span><span class="sxs-lookup"><span data-stu-id="d5603-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d5603-129">dependencyVersion (somente `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="d5603-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="d5603-130">O valor `DependencyVersion` padrão para a instalação, restauração e atualização do pacote, quando a opção `-DependencyVersion` não tiver sido especificada diretamente.</span><span class="sxs-lookup"><span data-stu-id="d5603-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="d5603-131">Esse valor também é usado pela interface do usuário do Gerenciador de Pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="d5603-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="d5603-132">Os valores são `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="d5603-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="d5603-133">globalPackagesFolder (projetos que usam PackageReference apenas)</span><span class="sxs-lookup"><span data-stu-id="d5603-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="d5603-134">O local da pasta de pacotes global padrão.</span><span class="sxs-lookup"><span data-stu-id="d5603-134">The location of the default global packages folder.</span></span> <span data-ttu-id="d5603-135">O padrão é `%userprofile%\.nuget\packages` (Windows) ou `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="d5603-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="d5603-136">Um caminho relativo pode ser usado em arquivos `nuget.config` específicos do projeto.</span><span class="sxs-lookup"><span data-stu-id="d5603-136">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="d5603-137">Essa configuração é substituída pela variável de ambiente NUGET_PACKAGES, que tem precedência.</span><span class="sxs-lookup"><span data-stu-id="d5603-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="d5603-138">repositoryPath (somente `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="d5603-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="d5603-139">O local no qual instalar os pacotes do NuGet em vez da pasta `$(Solutiondir)/packages` padrão.</span><span class="sxs-lookup"><span data-stu-id="d5603-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="d5603-140">Um caminho relativo pode ser usado em arquivos `nuget.config` específicos do projeto.</span><span class="sxs-lookup"><span data-stu-id="d5603-140">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="d5603-141">Essa configuração é substituída pela variável de ambiente NUGET_PACKAGES, que tem precedência.</span><span class="sxs-lookup"><span data-stu-id="d5603-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="d5603-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="d5603-142">defaultPushSource</span></span> | <span data-ttu-id="d5603-143">Identifica a URL ou o caminho da origem do pacote que deve ser usada como o padrão se nenhuma outra origem de pacote for encontrada para uma operação.</span><span class="sxs-lookup"><span data-stu-id="d5603-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="d5603-144">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="d5603-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="d5603-145">Configurações de proxy a serem usadas ao se conectar a origens de pacote; `http_proxy` deve estar no formato `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="d5603-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="d5603-146">As senhas são criptografadas e não podem ser adicionadas manualmente.</span><span class="sxs-lookup"><span data-stu-id="d5603-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="d5603-147">Para `no_proxy`, o valor é uma lista separada por vírgulas de domínios a ignorar no servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="d5603-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="d5603-148">Como alternativa, você pode usar as variáveis de ambiente http_proxy e no_proxy para esses valores.</span><span class="sxs-lookup"><span data-stu-id="d5603-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="d5603-149">Para ver detalhes adicionais, consulte [Configurações de proxy do NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="d5603-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="d5603-150">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="d5603-150">signatureValidationMode</span></span> | <span data-ttu-id="d5603-151">Especifica o modo de validação usado para verificar as assinaturas de pacote para instalação do pacote e restauração.</span><span class="sxs-lookup"><span data-stu-id="d5603-151">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="d5603-152">Os valores são `accept`, `require`.</span><span class="sxs-lookup"><span data-stu-id="d5603-152">Values are `accept`, `require`.</span></span> <span data-ttu-id="d5603-153">Assume o padrão de `accept`.</span><span class="sxs-lookup"><span data-stu-id="d5603-153">Defaults to `accept`.</span></span>

<span data-ttu-id="d5603-154">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="d5603-154">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="d5603-155">Seção bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="d5603-155">bindingRedirects section</span></span>

<span data-ttu-id="d5603-156">Configura se o NuGet realiza redirecionamentos de associação automática quando um pacote é instalado.</span><span class="sxs-lookup"><span data-stu-id="d5603-156">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="d5603-157">Chave</span><span class="sxs-lookup"><span data-stu-id="d5603-157">Key</span></span> | <span data-ttu-id="d5603-158">Valor</span><span class="sxs-lookup"><span data-stu-id="d5603-158">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d5603-159">skip</span><span class="sxs-lookup"><span data-stu-id="d5603-159">skip</span></span> | <span data-ttu-id="d5603-160">Um valor booliano que indica se os redirecionamentos de associação automática devem ser ignorados.</span><span class="sxs-lookup"><span data-stu-id="d5603-160">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="d5603-161">O padrão é falso.</span><span class="sxs-lookup"><span data-stu-id="d5603-161">The default is false.</span></span> |

<span data-ttu-id="d5603-162">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="d5603-162">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="d5603-163">Seção packageRestore</span><span class="sxs-lookup"><span data-stu-id="d5603-163">packageRestore section</span></span>

<span data-ttu-id="d5603-164">Controla a restauração de pacote durante builds.</span><span class="sxs-lookup"><span data-stu-id="d5603-164">Controls package restore during builds.</span></span>

| <span data-ttu-id="d5603-165">Chave</span><span class="sxs-lookup"><span data-stu-id="d5603-165">Key</span></span> | <span data-ttu-id="d5603-166">Valor</span><span class="sxs-lookup"><span data-stu-id="d5603-166">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d5603-167">habilitado</span><span class="sxs-lookup"><span data-stu-id="d5603-167">enabled</span></span> | <span data-ttu-id="d5603-168">Um valor booliano que indica se o NuGet pode executar uma restauração automática.</span><span class="sxs-lookup"><span data-stu-id="d5603-168">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="d5603-169">Você também pode definir a variável de ambiente `EnableNuGetPackageRestore` com um valor de `True` em vez de configurar essa chave no arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="d5603-169">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="d5603-170">automático</span><span class="sxs-lookup"><span data-stu-id="d5603-170">automatic</span></span> | <span data-ttu-id="d5603-171">Um valor booliano que indica se o NuGet deve verificar se há pacotes ausentes durante um build.</span><span class="sxs-lookup"><span data-stu-id="d5603-171">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="d5603-172">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="d5603-172">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="d5603-173">solution section</span><span class="sxs-lookup"><span data-stu-id="d5603-173">solution section</span></span>

<span data-ttu-id="d5603-174">Controla se a pasta `packages` de uma solução está incluída no controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="d5603-174">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="d5603-175">Esta seção funciona somente em arquivos `nuget.config` em uma pasta de solução.</span><span class="sxs-lookup"><span data-stu-id="d5603-175">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="d5603-176">Chave</span><span class="sxs-lookup"><span data-stu-id="d5603-176">Key</span></span> | <span data-ttu-id="d5603-177">Valor</span><span class="sxs-lookup"><span data-stu-id="d5603-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d5603-178">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="d5603-178">disableSourceControlIntegration</span></span> | <span data-ttu-id="d5603-179">Um booliano que indica se a pasta de pacotes deve ser ignorada ao trabalhar com o controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="d5603-179">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="d5603-180">O valor padrão é false.</span><span class="sxs-lookup"><span data-stu-id="d5603-180">The default value is false.</span></span> |

<span data-ttu-id="d5603-181">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="d5603-181">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="d5603-182">Seções de origem de pacote</span><span class="sxs-lookup"><span data-stu-id="d5603-182">Package source sections</span></span>

<span data-ttu-id="d5603-183">O `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` e `trustedSigners` trabalham todos juntos para configurar como o NuGet funciona com repositórios de pacote durante a instalação, restauração e operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="d5603-183">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="d5603-184">O [ `nuget sources` comando](../tools/cli-ref-sources.md) geralmente é usado para gerenciar essas configurações, exceto para `apikeys` que é gerenciado usando o [ `nuget setapikey` comando](../tools/cli-ref-setapikey.md), e `trustedSigners` que é gerenciado usando o [ `nuget trusted-signers` comando](../tools/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="d5603-184">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../tools/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="d5603-185">Observe que a URL de origem para nuget.org é `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="d5603-185">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="d5603-186">packageSources</span><span class="sxs-lookup"><span data-stu-id="d5603-186">packageSources</span></span>

<span data-ttu-id="d5603-187">Lista todas as origens de pacotes conhecidas.</span><span class="sxs-lookup"><span data-stu-id="d5603-187">Lists all known package sources.</span></span> <span data-ttu-id="d5603-188">A ordem é ignorada durante operações de restauração e com qualquer projeto usando o formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="d5603-188">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="d5603-189">NuGet respeita a ordem das fontes para instalar e atualizar operações com projetos usando `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="d5603-189">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="d5603-190">Chave</span><span class="sxs-lookup"><span data-stu-id="d5603-190">Key</span></span> | <span data-ttu-id="d5603-191">Valor</span><span class="sxs-lookup"><span data-stu-id="d5603-191">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d5603-192">(nome a ser atribuído à origem do pacote)</span><span class="sxs-lookup"><span data-stu-id="d5603-192">(name to assign to the package source)</span></span> | <span data-ttu-id="d5603-193">O caminho ou URL da origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="d5603-193">The path or URL of the package source.</span></span> |

<span data-ttu-id="d5603-194">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="d5603-194">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="d5603-195">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="d5603-195">packageSourceCredentials</span></span>

<span data-ttu-id="d5603-196">Armazena os nomes de usuário e senhas para as origens, geralmente especificado com as opções `-username` e `-password` com `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="d5603-196">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="d5603-197">As senhas são criptografadas por padrão, a menos que a opção `-storepasswordincleartext` também seja usada.</span><span class="sxs-lookup"><span data-stu-id="d5603-197">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="d5603-198">Chave</span><span class="sxs-lookup"><span data-stu-id="d5603-198">Key</span></span> | <span data-ttu-id="d5603-199">Valor</span><span class="sxs-lookup"><span data-stu-id="d5603-199">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d5603-200">username</span><span class="sxs-lookup"><span data-stu-id="d5603-200">username</span></span> | <span data-ttu-id="d5603-201">O nome de usuário para a origem em texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="d5603-201">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="d5603-202">password</span><span class="sxs-lookup"><span data-stu-id="d5603-202">password</span></span> | <span data-ttu-id="d5603-203">A senha criptografada para a origem.</span><span class="sxs-lookup"><span data-stu-id="d5603-203">The encrypted password for the source.</span></span> |
| <span data-ttu-id="d5603-204">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="d5603-204">cleartextpassword</span></span> | <span data-ttu-id="d5603-205">A senha não criptografada para a origem.</span><span class="sxs-lookup"><span data-stu-id="d5603-205">The unencrypted password for the source.</span></span> |

<span data-ttu-id="d5603-206">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="d5603-206">**Example:**</span></span>

<span data-ttu-id="d5603-207">No arquivo de configuração, o elemento `<packageSourceCredentials>` contém nós filho para cada nome de origem aplicável (espaços no nome serão substituídos por `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="d5603-207">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="d5603-208">Ou seja, para origens chamadas “Contoso” e “Origem de teste”, o arquivo de configuração contém o seguinte ao usar senhas criptografadas:</span><span class="sxs-lookup"><span data-stu-id="d5603-208">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="Password" value="..." />
    </Test_x0020_Source>
</packageSourceCredentials>
```

<span data-ttu-id="d5603-209">Ao usar senhas não criptografadas:</span><span class="sxs-lookup"><span data-stu-id="d5603-209">When using unencrypted passwords:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="33f!!lloppa" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a><span data-ttu-id="d5603-210">apikeys</span><span class="sxs-lookup"><span data-stu-id="d5603-210">apikeys</span></span>

<span data-ttu-id="d5603-211">Armazena as chaves de origens que usam autenticação de chave de API, conforme definido com o comando [`nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="d5603-211">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="d5603-212">Chave</span><span class="sxs-lookup"><span data-stu-id="d5603-212">Key</span></span> | <span data-ttu-id="d5603-213">Valor</span><span class="sxs-lookup"><span data-stu-id="d5603-213">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d5603-214">(URL de origem)</span><span class="sxs-lookup"><span data-stu-id="d5603-214">(source URL)</span></span> | <span data-ttu-id="d5603-215">A chave de API criptografada.</span><span class="sxs-lookup"><span data-stu-id="d5603-215">The encrypted API key.</span></span> |

<span data-ttu-id="d5603-216">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="d5603-216">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="d5603-217">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="d5603-217">disabledPackageSources</span></span>

<span data-ttu-id="d5603-218">Identificar fontes desabilitadas no momento.</span><span class="sxs-lookup"><span data-stu-id="d5603-218">Identified currently disabled sources.</span></span> <span data-ttu-id="d5603-219">Pode ficar em branco.</span><span class="sxs-lookup"><span data-stu-id="d5603-219">May be empty.</span></span>

| <span data-ttu-id="d5603-220">Chave</span><span class="sxs-lookup"><span data-stu-id="d5603-220">Key</span></span> | <span data-ttu-id="d5603-221">Valor</span><span class="sxs-lookup"><span data-stu-id="d5603-221">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d5603-222">(nome da origem)</span><span class="sxs-lookup"><span data-stu-id="d5603-222">(name of source)</span></span> | <span data-ttu-id="d5603-223">Um valor booliano que indica se a origem está desabilitada.</span><span class="sxs-lookup"><span data-stu-id="d5603-223">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="d5603-224">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="d5603-224">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="d5603-225">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="d5603-225">activePackageSource</span></span>

<span data-ttu-id="d5603-226">*(somente 2.x; preterido no 3.x ou superior)*</span><span class="sxs-lookup"><span data-stu-id="d5603-226">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="d5603-227">Identifica a fonte ativa no momento ou indica a agregação de todas as fontes.</span><span class="sxs-lookup"><span data-stu-id="d5603-227">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="d5603-228">Chave</span><span class="sxs-lookup"><span data-stu-id="d5603-228">Key</span></span> | <span data-ttu-id="d5603-229">Valor</span><span class="sxs-lookup"><span data-stu-id="d5603-229">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d5603-230">(nome da origem) ou `All`</span><span class="sxs-lookup"><span data-stu-id="d5603-230">(name of source) or `All`</span></span> | <span data-ttu-id="d5603-231">Se a chave é o nome de uma fonte, o valor é o caminho ou URL da origem.</span><span class="sxs-lookup"><span data-stu-id="d5603-231">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="d5603-232">Se `All`, o valor deve ser `(Aggregate source)` para combinar todas as origens de pacote que não foram desabilitadas.</span><span class="sxs-lookup"><span data-stu-id="d5603-232">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="d5603-233">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="d5603-233">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```
## <a name="trustedsigners-section"></a><span data-ttu-id="d5603-234">seção trustedSigners</span><span class="sxs-lookup"><span data-stu-id="d5603-234">trustedSigners section</span></span>

<span data-ttu-id="d5603-235">Repositórios confiam signatários usados para permitir que o pacote durante a instalação ou restauração.</span><span class="sxs-lookup"><span data-stu-id="d5603-235">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="d5603-236">Essa lista não pode estar vazia quando o usuário define `signatureValidationMode` para `require`.</span><span class="sxs-lookup"><span data-stu-id="d5603-236">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="d5603-237">Esta seção pode ser atualizada com o [ `nuget trusted-signers` comando](../tools/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="d5603-237">This section can be updated with the [`nuget trusted-signers` command](../tools/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="d5603-238">**Esquema**:</span><span class="sxs-lookup"><span data-stu-id="d5603-238">**Schema**:</span></span>

<span data-ttu-id="d5603-239">Um signatário confiável tem uma coleção de `certificate` itens que inscrever-se todos os certificados que identificam um determinado assinante.</span><span class="sxs-lookup"><span data-stu-id="d5603-239">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="d5603-240">Um signatário confiável pode ser um `Author` ou um `Repository`.</span><span class="sxs-lookup"><span data-stu-id="d5603-240">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="d5603-241">Um confiável *repositório* também especifica a `serviceIndex` para o repositório (que deve ser válido `https` uri) e, opcionalmente, pode especificar uma lista de delimitada por ponto e vírgula de `owners` para restringir ainda mais que é confiável meio desse repositório específico.</span><span class="sxs-lookup"><span data-stu-id="d5603-241">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="d5603-242">Os algoritmos de hash com suporte usados para uma impressão digital do certificado são `SHA256`, `SHA384` e `SHA512`.</span><span class="sxs-lookup"><span data-stu-id="d5603-242">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="d5603-243">Se um `certificate` especifica `allowUntrustedRoot` como `true` o certificado fornecido é permitido encadear para uma raiz não confiável ao criar a cadeia de certificados como parte da verificação de assinatura.</span><span class="sxs-lookup"><span data-stu-id="d5603-243">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="d5603-244">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="d5603-244">**Example**:</span></span>

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="using-environment-variables"></a><span data-ttu-id="d5603-245">Usando variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="d5603-245">Using environment variables</span></span>

<span data-ttu-id="d5603-246">Você pode usar variáveis de ambiente em valores `nuget.config` (NuGet 3.4 ou superior) para aplicar as configurações no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="d5603-246">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="d5603-247">Por exemplo, se a variável de ambiente `HOME` no Windows for definida como `c:\users\username`, o valor de `%HOME%\NuGetRepository` no arquivo de configuração é resolvido para `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="d5603-247">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="d5603-248">Da mesma forma, se o `HOME` no Mac/Linux for definido como `/home/myStuff`, `%HOME%/NuGetRepository` no arquivo de configuração será resolvido para `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="d5603-248">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="d5603-249">Se uma variável de ambiente não for encontrada, o NuGet usa o valor literal do arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="d5603-249">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="d5603-250">Exemplo de arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="d5603-250">Example config file</span></span>

<span data-ttu-id="d5603-251">Abaixo está um arquivo `nuget.config` de exemplo que ilustra diversas configurações:</span><span class="sxs-lookup"><span data-stu-id="d5603-251">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable. On Mac/Linux,
            use $PACKAGE_HOME/External as the value.
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%\External" />

        <!--
            Used to specify default source for the push command.
            See: nuget.exe help push
        -->

        <add key="defaultPushSource" value="https://MyRepo/ES/api/v2/package" />

        <!-- Proxy settings -->
        <add key="http_proxy" value="host" />
        <add key="http_proxy.user" value="username" />
        <add key="http_proxy.password" value="encrypted_password" />
    </config>

    <packageRestore>
        <!-- Allow NuGet to download missing packages -->
        <add key="enabled" value="True" />

        <!-- Automatically check for missing packages during build in Visual Studio -->
        <add key="automatic" value="True" />
    </packageRestore>

    <!--
        Used to specify the default Sources for list, install and update.
        See: nuget.exe help list
        See: nuget.exe help install
        See: nuget.exe help update
    -->
    <packageSources>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
        <add key="MyRepo - ES" value="https://MyRepo/ES/nuget" />
    </packageSources>

    <!-- Used to store credentials -->
    <packageSourceCredentials />

    <!-- Used to disable package sources  -->
    <disabledPackageSources />

    <!--
        Used to specify default API key associated with sources.
        See: nuget.exe help setApiKey
        See: nuget.exe help push
        See: nuget.exe help mirror
    -->
    <apikeys>
        <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
    </apikeys>

    <!--
        Used to specify trusted signers to allow during signature verification.
        See: nuget.exe help trusted-signers
    -->
    <trustedSigners>
        <author name="microsoft">
            <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
