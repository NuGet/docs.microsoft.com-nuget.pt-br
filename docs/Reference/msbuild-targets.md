---
title: "Empacotamento e restauração do NuGet como destinos do MSBuild | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 04/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: O pack e restore do NuGet podem funcionar diretamente como destinos do MSBuild com o NuGet 4.0 e superior.
keywords: NuGet e MSBuild, NuGet pack target, NuGet restore target
ms.reviewer:
- karann-msft
ms.openlocfilehash: 6c488f49e12b014e7bd197d57041745387a4d7b4
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>Empacotamento e restauração do NuGet como destinos do MSBuild

*NuGet 4.0 ou superior*

Com o formato PackageReference, NuGet 4.0 + pode armazenar manifesto todos os metadados diretamente dentro de um arquivo de projeto em vez de usar um separado `.nuspec` arquivo.

Com o MSBuild 15.1 ou superior, o NuGet também é um cidadão de primeira classe do MSBuild com os destinos `pack` e `restore`, conforme descrito abaixo. Esses destinos permitem que você trabalhe com o NuGet como faria com qualquer outra tarefa ou destino do MSBuild. (Para NuGet 3.x e anteriores, use os comandos [pack](../tools/cli-ref-pack.md) e [restore](../tools/cli-ref-restore.md) na CLI do NuGet.)

## <a name="target-build-order"></a>Ordem de build de destino

Como `pack` e `restore` são os destinos do MSBuild, você pode acessá-los para melhorar o fluxo de trabalho. Por exemplo, digamos que você deseja copiar o pacote para um compartilhamento de rede após empacotá-lo. Você pode fazer isso adicionando o seguinte ao seu arquivo de projeto:

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

Da mesma forma, você pode gravar uma tarefa do MSBuild, escrever seu próprio destino e consumir propriedades do NuGet na tarefa de MSBuild.

## <a name="pack-target"></a>pack target

Ao usar o destino do pacote, ou seja, `msbuild /t:pack`, MSBuild desenha suas entradas do arquivo de projeto. A tabela a seguir descreve as propriedades de MSBuild podem ser adicionadas a um arquivo de projeto no primeiro `<PropertyGroup>` nó. Você pode fazer essas edições facilmente no Visual Studio 2017 e posterior clicando com o botão direito do mouse no projeto e selecionando **Editar {project_name}** no menu de contexto. Para sua conveniência, a tabela é organizada pela propriedade equivalente em um arquivo [`.nuspec` ](../reference/nuspec.md).

Observe que as propriedades `Owners` e `Summary` de `.nuspec` não são compatíveis com o MSBuild.

| Valor de atributo/NuSpec | Propriedade do MSBuild | Padrão | Observações |
|--------|--------|--------|--------|
| Id | PackageId | AssemblyName | $(AssemblyName) do MSBuild |
| Versão | PackageVersion | Versão | Isso é compatível com semver, por exemplo “1.0.0”, “1.0.0-beta” ou “1.0.0-beta-00345” |
| VersionPrefix | PackageVersionPrefix | empty | Configuração PackageVersion substitui PackageVersionPrefix |
| VersionSuffix | PackageVersionSuffix | empty | $(VersionSuffix) do MSBuild. Configuração PackageVersion substitui PackageVersionSuffix |
| Autores | Autores | Nome do usuário atual | |
| Proprietários | N/D | Não está presente no NuSpec | |
| Título | Título | O PackageId| |
| Descrição | Descrição | “Package Description” | |
| Copyright | Copyright | empty | |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | false | |
| LicenseUrl | PackageLicenseUrl | empty | |
| ProjectUrl | PackageProjectUrl | empty | |
| IconUrl | PackageIconUrl | empty | |
| Marcas | PackageTags | empty | Marcas são delimitadas por ponto e vírgula. |
| ReleaseNotes | PackageReleaseNotes | empty | |
| RepositoryUrl | RepositoryUrl | empty | |
| RepositoryType | RepositoryType | empty | |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| Resumo | Sem suporte | | |

### <a name="pack-target-inputs"></a>pack target inputs

- IsPackable
- PackageVersion
- PackageId
- Autores
- Descrição
- Copyright
- PackageRequireLicenseAcceptance
- DevelopmentDependency
- PackageLicenseUrl
- PackageProjectUrl
- PackageIconUrl
- PackageReleaseNotes
- PackageTags
- PackageOutputPath
- IncludeSymbols
- IncludeSource
- PackageTypes
- IsTool
- RepositoryUrl
- RepositoryType
- NoPackageAnalysis
- MinClientVersion
- IncludeBuildOutput
- IncludeContentInPack
- BuildOutputTargetFolder
- ContentTargetFolders
- NuspecFile
- NuspecBasePath
- NuspecProperties

## <a name="pack-scenarios"></a>pack scenarios

### <a name="packageiconurl"></a>PackageIconUrl

