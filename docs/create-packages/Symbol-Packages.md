---
title: Criando pacotes de símbolos legados (.symbols.nupkg)
description: Como criar pacotes do NuGet que contêm apenas os símbolos compatíveis com a depuração de outros pacotes do NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 374e9ccfc01cd06508e76529765db3f849342222
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "77476263"
---
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a>Criando pacotes de símbolos legados (.symbols.nupkg)

> [!Important]
> O novo formato recomendado para pacotes de símbolos é .snupkg. Veja [Criando pacotes de símbolos (.snupkg)](Symbol-Packages-snupkg.md). </br>
> .symbols.nupkg ainda é compatível, mas exclusivamente por razões de compatibilidade.

Além de criar pacotes para nuget.org ou outras fontes, o NuGet também suporta a criação de pacotes de símbolos associados que podem ser publicados em servidores símbolo. O formato do pacote de símbolos legado, .symbols.nupkg, pode ser empurrado para o repositório SymbolSource.

Os consumidores de pacote podem adicionar `https://nuget.smbsrc.net` às suas origens de símbolos no Visual Studio, o que permite intervir no código do pacote no depurador do Visual Studio. Consulte [Especificar símbolos (.pdb) e arquivos de origem no depurador do Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) para obter mais detalhes sobre esse processo.

## <a name="creating-a-legacy-symbol-package"></a>Criando um pacote de símbolos legados

Para criar um pacote de símbolos legados, siga estas convenções:

- Nomeie o pacote primário (com o seu código) `{identifier}.nupkg` e inclua todos os arquivos, exceto os arquivos `.pdb`.
- Nomeie o `{identifier}.symbols.nupkg` pacote de símbolos `.pdb` legados e inclua seu dLL de montagem, arquivos, arquivos XMLDOC, arquivos de origem (veja as seções a seguir).

Você pode criar pacotes com a opção `-Symbols` de um arquivo `.nuspec` ou um arquivo de projeto:

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

Observe que `pack` requer o Mono 4.4.2 no Mac OS X e não funciona em sistemas Linux. Em um Mac, você também precisa converter os nomes de caminho do Windows no arquivo `.nuspec` em caminhos no estilo Unix.

## <a name="legacy-symbol-package-structure"></a>Estrutura do pacote de símbolos legado

Um pacote de símbolos legado pode atingir várias estruturas de destino da `lib` mesma forma que um pacote de biblioteca, de modo que a estrutura da pasta deve ser exatamente a mesma do pacote principal, apenas incluindo `.pdb` arquivos ao lado da DLL.

Por exemplo, um pacote de símbolos legado que tem como alvo o .NET 4.0 e o Silverlight 4 teria esse layout:

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

Arquivos de origem são, então, colocados em uma pasta especial separada chamada `src`, que precisa seguir a estrutura relativa do repositório de origem. Isso ocorre porque PDBs contêm caminhos absolutos para arquivos de origem usados para compilar a DLL correspondente e eles precisam ser encontrados durante o processo de publicação. Um caminho base (prefixo de caminho comum) pode ser retirado. Por exemplo, considere uma biblioteca construída a partir desses arquivos:

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

Além da `lib` pasta, um pacote de símbololegado precisaria conter esse layout:

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

Um pacote de símbololegado pode ser construído por convenções, a partir de uma estrutura `files` de pasta como descrito na seção anterior, ou especificando seu conteúdo na seção do manifesto. Por exemplo, para compilar o pacote mostrado na seção anterior, use o seguinte no arquivo `.nuspec`:

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a>Publicando um pacote de símbolos legados

> [!Important]
> Para enviar pacotes para o nuget.org, você deve usar o [nuget.exe v4.9.1 ou posterior](https://www.nuget.org/downloads), que implementa os [protocolos NuGet](../api/nuget-protocols.md) necessários.

1. Para sua conveniência, primeiro salve sua chave de API com o NuGet (consulte [publicar um pacote](../nuget-org/publish-a-package.md), que aplicará nuget.org e symbolsource.org, pois symbolsource.org verificará nuget.org para confirmar se você é o proprietário do pacote.

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. Depois de publicar seu pacote principal para nuget.org, empurre o pacote de símbololegado da `.symbols` seguinte forma, que usará automaticamente symbolsource.org como alvo por causa do nome do arquivo:

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. Para publicar em um repositório de símbolos diferente, ou para empurrar um `-Source` pacote de símbolos legado sem seguir a convenção de nomeação, use a opção:

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. Você também pode efetuar push nos pacotes primário e de símbolos para ambos os repositórios ao mesmo tempo usando o seguinte:

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > Com nuget.exe 4.5.0 ou superior, os pacotes de símbolos não são automaticamente empurrados para symbolsource.org. Você precisaria empurrar os pacotes de símbolos separadamente, como explicado nas etapas anteriores.
   
Nesse caso, o NuGet publicará `MyPackage.symbols.nupkg`, se presente, em https://nuget.smbsrc.net/ (a URL de push para symbolsource.org), depois de publicar o pacote principal em nuget.org.

## <a name="see-also"></a>Confira também

* [Criação de pacotes de símbolos (.snupkg)](Symbol-Packages-snupkg.md) - O novo formato recomendado para pacotes de símbolos
* [Mover para o novo mecanismo de SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)
