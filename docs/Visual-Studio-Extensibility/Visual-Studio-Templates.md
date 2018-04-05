---
title: Pacotes do NuGet em modelos do Visual Studio | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/03/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: As instruções para incluir pacotes do NuGet como parte dos modelos de projeto e de item do Visual Studio.
keywords: NuGet no Visual Studio, modelos de projeto do Visual Studio, modelos de item do Visual Studio, pacotes em modelos de projeto, pacotes em modelos de item
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 8c1751ba9caf5e71ace7a81575e4e5448b1e4185
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="packages-in-visual-studio-templates"></a><span data-ttu-id="14965-104">Pacotes em modelos do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="14965-104">Packages in Visual Studio templates</span></span>

<span data-ttu-id="14965-105">Os modelos de projeto e item do Visual Studio geralmente precisam garantir que determinados pacotes sejam instalados quando o projeto ou item for criado.</span><span class="sxs-lookup"><span data-stu-id="14965-105">Visual Studio project and item templates often need to ensure that certain packages are installed when a project or item is created.</span></span> <span data-ttu-id="14965-106">Por exemplo, o modelo do ASP.NET MVC 3 instala jQuery, Modernizr e outros pacotes.</span><span class="sxs-lookup"><span data-stu-id="14965-106">For example, the ASP.NET MVC 3 template installs jQuery, Modernizr, and other packages.</span></span>

<span data-ttu-id="14965-107">Para dar suporte a isso, os autores de modelo podem instruir o NuGet a instalar os pacotes necessários, em vez de bibliotecas individuais.</span><span class="sxs-lookup"><span data-stu-id="14965-107">To support this, template authors can instruct NuGet to install the necessary packages, rather than individual libraries.</span></span> <span data-ttu-id="14965-108">Os desenvolvedores podem atualizar facilmente esses pacotes posteriormente a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="14965-108">Developers can then easily update those packages at any later time.</span></span>

<span data-ttu-id="14965-109">Para saber mais sobre como criar modelos, consulte [Como fazer para criando modelos de projeto](/visualstudio/ide/how-to-create-project-templates) ou [Criando modelos personalizados de projeto e de item](/visualstudio/extensibility/creating-custom-project-and-item-templates).</span><span class="sxs-lookup"><span data-stu-id="14965-109">To learn more about authoring templates themselves, refer to [How to: Create Project Templates](/visualstudio/ide/how-to-create-project-templates) or [Creating Custom Project and Item Templates](/visualstudio/extensibility/creating-custom-project-and-item-templates).</span></span>

<span data-ttu-id="14965-110">O restante desta seção descreve as etapas específicas a serem tomadas ao criar um modelo para incluir corretamente os pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="14965-110">The remainder of this section describes the specific steps to take when authoring a template to properly include NuGet packages.</span></span>

