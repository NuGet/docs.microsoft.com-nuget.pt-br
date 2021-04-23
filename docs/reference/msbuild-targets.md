---
title: NuGet empacotar e restaurar como MSBuild destinos
description: NuGet o pacote e a restauração podem funcionar diretamente como MSBuild destinos com NuGet 4.0 +.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
no-loc:
- NuGet
- MSBuild
- .nuspec
- nuspec
ms.openlocfilehash: 0a10a6f1e4c71903232281c25a6c4b6bbc65fb34
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901479"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>NuGet empacotar e restaurar como MSBuild destinos

*NuGet 4.0 +*

Com o formato [PackageReference](../consume-packages/package-references-in-project-files.md) , o NuGet 4.0 + pode armazenar todos os metadados do manifesto diretamente dentro de um arquivo de projeto em vez de usar um `.nuspec` arquivo separado.

Com MSBuild o 15.1 +, NuGet também é um cidadão de primeira classe MSBuild com `pack` os `restore` destinos e, conforme descrito abaixo. Esses destinos permitem que você trabalhe com NuGet como faria com qualquer outra MSBuild tarefa ou destino. Para obter instruções sobre como criar um NuGet pacote usando o MSBuild , consulte [criar um NuGet pacote usando MSBuild o ](../create-packages/creating-a-package-msbuild.md). (Para NuGet 3. x e anteriores, você usará os comandos [Pack](../reference/cli-reference/cli-ref-pack.md) e [Restore](../reference/cli-reference/cli-ref-restore.md) por meio da NuGet CLI.)

## <a name="target-build-order"></a>Ordem de build de destino

Como `pack` e `restore` são  MSBuild destinos, você pode acessá-los para aprimorar seu fluxo de trabalho. Por exemplo, digamos que você deseja copiar o pacote para um compartilhamento de rede depois de empacotá-lo. Você pode fazer isso adicionando o seguinte ao seu arquivo de projeto:

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

Da mesma forma, você pode escrever uma MSBuild tarefa, escrever seu próprio destino e consumir NuGet as propriedades na MSBuild tarefa.

> [!NOTE]
> `$(OutputPath)` é relativo e espera que você esteja executando o comando da raiz do projeto.

## <a name="pack-target"></a>pack target

Para projetos .NET que usam o `PackageReference` formato, o uso de `msbuild -t:pack` desenha entradas do arquivo de projeto a ser usado na criação de um NuGet pacote.

A tabela a seguir descreve as MSBuild Propriedades que podem ser adicionadas a um arquivo de projeto dentro do primeiro `<PropertyGroup>` nó. Você pode fazer essas edições facilmente no Visual Studio 2017 e posterior clicando com o botão direito do mouse no projeto e selecionando **Editar {project_name}** no menu de contexto. Para sua conveniência, a tabela é organizada pela propriedade equivalente em um [ `.nuspec` arquivo](../reference/nuspec.md).

> [!NOTE]
> `Owners``Summary`as propriedades e de `.nuspec` não têm suporte com MSBuild .