Como parte da alteração para o [Problema do NuGet 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` eventualmente será alterado para `PackageIconUri` e pode ser um caminho relativo para um arquivo de ícone que será incluído na raiz do pacote resultante.

### <a name="output-assemblies"></a>Assemblies de saída

O `nuget pack` copia arquivos de saída com extensões `.exe`, `.dll`, `.xml`, `.winmd`, `.json` e `.pri`. Os arquivos de saída que são copiados dependem do que o MSBuild fornece do destino `BuiltOutputProjectGroup`.

Há duas propriedades de MSBuild que você pode usar em seu arquivo de projeto ou a linha de comando para controlar onde ficam os assemblies de saída:

- `IncludeBuildOutput`: um valor booliano que determina se os assemblies de saída de build devem ser incluídos no pacote.
- `BuildOutputTargetFolder`: especifica a pasta na qual os assemblies de saída devem ser colocados. Os assemblies de saída (e outros arquivos de saída) são copiados para suas respectivas pastas de estrutura.

### <a name="package-references"></a>Referências de pacote

Consulte [Referências de pacote em arquivos de projeto](../consume-packages/package-references-in-project-files.md).

### <a name="project-to-project-references"></a>Referências de projeto a projeto

As referências projeto a projeto são consideradas como referências de pacote do nuget por padrão, por exemplo:

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

Você também pode adicionar os seguintes metadados à referência de projeto:

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a>Incluindo o conteúdo em um pacote

Para incluir o conteúdo, adicione metadados extras ao item `<Content>` existente. Por padrão, tudo que pertencer ao tipo “Conteúdo” é incluído no pacote, a menos que seja substituído por entradas como a seguinte:

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

Por padrão, tudo é adicionado à raiz da pasta `content` e `contentFiles\any\<target_framework>` dentro de um pacote e preserva a estrutura e pasta relativa, a menos que você especifique um caminho de pacote:

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

Se você quiser copiar todo o conteúdo somente para determinadas pastas raiz (em vez de para `content` e `contentFiles`), será possível usar a propriedade `ContentTargetFolders` do MSBuild, que assume como padrão "content;contentFiles", mas pode ser definida como qualquer outro nome de pasta. Observe que só especificar “contentFiles” em `ContentTargetFolders` coloca os arquivos em `contentFiles\any\<target_framework>` ou `contentFiles\<language>\<target_framework>` com base em `buildAction`.

`PackagePath` pode ser um conjunto de caminhos de destino separados por ponto e vírgula. Especificar um caminho de pacote vazio adicionaria o arquivo à raiz do pacote. Por exemplo, o seguinte adiciona `libuv.txt` a `content\myfiles`, `content\samples` e a raiz do pacote:

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

Há também uma propriedade de MSBuild `$(IncludeContentInPack)`, que assume o padrão `true`. Se isso for definido como `false` em qualquer projeto, o conteúdo desse projeto não está incluso no pacote do nuget.

Outros metadados específicos do pacote que pode ser definido em qualquer um dos itens acima ```<PackageCopyToOutput>``` e ```<PackageFlatten>```, que define os valores ```CopyToOutput``` e ```Flatten``` na entrada ```contentFiles``` no nuspec de saída.

> [!Note]
> Além de itens de conteúdo, o `<Pack>` e `<PackagePath>` metadados também podem ser definidos em arquivos com uma ação de compilação de compilação, EmbeddedResource, ApplicationDefinition, página, recursos, tela inicial, DesignData, DesignDataWithDesignTimeCreateableTypes , CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource ou None.
>
> Para o pacote acrescentar o nome de arquivo ao caminho do pacote ao usar padrões glob, seu caminho de pacote deve terminar com o caractere separador de pasta, caso contrário, o caminho do pacote será tratado como o caminho completo, incluindo o nome do arquivo.

### <a name="includesymbols"></a>IncludeSymbols

Ao usar o `MSBuild /t:pack /p:IncludeSymbols=true`, os arquivos `.pdb` correspondentes são copiados junto com outros arquivos de saída (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`). Observe que a configuração `IncludeSymbols=true` cria um pacote regular *e* um pacote de símbolos.

### <a name="includesource"></a>IncludeSource

