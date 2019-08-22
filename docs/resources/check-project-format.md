---
title: Identificar o formato do projeto
description: Descreve como identificar o formato do projeto
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b151547e40e567b38acc2b0b9ee84c50d85000c9
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488487"
---
# <a name="identify-the-project-format"></a>Identificar o formato do projeto

O NuGet funciona com todos os projetos .NET. No entanto, o formato de projeto (estilo SDK ou não) determina algumas das ferramentas e dos métodos que você precisa usar para consumir e criar pacotes NuGet. Os projetos de estilo SDK usam o [atributo SDK](/dotnet/core/tools/csproj#additions). É importante identificar o tipo de projeto porque os métodos e as ferramentas que você usa para consumir e criar pacotes NuGet dependem do formato do projeto. Para projetos de estilo não SDK, os métodos e as ferramentas também dependem se o projeto foi migrado para o formato `PackageReference` ou não.

Se o seu projeto é do tipo SDK ou não depende do método usado para criar o projeto. A tabela a seguir mostra o formato de projeto padrão e a ferramenta CLI associada para seu projeto ao criá-lo usando o Visual Studio 2017 e versões posteriores.

| Projeto&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Formato padrão do projeto | Ferramenta CLI&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Observações |
|:------------- |:-------------|:-----|:-----|
| .NET Standard | Estilo SDK | [CLI do dotnet](../install-nuget-client-tools.md#dotnetexe-cli) | Os projetos criados antes do Visual Studio 2017 não são do tipo SDK. Use a CLI `nuget.exe`. |
| .NET Core | Estilo SDK | [CLI do dotnet](../install-nuget-client-tools.md#dotnetexe-cli) | Os projetos criados antes do Visual Studio 2017 não são do tipo SDK. Use a CLI `nuget.exe`. |
| .NET Framework | Estilo não SDK | [CLI do nuget.exe](../install-nuget-client-tools.md#nugetexe-cli) | Os projetos do .NET Framework criados usando outros métodos podem ser projetos em estilo SDK. Para isso, use o [CLI do dotnet](../install-nuget-client-tools.md#dotnetexe-cli) em vez disso. |
| Projeto .NET [migrado](../consume-packages/migrate-packages-config-to-package-reference.md) | Estilo não SDK| Para criar pacotes, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration). | Para criar pacotes, `msbuild -t:pack` é recomendado. Caso contrário, use o [CLI do dotnet](../install-nuget-client-tools.md#dotnetexe-cli). Projetos migrados não são projetos no estilo SDK. |

## <a name="check-the-project-format"></a>Verificar o formato do projeto

Se você não tiver certeza se o projeto está no formato de estilo SDK ou não, procure o atributo SDK no elemento `<Project>` no arquivo de projeto (para C#, é o arquivo *.csproj). Se houver, isso significará que o projeto está no estilo SDK.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <Authors>authorname</Authors>
    <PackageId>mypackageid</PackageId>
    <Company>mycompanyname</Company>
  </PropertyGroup>

</Project>
```

## <a name="check-the-project-format-in-visual-studio"></a>Verifique o formato do projeto no Visual Studio

Se você estiver trabalhando no Visual Studio, poderá verificar rapidamente o formato do projeto usando um dos seguintes métodos:

- Clique com o botão direito do mouse no projeto no Gerenciador de Soluções e selecione **Editar myprojectname.csproj**.

   Essa opção só está disponível a partir do Visual Studio 2017 para projetos que usam o atributo de estilo SDK. Caso contrário, use o outro método.

   ![Editar o arquivo de projeto](media/edit-project-file.png)

   Um projeto no estilo SDK mostra o [atributo SDK](/dotnet/core/tools/csproj#additions) no arquivo de projeto.
   
- No menu **Projeto**, escolha **Descarregar projeto** (ou clique com o botão direito e escolha **Descarregar projeto**).

   Este projeto não incluirá o atributo SDK no arquivo de projeto. Não é um projeto no estilo SDK.

   ![Descarregar o projeto](media/unload-project.png)

   Em seguida, clique com o botão direito do mouse no projeto descarregado e escolha **Editar myprojectname.csproj**.

## <a name="see-also"></a>Consulte também

- [Criar pacotes do .NET Standard com a CLI do dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [Criar pacotes do .NET Standard com o Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [Criar e publicar um pacote do .NET Framework (Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [Empacotamento e restauração do NuGet como destinos do MSBuild](../reference/msbuild-targets.md)
