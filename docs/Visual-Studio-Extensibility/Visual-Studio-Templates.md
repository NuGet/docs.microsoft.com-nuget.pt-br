---
title: Pacotes do NuGet em modelos do Visual Studio | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/3/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "As instruções para incluir pacotes do NuGet como parte dos modelos de projeto e de item do Visual Studio."
keywords: NuGet no Visual Studio, modelos de projeto do Visual Studio, modelos de item do Visual Studio, pacotes em modelos de projeto, pacotes em modelos de item
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 45a2ca2c08660be650f9cf38301f628923e1f8be
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="packages-in-visual-studio-templates"></a>Pacotes em modelos do Visual Studio

Os modelos de projeto e item do Visual Studio geralmente precisam garantir que determinados pacotes sejam instalados quando o projeto ou item for criado. Por exemplo, o modelo do ASP.NET MVC 3 instala jQuery, Modernizr e outros pacotes.

Para dar suporte a isso, os autores de modelo podem instruir o NuGet a instalar os pacotes necessários, em vez de bibliotecas individuais. Os desenvolvedores podem atualizar facilmente esses pacotes posteriormente a qualquer momento.

Para saber mais sobre como criar modelos, consulte [Como fazer para criando modelos de projeto](/visualstudio/ide/how-to-create-project-templates) ou [Criando modelos personalizados de projeto e de item](/visualstudio/extensibility/creating-custom-project-and-item-templates).

O restante desta seção descreve as etapas específicas a serem tomadas ao criar um modelo para incluir corretamente os pacotes do NuGet.