- [<span data-ttu-id="14965-111">Adicionar pacotes a um modelo</span><span class="sxs-lookup"><span data-stu-id="14965-111">Adding packages to a template</span></span>](#adding-packages-to-a-template)
- [<span data-ttu-id="14965-112">Práticas recomendadas</span><span class="sxs-lookup"><span data-stu-id="14965-112">Best practices</span></span>](#best-practices)

<span data-ttu-id="14965-113">Para ver um exemplo, consulte o [Exemplo de NuGetInVsTemplates](https://bitbucket.org/marcind/nugetinvstemplates).</span><span class="sxs-lookup"><span data-stu-id="14965-113">For an example, see the [NuGetInVsTemplates sample](https://bitbucket.org/marcind/nugetinvstemplates).</span></span>

## <a name="adding-packages-to-a-template"></a><span data-ttu-id="14965-114">Adicionar pacotes a um modelo</span><span class="sxs-lookup"><span data-stu-id="14965-114">Adding packages to a template</span></span>

<span data-ttu-id="14965-115">Quando um modelo é instanciado, um [Assistente de modelo](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) é invocado para carregar a lista de pacotes para instalar juntamente com informações sobre onde encontrar esses pacotes.</span><span class="sxs-lookup"><span data-stu-id="14965-115">When a template is instantiated, a [template wizard](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) is invoked to load the list of packages to install along with information about where to find those packages.</span></span> <span data-ttu-id="14965-116">Pacotes podem ser inseridos no VSIX, inseridos no modelo ou localizados no disco rígido local, quando então você usa uma chave do Registro para referenciar o caminho do arquivo.</span><span class="sxs-lookup"><span data-stu-id="14965-116">Packages can be embedded in the VSIX, embedded in the template, or located on the local hard drive in which case you use a registry key to reference the file path.</span></span> <span data-ttu-id="14965-117">Detalhes sobre esses locais são fornecidos mais adiante nesta seção.</span><span class="sxs-lookup"><span data-stu-id="14965-117">Details on these locations are given later in this section.</span></span>

<span data-ttu-id="14965-118">Pacotes pré-instalados funcionam usando [assistentes de modelo](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span><span class="sxs-lookup"><span data-stu-id="14965-118">Preinstalled packages work using [template wizards](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span></span> <span data-ttu-id="14965-119">Um assistente especial é invocado quando o modelo é instanciado.</span><span class="sxs-lookup"><span data-stu-id="14965-119">A special wizard gets invoked when the template gets instantiated.</span></span> <span data-ttu-id="14965-120">O assistente carrega a lista de pacotes que precisam ser instalados e transmite essas informações para as APIs do NuGet apropriadas.</span><span class="sxs-lookup"><span data-stu-id="14965-120">The wizard loads the list of packages that need to be installed and passes that information to the appropriate NuGet APIs.</span></span>

<span data-ttu-id="14965-121">Etapas para incluir pacotes em um modelo:</span><span class="sxs-lookup"><span data-stu-id="14965-121">Steps to include packages in a template:</span></span>

1. <span data-ttu-id="14965-122">No seu arquivo `vstemplate`, adicione uma referência ao assistente de modelo do NuGet adicionando um elemento [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates):</span><span class="sxs-lookup"><span data-stu-id="14965-122">In your `vstemplate` file, add a reference to the NuGet template wizard by adding a [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) element:</span></span>

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    <span data-ttu-id="14965-123">`NuGet.VisualStudio.Interop.dll` é um assembly que contém apenas a classe `TemplateWizard`, que é um wrapper simples que chama a implementação real em `NuGet.VisualStudio.dll`.</span><span class="sxs-lookup"><span data-stu-id="14965-123">`NuGet.VisualStudio.Interop.dll` is an assembly that contains only the `TemplateWizard` class, which is a simple wrapper that calls into the actual implementation in `NuGet.VisualStudio.dll`.</span></span> <span data-ttu-id="14965-124">A versão do assembly nunca será alterada para que os modelos de projeto/item continuem a funcionar com novas versões do NuGet.</span><span class="sxs-lookup"><span data-stu-id="14965-124">The assembly version will never change so that project/item templates continue to work with new versions of NuGet.</span></span>

1. <span data-ttu-id="14965-125">Adicione a lista de pacotes a serem instalados no projeto:</span><span class="sxs-lookup"><span data-stu-id="14965-125">Add the list of packages to install in the project:</span></span>

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    <span data-ttu-id="14965-126">O assistente é compatível com vários elementos `<package>` para dar suporte a várias origens de pacote.</span><span class="sxs-lookup"><span data-stu-id="14965-126">The wizard supports multiple `<package>` elements to support multiple package sources.</span></span> <span data-ttu-id="14965-127">Ambos os atributos `id` e `version` são necessários, o que significa que a versão específica de um pacote será instalada mesmo se uma versão mais recente estiver disponível.</span><span class="sxs-lookup"><span data-stu-id="14965-127">Both the `id` and `version` attributes are required, meaning that specific version of a package will be installed even if a newer version is available.</span></span> <span data-ttu-id="14965-128">Isso impede que atualizações do pacote interrompam o modelo, deixando a opção de atualizar o pacote para o desenvolvedor que usa o modelo.</span><span class="sxs-lookup"><span data-stu-id="14965-128">This prevents package updates from breaking the template, leaving the choice to update the package to the developer using the template.</span></span>

1. <span data-ttu-id="14965-129">Especifique o repositório em que o NuGet pode encontrar os pacotes conforme descrito nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="14965-129">Specify the repository where NuGet can find the packages as described in the following sections.</span></span>

### <a name="vsix-package-repository"></a><span data-ttu-id="14965-130">Repositório de pacote VSIX</span><span class="sxs-lookup"><span data-stu-id="14965-130">VSIX package repository</span></span>

<span data-ttu-id="14965-131">A abordagem de implantação recomendada para modelos de projeto/item do Visual Studio é um [extensão do VSIX](/visualstudio/extensibility/shipping-visual-studio-extensions) porque ela permite empacotar vários modelos de projeto/item juntos e permite que os desenvolvedores descubram facilmente seus modelos usando o Gerenciador de Extensões do VS ou a Galeria do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="14965-131">The recommended deployment approach for Visual Studio project/item templates is a [VSIX extension](/visualstudio/extensibility/shipping-visual-studio-extensions) because it allows you to package multiple project/item templates together and allows developers to easily discover your templates using the VS Extension Manager or the Visual Studio Gallery.</span></span> <span data-ttu-id="14965-132">Atualizações da extensão também são fáceis de implantar usando o [mecanismo de atualização automática do Gerenciador de Extensões do Visual Studio](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).</span><span class="sxs-lookup"><span data-stu-id="14965-132">Updates to the extension are also easy to deploy using the [Visual Studio Extension Manager automatic update mechanism](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).</span></span>

<span data-ttu-id="14965-133">O próprio VSIX pode servir como a origem para os pacotes necessários para o modelo:</span><span class="sxs-lookup"><span data-stu-id="14965-133">The VSIX itself can serve as the source for packages required by the template:</span></span>

1. <span data-ttu-id="14965-134">Modifique o elemento `<packages>` no arquivo `.vstemplate` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="14965-134">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="14965-135">O atributo `repository` especifica o tipo de repositório como `extension` enquanto `repositoryId` é o identificador exclusivo do VSIX (esse é o valor do atributo `ID` no arquivo `vsixmanifest` da extensão, consulte [Referência do Esquema de Extensão do VSIX 2.0](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span><span class="sxs-lookup"><span data-stu-id="14965-135">The `repository` attribute specifies the type of repository as `extension` while `repositoryId` is the unique identifier of the VSIX itself (This is the value of the `ID` attribute in the extension’s `vsixmanifest` file, see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span></span>

1. <span data-ttu-id="14965-136">Coloque seus arquivos `nupkg` em uma pasta chamada `Packages` dentro do VSIX.</span><span class="sxs-lookup"><span data-stu-id="14965-136">Place your `nupkg` files in a folder called `Packages` within the VSIX.</span></span>

1. <span data-ttu-id="14965-137">Adicione os arquivos de pacote necessários como `<Asset>` no seu arquivo `vsixmanifest` (consulte [Referência do Esquema de Extensão do VSIX 2.0](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):</span><span class="sxs-lookup"><span data-stu-id="14965-137">Add the necessary package files as `<Asset>` in your `vsixmanifest` file (see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):</span></span>

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. <span data-ttu-id="14965-138">Observe que você pode entregar os mesmos pacotes VSIX como seus modelos de projeto ou colocá-los em um VSIX separado se isso fizer mais sentido para o seu cenário.</span><span class="sxs-lookup"><span data-stu-id="14965-138">Note that you can deliver packages in the same VSIX as your project templates or you can put them in a separate VSIX if that makes more sense for your scenario.</span></span> <span data-ttu-id="14965-139">No entanto, não faça referência a nenhum VSIX que você não controla, pois as alterações para esta extensão podem interromper o modelo.</span><span class="sxs-lookup"><span data-stu-id="14965-139">However, do not reference any VSIX over which you do not have control, because changes to that extension could break your template.</span></span>

### <a name="template-package-repository"></a><span data-ttu-id="14965-140">Repositório de pacote de modelo</span><span class="sxs-lookup"><span data-stu-id="14965-140">Template package repository</span></span>

<span data-ttu-id="14965-141">Se você estiver distribuindo apenas um modelo de projeto/item único e não precisar empacotar vários modelos, será possível usar uma abordagem mais simples, mas mais limitada, que inclui pacotes diretamente no arquivo ZIP do modelo do projeto/item:</span><span class="sxs-lookup"><span data-stu-id="14965-141">If you are distributing only a single project/item template and do not need to package multiple templates together, you can use a simpler but more limited approach that includes packages directly in the project/item template ZIP file:</span></span>

1. <span data-ttu-id="14965-142">Modifique o elemento `<packages>` no arquivo `.vstemplate` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="14965-142">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="14965-143">O atributo `repository` tem o valor `template` e o atributo `repositoryId` não é necessário.</span><span class="sxs-lookup"><span data-stu-id="14965-143">The `repository` attribute has the value `template` and the `repositoryId` attribute is not required.</span></span>

1. <span data-ttu-id="14965-144">Coloque os pacotes na pasta raiz do arquivo ZIP do modelo de projeto/item.</span><span class="sxs-lookup"><span data-stu-id="14965-144">Place packages in the root folder of the project/item template ZIP file.</span></span>

<span data-ttu-id="14965-145">Observe que usar, usando essa abordagem, um VSIX que contém vários modelos leva a sobrecarga desnecessária quando um ou mais pacotes são comuns aos modelos.</span><span class="sxs-lookup"><span data-stu-id="14965-145">Note that using this approach in a VSIX that contains multiple templates leads to unnecessary bloat when one or more packages are common to the templates.</span></span> <span data-ttu-id="14965-146">Nesses casos, use o [VSIX como repositório](#vsix-package-repository) conforme descrito na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="14965-146">In such cases, use the [VSIX as the repository](#vsix-package-repository) as described in the previous section.</span></span>

### <a name="registry-specified-folder-path"></a><span data-ttu-id="14965-147">Caminho da pasta especificada do Registro</span><span class="sxs-lookup"><span data-stu-id="14965-147">Registry-specified folder path</span></span>

<span data-ttu-id="14965-148">SDKs que são instalados usando um MSI podem instalar os pacotes do NuGet diretamente no computador do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="14965-148">SDKs that are installed using an MSI can install NuGet packages directly on the developer's machine.</span></span> <span data-ttu-id="14965-149">Isso faz com que eles fiquem disponíveis imediatamente quando um modelo de projeto ou item é usado, em vez de precisar extrai-los durante esse período.</span><span class="sxs-lookup"><span data-stu-id="14965-149">This makes them immediately available when a project or item template is used, rather than having to extract them during that time.</span></span> <span data-ttu-id="14965-150">Modelos ASP.NET usam essa abordagem.</span><span class="sxs-lookup"><span data-stu-id="14965-150">ASP.NET templates use this approach.</span></span>

1. <span data-ttu-id="14965-151">Faça o MSI instalar pacotes no computador.</span><span class="sxs-lookup"><span data-stu-id="14965-151">Have the MSI install packages to the machine.</span></span> <span data-ttu-id="14965-152">Você pode instalar apenas os arquivos `.nupkg` ou instalá-los junto com o conteúdo expandido, que salva uma etapa adicional quando o modelo é usado.</span><span class="sxs-lookup"><span data-stu-id="14965-152">You can install only the `.nupkg` files, or you can install those along with the expanded contents, which saves an additional step when the template is used.</span></span> <span data-ttu-id="14965-153">Nesse caso, siga a estrutura de pasta padrão do NuGet no qual os arquivos `.nupkg` estão na pasta raiz e cada pacote tem uma subpasta com o par de ID/versão como o nome da subpasta.</span><span class="sxs-lookup"><span data-stu-id="14965-153">In this case, follow NuGet's standard folder structure wherein the `.nupkg` files are in the root folder, and then each package has a subfolder with the id/version pair as the subfolder name.</span></span>

1. <span data-ttu-id="14965-154">Grave uma chave do Registro para identificar a localização do pacote:</span><span class="sxs-lookup"><span data-stu-id="14965-154">Write a registry key to identify the package location:</span></span>

    - <span data-ttu-id="14965-155">localização da chave: o `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` em todo o computador ou, em caso de modelos e pacotes instalados por usuário, use `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository` como alternativa</span><span class="sxs-lookup"><span data-stu-id="14965-155">Key location: Either the machine-wide `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` or if it's per-user installed templates and packages, alternatively use `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span></span>
    - <span data-ttu-id="14965-156">Nome da chave: use um nome exclusivo para você.</span><span class="sxs-lookup"><span data-stu-id="14965-156">Key name: use a name that's unique to you.</span></span> <span data-ttu-id="14965-157">Por exemplo, os modelos do ASP.NET MVC 4 para VS 2012 usam `AspNetMvc4VS11`.</span><span class="sxs-lookup"><span data-stu-id="14965-157">For example, the ASP.NET MVC 4 templates for VS 2012 use `AspNetMvc4VS11`.</span></span>
    - <span data-ttu-id="14965-158">Valores: o caminho completo para a pasta de pacotes.</span><span class="sxs-lookup"><span data-stu-id="14965-158">Values: the full path to the packages folder.</span></span>

1. <span data-ttu-id="14965-159">No elemento `<packages>` no arquivo `.vstemplate`, adicione o atributo `repository="registry"` e especifique o nome da chave do Registro no atributo `keyName`.</span><span class="sxs-lookup"><span data-stu-id="14965-159">In the `<packages>` element in the `.vstemplate` file, add the attribute `repository="registry"` and specify your registry key name in the `keyName` attribute.</span></span>

    - <span data-ttu-id="14965-160">Se você já descompactou seus pacotes, use o atributo `isPreunzipped="true"`.</span><span class="sxs-lookup"><span data-stu-id="14965-160">If you have pre-unzipped your packages, use the `isPreunzipped="true"` attribute.</span></span>
    - <span data-ttu-id="14965-161">*(NuGet 3.2 e superior)* Se você quiser forçar um build de tempo de design no final da instalação do pacote, adicione o atributo `forceDesignTimeBuild="true"`.</span><span class="sxs-lookup"><span data-stu-id="14965-161">*(NuGet 3.2+)* If you want to force a design-time build at the end of package installation, add the `forceDesignTimeBuild="true"` attribute.</span></span>
    - <span data-ttu-id="14965-162">Como uma otimização, adicione `skipAssemblyReferences="true"` porque o próprio modelo já inclui as referências necessárias.</span><span class="sxs-lookup"><span data-stu-id="14965-162">As an optimization, add `skipAssemblyReferences="true"` because the template itself already includes the necessary references.</span></span>

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a><span data-ttu-id="14965-163">Práticas recomendadas</span><span class="sxs-lookup"><span data-stu-id="14965-163">Best Practices</span></span>

1. <span data-ttu-id="14965-164">Declare uma dependência no VSIX NuGet adicionando uma referência a ele no seu manifesto do VSIX:</span><span class="sxs-lookup"><span data-stu-id="14965-164">Declare a dependency on the NuGet VSIX by adding a reference to it in your VSIX manifest:</span></span>

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. <span data-ttu-id="14965-165">Exija que modelos de item/projeto sejam salvos na criação incluindo [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) no arquivo `.vstemplate`.</span><span class="sxs-lookup"><span data-stu-id="14965-165">Require project/item templates to be saved on creation by including [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) in the `.vstemplate` file.</span></span>

1. <span data-ttu-id="14965-166">Os modelos não incluem um arquivo `packages.config`, nem incluem nenhuma referência ou conteúdo que seria adicionada na instalação dos pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="14965-166">Templates do not include a `packages.config` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>
