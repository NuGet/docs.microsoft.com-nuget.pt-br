---
title: Referência de versão do pacote NuGet
description: Detalhes exatos sobre a especificação de números de versão e intervalos para outros pacotes sobre os quais um pacote NuGet depende e como as dependências são instaladas.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 7c6992d6bf3142eb6aca70f1fa3c46f72efd25a0
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69019991"
---
# <a name="package-versioning"></a>Controle de versão do pacote

Um pacote específico sempre é referenciado usando seu identificador de pacote e um número de versão exato. Por exemplo, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) no NuGet.org tem várias dúzias de pacotes específicos disponíveis, variando da versão *4.1.10311* para a versão *6.1.3* (a versão estável mais recente) e uma variedade de versões de pré-lançamento como *6.2.0-beta1* .

Ao criar um pacote, você atribui um número de versão específico com um sufixo de texto de pré-lançamento opcional. Ao consumir pacotes, por outro lado, você pode especificar um número de versão exato ou um intervalo de versões aceitáveis.

Neste tópico:

- [Noções básicas de versão](#version-basics) , incluindo sufixos de pré-lançamento.
- [Intervalos de versão e curingas](#version-ranges-and-wildcards)
- [Números de versão normalizados](#normalized-version-numbers)

## <a name="version-basics"></a>Noções básicas da versão

Um número de versão específico está no formato *Major. Minor. patch [-suffix]* , em que os componentes têm os seguintes significados:

- *Principal*: Alterações da falha
- *Secundária*: Novos recursos, mas compatível com versões anteriores
- *Patch*: Somente correções de bug compatíveis com versões anteriores
- *-Sufixo* (opcional): um hífen seguido por uma cadeia de caracteres que denota uma versão de pré-lançamento (seguindo a [Convenção de controle de versão semântico ou SemVer 1,0](http://semver.org/spec/v1.0.0.html)).

**Disso**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org rejeita qualquer upload de pacote que não tem um número de versão exato. A versão deve ser especificada no arquivo `.nuspec` de projeto ou usado para criar o pacote.

### <a name="pre-release-versions"></a>Versões de pré-lançamento

Tecnicamente, os criadores de pacote podem usar qualquer cadeia de caracteres como um sufixo para denotar uma versão de pré-lançamento, pois o NuGet trata dessa versão como pré-lançamento e não faz outra interpretação. Ou seja, o NuGet exibe a cadeia de caracteres da versão completa em qualquer interface do usuário envolvida, deixando qualquer interpretação do significado do sufixo para o consumidor.

Dito isso, os desenvolvedores de pacotes geralmente seguem as convenções de nomenclatura reconhecidas:

- `-alpha`: Versão Alfa, normalmente usada para trabalho em andamento e experimentação.
- `-beta`: Versão beta, normalmente uma completa com recursos para a próxima versão planejada, mas pode conter erros conhecidos.
- `-rc`: Versão Release Candidate, normalmente uma versão que é potencialmente a final (estável), a menos que surjam bugs significativos.

> [!Note]
> O NuGet 4.3.0 + dá suporte a [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), que dá suporte a números de pré-lançamento com notação de ponto, como em *1.0.1-Build. 23*. A notação de ponto não e compatível com as versões do NuGet anteriores à 4.3.0. Você pode usar um formulário como o *1.0.1-build23*.

Ao resolver referências de pacote e várias versões de pacote diferem somente por sufixo, o NuGet escolhe uma versão sem um sufixo primeiro e aplica precedência às versões de pré-lançamento em ordem alfabética inversa. Por exemplo, as seguintes versões seriam escolhidas na ordem exata mostrada:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>2\.0.0 de controle de versão semântico

Com o NuGet 4.3.0 + e o Visual Studio 2017 versão 15.3 +, o NuGet dá suporte à [2.0.0 semântica de controle de versão](http://semver.org/spec/v2.0.0.html).

Não há suporte para determinadas semânticas de SemVer v 2.0.0 em clientes mais antigos. O NuGet considera uma versão de pacote como SemVer v 2.0.0 específica se qualquer uma das seguintes instruções for verdadeira:

- O rótulo de pré-lançamento é separado por ponto, por exemplo, *1.0.0-Alpha. 1*
- A versão tem metadados de compilação, por exemplo, *1.0.0 + githash*

Para nuget.org, um pacote é definido como um pacote SemVer v 2.0.0 se uma das seguintes instruções for verdadeira:

- A versão do pacote é em conformidade com o SemVer v 2.0.0, mas não com o SemVer v 1.0.0 em conformidade, conforme definido acima.
- Qualquer um dos intervalos de versão de dependência do pacote tem uma versão mínima ou máxima que está em conformidade com o SemVer v 2.0.0, mas não com o SemVer v 1.0.0 em conformidade, definido acima; por exemplo, *[1.0.0-Alpha. 1,)* .

Se você carregar um pacote específico do SemVer v 2.0.0 no nuget.org, o pacote será invisível para clientes mais antigos e estará disponível apenas para os seguintes clientes do NuGet:

- NuGet 4.3.0 +
- Visual Studio 2017 versão 15.3 +
- Visual Studio 2015 com [NUGET VSIX v 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore. exe (SDK do .NET 2.0.0 +)

Clientes de terceiros:

- Cláusula JetBrains
- Paket versão 5.0 +

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>Intervalos de versão e curingas

Ao fazer referência a dependências de pacote, o NuGet dá suporte ao uso de notação de intervalo para especificar intervalos de versão, resumido da seguinte maneira:

| Notation | Regra aplicada | Descrição |
|----------|--------------|-------------|
| 1.0 | x ≥ 1,0 | Versão mínima, inclusiva |
| (1.0,) | x > 1,0 | Versão mínima, exclusiva |
| [1.0] | x = = 1,0 | Correspondência de versão exata |
| (,1.0] | x ≤ 1,0 | Versão máxima, inclusiva |
| (,1.0) | x < 1.0 | Versão máxima, exclusiva |
| [1.0,2.0] | 1,0 ≤ x ≤ 2,0 | Intervalo exato, inclusivo |
| (1.0,2.0) | 1,0 < x < 2,0 | Intervalo exato, exclusivo |
| [1.0,2.0) | 1,0 ≤ x < 2,0 | Versão mínima inclusiva e exclusiva misturada |
| (1.0)    | inválidos | inválidos |

Ao usar o formato PackageReference, o NuGet também dá suporte ao uso de \*uma notação curinga, para as partes de sufixo principal, secundária, patch e de pré-lançamento do número. Não há suporte para caracteres curinga com `packages.config` o formato.

> [!Note]
> Os intervalos de versão no PackageReference incluem versões de pré-lançamento. Por design, as versões flutuantes não resolvem versões de pré-lançamento, a menos que tenham optado por. Para obter o status da solicitação de recurso relacionada, consulte o [problema 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).

### <a name="examples"></a>Exemplos

Sempre especifique uma versão ou intervalo de versão para dependências de pacote em `packages.config` arquivos de projeto `.nuspec` , arquivos e arquivos. Sem uma versão ou intervalo de versão, o NuGet 2.8. x e anterior escolhe a versão de pacote mais recente disponível ao resolver uma dependência, enquanto o NuGet 3. x e posterior escolhe a versão de pacote mais baixa. A especificação de uma versão ou intervalo de versão evita essa incerteza.

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

No `packages.config`, cada dependência é listada com um `version` atributo exato que é usado durante a restauração de pacotes. O `allowedVersions` atributo é usado somente durante operações de atualização para restringir as versões para as quais o pacote pode ser atualizado.

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

**Referências em `.nuspec` arquivos**

O `version` atributo em um `<dependency>` elemento descreve as versões de intervalo aceitáveis para uma dependência.

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
> Essa é uma alteração significativa para o NuGet 3,4 e posterior.

Ao obter pacotes de um repositório durante as operações de instalação, reinstalação ou restauração, o NuGet 3.4 + trata os números de versão da seguinte maneira:

- Os zeros à esquerda são removidos dos números de versão:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Um zero na quarta parte do número de versão será omitido

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

`pack`e `restore` as operações normalizam versões sempre que possível. Para pacotes já compilados, essa normalização não afeta os números de versão nos próprios pacotes; Ele afeta apenas o modo como o NuGet corresponde às versões ao resolver as dependências.

No entanto, os repositórios do pacote NuGet devem tratar esses valores da mesma forma que o NuGet para impedir a duplicação da versão do pacote. Portanto, um repositório que contém a versão *1,0* de um pacote também não deve hospedar a versão *1.0.0* como um pacote separado e diferente.
