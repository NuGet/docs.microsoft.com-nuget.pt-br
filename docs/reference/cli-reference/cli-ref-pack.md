---
title: Comando NuGet CLI Pack
description: Referência para o comando do pacote NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 00e2ee760698afd8591909570d76e4bfe475a682
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383989"
---
# <a name="pack-command-nuget-cli"></a>Commando pack (NuGet CLI)

**Aplica-se a: criação de** pacote &bullet; **versões com suporte:** 2.7 +

Cria um pacote NuGet com base no arquivo [. nuspec](../nuspec.md) ou projeto especificado. O comando `dotnet pack` (consulte os [comandos dotnet](../dotnet-Commands.md)) e `msbuild -t:pack` (consulte [destinos do MSBuild](../msbuild-targets.md)) podem ser usados como alternativas.

> [!Important]
> Use [`dotnet pack`](../dotnet-Commands.md) ou [`msbuild -t:pack`](../msbuild-targets.md) para projetos baseados em [PackageReference](../../consume-packages/package-references-in-project-files.md) .
> Em mono, não há suporte para a criação de um pacote a partir de um arquivo de projeto. Você também precisa ajustar caminhos não locais no arquivo de `.nuspec` para caminhos em estilo UNIX, já que NuGet. exe não converte os próprios caminhos do Windows.

## <a name="usage"></a>Medição de

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

onde `<nuspecPath>` e `<projectPath>` especificam o arquivo de `.nuspec` ou de projeto, respectivamente.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| BasePath | Define o caminho base dos arquivos definidos no arquivo [. nuspec](../nuspec.md) . |
| {1&gt;Compilação&lt;1} | Especifica que o projeto deve ser compilado antes da criação do pacote. |
| Excluir | Especifica um ou mais padrões de curinga a serem excluídos ao criar um pacote. Para especificar mais de um padrão, repita o sinalizador-Exclude. Consulte o exemplo a seguir. |
| ExcludeEmptyDirectories | Impede a inclusão de diretórios vazios ao compilar o pacote. |
| ForceEnglishOutput | *(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês. |
| ConfigFile | Especifique o arquivo de configuração para o comando de pacote. |
| Ajuda | Exibe informações de ajuda para o comando. |
| IncludeReferencedProjects | Indica que o pacote criado deve incluir projetos referenciados como dependências ou como parte do pacote. Se um projeto referenciado tiver um arquivo de `.nuspec` correspondente que tenha o mesmo nome que o projeto, esse projeto referenciado será adicionado como uma dependência. Caso contrário, o projeto referenciado será adicionado como parte do pacote. |
| MinClientVersion | Defina o atributo *minClientVersion* para o pacote criado. Esse valor substituirá o valor do atributo *minClientVersion* existente (se houver) no arquivo `.nuspec`. |
| MSBuildPath | *(4.0 +)* Especifica o caminho do MSBuild a ser usado com o comando, tendo precedência sobre `-MSBuildVersion`. |
| MSBuildVersion | *(3,2 +)* Especifica a versão do MSBuild a ser usada com este comando. Os valores com suporte são 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Por padrão, o MSBuild em seu caminho é escolhido; caso contrário, ele usa a versão mais recente instalada do MSBuild. |
| NoDefaultExcludes | Impede a exclusão padrão de arquivos de pacote do NuGet e arquivos e pastas que começam com um ponto, como `.svn` e `.gitignore`. |
| NoPackageAnalysis | Especifica que o pacote não deve executar a análise de pacote após a compilação do pacote. |
| OutputDirectory | Especifica a pasta na qual o pacote criado é armazenado. Se nenhuma pasta for especificada, a pasta atual será usada. |
| {1&gt;Propriedades&lt;1} | Deve aparecer por último na linha de comando após outras opções. Especifica uma lista de propriedades que substituem valores no arquivo de projeto; consulte [Propriedades comuns do projeto MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) para nomes de propriedade. O argumento properties aqui é uma lista de pares token = valor, separados por ponto e vírgula, em que cada ocorrência de `$token$` no arquivo `.nuspec` será substituída pelo valor especificado. Os valores podem ser cadeias de caracteres entre aspas. Observe que, para a propriedade "Configuration", o padrão é "debug". Para alterar para uma configuração de versão, use `-Properties Configuration=Release`. |
| Suffix | *(3.4.4 +)* Acrescenta um sufixo ao número de versão gerado internamente, normalmente usado para anexar Build ou outros identificadores de pré-lançamento. Por exemplo, usar `-suffix nightly` criará um pacote com um número de versão, como `1.2.3-nightly`. Os sufixos devem começar com uma letra para evitar avisos, erros e possíveis incompatibilidades com versões diferentes do NuGet e do Gerenciador de pacotes NuGet. |
| Símbolos | Especifica que o pacote contém fontes e símbolos. Quando usado com um arquivo `.nuspec`, isso cria um arquivo de pacote NuGet regular e o pacote de símbolos correspondente. Por padrão, ele cria um [pacote de símbolos herdado](../../create-packages/Symbol-Packages.md). O novo formato recomendado para pacotes de símbolos é .snupkg. Veja [Criando pacotes de símbolos (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md). |
| Ferramenta | Especifica que os arquivos de saída do projeto devem ser colocados na pasta `tool`. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*. |
| Versão do | Substitui o número de versão do arquivo de `.nuspec`. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Excluindo dependências de desenvolvimento

Alguns pacotes NuGet são úteis como dependências de desenvolvimento, que ajudam você a criar sua própria biblioteca, mas não são necessariamente necessárias como dependências de pacote reais.

O comando `pack` ignorará `package` entradas em `packages.config` que têm o atributo `developmentDependency` definido como `true`. Essas entradas não serão incluídas como dependências no pacote criado.

Por exemplo, considere o seguinte arquivo de `packages.config` no projeto de origem:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Para este projeto, o pacote criado pelo `nuget pack` terá uma dependência de `jQuery` e `microsoft-web-helpers`, mas não `netfx-Guard`.

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
