---
title: Formato PackageReference do NuGet (referências de pacote em arquivos de projeto)
description: Veja detalhes sobre o PackageReference de NuGet em arquivos de projeto compatível com o NuGet 4.0 e posterior e o VS2017 e .Net Core 2.0
author: nkolev92
ms.author: nikolev
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: c7b963352e0e9640844a213767a58c883ed0eeb9
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323707"
---
# <a name="package-references-packagereference-in-project-files"></a>Referências de pacote ( `PackageReference` ) em arquivos de projeto

As referências de pacote, usando o nó `PackageReference`, gerenciam as dependências do NuGet diretamente nos arquivos de projeto (em vez de precisar de um arquivo `packages.config` separado). O uso de PackageReference, como ele é chamado, não afeta outros aspectos do NuGet; por exemplo, as configurações nos arquivos `NuGet.Config` (incluindo as origens do pacote) ainda são aplicadas, conforme explicado em [Configurações comuns do NuGet](configuring-nuget-behavior.md).

Com o PackageReference, você também pode usar as condições do MSBuild para escolher as referências de pacote por estrutura de destino ou outros agrupamentos. Ele também proporciona um controle refinado sobre as dependências e o fluxo de conteúdo. (Para obter mais detalhes, veja [Empacotamento e restauração do NuGet como destinos do MSBuild](../reference/msbuild-targets.md).)

## <a name="project-type-support"></a>Suporte do tipo de projeto

Por padrão, o PackageReference é usado para projetos do .NET Core, para projetos do .NET Standard e para projetos da UWP direcionados ao Windows 10 Build 15063 (Atualização para Criadores) e posterior, com exceção dos projetos da C ++ UWP. Os projetos do .NET Framework são compatíveis com o PackageReference, mas, no momento, contam com `packages.config` como padrão. Para usar PackageReference, [migre](../consume-packages/migrate-packages-config-to-package-reference.md) as dependências de `packages.config` para o arquivo de projeto e remova packages.config.

