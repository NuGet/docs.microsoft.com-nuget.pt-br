---
title: Empacotamento e restauração do NuGet como destinos do MSBuild
description: O pack e restore do NuGet podem funcionar diretamente como destinos do MSBuild com o NuGet 4.0 e superior.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 8e662194fffc031d0cfc0aa129a5a15b555a4231
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68420017"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>Empacotamento e restauração do NuGet como destinos do MSBuild

*NuGet 4.0 ou superior*

Com o formato [PackageReference](../consume-packages/package-references-in-project-files.md) , o NuGet 4.0 + pode armazenar todos os metadados do manifesto diretamente dentro de um arquivo de projeto `.nuspec` em vez de usar um arquivo separado.

Com o MSBuild 15.1 ou superior, o NuGet também é um cidadão de primeira classe do MSBuild com os destinos `pack` e `restore`, conforme descrito abaixo. Esses destinos permitem que você trabalhe com o NuGet como faria com qualquer outra tarefa ou destino do MSBuild. (Para NuGet 3.x e anteriores, use os comandos [pack](../reference/cli-reference/cli-ref-pack.md) e [restore](../reference/cli-reference/cli-ref-restore.md) na CLI do NuGet.)

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

Para projetos de .net Standard usando o formato PackageReference, `msbuild -t:pack` o uso de desenha entradas do arquivo de projeto para usar na criação de um pacote NuGet.

A tabela abaixo descreve as propriedades do MSBuild que podem ser adicionadas a um arquivo do projeto dentro do primeiro nó `<PropertyGroup>`. Você pode fazer essas edições facilmente no Visual Studio 2017 e posterior clicando com o botão direito do mouse no projeto e selecionando **Editar {project_name}** no menu de contexto. Para sua conveniência, a tabela é organizada pela propriedade equivalente em um arquivo [`.nuspec` ](../reference/nuspec.md).

Observe que as propriedades `Owners` e `Summary` de `.nuspec` não são compatíveis com o MSBuild.

| Valor de atributo/NuSpec | Propriedade do MSBuild | Padrão | Observações |
|--------|--------|--------|--------|
| Id | PackageId | AssemblyName | $(AssemblyName) do MSBuild |
| Versão | PackageVersion | Versão | Isso é compatível com semver, por exemplo “1.0.0”, “1.0.0-beta” ou “1.0.0-beta-00345” |
| VersionPrefix | PackageVersionPrefix | empty | A configuração PackageVersion substitui PackageVersionPrefix |
| VersionSuffix | PackageVersionSuffix | empty | $(VersionSuffix) do MSBuild. A configuração PackageVersion substitui PackageVersionSuffix |
| Autores | Autores | Nome do usuário atual | |
| Proprietários | N/D | Não está presente no NuSpec | |
| Título | Título | O PackageId| |
| Descrição | Descrição | “Package Description” | |
| Copyright | Copyright | empty | |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | false | |
| Carteira | PackageLicenseExpression | empty | Corresponde a`<license type="expression">` |
| Carteira | PackageLicenseFile | empty | Corresponde ao `<license type="file">`. Talvez seja necessário empacotar explicitamente o arquivo de licença referenciado. |
| LicenseUrl | PackageLicenseUrl | empty | `licenseUrl`está sendo preterido, use a propriedade PackageLicenseExpression ou PackageLicenseFile |
| ProjectUrl | PackageProjectUrl | empty | |
| IconUrl | PackageIconUrl | empty | |
| Marcas | PackageTags | empty | Marcas são delimitadas por ponto e vírgula. |
| ReleaseNotes | PackageReleaseNotes | empty | |
| Repositório/URL | RepositoryUrl | empty | URL do repositório usada para clonar ou recuperar o código-fonte. Exemplo *https://github.com/NuGet/NuGet.Client.git* |
| Repositório/tipo | RepositoryType | empty | Tipo de repositório. Exemplos: *git*, *TFS*. |
| Repositório/Branch | RepositoryBranch | empty | Informações opcionais da ramificação do repositório. *RepositoryUrl* também deve ser especificado para que essa propriedade seja incluída. Exemplo: *Master* (NuGet 4.7.0 +) |
| Repositório/confirmação | RepositoryCommit | empty | Confirmação opcional do repositório ou conjunto de alterações para indicar de qual fonte o pacote foi criado. *RepositoryUrl* também deve ser especificado para que essa propriedade seja incluída. Exemplo: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +) |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| Resumo | Sem suporte | | |

### <a name="pack-target-inputs"></a>pack target inputs

