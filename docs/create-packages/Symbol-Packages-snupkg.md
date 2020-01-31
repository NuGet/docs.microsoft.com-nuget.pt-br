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
ms.openlocfilehash: 0109aea95ec255b3e0abcdff4cf51b4bfeafbb8c
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813475"
---
# <a name="creating-symbol-packages-snupkg"></a>Criando pacotes de símbolos (.snupkg)

Os pacotes de símbolos permitem melhorar a experiência de depuração dos pacotes NuGet.

## <a name="prerequisites"></a>{1&gt;{2&gt;Pré-requisitos&lt;2}&lt;1}

[NuGet.exe v4.9.0 ou superior](https://www.nuget.org/downloads) ou [dotnet.exe v2.2.0 ou acima](https://www.microsoft.com/net/download/dotnet-core/2.2), que implementam os [protocolos NuGet](../api/nuget-protocols.md) necessários.

## <a name="creating-a-symbol-package"></a>Criar um pacote de símbolos

Se você estiver usando dotNet. exe ou MSBuild, precisará definir as propriedades `IncludeSymbols` e `SymbolPackageFormat` para criar um arquivo. snupkg além do arquivo. nupkg.

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

A propriedade [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) pode ter um destes dois valores: `symbols.nupkg` (o padrão) ou `snupkg`. Se essa propriedade não for especificada, um pacote de símbolos herdado será criado.

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

### <a name="nugetorg-symbol-package-constraints"></a>Restrições de pacote de símbolos NuGet.org

NuGet.org tem as seguintes restrições para pacotes de símbolo:

- Somente as seguintes extensões de arquivo são permitidas em pacotes de símbolos: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`
- Somente os [PDBs portáteis](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) gerenciados têm suporte no servidor de símbolos do NuGet. org.
- O PDBs e suas DLLs. nupkg associadas precisam ser compilados com o compilador no Visual Studio versão 15,9 ou superior (consulte o [hash de criptografia PDB](https://github.com/dotnet/roslyn/issues/24429))

Os pacotes de símbolo publicados no NuGet.org falharão na validação se essas restrições não forem atendidas. 

### <a name="symbol-package-validation-and-indexing"></a>Validação e indexação de pacote de símbolos

Os pacotes de símbolos publicados no [NuGet.org](https://www.nuget.org/) passam por várias validações, incluindo a verificação de malware. Se um pacote falhar em uma verificação de validação, a página de detalhes do pacote exibirá uma mensagem de erro. Além disso, os proprietários do pacote receberão um email com instruções sobre como corrigir os problemas identificados.

Quando o pacote de símbolos tiver passado por todas as validações, os símbolos serão indexados pelos servidores de símbolos do NuGet. org. Depois de indexar, o símbolo estará disponível para consumo dos servidores de símbolos NuGet.org.

A validação e indexação do pacote geralmente leva menos de 15 minutos. Se a publicação do pacote estiver demorando mais do que o esperado, visite [status.nuget.org](https://status.nuget.org/) para verificar se o NuGet.org está passando por alguma interrupção. Se todos os sistemas estiverem operacionais e o pacote não tiver sido publicado com êxito dentro de uma hora, faça logon no nuget.org e entre em contato conosco usando o link Entre em contato com o suporte na página de detalhes do pacote.

## <a name="symbol-package-structure"></a>Estrutura do pacote de símbolos

O arquivo .nupkg seria exatamente o mesmo como está hoje, mas o arquivo .snupkg teria as seguintes características:

1) O .snupkg terá a mesma ID e versão que o .nupkg correspondente.
2) O .snupkg terá exatamente a mesma a estrutura de pasta que o nupkg para todos os arquivos DLL ou EXE, com a diferença que, em vez de DLLs/EXEs, seus PDBs correspondentes serão incluídos na mesma hierarquia de pastas. Arquivos e pastas com extensões que não sejam PDB serão deixados de fora do snupkg.
3) O arquivo .nuspec no .snupkg também especificará um novo PackageType, conforme mostrado a seguir. Isso deve ser o único PackageType especificado.

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) Se um autor decide usar um nuspec personalizado para compilar seus nupkg e snupkg, o snupkg deve ter a mesma hierarquia de pastas e arquivos detalhados em 2).
5) Os campos a seguir serão excluídos do nuspec: ```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl```e ```icon```do snupkg.
6) Não use o elemento ```<license>```. Um .snupkg é coberto pela mesma licença que o .nupkg correspondente.

## <a name="see-also"></a>Veja também

Considere usar o link de origem para habilitar a depuração de código-fonte de assemblies .NET. Para obter mais informações, consulte as [diretrizes de link de origem](/dotnet/standard/library-guidance/sourcelink).

Para obter mais informações sobre pacotes de símbolos, consulte a [depuração do pacote NuGet &](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) a especificação de design de melhorias de símbolos.
