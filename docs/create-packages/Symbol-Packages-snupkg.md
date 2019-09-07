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
ms.openlocfilehash: 109df18bcfd3e6a3fbd3ef3da1707ffada585140
ms.sourcegitcommit: f4bfdbf62302c95f1f39e81ccf998f8bbc6d56b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70749035"
---
# <a name="creating-symbol-packages-snupkg"></a>Criando pacotes de símbolos (.snupkg)

Os pacotes de símbolos permitem melhorar a experiência de depuração dos pacotes NuGet.

## <a name="prerequisites"></a>Pré-requisitos

[NuGet.exe v4.9.0 ou superior](https://www.nuget.org/downloads) ou [dotnet.exe v2.2.0 ou acima](https://www.microsoft.com/net/download/dotnet-core/2.2), que implementam os [protocolos NuGet](../api/nuget-protocols.md) necessários.

## <a name="creating-a-symbol-package"></a>Criar um pacote de símbolos

Se você estiver usando dotNet. exe ou MSBuild, precisará definir as `IncludeSymbols` Propriedades e `SymbolPackageFormat` para criar um arquivo. snupkg além do arquivo. nupkg.

* Adicione as seguintes propriedades ao seu arquivo. csproj:

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols> 
      <SymbolPackageFormat>snupkg</SymbolPackageFormat> 
   </PropertyGroup>
   ```

* Ou especifique essas propriedades na linha de comando:

     ```cli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  ou

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

Se estiver usando o NuGet.exe, use os seguintes comandos para criar um arquivo .snupkg além do arquivo .nupkg:

```
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

O NuGet.org dá suporte a seu próprio repositório de servidor de símbolos e aceita apenas o novo formato de pacote de símbolos – `.snupkg`. Os consumidores de pacote podem usar os símbolos publicados no servidor de símbolos nuget.org adicionando `https://symbols.nuget.org/download/symbols` às suas origens de símbolos no Visual Studio, o que permite intervir no código do pacote no depurador do Visual Studio. Consulte [Especificar símbolos (.pdb) e arquivos de origem no depurador do Visual Studio](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) para obter mais detalhes sobre esse processo.

### <a name="nugetorg-symbol-package-constraints"></a>Restrições de pacote de símbolos do nuget.org

Os pacotes de símbolos compatíveis com o nuget.org têm as restrições a seguir

- Somente as extensões de arquivo a seguir podem ser adicionadas a um pacote de símbolos. ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- Somente [Pdbs portáteis](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) gerenciados são compatíveis com o servidor de símbolos do nuget atualmente.
- Os pdbs e dlls do nupkg associados precisam ser compilados com o compilador no Visual Studio versão 15.9 ou superior (veja [hash de criptografia de pdb](https://github.com/dotnet/roslyn/issues/24429))

A publicação de pacote de símbolos no nuget.org falhará se qualquer outro tipo de arquivo for incluído no .snupkg.

### <a name="symbol-package-validation-and-indexing"></a>Validação e indexação de pacote de símbolos

Os pacotes de símbolos publicados em [NuGet.org](https://www.nuget.org/) passam por várias validações, tais como verificações de vírus.

Quando o pacote tiver passado todas as verificações de validação, pode levar algum tempo para que os símbolos sejam indexados e estejam disponíveis para consumo nos servidores de símbolos do NuGet.org. Se a verificação de validação do pacote falhar, a página de detalhes do pacote para o .nupkg será atualizada para exibir o erro associado e você também receberá um email notificando-o sobre isso.

A validação e indexação do pacote geralmente leva menos de 15 minutos. Se a publicação do pacote estiver demorando mais do que o esperado, visite [status.nuget.org](https://status.nuget.org/) para verificar se o nuget.org está passando por alguma interrupção. Se todos os sistemas estiverem operacionais e o pacote não tiver sido publicado com êxito dentro de uma hora, faça logon no nuget.org e entre em contato conosco usando o link Entre em contato com o suporte na página de detalhes do pacote.

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
5) O campo ```authors``` e ```owners``` será excluído do nuspec do snupkg.
6) Não use o elemento ```<license>```. Um .snupkg é coberto pela mesma licença que o .nupkg correspondente.

## <a name="see-also"></a>Consulte também

[Aprimoramentos na depuração do pacote NuGet & símbolos](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
