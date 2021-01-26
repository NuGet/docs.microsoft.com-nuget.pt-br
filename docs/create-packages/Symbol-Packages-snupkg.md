---
title: Como publicar pacotes de símbolos do NuGet usando o novo formato de pacote de símbolos '.snupkg' | Microsoft Docs
author: JonDouglas
ms.author: jodou
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Como criar pacotes de símbolos do NuGet (snupkg).
keywords: Pacotes de símbolos do NuGet, depuração de pacote do NuGet, suporte à depuração de NuGet, símbolos de pacotes, convenções de símbolo de pacote do NuGet
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: 001637348fdd435e4ffd3a5a55e8128d1eab453c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774569"
---
# <a name="creating-symbol-packages-snupkg"></a>Criando pacotes de símbolos (.snupkg)

Uma boa experiência de depuração depende da presença de símbolos de depuração, pois eles fornecem informações críticas, como a associação entre o código de origem compilado e o, nomes de variáveis locais, rastreamentos de pilha e muito mais. Você pode usar pacotes de símbolos (. snupkg) para distribuir esses símbolos e melhorar a experiência de depuração de seus pacotes NuGet.

> Observe que o pacote de símbolos não é a única estratégia para disponibilizar os símbolos de depuração para os consumidores da sua biblioteca. Também é [possível `embed` fazer](https://docs.microsoft.com/dotnet/core/deploying/single-file#include-pdb-files-inside-the-bundle) isso no `dll` ou `exe` com a seguinte propriedade de projeto:`<DebugType>embedded</DebugType>`

## <a name="prerequisites"></a>Pré-requisitos

[nuget.exe v 4.9.0 ou superior](https://www.nuget.org/downloads) ou [dotnet CLI v 2.2.0 ou superior](https://www.microsoft.com/net/download/dotnet-core/2.2), que implementa os [protocolos NuGet](../api/nuget-protocols.md)necessários.

## <a name="creating-a-symbol-package"></a>Criar um pacote de símbolos

Se você estiver usando a CLI ou o MSBuild da dotnet, precisará definir as `IncludeSymbols` `SymbolPackageFormat` Propriedades e para criar um arquivo. snupkg além do arquivo. nupkg.

* Adicione as seguintes propriedades ao seu arquivo. csproj:

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* Ou especifique essas propriedades na linha de comando:

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  ou

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

Se estiver usando o NuGet.exe, use os seguintes comandos para criar um arquivo .snupkg além do arquivo .nupkg:

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

A [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) propriedade pode ter um destes dois valores: `symbols.nupkg` (o padrão) ou `snupkg` . Se essa propriedade não for especificada, um pacote de símbolos herdado será criado.

> [!Note]
> O formato herdado `.symbols.nupkg` ainda tem suporte, mas apenas por razões de compatibilidade, como pacotes nativos (consulte [pacotes de símbolo herdados](Symbol-Packages.md)). O servidor de símbolos da NuGet.org aceita apenas o novo formato de pacote de símbolos – `.snupkg`.

## <a name="publishing-a-symbol-package"></a>Publicando um pacote de símbolos

1. Para sua conveniência, primeiro salve sua chave de API com o NuGet (veja [Publicar um pacote](../nuget-org/publish-a-package.md)).

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. Depois de publicar o pacote principal para o nuget.org, envie por push o pacote de símbolos da seguinte maneira.

    ```cli
    nuget push MyPackage.snupkg
    ```

1. Você também pode efetuar push nos pacotes primário e de símbolos simultaneamente usando o comando abaixo. Ambos os arquivos .nupkg e .snupkg precisam estar presentes na pasta atual.

    ```cli
    nuget push MyPackage.nupkg
    ```

O NuGet publicará ambos os pacotes em nuget.org. O `MyPackage.nupkg` será publicado primeiro, seguido por `MyPackage.snupkg`.

> [!Note]
> Se o pacote de símbolos não for publicado, verifique se você configurou a fonte de NuGet.org como `https://api.nuget.org/v3/index.json`. A publicação de pacote de símbolos tem compatibilidade apenas [na API do NuGet V3](../api/overview.md#versioning).

## <a name="nugetorg-symbol-server"></a>Servidor de símbolos de NuGet.org

O NuGet.org dá suporte a seu próprio repositório de servidor de símbolos e aceita apenas o novo formato de pacote de símbolos – `.snupkg`. Os consumidores de pacote podem usar os símbolos publicados no servidor de símbolos nuget.org adicionando `https://symbols.nuget.org/download/symbols` às suas origens de símbolos no Visual Studio, o que permite intervir no código do pacote no depurador do Visual Studio. Consulte [Especificar símbolos (.pdb) e arquivos de origem no depurador do Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) para obter mais detalhes sobre esse processo.

### <a name="nugetorg-symbol-package-constraints"></a>Restrições de pacote de símbolos NuGet.org

NuGet.org tem as seguintes restrições para pacotes de símbolo:

- Somente as seguintes extensões de arquivo são permitidas em pacotes de símbolos:,,,, `.pdb` `.nuspec` `.xml` `.psmdcp` `.rels` , `.p7s`
- Somente os [PDBs portáteis](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) gerenciados têm suporte no servidor de símbolos do NuGet. org.
- O PDBs e suas DLLs. nupkg associadas precisam ser compilados com o compilador no Visual Studio versão 15,9 ou superior (consulte o [hash de criptografia PDB](https://github.com/dotnet/roslyn/issues/24429))

Os pacotes de símbolo publicados no NuGet.org falharão na validação se essas restrições não forem atendidas. 

> [!NOTE]
> Projetos nativos, como projetos C++, produzem PDBs do Windows em vez de PDBs portáteis. Não há suporte para eles no servidor de símbolos do NuGet. org. Em vez disso, use [pacotes de símbolo herdados](Symbol-Packages.md) .

### <a name="symbol-package-validation-and-indexing"></a>Validação e indexação de pacote de símbolos

Os pacotes de símbolos publicados no [NuGet.org](https://www.nuget.org/) passam por várias validações, incluindo a verificação de malware. Se um pacote falhar em uma verificação de validação, a página de detalhes do pacote exibirá uma mensagem de erro. Além disso, os proprietários do pacote receberão um email com instruções sobre como corrigir os problemas identificados.

Quando o pacote de símbolos tiver passado por todas as validações, os símbolos serão indexados pelos servidores de símbolos do NuGet. org e estarão disponíveis para consumo.

A validação e indexação do pacote geralmente leva menos de 15 minutos. Se a publicação do pacote demorar mais do que o esperado, visite [status.NuGet.org](https://status.nuget.org/) para verificar se o NuGet.org está enfrentando interrupções. Se todos os sistemas estiverem operacionais e o pacote não tiver sido publicado com êxito dentro de uma hora, faça logon no nuget.org e entre em contato conosco usando o link Entre em contato com o suporte na página de detalhes do pacote.

## <a name="symbol-package-structure"></a>Estrutura do pacote de símbolos

O pacote de símbolos (. snupkg) tem as seguintes características:

1) O. snupkg tem a mesma ID e versão que seu pacote NuGet correspondente (. nupkg).
2) O. snupkg tem a mesma estrutura de pastas que o. nupkg correspondente para quaisquer arquivos DLL ou EXE com a distinção que, em vez de DLLs/EXEs, seus PDBs correspondentes serão incluídos na mesma hierarquia de pastas. Arquivos e pastas com extensões que não sejam PDB serão deixados de fora do snupkg.
3) O arquivo. nuspec do pacote de símbolos tem o `SymbolsPackage` tipo de pacote:

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) Se um autor decide usar um nuspec personalizado para compilar seus nupkg e snupkg, o snupkg deve ter a mesma hierarquia de pastas e arquivos detalhados em 2).
5) Os campos a seguir serão excluídos do nuspec do snupkg: ```authors``` , ```owners``` ,, ```requireLicenseAcceptance``` , ```license type``` ```licenseUrl``` e  ```icon``` .
6) Não use o elemento ```<license>```. Um .snupkg é coberto pela mesma licença que o .nupkg correspondente.

## <a name="see-also"></a>Confira também

Considere usar o link de origem para habilitar a depuração de código-fonte de assemblies .NET. Para obter mais informações, consulte as [diretrizes de link de origem](/dotnet/standard/library-guidance/sourcelink).

Para obter mais informações sobre pacotes de símbolos, consulte a [depuração do pacote NuGet &](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) a especificação de design de melhorias de símbolos.