| Atributo/ nuspec valor | MSBuild Propriedade | Padrão | Observações |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | `$(AssemblyName)` de MSBuild |
| `Version` | `PackageVersion` | Versão | Isso é compatível com semver, por exemplo, `1.0.0` `1.0.0-beta` ou `1.0.0-beta-00345` |
| `VersionPrefix` | `PackageVersionPrefix` | vazio | Configurando `PackageVersion` substituições `PackageVersionPrefix` |
| `VersionSuffix` | `PackageVersionSuffix` | vazio | `$(VersionSuffix)` de MSBuild . Configurando `PackageVersion` substituições `PackageVersionSuffix` |
| `Authors` | `Authors` | Nome do usuário atual | Uma lista separada por ponto-e-vírgula de autores de pacotes, que correspondem aos nomes de perfil em nuget.org. Eles são exibidos na NuGet Galeria no NuGet.org e são usados para fazer referência cruzada de pacotes pelos mesmos autores. |
| `Owners` | N/D | Não presente em nuspec | |
| `Title` | `Title` | O `PackageId` | Um título amigável do pacote, geralmente usado em exibições de interface do usuário como em nuget.org e no Gerenciador de Pacotes do Visual Studio. |
| `Description` | `Description` | “Package Description” | Uma descrição longa para o manifesto do assembly. Se `PackageDescription` não for especificado, essa propriedade também será usada como a descrição do pacote. |
| `Copyright` | `Copyright` | vazio | Detalhes sobre direitos autorais do pacote. |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | Um valor booliano que especifica se o cliente deve solicitar que o consumidor aceite a licença do pacote antes de instalá-lo. |
| `license` | `PackageLicenseExpression` | vazio | Corresponde ao `<license type="expression">`. Consulte [empacotando uma expressão de licença ou um arquivo de licença](#packing-a-license-expression-or-a-license-file). |
| `license` | `PackageLicenseFile` | vazio | Caminho para um arquivo de licença dentro do pacote se você estiver usando uma licença personalizada ou uma licença que não tenha sido atribuída a um identificador SPDX. Você precisa empacotar explicitamente o arquivo de licença referenciado. Corresponde ao `<license type="file">`. Consulte [empacotando uma expressão de licença ou um arquivo de licença](#packing-a-license-expression-or-a-license-file). |
| `LicenseUrl` | `PackageLicenseUrl` | vazio | O `PackageLicenseUrl` foi preterido. Use `PackageLicenseExpression` ou `PackageLicenseFile` em vez disso. |
| `ProjectUrl` | `PackageProjectUrl` | vazio | |
| `Icon` | `PackageIcon` | vazio | Um caminho para uma imagem no pacote a ser usado como um ícone de pacote. Você precisa empacotar explicitamente o arquivo de imagem do ícone referenciado. Para obter mais informações, consulte [empacotando um arquivo de imagem de ícone](#packing-an-icon-image-file) e [ `icon` metadados](./nuspec.md#icon). |
| `IconUrl` | `PackageIconUrl` | vazio | `PackageIconUrl` é preterido em favor do `PackageIcon` . No entanto, para obter a melhor experiência de nível inferior, você deve especificar, `PackageIconUrl` além do `PackageIcon` . |
| `Readme` | `PackageReadmeFile` | vazio | Você precisa empacotar explicitamente o arquivo Leiame referenciado.|
| `Tags` | `PackageTags` | vazio | Uma lista delimitada por ponto e vírgula de marcas que designam o pacote. |
| `ReleaseNotes` | `PackageReleaseNotes` | vazio | Notas de versão do projeto. |
| `Repository/Url` | `RepositoryUrl` | vazio | URL do repositório usada para clonar ou recuperar o código-fonte. Exemplo: *https://github.com/ NuGet / NuGet . Client. git*. |
| `Repository/Type` | `RepositoryType` | vazio | Tipo de repositório. Exemplos: `git` (padrão), `tfs` . |
| `Repository/Branch` | `RepositoryBranch` | vazio | Informações opcionais da ramificação do repositório. `RepositoryUrl` também deve ser especificado para que essa propriedade seja incluída. Exemplo: *Master* ( NuGet 4.7.0 +). |
| `Repository/Commit` | `RepositoryCommit` | vazio | Confirmação opcional do repositório ou conjunto de alterações para indicar de qual fonte o pacote foi criado. `RepositoryUrl` também deve ser especificado para que essa propriedade seja incluída. Exemplo: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +). |
| `PackageType` | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| `Summary` | Sem suporte | | |

### <a name="pack-target-inputs"></a>pack target inputs

| Propriedade | Descrição |
| - | - |
| `IsPackable` | Um valor booliano que especifica se o projeto pode ser empacotado. O valor padrão é `true`. |
| `SuppressDependenciesWhenPacking` | Defina como `true` para suprimir as dependências de pacote do NuGet pacote gerado. |
| `PackageVersion` | Especifica a versão que o pacote resultante terá. Aceita todas as formas de NuGet cadeia de caracteres de versão. O padrão é o valor `$(Version)`, ou seja, da propriedade `Version` no projeto. |
| `PackageId` | Especifica o nome para o pacote resultante. Se não for especificado, a operação `pack` usará como padrão o `AssemblyName` ou o nome do diretório como o nome do pacote. |
| `PackageDescription` | Uma descrição longa do pacote para exibição de interface do usuário. |
| `Authors` | Uma lista separada por ponto-e-vírgula de autores de pacotes, que correspondem aos nomes de perfil em nuget.org. Eles são exibidos na NuGet Galeria no NuGet.org e são usados para fazer referência cruzada de pacotes pelos mesmos autores. |
| `Description` | Uma descrição longa para o manifesto do assembly. Se `PackageDescription` não for especificado, essa propriedade também será usada como a descrição do pacote. |
| `Copyright` | Detalhes sobre direitos autorais do pacote. |
| `PackageRequireLicenseAcceptance` | Um valor booliano que especifica se o cliente deve solicitar que o consumidor aceite a licença do pacote antes de instalá-lo. O padrão é `false`. |
| `DevelopmentDependency` | Um valor booliano que especifica se o pacote está marcado como uma dependência somente de desenvolvimento, o que impede que o pacote seja incluído como uma dependência em outros pacotes. Com `PackageReference` ( NuGet 4.8 +), esse sinalizador também significa que os ativos de tempo de compilação são excluídos da compilação. Para obter mais informações, confira [Suporte do DevelopmentDependency para PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference). |
| `PackageLicenseExpression` | Uma expressão ou um [identificador de licença SPDX](https://spdx.org/licenses/) , por exemplo, `Apache-2.0` . Para obter mais informações, consulte [empacotando uma expressão de licença ou um arquivo de licença](#packing-a-license-expression-or-a-license-file). |
| `PackageLicenseFile` | Caminho para um arquivo de licença dentro do pacote se você estiver usando uma licença personalizada ou uma licença que não tenha sido atribuída a um identificador SPDX. |
| `PackageLicenseUrl` | O `PackageLicenseUrl` foi preterido. Use `PackageLicenseExpression` ou `PackageLicenseFile` em vez disso. |
| `PackageProjectUrl` | |
| `PackageIcon` | Especifica o caminho do ícone de pacote, relativo à raiz do pacote. Para obter mais informações, consulte [empacotando um arquivo de imagem de ícone](#packing-an-icon-image-file). |
| `PackageReleaseNotes` | Notas de versão do projeto. |
| `PackageReadmeFile` | Leiame do pacote. |
| `PackageTags` | Uma lista delimitada por ponto e vírgula de marcas que designam o pacote. |
| `PackageOutputPath` | Determina o caminho de saída no qual o pacote empacotado será solto. O padrão é `$(OutputPath)`. |
| `IncludeSymbols` | Esse valor booliano indica se o pacote deve criar um pacote de símbolos adicionais quando o projeto é empacotado. O formato do pacote de símbolos é controlado pela propriedade `SymbolPackageFormat`. Para obter mais informações, consulte [IncludeSymbols](#includesymbols). |
| `IncludeSource` | Esse valor booliano indica se o processo do pacote deve criar um pacote de origem. O pacote de origem contém o código-fonte da biblioteca, bem como arquivos PDB. Os arquivos de origem são colocados no diretório `src/ProjectName`, no arquivo de pacote resultante. Para obter mais informações, consulte [includename](#includesource). |
| `PackageType` | |
| `IsTool` | Especifica se todos os arquivos de saída são copiados para a pasta *tools* em vez da pasta *lib*. Para obter mais informações, consulte [istool](#istool). |
| `RepositoryUrl` | URL do repositório usada para clonar ou recuperar o código-fonte. Exemplo: *https://github.com/ NuGet / NuGet . Client. git*. |
| `RepositoryType` | Tipo de repositório. Exemplos: `git` (padrão), `tfs` . |
| `RepositoryBranch` | Informações opcionais da ramificação do repositório. `RepositoryUrl` também deve ser especificado para que essa propriedade seja incluída. Exemplo: *Master* ( NuGet 4.7.0 +). |
| `RepositoryCommit` | Confirmação opcional do repositório ou conjunto de alterações para indicar de qual fonte o pacote foi criado. `RepositoryUrl` também deve ser especificado para que essa propriedade seja incluída. Exemplo: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +). |
| `SymbolPackageFormat` | Especifica o formato do pacote de símbolos. Se "Symbols. nupkg", um pacote de símbolos herdados será criado com uma extensão *. Symbols. nupkg* contendo PDBs, DLLs e outros arquivos de saída. Se "snupkg", um pacote de símbolos snupkg será criado contendo os PDBs portáteis. O padrão é "Symbols. nupkg". |
| `NoPackageAnalysis` | Especifica que o `pack` não deve executar a análise de pacote depois de criar o pacote. |
| `MinClientVersion` | Especifica a versão mínima do NuGet cliente que pode instalar este pacote, imposta por nuget.exe e o Gerenciador de pacotes do Visual Studio. |
| `IncludeBuildOutput` | Esse valor booliano especifica se os assemblies de saída da compilação devem ser empacotados no arquivo *. nupkg* ou não. |
| `IncludeContentInPack` | Esse valor booliano especifica se os itens que têm um tipo de `Content` são incluídos automaticamente no pacote resultante. O padrão é `true`. |
| `BuildOutputTargetFolder` | Especifica a pasta para colocar os assemblies de saída. Os assemblies de saída (e outros arquivos de saída) são copiados para suas respectivas pastas de estrutura. Para obter mais informações, consulte [assemblies de saída](#output-assemblies). |
| `ContentTargetFolders` | Especifica o local padrão de onde todos os arquivos de conteúdo devem ir se `PackagePath` não forem especificados para eles. O valor padrão é “content;contentFiles”. Para obter mais informações, consulte [Incluindo conteúdo em um pacote](#including-content-in-a-package). |
| `NuspecFile` | Caminho relativo ou absoluto para o *.nuspec* arquivo que está sendo usado para empacotamento. Se especificado, ele será usado **exclusivamente** para informações de empacotamento e quaisquer informações nos projetos não serão usadas. Para obter mais informações, consulte [empacotando .nuspec usando um ](#packing-using-a-nuspec-file). |
| `NuspecBasePath` | Caminho base do *.nuspec* arquivo. Para obter mais informações, consulte [empacotando .nuspec usando um ](#packing-using-a-nuspec-file). |
| `NuspecProperties` | Lista separada por ponto e vírgula de pares chave-valor. Para obter mais informações, consulte [empacotando .nuspec usando um ](#packing-using-a-nuspec-file). |

## <a name="pack-scenarios"></a>pack scenarios

### <a name="suppressing-dependencies"></a>Suprimindo dependências

Para suprimir as dependências de pacote do NuGet pacote gerado, defina `SuppressDependenciesWhenPacking` como `true` que permitirá ignorar todas as dependências do arquivo nupkg gerado.

### `PackageIconUrl`

`PackageIconUrl` é preterido em favor da [`PackageIcon`](#packageicon) propriedade. A partir NuGet do 5,3 e do Visual Studio 2019 versão 16,3, `pack` o gerará o aviso [NU5048](./errors-and-warnings/nu5048.md) se os metadados do pacote especificarem apenas `PackageIconUrl` .

### `PackageIcon`

> [!Tip]
> Para manter a compatibilidade com versões anteriores com clientes e fontes que ainda não dão suporte `PackageIcon` , especifique `PackageIcon` e `PackageIconUrl` . O Visual Studio dá suporte a `PackageIcon` pacotes provenientes de uma fonte baseada em pasta.

#### <a name="packing-an-icon-image-file"></a>Empacotando um arquivo de imagem de ícone

Ao empacotar um arquivo de imagem de ícone, use `PackageIcon` a propriedade para especificar o caminho do arquivo de ícone, em relação à raiz do pacote. Além disso, certifique-se de que o arquivo está incluído no pacote. O tamanho do arquivo de imagem é limitado a 1 MB. Os formatos de arquivo com suporte incluem JPEG e PNG. Recomendamos uma resolução de imagem de 128x128.

Por exemplo:

```xml
<PropertyGroup>
    ...
    <PackageIcon>icon.png</PackageIcon>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="images\icon.png" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

[Exemplo de ícone de pacote](https://github.com/NuGet/Samples/tree/main/PackageIconExample).

Para o nuspec equivalente, dê uma olhada na [ nuspec referência para o ícone](nuspec.md#icon).

### <a name="packagereadmefile"></a>PackageReadmeFile

*Com suporte com o **NuGet 5.10.0 Preview 2**  /  **.NET 5.0.3** e posterior*

Ao empacotar um arquivo Leiame, você precisa usar a `PackageReadmeFile` propriedade para especificar o caminho do pacote, em relação à raiz do pacote. Além disso, você precisa certificar-se de que o arquivo está incluído no pacote. Os formatos de arquivo com suporte incluem apenas redução (*. MD*).

Por exemplo:

```xml
<PropertyGroup>
    ...
    <PackageReadmeFile>readme.md</PackageReadmeFile>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="docs\readme.md" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

Para o nuspec equivalente, dê uma olhada na [ nuspec referência do Leiame](nuspec.md#readme).

### <a name="output-assemblies"></a>Assemblies de saída

O `nuget pack` copia arquivos de saída com extensões `.exe`, `.dll`, `.xml`, `.winmd`, `.json` e `.pri`. Os arquivos de saída copiados dependem do que o MSBuild fornece do `BuiltOutputProjectGroup` destino.

Há duas MSBuild  Propriedades que você pode usar em seu arquivo de projeto ou linha de comando para controlar onde os assemblies de saída vão:

- `IncludeBuildOutput`: um valor booliano que determina se os assemblies de saída de build devem ser incluídos no pacote.
- `BuildOutputTargetFolder`: especifica a pasta na qual os assemblies de saída devem ser colocados. Os assemblies de saída (e outros arquivos de saída) são copiados para suas respectivas pastas de estrutura.

### <a name="package-references"></a>Referências de pacote

Consulte [Referências de pacote em arquivos de projeto](../consume-packages/package-references-in-project-files.md).

### <a name="project-to-project-references"></a>Referências de projeto a projeto

As referências de projeto para projeto são consideradas por padrão como NuGet referências de pacote. Por exemplo:

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

Se você quiser copiar todo o conteúdo para apenas uma pasta (s) raiz específica (em vez de `content` e `contentFiles` ambos), poderá usar a MSBuild propriedade `ContentTargetFolders` , que usa como padrão "Content; contentFiles", mas pode ser definida como qualquer outro nome de pasta. Observe que só especificar “contentFiles” em `ContentTargetFolders` coloca os arquivos em `contentFiles\any\<target_framework>` ou `contentFiles\<language>\<target_framework>` com base em `buildAction`.

`PackagePath` pode ser um conjunto de caminhos de destino separados por ponto e vírgula. Especificar um caminho de pacote vazio adicionaria o arquivo à raiz do pacote. Por exemplo, o seguinte adiciona `libuv.txt` a `content\myfiles`, `content\samples` e a raiz do pacote:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

Há também uma MSBuild propriedade `$(IncludeContentInPack)` , que usa como padrão `true` . Se isso for definido como `false` em qualquer projeto, o conteúdo desse projeto não está incluso no pacote do nuget.

Outros metadados específicos do pacote que você pode definir em qualquer um dos itens acima incluem ```<PackageCopyToOutput>``` e ```<PackageFlatten>``` quais conjuntos ```CopyToOutput``` e ```Flatten``` valores na ```contentFiles``` entrada na saída nuspec .

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

Ao usar uma expressão de licença, use a `PackageLicenseExpression` propriedade. Para obter um exemplo, consulte [exemplo de expressão de licença](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

Para saber mais sobre as expressões de licença e as licenças que são aceitas pelo NuGet . org, consulte [metadados de licença](nuspec.md#license).

Ao empacotar um arquivo de licença, use `PackageLicenseFile` a propriedade para especificar o caminho do pacote, em relação à raiz do pacote. Além disso, certifique-se de que o arquivo está incluído no pacote. Por exemplo:

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

Para obter um exemplo, consulte [exemplo de arquivo de licença](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).

> [!NOTE]
> Somente um de `PackageLicenseExpression` , `PackageLicenseFile` e `PackageLicenseUrl` pode ser especificado por vez.

### <a name="packing-a-file-without-an-extension"></a>Empacotando um arquivo sem uma extensão

Em alguns cenários, como ao empacotar um arquivo de licença, talvez você queira incluir um arquivo sem uma extensão.
Por motivos históricos, NuGet  &  MSBuild trate os caminhos sem uma extensão como diretórios.

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

[Arquivo sem um exemplo de extensão](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).

### <a name="istool"></a>IsTool

Ao usar `MSBuild -t:pack -p:IsTool=true`, todos os arquivos de saída, conforme especificado no cenário [Assemblies de saída](#output-assemblies), são copiados para a pasta `tools` em vez da pasta `lib`. Observe que isso é diferente de um `DotNetCliTool` que é especificado pela configuração do `PackageType` no arquivo `.csproj`.

### <a name="packing-using-a-nuspec-file"></a>Empacotamento usando um `.nuspec` arquivo

Embora seja recomendável [incluir todas as propriedades](../reference/msbuild-targets.md#pack-target) que normalmente estão no `.nuspec` arquivo no arquivo de projeto, você pode optar por usar um `.nuspec` arquivo para empacotar seu projeto. Para um projeto de estilo não-SDK que usa `PackageReference` o, você deve importar `NuGet.Build.Tasks.Pack.targets` para que a tarefa de pacote possa ser executada. Você ainda precisa restaurar o projeto antes de poder empacotar um nuspec arquivo. (Um projeto no estilo SDK inclui os destinos do pacote por padrão.)

A estrutura de destino do arquivo de projeto é irrelevante e não é usada ao empacotar um nuspec . As três propriedades a seguir MSBuild são relevantes para empacotamento usando um `.nuspec` :

1. `NuspecFile`: caminho relativo ou absoluto para o arquivo `.nuspec` que está sendo usado para o empacotamento.
1. `NuspecProperties`: uma lista separada por ponto e vírgula de pares chave/valor. Devido à maneira como a MSBuild análise da linha de comando funciona, várias propriedades devem ser especificadas da seguinte maneira: `-p:NuspecProperties="key1=value1;key2=value2"` .  
1. `NuspecBasePath`: o caminho base para o arquivo `.nuspec`.

Se estiver usando `dotnet.exe` para empacotar seu projeto, use um comando como o seguinte:

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Se estiver usando MSBuild para empacotar seu projeto, use um comando como o seguinte:

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Observe que empacotar um nuspec usando dotnet.exe ou o MSBuild também leva a criar o projeto por padrão. Isso pode ser evitado passando ```--no-build``` a propriedade para dotnet.exe, que é o equivalente à configuração ```<NoBuild>true</NoBuild> ``` em seu arquivo de projeto, juntamente com ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` a configuração no arquivo de projeto.

Um exemplo de um arquivo *. csproj* para empacotar um nuspec arquivo é:

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

- `TargetsForTfmSpecificBuildOutput` destino: Use para arquivos dentro da `lib` pasta ou de uma pasta especificada usando `BuildOutputTargetFolder` .
- `TargetsForTfmSpecificContentInPackage` destino: Use para arquivos fora do `BuildOutputTargetFolder` .

#### `TargetsForTfmSpecificBuildOutput`

Escreva um destino personalizado e especifique-o como o valor da `$(TargetsForTfmSpecificBuildOutput)` propriedade. Para todos os arquivos que precisam entrar em `BuildOutputTargetFolder` (lib por padrão), o destino deve gravar esses arquivos no grupo de `BuildOutputInPackage` itens e definir os dois valores de metadados a seguir:

- `FinalOutputPath`: O caminho absoluto do arquivo; Se não for fornecido, a identidade será usada para avaliar o caminho de origem.
- `TargetPath`: (Opcional) defina quando o arquivo precisa entrar em uma subpasta no `lib\<TargetFramework>` , como assemblies satélite que estão em suas respectivas pastas de cultura. O padrão é o nome do arquivo.

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

#### `TargetsForTfmSpecificContentInPackage`

Escreva um destino personalizado e especifique-o como o valor da `$(TargetsForTfmSpecificContentInPackage)` propriedade. Para todos os arquivos a serem incluídos no pacote, o destino deve gravar esses arquivos no grupo de `TfmSpecificPackageFile` itens e definir os seguintes metadados opcionais:

- `PackagePath`: Caminho em que o arquivo deve ser apresentado no pacote. NuGet emite um aviso se mais de um arquivo for adicionado ao mesmo caminho de pacote.
- `BuildAction`: A ação de compilação a ser atribuída ao arquivo, necessária somente se o caminho do pacote estiver na `contentFiles` pasta. O padrão é "None".

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
1. Passar MSBuild dados para NuGet.Build.Tasks.dll
1. Executar restauração
1. Baixar os pacotes
1. Gravar arquivo de ativos, destinos e objetos

O `restore` destino funciona para projetos que usam o formato PackageReference.
`MSBuild 16.5+` também tem [suporte opcional](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) para o `packages.config` formato.

> [!NOTE]
> O `restore` destino [não deve ser executado](#restoring-and-building-with-one-msbuild-command) em combinação com o `build` destino.

### <a name="restore-properties"></a>Restaurar propriedades

As configurações de restauração adicionais podem vir de MSBuild Propriedades no arquivo de projeto. Os valores também podem ser definidos na linha de comando usando a opção `-p:` (consulte os Exemplos abaixo).

| Propriedade | Descrição |
|--------|--------|
| `RestoreSources` | Uma lista delimitada por ponto e vírgula de origens de pacote. |
| `RestorePackagesPath` | Caminho da pasta dos pacotes do usuário. |
| `RestoreDisableParallel` | Limite os downloads para um de cada vez. |
| `RestoreConfigFile` | Caminho para um arquivo `Nuget.Config` a ser aplicado. |
| `RestoreNoCache` | Se for true, evita o uso de pacotes armazenados em cache. Consulte [Gerenciando os pacotes globais e as pastas de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| `RestoreIgnoreFailedSources` | Se verdadeiro, ignora origens de pacote com falha ou ausentes. |
| `RestoreFallbackFolders` | Pastas de fallback, usadas da mesma maneira que a pasta pacotes de usuário é usada. |
| `RestoreAdditionalProjectSources` | Fontes adicionais a serem usadas durante a restauração. |
| `RestoreAdditionalProjectFallbackFolders` | Pastas de fallback adicionais a serem usadas durante a restauração. |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | Exclui as pastas de fallback especificadas em `RestoreAdditionalProjectFallbackFolders` |
| `RestoreTaskAssemblyFile` | Caminho para `NuGet.Build.Tasks.dll`. |
| `RestoreGraphProjectInput` | Lista separada por ponto e vírgula de projetos a serem restaurados, que devem conter caminhos absolutos. |
| `RestoreUseSkipNonexistentTargets`  | Quando os projetos são coletados por meio MSBuild dele, ele determina se eles são coletados usando a `SkipNonexistentTargets` otimização. Quando não definido, o padrão é `true` . A conseqüência é um comportamento com falha rápida quando os destinos de um projeto não podem ser importados. |
| `MSBuildProjectExtensionsPath` | Pasta de saída, padronizando para `BaseIntermediateOutputPath` e a `obj` pasta. |
| `RestoreForce` | Em projetos baseados em PackageReference, o forçará a resolução de todas as dependências, mesmo que a última restauração tenha sido bem-sucedida. A especificação desse sinalizador é semelhante à exclusão do `project.assets.json` arquivo. Isso não ignora o cache http. |
| `RestorePackagesWithLockFile` | Opta pelo uso de um arquivo de bloqueio. |
| `RestoreLockedMode` | Execute RESTORE no modo bloqueado. Isso significa que a restauração não reavaliará as dependências. |
| `NuGetLockFilePath` | Um local personalizado para o arquivo de bloqueio. O local padrão é ao lado do projeto e é nomeado `packages.lock.json` . |
| `RestoreForceEvaluate` | Força a restauração a recalcular as dependências e atualizar o arquivo de bloqueio sem nenhum aviso. |
| `RestorePackagesConfig` | Uma opção opcional que restaura projetos com packages.config. Suporte `MSBuild -t:restore` apenas com. |
| `RestoreUseStaticGraphEvaluation` | Uma opção opcional para usar a MSBuild avaliação estática do grafo em vez da avaliação padrão. A avaliação estática do grafo é um recurso experimental que é significativamente mais rápido para repositórios e soluções grandes. |

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
| `{projectName}.projectFileExtension.nuget.g.props` | Referências a MSBuild props contidas em pacotes |
| `{projectName}.projectFileExtension.nuget.g.targets` | Referências a MSBuild destinos contidos em pacotes |

### <a name="restoring-and-building-with-one-msbuild-command"></a>Restaurando e compilando com um MSBuild comando

Devido ao fato de que o NuGet pode restaurar pacotes que trazem MSBuild destinos e props, as avaliações de restauração e de compilação são executadas com propriedades globais diferentes.
Isso significa que o seguinte terá um comportamento imprevisível e geralmente incorreto.

```cli
msbuild -t:restore,build
```

 Em vez disso, a abordagem recomendada é:

```cli
msbuild -t:build -restore
```

A mesma lógica se aplica a outros destinos semelhantes a `build` .

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a>Restaurando projetos PackageReference e packages.config com MSBuild

Com o MSBuild packages.config de los +, também há suporte para o `msbuild -t:restore` .

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> `packages.config` a restauração está disponível apenas com o `MSBuild 16.5+` , e não com `dotnet.exe`

### <a name="restoring-with-msbuild-static-graph-evaluation"></a>Restaurando com a MSBuild avaliação estática do grafo

> [!NOTE]
> Com MSBuild o 16.6 +, NuGet adicionou um recurso experimental para usar a avaliação estática do grafo na linha de comando que melhora significativamente o tempo de restauração para repositórios grandes.

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

Como alternativa, você pode habilitá-lo definindo a propriedade em um diretório. Build. props.

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> A partir do Visual Studio 2019. x e NuGet 5. x, esse recurso é considerado experimental e opcional. Siga [ NuGet /Home # 9803](https://github.com/NuGet/Home/issues/9803) para obter detalhes sobre quando esse recurso será habilitado por padrão.

A restauração estática do grafo altera a parte do MSBuild da restauração, a leitura e a avaliação do projeto, mas não o algoritmo de restauração! O algoritmo de restauração é o mesmo em todas as NuGet ferramentas ( NuGet . exe, MSBuild . exe, dotnet.exe e Visual Studio).

Em poucos cenários, a restauração estática do grafo pode se comportar de forma diferente da restauração atual e determinados PackageReferences ou ProjectReferences declarados podem estar ausentes.

Para facilitar sua ideia, como uma verificação única, ao migrar para a restauração estática do grafo, considere a execução:

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

NuGet*não* deve relatar nenhuma alteração. Se você vir uma discrepância, registre um problema em [ NuGet /Home](https://github.com/nuget/home/issues/new).

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