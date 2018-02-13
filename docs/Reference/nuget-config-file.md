---
title: "Referência do arquivo NuGet.Config | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referência do arquivo NuGet.Config incluindo as seções config, bindingRedirects, packageRestore, solution e packageSource."
keywords: "Arquivo NuGet.Config, referência de configuração do NuGet, opções de configuração do NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: df602cb561a19f0eac085695de80db1fbaa1a313
ms.sourcegitcommit: 33436d122873249dbb20616556cd8c6783f38909
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2018
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="63ae0-104">Referência do NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="63ae0-104">NuGet.Config reference</span></span>

<span data-ttu-id="63ae0-105">O comportamento do NuGet é controlado pelas configurações em diferentes arquivos `NuGet.Config` conforme descrito em [Configurando o comportamento de NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="63ae0-105">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="63ae0-106">`NuGet.Config` é um arquivo XML que contém um nó `<configuration>` de nível superior, o qual contém os elementos da seção descritos neste tópico.</span><span class="sxs-lookup"><span data-stu-id="63ae0-106">`NuGet.Config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="63ae0-107">Cada seção contém zero ou mais elementos `<add>` com atributos `key` e `value`.</span><span class="sxs-lookup"><span data-stu-id="63ae0-107">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="63ae0-108">Consulte o [arquivo de configuração de exemplos](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="63ae0-108">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="63ae0-109">Nomes de configuração não diferenciam maiúsculas de minúsculas e podem usar valores [variáveis de ambiente](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="63ae0-109">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="63ae0-110">Neste tópico:</span><span class="sxs-lookup"><span data-stu-id="63ae0-110">In this topic:</span></span>

- [<span data-ttu-id="63ae0-111">seção de configuração</span><span class="sxs-lookup"><span data-stu-id="63ae0-111">config section</span></span>](#config-section)
- [<span data-ttu-id="63ae0-112">Seção bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="63ae0-112">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="63ae0-113">Seção packageRestore</span><span class="sxs-lookup"><span data-stu-id="63ae0-113">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="63ae0-114">solution section</span><span class="sxs-lookup"><span data-stu-id="63ae0-114">solution section</span></span>](#solution-section)
- <span data-ttu-id="63ae0-115">[Seções de origem de pacote](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="63ae0-115">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="63ae0-116">packageSources</span><span class="sxs-lookup"><span data-stu-id="63ae0-116">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="63ae0-117">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="63ae0-117">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="63ae0-118">apikeys</span><span class="sxs-lookup"><span data-stu-id="63ae0-118">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="63ae0-119">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="63ae0-119">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="63ae0-120">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="63ae0-120">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="63ae0-121">Usando variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="63ae0-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="63ae0-122">Exemplo de arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="63ae0-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="63ae0-123">seção de configuração</span><span class="sxs-lookup"><span data-stu-id="63ae0-123">config section</span></span>

<span data-ttu-id="63ae0-124">Contém diversas definições de configurações, que podem ser definidas usando o comando [`nuget config`](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="63ae0-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="63ae0-125">Observação: `dependencyVersion` e `repositoryPath` se aplicam apenas a projetos que usam `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="63ae0-125">Note: `dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="63ae0-126">`globalPackagesFolder` aplica-se somente a projetos usando o formato de PackageReference.</span><span class="sxs-lookup"><span data-stu-id="63ae0-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="63ae0-127">Chave</span><span class="sxs-lookup"><span data-stu-id="63ae0-127">Key</span></span> | <span data-ttu-id="63ae0-128">Valor</span><span class="sxs-lookup"><span data-stu-id="63ae0-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="63ae0-129">dependencyVersion (somente `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="63ae0-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="63ae0-130">O valor `DependencyVersion` padrão para a instalação, restauração e atualização do pacote, quando a opção `-DependencyVersion` não tiver sido especificada diretamente.</span><span class="sxs-lookup"><span data-stu-id="63ae0-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="63ae0-131">Esse valor também é usado pela interface do usuário do Gerenciador de Pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="63ae0-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="63ae0-132">Os valores são `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="63ae0-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="63ae0-133">globalPackagesFolder (projetos não usam `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="63ae0-133">globalPackagesFolder (projects not using `packages.config`)</span></span> | <span data-ttu-id="63ae0-134">O local da pasta de pacotes global padrão.</span><span class="sxs-lookup"><span data-stu-id="63ae0-134">The location of the default global packages folder.</span></span> <span data-ttu-id="63ae0-135">O padrão é `%USERPROFILE%\.nuget\packages` (Windows) ou `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="63ae0-135">The default is `%USERPROFILE%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="63ae0-136">Um caminho relativo pode ser usado em arquivos `Nuget.Config` específicos do projeto.</span><span class="sxs-lookup"><span data-stu-id="63ae0-136">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="63ae0-137">repositoryPath (somente `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="63ae0-137">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="63ae0-138">O local no qual instalar os pacotes do NuGet em vez da pasta `$(Solutiondir)/packages` padrão.</span><span class="sxs-lookup"><span data-stu-id="63ae0-138">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="63ae0-139">Um caminho relativo pode ser usado em arquivos `Nuget.Config` específicos do projeto.</span><span class="sxs-lookup"><span data-stu-id="63ae0-139">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="63ae0-140">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="63ae0-140">defaultPushSource</span></span> | <span data-ttu-id="63ae0-141">Identifica a URL ou o caminho da origem do pacote que deve ser usada como o padrão se nenhuma outra origem de pacote for encontrada para uma operação.</span><span class="sxs-lookup"><span data-stu-id="63ae0-141">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="63ae0-142">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="63ae0-142">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="63ae0-143">Configurações de proxy a serem usadas ao se conectar a origens de pacote; `http_proxy` deve estar no formato `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="63ae0-143">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="63ae0-144">As senhas são criptografadas e não podem ser adicionadas manualmente.</span><span class="sxs-lookup"><span data-stu-id="63ae0-144">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="63ae0-145">Para `no_proxy`, o valor é uma lista separada por vírgulas de domínios a ignorar no servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="63ae0-145">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="63ae0-146">Como alternativa, você pode usar as variáveis de ambiente http_proxy e no_proxy para esses valores.</span><span class="sxs-lookup"><span data-stu-id="63ae0-146">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="63ae0-147">Para ver detalhes adicionais, consulte [Configurações de proxy do NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="63ae0-147">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="63ae0-148">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="63ae0-148">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\repo" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="63ae0-149">Seção bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="63ae0-149">bindingRedirects section</span></span>

<span data-ttu-id="63ae0-150">Configura se o NuGet realiza redirecionamentos de associação automática quando um pacote é instalado.</span><span class="sxs-lookup"><span data-stu-id="63ae0-150">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="63ae0-151">Chave</span><span class="sxs-lookup"><span data-stu-id="63ae0-151">Key</span></span> | <span data-ttu-id="63ae0-152">Valor</span><span class="sxs-lookup"><span data-stu-id="63ae0-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="63ae0-153">skip</span><span class="sxs-lookup"><span data-stu-id="63ae0-153">skip</span></span> | <span data-ttu-id="63ae0-154">Um valor booliano que indica se os redirecionamentos de associação automática devem ser ignorados.</span><span class="sxs-lookup"><span data-stu-id="63ae0-154">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="63ae0-155">O padrão é falso.</span><span class="sxs-lookup"><span data-stu-id="63ae0-155">The default is false.</span></span> |

<span data-ttu-id="63ae0-156">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="63ae0-156">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="63ae0-157">Seção packageRestore</span><span class="sxs-lookup"><span data-stu-id="63ae0-157">packageRestore section</span></span>

<span data-ttu-id="63ae0-158">*Ignorado no 2.7 ou superior*</span><span class="sxs-lookup"><span data-stu-id="63ae0-158">*Ignored in 2.7+*</span></span>

<span data-ttu-id="63ae0-159">Controla a restauração de pacote durante builds.</span><span class="sxs-lookup"><span data-stu-id="63ae0-159">Controls package restore during builds.</span></span>

| <span data-ttu-id="63ae0-160">Chave</span><span class="sxs-lookup"><span data-stu-id="63ae0-160">Key</span></span> | <span data-ttu-id="63ae0-161">Valor</span><span class="sxs-lookup"><span data-stu-id="63ae0-161">Value</span></span> |
| --- | --- |
| <span data-ttu-id="63ae0-162">habilitado</span><span class="sxs-lookup"><span data-stu-id="63ae0-162">enabled</span></span> | <span data-ttu-id="63ae0-163">Um valor booliano que indica se o NuGet pode executar uma restauração automática.</span><span class="sxs-lookup"><span data-stu-id="63ae0-163">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="63ae0-164">Você também pode definir a variável de ambiente `EnableNuGetPackageRestore` com um valor de `True` em vez de configurar essa chave no arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="63ae0-164">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="63ae0-165">automático</span><span class="sxs-lookup"><span data-stu-id="63ae0-165">automatic</span></span> | <span data-ttu-id="63ae0-166">Um valor booliano que indica se o NuGet deve verificar se há pacotes ausentes durante um build.</span><span class="sxs-lookup"><span data-stu-id="63ae0-166">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="63ae0-167">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="63ae0-167">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="63ae0-168">solution section</span><span class="sxs-lookup"><span data-stu-id="63ae0-168">solution section</span></span>

<span data-ttu-id="63ae0-169">Controla se a pasta `packages` de uma solução está incluída no controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="63ae0-169">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="63ae0-170">Esta seção funciona somente em arquivos `Nuget.Config` em uma pasta de solução.</span><span class="sxs-lookup"><span data-stu-id="63ae0-170">This section works only in `Nuget.Config` files in a solution folder.</span></span>

| <span data-ttu-id="63ae0-171">Chave</span><span class="sxs-lookup"><span data-stu-id="63ae0-171">Key</span></span> | <span data-ttu-id="63ae0-172">Valor</span><span class="sxs-lookup"><span data-stu-id="63ae0-172">Value</span></span> |
| --- | --- |
| <span data-ttu-id="63ae0-173">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="63ae0-173">disableSourceControlIntegration</span></span> | <span data-ttu-id="63ae0-174">Um booliano que indica se a pasta de pacotes deve ser ignorada ao trabalhar com o controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="63ae0-174">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="63ae0-175">O valor padrão é false.</span><span class="sxs-lookup"><span data-stu-id="63ae0-175">The default value is false.</span></span> |

<span data-ttu-id="63ae0-176">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="63ae0-176">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="63ae0-177">Seções de origem de pacote</span><span class="sxs-lookup"><span data-stu-id="63ae0-177">Package source sections</span></span>

<span data-ttu-id="63ae0-178">O `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource` e `disabledPackageSources` trabalham todos juntos para configurar como o NuGet funciona com repositórios de pacote durante as operações de instalação, restauração e atualização.</span><span class="sxs-lookup"><span data-stu-id="63ae0-178">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="63ae0-179">O [`nuget sources` comando ](../tools/cli-ref-sources.md) geralmente é usado para gerenciar essas configurações, exceto para `apikeys`, que é gerenciado usando o [`nuget setapikey`comando ](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="63ae0-179">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="63ae0-180">Observe que a URL de origem para nuget.org é `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="63ae0-180">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="63ae0-181">packageSources</span><span class="sxs-lookup"><span data-stu-id="63ae0-181">packageSources</span></span>

<span data-ttu-id="63ae0-182">Lista todas as origens de pacotes conhecidas.</span><span class="sxs-lookup"><span data-stu-id="63ae0-182">Lists all known package sources.</span></span> <span data-ttu-id="63ae0-183">A ordem é ignorada durante operações de restauração e com qualquer projeto usando o formato de PackageReference.</span><span class="sxs-lookup"><span data-stu-id="63ae0-183">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="63ae0-184">NuGet respeita a ordem das fontes para instalar e atualizar as operações com projetos usando `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="63ae0-184">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="63ae0-185">Chave</span><span class="sxs-lookup"><span data-stu-id="63ae0-185">Key</span></span> | <span data-ttu-id="63ae0-186">Valor</span><span class="sxs-lookup"><span data-stu-id="63ae0-186">Value</span></span> |
| --- | --- |
| <span data-ttu-id="63ae0-187">(nome a ser atribuído à origem do pacote)</span><span class="sxs-lookup"><span data-stu-id="63ae0-187">(name to assign to the package source)</span></span> | <span data-ttu-id="63ae0-188">O caminho ou URL da origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="63ae0-188">The path or URL of the package source.</span></span> |

<span data-ttu-id="63ae0-189">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="63ae0-189">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="63ae0-190">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="63ae0-190">packageSourceCredentials</span></span>

<span data-ttu-id="63ae0-191">Armazena os nomes de usuário e senhas para as origens, geralmente especificado com as opções `-username` e `-password` com `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="63ae0-191">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="63ae0-192">As senhas são criptografadas por padrão, a menos que a opção `-storepasswordincleartext` também seja usada.</span><span class="sxs-lookup"><span data-stu-id="63ae0-192">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="63ae0-193">Chave</span><span class="sxs-lookup"><span data-stu-id="63ae0-193">Key</span></span> | <span data-ttu-id="63ae0-194">Valor</span><span class="sxs-lookup"><span data-stu-id="63ae0-194">Value</span></span> |
| --- | --- |
| <span data-ttu-id="63ae0-195">username</span><span class="sxs-lookup"><span data-stu-id="63ae0-195">username</span></span> | <span data-ttu-id="63ae0-196">O nome de usuário para a origem em texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="63ae0-196">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="63ae0-197">password</span><span class="sxs-lookup"><span data-stu-id="63ae0-197">password</span></span> | <span data-ttu-id="63ae0-198">A senha criptografada para a origem.</span><span class="sxs-lookup"><span data-stu-id="63ae0-198">The encrypted password for the source.</span></span> |
| <span data-ttu-id="63ae0-199">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="63ae0-199">cleartextpassword</span></span> | <span data-ttu-id="63ae0-200">A senha não criptografada para a origem.</span><span class="sxs-lookup"><span data-stu-id="63ae0-200">The unencrypted password for the source.</span></span> |

<span data-ttu-id="63ae0-201">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="63ae0-201">**Example:**</span></span>

<span data-ttu-id="63ae0-202">No arquivo de configuração, o elemento `<packageSourceCredentials>` contém nós filho para cada nome de origem aplicável (espaços no nome serão substituídos por `_x0020+`).</span><span class="sxs-lookup"><span data-stu-id="63ae0-202">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020+`).</span></span> <span data-ttu-id="63ae0-203">Ou seja, para origens chamadas “Contoso” e “Origem de teste”, o arquivo de configuração contém o seguinte ao usar senhas criptografadas:</span><span class="sxs-lookup"><span data-stu-id="63ae0-203">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="63ae0-204">Ao usar senhas não criptografadas:</span><span class="sxs-lookup"><span data-stu-id="63ae0-204">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="63ae0-205">apikeys</span><span class="sxs-lookup"><span data-stu-id="63ae0-205">apikeys</span></span>

<span data-ttu-id="63ae0-206">Armazena as chaves de origens que usam autenticação de chave de API, conforme definido com o comando [`nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="63ae0-206">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="63ae0-207">Chave</span><span class="sxs-lookup"><span data-stu-id="63ae0-207">Key</span></span> | <span data-ttu-id="63ae0-208">Valor</span><span class="sxs-lookup"><span data-stu-id="63ae0-208">Value</span></span> |
| --- | --- |
| <span data-ttu-id="63ae0-209">(URL de origem)</span><span class="sxs-lookup"><span data-stu-id="63ae0-209">(source URL)</span></span> | <span data-ttu-id="63ae0-210">A chave de API criptografada.</span><span class="sxs-lookup"><span data-stu-id="63ae0-210">The encrypted API key.</span></span> |

<span data-ttu-id="63ae0-211">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="63ae0-211">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="63ae0-212">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="63ae0-212">disabledPackageSources</span></span>

<span data-ttu-id="63ae0-213">Identificar fontes desabilitadas no momento.</span><span class="sxs-lookup"><span data-stu-id="63ae0-213">Identified currently disabled sources.</span></span> <span data-ttu-id="63ae0-214">Pode ficar em branco.</span><span class="sxs-lookup"><span data-stu-id="63ae0-214">May be empty.</span></span>

| <span data-ttu-id="63ae0-215">Chave</span><span class="sxs-lookup"><span data-stu-id="63ae0-215">Key</span></span> | <span data-ttu-id="63ae0-216">Valor</span><span class="sxs-lookup"><span data-stu-id="63ae0-216">Value</span></span> |
| --- | --- |
| <span data-ttu-id="63ae0-217">(nome da origem)</span><span class="sxs-lookup"><span data-stu-id="63ae0-217">(name of source)</span></span> | <span data-ttu-id="63ae0-218">Um valor booliano que indica se a origem está desabilitada.</span><span class="sxs-lookup"><span data-stu-id="63ae0-218">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="63ae0-219">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="63ae0-219">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="63ae0-220">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="63ae0-220">activePackageSource</span></span>

<span data-ttu-id="63ae0-221">*(somente 2.x; preterido no 3.x ou superior)*</span><span class="sxs-lookup"><span data-stu-id="63ae0-221">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="63ae0-222">Identifica a fonte ativa no momento ou indica a agregação de todas as fontes.</span><span class="sxs-lookup"><span data-stu-id="63ae0-222">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="63ae0-223">Chave</span><span class="sxs-lookup"><span data-stu-id="63ae0-223">Key</span></span> | <span data-ttu-id="63ae0-224">Valor</span><span class="sxs-lookup"><span data-stu-id="63ae0-224">Value</span></span> |
| --- | --- |
| <span data-ttu-id="63ae0-225">(nome da origem) ou `All`</span><span class="sxs-lookup"><span data-stu-id="63ae0-225">(name of source) or `All`</span></span> | <span data-ttu-id="63ae0-226">Se a chave é o nome de uma fonte, o valor é o caminho ou URL da origem.</span><span class="sxs-lookup"><span data-stu-id="63ae0-226">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="63ae0-227">Se `All`, o valor deve ser `(Aggregate source)` para combinar todas as origens de pacote que não foram desabilitadas.</span><span class="sxs-lookup"><span data-stu-id="63ae0-227">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="63ae0-228">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="63ae0-228">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="63ae0-229">Usando variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="63ae0-229">Using environment variables</span></span>

<span data-ttu-id="63ae0-230">Você pode usar variáveis de ambiente em valores `NuGet.Config` (NuGet 3.4 ou superior) para aplicar as configurações no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="63ae0-230">You can use environment variables in `NuGet.Config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="63ae0-231">Por exemplo, se a variável de ambiente `HOME` no Windows for definida como `c:\users\username`, o valor de `%HOME%\NuGetRepository` no arquivo de configuração é resolvido para `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="63ae0-231">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="63ae0-232">Da mesma forma, se o `HOME` no Mac/Linux for definido como `/home/myStuff`, `$HOME/NuGetRepository` no arquivo de configuração será resolvido para `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="63ae0-232">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `$HOME/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="63ae0-233">Se uma variável de ambiente não for encontrada, o NuGet usa o valor literal do arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="63ae0-233">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="63ae0-234">Exemplo de arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="63ae0-234">Example config file</span></span>

<span data-ttu-id="63ae0-235">Abaixo está um arquivo `NuGet.Config` de exemplo que ilustra diversas configurações:</span><span class="sxs-lookup"><span data-stu-id="63ae0-235">Below is an example `NuGet.Config` file that illustrates a number of settings:</span></span>

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
</configuration>
```
