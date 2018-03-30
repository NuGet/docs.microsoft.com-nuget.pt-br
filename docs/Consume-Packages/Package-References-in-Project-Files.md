---
title: Formato PackageReference do NuGet (referências de pacote em arquivos de projeto) | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/16/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Veja detalhes sobre o PackageReference de NuGet em arquivos de projeto compatível com o NuGet 4.0 e posterior e o VS2017 e .Net Core 2.0
keywords: Dependências de pacote NuGet, referências de pacote, arquivos de projeto, PackageReference, packages.config, VS2017, Visual Studio 2017, NuGet 4, .NET Core 2.0
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 99caf371ca1bd85e6af4e879741e3e2caab6e860
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="package-references-packagereference-in-project-files"></a>Referências de pacote (PackageReference) em arquivos de projeto

As referências de pacote, usando o nó `PackageReference`, gerenciam as dependências do NuGet diretamente nos arquivos de projeto (em vez de precisar de um arquivo `packages.config` separado). Usar o PackageReference, como ele é chamado, não afeta os outros aspectos do NuGet; por exemplo, as configurações nos arquivos `NuGet.Config` (inclusive nas origens de pacote) ainda são aplicadas, conforme explicado em [Configurando o comportamento do NuGet](configuring-nuget-behavior.md).

Com o PackageReference, você também pode usar condições do MSBuild para escolher as referências de pacote por estrutura de destino, por configuração, por plataforma ou por outros agrupamentos. Ele também proporciona um controle refinado sobre as dependências e o fluxo de conteúdo. (Para obter mais detalhes, veja [Empacotamento e restauração do NuGet como destinos do MSBuild](../reference/msbuild-targets.md).)

Por padrão, o PackageReference é usado para projetos do .NET Core, para projetos do .NET Standard e para projetos da UWP direcionados ao Windows 10 Build 15063 (Atualização para Criadores) e posterior, com exceção dos projetos da C ++ UWP. Os projetos com estrutura completa do .NET são compatíveis com o PackageReference, mas no momento contam com `packages.config` como padrão. Para usar PackageReference, migre as dependências de `packages.config` para o arquivo de projeto e remova packages.config.

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

No exemplo acima, 3.6.0 significa qualquer versão que é >=3.6.0 com preferência para a versão mais antiga, conforme descrito em [Controle de versão do pacote](../reference/package-versioning.md#version-ranges-and-wildcards).

## <a name="floating-versions"></a>Versões flutuantes

[Versões flutuante](../consume-packages/dependency-resolution.md#floating-versions) são compatíveis com `PackageReference`:

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

| Marca | Descrição | Valor padrão |
| --- | --- | --- |
| IncludeAssets | Esses ativos serão consumidos | all |
| ExcludeAssets | Esses ativos não serão consumidos | nenhum |
| PrivateAssets | Esses ativos serão consumidos, mas não fluem para o projeto pai | contentfiles;analyzers;build |

Os valores permitidos para essas marcas são os seguintes, com vários valores separados por ponto e vírgula, exceto com `all` e `none`, que devem aparecer sozinhos:

| Valor | Descrição |
| --- | ---
| compilar | O conteúdo da pasta `lib` |
| tempo de execução | O conteúdo da pasta `runtimes` |
| contentFiles | O conteúdo da pasta `contentfiles` |
| build | Objetos e propriedades na pasta `build` |
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

## <a name="adding-a-packagereference-condition"></a>Adicionar uma condição de PackageReference

É possível usar uma condição para controlar se um pacote está incluído, em que as condições podem usar qualquer variável MSBuild ou uma variável definida no arquivo de destinos ou objetos. No entanto, no momento, somente a variável `TargetFramework` é compatível.

Por exemplo, digamos que seu destino é `netstandard1.4` e `net452`, mas tem uma dependência que é aplicável somente para `net452`. Nesse caso, não é aconselhável ter um projeto `netstandard1.4` que está consumindo seu pacote para adicionar essa dependência desnecessária. Para evitar isso, você deve especificar uma condição no `PackageReference` da seguinte maneira:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

Um pacote compilado usando este projeto mostrará que Newtonsoft.json está incluído como uma dependência somente para um destino `net452`:

![O resultado da aplicação de uma condição em PackageReference com o VS2017](media/PackageReference-Condition.png)

As condições também podem ser aplicadas no nível de `ItemGroup` e serão aplicadas a todos os elementos `PackageReference` filhos:

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
