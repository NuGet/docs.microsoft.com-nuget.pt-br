---
title: Como publicar pacotes de símbolos do NuGet usando o novo formato de pacote de símbolos '.snupkg' | Microsoft Docs
author: cristinamanu
ms.author: cristinamanu
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
ms.openlocfilehash: c42032f1869f4be0af44ffa8fbd5ad522f73c459
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "80380412"
---
# <a name="creating-symbol-packages-snupkg"></a>Criando pacotes de símbolos (.snupkg)

Uma boa experiência de depuração depende da presença de símbolos de depuração, pois eles fornecem informações críticas, como a associação entre o compilado e o código fonte, nomes de variáveis locais, traços de pilha e muito mais. Você pode usar pacotes de símbolos (.snupkg) para distribuir esses símbolos e melhorar a experiência de depuração de seus pacotes NuGet.

## <a name="prerequisites"></a>Pré-requisitos

[nuget.exe v4.9.0 ou acima](https://www.nuget.org/downloads) ou [dotnet CLI v2.2.0 ou superior,](https://www.microsoft.com/net/download/dotnet-core/2.2)que implementam os [protocolos NuGet necessários](../api/nuget-protocols.md).

## <a name="creating-a-symbol-package"></a>Criar um pacote de símbolos

Se você estiver usando o DOtnet CLI ou MSBuild, você precisa definir as `IncludeSymbols` propriedades e `SymbolPackageFormat` as propriedades para criar um arquivo .snupkg, além do arquivo .nupkg.

* Adicione as seguintes propriedades ao seu arquivo .csproj:

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

A [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) propriedade pode ter um `symbols.nupkg` dos dois `snupkg`valores: (o padrão) ou . Se essa propriedade não for especificada, um pacote de símbolo legado será criado.

> [!Note]
> O formato herdado `.symbols.nupkg` ainda é compatível, mas apenas por razões de compatibilidade (veja [Pacotes de símbolos herdados](Symbol-Packages.md)). O servidor de símbolos da NuGet.org aceita apenas o novo formato de pacote de símbolos – `.snupkg`.

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

### <a name="nugetorg-symbol-package-constraints"></a>NuGet.org restrições do pacote de símbolos

NuGet.org tem as seguintes restrições para pacotes de símbolos:

- Somente as seguintes extensões de arquivo `.pdb` `.nuspec`são `.xml` `.psmdcp`permitidas em pacotes de símbolos: , , , , `.rels`,`.p7s`
- Somente [PDBs portáteis gerenciados](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) são suportados no servidor de símbolos do NuGet.org.
- Os PDBs e seus DLLs associados .nupkg precisam ser construídos com o compilador na versão 15.9 ou superior do Visual Studio (ver [hash cripto PDB](https://github.com/dotnet/roslyn/issues/24429))

Os pacotes de símbolos publicados para NuGet.org falharão na validação se essas restrições não forem atendidas. 

### <a name="symbol-package-validation-and-indexing"></a>Validação e indexação de pacote de símbolos

Pacotes de símbolos publicados para [NuGet.org](https://www.nuget.org/) passam por várias validações, incluindo a varredura de malware. Se um pacote falhar uma verificação de validação, a página de detalhes do pacote exibirá uma mensagem de erro. Além disso, os proprietários do pacote receberão um e-mail com instruções sobre como corrigir os problemas identificados.

Quando o pacote de símbolos tiver passado por todas as validações, os símbolos serão indexados pelos servidores símbolo sustais do NuGet.org e estarão disponíveis para consumo.

A validação e indexação do pacote geralmente leva menos de 15 minutos. Se a publicação do pacote demorar mais do que o esperado, visite [status.nuget.org](https://status.nuget.org/) para verificar se NuGet.org está sofrendo interrupções. Se todos os sistemas estiverem operacionais e o pacote não tiver sido publicado com êxito dentro de uma hora, faça logon no nuget.org e entre em contato conosco usando o link Entre em contato com o suporte na página de detalhes do pacote.

## <a name="symbol-package-structure"></a>Estrutura do pacote de símbolos

O pacote de símbolos (.snupkg) tem as seguintes características:

1) O .snupkg tem o mesmo id e versão que seu pacote NuGet correspondente (.nupkg).
2) O .snupkg tem a mesma estrutura de pasta que seu .nupkg correspondente para quaisquer arquivos DLL ou EXE com a distinção de que, em vez de DLLs/EXEs, seus PDBs correspondentes serão incluídos na mesma hierarquia de pastas. Arquivos e pastas com extensões que não sejam PDB serão deixados de fora do snupkg.
3) O arquivo .nuspec do pacote `SymbolsPackage` símbolo tem o tipo de pacote:

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) Se um autor decide usar um nuspec personalizado para compilar seus nupkg e snupkg, o snupkg deve ter a mesma hierarquia de pastas e arquivos detalhados em 2).
5) Os seguintes campos serão excluídos da nuspec ```authors```do ```owners``` ```requireLicenseAcceptance```snupkg: , , , ```license type``` ```licenseUrl```e ```icon```.
6) Não use o elemento ```<license>```. Um .snupkg é coberto pela mesma licença que o .nupkg correspondente.

## <a name="see-also"></a>Confira também

Considere usar o Source Link para habilitar a depuração do código fonte dos conjuntos .NET. Para obter mais informações, consulte a [orientação do Link de Origem](/dotnet/standard/library-guidance/sourcelink).

Para obter mais informações sobre pacotes de símbolos, consulte a [especificação de design de depuração de & símbolos do pacote NuGet.](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
