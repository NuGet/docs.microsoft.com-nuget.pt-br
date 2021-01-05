---
title: API do NuGet no Visual Studio
description: Referência da interface para a API que o NuGet exporta pelo Managed Extensibility Framework no Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: 3592280d5398e13e71403023fbb361b5e26e7786
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699874"
---
# <a name="nuget-api-in-visual-studio"></a><span data-ttu-id="2101f-103">API do NuGet no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2101f-103">NuGet API in Visual Studio</span></span>

<span data-ttu-id="2101f-104">Além da interface do usuário e o Console do Gerenciador de Pacotes no Visual Studio, o NuGet também exporta alguns serviços úteis por meio do [MEF (Managed Extensibility Framework)](/dotnet/framework/mef/index).</span><span class="sxs-lookup"><span data-stu-id="2101f-104">In addition to the Package Manager UI and Console in Visual Studio, NuGet also exports some useful services through the [Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index).</span></span> <span data-ttu-id="2101f-105">Essa interface permite que outros componentes no Visual Studio interajam com o NuGet, que pode ser usado para instalar e desinstalar pacotes e para obter informações sobre os pacotes instalados.</span><span class="sxs-lookup"><span data-stu-id="2101f-105">This interface allows other components in Visual Studio to interact with NuGet, which can be used to install and uninstall packages, and to obtain information about installed packages.</span></span>

<span data-ttu-id="2101f-106">Ao longo dos anos, o NuGet adicionou muitos serviços que residem no `NuGet.VisualStudio` namespace no `NuGet.VisualStudio.dll` assembly:</span><span class="sxs-lookup"><span data-stu-id="2101f-106">Over the years, NuGet has added many services all of which reside in the `NuGet.VisualStudio` namespace in the `NuGet.VisualStudio.dll` assembly:</span></span>

<span data-ttu-id="2101f-107">A partir do NuGet 3.3 +, o NuGet exporta o seguinte</span><span class="sxs-lookup"><span data-stu-id="2101f-107">As of NuGet 3.3+, NuGet exports the following</span></span>

