---
title: Referência da versão do pacote NuGet
description: Detalhes exatos sobre a especificação de números de versão e intervalos para outros pacotes dos quais um pacote NuGet depende e como as dependências são instaladas.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 7c6992d6bf3142eb6aca70f1fa3c46f72efd25a0
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69520346"
---
# <a name="package-versioning"></a>Controle de versão do pacote

Um pacote específico é sempre referenciado usando seu identificador de pacote e um número de versão exato. Por exemplo, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) em nuget.org tem várias dezenas de pacotes específicos disponíveis, desde a versão *4.1.10311* até a versão *6.1.3* (a última versão estável) e uma variedade de versões de pré-lançamento, como *6.2.0-beta1*.

Ao criar um pacote, você atribui um número de versão específico a um sufixo de texto de pré-lançamento opcional. Ao consumir pacotes, por outro lado, você pode especificar um número de versão exato ou um intervalo de versões aceitáveis.

Neste tópico:

- [Noções básicas sobre versão](#version-basics), incluindo sufixos de pré-lançamento.
- [Intervalos de versão e curingas](#version-ranges-and-wildcards)
- [Números de versão normalizados](#normalized-version-numbers)

## <a name="version-basics"></a>Noções básicas sobre versão

Um número de versão específico está no formato *Principal.Secundário.Patch [-Sufixo]* , em que os componentes possuem os seguintes significados:

- *Principal*: Alterações da falha
- *Secundária*: Novos recursos, mas compatível com versões anteriores
- *Patch*: Somente correções de bug compatíveis com versões anteriores
- *-Sufixo* (opcional): um hífen seguido por uma cadeia de caracteres denotando uma versão de pré-lançamento (seguindo a [convenção Controle de Versão Semântico ou SemVer 1.0](http://semver.org/spec/v1.0.0.html)).

**Exemplos:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org rejeita qualquer upload de pacote que não tenha um número de versão exato. A versão precisa ser especificada no `.nuspec` ou no arquivo de projeto usado para criar o pacote.

### <a name="pre-release-versions"></a>Versões de pré-lançamento

Tecnicamente falando, os criadores de pacotes podem usar qualquer cadeia de caracteres como sufixo para denotar uma versão de pré-lançamento, já que o NuGet trata qualquer versão como pré-lançamento e não faz outra interpretação. Ou seja, o NuGet exibe a cadeia de caracteres de versão completa em qualquer interface do usuário, deixando qualquer interpretação do significado do sufixo para o consumidor.

Dito isso, os desenvolvedores de pacotes geralmente seguem as convenções de nomenclatura reconhecidas:

- `-alpha`: versão alfa, normalmente usada para trabalho em andamento e experimentação.
- `-beta`: Versão beta, normalmente uma completa com recursos para a próxima versão planejada, mas pode conter erros conhecidos.
- `-rc`: Versão Release Candidate, normalmente uma versão que é potencialmente a final (estável), a menos que surjam bugs significativos.

> [!Note]
> O NuGet 4.3.0+ é compatível com o [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), que oferece suporte para números com notação de ponto pré-lançamento, como no *1.0.1-build.23*. A notação de ponto não e compatível com as versões do NuGet anteriores à 4.3.0. Você pode usar um formulário como *1.0.1-build23*.

Quando as referências de pacote e várias versões de pacote diferem apenas pelo sufixo, o NuGet escolhe uma versão sem um sufixo primeiro e, em seguida, aplica a precedência às versões de pré-lançamento em ordem alfabética inversa. Por exemplo, as seguintes versões seriam escolhidas na ordem exata mostrada:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Controle de Versão Semântico 2.0.0

Com o NuGet 4.3.0+ e o Visual Studio 2017 versão 15.3+, o NuGet oferece suporte ao [Controle de Versão Semântico 2.0.0](http://semver.org/spec/v2.0.0.html).

Determinadas semânticas do SemVer v2.0.0 não têm suporte em clientes mais antigos. O NuGet considerará uma versão do pacote como SemVer v2.0.0 específica se qualquer uma das seguintes afirmações for verdadeira:

- O rótulo de pré-lançamento é separado por pontos, por exemplo,*1.0.0-alpha.1*
- A versão tem metadados de build, por exemplo, *1.0.0+githash*

Para nuget.org, um pacote será definido como um pacote SemVer v2.0.0 se qualquer uma das seguintes afirmações for verdadeira:

- A versão do pacote é compatível com SemVer v2.0.0, mas não compatível com SemVer v1.0.0, conforme definido acima.
- Qualquer um dos intervalos de versão de dependência do pacote tem uma versão mínima ou máxima que é compatível com SemVer v2.0.0, mas não compatível com SemVer v1.0.0, definida acima; por exemplo, *[1.0.0-alpha.1, )* .

Se você carregar um pacote específico do SemVer v2.0.0 para o nuget.org, o pacote ficará invisível para os clientes mais antigos e estará disponível apenas para os seguintes clientes do NuGet:

- NuGet 4.3.0+
- Versão do Visual Studio 2017 15.3+
- Visual Studio 2015 com [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore.exe (.NET SDK 2.0.0+)

Clientes de terceiros:

- JetBrains Rider
- Paket versão 5.0+

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>Intervalos de versão e curingas

Ao se referir a dependências de pacote, o NuGet oferece suporte ao uso de notação de intervalo para especificar intervalos de versão, resumidos da seguinte forma:

| Notation | Regra aplicada | DESCRIÇÃO |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | Versão mínima, inclusiva |
| (1.0,) | x > 1.0 | Versão mínima, exclusiva |
| [1.0] | x == 1.0 | Correspondência exata da versão |
| (,1.0] | x ≤ 1.0 | Versão máxima, inclusiva |
| (,1.0) | x < 1.0 | Versão máxima, exclusiva |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Intervalo exato, inclusivo |
| (1.0,2.0) | 1.0 < x < 2.0 | Intervalo exato, exclusivo |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | Versão mínima inclusiva e máxima exclusiva combinadas |
| (1.0)    | inválidos | inválidos |

Ao usar o formato PackageReference, o NuGet também oferece suporte ao uso de uma notação de curinga, \*, para as partes principal, secundária, patch e de sufixo de pré-lançamento do número. Não há suporte para caracteres curinga com o formato `packages.config`.

> [!Note]
> Os intervalos de versão no PackageReference incluem versões de pré-lançamento. Por design, versões flutuantes não resolvem as versões de pré-lançamento, a menos que sejam aceitas. Para obter o status da solicitação de recurso relacionada, confira [Problema 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).

### <a name="examples"></a>Exemplos

Sempre especifique uma versão ou intervalo de versão para dependências de pacote em arquivos de projeto, arquivos `packages.config` e arquivos `.nuspec`. Sem uma versão ou intervalo de versão, o NuGet 2.8.x e versões anteriores escolhem a versão do pacote disponível mais recente ao resolver uma dependência, enquanto o NuGet 3.xe posterior escolhe a versão de pacote mais baixa. Especificar uma versão ou um intervalo de versões evita essa incerteza.

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

**Referências em `packages.config`:**

Em `packages.config`, toda dependência é listada com um atributo de `version` exato que é usado ao restaurar pacotes. O atributo `allowedVersions` é usado apenas durante as operações de atualização para restringir as versões às quais o pacote pode ser atualizado.

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

**Referências em arquivos `.nuspec`**

O atributo `version` em um elemento `<dependency>` descreve as versões de intervalo aceitáveis ​​para uma dependência.

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

## <a name="normalized-version-numbers"></a>Números de versão normalizados

> [!Note]
> Essa é uma alteração significativa para o NuGet 3.4 e posterior.

Ao obter pacotes de um repositório durante a instalação, reinstalação ou restauração de operações, o NuGet 3.4+ trata os números de versão da seguinte maneira:

- Zeros à esquerda são removidos dos números de versão:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- um zero na quarta parte do número de versão será omitido

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

As operações `pack` e `restore` normalizam as versões sempre que possível. Para pacotes já compilados, essa normalização não afeta os números de versão nos próprios pacotes; ela afeta apenas como o NuGet faz a correspondência das versões ao resolver dependências.

No entanto, os repositórios de pacotes do NuGet devem tratar esses valores da mesma maneira que o NuGet para evitar a duplicação da versão do pacote. Portanto, um repositório que contenha a versão *1.0* de um pacote não deve hospedar também a versão *1.0.0* como um pacote separado e diferente.