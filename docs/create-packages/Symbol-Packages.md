---
title: Como criar pacotes de símbolos do NuGet
description: Como criar pacotes do NuGet que contêm apenas os símbolos compatíveis com a depuração de outros pacotes do NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 56125516345b2255998c1f734db60b58b9a92a06
ms.sourcegitcommit: 585394f063e95dcbc24d7ac0ce07de643eaf6f4d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55046322"
---
# <a name="creating-symbol-packages-legacy"></a>Criando pacotes de símbolos (herdado)

> [!Important]
> O novo formato recomendado para pacotes de símbolos é .snupkg. Veja [Criando pacotes de símbolos (.snupkg)](Symbol-Packages-snupkg.md). </br>
> .symbols.nupkg ainda é compatível, mas exclusivamente por razões de compatibilidade.

Além de compilar pacotes para nuget.org ou outras origens, o NuGet também dá suporte à criação de pacotes de símbolos associados e publica-os no repositório SymbolSource.

Os consumidores de pacote podem adicionar `https://nuget.smbsrc.net` às suas origens de símbolos no Visual Studio, o que permite intervir no código do pacote no depurador do Visual Studio. Consulte [Especificar símbolos (.pdb) e arquivos de origem no depurador do Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) para obter mais detalhes sobre esse processo.

## <a name="creating-a-symbol-package"></a>Criar um pacote de símbolos

Para criar um pacote de símbolos, siga essas convenções:

- Nomeie o pacote primário (com o seu código) `{identifier}.nupkg` e inclua todos os arquivos, exceto os arquivos `.pdb`.
- Nomeie o pacote de símbolos `{identifier}.symbols.nupkg` e inclua sua DLL de assembly, arquivos `.pdb`, arquivos XMLDOC, arquivos de origem (consulte as seções a seguir).

Você pode criar pacotes com a opção `-Symbols` de um arquivo `.nuspec` ou um arquivo de projeto:

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

Observe que `pack` requer o Mono 4.4.2 no Mac OS X e não funciona em sistemas Linux. Em um Mac, você também precisa converter os nomes de caminho do Windows no arquivo `.nuspec` em caminhos no estilo Unix.

## <a name="symbol-package-structure"></a>Estrutura do pacote de símbolos

Um pacote de símbolos pode ser direcionado a várias estruturas de destino da mesma maneira que um pacote de biblioteca, portanto, a estrutura da pasta `lib` deve ser exatamente a mesma que o pacote primário, incluindo somente arquivos `.pdb` junto com a DLL.

Por exemplo, um pacote de símbolos voltado para o .NET 4.0 e o Silverlight 4 teria este layout:

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

Arquivos de origem são, então, colocados em uma pasta especial separada chamada `src`, que precisa seguir a estrutura relativa do repositório de origem. Isso ocorre porque PDBs contêm caminhos absolutos para arquivos de origem usados para compilar a DLL correspondente e eles precisam ser encontrados durante o processo de publicação. Um caminho base (prefixo de caminho comum) pode ser eliminado. Por exemplo, considere uma biblioteca compilada com base nesses arquivos:

    C:\Projects
        \MyProject
            \Common
                \MyClass.cs
            \Full
                \Properties
                    \AssemblyInfo.cs
                \MyAssembly.csproj (producing \lib\net40\MyAssembly.dll)
            \Silverlight
                \Properties
                    \AssemblyInfo.cs
                \MySilverlightExtensions.cs
                \MyAssembly.csproj (producing \lib\sl4\MyAssembly.dll)

Além da pasta `lib`, um pacote de símbolos precisaria conter este layout:

    \src
        \Common
            \MyClass.cs
        \Full
            \Properties
                \AssemblyInfo.cs
        \Silverlight
            \Properties
                \AssemblyInfo.cs
            \MySilverlightExtensions.cs

## <a name="referring-to-files-in-the-nuspec"></a>Fazendo referência a arquivos no nuspec

Um pacote de símbolos pode ser compilado por convenções, de uma estrutura de pasta conforme descrito na seção anterior ou especificando o conteúdo na seção `files` do manifesto. Por exemplo, para compilar o pacote mostrado na seção anterior, use o seguinte no arquivo `.nuspec`:

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a>Publicando um pacote de símbolos

> [!Important]
> Para enviar pacotes para o nuget.org, você deve usar o [nuget.exe v4.9.1 ou posterior](https://www.nuget.org/downloads), que implementa os [protocolos NuGet](../api/nuget-protocols.md) necessários.

1. Para sua conveniência, primeiro salve sua chave de API com o NuGet (consulte [publicar um pacote](../create-packages/publish-a-package.md), que aplicará nuget.org e symbolsource.org, pois symbolsource.org verificará nuget.org para confirmar se você é o proprietário do pacote.

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. Depois de publicar o pacote principal no nuget.org, efetue push do pacote de símbolos como mostrado a seguir, que usará automaticamente symbolsource.org como o destino devido ao `.symbols` no nome de arquivo:

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. Para publicar em um repositório de símbolos diferente ou para efetuar push em um pacote de símbolos que não segue a convenção de nomenclatura, use a opção `-Source`:

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. Você também pode efetuar push nos pacotes primário e de símbolos para ambos os repositórios ao mesmo tempo usando o seguinte:

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > Com o nuget.exe 4.5.0 ou superior, os pacotes de símbolos não são enviados por push automaticamente para o symbolsource.org. Você precisaria efetuar push nos pacotes de símbolos separadamente, conforme explicado na próxima etapa.
   
Nesse caso, o NuGet publicará `MyPackage.symbols.nupkg`, se presente, em https://nuget.smbsrc.net/ (a URL de push para symbolsource.org), depois de publicar o pacote principal em nuget.org.

## <a name="see-also"></a>Consulte também

[Mover para o novo mecanismo de SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)