Os aplicativos ASP.NET do .NET Framework completo incluem apenas [suporte limitado](https://github.com/NuGet/Home/issues/5877) para PackageReference. Não há suporte para tipos de projeto C++ e JavaScript.

## <a name="adding-a-packagereference"></a>Adicionar um PackageReference

Adicione uma dependência ao arquivo de projeto usando a seguinte sintaxe:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a>Controlar a versão de dependência

A convenção para especificar a versão de um pacote é a mesma que usar `packages.config`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

No exemplo acima, 3.6.0 significa qualquer versão que é >=3.6.0 com preferência para a versão mais antiga, conforme descrito em [Controle de versão do pacote](../concepts/package-versioning.md#version-ranges).

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a>Usando PackageReference para um projeto sem PackageReferences

Avançado: se você não tem pacotes instalados em um projeto (não tem PackageReferences no arquivo de projeto nem um arquivo packages.config), mas deseja que o projeto seja restaurado como o estilo PackageReference, você pode definir uma propriedade de projeto RestoreProjectStyle como PackageReference em seu arquivo de projeto.

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

Isso poderá ser útil se você fizer referência a projetos que são do estilo PackageReference (projetos de estilo csproj ou SDK existentes). Isso permitirá que os pacotes aos quais esses projetos fazem referência sejam referenciados "transitivamente" pelo seu projeto.

## <a name="packagereference-and-sources"></a>PackageReference e fontes

Em projetos PackageReference, as versões de dependência transitivas são resolvidas no momento da restauração. Como tal, em projetos PackageReference, todas as fontes precisam estar disponíveis para todas as restaurações. 

## <a name="floating-versions"></a>Versões flutuantes

[Versões flutuante](../concepts/dependency-resolution.md#floating-versions) são compatíveis com `PackageReference`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>Controlar ativos de dependência

Você pode estar usando uma dependência puramente como uma estrutura de desenvolvimento e pode não querer expor isso aos projetos que consumirão o pacote. Nesse cenário, você pode usar os metadados do `PrivateAssets` para controlar esse comportamento.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

As seguintes marcas de metadados controlam ativos de dependência:

| Marca | Descrição | Valor Padrão |
| --- | --- | --- |
| IncludeAssets | Esses ativos serão consumidos | all |
| ExcludeAssets | Esses ativos não serão consumidos | nenhum |
| PrivateAssets | Esses ativos serão consumidos, mas não fluem para o projeto pai | contentfiles;analyzers;build |

Os valores permitidos para essas marcas são os seguintes, com vários valores separados por ponto e vírgula, exceto com `all` e `none`, que devem aparecer sozinhos:

| Valor | Descrição |
| --- | ---
| compilar | Conteúdo da pasta `lib` e controles se seu projeto puder compilar em relação aos assemblies dentro da pasta |
| runtime | Conteúdo da pasta `lib` e `runtimes` pasta e controles se esses assemblies forem copiados para o diretório de saída de compilação |
| contentFiles | O conteúdo da pasta `contentfiles` |
| compilar | `.props` e `.targets` na pasta `build` |
| buildMultitargeting | *(4.0)* `.props` e `.targets` na pasta `buildMultitargeting`, para direcionamento entre estruturas |
| buildTransitive | *(5.0+)* `.props` e `.targets` na pasta `buildTransitive`, para ativos que fluem transitivamente para qualquer projeto de consumo. Confira a página de [recursos](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior). |
| analisadores | Analisadores de .NET |
| nativa | O conteúdo da pasta `native` |
| nenhum | Nenhuma das opções acima é usada. |
| all | Todas as anteriores (exceto `none`) |

No exemplo a seguir, tudo, exceto os arquivos de conteúdo do pacote, poderia ser consumido pelo projeto e tudo, exceto analisadores e arquivos de conteúdo, fluiria para o projeto pai.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Observe que, como `build` não está incluído em `PrivateAssets`, destino e objetos *fluirão* para o projeto pai. Considere, por exemplo, que a referência acima é usada em um projeto que compila um pacote do NuGet chamado AppLogger. O AppLogger pode consumir os destinos e objetos de `Contoso.Utility.UsefulStuff`, bem como projetos que consomem AppLogger.

> [!NOTE]
> Quando `developmentDependency` é definido como `true` em um arquivo `.nuspec`, isso marca um pacote como uma dependência somente de desenvolvimento, o que impede que o pacote seja incluído como uma dependência em outros pacotes. Com PackageReference *(NuGet 4.8+)*, esse sinalizador também significa que ele excluirá os recursos em tempo de compilação. Para obter mais informações, confira [Suporte do DevelopmentDependency para PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).

## <a name="adding-a-packagereference-condition"></a>Adicionar uma condição de PackageReference

É possível usar uma condição para controlar se um pacote está incluído, em que as condições podem usar qualquer variável MSBuild ou uma variável definida no arquivo de destinos ou objetos. No entanto, no momento, somente a variável `TargetFramework` é compatível.

Por exemplo, digamos que seu destino é `netstandard1.4` e `net452`, mas tem uma dependência que é aplicável somente para `net452`. Nesse caso, não é aconselhável ter um projeto `netstandard1.4` que está consumindo seu pacote para adicionar essa dependência desnecessária. Para evitar isso, você deve especificar uma condição no `PackageReference` da seguinte maneira:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

Um pacote compilado usando este projeto mostrará que Newtonsoft.Json está incluído como uma dependência somente para um destino `net452`:

![O resultado da aplicação de uma condição em PackageReference com o VS2017](media/PackageReference-Condition.png)

As condições também podem ser aplicadas no nível de `ItemGroup` e serão aplicadas a todos os elementos `PackageReference` filhos:

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a>GeneratePathProperty

Esse recurso está disponível com o NuGet **5,0** ou superior e com o Visual Studio 2019 **16,0** ou superior.

Às vezes, é desejável referenciar arquivos em um pacote de um destino do MSBuild.
Em `packages.config` projetos baseados, os pacotes são instalados em uma pasta relativa ao arquivo de projeto. No entanto, no PackageReference, os pacotes são [consumidos](../concepts/package-installation-process.md) a partir da pasta *global-Packages* , que pode variar de máquina para máquina.

Para preencher essa lacuna, o NuGet introduziu uma propriedade que aponta para o local do qual o pacote será consumido.

Exemplo:

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

Além disso, o NuGet gerará automaticamente as propriedades para pacotes que contêm uma pasta de ferramentas.

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
```

As propriedades do MSBuild e as identidades do pacote não têm as mesmas restrições para que a identidade do pacote precise ser alterada para um nome amigável do MSBuild, prefixado pela palavra `Pkg` .
Para verificar o nome exato da propriedade gerada, examine o arquivo [NuGet. g. props](../reference/msbuild-targets.md#restore-outputs) gerado.

## <a name="packagereference-aliases"></a>Aliases de PackageReference

Em algumas instâncias raras, pacotes diferentes conterão classes no mesmo namespace. A partir do NuGet 5,7 & o Visual Studio 2019 atualização 7, equivalente a ProjectReference, o PackageReference dá suporte a [`Aliases`](/dotnet/api/microsoft.codeanalysis.projectreference.aliases) .
Por padrão, nenhum alias é fornecido. Quando um alias é especificado, *todos os* assemblies provenientes do pacote anotado precisam ser referenciados com um alias.

Você pode examinar o uso de exemplo em [NuGet\Samples](https://github.com/NuGet/Samples/tree/main/PackageReferenceAliasesExample)

No arquivo de projeto, especifique os aliases da seguinte forma:

```xml
  <ItemGroup>
    <PackageReference Include="NuGet.Versioning" Version="5.8.0" Aliases="ExampleAlias" />
  </ItemGroup>
```

e, no código, use-o da seguinte forma:

```cs
extern alias ExampleAlias;

namespace PackageReferenceAliasesExample
{
...
        {
            var version = ExampleAlias.NuGet.Versioning.NuGetVersion.Parse("5.0.0");
            Console.WriteLine($"Version : {version}");
        }
...
}

```

## <a name="nuget-warnings-and-errors"></a>Avisos e erros do NuGet

*Esse recurso está disponível com o NuGet **4.3** ou superior e com Visual Studio 2017 **15.3** ou superior.*

Para muitos cenários de pacote e restauração, todos os avisos e erros do NuGet são codificados e começam com `NU****` . Todos os avisos e erros do NuGet são listados na [documentação de](../reference/errors-and-warnings.md) referência.

O NuGet observa as seguintes propriedades de aviso:

- `TreatWarningsAsErrors`, trate todos os avisos como erros
- `WarningsAsErrors`, trate avisos específicos como erros
- `NoWarn`, o oculta avisos específicos, em todo o projeto ou em todo o pacote.

Exemplos:

```xml
<PropertyGroup>
    <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <WarningsAsErrors>$(WarningsAsErrors);NU1603;NU1605</WarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <NoWarn>$(NoWarn);NU5124</NoWarn>
</PropertyGroup>
...
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0" NoWarn="NU1605" />
</ItemGroup>
```

### <a name="suppressing-nuget-warnings"></a>Suprimindo avisos do NuGet

Embora seja recomendável que você resolva todos os avisos do NuGet durante as operações de pacote e restauração, em determinadas situações, a supressão deles é assegurada.
Para suprimir um projeto de aviso em todo o projeto, considere fazer:

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

Às vezes, os avisos se aplicam somente a um determinado pacote no grafo. Podemos optar por suprimir esse aviso de forma mais seletiva adicionando `NoWarn` um no item PackageReference. 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a>Suprimindo avisos de pacote NuGet Visual Studio

Quando estiver Visual Studio, você também poderá [suprimir avisos por](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) meio do IDE.

## <a name="locking-dependencies"></a>Bloqueio de dependências

*Esse recurso está disponível no NuGet **4.9** ou superior e no Visual Studio 2017 **15.9** ou superior.*

A entrada da restauração do NuGet é um conjunto de Referências de pacote do arquivo de projeto (dependências de nível superior ou diretas), e a saída é um fechamento completo de todas as dependências do pacote, incluindo as dependências transitivas. Se a lista PackageReference de entrada não tiver sido alterada, o NuGet tenta sempre produzir o mesmo fechamento completo das dependências de pacotes. No entanto, em alguns cenários, isso não poderá ser feito. Por exemplo:

* Quando você usa versões flutuantes como `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`. Embora a intenção aqui seja derivar para a versão mais recente sempre que uma restauração de pacotes ocorrer, há cenários em que os usuários exigem que o grafo seja bloqueado em uma determinada versão mais recente e derive para uma versão posterior, se disponível, mediante um gesto explícito.
* Uma versão mais recente do pacote que corresponde aos requisitos de versão do PackageReference é publicada. Por ex.: 

  * Dia 1: se você tiver especificado `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`, mas as versões disponíveis nos repositórios do NuGet forem 4.1.0, 4.2.0 e 4.3.0. Nesse caso, o NuGet teria que ser resolvido como 4.1.0 (mais próximo da versão mínima)

  * Dia 2: a versão 4.0.0 é publicada. O NuGet agora encontrará a correspondência exata e iniciará a resolução como 4.0.0

* Uma determinada versão de pacote é removida do repositório. Embora nuget.org não permita exclusões de pacotes, nem todos os repositórios de pacotes possuem essas restrições. Isso faz com que o NuGet encontre a melhor correspondência quando não puder resolver a versão excluída.

### <a name="enabling-lock-file"></a>Habilitar o arquivo de bloqueio

Para persistir o fechamento completo das dependências de pacotes, você pode optar pelo recurso de bloqueio de arquivos definindo a propriedade `RestorePackagesWithLockFile` do MSBuild para seu projeto:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

Se essa propriedade for definida, a restauração do NuGet gerará um arquivo de bloqueio – arquivo `packages.lock.json` no diretório raiz do projeto que lista todas as dependências do pacote. 

> [!Note]
> Se um projeto tiver o arquivo `packages.lock.json` no diretório raiz, o arquivo de bloqueio sempre será usado com a restauração, mesmo que a propriedade `RestorePackagesWithLockFile` não esteja definida. Portanto, outra maneira de optar por esse recurso é através da criação um arquivo `packages.lock.json` fictício em branco no diretório raiz do projeto.

### <a name="restore-behavior-with-lock-file"></a>Comportamento `restore` com o arquivo de bloqueio
Se houver um arquivo de bloqueio para o projeto, o NuGet usará esse arquivo de bloqueio para executar `restore`. O NuGet faz uma verificação rápida para ver se houve alguma alteração nas dependências do pacote, conforme mencionado no arquivo do projeto (ou nos arquivos dependentes dos projetos) e, se não houver alterações, ele apenas restaurará os pacotes mencionados no arquivo de bloqueio. Não há reavaliações das dependências do pacote.

Se o NuGet detectar uma alteração nas dependências definidas, conforme mencionado nos arquivos de projeto, ele reavaliará o grafo do pacote e atualizará o arquivo de bloqueio para refletir o novo fechamento do pacote para o projeto.

Para CI/CD e outros cenários, em que você não deseja alterar as dependências de pacote rapidamente, é possível configurar o `lockedmode` como `true`:

Para dotnet.exe, execute:

```
> dotnet.exe restore --locked-mode
```

Para msbuild.exe, execute:

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

Você também pode definir essa propriedade condicional do MSBuild em seu arquivo de projeto:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

Se o modo de bloqueio for `true`, a restauração ocorrerá nos pacotes exatos conforme listado no arquivo de bloqueio ou não ocorrerá se você tiver atualizado as dependências de pacote definidas para o projeto após a criação do arquivo de bloqueio.

### <a name="make-lock-file-part-of-your-source-repository"></a>Tornar o arquivo de bloqueio parte de seu repositório de origem
Se você estiver compilando um aplicativo, um executável e o projeto em questão estarão no início da cadeia da dependência, portanto, verifique o arquivo de bloqueio no repositório do código-fonte para que o NuGet possa utilizá-lo durante a restauração.

No entanto, se seu projeto for um projeto de biblioteca que não é enviado ou um projeto de código comum do qual outros projetos dependem, você **não deverá** fazer check-in do arquivo de bloqueio como parte de seu código-fonte. Não há mal nenhum em manter o arquivo de bloqueio. No entanto, as dependências do pacote bloqueado do projeto de código comum não podem ser usadas, conforme listado no arquivo de bloqueio, durante a restauração/compilação de um projeto que depende desse projeto de código comum.

Por exemplo:

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

Se `ProjectA` tiver uma dependência em uma versão `2.0.0` do `PackageX`, além de referências `ProjectB` que dependem da versão `1.0.0` do `PackageX`, o arquivo de bloqueio de `ProjectB` listará uma dependência na versão `1.0.0` do `PackageX`. No entanto, quando é criado, seu arquivo de bloqueio conterá uma dependência na versão e não conforme listado no `ProjectA` arquivo de bloqueio para `PackageX` **`2.0.0`**  `1.0.0` `ProjectB` . Portanto, o arquivo de bloqueio de um projeto de código comum tem pouco a dizer sobre os pacotes resolvidos de projetos que dependem dele.

### <a name="lock-file-extensibility"></a>Extensibilidade do arquivo de bloqueio

Você pode controlar vários comportamentos de restauração com o arquivo de bloqueio conforme descrito abaixo:

| NuGet.exe opção | Opção dotnet | Opção equivalente do MSBuild | Descrição |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | RestorePackagesWithLockFile | Opta pelo uso de um arquivo de bloqueio. |
| `-LockedMode` | `--locked-mode` | RestoreLockedMode | Habilita o modo de bloqueio para a restauração. Isso é útil em cenários de CI/CD em que você deseja builds re repetitivas.|   
| `-ForceEvaluate` | `--force-evaluate` | RestoreForceEvaluate | Esta opção é útil com pacotes que têm a versão flutuante definida no projeto. Por padrão, a restauração do NuGet não atualizará a versão do pacote automaticamente em cada restauração, a menos que você execute a restauração com essa opção. |
| `-LockFilePath` | `--lock-file-path` | NuGetLockFilePath | Define o local de um arquivo de bloqueio personalizado para um projeto. Por padrão, o NuGet é compatível com `packages.lock.json` no diretório raiz. Se você tiver vários projetos no mesmo diretório, o NuGet oferecerá suporte ao arquivo de bloqueio `packages.<project_name>.lock.json` específico do projeto |

## <a name="assettargetfallback"></a>AssetTargetFallback

A propriedade permite especificar versões de estrutura compatíveis adicionais para projetos que seu projeto referencia e pacotes NuGet que `AssetTargetFallback` seu projeto consome.

Se você especificar uma dependência de pacote usando, mas esse pacote não contém ativos compatíveis com a estrutura de destino de seus projetos, a propriedade `PackageReference` `AssetTargetFallback` entra em ação. A compatibilidade do pacote referenciado é verificado novamente usando cada estrutura de destino especificada em `AssetTargetFallback` .
Quando um `project` ou um `package` é referenciado por meio de , `AssetTargetFallback` o aviso [NU1701](../reference/errors-and-warnings/NU1701.md) será gerado.

Consulte a tabela abaixo para ver exemplos de como `AssetTargetFallback` afeta a compatibilidade.

| Estrutura do projeto | AssetTargetFallback | Estruturas de pacote | Resultado |
|-------------------|---------------------|--------------------|--------|
| .NET Framework 4.7.2 | | .NET Standard 2.0 | .NET Standard 2.0 |
| Aplicativo .NET Core 3.1 | | .NET Standard 2.0, .NET Framework 4.7.2 | .NET Standard 2.0 |
| Aplicativo .NET Core 3.1 | | .NET Framework 4.7.2 | Incompatível, falha com [`NU1202`](../reference/errors-and-warnings/NU1202.md) |
| Aplicativo .NET Core 3.1 | net472;net471 | .NET Framework 4.7.2 | .NET Framework 4.7.2 com [`NU1701`](../reference/errors-and-warnings/NU1701.md) |

Várias estruturas podem ser especificadas usando `;` como umlimidor. Para adicionar uma estrutura de fallback, você pode fazer o seguinte:

```xml
<AssetTargetFallback Condition=" '$(TargetFramework)'=='netcoreapp3.1' ">
    $(AssetTargetFallback);net472;net471
</AssetTargetFallback>
```

Você pode deixar desativado `$(AssetTargetFallback)` se desejar substituir, em vez de adicionar aos `AssetTargetFallback` valores existentes.

> [!NOTE]
> Se você estiver usando um [projeto baseado no SDK do .net](/dotnet/core/sdk), `$(AssetTargetFallback)` os valores apropriados serão configurados e você não precisará defini-los manualmente.
>
> `$(PackageTargetFallback)` foi um recurso anterior que tentou resolver esse desafio, mas ele é dividido de maneira fundamental e não *deve* ser usado. Para migrar do `$(PackageTargetFallback)` para `$(AssetTargetFallback)` o, basta alterar o nome da propriedade.