- IsPackable
- SuppressDependenciesWhenPacking
- PackageVersion
- PackageId
- Autores
- Descrição
- Copyright
- PackageRequireLicenseAcceptance
- DevelopmentDependency
- PackageLicenseExpression
- PackageLicenseFile
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
- RepositoryBranch
- RepositoryCommit
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

### <a name="suppress-dependencies"></a>Suprimir dependências

Para suprimir dependências de pacote do pacote NuGet `SuppressDependenciesWhenPacking` gerado `true` , defina como que permitirá ignorar todas as dependências do arquivo nupkg gerado.

### <a name="packageiconurl"></a>PackageIconUrl

Como parte da alteração do [problema do NuGet 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` eventualmente será alterado para `PackageIconUri` e pode ser um caminho relativo para um arquivo de ícone que será incluído na raiz do pacote resultante.

### <a name="output-assemblies"></a>Assemblies de saída

O `nuget pack` copia arquivos de saída com extensões `.exe`, `.dll`, `.xml`, `.winmd`, `.json` e `.pri`. Os arquivos de saída que são copiados dependem do que o MSBuild fornece do destino `BuiltOutputProjectGroup`.

Há duas propriedades de MSBuild que você pode usar em seu arquivo de projeto ou a linha de comando para controlar onde ficam os assemblies de saída:

- `IncludeBuildOutput`: Um booliano que determina se os assemblies de saída de compilação devem ser incluídos no pacote.
- `BuildOutputTargetFolder`: Especifica a pasta na qual os assemblies de saída devem ser colocados. Os assemblies de saída (e outros arquivos de saída) são copiados para suas respectivas pastas de estrutura.

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
> Além de itens de Conteúdo, os metadados `<Pack>` e `<PackagePath>` também podem ser definidos em arquivos com uma ação de Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource ou None.
>
> Para o pacote acrescentar o nome de arquivo ao caminho do pacote ao usar padrões glob, seu caminho de pacote deve terminar com o caractere separador de pasta, caso contrário, o caminho do pacote será tratado como o caminho completo, incluindo o nome do arquivo.

### <a name="includesymbols"></a>IncludeSymbols

Ao usar o `MSBuild -t:pack -p:IncludeSymbols=true`, os arquivos `.pdb` correspondentes são copiados junto com outros arquivos de saída (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`). Observe que a configuração `IncludeSymbols=true` cria um pacote regular *e* um pacote de símbolos.

### <a name="includesource"></a>IncludeSource

Isso é o mesmo que `IncludeSymbols`, exceto que também copia os arquivos de origem com arquivos `.pdb`. Todos os arquivos do tipo `Compile` são copiadas para `src\<ProjectName>\`, preservando a estrutura de pastas do caminho relativo no pacote resultante. O mesmo também ocorre para arquivos de origem de qualquer `ProjectReference` que tem `TreatAsPackageReference` definido como `false`.

Se um arquivo do tipo Compilação estiver fora da pasta de projeto, ele será adicionado apenas a `src\<ProjectName>\`.

### <a name="packing-a-license-expression-or-a-license-file"></a>Empacotando uma expressão de licença ou um arquivo de licença

Ao usar uma expressão de licença, a propriedade PackageLicenseExpression deve ser usada. 
[Exemplo de expressão de licença](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

[Saiba mais sobre as expressões de licença e as licenças que são aceitas pelo NuGet.org](nuspec.md#license).

Ao empacotar um arquivo de licença, você precisa usar a propriedade PackageLicenseFile para especificar o caminho do pacote, em relação à raiz do pacote. Além disso, você precisa certificar-se de que o arquivo está incluído no pacote. Por exemplo:

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```
[Exemplo de arquivo de licença](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).

### <a name="istool"></a>IsTool

