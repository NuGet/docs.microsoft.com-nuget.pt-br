---
title: Comando de pacote do NuGet CLI | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 55e9e4d2-8039-4e9b-bdd9-c8b3eb0e894b
description: "Referência para o comando de pacote nuget.exe"
keywords: "referência de pacote do NuGet, o comando de pacote"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0dbecb8f01acf781ab8d2e77e8df7fa405f74cf1
ms.sourcegitcommit: d576d84fb4b6a178eb2ac11f55deb08ac771ba1c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2018
---
# <a name="pack-command-nuget-cli"></a>comando de pacote NuGet CLI)

**Aplica-se a:** criação do pacote &bullet; **versões com suporte:** 2.7 +

Cria um pacote do NuGet com base em especificado `.nuspec` ou arquivo de projeto. O `dotnet pack` comando (consulte [comandos dotnet](dotnet-Commands.md)) e `msbuild /t:pack` (consulte [destinos do MSBuild](../schema/msbuild-targets.md)) podem ser usadas como alternativas.

> [!Important]
> Em Mono, criando um pacote de um arquivo de projeto não é suportado. Você também precisa ajustar caminhos de local não o `.nuspec` de arquivos para caminhos no estilo Unix, como nuget.exe não converte nomes de caminho do Windows em si.

## <a name="usage"></a>Uso

```
nuget pack <nuspecPath | projectPath> [options]
```

onde `<nuspecPath>` e `<projectPath>` especificar o `.nuspec` ou projeto de arquivo, respectivamente.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| BasePath | Define o caminho base dos arquivos definidos no `.nuspec` arquivo. |
| Build | Especifica que o projeto deve ser criado antes de criar o pacote. |
| Excluir | Especifica um ou mais padrões de curinga para excluir ao criar um pacote. Para especificar mais de um padrão, repita-sinalizador de exclusão. Consulte o exemplo a seguir. |
| ExcludeEmptyDirectories | Impede a inclusão de diretórios vazios ao criar o pacote. |
| ForceEnglishOutput | *(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Ajuda | Exibe informações de ajuda para o comando. |
| IncludeReferencedProjects | Indica que o pacote criado deve incluir projetos referenciados como dependências ou como parte do pacote. Se um projeto referenciado tem um correspondente `.nuspec` arquivo que tem o mesmo nome do projeto, em seguida, o projeto referenciado será adicionado como uma dependência. Caso contrário, o projeto referenciado é adicionado como parte do pacote. |
| MinClientVersion | Definir o *minClientVersion* atributo para o pacote criado. Esse valor substituirá o valor existente *minClientVersion* atributo (se houver) no `.nuspec` arquivo. |
| MSBuildPath | *(4.0 +)*  Especifica o caminho do MSBuild para usar com o comando tendo precedência sobre `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Especifica a versão do MSBuild a ser usado com este comando. Valores com suporte são 4, 12, 14, 15. Por padrão que o MSBuild em seu caminho é separado, caso contrário, o padrão é a versão mais recente instalada do MSBuild. |
| NoDefaultExcludes | Impede a exclusão padrão do NuGet compactar arquivos e arquivos e pastas que iniciam com um ponto, como `.svn` e `.gitignore`. |
| NoPackageAnalysis | Especifica que o pacote não deve executar a análise de pacote após a compilação do pacote. |
| OutputDirectory | Especifica a pasta na qual o pacote criado é armazenado. Se nenhuma pasta for especificada, a pasta atual será usada. |
| Propriedades | Especifica uma lista de propriedades que substituem os valores no arquivo de projeto; consulte [propriedades comuns de projeto MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) para nomes de propriedade. O argumento de propriedades aqui está uma lista de token = pares de valor, separados por ponto e vírgula, onde cada ocorrência de `$token$` no `.nuspec` arquivo será substituído pelo valor especificado. Valores podem ser cadeias de caracteres entre aspas. Observe que para a propriedade "Configuração", o padrão é "Debug". Para alterar para uma configuração de versão, use `-Properties Configuration=Release`. |
| Sufixo | *(3.4.4+)*  Anexa um sufixo para o número de versão gerados internamente, normalmente usado para anexar construção ou outros identificadores de pré-lançamento. Por exemplo, usando `-suffix nightly` criará um pacote com um tipo de número de versão `1.2.3-nightly`. Sufixos devem começar com uma letra para evitar avisos, erros e incompatibilidades com versões diferentes do NuGet e o NuGet Package Manager. |
| Símbolos | Especifica que o pacote contém fontes e símbolos. Quando usado com um `.nuspec` arquivo, isso cria um arquivo de pacote do NuGet regular e pacote de símbolos correspondentes. |
| Ferramenta | Especifica que os arquivos de saída do projeto devem ser colocados no `tool` pasta. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas (2.5 +)*. |
| Versão | Substitui o número da versão de `.nuspec` arquivo. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Excluindo dependências de desenvolvimento

Alguns pacotes NuGet são úteis como dependências de desenvolvimento, o que ajuda a criar sua própria biblioteca, mas não são necessariamente necessários como dependências do pacote real.

O `pack` comando irá ignorar `package` entradas em `packages.config` que têm o `developmentDependency` atributo definido como `true`. Essas entradas não incluirá como um dependências do pacote criado.

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

```
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5" -MSBuildVersion 12

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
