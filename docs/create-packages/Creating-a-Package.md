---
title: Criar um pacote do NuGet usando a CLI nuget.exe
description: Um guia detalhado para o processo de design e criação de um pacote do NuGet, incluindo os principais pontos de decisão como arquivos e controle de versão.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: f33624cf50248d8a137216ed0d725ed88c0defd2
ms.sourcegitcommit: ba8ad1bd13a4bba3df94374e34e20c425a05af2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68833368"
---
# <a name="create-a-package-using-the-nugetexe-cli"></a>Criar um pacote usando a CLI nuget.exe

Independentemente do pacote ou do código que ele contém, use uma das ferramentas de CLI, seja `nuget.exe` ou `dotnet.exe`, para empacotar essa funcionalidade em um componente que possa ser compartilhado e usado por diversos desenvolvedores. Para instalar as ferramentas de CLI do NuGet, confira [Instalar ferramentas de cliente do NuGet](../install-nuget-client-tools.md). Observe que o Visual Studio não inclui automaticamente uma ferramenta de CLI.

- Para projetos no estilo não SDK, normalmente projetos do .NET Framework, siga as etapas descritas neste artigo para criar um pacote. Para saber mais sobre como usar o Visual Studio e a CLI `nuget.exe`, confira [Criar e publicar um pacote do .NET Framework](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).

- Para projetos .NET Core e .NET Standard que usam o [formato de estilo SDK](../resources/check-project-format.md) e quaisquer outros projetos de estilo SDK, confira [Criar um pacote do NuGet usando a CLI dotnet](creating-a-package-dotnet-cli.md).

- Para projetos migrados de `packages.config` para [PackageReference](../consume-packages/package-references-in-project-files.md), use [msbuild -t:pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).

Tecnicamente, um pacote do NuGet é apenas um arquivo ZIP que foi renomeado com a extensão `.nupkg` e cujo conteúdo corresponde a certas convenções. Este tópico descreve o processo detalhado da criação de um pacote que cumpre as convenções.

O empacotamento começa com o código compilado (assemblies), símbolos e/ou outros arquivos que você deseja entregar como um pacote (consulte [Visão geral e o fluxo de trabalho](overview-and-workflow.md)). Esse processo é independente da compilação ou de qualquer outra forma de geração dos arquivos que entram no pacote, embora seja possível extrair informações em um arquivo de projeto para manter os assemblies e pacotes compilados em sincronização.

> [!Important]
> Este tópico se aplica a projetos no estilo não SDK, normalmente projetos que não sejam .NET Core e .NET Standard e que usam o Visual Studio 2017 e versões superiores e o NuGet 4.0 e posterior.

## <a name="decide-which-assemblies-to-package"></a>Decida quais assemblies são empacotados

Mais pacotes para fins gerais contêm um ou mais assemblies que outros desenvolvedores podem usar em seus próprios projetos.

- Em geral, é recomendável ter um assembly por pacote do NuGet, desde que cada assembly seja útil independentemente. Por exemplo, se você tiver um `Utilities.dll` que depende de `Parser.dll` e `Parser.dll` é útil por conta própria, crie um pacote para cada um. Isso permite aos desenvolvedores usar `Parser.dll` independentemente de `Utilities.dll`.

- Se sua biblioteca é composta por vários assemblies que não são úteis independentemente, não há problema em combiná-los em um pacote. Usando o exemplo anterior, se `Parser.dll` contém código que é usado apenas por `Utilities.dll`, não há problema em manter `Parser.dll` no mesmo pacote.

- Da mesma forma, se `Utilities.dll` depende de `Utilities.resources.dll`, em que novamente o último não é útil por conta própria, coloque ambos no mesmo pacote.

Os recursos são, na verdade, um caso especial. Quando um pacote é instalado em um projeto, o NuGet adiciona automaticamente as referências de assembly às DLLs do pacote, *excluindo* aquelas que são nomeados `.resources.dll` porque são considerados assemblies satélites (consulte [Criando pacotes localizados](creating-localized-packages.md)). Por esse motivo, evite usar `.resources.dll` para arquivos que contêm código de pacote essencial.