Ao usar `MSBuild -t:pack -p:IsTool=true`, todos os arquivos de saída, conforme especificado no cenário [Assemblies de saída](#output-assemblies), são copiados para a pasta `tools` em vez da pasta `lib`. Observe que isso é diferente de um `DotNetCliTool` que é especificado pela configuração do `PackageType` no arquivo `.csproj`.

### <a name="packing-using-a-nuspec"></a>Empacotamento usando um .nuspec

Embora seja recomendável [incluir todas as propriedades](../reference/msbuild-targets.md#pack-target) que normalmente estão no `.nuspec` arquivo no arquivo de projeto, você pode optar por usar um `.nuspec` arquivo para empacotar seu projeto. Para um projeto de estilo não-SDK que usa `PackageReference`o, você deve `NuGet.Build.Tasks.Pack.targets` importar para que a tarefa de pacote possa ser executada. Você ainda precisa restaurar o projeto antes de poder empacotar um arquivo nuspec. (Um projeto no estilo SDK inclui os destinos do pacote por padrão.)

A estrutura de destino do arquivo de projeto é irrelevante e não é usada ao empacotar um nuspec. As três propriedades MSBuild a seguir são relevantes para empacotamento usando um `.nuspec`:

1. `NuspecFile`: caminho relativo ou absoluto para o arquivo `.nuspec` que está sendo usado para o empacotamento.
1. `NuspecProperties`: uma lista separada por ponto e vírgula de pares chave/valor. Devido à maneira como a análise de linha de comando do MSBuild funciona, várias propriedades precisam ser especificadas da seguinte maneira: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.  
1. `NuspecBasePath`: Caminho base do `.nuspec` arquivo.

Se estiver usando `dotnet.exe` para empacotar seu projeto, use um comando como o seguinte:

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Se estiver usando o MSBuild para empacotar seu projeto, use um comando como o seguinte:

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Observe que empacotar um nuspec usando dotNet. exe ou MSBuild também leva a criar o projeto por padrão. Isso pode ser evitado passando ```--no-build``` a propriedade para dotnet. exe, que é o equivalente à ```<NoBuild>true</NoBuild> ``` configuração em seu arquivo de projeto, juntamente ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` com a configuração no arquivo de projeto.

Um exemplo de um arquivo *. csproj* para empacotar um arquivo nuspec é:

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <NoBuild>true</NoBuild>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <NuspecFile>PATH_TO_NUSPEC_FILE</NuspecFile>
    <NuspecProperties>add nuspec properties here</NuspecProperties>
    <NuspecBasePath>optional to provide</NuspecBasePath>
  </PropertyGroup>
</Project>
```

### <a name="advanced-extension-points-to-create-customized-package"></a>Pontos de extensão avançados para criar pacote personalizado

O `pack` destino fornece dois pontos de extensão que são executados na compilação interna, específica da estrutura de destino. Os pontos de extensão dão suporte à inclusão de conteúdo específico da estrutura de destino e assemblies em um pacote:

- `TargetsForTfmSpecificBuildOutput`alvo Use para arquivos dentro da `lib` pasta ou de uma pasta especificada `BuildOutputTargetFolder`usando.
- `TargetsForTfmSpecificContentInPackage`alvo Use para arquivos fora do `BuildOutputTargetFolder`.

#### <a name="targetsfortfmspecificbuildoutput"></a>TargetsForTfmSpecificBuildOutput

Escreva um destino personalizado e especifique-o como o valor da `$(TargetsForTfmSpecificBuildOutput)` propriedade. Para todos os arquivos que precisam entrar em `BuildOutputTargetFolder` (lib por padrão), o destino deve gravar esses arquivos no grupo `BuildOutputInPackage` de itens e definir os dois valores de metadados a seguir:

- `FinalOutputPath`: O caminho absoluto do arquivo; Se não for fornecido, a identidade será usada para avaliar o caminho de origem.
- `TargetPath`:  Adicional Defina quando o arquivo precisa entrar em uma subpasta no `lib\<TargetFramework>` , como assemblies satélite que estão sob suas respectivas pastas de cultura. O padrão é o nome do arquivo.

Exemplo:

```xml
<PropertyGroup>
  <TargetsForTfmSpecificBuildOutput>$(TargetsForTfmSpecificBuildOutput);GetMyPackageFiles</TargetsForTfmSpecificBuildOutput>
</PropertyGroup>

<Target Name="GetMyPackageFiles">
  <ItemGroup>
    <BuildOutputInPackage Include="$(OutputPath)cs\$(AssemblyName).resources.dll">
        <TargetPath>cs</TargetPath>
    </BuildOutputInPackage>
  </ItemGroup>
</Target>
```

#### <a name="targetsfortfmspecificcontentinpackage"></a>TargetsForTfmSpecificContentInPackage

Escreva um destino personalizado e especifique-o como o valor da `$(TargetsForTfmSpecificContentInPackage)` propriedade. Para todos os arquivos a serem incluídos no pacote, o destino deve gravar esses arquivos no grupo `TfmSpecificPackageFile` de itens e definir os seguintes metadados opcionais:

- `PackagePath`: Caminho em que o arquivo deve ser apresentado no pacote. O NuGet emitirá um aviso se mais de um arquivo for adicionado ao mesmo caminho de pacote.
- `BuildAction`: A ação de compilação a ser atribuída ao arquivo, necessária somente se o caminho do pacote estiver `contentFiles` na pasta. O padrão é "None".

Um exemplo:
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name="CustomContentTarget">
  <ItemGroup>
    <TfmSpecificPackageFile Include="abc.txt">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include="Extensions/ext.txt" Condition="'$(TargetFramework)' == 'net46'">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a>restore target

`MSBuild -t:restore` (que `nuget restore` e `dotnet restore` usam com projetos do .NET Core), restaura pacotes referenciados no arquivo de projeto da seguinte maneira:

1. Ler todas as referências projeto a projeto
1. Ler as propriedades do projeto para localizar a pasta intermediária e as estruturas de destino
1. Transmitir dados do MSBuild para NuGet. Build. Tasks. dll
1. Executar restauração
1. Baixar os pacotes
1. Gravar arquivo de ativos, destinos e objetos

O `restore` destino funciona **apenas** para projetos que usam o formato PackageReference. Ele não **funciona para** projetos que usam o `packages.config` formato; em vez disso, use a [restauração do NuGet](../reference/cli-reference/cli-ref-restore.md) .

### <a name="restore-properties"></a>Restaurar propriedades

Configurações de restauração adicionais podem vir de propriedades MSBuild no arquivo de projeto. Os valores também podem ser definidos na linha de comando usando a opção `-p:` (consulte os Exemplos abaixo).

| Propriedade | Descrição |
|--------|--------|
| RestoreSources | Uma lista delimitada por ponto e vírgula de origens de pacote. |
| RestorePackagesPath | Caminho da pasta dos pacotes do usuário. |
| RestoreDisableParallel | Limite os downloads para um de cada vez. |
| RestoreConfigFile | Caminho para um arquivo `Nuget.Config` a ser aplicado. |
| RestoreNoCache | Se for true, evita o uso de pacotes armazenados em cache. Consulte [Gerenciando os pacotes globais e as pastas de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| RestoreIgnoreFailedSources | Se verdadeiro, ignora origens de pacote com falha ou ausentes. |
| RestoreFallbackFolders | Pastas de fallback, usadas da mesma maneira que a pasta pacotes de usuário é usada. |
| RestoreAdditionalProjectSources | Fontes adicionais a serem usadas durante a restauração. |
| RestoreAdditionalProjectFallbackFolders | Pastas de fallback adicionais a serem usadas durante a restauração. |
| RestoreAdditionalProjectFallbackFoldersExcludes | Exclui as pastas de fallback especificadas em`RestoreAdditionalProjectFallbackFolders` |
| RestoreTaskAssemblyFile | Caminho para `NuGet.Build.Tasks.dll`. |
| RestoreGraphProjectInput | Lista separada por ponto e vírgula de projetos a serem restaurados, que devem conter caminhos absolutos. |
| RestoreUseSkipNonexistentTargets  | Quando os projetos são coletados via MSBuild, ele determina se eles são coletados usando a `SkipNonexistentTargets` otimização. Quando não definido, o padrão é `true`. A conseqüência é um comportamento com falha rápida quando os destinos de um projeto não podem ser importados. |
| MSBuildProjectExtensionsPath | Pasta de saída, padronizando `BaseIntermediateOutputPath` para e `obj` a pasta. |

#### <a name="examples"></a>Exemplos

Linha de comando:

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

Arquivo de projeto:

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a>Restaurar saídas

A restauração cria os seguintes arquivos na pasta `obj` de build:

| Arquivo | Descrição |
|--------|--------|
| `project.assets.json` | Contém o grafo de dependência de todas as referências de pacote. |
| `{projectName}.projectFileExtension.nuget.g.props` | Referências a objetos do MSBuild contidos em pacotes |
| `{projectName}.projectFileExtension.nuget.g.targets` | Referências a destinos do MSBuild contidos em pacotes |

### <a name="restoring-and-building-with-one-msbuild-command"></a>Restaurando e compilando com um comando do MSBuild

Devido ao fato de que o NuGet pode restaurar pacotes que desativam destinos e props do MSBuild, as avaliações de restauração e compilação são executadas com propriedades globais diferentes.
Isso significa que o seguinte terá um comportamento imprevisível e geralmente incorreto.

```cli
msbuild -t:restore,build
```

 Em vez disso, a abordagem recomendada é:

```cli
msbuild -t:build -restore
```

A mesma lógica se aplica a outros destinos semelhantes `build`a.

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
