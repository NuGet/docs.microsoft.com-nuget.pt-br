---
title: Criar pacotes do NuGet do .NET Standard 2.0 com o Visual Studio 2017 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 5/23/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c1de334-fdc9-4e1e-8ef6-a90b3e77ff0f
description: "Uma explicação passo a passo de ponta a ponta da criação de pacotes do NuGet do .NET Standard 2.0 usando o NuGet 4.x e o Visual Studio 2017."
keywords: criar um pacote, pacotes do .NET Standard, .NET Core
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5b48ad2f062fd3a9b99985dbda6f89e6039dac4d
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="create-net-standard-20-packages-with-visual-studio-2017"></a>Criar pacotes do .NET Standard 2.0 com o Visual Studio 2017

*Aplica-se ao NuGet 4.x ou superior e o MSBuild 15.3 ou superior fornecido com o Visual Studio 2017 Atualização 3. Para versões anteriores do Visual Studio 2017, estas instruções se aplicam ao .NET Standard 1.4 a 1.6 alterando a propriedade \<TargetFramework\>. Consulte também [Criar pacotes do .NET Standard com o Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md) para trabalhar com o NuGet 3.x ou superior.*

A [Biblioteca do .NET Standard](/dotnet/articles/standard/library) é uma especificação formal de APIs .NET que devem estar disponíveis em todos os tempos de execução do .NET, estabelecendo dessa forma uma maior uniformidade no ecossistema do .NET. A Biblioteca do .NET Standard define um conjunto uniforme de APIs de BCL (Biblioteca de Classes Base) para implementação em todas as plataformas do .NET, independentemente da carga de trabalho. Ele permite que os desenvolvedores produzam PCLs que podem ser usados em todos os tempos de execução do .NET e reduz ou elimina as diretivas de compilação condicional específicas da plataforma em código compartilhado.

Este guia orientará você durante a criação de um pacote do nuget direcionado para a Biblioteca do .NET Standard 2.0 com o Visual Studio 2017 Atualização 3 e o NuGet 4.0.