Se sua biblioteca contém assemblies de interoperabilidade COM, siga as diretrizes adicionais em [Criar pacotes com assemblies de interoperabilidade COM](author-packages-with-com-interop-assemblies.md).

## <a name="the-role-and-structure-of-the-nuspec-file"></a>A função e a estrutura do arquivo .nuspec

Depois que você sabe quais arquivos deseja empacotar, a próxima etapa é criar um manifesto de pacote em um arquivo XML `.nuspec`.

O manifesto:

1. Descreve o conteúdo do pacote e é incluído nele.
1. Controla a criação do pacote e instrui o NuGet sobre como instalá-lo em um projeto. Por exemplo, o manifesto identifica outras dependências de pacote, de modo que o NuGet também pode instalar essas dependências quando o pacote principal é instalado.
1. Contém propriedades obrigatórias e opcionais, conforme descrito abaixo. Para obter detalhes exatos, incluindo outras propriedades não mencionadas aqui, consulte a [Referência de .nuspec](../reference/nuspec.md).

Propriedades necessárias:

- O identificador de pacotes, que deve ser exclusivo entre a galeria que hospeda o pacote.
- Um número de versão específico na forma *Principal.Secundário.Patch[-Suffix]* em que *-Suffix* identifica [versões de pré-lançamento](prerelease-packages.md)
- O título do pacote como ele deve aparecer no host (como nuget.org)
- Informações de autor e proprietário.
- Uma descrição longa do pacote.

Propriedades opcionais comuns:

