---
title: Como publicar pacotes de símbolos do NuGet usando o novo formato de pacote de símbolos '.snupkg' | Microsoft Docs
author:
- cristinamanu
- kraigb
ms.author:
- cristinamanu
- kraigb
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
ms.openlocfilehash: 1fbb243a7b3518307a393b5f371feae1edb7623a
ms.sourcegitcommit: 5c5f0f0e1f79098e27d9566dd98371f6ee16f8b5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645653"
---
# <a name="creating-symbol-packages-snupkg"></a>Criando pacotes de símbolos (.snupkg)

## <a name="prerequisites"></a>Pré-requisitos

[NuGet.exe v4.9.0 ou superior](https://www.nuget.org/downloads) ou [dotnet.exe v2.2.0 ou acima](https://www.microsoft.com/net/download/dotnet-core/2.2), que implementam os [protocolos NuGet](../api/nuget-protocols.md) necessários.

## <a name="creating-a-symbol-package"></a>Criar um pacote de símbolos

Um pacote de símbolos snupkg pode ser criado com base em um arquivo .nuspec ou de um arquivo .csproj. NuGet.exe e dotnet.exe são ambos compatíveis. Quando as opções ```-Symbols -SymbolPackageFormat snupkg``` são usadas no comando do pacote nuget.exe, um arquivo .snupkg será criado, além do arquivo .nupkg.

Comandos de exemplo para criar arquivos .snupkg
```
dotnet pack MyPackage.csproj --include-symbols -p:SymbolPackageFormat=snupkg

nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg

msbuild -t:pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
```

`.snupkgs` não são produzidos por padrão. Você deve passar a propriedade `SymbolPackageFormat` junto com `-Symbols` em caso de nuget.exe, `--include-symbols` em caso de dotnet.exe ou `-p:IncludeSymbols` em caso do msbuild.

A propriedade SymbolPackageFormat pode ter um dos dois valores: `symbols.nupkg` (o padrão) ou `snupkg`. Se o SymbolPackageFormat não for especificado, ele assumirá `symbols.nupkg` por padrão e um pacote de símbolos herdados será criado.

> [!Note]
> O formato herdado `.symbols.nupkg` ainda é compatível, mas apenas por razões de compatibilidade (veja [Pacotes de símbolos herdados](Symbol-Packages.md)). Servidor de símbolos de NuGet.org aceita apenas o novo formato de pacote de símbolos – `.snupkg`.

## <a name="publishing-a-symbol-package"></a>Publicando um pacote de símbolos

1. Para sua conveniência, primeiro salve sua chave de API com o NuGet (veja [Publicar um pacote](../create-packages/publish-a-package.md)).

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
``` 
<packageTypes>
  <packageType name="SymbolsPackage"/>
</packageTypes>
```
4) Se um autor decide usar um nuspec personalizado para compilar seus nupkg e snupkg, o snupkg deve ter a mesma hierarquia de pastas e arquivos detalhados em 2).
5) O campo ```authors``` e ```owners``` será excluído do nuspec do snupkg.

## <a name="see-also"></a>Consulte também

[NuGet-Package-Debugging-&-Symbols-Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
