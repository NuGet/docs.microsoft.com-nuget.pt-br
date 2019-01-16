---
title: Referência de arquivo. NuSpec para NuGet
description: O arquivo .nuspec contém metadados de pacote usados ao compilar um pacote e para fornecer informações para os consumidores do pacote.
author: karann-msft
ms.author: karann
ms.date: 08/29/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 009be99a1c6623a00b4bdbe6db3164ca70782212
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324897"
---
# <a name="nuspec-reference"></a>Referência do .nuspec

Um arquivo `.nuspec` é um manifesto XML que contém metadados do pacote. Esse manifesto é usado para compilar o pacote e fornecer informações aos consumidores. O manifesto sempre é incluído em um pacote.

Neste tópico:

- [Formato e esquema geral](#general-form-and-schema)
- [Tokens de substituição](#replacement-tokens) (quando usados com um projeto do Visual Studio)
- [Dependências](#dependencies)
- [Referências de assembly explícitas](#explicit-assembly-references)
- [Referências de assembly de estrutura](#framework-assembly-references)
- [Incluindo arquivos do assembly](#including-assembly-files)
- [Incluindo arquivos de conteúdo](#including-content-files)
- [Arquivos de exemplo do nuspec](#example-nuspec-files)

## <a name="general-form-and-schema"></a>Formato e esquema geral

O arquivo de esquema `nuspec.xsd` atual pode ser encontrado no [repositório GitHub do NuGet](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).

Dentro desse esquema, um arquivo `.nuspec` tem o seguinte formato geral:

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

Para obter uma representação visual do esquema, abra o arquivo de esquema no Visual Studio no modo de Design e clique no link **Gerenciador de Esquema XML**. Como alternativa, abra o arquivo como código, clique com o botão direito do mouse no editor e selecione **Mostrar Gerenciador de Esquema XML**. De qualquer forma, você receberá uma exibição como a mostrada abaixo (quando expandido):

![Gerenciador de Esquema do Visual Studio com o nuspec.xsd aberto](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a>Elementos de metadados necessários

Embora os elementos a seguir sejam os requisitos mínimos para um pacote, considere adicionar os [elementos de metadados opcionais](#optional-metadata-elements) para melhorar a experiência geral que os desenvolvedores têm com o pacote. 

Esses elementos precisam aparecer dentro de um elemento `<metadata>`.

#### <a name="id"></a>id 
O identificador de pacote que não diferencia maiúsculas de minúsculas, o qual deve ser exclusivo no nuget.org ou em qualquer galeria na qual o pacote reside. IDs podem não conter espaços nem caracteres que não sejam válidos para uma URL e geralmente seguem as regras de namespace do .NET. Consulte [Escolhendo um identificador de pacote exclusivo](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) para ver diretrizes.
#### <a name="version"></a>version
A versão do pacote, seguindo o padrão *principal.secundária.patch*. Os números de versão podem incluir um sufixo de pré-lançamento, conforme descrito em [Controle de versões de pré-lançamento](../reference/package-versioning.md#pre-release-versions). 
#### <a name="description"></a>descrição
Uma descrição longa do pacote para exibição de interface do usuário. 
#### <a name="authors"></a>authors
Uma lista separada por vírgulas de autores de pacotes, que correspondem aos nomes de perfil em nuget.org. Eles são exibidos na Galeria do NuGet em nuget.org e são usados para fazer referência cruzada aos pacotes dos mesmos autores. 

### <a name="optional-metadata-elements"></a>Elementos de metadados opcionais

#### <a name="title"></a>título
Um título amigável do pacote, geralmente usado em exibições de interface do usuário como em nuget.org e no Gerenciador de Pacotes do Visual Studio. Se não for especificado, a ID do pacote será usada. 
#### <a name="owners"></a>owners
Uma lista separada por vírgulas de criadores de pacotes que usam nomes de perfil no nuget.org. Essa geralmente é a mesma lista que `authors` e é ignorado ao carregar o pacote no nuget.org. Consulte [Gerenciando os proprietários de pacote no nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg). 
#### <a name="projecturl"></a>projectUrl
Uma URL para a home page do pacote, geralmente mostrada em exibições de interface do usuário, bem como em nuget.org. 
#### <a name="licenseurl"></a>licenseUrl
> [!Important]
> licenseUrl está sendo preterido. Licença de uso em vez disso.

Uma URL para a licença do pacote, geralmente mostrada em exibições de interface do usuário, bem como no nuget.org.
#### <a name="license"></a>licença
Uma expressão de licença SPDX ou o caminho para um arquivo de licença dentro do pacote, geralmente mostrado em exibições IU bem como em nuget.org. Se você esteja licenciando o pacote sob uma licença comuns, como a cláusula de 2 BSD ou MIT, use o identificador de licença SPDX associado.<br>Por exemplo: `<license type="expression">MIT</license>`

Aqui está a lista completa dos [identificadores de licença SPDX](https://spdx.org/licenses/). NuGet.org aceita apenas OSI ou licenças FSF aprovado ao usar expressão de tipo de licença.

Se o pacote é licenciado sob várias licenças comuns, você pode especificar uma licença de composição usando o [SPDX versão 2.0 da sintaxe de expressão](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).<br>Por exemplo: `<license type="expression">BSD-2-Clause OR MIT</license>`

Se você estiver usando uma licença que não tenha sido atribuída a um identificador SPDX ou é uma licença personalizada, você pode empacotar um arquivo com o texto de licença. Por exemplo:
```xml
<package>
  <metadata>
    ...
    <license type="file">LICENSE.txt</license>
    ...
  </metadata>
  <files>
    ...
    <file src="licenses\LICENSE.txt" target="" />
    ...
  </files>
</package>
```

Para o equivalente do MSBuild, dar uma olhada [uma expressão de licença ou um arquivo de licença de remessa](msbuild-targets.md#packing-a-license-expression-or-a-license-file).

A sintaxe exata de expressões de licença do NuGet é descrita abaixo em [ABNF](https://tools.ietf.org/html/rfc5234).
```cli
license-id            = <short form license identifier from https://spdx.org/spdx-specification-21-web-version#h.luq9dgcle9mo>

license-exception-id  = <short form license exception identifier from https://spdx.org/spdx-specification-21-web-version#h.ruv3yl8g6czd>

simple-expression = license-id / license-id”+”

compound-expression =  1*1(simple-expression /
                simple-expression "WITH" license-exception-id /
                compound-expression "AND" compound-expression /
                compound-expression "OR" compound-expression ) /                
                "(" compound-expression ")" )

license-expression =  1*1(simple-expression / compound-expression / UNLICENSED)
```

#### <a name="iconurl"></a>iconUrl
Uma URL para uma imagem 64x64 com a tela de fundo transparente a ser usada como o ícone do pacote na exibição de interface do usuário. Verifique se esse elemento contém a *URL direta da imagem* e não a URL de uma página da Web que contém a imagem. Por exemplo, para usar uma imagem do GitHub, use o arquivo URL bruto como <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>. 

#### <a name="requirelicenseacceptance"></a>requireLicenseAcceptance
Um valor booliano que especifica se o cliente precisa solicitar que o consumidor aceite a licença do pacote antes de instalá-lo.
#### <a name="developmentdependency"></a>developmentDependency
*(2.8 ou superior)* Um valor booliano que especifica se o pacote está marcado como uma dependência somente de desenvolvimento, que impede que o pacote seja incluído como uma dependência em outros pacotes. Com o PackageReference (NuGet 4.8 +), esse sinalizador também significa que ele excluirá os ativos de tempo de compilação da compilação. Consulte [DevelopmentDependency suporte para PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)
#### <a name="summary"></a>resumo
Uma breve descrição do pacote para exibição de interface do usuário. Se omitido, uma versão truncada do `description` é usada.
#### <a name="releasenotes"></a>releaseNotes
*(1.5 ou superior)* Uma descrição das alterações feitas nesta versão do pacote, frequentemente usado na interface do usuário como a guia **Atualizações** do Gerenciador de Pacotes do Visual Studio em vez da descrição do pacote.
#### <a name="copyright"></a>direitos autorais
*(1.5 ou superior)* Detalhes sobre direitos autorais do pacote.
#### <a name="language"></a>linguagem
A identificação de localidade para o pacote. Consulte [Criando pacotes localizados](../create-packages/creating-localized-packages.md).
#### <a name="tags"></a>marcações
Uma lista delimitada por espaço de marcas e palavras-chave que descrevem o pacote e auxiliam na descoberta de pacotes por meio de pesquisa e filtragem. 
#### <a name="serviceable"></a>facilidade de manutenção 
*(3.3 ou superior)* Somente para uso interno do NuGet.
#### <a name="repository"></a>repositório
Repositório de metadados, consiste em quatro atributos opcionais: *tipo* e *url* *(4.0 e posteriores)*, e *branch* e  *confirmação* *(4.6 +)*. Esses atributos permitem que você mapeie o. nupkg ao repositório que criou, com potencial para ficarem conforme detalhado de como a ramificação individual ou a confirmação que criou o pacote. Isso deve ser uma url disponível publicamente que pode ser invocado diretamente por um software de controle de versão. Ele não deve ser uma página html pois destina-se para o computador. Para vincular a página do projeto, use o `projectUrl` campo, em vez disso.

#### <a name="minclientversion"></a>minClientVersion
Especifica a versão mínima do cliente NuGet que pode instalar esse pacote, imposta pelo nuget.exe e pelo Gerenciador de Pacotes do Visual Studio. Isso é usado sempre que o pacote depender de recursos específicos do arquivo `.nuspec` que foram adicionados em uma versão específica do cliente do NuGet. Por exemplo, um pacote usando o atributo `developmentDependency` deve especificar “2.8” para `minClientVersion`. Da mesma forma, um pacote usando o elemento `contentFiles` (consulte a próxima seção) deve definir `minClientVersion` para “3.3”. Observe também que, como os clientes do NuGet antes de 2.5 não reconhecem esse sinalizador, eles *sempre* recusam instalar o pacote, não importando o que `minClientVersion` contém.

#### <a name="collection-elements"></a>Elementos de coleção

#### <a name="packagetypes"></a>packageTypes
*(3.5 ou superior)* Uma coleção de zero ou mais elementos `<packageType>` que especificam o tipo do pacote se for diferente de um pacote de dependência tradicional. Cada packageType tem os atributos de *name* e *version*. Consulte [Definindo um tipo de pacote](../create-packages/creating-a-package.md#setting-a-package-type).
#### <a name="dependencies"></a>dependências
Uma coleção de zero ou mais elementos `<dependency>` que especificam as dependências do pacote. Cada dependência tem atributos de *id*, *version*, *include* (3.x ou superior) e *exclude* (3.x ou superior). Consulte [Dependências](#dependencies-element) abaixo.
#### <a name="frameworkassemblies"></a>frameworkAssemblies
*(1.2 ou superior)* Uma coleção de zero ou mais elementos `<frameworkAssembly>` identifica as referências de assembly do .NET Framework que este pacote requer, o que garante que elas sejam adicionadas aos projetos que consomem o pacote. Cada frameworkAssembly tem os atributos *assemblyName* e *targetFramework*. Consulte [Especificando as referências GAC de assembly do framework](#specifying-framework-assembly-references-gac) abaixo. |
#### <a name="references"></a>referências
*(1.5 ou superior)* Uma coleção de zero ou mais assemblies de nomenclatura de elementos `<reference>` na pasta `lib` do pacote que são adicionados como referências de projeto. Cada referência tem um atributo *file*. `<references>` também pode conter um elemento `<group>` com um atributo *targetFramework*, que contém elementos `<reference>`. Se omitido, todas as referências no `lib` são incluídas. Consulte [Especificando referências de assembly explícitas](#specifying-explicit-assembly-references) abaixo.
#### <a name="contentfiles"></a>contentFiles
*(3.3 ou superior)* Uma coleção de elementos `<files>` que identificam os arquivos de conteúdo para incluir o projeto consumidor. Esses arquivos são especificados com um conjunto de atributos que descrevem como eles devem ser usados dentro do sistema de projeto. Consulte [Especificando arquivos a serem incluídos no pacote](#specifying-files-to-include-in-the-package) abaixo.
#### <a name="files"></a>arquivos 
O `<package>` nó pode conter um `<files>` nó como um irmão à `<metadata>`e uma `<contentFiles>` filho em `<metadata>`, para especificar quais arquivos de assembly e o conteúdo para incluir no pacote. Consulte [Incluindo arquivos do assembly](#including-assembly-files) e [Incluindo arquivos de conteúdo](#including-content-files) mais adiante neste tópico para obter detalhes.

## <a name="replacement-tokens"></a>Tokens de substituição

Ao criar um pacote, o comando [`nuget pack`](../tools/cli-ref-pack.md) substitui tokens delimitados por $ no nó `<metadata>` do arquivo `.nuspec` com valores que vêm de um arquivo de projeto ou a opção `-properties` do comando `pack`.

Na linha de comando, você especifica os valores de token com `nuget pack -properties <name>=<value>;<name>=<value>`. Por exemplo, você pode usar um token como `$owners$` e `$desc$` no `.nuspec` e fornecer os valores no tempo de empacotamento da seguinte maneira:

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

Para usar valores de um projeto, especifique os tokens descritos na tabela a seguir (AssemblyInfo refere-se ao arquivo em `Properties` como `AssemblyInfo.cs` ou `AssemblyInfo.vb`).

Para usar esses tokens, execute `nuget pack` com o arquivo de projeto em vez de apenas o `.nuspec`. Por exemplo, ao usar o comando a seguir, os tokens `$id$` e `$version$` em um arquivo `.nuspec` são substituídos pelos valores `AssemblyName` e `AssemblyVersion` do projeto:

```ps
nuget pack MyProject.csproj
```

Normalmente, quando você tem um projeto, você cria o `.nuspec` inicialmente usando `nuget spec MyProject.csproj`, o que inclui alguns desses tokens padrão automaticamente. No entanto, se um projeto não tiver valores para os elementos `.nuspec` necessários, `nuget pack` falhará. Além disso, se você alterar os valores de projeto, lembre-se de recompilá-lo antes de criar o pacote. Isso pode ser feito convenientemente com a opção `build` do comando do pacote.

Com exceção de `$configuration$`, os valores do projeto são usados como preferenciais sobre qualquer um com o mesmo token na linha de comando.

| Token | Origem do valor | Valor
| --- | --- | ---
| **$id$** | Arquivo de projeto | AssemblyName (título) do arquivo de projeto |
| **$version$** | AssemblyInfo | AssemblyInformationalVersion se existir, caso contrário AssemblyVersion |
| **$authors$** | AssemblyInfo | AssemblyCompany |
| **$title$** | AssemblyInfo | AssemblyTitle |
| **$description$** | AssemblyInfo | AssemblyDescription |
| **$copyright$** | AssemblyInfo | AssemblyCopyright |
| **$configuration$** | DLL de assembly | Configuração usada para compilar o assembly, com Depuração como padrão. Observe que, para criar um pacote usando uma configuração de Versão, você sempre usará `-properties Configuration=Release` na linha de comando. |

Tokens também podem ser usados para resolver caminhos quando você incluir [arquivos do assembly](#including-assembly-files) e [arquivos de conteúdo](#including-content-files). Os tokens têm os mesmos nomes que as propriedades do MSBuild, tornando possível selecionar os arquivos a serem incluídos, dependendo da configuração de build atual. Por exemplo, se você usar os seguintes tokens no arquivo `.nuspec`:

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

E você compila um assembly cujo `AssemblyName` é `LoggingLibrary` com a configuração `Release` no MSBuild, as linhas resultantes no arquivo `.nuspec` do pacote são as seguintes:

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a>Elemento de dependências

O elemento `<dependencies>` dentro do `<metadata>` contém diversos elementos `<dependency>` que identificam os outros pacotes dos quais o pacote de nível superior depende. Os atributos para cada `<dependency>` são os seguintes:

| Atributo | Descrição |
| --- | --- |
| `id` | (Obrigatório) A ID do pacote de dependência, como "EntityFramework" e "NUnit", que é o nome do pacote nuget.org mostrado em uma página do pacote. |
| `version` | (Obrigatório) O intervalo de versões aceitáveis como uma dependência. Consulte [Controle de versão do pacote](../reference/package-versioning.md#version-ranges-and-wildcards) para ver a sintaxe exata. |
| include | Uma lista delimitada por vírgulas de marcas de inclusão/exclusão (veja abaixo) que indicam a dependência a ser incluída no pacote final. O valor padrão é `all`. |
| exclude | Uma lista delimitada por vírgulas de marcas de inclusão/exclusão (veja abaixo) que indicam a dependência a ser excluída do pacote final. O valor padrão é `build,analyzers` que pode ser escrito em excesso. Mas `content/ ContentFiles` implicitamente também são excluídos no pacote final que não pode ser escrito em excesso. Marcas especificadas com `exclude` têm precedência sobre aquelas especificadas com `include`. Por exemplo, `include="runtime, compile" exclude="compile"` é o mesmo que `include="runtime"`. |

| Marca Incluir/Excluir | Pastas afetadas do destino |
| --- | --- |
| contentFiles | Conteúdo |
| tempo de execução | Runtime, Resources e FrameworkAssemblies |
| compilar | lib |
| build | build (objetos e destinos do MSBuild) |
| nativa | nativa |
| nenhum | Nenhuma pasta |
| all | Todas as pastas |

Por exemplo, as linhas a seguir indicam as dependências no `PackageA` versão 1.1.0 ou superior e `PackageB` versão 1.x.

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

As linhas a seguir indicam dependências nos mesmos pacotes, mas especificam a inclusão de pastas `contentFiles` e `build` de `PackageA` tudo, mas as pastas `native` e `compile` de `PackageB`"

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

Observação: Ao criar uma `.nuspec` de um projeto usando `nuget spec`, as dependências que existem no projeto são incluídas automaticamente no resultante `.nuspec` arquivo.

### <a name="dependency-groups"></a>Grupos de dependência

*Versão 2.0 ou superior*

Como alternativa a uma única lista simples, as dependências podem ser especificadas de acordo com o perfil da estrutura do projeto de destino usando elementos `<group>` dentro de `<dependencies>`.

Cada grupo tem um atributo chamado `targetFramework` e contém zero ou mais elementos `<dependency>`. Essas referências são instaladas juntas quando a estrutura de destino é compatível com o perfil da estrutura do projeto.

O elemento `<group>` sem um atributo `targetFramework` será usado como a lista de dependências padrão ou de fallback. Consulte [Estruturas de destino](../reference/target-frameworks.md) para ver os identificadores de estrutura exatos.

> [!Important]
> O formato do grupo não pode ser combinado com uma lista simples.

O exemplo a seguir mostra diferentes variações do elemento `<group>`:

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a>Referências de assembly explícitas

O elemento `<references>` especifica explicitamente os assemblies que o projeto de destino deve referenciar usando o pacote. Quando esse elemento está presente, o NuGet adiciona referências apenas aos assemblies listados; ele não adiciona referências a outros assemblies da pasta `lib` do pacote.

Por exemplo, o elemento `<references>` a seguir instrui o NuGet a adicionar referências a apenas `xunit.dll` e `xunit.extensions.dll`, mesmo se houver assemblies adicionais no pacote:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

Referências explícitas são geralmente usadas apenas para assemblies de tempo de design. Ao usar [Contratos de código](/dotnet/framework/debug-trace-profile/code-contracts), por exemplo, os assemblies de contrato precisam ser próximos dos assemblies de tempo de execução que eles aumentar para que o Visual Studio possa encontrá-los, mas os assemblies de contrato não precisam ser referenciados pelo projeto ou copiados para a pasta `bin` do projeto.

Da mesma forma, as referências explícitas podem ser usadas para estruturas de teste de unidade, como XUnit, que precisam de ferramentas de assemblies localizados ao lado de assemblies de tempo de execução, mas não precisa que eles estejam incluídos como referências de projeto.

### <a name="reference-groups"></a>Grupos de referência

Como alternativa a uma única lista simples, as referências podem ser especificadas de acordo com o perfil da estrutura do projeto de destino usando elementos `<group>` dentro de `<references>`.

Cada grupo tem um atributo chamado `targetFramework` e contém zero ou mais elementos `<reference>`. Essas referências são adicionadas a um projeto quando a estrutura de destino é compatível com o perfil de estrutura do projeto.

O elemento `<group>` sem um atributo `targetFramework` será usado como a lista de referências padrão ou de fallback. Consulte [Estruturas de destino](../reference/target-frameworks.md) para ver os identificadores de estrutura exatos.

> [!Important]
> O formato do grupo não pode ser combinado com uma lista simples.

O exemplo a seguir mostra diferentes variações do elemento `<group>`:

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a>Referências de assembly de estrutura

Assemblies do Framework são aqueles que fazem parte do .NET Framework e já devem estar no GAC (cache de assembly global) para qualquer computador especificado. Ao identificar assemblies dentro do elemento `<frameworkAssemblies>`, um pacote pode garantir que as referências necessárias sejam adicionadas a um projeto caso este já não tenha essas referências. Tais assemblies, obviamente, não são incluídos em um pacote diretamente.

O elemento `<frameworkAssemblies>` contém zero ou mais elementos `<frameworkAssembly>`, cada um deles especifica os seguintes atributos:

| Atributo | Descrição |
| --- | --- |
| **assemblyName** | (Obrigatório) O nome totalmente qualificado do assembly. |
| **targetFramework** | (Opcional) Especifica a estrutura de destino à qual esta referência se aplica. Se omitido, indica que a referência se aplica a todas as estruturas. Consulte [Estruturas de destino](../reference/target-frameworks.md) para ver os identificadores de estrutura exatos. |

O exemplo a seguir mostra uma referência a `System.Net` todas as estruturas de destino e uma referência a `System.ServiceModel` apenas para o .NET Framework 4.0:

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a>Incluindo arquivos do assembly

Se você seguir as convenções descritas em [Criando um pacote](../create-packages/creating-a-package.md), não será necessário especificar explicitamente uma lista de arquivos no arquivo `.nuspec`. O comando `nuget pack` escolherá automaticamente os arquivos necessários.

> [!Important]
> Quando um pacote é instalado em um projeto, o NuGet adiciona automaticamente as referências de assembly às DLLs do pacote, *excluindo* aquelas que são nomeados `.resources.dll` porque são considerados assemblies satélites. Por esse motivo, evite usar `.resources.dll` para arquivos que contêm código de pacote essencial.

Para ignorar esse comportamento automático e controlar explicitamente quais arquivos são incluídos em um pacote, coloque uma elemento `<files>` como um filho de `<package>` (e um irmão de `<metadata>`), identificando cada arquivo com um elemento `<file>` separado. Por exemplo:

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

Com o NuGet 2.x e anteriores, e em projetos que usam `packages.config`, o elemento `<files>` também é usado para incluir arquivos de conteúdo imutáveis quando um pacote é instalado. Com o NuGet 3.3 ou superior e projetos PackageReference, o elemento `<contentFiles>` é usado. Consulte [Incluindo arquivos de conteúdo](#including-content-files) abaixo para ver os detalhes.

### <a name="file-element-attributes"></a>Atributos do elemento de arquivo

Cada elemento `<file>` especifica os seguintes atributos:

| Atributo | Descrição |
| --- | --- |
| **src** | O local do arquivo ou arquivos a serem incluídos, sujeito a exclusões especificadas pelo atributo `exclude`. O caminho é relativo ao arquivo `.nuspec`, a menos que um caminho absoluto seja especificado. O caractere curinga `*` é permitido e o caractere curinga duplo `**` sugere uma pesquisa de pastas recursiva. |
| **target** | O caminho relativo para a pasta dentro do pacote em que os arquivos de origem são colocados, os quais devem começar com `lib`, `content`, `build` ou `tools`. Consulte [Criando um .nuspec de um diretório de trabalho baseado em convenção](../create-packages/creating-a-package.md#from-a-convention-based-working-directory). |
| **exclude** | Uma lista separada por ponto-e-vírgula de arquivos ou padrões de arquivo para excluir o local `src`. O caractere curinga `*` é permitido e o caractere curinga duplo `**` sugere uma pesquisa de pastas recursiva. |

### <a name="examples"></a>Exemplos

**Assembly único**

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

**Assembly único específico para uma estrutura de destino**

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

**Conjunto de DLLs que usam um caractere curinga**

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

**DLLs de estruturas diferentes**

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

**Excluindo arquivos**

    Source files:
        \tools\fileA.bak
        \tools\fileB.bak
        \tools\fileA.log
        \tools\build\fileB.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a>Incluindo arquivos de conteúdo

Arquivos de conteúdo são arquivos imutáveis que um pacote incluir em um projeto. Sendo imutáveis, eles não foram projetados para serem modificados pelo projeto consumidor. Alguns exemplos de arquivos de conteúdo:

- Imagens que são inseridas como recursos
- Arquivos de origem que já são compilados
- Scripts que precisam ser incluídos na saída de build do projeto
- Arquivos de configuração para o pacote que precisam ser incluídos no projeto, mas não precisam de nenhuma alteração específica do projeto

Arquivos de conteúdo são incluídos em um pacote usando o elemento `<files>`, especificando a pasta `content` no atributo `target`. No entanto, esses arquivos são ignorados quando o pacote é instalado em um projeto usando PackageReference, que usa o elemento `<contentFiles>`.

Para máxima compatibilidade com projetos de consumo, é ideal que um pacote especifique os arquivos de conteúdo em ambos os elementos.

### <a name="using-the-files-element-for-content-files"></a>Usando o elemento de arquivos para arquivos de conteúdo

Para arquivos de conteúdo, basta usar o mesmo formato que os arquivos do assembly, porém especifique `content` como a pasta base no atributo `target` conforme mostrado nos exemplos a seguir.

**Arquivos de conteúdo básico**

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

**Arquivos de conteúdo com a estrutura de diretório**

    Source files:
        css\mobile\style.css
        css\mobile\wp7\style.css
        css\browser\style.css

    .nuspec entry:
        <file src="css\**\*.css" target="content\css" />

    Packaged result:
        content\css\mobile\style.css
        content\css\mobile\wp7\style.css
        content\css\browser\style.css

**Arquivo de conteúdo específico para uma estrutura de destino**

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

**Arquivo de conteúdo copiado para uma pasta com ponto no nome**

Nesse caso, o NuGet vê que a extensão em `target` não corresponde à extensão em `src` e, portanto, trata essa parte do nome no `target` como uma pasta:

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

**Arquivos de conteúdo sem extensões**

Para incluir arquivos sem extensão, use os curingas `*` ou `**`:

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

**Arquivos de conteúdo com caminho e destino profundos**

Nesse caso, como as extensões de arquivo de origem e de destino correspondem, o NuGet pressupõe que o destino é um nome de arquivo e não uma pasta:

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

**Renomeando um arquivo de conteúdo no pacote**

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

**Excluindo arquivos**

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a>Usando o elemento contentFiles para arquivos de conteúdo

*NuGet 4.0 e posteriores com PackageReference*

Por padrão, um pacote coloca o conteúdo em uma pasta `contentFiles` (veja abaixo) e `nuget pack` incluiu todos os arquivos nessa pasta usando os atributos padrão. Nesse caso, não é necessário incluir um nó `contentFiles` no `.nuspec`.

Para controlar quais arquivos são incluídos, o elemento `<contentFiles>` especifica uma coleção de elementos `<files>` que identificam as inclusões dos arquivos exatos.

Esses arquivos são especificados com um conjunto de atributos que descrevem como eles devem ser usados dentro do sistema de projeto:

| Atributo | Descrição |
| --- | --- |
| **include** | (Obrigatório) O local do arquivo ou arquivos a serem incluídos, sujeito a exclusões especificadas pelo atributo `exclude`. O caminho é relativo ao arquivo `.nuspec`, a menos que um caminho absoluto seja especificado. O caractere curinga `*` é permitido e o caractere curinga duplo `**` sugere uma pesquisa de pastas recursiva. |
| **exclude** | Uma lista separada por ponto-e-vírgula de arquivos ou padrões de arquivo para excluir o local `src`. O caractere curinga `*` é permitido e o caractere curinga duplo `**` sugere uma pesquisa de pastas recursiva. |
| **buildAction** | A ação de build para atribuir ao item de conteúdo para o MSBuild, como `Content`, `None`, `Embedded Resource`, `Compile`, etc. O padrão é `Compile`. |
| **copyToOutput** | Um booliano que indica se a pasta de saída copiar itens de conteúdo para a compilação (ou publicar). O padrão é falso. |
| **flatten** | Um valor booliano que indica se os itens de conteúdo devem ser copiados para uma única pasta na saída do build (verdadeiro) ou preservar a estrutura de pasta no pacote (falso). Esse sinalizador só funciona quando o sinalizador copyToOutput está definido como true. O padrão é falso. |

Ao instalar um pacote, o NuGet aplicará os elementos filho de `<contentFiles>` de cima para baixo. Se várias entradas corresponderem ao mesmo arquivo, todas as entradas serão aplicadas. A entrada superior substitui as entradas mais baixas em caso de conflito para o mesmo atributo.

#### <a name="package-folder-structure"></a>Estrutura de pastas do pacote

O projeto do pacote deve estruturar o conteúdo usando o seguinte padrão:

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- `codeLanguages` pode ser `cs`, `vb`, `fs`, `any` ou o equivalente em letras minúsculas de determinado `$(ProjectLanguage)`
- `TxM` é qualquer moniker da estrutura de destino legal compatível com o NuGet (consulte [Estruturas de destino](../reference/target-frameworks.md)).
- Qualquer estrutura de pasta pode ser acrescentada ao final dessa sintaxe.

Por exemplo:

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

As pastas vazias podem usar `.` para recusar o fornecimento de conteúdo para certas combinações de idioma e TxM, por exemplo:

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a>Exemplo da seção contentFiles

```xml
<contentFiles>
    <!-- Embed image resources -->
    <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
    <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

    <!-- Embed all image resources under contentFiles/cs/ -->
    <files include="cs/**/*.png" buildAction="EmbeddedResource" />

    <!-- Copy config.xml to the root of the output folder -->
    <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

    <!-- Copy run.cmd to the output folder and keep the directory structure -->
    <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

    <!-- Include everything in the scripts folder except exe files -->
    <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
</contentFiles>
```

## <a name="example-nuspec-files"></a>Arquivos de exemplo do nuspec

**Um simples `.nuspec` que não especifica dependências ou arquivos**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <license type="expression">MIT</license>
    </metadata>
</package>
```

**Um `.nuspec` com dependências**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

**Um `.nuspec` com arquivos**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

**Um `.nuspec` com assemblies de estrutura**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

Neste exemplo, os seguintes itens são instalados em destinos específicos do projeto:

- .NET4 -> `System.Web`, `System.Net`
- Perfil de Cliente do .NET4 -> `System.Net`
- Silverlight 3 -> `System.Json`
- Silverlight 4 -> `System.Windows.Controls.DomainServices`
- WindowsPhone -> `Microsoft.Devices.Sensors`
