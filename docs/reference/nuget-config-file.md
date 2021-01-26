---
title: Referência de arquivo de nuget.config
description: Referência do arquivo NuGet.Config incluindo as seções config, bindingRedirects, packageRestore, solution e packageSource.
author: JonDouglas
ms.author: jodou
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: 9b15550d0e6e8aec4d526391d77c654a756f343e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777659"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="7eee3-103">Referência de nuget.config</span><span class="sxs-lookup"><span data-stu-id="7eee3-103">nuget.config reference</span></span>

<span data-ttu-id="7eee3-104">O comportamento do NuGet é controlado por configurações `NuGet.Config` em `nuget.config` arquivos diferentes ou conforme descrito em [configurações comuns do NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="7eee3-104">NuGet behavior is controlled by settings in different `NuGet.Config` or `nuget.config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="7eee3-105">`nuget.config` é um arquivo XML que contém um nó `<configuration>` de nível superior, o qual contém os elementos da seção descritos neste tópico.</span><span class="sxs-lookup"><span data-stu-id="7eee3-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="7eee3-106">Cada seção contém zero ou mais itens.</span><span class="sxs-lookup"><span data-stu-id="7eee3-106">Each section contains zero or more items.</span></span> <span data-ttu-id="7eee3-107">Consulte o [arquivo de configuração de exemplos](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="7eee3-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="7eee3-108">Nomes de configuração não diferenciam maiúsculas de minúsculas e podem usar valores [variáveis de ambiente](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="7eee3-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="7eee3-109">seção de configuração</span><span class="sxs-lookup"><span data-stu-id="7eee3-109">config section</span></span>

<span data-ttu-id="7eee3-110">Contém diversas definições de configuração, que podem ser definidas usando o [ `nuget config` comando](../reference/cli-reference/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="7eee3-110">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="7eee3-111">`dependencyVersion` e `repositoryPath` aplicam-se somente a projetos que usam o `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="7eee3-111">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="7eee3-112">`globalPackagesFolder` aplica-se somente a projetos que usam o formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="7eee3-112">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="7eee3-113">Chave</span><span class="sxs-lookup"><span data-stu-id="7eee3-113">Key</span></span> | <span data-ttu-id="7eee3-114">Valor</span><span class="sxs-lookup"><span data-stu-id="7eee3-114">Value</span></span> |
| --- | --- |
| <span data-ttu-id="7eee3-115">dependencyVersion (somente `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="7eee3-115">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="7eee3-116">O valor `DependencyVersion` padrão para a instalação, restauração e atualização do pacote, quando a opção `-DependencyVersion` não tiver sido especificada diretamente.</span><span class="sxs-lookup"><span data-stu-id="7eee3-116">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="7eee3-117">Esse valor também é usado pela interface do usuário do Gerenciador de Pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="7eee3-117">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="7eee3-118">Os valores são `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="7eee3-118">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="7eee3-119">globalPackagesFolder (projetos usando apenas PackageReference)</span><span class="sxs-lookup"><span data-stu-id="7eee3-119">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="7eee3-120">O local da pasta de pacotes global padrão.</span><span class="sxs-lookup"><span data-stu-id="7eee3-120">The location of the default global packages folder.</span></span> <span data-ttu-id="7eee3-121">O padrão é `%userprofile%\.nuget\packages` (Windows) ou `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="7eee3-121">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="7eee3-122">Um caminho relativo pode ser usado em arquivos `nuget.config` específicos do projeto.</span><span class="sxs-lookup"><span data-stu-id="7eee3-122">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="7eee3-123">Essa configuração é substituída pela variável de ambiente NUGET_PACKAGES, que tem precedência.</span><span class="sxs-lookup"><span data-stu-id="7eee3-123">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="7eee3-124">repositoryPath (somente `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="7eee3-124">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="7eee3-125">O local no qual instalar os pacotes do NuGet em vez da pasta `$(Solutiondir)/packages` padrão.</span><span class="sxs-lookup"><span data-stu-id="7eee3-125">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="7eee3-126">Um caminho relativo pode ser usado em arquivos `nuget.config` específicos do projeto.</span><span class="sxs-lookup"><span data-stu-id="7eee3-126">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="7eee3-127">Essa configuração é substituída pela variável de ambiente NUGET_PACKAGES, que tem precedência.</span><span class="sxs-lookup"><span data-stu-id="7eee3-127">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="7eee3-128">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="7eee3-128">defaultPushSource</span></span> | <span data-ttu-id="7eee3-129">Identifica a URL ou o caminho da origem do pacote que deve ser usada como o padrão se nenhuma outra origem de pacote for encontrada para uma operação.</span><span class="sxs-lookup"><span data-stu-id="7eee3-129">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="7eee3-130">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="7eee3-130">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="7eee3-131">Configurações de proxy a serem usadas ao se conectar a origens de pacote; `http_proxy` deve estar no formato `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="7eee3-131">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="7eee3-132">As senhas são criptografadas e não podem ser adicionadas manualmente.</span><span class="sxs-lookup"><span data-stu-id="7eee3-132">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="7eee3-133">Para `no_proxy`, o valor é uma lista separada por vírgulas de domínios a ignorar no servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="7eee3-133">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="7eee3-134">Como alternativa, você pode usar as variáveis de ambiente http_proxy e no_proxy para esses valores.</span><span class="sxs-lookup"><span data-stu-id="7eee3-134">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="7eee3-135">Para ver detalhes adicionais, consulte [Configurações de proxy do NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="7eee3-135">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="7eee3-136">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="7eee3-136">signatureValidationMode</span></span> | <span data-ttu-id="7eee3-137">Especifica o modo de validação usado para verificar assinaturas de pacote para instalação do pacote e restauração.</span><span class="sxs-lookup"><span data-stu-id="7eee3-137">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="7eee3-138">Os valores são `accept` , `require` .</span><span class="sxs-lookup"><span data-stu-id="7eee3-138">Values are `accept`, `require`.</span></span> <span data-ttu-id="7eee3-139">Assume o padrão de `accept`.</span><span class="sxs-lookup"><span data-stu-id="7eee3-139">Defaults to `accept`.</span></span>

<span data-ttu-id="7eee3-140">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="7eee3-140">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="7eee3-141">Seção bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="7eee3-141">bindingRedirects section</span></span>

<span data-ttu-id="7eee3-142">Configura se o NuGet realiza redirecionamentos de associação automática quando um pacote é instalado.</span><span class="sxs-lookup"><span data-stu-id="7eee3-142">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="7eee3-143">Chave</span><span class="sxs-lookup"><span data-stu-id="7eee3-143">Key</span></span> | <span data-ttu-id="7eee3-144">Valor</span><span class="sxs-lookup"><span data-stu-id="7eee3-144">Value</span></span> |
| --- | --- |
| <span data-ttu-id="7eee3-145">skip</span><span class="sxs-lookup"><span data-stu-id="7eee3-145">skip</span></span> | <span data-ttu-id="7eee3-146">Um valor booliano que indica se os redirecionamentos de associação automática devem ser ignorados.</span><span class="sxs-lookup"><span data-stu-id="7eee3-146">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="7eee3-147">O padrão é falso.</span><span class="sxs-lookup"><span data-stu-id="7eee3-147">The default is false.</span></span> |

<span data-ttu-id="7eee3-148">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="7eee3-148">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="7eee3-149">Seção packageRestore</span><span class="sxs-lookup"><span data-stu-id="7eee3-149">packageRestore section</span></span>

<span data-ttu-id="7eee3-150">Controla a restauração de pacote durante builds.</span><span class="sxs-lookup"><span data-stu-id="7eee3-150">Controls package restore during builds.</span></span>

| <span data-ttu-id="7eee3-151">Chave</span><span class="sxs-lookup"><span data-stu-id="7eee3-151">Key</span></span> | <span data-ttu-id="7eee3-152">Valor</span><span class="sxs-lookup"><span data-stu-id="7eee3-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="7eee3-153">Habilitado</span><span class="sxs-lookup"><span data-stu-id="7eee3-153">enabled</span></span> | <span data-ttu-id="7eee3-154">Um valor booliano que indica se o NuGet pode executar uma restauração automática.</span><span class="sxs-lookup"><span data-stu-id="7eee3-154">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="7eee3-155">Você também pode definir a variável de ambiente `EnableNuGetPackageRestore` com um valor de `True` em vez de configurar essa chave no arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="7eee3-155">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="7eee3-156">automático</span><span class="sxs-lookup"><span data-stu-id="7eee3-156">automatic</span></span> | <span data-ttu-id="7eee3-157">Um valor booliano que indica se o NuGet deve verificar se há pacotes ausentes durante um build.</span><span class="sxs-lookup"><span data-stu-id="7eee3-157">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="7eee3-158">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="7eee3-158">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="7eee3-159">solution section</span><span class="sxs-lookup"><span data-stu-id="7eee3-159">solution section</span></span>

<span data-ttu-id="7eee3-160">Controla se a pasta `packages` de uma solução está incluída no controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="7eee3-160">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="7eee3-161">Esta seção funciona somente em arquivos `nuget.config` em uma pasta de solução.</span><span class="sxs-lookup"><span data-stu-id="7eee3-161">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="7eee3-162">Chave</span><span class="sxs-lookup"><span data-stu-id="7eee3-162">Key</span></span> | <span data-ttu-id="7eee3-163">Valor</span><span class="sxs-lookup"><span data-stu-id="7eee3-163">Value</span></span> |
| --- | --- |
| <span data-ttu-id="7eee3-164">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="7eee3-164">disableSourceControlIntegration</span></span> | <span data-ttu-id="7eee3-165">Um booliano que indica se a pasta de pacotes deve ser ignorada ao trabalhar com o controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="7eee3-165">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="7eee3-166">O valor padrão é false.</span><span class="sxs-lookup"><span data-stu-id="7eee3-166">The default value is false.</span></span> |

<span data-ttu-id="7eee3-167">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="7eee3-167">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="7eee3-168">Seções de origem de pacote</span><span class="sxs-lookup"><span data-stu-id="7eee3-168">Package source sections</span></span>

<span data-ttu-id="7eee3-169">O `packageSources` , `packageSourceCredentials` , `apikeys` , `activePackageSource` , `disabledPackageSources` e `trustedSigners` todos trabalham juntos para configurar como o NuGet funciona com repositórios de pacotes durante operações de instalação, restauração e atualização.</span><span class="sxs-lookup"><span data-stu-id="7eee3-169">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="7eee3-170">O [ `nuget sources` comando](../reference/cli-reference/cli-ref-sources.md) geralmente é usado para gerenciar essas configurações, exceto para o `apikeys` que é gerenciado usando o [ `nuget setapikey` comando](../reference/cli-reference/cli-ref-setapikey.md)e `trustedSigners` que é gerenciado usando o [ `nuget trusted-signers` comando](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="7eee3-170">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="7eee3-171">Observe que a URL de origem para nuget.org é `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="7eee3-171">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="7eee3-172">packageSources</span><span class="sxs-lookup"><span data-stu-id="7eee3-172">packageSources</span></span>

<span data-ttu-id="7eee3-173">Lista todas as origens de pacotes conhecidas.</span><span class="sxs-lookup"><span data-stu-id="7eee3-173">Lists all known package sources.</span></span> <span data-ttu-id="7eee3-174">A ordem é ignorada durante as operações de restauração e com qualquer projeto usando o formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="7eee3-174">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="7eee3-175">O NuGet respeita a ordem de fontes para operações de instalação e atualização com projetos usando o `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="7eee3-175">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="7eee3-176">Chave</span><span class="sxs-lookup"><span data-stu-id="7eee3-176">Key</span></span> | <span data-ttu-id="7eee3-177">Valor</span><span class="sxs-lookup"><span data-stu-id="7eee3-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="7eee3-178">(nome a ser atribuído à origem do pacote)</span><span class="sxs-lookup"><span data-stu-id="7eee3-178">(name to assign to the package source)</span></span> | <span data-ttu-id="7eee3-179">O caminho ou URL da origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="7eee3-179">The path or URL of the package source.</span></span> |

<span data-ttu-id="7eee3-180">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="7eee3-180">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

> [!Tip]
> <span data-ttu-id="7eee3-181">Quando `<clear />` está presente para um nó específico, o NuGet ignora os valores de configuração definidos anteriormente para esse nó.</span><span class="sxs-lookup"><span data-stu-id="7eee3-181">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span> <span data-ttu-id="7eee3-182">[Leia mais sobre como as configurações são aplicadas](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span><span class="sxs-lookup"><span data-stu-id="7eee3-182">[Read more about how settings are applied](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

### <a name="packagesourcecredentials"></a><span data-ttu-id="7eee3-183">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="7eee3-183">packageSourceCredentials</span></span>

<span data-ttu-id="7eee3-184">Armazena os nomes de usuário e senhas para as origens, geralmente especificado com as opções `-username` e `-password` com `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="7eee3-184">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="7eee3-185">As senhas são criptografadas por padrão, a menos que a opção `-storepasswordincleartext` também seja usada.</span><span class="sxs-lookup"><span data-stu-id="7eee3-185">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>
<span data-ttu-id="7eee3-186">Opcionalmente, os tipos de autenticação válidos podem ser especificados com a `-validauthenticationtypes` opção.</span><span class="sxs-lookup"><span data-stu-id="7eee3-186">Optionally, valid authentication types can be specified with the `-validauthenticationtypes` switch.</span></span>

| <span data-ttu-id="7eee3-187">Chave</span><span class="sxs-lookup"><span data-stu-id="7eee3-187">Key</span></span> | <span data-ttu-id="7eee3-188">Valor</span><span class="sxs-lookup"><span data-stu-id="7eee3-188">Value</span></span> |
| --- | --- |
| <span data-ttu-id="7eee3-189">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="7eee3-189">username</span></span> | <span data-ttu-id="7eee3-190">O nome de usuário para a origem em texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="7eee3-190">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="7eee3-191">password</span><span class="sxs-lookup"><span data-stu-id="7eee3-191">password</span></span> | <span data-ttu-id="7eee3-192">A senha criptografada para a origem.</span><span class="sxs-lookup"><span data-stu-id="7eee3-192">The encrypted password for the source.</span></span> <span data-ttu-id="7eee3-193">As senhas criptografadas só têm suporte no Windows e só podem ser descriptografadas quando usadas no mesmo computador e por meio do mesmo usuário que a criptografia original.</span><span class="sxs-lookup"><span data-stu-id="7eee3-193">Encrypted passwords are only supported on Windows, and only can be decrypted when used on the same machine and via the same user as the original encryption.</span></span> |
| <span data-ttu-id="7eee3-194">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="7eee3-194">cleartextpassword</span></span> | <span data-ttu-id="7eee3-195">A senha não criptografada para a origem.</span><span class="sxs-lookup"><span data-stu-id="7eee3-195">The unencrypted password for the source.</span></span> <span data-ttu-id="7eee3-196">Observação: as variáveis de ambiente podem ser usadas para aumentar a segurança.</span><span class="sxs-lookup"><span data-stu-id="7eee3-196">Note: environment variables can be used for improved security.</span></span> |
| <span data-ttu-id="7eee3-197">validauthenticationtypes</span><span class="sxs-lookup"><span data-stu-id="7eee3-197">validauthenticationtypes</span></span> | <span data-ttu-id="7eee3-198">Lista separada por vírgulas de tipos de autenticação válidos para esta fonte.</span><span class="sxs-lookup"><span data-stu-id="7eee3-198">Comma-separated list of valid authentication types for this source.</span></span> <span data-ttu-id="7eee3-199">Defina isso como `basic` se o servidor anunciar NTLM ou negociar e suas credenciais devem ser enviadas usando o mecanismo básico, por exemplo, ao usar uma Pat com Azure DevOps Server locais.</span><span class="sxs-lookup"><span data-stu-id="7eee3-199">Set this to `basic` if the server advertises NTLM or Negotiate and your credentials must be sent using the Basic mechanism, for instance when using a PAT with on-premises Azure DevOps Server.</span></span> <span data-ttu-id="7eee3-200">Outros valores válidos incluem `negotiate` , `kerberos` , `ntlm` e `digest` , mas esses valores são improvável de ser úteis.</span><span class="sxs-lookup"><span data-stu-id="7eee3-200">Other valid values include `negotiate`, `kerberos`, `ntlm`, and `digest`, but these values are unlikely to be useful.</span></span> |

<span data-ttu-id="7eee3-201">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="7eee3-201">**Example:**</span></span>

<span data-ttu-id="7eee3-202">No arquivo de configuração, o elemento `<packageSourceCredentials>` contém nós filho para cada nome de origem aplicável (espaços no nome serão substituídos por `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="7eee3-202">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="7eee3-203">Ou seja, para origens chamadas “Contoso” e “Origem de teste”, o arquivo de configuração contém o seguinte ao usar senhas criptografadas:</span><span class="sxs-lookup"><span data-stu-id="7eee3-203">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="7eee3-204">Ao usar senhas não criptografadas armazenadas em uma variável de ambiente:</span><span class="sxs-lookup"><span data-stu-id="7eee3-204">When using unencrypted passwords stored in an environment variable:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="%ContosoPassword%" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="%TestSourcePassword%" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

<span data-ttu-id="7eee3-205">Ao usar senhas não criptografadas:</span><span class="sxs-lookup"><span data-stu-id="7eee3-205">When using unencrypted passwords:</span></span>

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

<span data-ttu-id="7eee3-206">Além disso, os métodos de autenticação válidos podem ser fornecidos:</span><span class="sxs-lookup"><span data-stu-id="7eee3-206">Additionally, valid authentication methods can be supplied:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
        <add key="ValidAuthenticationTypes" value="basic" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
        <add key="ValidAuthenticationTypes" value="basic, negotiate" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a><span data-ttu-id="7eee3-207">apikeys</span><span class="sxs-lookup"><span data-stu-id="7eee3-207">apikeys</span></span>

<span data-ttu-id="7eee3-208">Armazena chaves para fontes que usam autenticação de chave de API, conforme definido com o [ `nuget setapikey` comando](../reference/cli-reference/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="7eee3-208">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="7eee3-209">Chave</span><span class="sxs-lookup"><span data-stu-id="7eee3-209">Key</span></span> | <span data-ttu-id="7eee3-210">Valor</span><span class="sxs-lookup"><span data-stu-id="7eee3-210">Value</span></span> |
| --- | --- |
| <span data-ttu-id="7eee3-211">(URL de origem)</span><span class="sxs-lookup"><span data-stu-id="7eee3-211">(source URL)</span></span> | <span data-ttu-id="7eee3-212">A chave de API criptografada.</span><span class="sxs-lookup"><span data-stu-id="7eee3-212">The encrypted API key.</span></span> |

<span data-ttu-id="7eee3-213">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="7eee3-213">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="7eee3-214">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="7eee3-214">disabledPackageSources</span></span>

<span data-ttu-id="7eee3-215">Identificar fontes desabilitadas no momento.</span><span class="sxs-lookup"><span data-stu-id="7eee3-215">Identified currently disabled sources.</span></span> <span data-ttu-id="7eee3-216">Pode ficar em branco.</span><span class="sxs-lookup"><span data-stu-id="7eee3-216">May be empty.</span></span>

| <span data-ttu-id="7eee3-217">Chave</span><span class="sxs-lookup"><span data-stu-id="7eee3-217">Key</span></span> | <span data-ttu-id="7eee3-218">Valor</span><span class="sxs-lookup"><span data-stu-id="7eee3-218">Value</span></span> |
| --- | --- |
| <span data-ttu-id="7eee3-219">(nome da origem)</span><span class="sxs-lookup"><span data-stu-id="7eee3-219">(name of source)</span></span> | <span data-ttu-id="7eee3-220">Um valor booliano que indica se a origem está desabilitada.</span><span class="sxs-lookup"><span data-stu-id="7eee3-220">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="7eee3-221">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="7eee3-221">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="7eee3-222">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="7eee3-222">activePackageSource</span></span>

<span data-ttu-id="7eee3-223">*(somente 2.x; preterido no 3.x ou superior)*</span><span class="sxs-lookup"><span data-stu-id="7eee3-223">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="7eee3-224">Identifica a fonte ativa no momento ou indica a agregação de todas as fontes.</span><span class="sxs-lookup"><span data-stu-id="7eee3-224">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="7eee3-225">Chave</span><span class="sxs-lookup"><span data-stu-id="7eee3-225">Key</span></span> | <span data-ttu-id="7eee3-226">Valor</span><span class="sxs-lookup"><span data-stu-id="7eee3-226">Value</span></span> |
| --- | --- |
| <span data-ttu-id="7eee3-227">(nome da origem) ou `All`</span><span class="sxs-lookup"><span data-stu-id="7eee3-227">(name of source) or `All`</span></span> | <span data-ttu-id="7eee3-228">Se a chave é o nome de uma fonte, o valor é o caminho ou URL da origem.</span><span class="sxs-lookup"><span data-stu-id="7eee3-228">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="7eee3-229">Se `All`, o valor deve ser `(Aggregate source)` para combinar todas as origens de pacote que não foram desabilitadas.</span><span class="sxs-lookup"><span data-stu-id="7eee3-229">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="7eee3-230">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="7eee3-230">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a><span data-ttu-id="7eee3-231">seção trustedSigners</span><span class="sxs-lookup"><span data-stu-id="7eee3-231">trustedSigners section</span></span>

<span data-ttu-id="7eee3-232">Armazena os assinantes confiáveis usados para permitir o pacote durante a instalação ou restauração.</span><span class="sxs-lookup"><span data-stu-id="7eee3-232">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="7eee3-233">Esta lista não pode estar vazia quando o usuário define `signatureValidationMode` como `require` .</span><span class="sxs-lookup"><span data-stu-id="7eee3-233">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="7eee3-234">Esta seção pode ser atualizada com o [ `nuget trusted-signers` comando](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="7eee3-234">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="7eee3-235">**Esquema**:</span><span class="sxs-lookup"><span data-stu-id="7eee3-235">**Schema**:</span></span>

<span data-ttu-id="7eee3-236">Um assinante confiável tem uma coleção de `certificate` itens que inscrevem todos os certificados que identificam um determinado signatário.</span><span class="sxs-lookup"><span data-stu-id="7eee3-236">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="7eee3-237">Um signatário confiável pode ser um `Author` ou um `Repository` .</span><span class="sxs-lookup"><span data-stu-id="7eee3-237">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="7eee3-238">Um *repositório* confiável também especifica o `serviceIndex` para o repositório (que deve ser um URI válido `https` ) e pode, opcionalmente, especificar uma lista delimitada por ponto e vírgula de `owners` para restringir ainda mais o que é confiável desse repositório específico.</span><span class="sxs-lookup"><span data-stu-id="7eee3-238">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="7eee3-239">Os algoritmos de hash com suporte usados para uma impressão digital de certificado são `SHA256` `SHA384` e `SHA512` .</span><span class="sxs-lookup"><span data-stu-id="7eee3-239">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="7eee3-240">Se um `certificate` especifica `allowUntrustedRoot` que `true` o certificado fornecido pode encadear a uma raiz não confiável ao criar a cadeia de certificados como parte da verificação de assinatura.</span><span class="sxs-lookup"><span data-stu-id="7eee3-240">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="7eee3-241">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="7eee3-241">**Example**:</span></span>

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="fallbackpackagefolders-section"></a><span data-ttu-id="7eee3-242">seção fallbackPackageFolders</span><span class="sxs-lookup"><span data-stu-id="7eee3-242">fallbackPackageFolders section</span></span>

<span data-ttu-id="7eee3-243">*(3,5 +)* Fornece uma maneira de pré-instalar pacotes para que nenhum trabalho precise ser feito se o pacote for encontrado nas pastas de fallback.</span><span class="sxs-lookup"><span data-stu-id="7eee3-243">*(3.5+)* Provides a way to preinstall packages so that no work needs to be done if the package is found in the fallback folders.</span></span> <span data-ttu-id="7eee3-244">As pastas de pacote de fallback têm exatamente a mesma estrutura de pasta e arquivo que a pasta de pacote global: *. nupkg* está presente e todos os arquivos são extraídos.</span><span class="sxs-lookup"><span data-stu-id="7eee3-244">Fallback package folders have the exact same folder and file structure as the global package folder: *.nupkg* is present, and all files are extracted.</span></span>

<span data-ttu-id="7eee3-245">A lógica de pesquisa para essa configuração é:</span><span class="sxs-lookup"><span data-stu-id="7eee3-245">The lookup logic for this configuration is:</span></span>

- <span data-ttu-id="7eee3-246">Procure na pasta de pacote global para ver se o pacote/versão já foi baixado.</span><span class="sxs-lookup"><span data-stu-id="7eee3-246">Look in global package folder to see if the package/version is already downloaded.</span></span>

- <span data-ttu-id="7eee3-247">Procure uma correspondência de pacote/versão nas pastas de fallback.</span><span class="sxs-lookup"><span data-stu-id="7eee3-247">Look in the fallback folders for a package/version match.</span></span>

<span data-ttu-id="7eee3-248">Se a pesquisa for bem-sucedida, nenhum download será necessário.</span><span class="sxs-lookup"><span data-stu-id="7eee3-248">If either lookup is successful, then no download is necessary.</span></span>

<span data-ttu-id="7eee3-249">Se uma correspondência não for encontrada, o NuGet verificará as fontes de arquivo e, em seguida, as fontes http e baixará os pacotes.</span><span class="sxs-lookup"><span data-stu-id="7eee3-249">If a match is not found, then NuGet checks file sources, and then http sources, and then it downloads the packages.</span></span>

| <span data-ttu-id="7eee3-250">Chave</span><span class="sxs-lookup"><span data-stu-id="7eee3-250">Key</span></span> | <span data-ttu-id="7eee3-251">Valor</span><span class="sxs-lookup"><span data-stu-id="7eee3-251">Value</span></span> |
| --- | --- |
| <span data-ttu-id="7eee3-252">(nome da pasta de fallback)</span><span class="sxs-lookup"><span data-stu-id="7eee3-252">(name of fallback folder)</span></span> | <span data-ttu-id="7eee3-253">Caminho para a pasta de fallback.</span><span class="sxs-lookup"><span data-stu-id="7eee3-253">Path to fallback folder.</span></span> |

<span data-ttu-id="7eee3-254">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="7eee3-254">**Example**:</span></span>

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a><span data-ttu-id="7eee3-255">seção packageManagement</span><span class="sxs-lookup"><span data-stu-id="7eee3-255">packageManagement section</span></span>

<span data-ttu-id="7eee3-256">Define o formato de gerenciamento de pacote padrão, *packages.config* ou PackageReference.</span><span class="sxs-lookup"><span data-stu-id="7eee3-256">Sets the default package management format, either *packages.config* or PackageReference.</span></span> <span data-ttu-id="7eee3-257">Projetos no estilo SDK sempre usam PackageReference.</span><span class="sxs-lookup"><span data-stu-id="7eee3-257">SDK-style projects always use PackageReference.</span></span>

| <span data-ttu-id="7eee3-258">Chave</span><span class="sxs-lookup"><span data-stu-id="7eee3-258">Key</span></span> | <span data-ttu-id="7eee3-259">Valor</span><span class="sxs-lookup"><span data-stu-id="7eee3-259">Value</span></span> |
| --- | --- |
| <span data-ttu-id="7eee3-260">format</span><span class="sxs-lookup"><span data-stu-id="7eee3-260">format</span></span> | <span data-ttu-id="7eee3-261">Um booliano que indica o formato de gerenciamento de pacote padrão.</span><span class="sxs-lookup"><span data-stu-id="7eee3-261">A Boolean indicating the default package management format.</span></span> <span data-ttu-id="7eee3-262">Se `1` , Format for PackageReference.</span><span class="sxs-lookup"><span data-stu-id="7eee3-262">If `1`, format is PackageReference.</span></span> <span data-ttu-id="7eee3-263">Se `0` , o formato é *packages.config*.</span><span class="sxs-lookup"><span data-stu-id="7eee3-263">If `0`, format is *packages.config*.</span></span> |
| <span data-ttu-id="7eee3-264">desabilitado</span><span class="sxs-lookup"><span data-stu-id="7eee3-264">disabled</span></span> | <span data-ttu-id="7eee3-265">Um booliano que indica se o prompt deve ser mostrado para selecionar um formato de pacote padrão na instalação do primeiro pacote.</span><span class="sxs-lookup"><span data-stu-id="7eee3-265">A Boolean indicating whether to show the prompt to select a default package format on first package install.</span></span> <span data-ttu-id="7eee3-266">`False` oculta o prompt.</span><span class="sxs-lookup"><span data-stu-id="7eee3-266">`False` hides the prompt.</span></span> |

<span data-ttu-id="7eee3-267">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="7eee3-267">**Example**:</span></span>

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a><span data-ttu-id="7eee3-268">Usando variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="7eee3-268">Using environment variables</span></span>

<span data-ttu-id="7eee3-269">Você pode usar variáveis de ambiente em valores `nuget.config` (NuGet 3.4 ou superior) para aplicar as configurações no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="7eee3-269">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="7eee3-270">Por exemplo, se a variável de ambiente `HOME` no Windows for definida como `c:\users\username`, o valor de `%HOME%\NuGetRepository` no arquivo de configuração é resolvido para `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="7eee3-270">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="7eee3-271">Observe que você precisa usar variáveis de ambiente no estilo do Windows (começa e termina com%) mesmo no Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="7eee3-271">Note that you have to use Windows-style environment variables (starts and ends with %) even on Mac/Linux.</span></span> <span data-ttu-id="7eee3-272">Ter `$HOME/NuGetRepository` em um arquivo de configuração não será resolvido.</span><span class="sxs-lookup"><span data-stu-id="7eee3-272">Having `$HOME/NuGetRepository` in a configuration file will not resolve.</span></span> <span data-ttu-id="7eee3-273">No Mac/Linux, o valor de `%HOME%/NuGetRepository` será resolvido para `/home/myStuff/NuGetRepository` .</span><span class="sxs-lookup"><span data-stu-id="7eee3-273">On Mac/Linux the value of `%HOME%/NuGetRepository` will resolve to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="7eee3-274">Se uma variável de ambiente não for encontrada, o NuGet usa o valor literal do arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="7eee3-274">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span> <span data-ttu-id="7eee3-275">Por exemplo, `%MY_UNDEFINED_VAR%/NuGetRepository` será resolvido como `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`</span><span class="sxs-lookup"><span data-stu-id="7eee3-275">For example `%MY_UNDEFINED_VAR%/NuGetRepository` will be resolved as `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`</span></span>

<span data-ttu-id="7eee3-276">A tabela abaixo mostra a sintaxe da variável ambiente e o suporte ao separador de caminho para arquivos de NuGet.Config.</span><span class="sxs-lookup"><span data-stu-id="7eee3-276">The table below show environnment variable syntax and path separator support for NuGet.Config files.</span></span>

### <a name="nugetconfig-environment-variable-support"></a><span data-ttu-id="7eee3-277">Suporte à variável de ambiente NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="7eee3-277">NuGet.Config environment variable support</span></span>

| <span data-ttu-id="7eee3-278">Syntax</span><span class="sxs-lookup"><span data-stu-id="7eee3-278">Syntax</span></span> | <span data-ttu-id="7eee3-279">Separador de dir</span><span class="sxs-lookup"><span data-stu-id="7eee3-279">Dir separator</span></span> | <span data-ttu-id="7eee3-280">nuget.exe do Windows</span><span class="sxs-lookup"><span data-stu-id="7eee3-280">Windows nuget.exe</span></span> | <span data-ttu-id="7eee3-281">dotnet.exe do Windows</span><span class="sxs-lookup"><span data-stu-id="7eee3-281">Windows dotnet.exe</span></span> | <span data-ttu-id="7eee3-282">nuget.exe do Mac (em mono)</span><span class="sxs-lookup"><span data-stu-id="7eee3-282">Mac nuget.exe (in Mono)</span></span> | <span data-ttu-id="7eee3-283">dotnet.exe Mac</span><span class="sxs-lookup"><span data-stu-id="7eee3-283">Mac dotnet.exe</span></span> |
|---|---|---|---|---|---|
| `%MY_VAR%` | `/`  | <span data-ttu-id="7eee3-284">Sim</span><span class="sxs-lookup"><span data-stu-id="7eee3-284">Yes</span></span> | <span data-ttu-id="7eee3-285">Sim</span><span class="sxs-lookup"><span data-stu-id="7eee3-285">Yes</span></span> | <span data-ttu-id="7eee3-286">Sim</span><span class="sxs-lookup"><span data-stu-id="7eee3-286">Yes</span></span> | <span data-ttu-id="7eee3-287">Sim</span><span class="sxs-lookup"><span data-stu-id="7eee3-287">Yes</span></span> |
| `%MY_VAR%` | `\`  | <span data-ttu-id="7eee3-288">Sim</span><span class="sxs-lookup"><span data-stu-id="7eee3-288">Yes</span></span> | <span data-ttu-id="7eee3-289">Sim</span><span class="sxs-lookup"><span data-stu-id="7eee3-289">Yes</span></span> | <span data-ttu-id="7eee3-290">Não</span><span class="sxs-lookup"><span data-stu-id="7eee3-290">No</span></span> | <span data-ttu-id="7eee3-291">Não</span><span class="sxs-lookup"><span data-stu-id="7eee3-291">No</span></span> |
| `$MY_VAR` | `/`  | <span data-ttu-id="7eee3-292">Não</span><span class="sxs-lookup"><span data-stu-id="7eee3-292">No</span></span> | <span data-ttu-id="7eee3-293">Não</span><span class="sxs-lookup"><span data-stu-id="7eee3-293">No</span></span> | <span data-ttu-id="7eee3-294">Não</span><span class="sxs-lookup"><span data-stu-id="7eee3-294">No</span></span> | <span data-ttu-id="7eee3-295">Não</span><span class="sxs-lookup"><span data-stu-id="7eee3-295">No</span></span> |
| `$MY_VAR` | `\`  | <span data-ttu-id="7eee3-296">Não</span><span class="sxs-lookup"><span data-stu-id="7eee3-296">No</span></span> | <span data-ttu-id="7eee3-297">Não</span><span class="sxs-lookup"><span data-stu-id="7eee3-297">No</span></span> | <span data-ttu-id="7eee3-298">Não</span><span class="sxs-lookup"><span data-stu-id="7eee3-298">No</span></span> | <span data-ttu-id="7eee3-299">Não</span><span class="sxs-lookup"><span data-stu-id="7eee3-299">No</span></span> |


## <a name="example-config-file"></a><span data-ttu-id="7eee3-300">Exemplo de arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="7eee3-300">Example config file</span></span>

<span data-ttu-id="7eee3-301">Abaixo está um `nuget.config` arquivo de exemplo que ilustra várias configurações, incluindo as opcionais:</span><span class="sxs-lookup"><span data-stu-id="7eee3-301">Below is an example `nuget.config` file that illustrates a number of settings including optional ones:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable.
            This syntax works on Windows/Mac/Linux
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%/External" />

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
            <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