- <span data-ttu-id="2101f-108">[`IRegistryKey`](#iregistrykey-interface): Método para recuperar um valor de uma subchave do registro.</span><span class="sxs-lookup"><span data-stu-id="2101f-108">[`IRegistryKey`](#iregistrykey-interface): Method to retrieve a value from a registry subkey.</span></span> <span data-ttu-id="2101f-109">(3.3 +)</span><span class="sxs-lookup"><span data-stu-id="2101f-109">(3.3+)</span></span>
- <span data-ttu-id="2101f-110">[`IVsCredentialProvider`](#ivscredentialprovider-interface) Contém métodos para obter credenciais para operações do NuGet.</span><span class="sxs-lookup"><span data-stu-id="2101f-110">[`IVsCredentialProvider`](#ivscredentialprovider-interface) Contains methods to get credentials for NuGet operations.</span></span> <span data-ttu-id="2101f-111">(4.0 +)</span><span class="sxs-lookup"><span data-stu-id="2101f-111">(4.0+)</span></span>
- <span data-ttu-id="2101f-112">[`IVsFrameworkCompatibility`](#ivsframeworkcompatibility-interface) Contém métodos para descobrir estruturas e compatibilidade entre estruturas.</span><span class="sxs-lookup"><span data-stu-id="2101f-112">[`IVsFrameworkCompatibility`](#ivsframeworkcompatibility-interface) Contains methods to discover frameworks and compatibility between frameworks.</span></span> <span data-ttu-id="2101f-113">(4.0 +)</span><span class="sxs-lookup"><span data-stu-id="2101f-113">(4.0+)</span></span>
- <span data-ttu-id="2101f-114">[`IVsFrameworkCompatibility2`](#ivsframeworkcompatibility2-interface) Contém métodos para descobrir estruturas e compatibilidade entre estruturas.</span><span class="sxs-lookup"><span data-stu-id="2101f-114">[`IVsFrameworkCompatibility2`](#ivsframeworkcompatibility2-interface) Contains methods to discover frameworks and compatibility between frameworks.</span></span> <span data-ttu-id="2101f-115">(4.0 +)</span><span class="sxs-lookup"><span data-stu-id="2101f-115">(4.0+)</span></span>
- <span data-ttu-id="2101f-116">[`IVsFrameworkCompatibility3`](#ivsframeworkcompatibility3-interface) Contém métodos para descobrir estruturas e compatibilidade entre estruturas.</span><span class="sxs-lookup"><span data-stu-id="2101f-116">[`IVsFrameworkCompatibility3`](#ivsframeworkcompatibility3-interface) Contains methods to discover frameworks and compatibility between frameworks.</span></span> <span data-ttu-id="2101f-117">(5,8 +)</span><span class="sxs-lookup"><span data-stu-id="2101f-117">(5.8+)</span></span>
- <span data-ttu-id="2101f-118">[`IVsFrameworkParser`](#ivsframeworkparser-interface) Uma interface para lidar com a conversão entre cadeias de caracteres e [FrameworkName](/dotnet/api/system.runtime.versioning.frameworkname) (4.0 +)</span><span class="sxs-lookup"><span data-stu-id="2101f-118">[`IVsFrameworkParser`](#ivsframeworkparser-interface) An interface for dealing with the conversion between strings and [FrameworkName](/dotnet/api/system.runtime.versioning.frameworkname) (4.0+)</span></span>
- <span data-ttu-id="2101f-119">[`IVsFrameworkParser2`](#ivsframeworkparser2-interface) Uma interface para analisar .NET Framework cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="2101f-119">[`IVsFrameworkParser2`](#ivsframeworkparser2-interface) An interface to parse .NET Framework strings.</span></span> <span data-ttu-id="2101f-120">Consulte [NuGet-IVsFrameworkParser](https://aka.ms/NuGet-IVsFrameworkParser).</span><span class="sxs-lookup"><span data-stu-id="2101f-120">See [NuGet-IVsFrameworkParser](https://aka.ms/NuGet-IVsFrameworkParser).</span></span> <span data-ttu-id="2101f-121">(5,8 +)</span><span class="sxs-lookup"><span data-stu-id="2101f-121">(5.8+)</span></span>
- <span data-ttu-id="2101f-122">[`IVsGlobalPackagesInitScriptExecutor`](#ivsglobalpackagesinitscriptexecutor-interface) Executar scripts do PowerShell de pacotes em uma solução (4.0 +)</span><span class="sxs-lookup"><span data-stu-id="2101f-122">[`IVsGlobalPackagesInitScriptExecutor`](#ivsglobalpackagesinitscriptexecutor-interface) Execute powershell scripts from package(s) in a solution (4.0+)</span></span>
- <span data-ttu-id="2101f-123">[`IVsNuGetFramework`](#ivsnugetframework-interface) Um tipo que representa os componentes de um moniker da estrutura de destino .NET.</span><span class="sxs-lookup"><span data-stu-id="2101f-123">[`IVsNuGetFramework`](#ivsnugetframework-interface) A type that represents the components of a .NET Target Framework Moniker.</span></span> <span data-ttu-id="2101f-124">(5,8 +)</span><span class="sxs-lookup"><span data-stu-id="2101f-124">(5.8+)</span></span>
- <span data-ttu-id="2101f-125">[`IVsPackageInstaller`](#ivspackageinstaller-interface): Métodos para instalar pacotes NuGet em projetos.</span><span class="sxs-lookup"><span data-stu-id="2101f-125">[`IVsPackageInstaller`](#ivspackageinstaller-interface): Methods to install NuGet packages into projects.</span></span> <span data-ttu-id="2101f-126">(3.3 +)</span><span class="sxs-lookup"><span data-stu-id="2101f-126">(3.3+)</span></span>
- <span data-ttu-id="2101f-127">[' IVsPackageInstaller2](#ivspackageinstaller2-interface) Contém o método para instalar a versão mais recente de um único pacote em um projeto dentro da solução atual.</span><span class="sxs-lookup"><span data-stu-id="2101f-127">[\`IVsPackageInstaller2](#ivspackageinstaller2-interface) Contains method to install latest version of a single package into a project within the current solution.</span></span>
- <span data-ttu-id="2101f-128">[`IVsPackageInstallerEvents`](#ivspackageinstallerevents-interface): Eventos para instalação/desinstalação do pacote.</span><span class="sxs-lookup"><span data-stu-id="2101f-128">[`IVsPackageInstallerEvents`](#ivspackageinstallerevents-interface): Events for package install/uninstall.</span></span> <span data-ttu-id="2101f-129">(3.3 +)</span><span class="sxs-lookup"><span data-stu-id="2101f-129">(3.3+)</span></span>
- <span data-ttu-id="2101f-130">[`IVsPackageInstallerProjectEvents`](#ivspackageinstallerprojectevents-interface): Eventos em lote para instalação/desinstalação do pacote.</span><span class="sxs-lookup"><span data-stu-id="2101f-130">[`IVsPackageInstallerProjectEvents`](#ivspackageinstallerprojectevents-interface): Batch events for package install/uninstall.</span></span> <span data-ttu-id="2101f-131">(3.3 +)</span><span class="sxs-lookup"><span data-stu-id="2101f-131">(3.3+)</span></span>
- <span data-ttu-id="2101f-132">[`IVsPackageInstallerServices`](#ivspackageinstallerservices-interface): Métodos para recuperar os pacotes instalados na solução atual e verificar se um determinado pacote está instalado em um projeto.</span><span class="sxs-lookup"><span data-stu-id="2101f-132">[`IVsPackageInstallerServices`](#ivspackageinstallerservices-interface): Methods to retrieve installed packages in the current solution and to check whether a given package is installed in a project.</span></span> <span data-ttu-id="2101f-133">(3.3 +)</span><span class="sxs-lookup"><span data-stu-id="2101f-133">(3.3+)</span></span>
- <span data-ttu-id="2101f-134">[`IVsPackageManagerProvider`](#ivspackagemanagerprovider-interface): Métodos para fornecer sugestões de Gerenciador de pacotes alternativas para um pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="2101f-134">[`IVsPackageManagerProvider`](#ivspackagemanagerprovider-interface): Methods to provide alternative Package Manager suggestions for a NuGet package.</span></span> <span data-ttu-id="2101f-135">(3.3 +)</span><span class="sxs-lookup"><span data-stu-id="2101f-135">(3.3+)</span></span>
- <span data-ttu-id="2101f-136">[`IVsPackageMetadata`](#ivspackagemetadata-interface): Métodos para recuperar informações sobre um pacote instalado.</span><span class="sxs-lookup"><span data-stu-id="2101f-136">[`IVsPackageMetadata`](#ivspackagemetadata-interface): Methods to retrieve information about an installed package.</span></span> <span data-ttu-id="2101f-137">(3.3 +)</span><span class="sxs-lookup"><span data-stu-id="2101f-137">(3.3+)</span></span>
- <span data-ttu-id="2101f-138">[`IVsPackageProjectMetadata`](#ivspackageprojectmetadata-interface): Métodos para recuperar informações sobre um projeto em que as ações do NuGet estão sendo executadas.</span><span class="sxs-lookup"><span data-stu-id="2101f-138">[`IVsPackageProjectMetadata`](#ivspackageprojectmetadata-interface): Methods to retrieve information about a project where NuGet actions are being executed.</span></span> <span data-ttu-id="2101f-139">(3.3 +)</span><span class="sxs-lookup"><span data-stu-id="2101f-139">(3.3+)</span></span>
- <span data-ttu-id="2101f-140">[`IVsPackageRestorer`](#ivspackagerestorer-interface): Métodos para restaurar pacotes instalados em um projeto.</span><span class="sxs-lookup"><span data-stu-id="2101f-140">[`IVsPackageRestorer`](#ivspackagerestorer-interface): Methods to restore packages installed in a project.</span></span> <span data-ttu-id="2101f-141">(3.3 +)</span><span class="sxs-lookup"><span data-stu-id="2101f-141">(3.3+)</span></span>
- <span data-ttu-id="2101f-142">[`IVsPackageSourceProvider`](#ivspackagesourceprovider-interface): Métodos para recuperar uma lista de fontes de pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="2101f-142">[`IVsPackageSourceProvider`](#ivspackagesourceprovider-interface): Methods to retrieve a list of NuGet package sources.</span></span> <span data-ttu-id="2101f-143">(3.3 +)</span><span class="sxs-lookup"><span data-stu-id="2101f-143">(3.3+)</span></span>
- <span data-ttu-id="2101f-144">[`IVsPackageUninstaller`](#ivspackageuninstaller-interface): Métodos para desinstalar pacotes NuGet de projetos.</span><span class="sxs-lookup"><span data-stu-id="2101f-144">[`IVsPackageUninstaller`](#ivspackageuninstaller-interface): Methods to uninstall NuGet packages from projects.</span></span> <span data-ttu-id="2101f-145">(3.3 +)</span><span class="sxs-lookup"><span data-stu-id="2101f-145">(3.3+)</span></span>
- <span data-ttu-id="2101f-146">[`IVsPathContext`](#ivspathcontext-interface) Informações de caminho do NuGet específicas para o contexto atual (por exemplo, contexto do projeto).</span><span class="sxs-lookup"><span data-stu-id="2101f-146">[`IVsPathContext`](#ivspathcontext-interface) NuGet path information specific to the current context (e.g. project context).</span></span> <span data-ttu-id="2101f-147">(4.0 +)</span><span class="sxs-lookup"><span data-stu-id="2101f-147">(4.0+)</span></span>
- <span data-ttu-id="2101f-148">[`IVsPathContext2`](#ivspathcontext2-interface) Informações de caminho do NuGet específicas para o contexto atual (por exemplo, contexto do projeto).</span><span class="sxs-lookup"><span data-stu-id="2101f-148">[`IVsPathContext2`](#ivspathcontext2-interface) NuGet path information specific to the current context (e.g. project context).</span></span> <span data-ttu-id="2101f-149">(5.0 +)</span><span class="sxs-lookup"><span data-stu-id="2101f-149">(5.0+)</span></span>
- <span data-ttu-id="2101f-150">[`IVsPathContextProvider`](#ivspathcontextprovider-interface) Uma fábrica para inicializar instâncias de [IVsPathContext](#ivspathcontext-interface) .</span><span class="sxs-lookup"><span data-stu-id="2101f-150">[`IVsPathContextProvider`](#ivspathcontextprovider-interface) A factory to initialize [IVsPathContext](#ivspathcontext-interface) instances.</span></span> <span data-ttu-id="2101f-151">(4.0 +)</span><span class="sxs-lookup"><span data-stu-id="2101f-151">(4.0+)</span></span>
- <span data-ttu-id="2101f-152">[`IVsPathContextProvider2`](#ivspathcontextprovider2-interface) Uma fábrica para inicializar instâncias de [IVsPathContext2](#ivspathcontext2-interface) .</span><span class="sxs-lookup"><span data-stu-id="2101f-152">[`IVsPathContextProvider2`](#ivspathcontextprovider2-interface) A factory to initialize [IVsPathContext2](#ivspathcontext2-interface) instances.</span></span> <span data-ttu-id="2101f-153">(5.0 +)</span><span class="sxs-lookup"><span data-stu-id="2101f-153">(5.0+)</span></span>
- <span data-ttu-id="2101f-154">[`IVsProjectJsonToPackageReferenceMigrateResult`](#ivsprojectjsontopackagereferencemigrateresult-interface)  Contém o resultado da operação de migração em um project.jsherdado no projeto (4.3 +)</span><span class="sxs-lookup"><span data-stu-id="2101f-154">[`IVsProjectJsonToPackageReferenceMigrateResult`](#ivsprojectjsontopackagereferencemigrateresult-interface)  Contains the result of the migrate operation on a legacy project.json project (4.3+)</span></span>
- <span data-ttu-id="2101f-155">[`IVsProjectJsonToPackageReferenceMigrator`](#ivsprojectjsontopackagereferencemigrator-interface) Contém métodos para migrar um project.jsno projeto herdado baseado em um projeto baseado em PackageReference.</span><span class="sxs-lookup"><span data-stu-id="2101f-155">[`IVsProjectJsonToPackageReferenceMigrator`](#ivsprojectjsontopackagereferencemigrator-interface) Contains methods to migrate a project.json based legacy project to PackageReference based project.</span></span> <span data-ttu-id="2101f-156">(4.3 +)</span><span class="sxs-lookup"><span data-stu-id="2101f-156">(4.3+)</span></span>
- <span data-ttu-id="2101f-157">[`IVsSemanticVersionComparer`](#ivssemanticversioncomparer-interface) Uma interface para comparar duas cadeias de caracteres de versão opacas tratando-as como semântica NuGet (4.0 +)</span><span class="sxs-lookup"><span data-stu-id="2101f-157">[`IVsSemanticVersionComparer`](#ivssemanticversioncomparer-interface) An interface for comparing two opaque version strings by treating them as NuGet semantic (4.0+)</span></span>
- <span data-ttu-id="2101f-158">[`IVsTemplateWizard`](#ivstemplatewizard-interface): Projetado para modelos de projeto/item para incluir pacotes pré-instalados; Esta interface *não* deve ser invocada a partir do código e não tem métodos públicos.</span><span class="sxs-lookup"><span data-stu-id="2101f-158">[`IVsTemplateWizard`](#ivstemplatewizard-interface): Designed for project/item templates to include pre-installed packages; this interface is *not* meant to be invoked from code and has no public methods.</span></span> <span data-ttu-id="2101f-159">(3.3 +)</span><span class="sxs-lookup"><span data-stu-id="2101f-159">(3.3+)</span></span>

## <a name="using-nuget-services"></a><span data-ttu-id="2101f-160">Usando os serviços do NuGet</span><span class="sxs-lookup"><span data-stu-id="2101f-160">Using NuGet services</span></span>

1. <span data-ttu-id="2101f-161">Instale o [`NuGet.VisualStudio`](https://www.nuget.org/packages/NuGet.VisualStudio) pacote em seu projeto, que contém o `NuGet.VisualStudio.dll` assembly.</span><span class="sxs-lookup"><span data-stu-id="2101f-161">Install the [`NuGet.VisualStudio`](https://www.nuget.org/packages/NuGet.VisualStudio) package into your project, which contains the `NuGet.VisualStudio.dll` assembly.</span></span>

    <span data-ttu-id="2101f-162">Quando instalado, o pacote define automaticamente a propriedade dos **Tipos de Interoperabilidade Inseridos** da referência de assembly para **True**.</span><span class="sxs-lookup"><span data-stu-id="2101f-162">When installed, the package automatically sets the **Embed Interop Types** property of the assembly reference to **True**.</span></span> <span data-ttu-id="2101f-163">Isso torna o seu código resiliente contra alterações de versão quando os usuários atualizam para versões mais recentes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="2101f-163">This makes your code  resilient against version changes when users update to newer versions of NuGet.</span></span>

> [!Warning]
> <span data-ttu-id="2101f-164">Não use nenhum outro tipo além das interfaces públicas no seu código e não faça referência a outros assemblies NuGet, incluindo `NuGet.Core.dll`.</span><span class="sxs-lookup"><span data-stu-id="2101f-164">Do not use any other types besides the public interfaces in your code, and do not reference any other NuGet assemblies, including `NuGet.Core.dll`.</span></span>

1. <span data-ttu-id="2101f-165">Para usar um serviço, importe-o por meio do [atributo Import MEF](/dotnet/framework/mef/index#imports-and-exports-with-attributes) ou por meio do [serviço IComponentModel](/dotnet/api/microsoft.visualstudio.componentmodelhost.icomponentmodel).</span><span class="sxs-lookup"><span data-stu-id="2101f-165">To use a service, import it through the [MEF Import attribute](/dotnet/framework/mef/index#imports-and-exports-with-attributes), or through the [IComponentModel service](/dotnet/api/microsoft.visualstudio.componentmodelhost.icomponentmodel).</span></span>

    ```cs
    //Using the Import attribute
    [Import(typeof(IVsPackageInstaller2))]
    public IVsPackageInstaller2 packageInstaller;
    packageInstaller.InstallLatestPackage(null, currentProject,
        "Newtonsoft.Json", false, false);

    //Using the IComponentModel service
    var componentModel = (IComponentModel)GetService(typeof(SComponentModel));
    IVsPackageInstallerServices installerServices =
        componentModel.GetService<IVsPackageInstallerServices>();

    var installedPackages = installerServices.GetInstalledPackages();
    ```

<span data-ttu-id="2101f-166">Para referência, o código-fonte do NuGet.VisualStudio está contido dentro do [repositório NuGet.Clients](https://github.com/NuGet/NuGet.Client/tree/dev/src/NuGet.Clients/NuGet.VisualStudio).</span><span class="sxs-lookup"><span data-stu-id="2101f-166">For reference, the source code for NuGet.VisualStudio is contained within the [NuGet.Clients repository](https://github.com/NuGet/NuGet.Client/tree/dev/src/NuGet.Clients/NuGet.VisualStudio).</span></span>

## <a name="iregistrykey-interface"></a><span data-ttu-id="2101f-167">Interface IRegistryKey</span><span class="sxs-lookup"><span data-stu-id="2101f-167">IRegistryKey interface</span></span>

```cs
/// <summary>
/// Specifies methods for manipulating a key in the Windows registry.
/// </summary>
public interface IRegistryKey
    {
    /// <summary>
    /// Retrieves the specified subkey for read or read/write access.
    /// </summary>
    /// <param name="name">The name or path of the subkey to create or open.</param>
    /// <returns>The subkey requested, or null if the operation failed.</returns>
    IRegistryKey OpenSubKey(string name);


    /// <summary>
    /// Retrieves the value associated with the specified name.
    /// </summary>
    /// <param name="name">The name of the value to retrieve. This string is not case-sensitive.</param>
    /// <returns>The value associated with name, or null if name is not found.</returns>
    object GetValue(string name);


    /// <summary>
    /// Closes the key and flushes it to disk if its contents have been modified.
    /// </summary>
    void Close();
}
```

## <a name="ivscredentialprovider-interface"></a><span data-ttu-id="2101f-168">Interface IVsCredentialProvider</span><span class="sxs-lookup"><span data-stu-id="2101f-168">IVsCredentialProvider interface</span></span>

```cs
    /// <summary>
    /// Contains methods to get credentials for NuGet operations.
    /// </summary>
    public interface IVsCredentialProvider
    {
        /// <summary>
        /// Get credentials for the supplied package source Uri.
        /// </summary>
        /// <param name="uri">The NuGet package source Uri for which credentials are being requested. Implementors are
        /// expected to first determine if this is a package source for which they can supply credentials.
        /// If not, then Null should be returned.</param>
        /// <param name="proxy">Web proxy to use when comunicating on the network.  Null if there is no proxy
        /// authentication configured.</param>
        /// <param name="isProxyRequest">True if if this request is to get proxy authentication
        /// credentials. If the implementation is not valid for acquiring proxy credentials, then
        /// null should be returned.</param>
        /// <param name="isRetry">True if credentials were previously acquired for this uri, but
        /// the supplied credentials did not allow authorized access.</param>
        /// <param name="nonInteractive">If true, then interactive prompts must not be allowed.</param>
        /// <param name="cancellationToken">This cancellation token should be checked to determine if the
        /// operation requesting credentials has been cancelled.</param>
        /// <returns>Credentials acquired by this provider for the given package source uri.
        /// If the provider does not handle requests for the input parameter set, then null should be returned.
        /// If the provider does handle the request, but cannot supply credentials, an exception should be thrown.</returns>
        Task<ICredentials> GetCredentialsAsync(Uri uri,
            IWebProxy proxy,
            bool isProxyRequest,
            bool isRetry,
            bool nonInteractive,
            CancellationToken cancellationToken);
    }
```

## <a name="ivsframeworkcompatibility-interface"></a><span data-ttu-id="2101f-169">Interface IVsFrameworkCompatibility</span><span class="sxs-lookup"><span data-stu-id="2101f-169">IVsFrameworkCompatibility interface</span></span>

```cs
    /// <summary>
    /// Contains methods to discover frameworks and compatibility between frameworks.
    /// </summary>
    public interface IVsFrameworkCompatibility
    {
        /// <summary>
        /// Gets all .NETStandard frameworks currently supported, in ascending order by version.
        /// </summary>
        IEnumerable<FrameworkName> GetNetStandardFrameworks();

        /// <summary>
        /// Gets frameworks that support packages of the provided .NETStandard version.
        /// </summary>
        /// <remarks>
        /// The result list is not exhaustive as it is meant to human-readable. For example,
        /// equivalent frameworks are not returned. Additionally, a framework name with version X
        /// in the result implies that framework names with versions greater than or equal to X
        /// but having the same <see cref="FrameworkName.Identifier"/> are also supported.
        /// </remarks>
        /// <param name="frameworkName">The .NETStandard version to get supporting frameworks for.</param>
        IEnumerable<FrameworkName> GetFrameworksSupportingNetStandard(FrameworkName frameworkName);

        /// <summary>
        /// Selects the framework from <paramref name="frameworks"/> that is nearest
        /// to the <paramref name="targetFramework"/>, according to NuGet's framework
        /// compatibility rules. <c>null</c> is returned of none of the frameworks
        /// are compatible.
        /// </summary>
        /// <param name="targetFramework">The target framework.</param>
        /// <param name="frameworks">The list of frameworks to choose from.</param>
        /// <exception cref="ArgumentException">If any of the arguments are <c>null</c>.</exception>
        /// <returns>The nearest framework.</returns>
        FrameworkName GetNearest(FrameworkName targetFramework, IEnumerable<FrameworkName> frameworks);
    }
```

## <a name="ivsframeworkcompatibility2-interface"></a><span data-ttu-id="2101f-170">Interface IVsFrameworkCompatibility2</span><span class="sxs-lookup"><span data-stu-id="2101f-170">IVsFrameworkCompatibility2 interface</span></span>

```cs
    /// <summary>
    /// Gets all .NETStandard frameworks currently supported, in ascending order by version.
    /// </summary>
    public interface IVsFrameworkCompatibility2 : IVsFrameworkCompatibility
    {
        /// <summary>
        /// Selects the framework from <paramref name="frameworks"/> that is nearest
        /// to the <paramref name="targetFramework"/>, according to NuGet's framework
        /// compatibility rules. <c>null</c> is returned of none of the frameworks
        /// are compatible.
        /// </summary>
        /// <param name="targetFramework">The target framework.</param>
        /// <param name="fallbackTargetFrameworks">
        /// Target frameworks to use if the provided <paramref name="targetFramework"/> is not compatible.
        /// These fallback frameworks are attempted in sequence after <paramref name="targetFramework"/>.
        /// </param>
        /// <param name="frameworks">The list of frameworks to choose from.</param>
        /// <exception cref="ArgumentException">If any of the arguments are <c>null</c>.</exception>
        /// <returns>The nearest framework.</returns>
        FrameworkName GetNearest(
            FrameworkName targetFramework,
            IEnumerable<FrameworkName> fallbackTargetFrameworks,
            IEnumerable<FrameworkName> frameworks);
    }
```

## <a name="ivsframeworkcompatibility3-interface"></a><span data-ttu-id="2101f-171">Interface IVsFrameworkCompatibility3</span><span class="sxs-lookup"><span data-stu-id="2101f-171">IVsFrameworkCompatibility3 interface</span></span>

```cs
    /// <summary>
    /// Gets all .NETStandard frameworks currently supported, in ascending order by version.
    /// </summary>
    public interface IVsFrameworkCompatibility3
    {
        /// <summary>
        /// Selects the framework from <paramref name="frameworks"/> that is nearest
        /// to the <paramref name="targetFramework"/>, according to NuGet's framework
        /// compatibility rules. <c>null</c> is returned of none of the frameworks
        /// are compatible.
        /// </summary>
        /// <param name="targetFramework">The target framework.</param>
        /// <param name="frameworks">The list of frameworks to choose from.</param>
        /// <exception cref="ArgumentNullException">If any of the arguments are null.</exception>
        /// <exception cref="ArgumentException">If any of the frameworks cannot be parsed.</exception>
        /// <returns>The nearest framework.</returns>
        /// <remarks>This API is <a href="https://github.com/microsoft/vs-threading/blob/9f065f155525c4561257e02ad61e66e93e073886/doc/cookbook_vs.md#how-do-i-effectively-verify-that-my-code-is-fully-free-threaded">free-threaded</a>.</remarks>
        IVsNuGetFramework GetNearest(IVsNuGetFramework targetFramework, IEnumerable<IVsNuGetFramework> frameworks);

        /// <summary>
        /// Selects the framework from <paramref name="frameworks"/> that is nearest
        /// to the <paramref name="targetFramework"/>, according to NuGet's framework
        /// compatibility rules. <c>null</c> is returned of none of the frameworks
        /// are compatible.
        /// </summary>
        /// <param name="targetFramework">The target framework.</param>
        /// <param name="fallbackTargetFrameworks">
        /// Target frameworks to use if the provided <paramref name="targetFramework"/> is not compatible.
        /// These fallback frameworks are attempted in sequence after <paramref name="targetFramework"/>.
        /// </param>
        /// <param name="frameworks">The list of frameworks to choose from.</param>
        /// <exception cref="ArgumentNullException">If any of the arguments are null.</exception>
        /// <exception cref="ArgumentException">If any of the frameworkscannot be parsed.</exception>
        /// <returns>The nearest framework.</returns>
        /// <remarks>This API is <a href="https://github.com/microsoft/vs-threading/blob/9f065f155525c4561257e02ad61e66e93e073886/doc/cookbook_vs.md#how-do-i-effectively-verify-that-my-code-is-fully-free-threaded">free-threaded</a>.</remarks>
        IVsNuGetFramework GetNearest(
            IVsNuGetFramework targetFramework,
            IEnumerable<IVsNuGetFramework> fallbackTargetFrameworks,
            IEnumerable<IVsNuGetFramework> frameworks);
    }
```

## <a name="ivsframeworkparser-interface"></a><span data-ttu-id="2101f-172">Interface IVsFrameworkParser</span><span class="sxs-lookup"><span data-stu-id="2101f-172">IVsFrameworkParser interface</span></span>

```cs
    /// <summary>
    /// An interface for dealing with the conversion between strings and <see cref="FrameworkName"/>
    /// instances.
    /// </summary>
    public interface IVsFrameworkParser
    {
        /// <summary>
        /// Parses a short framework name (e.g. "net45") or a full framework name
        /// (e.g. ".NETFramework,Version=v4.5") into a <see cref="FrameworkName"/>
        /// instance.
        /// </summary>
        /// <param name="shortOrFullName">The framework string.</param>
        /// <exception cref="ArgumentNullException">If the provided string is null.</exception>
        /// <exception cref="ArgumentException">If the provided string cannot be parsed.</exception>
        /// <returns>The parsed framework.</returns>
        FrameworkName ParseFrameworkName(string shortOrFullName);

        /// <summary>
        /// Gets the shortened version of the framework name from a <see cref="FrameworkName"/>
        /// instance.
        /// </summary>
        /// <remarks>
        /// For example, ".NETFramework,Version=v4.5" is converted to "net45". This is the value
        /// used inside of .nupkg folder structures as well as in project.json files.
        /// </remarks>
        /// <param name="frameworkName">The framework name.</param>
        /// <exception cref="ArgumentNullException">If the input is null.</exception>
        /// <exception cref="ArgumentException">
        /// If the provided framework name cannot be converted to a short name.
        /// </exception>
        /// <returns>The short framework name. </returns>
        string GetShortFrameworkName(FrameworkName frameworkName);
    }
```

## <a name="ivsframeworkparser2-interface"></a><span data-ttu-id="2101f-173">Interface IVsFrameworkParser2</span><span class="sxs-lookup"><span data-stu-id="2101f-173">IVsFrameworkParser2 interface</span></span>

```cs
    /// <summary>An interface to parse .NET Framework strings. See <a href="http://aka.ms/NuGet-IVsFrameworkParser">http://aka.ms/NuGet-IVsFrameworkParser</a>.</summary>
    public interface IVsFrameworkParser2
    {
        /// <summary>
        /// Parses a short framework name (e.g. "net45") or a full Target Framework Moniker
        /// (e.g. ".NETFramework,Version=v4.5") into a <see cref="IVsNuGetFramework"/>
        /// instance.
        /// </summary>
        /// <param name="input">The framework string</param>
        /// <param name="nuGetFramework">The resulting <see cref="IVsNuGetFramework"/>. If the method returns false, this return NuGet's "Unsupported" framework details.</param>
        /// <returns>A boolean to specify whether the input could be parsed into a valid <see cref="IVsNuGetFramework"/> object.</returns>
        /// <remarks>This API is not needed to get framework information about loaded projects, and should not be used to parse the project's TargetFramework property. See <a href="http://aka.ms/NuGet-IVsFrameworkParser">http://aka.ms/NuGet-IVsFrameworkParser</a>.<br/>
        /// This API is <a href="https://github.com/microsoft/vs-threading/blob/9f065f155525c4561257e02ad61e66e93e073886/doc/cookbook_vs.md#how-do-i-effectively-verify-that-my-code-is-fully-free-threaded">free-threaded</a>.</remarks>
        bool TryParse(string input, out IVsNuGetFramework nuGetFramework);
    }
```

## <a name="ivsglobalpackagesinitscriptexecutor-interface"></a><span data-ttu-id="2101f-174">Interface IVsGlobalPackagesInitScriptExecutor</span><span class="sxs-lookup"><span data-stu-id="2101f-174">IVsGlobalPackagesInitScriptExecutor interface</span></span>

```cs
    /// <summary>
    /// Execute powershell scripts from package(s) in a solution
    /// </summary>
    /// <remarks>Intended for internal use only.</remarks>
    public interface IVsGlobalPackagesInitScriptExecutor
    {
        /// <summary>
        /// Executes the init script of the given package if available.
        /// 1) If the init.ps1 script has already been executed by the powershell host, it will not be executed again.
        /// True is returned.
        /// 2) If the package is found in the global packages folder it will be used.
        /// If not, it will return false and do nothing.
        /// 3) Also, note if other scripts are executing while this call was made, it will wait for them to complete.
        /// </summary>
        /// <param name="packageId">Id of the package whose init.ps1 will be executed.</param>
        /// <param name="packageVersion">Version of the package whose init.ps1 will be executed.</param>
        /// <returns>Returns true if the script was executed or has been executed already.</returns>
        /// <remarks>This method throws if the init.ps1 being executed throws.</remarks>
        Task<bool> ExecuteInitScriptAsync(string packageId, string packageVersion);
    }
```

## <a name="ivsnugetframework-interface"></a><span data-ttu-id="2101f-175">Interface IVsNuGetFramework</span><span class="sxs-lookup"><span data-stu-id="2101f-175">IVsNuGetFramework interface</span></span>

```cs
    /// <summary>A type that represents the components of a .NET Target Framework Moniker.</summary>
    /// <remarks><see cref="System.Runtime.Versioning.FrameworkName"/> does not support .NET 5 Target Framework Monikers with a platform, but this type does.</remarks>
    public interface IVsNuGetFramework
    {
        /// <summary>The framework moniker.</summary>
        string TargetFrameworkMoniker { get; }

        /// <summary>The platform moniker.</summary>
        string TargetPlatformMoniker { get; }

        /// <summary>The platform minimum version.</summary>
        /// <remarks>This property is read by <see cref="IVsFrameworkCompatibility3" />, but will always have a null value when returned from <see cref="IVsFrameworkParser2"/>.</remarks>
        string TargetPlatformMinVersion { get; }
    }
```

## <a name="ivspackageinstaller-interface"></a><span data-ttu-id="2101f-176">Interface IVsPackageInstaller</span><span class="sxs-lookup"><span data-stu-id="2101f-176">IVsPackageInstaller interface</span></span>

```cs
public interface IVsPackageInstaller
{
    /// <summary>
    /// Installs a single package from the specified package source.
    /// </summary>
    /// <param name="source">
    /// The package source to install the package from. This value can be <c>null</c>
    /// to indicate that the user's configured sources should be used. Otherwise,
    /// this should be the source path as a string. If the user has credentials
    /// configured for a source, this value must exactly match the configured source
    /// value.
    /// </param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageId">The package ID of the package to install.</param>
    /// <param name="version">
    /// The version of the package to install. <c>null</c> can be provided to
    /// install the latest version of the package.
    /// </param>
    /// <param name="ignoreDependencies">
    /// A boolean indicating whether or not to ignore the package's dependencies
    /// during installation.
    /// </param>
    void InstallPackage(string source, Project project, string packageId, Version version, bool ignoreDependencies);

    /// <summary>
    /// Installs a single package from the specified package source.
    /// </summary>
    /// <param name="source">
    /// The package source to install the package from. This value can be <c>null</c>
    /// to indicate that the user's configured sources should be used. Otherwise,
    /// this should be the source path as a string. If the user has credentials
    /// configured for a source, this value must exactly match the configured source
    /// value.
    /// </param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageId">The package ID of the package to install.</param>
    /// <param name="version">
    /// The version of the package to install. <c>null</c> can be provided to
    /// install the latest version of the package.
    /// </param>
    /// <param name="ignoreDependencies">
    /// A boolean indicating whether or not to ignore the package's dependencies
    /// during installation.
    /// </param>
    void InstallPackage(string source, Project project, string packageId, string version, bool ignoreDependencies);

    /// <summary>
    /// Installs a single package from the specified package source.
    /// </summary>
    /// <param name="repository">The package repository to install the package from.</param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageId">The package id of the package to install.</param>
    /// <param name="version">
    /// The version of the package to install. <c>null</c> can be provided to
    /// install the latest version of the package.
    /// </param>
    /// <param name="ignoreDependencies">
    /// A boolean indicating whether or not to ignore the package's dependencies
    /// during installation.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating if assembly references from the package should be
    /// skipped.
    /// </param>
    void InstallPackage(IPackageRepository repository, Project project, string packageId, string version, bool ignoreDependencies, bool skipAssemblyReferences);

    /// <summary>
    /// Installs one or more packages that exist on disk in a folder defined in the registry.
    /// </summary>
    /// <param name="keyName">
    /// The registry key name (under NuGet's repository key) that defines the folder on disk
    /// containing the packages.
    /// </param>
    /// <param name="isPreUnzipped">
    /// A boolean indicating whether the folder contains packages that are
    /// pre-unzipped.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating whether the assembly references from the packages
    /// should be skipped.
    /// </param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageVersions">
    /// A dictionary of packages/versions to install where the key is the package id
    /// and the value is the version.
    /// </param>
    /// <remarks>
    /// If any version of the package is already installed, no action will be taken.
    /// <para>
    /// Dependencies are always ignored.
    /// </para>
    /// </remarks>
    void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

    /// <summary>
    /// Installs one or more packages that exist on disk in a folder defined in the registry.
    /// </summary>
    /// <param name="keyName">
    /// The registry key name (under NuGet's repository key) that defines the folder on disk
    /// containing the packages.
    /// </param>
    /// <param name="isPreUnzipped">
    /// A boolean indicating whether the folder contains packages that are
    /// pre-unzipped.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating whether the assembly references from the packages
    /// should be skipped.
    /// </param>
    /// <param name="ignoreDependencies">A boolean indicating whether the package's dependencies should be ignored</param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageVersions">
    /// A dictionary of packages/versions to install where the key is the package id
    /// and the value is the version.
    /// </param>
    /// <remarks>
    /// If any version of the package is already installed, no action will be taken.
    /// </remarks>
    void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, bool ignoreDependencies, Project project, IDictionary<string, string> packageVersions);

    /// <summary>
    /// Installs one or more packages that are embedded in a Visual Studio Extension Package.
    /// </summary>
    /// <param name="extensionId">The Id of the Visual Studio Extension Package.</param>
    /// <param name="isPreUnzipped">
    /// A boolean indicating whether the folder contains packages that are
    /// pre-unzipped.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating whether the assembly references from the packages
    /// should be skipped.
    /// </param>
    /// <param name="project">The target project for package installation</param>
    /// <param name="packageVersions">
    /// A dictionary of packages/versions to install where the key is the package id
    /// and the value is the version.
    /// </param>
    /// <remarks>
    /// If any version of the package is already installed, no action will be taken.
    /// <para>
    /// Dependencies are always ignored.
    /// </para>
    /// </remarks>
    void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

    /// <summary>
    /// Installs one or more packages that are embedded in a Visual Studio Extension Package.
    /// </summary>
    /// <param name="extensionId">The Id of the Visual Studio Extension Package.</param>
    /// <param name="isPreUnzipped">
    /// A boolean indicating whether the folder contains packages that are
    /// pre-unzipped.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating whether the assembly references from the packages
    /// should be skipped.
    /// </param>
    /// <param name="ignoreDependencies">A boolean indicating whether the package's dependencies should be ignored</param>
    /// <param name="project">The target project for package installation</param>
    /// <param name="packageVersions">
    /// A dictionary of packages/versions to install where the key is the package id
    /// and the value is the version.
    /// </param>
    /// <remarks>
    /// If any version of the package is already installed, no action will be taken.
    /// </remarks>
    void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, bool ignoreDependencies, Project project, IDictionary<string, string> packageVersions);
}
```

## <a name="ivspackageinstaller2-interface"></a><span data-ttu-id="2101f-177">Interface IVsPackageinstaller2</span><span class="sxs-lookup"><span data-stu-id="2101f-177">IVsPackageinstaller2 interface</span></span>

```cs
   [Guid("4F3B122B-A53B-432C-8D85-0FAFB8BE4FF4")]
    public interface IVsPackageInstaller2 : IVsPackageInstaller
    {
        /// <summary>
        /// Installs the latest version of a single package from the specified package source.
        /// </summary>
        /// <param name="source">
        /// The package source to install the package from. This value can be <c>null</c>
        /// to indicate that the user's configured sources should be used. Otherwise,
        /// this should be the source path as a string. If the user has credentials
        /// configured for a source, this value must exactly match the configured source
        /// value.
        /// </param>
        /// <param name="project">The target project for package installation.</param>
        /// <param name="packageId">The package ID of the package to install.</param>
        /// <param name="includePrerelease">
        /// Whether or not to consider prerelease versions when finding the latest version
        /// to install.
        /// </param>
        /// <param name="ignoreDependencies">
        /// A boolean indicating whether or not to ignore the package's dependencies
        /// during installation.
        /// </param>
        /// <exception cref="InvalidOperationException">
        /// Thrown when <see paramref="includePrerelease"/> is <c>false</c> and no stable version
        /// of the package exists.
        /// </exception>
        void InstallLatestPackage(
            string source,
            Project project,
            string packageId,
            bool includePrerelease,
            bool ignoreDependencies);
    }
```

## <a name="ivspackageinstallerevents-interface"></a><span data-ttu-id="2101f-178">Interface IVsPackageInstallerEvents</span><span class="sxs-lookup"><span data-stu-id="2101f-178">IVsPackageInstallerEvents interface</span></span>

```cs
public interface IVsPackageInstallerEvents
{
    /// <summary>
    /// Raised when a package is about to be installed into the current solution.
    /// </summary>
    event VsPackageEventHandler PackageInstalling;

    /// <summary>
    /// Raised after a package has been installed into the current solution.
    /// </summary>
    event VsPackageEventHandler PackageInstalled;

    /// <summary>
    /// Raised when a package is about to be uninstalled from the current solution.
    /// </summary>
    event VsPackageEventHandler PackageUninstalling;

    /// <summary>
    /// Raised after a package has been uninstalled from the current solution.
    /// </summary>
    event VsPackageEventHandler PackageUninstalled;

    /// <summary>
    /// Raised after a package has been installed into a project within the current solution.
    /// </summary>
    event VsPackageEventHandler PackageReferenceAdded;

    /// <summary>
    /// Raised after a package has been uninstalled from a project within the current solution.
    /// </summary>
    event VsPackageEventHandler PackageReferenceRemoved;
}
```

## <a name="ivspackageinstallerprojectevents-interface"></a><span data-ttu-id="2101f-179">Interface IVsPackageInstallerProjectEvents</span><span class="sxs-lookup"><span data-stu-id="2101f-179">IVsPackageInstallerProjectEvents interface</span></span>

```cs
public interface IVsPackageInstallerProjectEvents
{
    /// <summary>
    /// Raised before any IVsPackageInstallerEvents events are raised for a project.
    /// </summary>
    event VsPackageProjectEventHandler BatchStart;

    /// <summary>
    /// Raised after all IVsPackageInstallerEvents events are raised for a project.
    /// </summary>
    event VsPackageProjectEventHandler BatchEnd;
}
```

## <a name="ivspackageinstallerservices-interface"></a><span data-ttu-id="2101f-180">Interface IVsPackageInstallerServices</span><span class="sxs-lookup"><span data-stu-id="2101f-180">IVsPackageInstallerServices interface</span></span>

```cs
public interface IVsPackageInstallerServices
{
    // IMPORTANT: do NOT rearrange the methods here. The order is important to maintain
    // backwards compatibility with clients that were compiled against old versions of NuGet.

    /// <summary>
    /// Get the list of NuGet packages installed in the current solution.
    /// </summary>
    IEnumerable<IVsPackageMetadata> GetInstalledPackages();

    /// <summary>
    /// Checks if a NuGet package with the specified Id is installed in the specified project.
    /// </summary>
    /// <param name="project">The project to check for NuGet package.</param>
    /// <param name="id">The id of the package to check.</param>
    /// <returns><c>true</c> if the package is install. <c>false</c> otherwise.</returns>
    bool IsPackageInstalled(Project project, string id);

    /// <summary>
    /// Checks if a NuGet package with the specified Id and version is installed in the specified project.
    /// </summary>
    /// <param name="project">The project to check for NuGet package.</param>
    /// <param name="id">The id of the package to check.</param>
    /// <param name="version">The version of the package to check.</param>
    /// <returns><c>true</c> if the package is install. <c>false</c> otherwise.</returns>
    bool IsPackageInstalled(Project project, string id, SemanticVersion version);

    /// <summary>
    /// Checks if a NuGet package with the specified Id and version is installed in the specified project.
    /// </summary>
    /// <param name="project">The project to check for NuGet package.</param>
    /// <param name="id">The id of the package to check.</param>
    /// <param name="versionString">The version of the package to check.</param>
    /// <returns><c>true</c> if the package is install. <c>false</c> otherwise.</returns>
    /// <remarks>
    /// The reason this method is named IsPackageInstalledEx, instead of IsPackageInstalled, is that
    /// when client project compiles against this assembly, the compiler would attempt to bind against
    /// the other overload which accepts SemanticVersion and would require client project to reference NuGet.Core.
    /// </remarks>
    bool IsPackageInstalledEx(Project project, string id, string versionString);

    /// <summary>
    /// Get the list of NuGet packages installed in the specified project.
    /// </summary>
    /// <param name="project">The project to get NuGet packages from.</param>
    IEnumerable<IVsPackageMetadata> GetInstalledPackages(Project project);
}
```

## <a name="ivspackagemanagerprovider-interface"></a><span data-ttu-id="2101f-181">Interface IVsPackageManagerProvider</span><span class="sxs-lookup"><span data-stu-id="2101f-181">IVsPackageManagerProvider interface</span></span>

```cs
public interface IVsPackageManagerProvider
{
    /// <summary>
    /// Localized display package manager name.
    /// </summary>
    string PackageManagerName { get; }

    /// <summary>
    /// Package manager unique id.
    /// </summary>
    string PackageManagerId { get; }

    /// <summary>
    /// The tool tip description for the package
    /// </summary>
    string Description { get; }

    /// <summary>
    /// Check if a recommendation should be surfaced for an alternate package manager.
    /// This code should not rely on slow network calls, and should return rapidly.
    /// </summary>
    /// <param name="packageId">Current package id</param>
    /// <param name="projectName">Unique project name for finding the project through VS dte</param>
    /// <param name="token">Cancellation Token</param>
    /// <returns>return true if need to direct to integrated package manager for this package</returns>
    Task<bool> CheckForPackageAsync(string packageId, string projectName, CancellationToken token);

    /// <summary>
    /// This Action should take the user to the other package manager.
    /// </summary>
    /// <param name="packageId">Current package id</param>
    /// <param name="projectName">Unique project name for finding the project through VS dte</param>
    void GoToPackage(string packageId, string projectName);
}
```

## <a name="ivspackagemetadata-interface"></a><span data-ttu-id="2101f-182">Interface IVsPackageMetadata</span><span class="sxs-lookup"><span data-stu-id="2101f-182">IVsPackageMetadata interface</span></span>

```cs
public interface IVsPackageMetadata
{
    /// <summary>
    /// Id of the package.
    /// </summary>
    string Id { get; }

    /// <summary>
    /// Version of the package.
    /// </summary>
    /// <remarks>
    /// Do not use this property because it will require referencing NuGet.Core.dll assembly. Use the VersionString
    /// property instead.
    /// </remarks>
    [Obsolete("Do not use this property because it will require referencing NuGet.Core.dll assembly. Use the VersionString property instead.")]
    NuGet.SemanticVersion Version { get; }

    /// <summary>
    /// Title of the package.
    /// </summary>
    string Title { get; }

    /// <summary>
    /// Description of the package.
    /// </summary>
    string Description { get; }

    /// <summary>
    /// The authors of the package.
    /// </summary>
    IEnumerable<string> Authors { get; }

    /// <summary>
    /// The location where the package is installed on disk.
    /// </summary>
    string InstallPath { get; }

    // IMPORTANT: This property must come LAST, because it was added in 2.5. Having it declared
    // LAST will avoid breaking components that compiled against earlier versions which doesn't
    // have this property.
    /// <summary>
    /// The version of the package.
    /// </summary>
    /// <remarks>
    /// Use this property instead of the Version property becase with the type string,
    /// it doesn't require referencing NuGet.Core.dll assembly.
    /// </remarks>
    string VersionString { get; }
}
```

## <a name="ivspackageprojectmetadata-interface"></a><span data-ttu-id="2101f-183">Interface IVsPackageProjectMetadata</span><span class="sxs-lookup"><span data-stu-id="2101f-183">IVsPackageProjectMetadata interface</span></span>

```cs
public interface IVsPackageProjectMetadata
{
    /// <summary>
    /// Unique batch id for batch start/end events of the project.
    /// </summary>
    string BatchId { get; }

    /// <summary>
    /// Name of the project.
    /// </summary>
    string ProjectName { get; }
}
```

## <a name="ivspackagerestorer-interface"></a><span data-ttu-id="2101f-184">Interface IVsPackageRestorer</span><span class="sxs-lookup"><span data-stu-id="2101f-184">IVsPackageRestorer interface</span></span>

```cs
public interface IVsPackageRestorer
{
    /// <summary>
    /// Returns a value indicating whether the user consent to download NuGet packages
    /// has been granted.
    /// </summary>
    /// <returns>true if the user consent has been granted; otherwise, false.</returns>
    bool IsUserConsentGranted();

    /// <summary>
    /// Restores NuGet packages installed in the given project within the current solution.
    /// </summary>
    /// <param name="project">The project whose NuGet packages to restore.</param>
    void RestorePackages(Project project);
}
```

## <a name="ivspackagesourceprovider-interface"></a><span data-ttu-id="2101f-185">Interface IVsPackageSourceProvider</span><span class="sxs-lookup"><span data-stu-id="2101f-185">IVsPackageSourceProvider interface</span></span>

```cs
/// <summary>
/// A public API for retrieving the list of NuGet package sources.
/// </summary>
public interface IVsPackageSourceProvider
{
    /// <summary>
    /// Provides the list of package sources.
    /// </summary>
    /// <param name="includeUnOfficial">Unofficial sources will be included in the results</param>
    /// <param name="includeDisabled">Disabled sources will be included in the results</param>
    /// <remarks>Does not require the UI thread.</remarks>
    /// <exception cref="ArgumentException">Thrown if a NuGet configuration file is invalid.</exception>
    /// <exception cref="ArgumentNullException">Thrown if a NuGet configuration file is invalid.</exception>
    /// <exception cref="InvalidOperationException">Thrown if a NuGet configuration file is invalid.</exception>
    /// <exception cref="InvalidDataException">Thrown if a NuGet configuration file is invalid.</exception>
    /// <returns>Key: source name Value: source URI</returns>
    IEnumerable<KeyValuePair<string, string>> GetSources(bool includeUnOfficial, bool includeDisabled);

    /// <summary>
    /// Raised when sources are added, removed, disabled, or modified.
    /// </summary>
    event EventHandler SourcesChanged;
}
```

## <a name="ivspackageuninstaller-interface"></a><span data-ttu-id="2101f-186">Interface IVsPackageUninstaller</span><span class="sxs-lookup"><span data-stu-id="2101f-186">IVsPackageUninstaller interface</span></span>

```cs
public interface IVsPackageUninstaller
{
    /// <summary>
    /// Uninstall the specified package from a project and specify whether to uninstall its dependency packages
    /// too.
    /// </summary>
    /// <param name="project">The project from which the package is uninstalled.</param>
    /// <param name="packageId">The package to be uninstalled</param>
    /// <param name="removeDependencies">
    /// A boolean to indicate whether the dependency packages should be
    /// uninstalled too.
    /// </param>
    void UninstallPackage(Project project, string packageId, bool removeDependencies);
}
```

## <a name="ivspathcontext-interface"></a><span data-ttu-id="2101f-187">Interface IVsPathContext</span><span class="sxs-lookup"><span data-stu-id="2101f-187">IVsPathContext interface</span></span>

```cs
/// <summary>
    /// NuGet path information specific to the current context (e.g. project context).
    /// Represents captured snapshot associated with current project/solution settings.
    /// Should be discarded immediately after all queries are done.
    /// </summary>
    [ComImport]
    [Guid("24A1A187-75EE-4296-A8B3-59F0E0707119")]
    public interface IVsPathContext
    {
        /// <summary>
        /// User package folder directory. The path returned is an absolute path.
        /// </summary>
        string UserPackageFolder { get; }

        /// <summary>
        /// Fallback package folder locations. The paths (if any) in the returned list are absolute paths. If no
        /// fallback package folders are configured, an empty list is returned. The item type of this sequence is
        /// <see cref="string"/>.
        /// </summary>
        IEnumerable FallbackPackageFolders { get; }

        /// <summary>
        /// Fetch a package directory containing the provided asset path.
        /// </summary>
        /// <param name="packageAssetPath">Absolute path to package asset file.</param>
        /// <param name="packageDirectoryPath">Full path to a package directory. 
        /// <code>null</code> if returned falue is <code>false</code>.</param>
        /// <returns>
        /// <code>true</code> when a package containing the given file was found, <code>false</code> - otherwise.
        /// </returns>
        /// <example>
        /// Suppose the project is a packages.config project and the following asset paths are provided:
        /// 
        /// - C:\src\MyProject\packages\NuGet.Versioning.3.5.0-rc1-final\lib\net45\NuGet.Versioning.dll
        /// - C:\path\to\non\package\assembly\Newtonsoft.Json.dll
        /// - C:\src\MyOtherProject\packages\NuGet.Core.2.12.0\lib\net40\NuGet.Core.dll
        /// - C:\src\MyProject\packages\Autofac.3.5.2\lib\net40\Autofac.dll
        /// - C:\src\MyProject\packages\Autofac.3.5.2\lib\net40\Autofac.Fake.dll
        /// 
        /// The result will be:
        /// 
        /// - C:\src\MyProject\packages\NuGet.Versioning.3.5.0-rc1-final
        /// - null
        /// - null
        /// - C:\src\MyProject\packages\Autofac.3.5.2
        /// - C:\src\MyProject\packages\Autofac.3.5.2
        /// </example>
        bool TryResolvePackageAsset(string packageAssetPath, out string packageDirectoryPath);
    }
```

## <a name="ivspathcontext2-interface"></a><span data-ttu-id="2101f-188">Interface IVsPathContext2</span><span class="sxs-lookup"><span data-stu-id="2101f-188">IVsPathContext2 interface</span></span>

```cs
/// <summary>
    /// NuGet path information specific to the current context (e.g. project context) or solution context
    /// Represents captured snapshot associated with current project/solution settings.
    /// Should be discarded immediately after all queries are done.
    /// </summary>
    public interface IVsPathContext2 : IVsPathContext
    {
        /// <summary>
        /// Solution packages folder directory. This will always be set irrespective if folder actually exists or not.
        /// The path returned is an absolute path.
        /// </summary>
        string SolutionPackageFolder { get; }
    }
```

## <a name="ivspathcontextprovider-interface"></a><span data-ttu-id="2101f-189">Interface IVsPathContextProvider</span><span class="sxs-lookup"><span data-stu-id="2101f-189">IVsPathContextProvider interface</span></span>

```cs
    /// <summary>
    /// A factory to initialize <see cref="IVsPathContext"/> instances.
    /// </summary>
    public interface IVsPathContextProvider
    {
        /// <summary>
        /// Attempts to create an instance of <see cref="IVsPathContext"/>.
        /// </summary>
        /// <param name="projectUniqueName">
        /// Unique identificator of the project. Should be a full path to project file.
        /// </param>
        /// <param name="context">The path context associated with given project.</param>
        /// <returns>
        /// <code>True</code> if operation has succeeded and context was created.
        /// False, otherwise, e.g. when provided project is not managed by NuGet.
        /// </returns>
        /// <throws>
        /// <code>ArgumentNullException</code> if projectUniqueName is passed as null.
        /// <code>InvalidOperationException</code> when it fails to create a context and return appropriate error message.
        /// </throws>
        bool TryCreateContext(string projectUniqueName, out IVsPathContext context);
    }
```

## <a name="ivspathcontextprovider2-interface"></a><span data-ttu-id="2101f-190">Interface IVsPathContextProvider2</span><span class="sxs-lookup"><span data-stu-id="2101f-190">IVsPathContextProvider2 interface</span></span>

```cs
    /// <summary>
    /// A factory to initialize <see cref="IVsPathContext2"/> instances.
    /// </summary>
    public interface IVsPathContextProvider2 : IVsPathContextProvider
    {
        /// <summary>
        /// Attempts to create an instance of <see cref="IVsPathContext2"/> for the solution.
        /// </summary>
        /// <param name="context">The path context associated with this solution.</param>
        /// <returns>
        /// <code>True</code> if operation has succeeded and context was created.
        /// <code>False</code> otherwise.
        /// </returns>
        /// <throws>
        /// <code>InvalidOperationException</code> when it fails to create a context and return appropriate error message.
        /// </throws>
        bool TryCreateSolutionContext(out IVsPathContext2 context);

        /// <summary>
        /// Attempts to create an instance of <see cref="IVsPathContext2"/> for the solution.
        /// </summary>
        /// <param name="solutionDirectory">
        /// path to the solution directory. Must be an absolute path.
        /// It will be performant to pass the solution directory if it's available.
        /// </param>
        /// <param name="context">The path context associated with this solution.</param>
        /// <returns>
        /// <code>True</code> if operation has succeeded and context was created.
        /// <code>False</code> otherwise.
        /// </returns>
        /// <throws>
        /// <code>ArgumentNullException</code> if solutionDirectory is passed as null.
        /// <code>InvalidOperationException</code> when it fails to create a context and return appropriate error message.
        /// </throws>
        bool TryCreateSolutionContext(string solutionDirectory, out IVsPathContext2 context);

        /// <summary>
        /// Attempts to create an instance of <see cref="IVsPathContext"/> containing only the user wide and machine wide configurations.
        /// If a solution is loaded, note that the values in the path context might not be the actual effective values for the solution.
        /// If a customer has overriden the `globalPackagesFolder` key or cleared the `fallbackPackageFolders`, these values will be incorrect.
        /// It is important to keep this scenario in mind when working with this path. To predict differences you can call this in combination with <see cref="TryCreateSolutionContext(out IVsPathContext2)"/>.
        /// </summary>
        /// <returns>
        /// <code>True</code> if operation has succeeded and context was created.
        /// <code>False</code> otherwise.
        /// </returns>
        /// <remarks>
        /// This method can be safely invoked from a background thread. Do note that this method might switch to the UI thread internally, so be mindful of blocking the UI thread on this.
        /// </remarks>
        bool TryCreateNoSolutionContext(out IVsPathContext vsPathContext);

```

## <a name="ivsprojectjsontopackagereferencemigrateresult-interface"></a><span data-ttu-id="2101f-191">Interface IVsProjectJsonToPackageReferenceMigrateResult</span><span class="sxs-lookup"><span data-stu-id="2101f-191">IVsProjectJsonToPackageReferenceMigrateResult interface</span></span>

```cs
    /// <summary>
    /// Contains the result of the migrate operation on a legacy project.json project
    /// </summary>
    public interface IVsProjectJsonToPackageReferenceMigrateResult
    {
        /// <summary>
        /// Returns the success value of the migration operation.
        /// </summary>
        bool IsSuccess { get; }

        /// <summary>
        /// If migrate operation was unsuccessful, stores the error message in the exception.
        /// </summary>
        string ErrorMessage { get; }
    }
```

## <a name="ivsprojectjsontopackagereferencemigrator-interface"></a><span data-ttu-id="2101f-192">Interface IVsProjectJsonToPackageReferenceMigrator</span><span class="sxs-lookup"><span data-stu-id="2101f-192">IVsProjectJsonToPackageReferenceMigrator interface</span></span>

```cs
    /// <summary>
    /// Contains methods to migrate a project.json based legacy project to PackageReference based project.
    /// </summary>
    public interface IVsProjectJsonToPackageReferenceMigrator
    {
        /// <summary>
        /// Migrates a legacy Project.json based project to Package Reference based project. The result 
        /// should be casted to type <see cref="IVsProjectJsonToPackageReferenceMigrateResult"/>
        /// The backup of the original project file and project.json file is created in the Backup folder
        /// in the root of the project directory.
        /// </summary>
        /// <param name="projectUniqueName">The full path to the project that needs to be migrated</param>
        Task<object> MigrateProjectJsonToPackageReferenceAsync(string projectUniqueName);

    }
```

## <a name="ivssemanticversioncomparer-interface"></a><span data-ttu-id="2101f-193">Interface IVsSemanticVersionComparer</span><span class="sxs-lookup"><span data-stu-id="2101f-193">IVsSemanticVersionComparer interface</span></span>

```cs
    /// <summary>
    /// An interface for comparing two opaque version strings by treating them as NuGet semantic
    /// versions.
    /// </summary>
    public interface IVsSemanticVersionComparer
    {
        /// <summary>
        /// Compares two version strings as if they were NuGet semantic version
        /// strings. Returns a number less than zero if <paramref name="versionA"/>
        /// is less than <paramref name="versionB"/>. Returns zero if the two versions 
        /// are equivalent. Returns a number greater than zero if <paramref name="versionA"/>
        /// is greater than <paramref name="versionB"/>.
        /// </summary>
        /// <param name="versionA">The first version string.</param>
        /// <param name="versionB">The second version string.</param>
        /// <exception cref="ArgumentNullException">If either version string is null.</exception>
        /// <exception cref="ArgumentException">If either string cannot be parsed.</exception>
        /// <returns>
        /// A standard comparison integer based on the relationship between the
        /// two provided versions.
        /// </returns>
        int Compare(string versionA, string versionB);
    }
```

## <a name="ivstemplatewizard-interface"></a><span data-ttu-id="2101f-194">Interface IVsTemplateWizard</span><span class="sxs-lookup"><span data-stu-id="2101f-194">IVsTemplateWizard interface</span></span>

```cs
/// <summary>
/// Defines the logic for a template wizard extension.
/// </summary>

public interface IVsTemplateWizard : IWizard
{
}
```
