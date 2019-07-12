---
title: Comando de pacote da CLI do NuGet
description: Referência do comando de pacote nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: c3a01b7747be96f02f7b93b3bf66f5d1783ceed7
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842549"
---
# <a name="pack-command-nuget-cli"></a>Commando pack (NuGet CLI)

**Aplica-se a:** criação do pacote &bullet; **versões com suporte:** 2.7+

Cria um pacote do NuGet com base em especificado `.nuspec` ou arquivo de projeto. O `dotnet pack` comando (consulte [comandos dotnet](dotnet-Commands.md)) e `msbuild -t:pack` (consulte [destinos do MSBuild](../reference/msbuild-targets.md)) pode ser usado como alternativas.

> [!Important]
> Em Mono, criando um pacote em um arquivo de projeto não é suportado. Você também precisará ajustar os caminhos de local não no `.nuspec` de arquivo para caminhos no estilo Unix, como nuget.exe não converte nomes de caminhos do Windows em si.

## <a name="usage"></a>Uso

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

em que `<nuspecPath>` e `<projectPath>` especifique o `.nuspec` ou projeto de arquivo, respectivamente.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| BasePath | Define o caminho base dos arquivos definidos no `.nuspec` arquivo. |
| Build | Especifica que o projeto deve ser compilado antes de compilar o pacote. |
| Excluir | Especifica um ou mais padrões de curinga a ser excluído durante a criação de um pacote. Para especificar mais de um padrão, repita-sinalizador de exclusão. Consulte o exemplo a seguir. |
| ExcludeEmptyDirectories | Impede a inclusão de diretórios vazios ao criar o pacote. |
| ForceEnglishOutput | *(3.5 ou superior)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| ConfigFile | Especifique o arquivo de configuração para o comando pack. |
| Ajuda | Exibe informações de ajuda para o comando. |
| IncludeReferencedProjects | Indica que o pacote criado deve incluir nos projetos referenciados como dependências ou como parte do pacote. Se um projeto referenciado tem um correspondente `.nuspec` arquivo que tem o mesmo nome que o projeto, em seguida, esse projeto referenciado é adicionado como uma dependência. Caso contrário, o projeto referenciado é adicionado como parte do pacote. |
| MinClientVersion | Defina as *minClientVersion* atributo para o pacote criado. Esse valor substituirá o valor existente *minClientVersion* atributo (se houver) no `.nuspec` arquivo. |
| MSBuildPath | *(4.0 e posteriores)*  Especifica o caminho do MSBuild a usar com o comando, tendo precedência sobre `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 e superior)*  Especifica a versão do MSBuild a ser usado com este comando. Valores com suporte são 4, 12, 14, 15.1, 15.3, 15.4, 15,5, 15.6, 15.7, 15,8, 15,9. Por padrão que o MSBuild em seu caminho é escolhido, caso contrário, o padrão é a versão mais recente instalada do MSBuild. |
| NoDefaultExcludes | Impede a exclusão de padrão do NuGet empacotar arquivos e arquivos e pastas que iniciam com um ponto, como `.svn` e `.gitignore`. |
| NoPackageAnalysis | Especifica que o pacote não deve executar a análise de pacote após a compilação do pacote. |
| OutputDirectory | Especifica a pasta na qual o pacote criado é armazenado. Se nenhuma pasta for especificada, a pasta atual será usada. |
| Propriedades | Deve aparecer por último na linha de comando após outras opções. Especifica uma lista de propriedades que substituem os valores no arquivo de projeto; ver [propriedades de projeto comuns do MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) para nomes de propriedade. O argumento de propriedades aqui está uma lista de token = pares de valor, separados por ponto e vírgula, onde cada ocorrência de `$token$` no `.nuspec` arquivo será substituído com o valor fornecido. Valores podem ser cadeias de caracteres entre aspas. Observe que para a propriedade de "Configuração", o padrão é "Debug". Para alterar para uma configuração de versão, use `-Properties Configuration=Release`. |
| Sufixo | *(3.4.4+)*  Anexa um sufixo para o número de versão gerado internamente, normalmente usado para acrescentar o build ou outros identificadores de pré-lançamento. Por exemplo, usando `-suffix nightly` criará um pacote com um tipo de número de versão `1.2.3-nightly`. Sufixos devem começar com uma letra para evitar possíveis incompatibilidades com diferentes versões do NuGet e o Gerenciador de pacotes do NuGet, erros e avisos. |
| Símbolos | Especifica que o pacote contém fontes e símbolos. Quando usado com um `.nuspec` arquivo, isso cria um arquivo de pacote do NuGet regular e correspondente símbolos de pacote. Por padrão, ele cria um [pacote de símbolos herdados](../create-packages/Symbol-Packages.md). O novo formato recomendado para pacotes de símbolos é .snupkg. Veja [Criando pacotes de símbolos (.snupkg)](../create-packages/Symbol-Packages-snupkg.md). |
| SymbolPackageFormat | Especifica o formato do pacote de símbolos: *Symbols* (herdados) ou *snupkg* (recomendado). Por padrão, ele cria um [pacote de símbolos herdados](../create-packages/Symbol-Packages.md). Veja [Criando pacotes de símbolos (.snupkg)](../create-packages/Symbol-Packages-snupkg.md). |
| Ferramenta | Especifica que os arquivos de saída do projeto devem ser colocados no `tool` pasta. |
| Verbosity | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |
| Versão | Substitui o número de versão dos `.nuspec` arquivo. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Excluindo as dependências de desenvolvimento

Alguns pacotes do NuGet são úteis como dependências de desenvolvimento, que ajudam a criar sua própria biblioteca, mas não são necessariamente necessários como dependências do pacote real.

O `pack` comando ignorará `package` entradas na `packages.config` que têm o `developmentDependency` atributo definido como `true`. Essas entradas não incluirá como um dependências no pacote criado.

Por exemplo, considere o seguinte `packages.config` arquivo no projeto de origem:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Para este projeto, o pacote criado pelo `nuget pack` terá uma dependência no `jQuery` e `microsoft-web-helpers` mas não `netfx-Guard`.

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
