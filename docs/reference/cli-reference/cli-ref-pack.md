---
title: Comando NuGet CLI Pack
description: Referência para o comando do pacote de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 649c440d868c89068a069a396919b58b999369e5
ms.sourcegitcommit: f29fa9b93fd59e679fab50d7413bbf67da3ea5b3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86451132"
---
# <a name="pack-command-nuget-cli"></a>comando Pack (NuGet CLI)

**Aplica-se a:** &bullet; **versões com suporte** para criação de pacote: 2.7 +

Cria um pacote NuGet com base no arquivo [. nuspec](../nuspec.md) ou projeto especificado. O `dotnet pack` comando (consulte os [comandos dotnet](../dotnet-Commands.md)) e `msbuild -t:pack` (consulte [destinos do MSBuild](../msbuild-targets.md)) pode ser usado como alternativas.

> [!Important]
> Use o [`dotnet pack`](../dotnet-Commands.md) ou [`msbuild -t:pack`](../msbuild-targets.md) para projetos baseados em [PackageReference](../../consume-packages/package-references-in-project-files.md) .
> Em mono, não há suporte para a criação de um pacote a partir de um arquivo de projeto. Você também precisa ajustar caminhos não locais no `.nuspec` arquivo para caminhos em estilo UNIX, pois nuget.exe não converte os próprios caminhos do Windows.

## <a name="usage"></a>Uso

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

onde `<nuspecPath>` e `<projectPath>` especifique o `.nuspec` arquivo de projeto ou, respectivamente.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| BasePath | Define o caminho base dos arquivos definidos no arquivo [. nuspec](../nuspec.md) . |
| Build | Especifica que o projeto deve ser compilado antes da criação do pacote. |
| Excluir | Especifica um ou mais padrões de curinga a serem excluídos ao criar um pacote. Para especificar mais de um padrão, repita o sinalizador-Exclude. Consulte o exemplo a seguir. |
| ExcludeEmptyDirectories | Impede a inclusão de diretórios vazios ao compilar o pacote. |
| ForceEnglishOutput | *(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês. |
| ConfigFile | Especifique o arquivo de configuração para o comando de pacote. |
| Ajuda | Exibe informações de ajuda para o comando. |
| IncludeReferencedProjects | Indica que o pacote criado deve incluir projetos referenciados como dependências ou como parte do pacote. Se um projeto referenciado tiver um `.nuspec` arquivo correspondente que tenha o mesmo nome que o projeto, esse projeto referenciado será adicionado como uma dependência. Caso contrário, o projeto referenciado será adicionado como parte do pacote. |
| MinClientVersion | Defina o atributo *minClientVersion* para o pacote criado. Esse valor substituirá o valor do atributo *minClientVersion* existente (se houver) no `.nuspec` arquivo. |
| MSBuildPath | *(4.0 +)* Especifica o caminho do MSBuild a ser usado com o comando, tendo precedência sobre `-MSBuildVersion` . |
| MSBuildVersion | *(3,2 +)* Especifica a versão do MSBuild a ser usada com este comando. Os valores com suporte são 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Por padrão, o MSBuild em seu caminho é escolhido; caso contrário, ele usa a versão mais recente instalada do MSBuild. |
| NoDefaultExcludes | Impede a exclusão padrão de arquivos de pacote do NuGet e arquivos e pastas que começam com um ponto, como `.svn` e `.gitignore` . |
| NoPackageAnalysis | Especifica que o pacote não deve executar a análise de pacote após a compilação do pacote. |
| OutputDirectory | Especifica a pasta na qual o pacote criado é armazenado. Se nenhuma pasta for especificada, a pasta atual será usada. |
| Propriedades | Deve aparecer por último na linha de comando após outras opções. Especifica uma lista de propriedades que substituem valores no arquivo de projeto; consulte [Propriedades comuns do projeto MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) para nomes de propriedade. O argumento properties aqui é uma lista de pares token = valor, separados por ponto e vírgula, em que cada ocorrência de `$token$` no `.nuspec` arquivo será substituída pelo valor especificado. Os valores podem ser cadeias de caracteres entre aspas. Observe que, para a propriedade "Configuration", o padrão é "debug". Para alterar para uma configuração de versão, use `-Properties Configuration=Release` . **Em geral**, as propriedades devem ser as mesmas que foram usadas durante a compilação do projeto correspondente, a fim de evitar um comportamento potencialmente estranho. |
| Sufixo | *(3.4.4 +)* Acrescenta um sufixo ao número de versão gerado internamente, normalmente usado para anexar Build ou outros identificadores de pré-lançamento. Por exemplo, usar `-suffix nightly` criará um pacote com um número de versão como `1.2.3-nightly` . Os sufixos devem começar com uma letra para evitar avisos, erros e possíveis incompatibilidades com versões diferentes do NuGet e do Gerenciador de pacotes NuGet. |
| Símbolos | Especifica que o pacote contém fontes e símbolos. Quando usado com um `.nuspec` arquivo, isso cria um arquivo de pacote NuGet regular e o pacote de símbolos correspondente. Por padrão, ele cria um [pacote de símbolos herdado](../../create-packages/Symbol-Packages.md). O novo formato recomendado para pacotes de símbolos é .snupkg. Veja [Criando pacotes de símbolos (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md). |
| Ferramenta | Especifica que os arquivos de saída do projeto devem ser colocados na `tool` pasta. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*. |
| Versão | Substitui o número de versão do `.nuspec` arquivo. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Excluindo dependências de desenvolvimento

Alguns pacotes NuGet são úteis como dependências de desenvolvimento, que ajudam você a criar sua própria biblioteca, mas não são necessariamente necessárias como dependências de pacote reais.

O `pack` comando irá ignorar `package` entradas no `packages.config` que têm o `developmentDependency` atributo definido como `true` . Essas entradas não serão incluídas como dependências no pacote criado.

Por exemplo, considere o seguinte `packages.config` arquivo no projeto de origem:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Para este projeto, o pacote criado pelo `nuget pack` terá uma dependência de `jQuery` e `microsoft-web-helpers` , mas não `netfx-Guard` .

## <a name="suppressing-pack-warnings"></a>Suprimindo avisos de pacote

Embora seja recomendável que você resolva todos os avisos do NuGet durante suas operações de pacote, em determinadas situações, a supressão deles é garantida.

Você pode conseguir isso da seguinte maneira: 

> Pacote do pacote de nuget.exe. nuspec – Propriedades nowarn = NU5104

## <a name="examples"></a>Exemplos

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