- Notas de Versão
- Informações de direitos autorais
- Uma breve descrição para a [Interface do usuário do Gerenciador de Pacotes no Visual Studio](../consume-packages/install-use-packages-visual-studio.md)
- Uma identificação de localidade
- URL de Projeto
- Licença como uma expressão ou um arquivo (`licenseUrl` está sendo preterido, use o elemento de metadados de nuspec [`license`](../reference/nuspec.md#license))
- Uma URL de ícone
- Listas de dependências e referências
- Marcas que auxiliam em pesquisas de galeria

A seguir está um arquivo `.nuspec` típico (mas fictício), com os comentários que descrevem as propriedades:

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
        <!-- The identifier that must be unique within the hosting gallery -->
        <id>Contoso.Utility.UsefulStuff</id>

        <!-- The package version number that is used when resolving dependencies -->
        <version>1.8.3-beta</version>

        <!-- Authors contain text that appears directly on the gallery -->
        <authors>Dejana Tesic, Rajeev Dey</authors>

        <!-- 
            Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  
        -->
        <owners>dejanatc, rjdey</owners>
        
         <!-- Project URL provides a link for the gallery -->
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

         <!-- License information is displayed on the gallery -->
        <license type="expression">Apache-2.0</license>
        

        <!-- The icon is used in Visual Studio's package manager UI -->
        <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

        <!-- 
            If true, this value prompts the user to accept the license when
            installing the package. 
        -->
        <requireLicenseAcceptance>false</requireLicenseAcceptance>

        <!-- Any details about this particular release -->
        <releaseNotes>Bug fixes and performance improvements</releaseNotes>

        <!-- 
            The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. 
        -->
        <description>Core utility functions for web applications</description>

        <!-- Copyright information -->
        <copyright>Copyright ©2016 Contoso Corporation</copyright>

        <!-- Tags appear in the gallery and can be used for tag searches -->
        <tags>web utility http json url parsing</tags>

        <!-- Dependencies are automatically installed when the package is installed -->
        <dependencies>
            <dependency id="Newtonsoft.Json" version="9.0" />
        </dependencies>
    </metadata>

    <!-- A readme.txt to display when the package is installed -->
    <files>
        <file src="readme.txt" target="" />
    </files>
</package>
```

Para obter detalhes sobre como declarar dependências e especificar números de versão, consulte [packages.config](../reference/packages-config.md) e [Controle de versão do pacote](../reference/package-versioning.md). Também é possível extrair ativos das dependências diretamente no pacote usando o os atributos `include` e `exclude` no elemento `dependency`. Consulte [Referência de .nuspec – Dependências](../reference/nuspec.md#dependencies).

Como o manifesto está incluído no pacote criado com base nele, encontre vários exemplos adicionais examinando os pacotes existentes. Uma boa fonte é a pasta *global-packages* em seu computador, cuja localização é retornada pelo comando a seguir:

```cli
nuget locals -list global-packages
```

Acesse qualquer pasta *package\version*, copie o arquivo `.nupkg` para um arquivo `.zip` e depois abra esse arquivo `.zip` e examine o `.nuspec` dentro dele.

> [!Note]
> Ao criar um `.nuspec` de um projeto do Visual Studio, o manifesto contém tokens que são substituídos com informações do projeto quando o pacote é compilado. Consulte [Criando o .nuspec de um projeto do Visual Studio](#from-a-visual-studio-project).

## <a name="create-the-nuspec-file"></a>Criar o arquivo .nuspec

Criar um manifesto completo normalmente começa com um arquivo `.nuspec` básico gerado usando um dos seguintes métodos:

- [Um diretório de trabalho baseado em convenção](#from-a-convention-based-working-directory)
- [Uma DLL de assembly](#from-an-assembly-dll)
- [Um projeto do Visual Studio](#from-a-visual-studio-project)    
- [Novo arquivo com valores padrão](#new-file-with-default-values)

Em seguida, edite o arquivo manualmente para que ele descreva o conteúdo exato que você deseja no pacote final.

> [!Important]
> Arquivos `.nuspec` gerados contêm espaços reservados que precisam ser modificados antes de criar o pacote com o comando `nuget pack`. Esse comando falhará se o `.nuspec` contiver algum espaço reservado.

### <a name="from-a-convention-based-working-directory"></a>De um diretório de trabalho baseado em convenção

Como um pacote do NuGet é apenas um arquivo ZIP que foi renomeado com a extensão `.nupkg`, geralmente é mais fácil criar a estrutura de pastas que você deseja no sistema de arquivos local para depois criar o arquivo `.nuspec` diretamente dessa estrutura. O comando `nuget pack` adicionará automaticamente todos os arquivos nessa estrutura de pastas (excluindo as pastas que começam com `.`, permitindo que você mantenha arquivos particulares na mesma estrutura).

A vantagem dessa abordagem é que você não precisa especificar no manifesto quais arquivos você deseja incluir no pacote (conforme explicado mais adiante neste tópico). Basta fazer com que o processo de build produza a estrutura de pasta exata que vai para o pacote e incluir facilmente outros arquivos que não podem fazer parte de um projeto, caso contrário:

- O conteúdo e o código-fonte que devem ser inseridos no projeto de destino.
- Scripts do PowerShell
- Transformações em configuração existentes e arquivos de código-fonte em um projeto.

As convenções de pasta são as seguintes:

| Pasta | DESCRIÇÃO | Ação após a instalação do pacote |
| --- | --- | --- |
| (raiz) | Local para leiame.txt | O Visual Studio exibe um arquivo Leiame.txt na raiz do pacote quando este é instalado. |
| lib/{tfm} | Arquivos de assembly (`.dll`), documentação (`.xml`) e símbolo (`.pdb`) para TFM (Moniker de Estrutura de Destino) | Os assemblies são adicionados como referências para a compilação e o tempo de execução também; `.xml` e `.pdb` são copiados para as pastas do projeto. Consulte [Suporte a várias estruturas de destino](supporting-multiple-target-frameworks.md) para ver a criação de subpastas específicas de destino da estrutura. |
| ref/{tfm} | Arquivos de assembly (`.dll`) e símbolo (`.pdb`) para TFM (Moniker de Estrutura de Destino) | Assemblies são adicionados como referências apenas para o tempo de compilação, portanto, nada será copiado para a pasta lixeira do projeto. |
| runtimes | Arquivos de assembly específico de arquitetura (`.dll`), símbolo (`.pdb`) e recurso nativo (`.pri`) | Assemblies são adicionados como referências apenas para o tempo de execução. Outros arquivos são copiados para as pastas do projeto. Deve sempre haver um assembly específico (TFM) `AnyCPU` correspondente na pasta `/ref/{tfm}` para oferecer o assembly de tempo de compilação correspondente. Consulte [Suporte a várias estruturas de destino](supporting-multiple-target-frameworks.md). |
| conteúdo | Arquivos arbitrários | O conteúdo é copiado para a raiz do projeto. Pense na pasta **content** como a raiz do aplicativo de destino que, enfim, consome o pacote. Para fazer o pacote adicionar uma imagem à pasta */imagens* do aplicativo, coloque-o na pasta *content/images* do pacote. |
| build | Arquivos `.targets` e `.props` do MSBuild | Inserido automaticamente no arquivo de projeto ou em `project.lock.json` (NuGet 3.x+). |
| ferramentas | Scripts e programas do Powershell acessíveis do Console do Gerenciador de Pacotes | A pasta `tools` é adicionada à variável de ambiente `PATH` somente para o Console do Gerenciador de Pacotes (especificamente, *não* para o `PATH` conforme definido para MSBuild ao criar o projeto). |

Como a estrutura de pastas pode conter qualquer número de assemblies para uma infinidade de estruturas de destino, esse método é necessário ao criar pacotes compatíveis com várias estruturas.

Em qualquer caso, uma vez que a estrutura de pastas esteja em vigor, execute o seguinte comando nessa pasta para criar o arquivo `.nuspec`:

```cli
nuget spec
```

Novamente, o `.nuspec` gerado não contém nenhuma referência explícita a arquivos na estrutura de pasta. O NuGet inclui automaticamente todos os arquivos quando o pacote é criado. No entanto, você ainda precisa editar os valores de espaço reservado em outras partes do manifesto.

### <a name="from-an-assembly-dll"></a>De uma DLL de assembly

No caso mais simples de criar um pacote de um assembly, você pode gerar um arquivo `.nuspec` dos metadados no assembly usando o seguinte comando:

```cli
nuget spec <assembly-name>.dll
```

Usar este formulário substitui alguns espaços reservados no manifesto por valores específicos do assembly. Por exemplo, a propriedade `<id>` é definida como o nome do assembly e `<version>` é definido como a versão do assembly. Outras propriedades no manifesto, no entanto, não têm valores correspondentes no assembly e, portanto, ainda contêm espaços reservados.

### <a name="from-a-visual-studio-project"></a>De um projeto do Visual Studio

É muito conveniente criar um `.nuspec` de um arquivo `.csproj` ou `.vbproj`, pois outros pacotes que foram instalados nesses projetos são referenciados automaticamente como dependências. Simplesmente use o comando a seguir na mesma pasta que o arquivo de projeto:

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

O arquivo `<project-name>.nuspec` resultante contém *tokens* que são substituídos no tempo de empacotamento pelos valores do projeto, incluindo referências aos outros pacotes que já foram instalados.

Um token é delimitado por símbolos `$` em ambos os lados da propriedade de projeto. Por exemplo, o valor `<id>` em um manifesto gerado dessa forma normalmente aparece da seguinte maneira:

```xml
<id>$id$</id>
```

Esse token é substituído pelo valor `AssemblyName` do arquivo de projeto no tempo de empacotamento. Para ver o mapeamento exato de valores de projeto para tokens `.nuspec`, consulte a [Referência de tokens de substituição](../reference/nuspec.md#replacement-tokens).

Tokens eliminam a necessidade de atualizar valores cruciais como o número de versão do `.nuspec` ao atualizar o projeto. (Você sempre pode substituir os tokens por valores literais, se desejado.) 

Observe que há várias opções de empacotamento adicional disponíveis ao trabalhar em um projeto do Visual Studio, conforme descrito em [Executando o pacote do nuget para gerar o arquivo .nupkg](#run-nuget-pack-to-generate-the-nupkg-file) posteriormente.

#### <a name="solution-level-packages"></a>Pacotes de nível de solução

*Somente NuGet 2.x. Não disponível no NuGet 3.0 ou superior.*

O NuGet 2.x é compatível com a noção de um pacote de nível de solução que instala ferramentas ou comandos adicionais para o Console do Gerenciador de Pacotes (o conteúdo da pasta `tools`), mas não adiciona referências, conteúdo ou personalizações de build aos projetos na solução. Esses pacotes não contém arquivos em suas pastas `lib`, `content` ou `build` diretas e nenhuma de suas dependências têm arquivos em suas respectivas pastas `lib`, `content` ou `build`.

O NuGet rastreia os pacotes instalados no nível da solução em um arquivo `packages.config` na pasta `.nuget`, em vez do arquivo `packages.config` do projeto.

### <a name="new-file-with-default-values"></a>Novo arquivo com valores padrão

O comando a seguir cria um manifesto padrão com espaços reservados, que garante que você inicie com a estrutura de arquivos apropriada:

```cli
nuget spec [<package-name>]
```

Se você omitir \<package-name\>, o arquivo resultante será `Package.nuspec`. Se você fornecer um nome como `Contoso.Utility.UsefulStuff`, o arquivo será `Contoso.Utility.UsefulStuff.nuspec`.

O `.nuspec` resultante contém espaços reservados para valores como o `projectUrl`. Edite o arquivo antes de usá-lo para criar o arquivo `.nupkg` final.

## <a name="choose-a-unique-package-identifier-and-setting-the-version-number"></a>Escolha um identificador de pacote exclusivo e definindo o número de versão

O identificador de pacote (elemento `<id>`) e o número de versão (elemento `<version>`) são os dois valores mais importantes no manifesto, pois eles identificam exclusivamente o código exato que está contido no pacote.

**Práticas recomendadas para o identificador de pacote:**

- **Exclusividade**: o identificador deve ser exclusivo no nuget.org ou em qualquer galeria que hospede o pacote. Antes de decidir sobre um identificador, pesquise a galeria aplicável para verificar se o nome já está em uso. Para evitar conflitos, um bom padrão é usar o nome da sua empresa como a primeira parte do identificador, como `Contoso.`.
- **Nomes semelhante a namespace**: siga um padrão semelhante aos namespaces no .NET, usando a notação de ponto em vez de hifens. Por exemplo, use `Contoso.Utility.UsefulStuff` em vez de `Contoso-Utility-UsefulStuff` ou `Contoso_Utility_UsefulStuff`. Também é útil para os consumidores quando o identificador de pacote corresponde os namespaces usados no código.
- **Pacotes de exemplo**: se você gerar um pacote de código de exemplo que demonstra como usar outro pacote, anexe `.Sample` como um sufixo ao identificador, como em `Contoso.Utility.UsefulStuff.Sample`. (O pacote de exemplo logicamente teria uma dependência do outro pacote.) Ao criar um pacote de exemplo, use o método de diretório de trabalho baseado em convenção descrito anteriormente. Na pasta `content`, organize o código de exemplo em uma pasta chamada `\Samples\<identifier>` como no `\Samples\Contoso.Utility.UsefulStuff.Sample`.

**Práticas recomendadas para a versão de pacote:**

- Em geral, defina a versão do pacote para corresponder à biblioteca, embora isso não seja estritamente necessário. Isso é muito simples quando você limita um pacote a um único assembly, conforme descrito anteriormente em [Decidir quais assemblies serão empacotados](#decide-which-assemblies-to-package). Em geral, lembre-se que o NuGet em si lida com versões do pacote ao resolver as dependências, não versões de assembly.
- Ao usar um esquema de versão não padrão, considere as regras de controle de versão do NuGet, conforme explicado em [Controle de versão do pacote](../reference/package-versioning.md).

> A seguinte série de breves postagens no blog também é útil para entender o controle de versão:
>
> - [Parte 1: Como assumir o DLL Hell](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Parte 2: O algoritmo principal](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Parte 3: Unificação por meio de redirecionamentos de associação](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="add-a-readme-and-other-files"></a>Adicione um Leiame e outros arquivos

Para especificar diretamente os arquivos a serem incluídos no pacote, use o nó `<files>` no arquivo `.nuspec`, que *segue* a marca `<metadata>`:

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
        <!-- Add a readme -->
        <file src="readme.txt" target="" />

        <!-- Add files from an arbitrary folder that's not necessarily in the project -->
        <file src="..\..\SomeRoot\**\*.*" target="" />
    </files>
</package>
```

> [!Tip]
> Ao usar a abordagem de diretório de trabalho baseado em convenção, você pode colocar o Leiame.txt na raiz do pacote e outros conteúdos na pasta `content`. Nenhum elemento `<file>` é necessário no manifesto.

Quando você inclui um arquivo chamado `readme.txt` na raiz do pacote, o Visual Studio exibe o conteúdo do arquivo como texto sem formatação imediatamente depois de instalar o pacote diretamente. (Arquivos Leiame não são exibidos para pacotes instalados como dependências). Por exemplo, mostramos aqui como o arquivo Leiame para o pacote HtmlAgilityPack é exibido:

![A exibição de um arquivo Leiame para um pacote do NuGet na instalação](media/Create_01-ShowReadme.png)

> [!Note]
> Se você incluir um nó `<files>` vazio no arquivo `.nuspec`, o NuGet não incluirá nenhum outro conteúdo no pacote que não seja o que está na pasta `lib`.

## <a name="include-msbuild-props-and-targets-in-a-package"></a>Incluir objetivos e destinos de MSBuild em um pacote

Em alguns casos, convém adicionar destinos ou propriedades de build personalizados a projetos que consomem o pacote, como a execução de uma ferramenta personalizada ou um processo durante o build. Faça isso colocando arquivos no formato `<package_id>.targets` ou `<package_id>.props` (como `Contoso.Utility.UsefulStuff.targets`) dentro da pasta `\build` do projeto.

Arquivos na pasta `\build` raiz são considerados adequados para todas as estruturas de destino. Para fornecer arquivos específicos de estrutura, primeiro coloque-os em subpastas apropriadas, como os seguintes:

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

Em seguida, no arquivo `.nuspec`, faça referência a esses arquivos no nó `<files>`:

```xml
<?xml version="1.0"?>
<package >
    <metadata minClientVersion="2.5">
    <!-- ... -->
    </metadata>
    <files>
        <!-- Include everything in \build -->
        <file src="build\**" target="build" />

        <!-- Other files -->
        <!-- ... -->
    </files>
</package>
```

Incluindo os arquivos de propriedades e de destinos do MSBuild em um pacote [introduzidos com o NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), portanto é recomendado adicionar o atributo `minClientVersion="2.5"` ao elemento `metadata` para indicar a versão mínima necessária do cliente NuGet para consumir o pacote.

Quando o NuGet instala um pacote com arquivos `\build`, ele adiciona elementos `<Import>` do MSBuild ao arquivo de projeto que aponta para os arquivos `.targets` e `.props`. (`.props` é adicionado à parte superior do arquivo de projeto; `.targets` é adicionado à parte inferior.) Um elemento `<Import>` do MSBuild condicional separado é adicionado para cada estrutura de destino.

É possível colocar os arquivos `.props` e `.targets` do MSBuild na pasta `\buildMultiTargeting` para direcionamento entre estruturas. Durante a instalação do pacote, o NuGet adiciona elementos `<Import>` correspondentes ao arquivo de projeto contanto que a estrutura de destino não esteja definida (a propriedade `$(TargetFramework)` do MSBuild deve estar vazia).

Com o NuGet 3.x, os destinos não são adicionados ao projeto, mas são disponibilizados por meio do `project.lock.json`.

## <a name="run-nuget-pack-to-generate-the-nupkg-file"></a>Execute o nuget pack para gerar o arquivo .nupkg

Ao usar um assembly ou o diretório de trabalho baseado em convenção, crie um pacote executando `nuget pack` com seu arquivo `.nuspec`, substituindo `<project-name>` pelo nome do seu arquivo específico:

```cli
nuget pack <project-name>.nuspec
```

Ao usar um projeto do Visual Studio, execute `nuget pack` com o arquivo de projeto, que carrega automaticamente o arquivo `.nuspec` do projeto e substitui todos os tokens dentro dele usando valores no arquivo de projeto:

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> É necessário usar o arquivo de projeto diretamente para a substituição do token porque o projeto é a origem dos valores de token. A substituição do token não ocorre se você usar `nuget pack` com um arquivo `.nuspec`.

Em todos os casos, o `nuget pack` exclui pastas que começam com um ponto, como `.git` ou `.hg`.

O NuGet indica se há erros no arquivo `.nuspec` que precisam de correção, como se esquecer de alterar os valores de espaço reservado no manifesto.

Depois que o `nuget pack` for bem-sucedido, você tem um arquivo `.nupkg` que pode ser publicado para uma galeria adequada conforme descrito em [Publicar um pacote](../nuget-org/publish-a-package.md).

> [!Tip]
> Uma maneira útil de examinar um pacote após a criação é abri-lo na ferramenta [Explorador de Pacotes](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer). Isso fornece uma exibição gráfica do conteúdo do pacote e seu manifesto. Você também pode renomear o arquivo `.nupkg` resultante para um arquivo `.zip` e explorar seu conteúdo diretamente.

### <a name="additional-options"></a>Opções adicionais

Você pode usar várias opções de linha de comando com `nuget pack` para excluir arquivos, substituir o número de versão no manifesto e alterar a pasta de saída, entre outros recursos. Para ver uma lista completa, consulte a [referência de comandos do pacote](../reference/cli-reference/cli-ref-pack.md).

As opções a seguir são algumas das escolhas comuns nos projetos do Visual Studio:

- **Projetos referenciados**: se o projeto faz referência a outros projetos, você pode adicionar os projetos referenciados, como parte do pacote ou como dependências, usando a opção `-IncludeReferencedProjects`:

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    Esse processo de inclusão é recursivo, portanto, se `MyProject.csproj` faz referência a projetos B e C e os projetos fazem referência a D, E e F, os arquivos de B, C, D, E e F estarão incluídos no pacote.

    Se um projeto referenciado inclui um arquivo `.nuspec` próprio, o NuGet adiciona esse projeto referenciado como uma dependência em vez disso.  Esse projeto precisa ser empacotado e publicado separadamente.

- **Configuração de build**: por padrão, o NuGet usa a configuração de build padrão definida no arquivo de projeto, normalmente *Depurar*. Para empacotar arquivos de uma configuração de build diferente, como *Versão*, use a opção `-properties` com a configuração:

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- **Símbolos**: para incluir os símbolos que permitem que os consumidores executem o código do seu pacote em etapas no depurador, use a opção `-Symbols`:

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="test-package-installation"></a>Instalação do pacote de teste

Antes de publicar um pacote, geralmente é recomendável testar o processo de instalação de um pacote em um projeto. Os testes garantem que os arquivos todos terminem em seus lugares corretos no projeto.

Você pode testar instalações manualmente no Visual Studio ou na linha de comando usando as [etapas de instalação do pacote](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package) normais.

Para testes automatizados, o processo básico é o seguinte:

1. Copie o arquivo `.nupkg` para uma pasta local.
1. Adicione a pasta às origens de pacote usando o comando `nuget sources add -name <name> -source <path>` (consulte [origens do nuget](../reference/cli-reference/cli-ref-sources.md)). Observe que é preciso apenas configurar essa origem local uma vez em qualquer computador.
1. Instale o pacote da origem usando `nuget install <packageID> -source <name>` em que `<name>` corresponde ao nome de sua origem conforme fornecido para `nuget sources`. Especificar a origem garante que o pacote seja instalado somente dela.
1. Examine seu sistema de arquivos para verificar se os arquivos estão instalados corretamente.

## <a name="next-steps"></a>Próximas etapas

Depois de criar um pacote, que é um arquivo `.nupkg`, você pode publicá-lo na galeria de sua escolha conforme descrito em [Publicar um pacote](../nuget-org/publish-a-package.md).

Você também poderá estender os recursos do seu pacote ou dar suporte a outros cenários conforme descrito nos tópicos a seguir:

- [Controle de versão do pacote](../reference/package-versioning.md)
- [Suporte a várias estruturas de destino](../create-packages/supporting-multiple-target-frameworks.md)
- [Transformações dos arquivos de configuração e de origem](../create-packages/source-and-config-file-transformations.md)
- [Localização](../create-packages/creating-localized-packages.md)
- [Versões de pré-lançamento](../create-packages/prerelease-packages.md)
- [Definir tipo de pacote](../create-packages/set-package-type.md)
- [Criar pacotes com assemblies de interoperabilidade COM](../create-packages/author-packages-with-COM-interop-assemblies.md)

Por fim, há tipos de pacote adicionais a serem considerados:

- [Pacotes nativos](../create-packages/native-packages.md)
- [Pacotes de Símbolo](../create-packages/symbol-packages.md)