- [Adicionar pacotes a um modelo](#adding-packages-to-a-template)
- [Práticas recomendadas](#best-practices)

Para ver um exemplo, consulte o [Exemplo de NuGetInVsTemplates](https://bitbucket.org/marcind/nugetinvstemplates).

## <a name="adding-packages-to-a-template"></a>Adicionar pacotes a um modelo

Quando um modelo é instanciado, um [Assistente de modelo](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) é invocado para carregar a lista de pacotes para instalar juntamente com informações sobre onde encontrar esses pacotes. Pacotes podem ser inseridos no VSIX, inseridos no modelo ou localizados no disco rígido local, quando então você usa uma chave do Registro para referenciar o caminho do arquivo. Detalhes sobre esses locais são fornecidos mais adiante nesta seção.

Pacotes pré-instalados funcionam usando [assistentes de modelo](/visualstudio/extensibility/how-to-use-wizards-with-project-templates). Um assistente especial é invocado quando o modelo é instanciado. O assistente carrega a lista de pacotes que precisam ser instalados e transmite essas informações para as APIs do NuGet apropriadas.

Etapas para incluir pacotes em um modelo:

1. No seu arquivo `vstemplate`, adicione uma referência ao assistente de modelo do NuGet adicionando um elemento [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates):

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    `NuGet.VisualStudio.Interop.dll` é um assembly que contém apenas a classe `TemplateWizard`, que é um wrapper simples que chama a implementação real em `NuGet.VisualStudio.dll`. A versão do assembly nunca será alterada para que os modelos de projeto/item continuem a funcionar com novas versões do NuGet.

1. Adicione a lista de pacotes a serem instalados no projeto:

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    *(NuGet 2.2.1 ou superior)*  O assistente é compatível com vários elementos `<package>` para dar suporte a várias origens de pacote. Ambos os atributos `id` e `version` são necessários, o que significa que a versão específica de um pacote será instalada mesmo se uma versão mais recente estiver disponível. Isso impede que atualizações do pacote interrompam o modelo, deixando a opção de atualizar o pacote para o desenvolvedor que usa o modelo.

1. Especifique o repositório em que o NuGet pode encontrar os pacotes conforme descrito nas seções a seguir.

### <a name="vsix-package-repository"></a>Repositório de pacote VSIX

A abordagem de implantação recomendada para modelos de projeto/item do Visual Studio é um [extensão do VSIX](/visualstudio/extensibility/shipping-visual-studio-extensions) porque ela permite empacotar vários modelos de projeto/item juntos e permite que os desenvolvedores descubram facilmente seus modelos usando o Gerenciador de Extensões do VS ou a Galeria do Visual Studio. Atualizações da extensão também são fáceis de implantar usando o [mecanismo de atualização automática do Gerenciador de Extensões do Visual Studio](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).

O próprio VSIX pode servir como a origem para os pacotes necessários para o modelo:

1. Modifique o elemento `<packages>` no arquivo `.vstemplate` da seguinte maneira:

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    O atributo `repository` especifica o tipo de repositório como `extension` enquanto `repositoryId` é o identificador exclusivo do VSIX (esse é o valor do atributo `ID` no arquivo `vsixmanifest` da extensão, consulte [Referência do Esquema de Extensão do VSIX 2.0](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).

1. Coloque seus arquivos `nupkg` em uma pasta chamada `Packages` dentro do VSIX.

1. Adicione os arquivos de pacote necessários como `<Asset>` no seu arquivo `vsixmanifest` (consulte [Referência do Esquema de Extensão do VSIX 2.0](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. Observe que você pode entregar os mesmos pacotes VSIX como seus modelos de projeto ou colocá-los em um VSIX separado se isso fizer mais sentido para o seu cenário. No entanto, não faça referência a nenhum VSIX que você não controla, pois as alterações para esta extensão podem interromper o modelo.

### <a name="template-package-repository"></a>Repositório de pacote de modelo

Se você estiver distribuindo apenas um modelo de projeto/item único e não precisar empacotar vários modelos, será possível usar uma abordagem mais simples, mas mais limitada, que inclui pacotes diretamente no arquivo ZIP do modelo do projeto/item:

1. Modifique o elemento `<packages>` no arquivo `.vstemplate` da seguinte maneira:

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    O atributo `repository` tem o valor `template` e o atributo `repositoryId` não é necessário.

1. Coloque os pacotes na pasta raiz do arquivo ZIP do modelo de projeto/item.

Observe que usar, usando essa abordagem, um VSIX que contém vários modelos leva a sobrecarga desnecessária quando um ou mais pacotes são comuns aos modelos. Nesses casos, use o [VSIX como repositório](#vsix-package-repository) conforme descrito na seção anterior.

### <a name="registry-specified-folder-path"></a>Caminho da pasta especificada do Registro

SDKs que são instalados usando um MSI podem instalar os pacotes do NuGet diretamente no computador do desenvolvedor. Isso faz com que eles fiquem disponíveis imediatamente quando um modelo de projeto ou item é usado, em vez de precisar extrai-los durante esse período. Modelos ASP.NET usam essa abordagem.

1. Faça o MSI instalar pacotes no computador. Você pode instalar apenas os arquivos `.nupkg` ou instalá-los junto com o conteúdo expandido, que salva uma etapa adicional quando o modelo é usado. Nesse caso, siga a estrutura de pasta padrão do NuGet no qual os arquivos `.nupkg` estão na pasta raiz e cada pacote tem uma subpasta com o par de ID/versão como o nome da subpasta.

1. Grave uma chave do Registro para identificar o local do pacote:

    - Local da chave: o `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` em todo o computador ou, em caso de modelos e pacotes instalados por usuário, use `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository` como alternativa
    - Nome da chave: use um nome exclusivo para você. Por exemplo, os modelos do ASP.NET MVC 4 para VS 2012 usam `AspNetMvc4VS11`.
    - Valores: o caminho completo para a pasta de pacotes.

1. No elemento `<packages>` no arquivo `.vstemplate`, adicione o atributo `repository="registry"` e especifique o nome da chave do Registro no atributo `keyName`.

    - Se você já descompactou seus pacotes, use o atributo `isPreunzipped="true"`.
    - *(NuGet 3.2 e superior)* Se você quiser forçar um build de tempo de design no final da instalação do pacote, adicione o atributo `forceDesignTimeBuild="true"`.
    - Como uma otimização, adicione `skipAssemblyReferences="true"` porque o próprio modelo já inclui as referências necessárias.

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a>Práticas recomendadas

1. Declare uma dependência no VSIX NuGet adicionando uma referência a ele no seu manifesto do VSIX:

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. Exija que modelos de item/projeto sejam salvos na criação incluindo [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) no arquivo `.vstemplate`.

1. Os modelos não incluem um arquivo `packages.config` ou `project.json`, nem incluem nenhuma referência ou conteúdo que seria adicionado quando os pacotes do NuGet são instalados.
