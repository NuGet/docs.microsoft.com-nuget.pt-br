---
title: Referência de versão do pacote do NuGet
description: Obter detalhes exatos sobre como especificar números de versão e intervalos para outros pacotes mediante o qual depende de um pacote do NuGet e como as dependências são instaladas.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 6407cd2ea5e5e7a9c9e2be679764a8a0d5dd9260
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852462"
---
# <a name="package-versioning"></a>Controle de versão do pacote

Um pacote específico é sempre chamado usando seu identificador de pacote e um número de versão exato. Por exemplo, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) em nuget.org tem vários pacotes específicos doze disponíveis, variando desde a versão *4.1.10311* para a versão *6.1.3* (o estável mais recente versão) e, como uma variedade de versões de pré-lançamento *6.2.0-beta1*.

Ao criar um pacote, você pode atribuir um número de versão específico com um sufixo de pré-lançamento um texto opcional. Ao consumir pacotes, por outro lado, você pode especificar um número de versão exato ou um intervalo de versões aceitáveis.

Neste tópico:

- [Noções básicas de versão](#version-basics) incluindo sufixos de versão de pré-lançamento.
- [Curingas e intervalos de versão](#version-ranges-and-wildcards)
- [Números de versão normalizado](#normalized-version-numbers)

## <a name="version-basics"></a>Noções básicas de versão

Um número de versão específico está no formato *Major [-sufixo]*, onde os componentes têm os seguintes significados:

- *Principais*: Alterações da falha
- *Pequenas*: Novos recursos, mas compatível com versões anteriores
- *Patch*: Somente correções de bug compatíveis com versões anteriores
- *-Sufixo* (opcional): um hífen seguido por uma cadeia de caracteres que indica uma versão de pré-lançamento (seguir as [convenção de SemVer 1.0 ou de controle de versão semântico](http://semver.org/spec/v1.0.0.html)).

**Exemplos:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> NuGet.org rejeita qualquer upload do pacote que não tem um número de versão exato. A versão deve ser especificada no `.nuspec` ou arquivo de projeto usado para criar o pacote.

### <a name="pre-release-versions"></a>As versões de pré-lançamento

Tecnicamente falando, criadores de pacote podem usar qualquer cadeia de caracteres como um sufixo a para denotar uma versão de pré-lançamento, como o NuGet trata qualquer versão tal como versões de pré-lançamento e não faz com que nenhuma outra interpretação. Ou seja, exibe o NuGet a versão completa da cadeia de caracteres em qualquer interface do usuário estiver envolvido, deixando qualquer interpretação do significado do sufixo para o consumidor.

Dito isso, os desenvolvedores de pacote geralmente seguem as convenções de nomenclatura reconhecidas:

- `-alpha`: Versão alfa, normalmente usado para em andamento e experimentação.
- `-beta`: Versão beta, normalmente uma completa com recursos para a próxima versão planejada, mas pode conter erros conhecidos.
- `-rc`: Versão Release Candidate, normalmente uma versão que é potencialmente a final (estável), a menos que surjam bugs significativos.

> [!Note]
> Dá suporte a NuGet 4.3.0 [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), que oferece suporte a números de versão de pré-lançamento com a notação de ponto, como em *1.0.1-build.23*. A notação de ponto não e compatível com as versões do NuGet anteriores à 4.3.0. Você pode usar um formulário como *1.0.1-build23*.

Para resolver referências de pacote e várias versões de pacote diferem apenas pelo sufixo, NuGet escolhe uma versão sem um sufixo pela primeira vez, em seguida, aplica-se a precedência para versões de pré-lançamento em ordem alfabética inversa. Por exemplo, as versões a seguir serão escolhidas na ordem exata mostrada:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Controle de versão semântico 2.0.0

Com o NuGet 4.3.0 e Visual Studio 2017 versão 15.3 ou superior, o NuGet dá suporte a [controle de versão semântico 2.0.0](http://semver.org/spec/v2.0.0.html).

Não há suporte para determinadas semântica de SemVer v2.0.0 em clientes mais antigos. O NuGet considerará uma versão do pacote de SemVer v2.0.0 específico se qualquer uma das instruções a seguir for verdadeira:

- O rótulo de pré-lançamento é separado por ponto, por exemplo, *1.0.0-alpha.1*
- A versão tem metadados de compilação, por exemplo, *1.0.0+githash*

Para nuget.org, um pacote é definido como um pacote de v2.0.0 SemVer se qualquer uma das instruções a seguir for verdadeira:

- A versão do pacote é SemVer v2.0.0 em conformidade, mas não SemVer v1.0.0 em conformidade, conforme definido acima.
- Qualquer um dos intervalos de versão de dependência do pacote tem uma versão mínima ou máxima é SemVer v2.0.0 em conformidade, mas não SemVer v1.0.0 em conformidade, definido acima; Por exemplo, *[1.0.0-alpha.1,)*.

Se você carregar um pacote do SemVer v2.0.0 específicas para o nuget.org, o pacote é invisível para os clientes mais antigos e está disponível para os seguintes clientes NuGet:

- O NuGet 4.3.0
- Visual Studio 2017 versão 15.3 ou superior
- Visual Studio 2015 com [v3.6.0 VSIX NuGet](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore.exe (.NET SDK 2.0.0+)

Clientes de terceiros:

- Rider da JetBrains
- Paket versão 5.0 ou superior

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>Curingas e intervalos de versão

Ao fazer referência às dependências do pacote, o NuGet dá suporte a usando a notação de intervalo para especificar os intervalos de versão, resumidos da seguinte maneira:

| Notation | Regra aplicada | Descrição |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | Versão mínima, inclusive |
| (1.0,) | x > 1.0 | Versão mínima, exclusivo |
| [1.0] | x = = 1.0 | Correspondência exata de versão |
| (,1.0] | x ≤ 1.0 | Versão máxima, inclusive |
| (,1.0) | x < 1.0 | Versão máxima, exclusivo |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Intervalo exato, inclusive |
| (1.0,2.0) | 1.0 < x < 2.0 | Intervalo exato, exclusivo |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | Misto inclusivo mínimo e exclusivo versão máxima do |
| (1.0)    | inválidos | inválidos |

Ao usar o formato PackageReference, o NuGet também suporta o uso de uma notação de curinga, \*, para Major, Minor, Patch e partes de sufixo de pré-lançamento do número. Não há suporte para caracteres curinga com o `packages.config` formato.

> [!Note]
> As versões de pré-lançamento não são incluídas durante a resolução de intervalos de versão. Versões de pré-lançamento *estão* incluídos ao usar um caractere curinga (\*). O intervalo de versão *[1.0,2.0]*, por exemplo, não incluem 2.0 beta, mas a notação de curinga _2.0-*_ faz. Ver [emitir 912](https://github.com/NuGet/Home/issues/912) para uma discussão mais detalhada sobre curingas de pré-lançamento.

### <a name="examples"></a>Exemplos

Sempre especifique uma versão ou intervalo de versão para dependências do pacote em arquivos de projeto `packages.config` arquivos, e `.nuspec` arquivos. Sem uma versão ou intervalo de versão, o NuGet 2.8.x e escolhe anteriormente a versão mais recente do pacote disponíveis ao resolver uma dependência, enquanto o NuGet 3.x e posterior, escolhe a versão mais antiga do pacote. Especificando uma versão ou intervalo evita essa incerteza.

#### <a name="references-in-project-files-packagereference"></a>Referências em arquivos de projeto (PackageReference)

```xml
<!-- Accepts any version 6.1 and above. -->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version. -->
<PackageReference Include="ExamplePackage" Version="6.*" />
<PackageReference Include="ExamplePackage" Version="[6,7)" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

**Referências no `packages.config`:**

Na `packages.config`, cada dependência é listada com um exata `version` atributo que é usado ao restaurar os pacotes. O `allowedVersions` atributo é usado somente durante as operações de atualização para restringir as versões aos quais o pacote pode ser atualizado.

```xml
<!-- Install/restore version 6.1.0, accept any version 6.1.0 and above on update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="6.1.0" />

<!-- Install/restore version 6.1.0, and do not change during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6.1.0]" />

<!-- Install/restore version 6.1.0, accept any 6.x version during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6,7)" />

<!-- Install/restore version 4.1.4, accept any version above, but not including, 4.1.3.
     Could be used to guarantee a dependency with a specific bug fix. -->
<package id="ExamplePackage" version="4.1.4" allowedVersions="(4.1.3,)" />

<!-- Install/restore version 3.1.2, accept any version up below 5.x on update, which might be
     used to prevent pulling in a later version of a dependency that changed its interface.
     However, this form is not recommended because it can be difficult to determine the lowest version. -->
<package id="ExamplePackage" version="3.1.2" allowedVersions="(,5.0)" />

<!-- Install/restore version 1.1.4, accept any 1.x or 2.x version on update, but not
     0.x or 3.x and higher. -->
<package id="ExamplePackage" version="1.1.4" allowedVersions="[1,3)" />

<!-- Install/restore version 1.3.5, accepts 1.3.2 up to 1.4.x on update, but not 1.5 and higher. -->
<package id="ExamplePackage" version="1.3.5" allowedVersions="[1.3.2,1.5)" />
```

**Referências no `.nuspec` arquivos**

O `version` de atributo em um `<dependency>` elemento descreve as versões de intervalo são aceitáveis para uma dependência.

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<dependency id="ExamplePackage" version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<dependency id="ExamplePackage" version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<dependency id="ExamplePackage" version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<dependency id="ExamplePackage" version="[1.3.2,1.5)" />
```

## <a name="normalized-version-numbers"></a>Números de versão normalizado

> [!Note]
> Isso é uma alteração significativa para o NuGet 3.4 e posterior.

Ao obter pacotes de um repositório durante a instalação, reinstalar ou restaurar as operações, o NuGet 3.4 ou superior trata números de versão da seguinte maneira:

- Zeros à esquerda são removidos de números de versão:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Um zero na quarta parte do número de versão será omitido

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

Essa normalização não afeta os números de versão dos pacotes em si; ela afeta como o NuGet corresponde apenas versões ao resolver as dependências.

No entanto, os repositórios de pacote do NuGet devem tratar esses valores da mesma maneira como o NuGet para evitar a duplicação de versão do pacote. Portanto, um repositório que contém a versão *1.0* de um pacote não devem também hospedar versão *1.0.0* como um pacote separado e diferente.
