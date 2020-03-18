---
title: Referência do arquivo NuGet. config
description: Referência do arquivo NuGet.Config incluindo as seções config, bindingRedirects, packageRestore, solution e packageSource.
author: karann-msft
ms.author: karann
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: cd321084c46709e3d1d22872c37485edacd33afa
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79429125"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="4e9d6-103">referência de NuGet. config</span><span class="sxs-lookup"><span data-stu-id="4e9d6-103">nuget.config reference</span></span>

<span data-ttu-id="4e9d6-104">O comportamento do NuGet é controlado por configurações em arquivos `NuGet.Config` ou `nuget.config` diferentes, conforme descrito em [configurações comuns do NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="4e9d6-104">NuGet behavior is controlled by settings in different `NuGet.Config` or `nuget.config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="4e9d6-105">`nuget.config` é um arquivo XML que contém um nó `<configuration>` de nível superior, o qual contém os elementos da seção descritos neste tópico.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="4e9d6-106">Cada seção contém zero ou mais itens.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-106">Each section contains zero or more items.</span></span> <span data-ttu-id="4e9d6-107">Consulte o [arquivo de configuração de exemplos](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="4e9d6-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="4e9d6-108">Nomes de configuração não diferenciam maiúsculas de minúsculas e podem usar valores [variáveis de ambiente](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="4e9d6-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="4e9d6-109">seção de configuração</span><span class="sxs-lookup"><span data-stu-id="4e9d6-109">config section</span></span>

<span data-ttu-id="4e9d6-110">Contém diversas definições de configurações, que podem ser definidas usando o comando [`nuget config`](../reference/cli-reference/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="4e9d6-110">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="4e9d6-111">`dependencyVersion` e `repositoryPath` se aplicam somente a projetos que usam `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-111">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="4e9d6-112">`globalPackagesFolder` aplica-se somente a projetos que usam o formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-112">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="4e9d6-113">Chave</span><span class="sxs-lookup"><span data-stu-id="4e9d6-113">Key</span></span> | <span data-ttu-id="4e9d6-114">Valor</span><span class="sxs-lookup"><span data-stu-id="4e9d6-114">Value</span></span> |
| --- | --- |
| <span data-ttu-id="4e9d6-115">dependencyVersion (somente `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="4e9d6-115">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="4e9d6-116">O valor `DependencyVersion` padrão para a instalação, restauração e atualização do pacote, quando a opção `-DependencyVersion` não tiver sido especificada diretamente.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-116">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="4e9d6-117">Esse valor também é usado pela interface do usuário do Gerenciador de Pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-117">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="4e9d6-118">Os valores são `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-118">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="4e9d6-119">globalPackagesFolder (projetos usando apenas PackageReference)</span><span class="sxs-lookup"><span data-stu-id="4e9d6-119">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="4e9d6-120">O local da pasta de pacotes global padrão.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-120">The location of the default global packages folder.</span></span> <span data-ttu-id="4e9d6-121">O padrão é `%userprofile%\.nuget\packages` (Windows) ou `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="4e9d6-121">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="4e9d6-122">Um caminho relativo pode ser usado em arquivos `nuget.config` específicos do projeto.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-122">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="4e9d6-123">Essa configuração é substituída pela variável de ambiente NUGET_PACKAGES, que tem precedência.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-123">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="4e9d6-124">repositoryPath (somente `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="4e9d6-124">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="4e9d6-125">O local no qual instalar os pacotes do NuGet em vez da pasta `$(Solutiondir)/packages` padrão.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-125">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="4e9d6-126">Um caminho relativo pode ser usado em arquivos `nuget.config` específicos do projeto.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-126">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="4e9d6-127">Essa configuração é substituída pela variável de ambiente NUGET_PACKAGES, que tem precedência.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-127">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="4e9d6-128">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="4e9d6-128">defaultPushSource</span></span> | <span data-ttu-id="4e9d6-129">Identifica a URL ou o caminho da origem do pacote que deve ser usada como o padrão se nenhuma outra origem de pacote for encontrada para uma operação.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-129">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="4e9d6-130">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="4e9d6-130">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="4e9d6-131">Configurações de proxy a serem usadas ao se conectar a origens de pacote; `http_proxy` deve estar no formato `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-131">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="4e9d6-132">As senhas são criptografadas e não podem ser adicionadas manualmente.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-132">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="4e9d6-133">Para `no_proxy`, o valor é uma lista separada por vírgulas de domínios a ignorar no servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-133">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="4e9d6-134">Como alternativa, você pode usar as variáveis de ambiente http_proxy e no_proxy para esses valores.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-134">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="4e9d6-135">Para ver detalhes adicionais, consulte [Configurações de proxy do NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="4e9d6-135">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="4e9d6-136">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="4e9d6-136">signatureValidationMode</span></span> | <span data-ttu-id="4e9d6-137">Especifica o modo de validação usado para verificar assinaturas de pacote para instalação do pacote e restauração.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-137">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="4e9d6-138">Os valores são `accept`, `require`.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-138">Values are `accept`, `require`.</span></span> <span data-ttu-id="4e9d6-139">Usa `accept` como padrão.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-139">Defaults to `accept`.</span></span>

<span data-ttu-id="4e9d6-140">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="4e9d6-140">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="4e9d6-141">Seção bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="4e9d6-141">bindingRedirects section</span></span>

<span data-ttu-id="4e9d6-142">Configura se o NuGet realiza redirecionamentos de associação automática quando um pacote é instalado.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-142">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="4e9d6-143">Chave</span><span class="sxs-lookup"><span data-stu-id="4e9d6-143">Key</span></span> | <span data-ttu-id="4e9d6-144">Valor</span><span class="sxs-lookup"><span data-stu-id="4e9d6-144">Value</span></span> |
| --- | --- |
| <span data-ttu-id="4e9d6-145">skip</span><span class="sxs-lookup"><span data-stu-id="4e9d6-145">skip</span></span> | <span data-ttu-id="4e9d6-146">Um valor booliano que indica se os redirecionamentos de associação automática devem ser ignorados.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-146">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="4e9d6-147">O padrão é false.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-147">The default is false.</span></span> |

<span data-ttu-id="4e9d6-148">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="4e9d6-148">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="4e9d6-149">Seção packageRestore</span><span class="sxs-lookup"><span data-stu-id="4e9d6-149">packageRestore section</span></span>

<span data-ttu-id="4e9d6-150">Controla a restauração de pacote durante builds.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-150">Controls package restore during builds.</span></span>

| <span data-ttu-id="4e9d6-151">Chave</span><span class="sxs-lookup"><span data-stu-id="4e9d6-151">Key</span></span> | <span data-ttu-id="4e9d6-152">Valor</span><span class="sxs-lookup"><span data-stu-id="4e9d6-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="4e9d6-153">Habilitado</span><span class="sxs-lookup"><span data-stu-id="4e9d6-153">enabled</span></span> | <span data-ttu-id="4e9d6-154">Um valor booliano que indica se o NuGet pode executar uma restauração automática.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-154">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="4e9d6-155">Você também pode definir a variável de ambiente `EnableNuGetPackageRestore` com um valor de `True` em vez de configurar essa chave no arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-155">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="4e9d6-156">automático</span><span class="sxs-lookup"><span data-stu-id="4e9d6-156">automatic</span></span> | <span data-ttu-id="4e9d6-157">Um valor booliano que indica se o NuGet deve verificar se há pacotes ausentes durante um build.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-157">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="4e9d6-158">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="4e9d6-158">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="4e9d6-159">solution section</span><span class="sxs-lookup"><span data-stu-id="4e9d6-159">solution section</span></span>

<span data-ttu-id="4e9d6-160">Controla se a pasta `packages` de uma solução está incluída no controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-160">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="4e9d6-161">Esta seção funciona somente em arquivos `nuget.config` em uma pasta de solução.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-161">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="4e9d6-162">Chave</span><span class="sxs-lookup"><span data-stu-id="4e9d6-162">Key</span></span> | <span data-ttu-id="4e9d6-163">Valor</span><span class="sxs-lookup"><span data-stu-id="4e9d6-163">Value</span></span> |
| --- | --- |
| <span data-ttu-id="4e9d6-164">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="4e9d6-164">disableSourceControlIntegration</span></span> | <span data-ttu-id="4e9d6-165">Um booliano que indica se a pasta de pacotes deve ser ignorada ao trabalhar com o controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-165">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="4e9d6-166">O valor padrão é false.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-166">The default value is false.</span></span> |

<span data-ttu-id="4e9d6-167">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="4e9d6-167">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="4e9d6-168">Seções de origem de pacote</span><span class="sxs-lookup"><span data-stu-id="4e9d6-168">Package source sections</span></span>

<span data-ttu-id="4e9d6-169">O `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` e `trustedSigners` todos trabalham juntos para configurar como o NuGet funciona com repositórios de pacotes durante as operações de instalação, restauração e atualização.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-169">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="4e9d6-170">O [comando`nuget sources`](../reference/cli-reference/cli-ref-sources.md) geralmente é usado para gerenciar essas configurações, exceto pelo `apikeys` que é gerenciado usando o [comando`nuget setapikey`](../reference/cli-reference/cli-ref-setapikey.md)e `trustedSigners` que é gerenciado usando o [comando`nuget trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="4e9d6-170">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="4e9d6-171">Observe que a URL de origem para nuget.org é `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-171">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="4e9d6-172">packageSources</span><span class="sxs-lookup"><span data-stu-id="4e9d6-172">packageSources</span></span>

<span data-ttu-id="4e9d6-173">Lista todas as origens de pacotes conhecidas.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-173">Lists all known package sources.</span></span> <span data-ttu-id="4e9d6-174">A ordem é ignorada durante as operações de restauração e com qualquer projeto usando o formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-174">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="4e9d6-175">O NuGet respeita a ordem de fontes para operações de instalação e atualização com projetos usando `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-175">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="4e9d6-176">Chave</span><span class="sxs-lookup"><span data-stu-id="4e9d6-176">Key</span></span> | <span data-ttu-id="4e9d6-177">Valor</span><span class="sxs-lookup"><span data-stu-id="4e9d6-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="4e9d6-178">(nome a ser atribuído à origem do pacote)</span><span class="sxs-lookup"><span data-stu-id="4e9d6-178">(name to assign to the package source)</span></span> | <span data-ttu-id="4e9d6-179">O caminho ou URL da origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-179">The path or URL of the package source.</span></span> |

<span data-ttu-id="4e9d6-180">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="4e9d6-180">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

> [!Tip]
> <span data-ttu-id="4e9d6-181">Quando `<clear />` está presente para um nó específico, o NuGet ignora os valores de configuração definidos anteriormente para esse nó.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-181">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span> <span data-ttu-id="4e9d6-182">[Leia mais sobre como as configurações são aplicadas](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span><span class="sxs-lookup"><span data-stu-id="4e9d6-182">[Read more about how settings are applied](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

### <a name="packagesourcecredentials"></a><span data-ttu-id="4e9d6-183">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="4e9d6-183">packageSourceCredentials</span></span>

<span data-ttu-id="4e9d6-184">Armazena os nomes de usuário e senhas para as origens, geralmente especificado com as opções `-username` e `-password` com `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-184">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="4e9d6-185">As senhas são criptografadas por padrão, a menos que a opção `-storepasswordincleartext` também seja usada.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-185">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="4e9d6-186">Chave</span><span class="sxs-lookup"><span data-stu-id="4e9d6-186">Key</span></span> | <span data-ttu-id="4e9d6-187">Valor</span><span class="sxs-lookup"><span data-stu-id="4e9d6-187">Value</span></span> |
| --- | --- |
| <span data-ttu-id="4e9d6-188">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="4e9d6-188">username</span></span> | <span data-ttu-id="4e9d6-189">O nome de usuário para a origem em texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-189">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="4e9d6-190">password</span><span class="sxs-lookup"><span data-stu-id="4e9d6-190">password</span></span> | <span data-ttu-id="4e9d6-191">A senha criptografada para a origem.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-191">The encrypted password for the source.</span></span> |
| <span data-ttu-id="4e9d6-192">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="4e9d6-192">cleartextpassword</span></span> | <span data-ttu-id="4e9d6-193">A senha não criptografada para a origem.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-193">The unencrypted password for the source.</span></span> |

<span data-ttu-id="4e9d6-194">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="4e9d6-194">**Example:**</span></span>

<span data-ttu-id="4e9d6-195">No arquivo de configuração, o elemento `<packageSourceCredentials>` contém nós filho para cada nome de origem aplicável (espaços no nome serão substituídos por `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="4e9d6-195">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="4e9d6-196">Ou seja, para origens chamadas “Contoso” e “Origem de teste”, o arquivo de configuração contém o seguinte ao usar senhas criptografadas:</span><span class="sxs-lookup"><span data-stu-id="4e9d6-196">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="4e9d6-197">Ao usar senhas não criptografadas:</span><span class="sxs-lookup"><span data-stu-id="4e9d6-197">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="4e9d6-198">apikeys</span><span class="sxs-lookup"><span data-stu-id="4e9d6-198">apikeys</span></span>

<span data-ttu-id="4e9d6-199">Armazena as chaves de origens que usam autenticação de chave de API, conforme definido com o comando [`nuget setapikey`](../reference/cli-reference/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="4e9d6-199">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="4e9d6-200">Chave</span><span class="sxs-lookup"><span data-stu-id="4e9d6-200">Key</span></span> | <span data-ttu-id="4e9d6-201">Valor</span><span class="sxs-lookup"><span data-stu-id="4e9d6-201">Value</span></span> |
| --- | --- |
| <span data-ttu-id="4e9d6-202">(URL de origem)</span><span class="sxs-lookup"><span data-stu-id="4e9d6-202">(source URL)</span></span> | <span data-ttu-id="4e9d6-203">A chave de API criptografada.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-203">The encrypted API key.</span></span> |

<span data-ttu-id="4e9d6-204">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="4e9d6-204">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="4e9d6-205">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="4e9d6-205">disabledPackageSources</span></span>

<span data-ttu-id="4e9d6-206">Identificar fontes desabilitadas no momento.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-206">Identified currently disabled sources.</span></span> <span data-ttu-id="4e9d6-207">Pode ficar em branco.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-207">May be empty.</span></span>

| <span data-ttu-id="4e9d6-208">Chave</span><span class="sxs-lookup"><span data-stu-id="4e9d6-208">Key</span></span> | <span data-ttu-id="4e9d6-209">Valor</span><span class="sxs-lookup"><span data-stu-id="4e9d6-209">Value</span></span> |
| --- | --- |
| <span data-ttu-id="4e9d6-210">(nome da origem)</span><span class="sxs-lookup"><span data-stu-id="4e9d6-210">(name of source)</span></span> | <span data-ttu-id="4e9d6-211">Um valor booliano que indica se a origem está desabilitada.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-211">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="4e9d6-212">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="4e9d6-212">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="4e9d6-213">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="4e9d6-213">activePackageSource</span></span>

<span data-ttu-id="4e9d6-214">*(somente 2.x; preterido no 3.x ou superior)*</span><span class="sxs-lookup"><span data-stu-id="4e9d6-214">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="4e9d6-215">Identifica a fonte ativa no momento ou indica a agregação de todas as fontes.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-215">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="4e9d6-216">Chave</span><span class="sxs-lookup"><span data-stu-id="4e9d6-216">Key</span></span> | <span data-ttu-id="4e9d6-217">Valor</span><span class="sxs-lookup"><span data-stu-id="4e9d6-217">Value</span></span> |
| --- | --- |
| <span data-ttu-id="4e9d6-218">(nome da origem) ou `All`</span><span class="sxs-lookup"><span data-stu-id="4e9d6-218">(name of source) or `All`</span></span> | <span data-ttu-id="4e9d6-219">Se a chave é o nome de uma fonte, o valor é o caminho ou URL da origem.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-219">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="4e9d6-220">Se `All`, o valor deve ser `(Aggregate source)` para combinar todas as origens de pacote que não foram desabilitadas.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-220">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="4e9d6-221">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="4e9d6-221">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a><span data-ttu-id="4e9d6-222">seção trustedSigners</span><span class="sxs-lookup"><span data-stu-id="4e9d6-222">trustedSigners section</span></span>

<span data-ttu-id="4e9d6-223">Armazena os assinantes confiáveis usados para permitir o pacote durante a instalação ou restauração.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-223">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="4e9d6-224">Esta lista não pode ficar vazia quando o usuário define `signatureValidationMode` para `require`.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-224">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="4e9d6-225">Esta seção pode ser atualizada com o [comando`nuget trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="4e9d6-225">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="4e9d6-226">**Esquema**:</span><span class="sxs-lookup"><span data-stu-id="4e9d6-226">**Schema**:</span></span>

<span data-ttu-id="4e9d6-227">Um signatário confiável tem uma coleção de `certificate` itens que inscrevem todos os certificados que identificam um determinado assinante.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-227">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="4e9d6-228">Um signatário confiável pode ser um `Author` ou um `Repository`.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-228">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="4e9d6-229">Um *repositório* confiável também especifica o `serviceIndex` para o repositório (que deve ser um uri de `https` válido) e, opcionalmente, pode especificar uma lista delimitada por ponto-e-vírgula de `owners` para restringir ainda mais a confiança desse repositório específico.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-229">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="4e9d6-230">Os algoritmos de hash com suporte usados para uma impressão digital de certificado são `SHA256`, `SHA384` e `SHA512`.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-230">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="4e9d6-231">Se um `certificate` especificar `allowUntrustedRoot` como `true` o certificado fornecido poderá ser encadeado a uma raiz não confiável durante a criação da cadeia de certificados como parte da verificação da assinatura.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-231">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="4e9d6-232">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="4e9d6-232">**Example**:</span></span>

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

## <a name="fallbackpackagefolders-section"></a><span data-ttu-id="4e9d6-233">seção fallbackPackageFolders</span><span class="sxs-lookup"><span data-stu-id="4e9d6-233">fallbackPackageFolders section</span></span>

<span data-ttu-id="4e9d6-234">*(3,5 +)* Fornece uma maneira de pré-instalar pacotes para que nenhum trabalho precise ser feito se o pacote for encontrado nas pastas de fallback.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-234">*(3.5+)* Provides a way to preinstall packages so that no work needs to be done if the package is found in the fallback folders.</span></span> <span data-ttu-id="4e9d6-235">As pastas de pacote de fallback têm exatamente a mesma estrutura de pasta e arquivo que a pasta de pacote global: *. nupkg* está presente e todos os arquivos são extraídos.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-235">Fallback package folders have the exact same folder and file structure as the global package folder: *.nupkg* is present, and all files are extracted.</span></span>

<span data-ttu-id="4e9d6-236">A lógica de pesquisa para essa configuração é:</span><span class="sxs-lookup"><span data-stu-id="4e9d6-236">The lookup logic for this configuration is:</span></span>

- <span data-ttu-id="4e9d6-237">Procure na pasta de pacote global para ver se o pacote/versão já foi baixado.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-237">Look in global package folder to see if the package/version is already downloaded.</span></span>

- <span data-ttu-id="4e9d6-238">Procure uma correspondência de pacote/versão nas pastas de fallback.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-238">Look in the fallback folders for a package/version match.</span></span>

<span data-ttu-id="4e9d6-239">Se a pesquisa for bem-sucedida, nenhum download será necessário.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-239">If either lookup is successful, then no download is necessary.</span></span>

<span data-ttu-id="4e9d6-240">Se uma correspondência não for encontrada, o NuGet verificará as fontes de arquivo e, em seguida, as fontes http e baixará os pacotes.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-240">If a match is not found, then NuGet checks file sources, and then http sources, and then it downloads the packages.</span></span>

| <span data-ttu-id="4e9d6-241">Chave</span><span class="sxs-lookup"><span data-stu-id="4e9d6-241">Key</span></span> | <span data-ttu-id="4e9d6-242">Valor</span><span class="sxs-lookup"><span data-stu-id="4e9d6-242">Value</span></span> |
| --- | --- |
| <span data-ttu-id="4e9d6-243">(nome da pasta de fallback)</span><span class="sxs-lookup"><span data-stu-id="4e9d6-243">(name of fallback folder)</span></span> | <span data-ttu-id="4e9d6-244">Caminho para a pasta de fallback.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-244">Path to fallback folder.</span></span> |

<span data-ttu-id="4e9d6-245">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="4e9d6-245">**Example**:</span></span>

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a><span data-ttu-id="4e9d6-246">seção packageManagement</span><span class="sxs-lookup"><span data-stu-id="4e9d6-246">packageManagement section</span></span>

<span data-ttu-id="4e9d6-247">Define o formato de gerenciamento de pacote padrão, *Packages. config* ou PackageReference.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-247">Sets the default package management format, either *packages.config* or PackageReference.</span></span> <span data-ttu-id="4e9d6-248">Projetos no estilo SDK sempre usam PackageReference.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-248">SDK-style projects always use PackageReference.</span></span>

| <span data-ttu-id="4e9d6-249">Chave</span><span class="sxs-lookup"><span data-stu-id="4e9d6-249">Key</span></span> | <span data-ttu-id="4e9d6-250">Valor</span><span class="sxs-lookup"><span data-stu-id="4e9d6-250">Value</span></span> |
| --- | --- |
| <span data-ttu-id="4e9d6-251">format</span><span class="sxs-lookup"><span data-stu-id="4e9d6-251">format</span></span> | <span data-ttu-id="4e9d6-252">Um booliano que indica o formato de gerenciamento de pacote padrão.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-252">A Boolean indicating the default package management format.</span></span> <span data-ttu-id="4e9d6-253">Se `1`, o formato será PackageReference.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-253">If `1`, format is PackageReference.</span></span> <span data-ttu-id="4e9d6-254">Se `0`, Format será *Packages. config*.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-254">If `0`, format is *packages.config*.</span></span> |
| <span data-ttu-id="4e9d6-255">desabilitado</span><span class="sxs-lookup"><span data-stu-id="4e9d6-255">disabled</span></span> | <span data-ttu-id="4e9d6-256">Um booliano que indica se o prompt deve ser mostrado para selecionar um formato de pacote padrão na instalação do primeiro pacote.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-256">A Boolean indicating whether to show the prompt to select a default package format on first package install.</span></span> <span data-ttu-id="4e9d6-257">`False` oculta o prompt.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-257">`False` hides the prompt.</span></span> |

<span data-ttu-id="4e9d6-258">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="4e9d6-258">**Example**:</span></span>

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a><span data-ttu-id="4e9d6-259">Usando variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="4e9d6-259">Using environment variables</span></span>

<span data-ttu-id="4e9d6-260">Você pode usar variáveis de ambiente em valores `nuget.config` (NuGet 3.4 ou superior) para aplicar as configurações no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-260">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="4e9d6-261">Por exemplo, se a variável de ambiente `HOME` no Windows for definida como `c:\users\username`, o valor de `%HOME%\NuGetRepository` no arquivo de configuração é resolvido para `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-261">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="4e9d6-262">Observe que você precisa usar variáveis de ambiente no estilo do Windows (começa e termina com%) mesmo no Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-262">Note that you have to use Windows-style environment variables (starts and ends with %) even on Mac/Linux.</span></span> <span data-ttu-id="4e9d6-263">Ter `$HOME/NuGetRepository` em um arquivo de configuração não será resolvido.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-263">Having `$HOME/NuGetRepository` in a configuration file will not resolve.</span></span> <span data-ttu-id="4e9d6-264">No Mac/Linux, o valor de `%HOME%\NuGetRepository` será resolvido para `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-264">On Mac/Linux the value of `%HOME%\NuGetRepository` will resolve to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="4e9d6-265">Se uma variável de ambiente não for encontrada, o NuGet usa o valor literal do arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="4e9d6-265">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="4e9d6-266">Exemplo de arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="4e9d6-266">Example config file</span></span>

<span data-ttu-id="4e9d6-267">Veja abaixo um exemplo `nuget.config` arquivo que ilustra várias configurações, incluindo as opcionais:</span><span class="sxs-lookup"><span data-stu-id="4e9d6-267">Below is an example `nuget.config` file that illustrates a number of settings including optional ones:</span></span>

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