1. [Pré-requisitos](#pre-requisites)
1. [Criar o projeto da biblioteca de classes](#create-the-netstandard-class-library-project)
1. [Editar metadados no arquivo .csproj](#edit-metadata-in-the-csproj-file)
1. [Empacotar o componente](#package-the-component)
1. [Tópicos relacionados](#related-topics)

## <a name="pre-requisites"></a>Pré-requisitos

Esta explicação passo a passo requer o Visual Studio 2017 Atualização 3 com a carga de trabalho **Desenvolvimento de multiplaforma do .NET Core**. Você pode instalar a edição Community gratuitamente no [visualstudio.com](https://www.visualstudio.com/) ou usar as edições Professional e Enterprise.

A carga de trabalho exigida aparece da seguinte maneira no instalador do Visual Studio:

![Carga de trabalho de desenvolvimento multiplataforma do .NET Core no Instalador do Visual Studio](media/NuGet4-01-Workload.png)

## <a name="create-the-net-standard-class-library-project"></a>Cria o projeto da biblioteca de classe do .NET Standard

1. No Visual Studio, **Arquivo > Novo > Projeto**, expanda o nó **Visual C# > .NET Standard**, selecione **Biblioteca de Classes (Net Standard)**, altere o nome para AppLogger e clique em OK.

    ![Criar um novo projeto de biblioteca de classes](media/NuGet4-02-NewProject.png)

1. Altere a configuração de build para **Versão**.
1. Clique com o botão direito do mouse no projeto `AppLogger` no Gerenciador de Soluções, selecione **Propriedades**, selecione a guia **Criar**, marque a caixa de **arquivo de documentação XML** e defina o nome de arquivo para apenas `AppLogger.xml`. Em seguida, salve o projeto.

1. Adicione seu código ao componente, como mostrado a seguir (que claramente apenas envia as mensagens como saída para o console):

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. Compile o projeto (com a configuração de Versão) e verifique se os arquivos DLL e XML são produzidos dentro da pasta `bin\Release\netstandard2.0`.

## <a name="edit-metadata-in-the-csproj-file"></a>Editar metadados no arquivo .csproj

Com projetos do NuGet 4.0 e .NET Core, os metadados de pacote estão contidos diretamente no arquivo `.csproj` em vez de arquivos externos, como um `.nuspec`. Uma descrição completa dos metadados é encontrada em [Empacotamento e restauração do NuGet como destinos do MSBuild](../schema/msbuild-targets.md#pack-target).

1. Clique com botão direito do mouse no projeto no Gerenciador de Soluções, selecione **Editar AppLogger.csproj** e, em seguida, edite o primeiro grupo de propriedades para incluir informações de pacote como o seguinte:

    ```xml
    <PropertyGroup>
        <TargetFramework>netstandard2.0</TargetFramework>
        <PackageId>AppLogger.YOUR_NAME</PackageId>
        <PackageVersion>1.0.0</PackageVersion>
        <Authors>YOUR_NAME</Authors>
        <Description>Awesome application logging utility</Description>
        <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
        <PackageReleaseNotes>First release</PackageReleaseNotes>
        <Copyright>Copyright 2017 (c) Contoso Corporation. All rights reserved.</Copyright>
        <PackageTags>logger logging logs</PackageTags>
    </PropertyGroup>
    ```

1. Salve o projeto, clique com o botão direito do mouse na solução e selecione **Compilar solução**, novamente, para gerar todos os arquivos de pacote, dessa vez com os metadados corretos.


## <a name="package-the-component"></a>Empacotar o componente

O NuGet 4.0 é compatível com um destino de pacote que usa o MSBuild versão 15.1 ou superior (incluindo MSBuild 15.3 como parte do Visual Studio 2017 Atualização 3) quando o projeto contém os metadados de pacote necessários, que foi adicionado na seção anterior. Para invocar o MSBuild dessa forma, basta especificar o destino do pacote na linha de comando na mesma pasta que o arquivo `.csproj`:

    msbuild /t:pack /p:Configuration=Release

Para ver opções adicionais com `msbuild /t:pack`, tal como incluir arquivos de conteúdo, símbolos e código-fonte, consulte [Empacotamento e restauração do NuGet como destinos do MSBuild](../schema/msbuild-targets.md#pack-target).

Em qualquer caso, o comando acima gera `AppLogger.YOUR_NAME.1.0.0.nupkg` na pasta `bin\Release` por padrão, pois ele compila essa configuração. Se você omitir a opção `/p`, a configuração padrão será `Debug`. 

Ao abrir este arquivo em uma ferramenta como o [Explorador de Pacotes do NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) e expandir todos os nós, você verá o seguinte conteúdo:

![O Explorador de Pacotes do NuGet mostrando o pacote AppLogger](media/NuGet4-03-PackageExplorer.png)

> [!Tip]
> O arquivo `.nupkg` é apenas um arquivo ZIP com uma extensão diferente. Também é possível examinar o conteúdo do pacote alterando `.nupkg` para `.zip`, mas lembre-se de restaurar a extensão antes de carregar um pacote para o nuget.org.

Para disponibilizar seu pacote para outros desenvolvedores, siga as instruções em [Publicar um pacote](../create-packages/publish-a-package.md).

## <a name="related-topics"></a>Tópicos relacionados

- [Referências de pacote nos arquivos de projeto](../consume-packages/package-references-in-project-files.md) descreve todos os detalhes de descrever seu pacote diretamente no arquivo de projeto.
- [Empacotamento e restauração do NuGet como destinos do MSBuild](../schema/msbuild-targets.md) descreve todas as opções para usar `msbuild /t:pack` para criar o pacote.
- [Documentação da Biblioteca do .NET Standard](/dotnet/articles/standard/library)
- [Portabilidade para o .NET Core do .NET Framework](/dotnet/articles/core/porting/index)