Isso é o mesmo que `IncludeSymbols`, exceto que também copia os arquivos de origem com arquivos `.pdb`. Todos os arquivos do tipo `Compile` são copiadas para `src\<ProjectName>\`, preservando a estrutura de pastas do caminho relativo no pacote resultante. O mesmo também ocorre para arquivos de origem de qualquer `ProjectReference` que tem `TreatAsPackageReference` definido como `false`.

Se um arquivo do tipo Compilação estiver fora da pasta de projeto, ele será adicionado apenas a `src\<ProjectName>\`.

### <a name="istool"></a>IsTool

Ao usar `MSBuild /t:pack /p:IsTool=true`, todos os arquivos de saída, conforme especificado no cenário [Assemblies de saída](#output-assemblies), são copiados para a pasta `tools` em vez da pasta `lib`. Observe que isso é diferente de um `DotNetCliTool` que é especificado pela configuração do `PackageType` no arquivo `.csproj`.

### <a name="packing-using-a-nuspec"></a>Empacotamento usando um .nuspec

Você pode usar um arquivo `.nuspec` para empacotar seu projeto desde que tenha um arquivo de projeto para importar `NuGet.Build.Tasks.Pack.targets` a fim de executar a tarefa de empacotamento. As três propriedades MSBuild a seguir são relevantes para empacotamento usando um `.nuspec`:

1. `NuspecFile`: caminho relativo ou absoluto para o arquivo `.nuspec` que está sendo usado para o empacotamento.
1. `NuspecProperties`: uma lista separada por ponto e vírgula de pares chave/valor. Devido à maneira como a análise de linha de comando do MSBuild funciona, várias propriedades precisam ser especificadas da seguinte maneira: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.  
1. `NuspecBasePath`: o caminho base para o arquivo `.nuspec`.

Se estiver usando `dotnet.exe` para empacotar seu projeto, use um comando como o seguinte:

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

Se estiver usando o MSBuild para empacotar seu projeto, use um comando como o seguinte:

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a>restore target

`MSBuild /t:restore` (que `nuget restore` e `dotnet restore` usam com projetos do .NET Core), restaura pacotes referenciados no arquivo de projeto da seguinte maneira:

1. Ler todas as referências projeto a projeto
1. Ler as propriedades do projeto para localizar a pasta intermediária e as estruturas de destino
1. Passar dados do msbuild para NuGet.Build.Tasks.dll
1. Executar restauração
1. Baixar os pacotes
1. Gravar arquivo de ativos, destinos e objetos

### <a name="restore-properties"></a>Restaurar propriedades

Configurações de restauração adicionais podem vir de propriedades MSBuild no arquivo de projeto. Os valores também podem ser definidos na linha de comando usando a opção `/p:` (consulte os Exemplos abaixo).

| Propriedade | Descrição |
|--------|--------|
| RestoreSources | Uma lista delimitada por ponto e vírgula de origens de pacote. |
| RestorePackagesPath | Caminho da pasta dos pacotes do usuário. |
| RestoreDisableParallel | Limite os downloads para um de cada vez. |
| RestoreConfigFile | Caminho para um arquivo `Nuget.Config` a ser aplicado. |
| RestoreNoCache | Se verdadeiro, evita o uso de cache da Web. |
| RestoreIgnoreFailedSources | Se verdadeiro, ignora origens de pacote com falha ou ausentes. |
| RestoreTaskAssemblyFile | Caminho para `NuGet.Build.Tasks.dll`. |
| RestoreGraphProjectInput | Lista separada por ponto e vírgula de projetos a serem restaurados, que devem conter caminhos absolutos. |
| RestoreOutputPath | Pasta de saída que usa a pasta `obj` como padrão. |

#### <a name="examples"></a>Exemplos

Linha de comando:

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

Arquivo de projeto:

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a>Restaurar saídas

A restauração cria os seguintes arquivos na pasta `obj` de build:

| Arquivo | Descrição |
|--------|--------|
| `project.assets.json` | Anteriormente `project.lock.json` |
| `{projectName}.projectFileExtension.nuget.g.props` | Referências a objetos do MSBuild contidos em pacotes |
| `{projectName}.projectFileExtension.nuget.g.targets` | Referências a destinos do MSBuild contidos em pacotes |

### <a name="packagetargetfallback"></a>PackageTargetFallback

O elemento `PackageTargetFallback` permite especificar um conjunto de destinos compatíveis a serem usados ao restaurar os pacotes. Ele foi desenvolvido para permitir que os pacotes que usam o dotnet [TxM](../reference/target-frameworks.md) funcionem com pacotes compatíveis que não declaram um dotnet TxM. Ou seja, se o projeto usar o dotnet TxM, todos os pacotes dos quais ele depende também deverão ter um dotnet TxM, a menos que você adicione o `<PackageTargetFallback>` ao projeto para permitir que plataformas não dotnet sejam compatíveis com o dotnet.

Por exemplo, se o projeto está usando o `netstandard1.6` TxM e um pacote dependente contém apenas `lib/net45/a.dll` e `lib/portable-net45+win81/a.dll`, o projeto não será compilado. Se a DLL que você deseja colocar é esta última, é possível adicionar um `PackageTargetFallback` como mostrado a seguir para dizer que a DLL `portable-net45+win81` é compatível:

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

Para declarar um fallback para todos os destinos em seu projeto, deixe o atributo `Condition` de fora. Você também pode estender qualquer `PackageTargetFallback` existente incluindo `$(PackageTargetFallback)` conforme mostrado aqui:

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a>Substituindo uma biblioteca de um grafo de restauração

Se uma restauração está trazendo o assembly errado, é possível excluir a escolha padrão do pacote e substituí-lo por outro de sua escolha. Primeiro com um `PackageReference` de nível superior, exclua todos os ativos:

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

Em seguida, adicione sua própria referência à cópia local apropriada da DLL:

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
