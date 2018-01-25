---
title: "Referência de versão do pacote do NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Informações sobre como especificar números de versão e intervalos para outros pacotes que depende de um pacote do NuGet e como as dependências estejam instaladas."
keywords: "controle de versão, as dependências de pacotes do NuGet, versões de dependência NuGet, números de versão do NuGet, versão do pacote NuGet, intervalos de versão, especificações de versão, os números de versão normalizada"
ms.reviewer:
- anandr
- karann-msft
- unniravindranathan
ms.openlocfilehash: 70472d7d97d073009237a047e0fdf528b221dfd0
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="package-versioning"></a>Controle de versão do pacote

Um pacote específico é sempre chamado usando seu identificador de pacote e um número de versão exata. Por exemplo, [do Entity Framework](https://www.nuget.org/packages/EntityFramework/) em nuget.org tem vários pacotes específicos de doze disponíveis, variando de versão *4.1.10311* versão *6.1.3* (o mais recente estável versão) e uma variedade de versões de pré-lançamento como *6.2.0-beta1*.

Ao criar um pacote, você pode atribuir um número de versão específico com um sufixo de texto opcional de pré-lançamento. Ao consumir pacotes, por outro lado, você pode especificar um número de versão exata ou um intervalo de versões aceitáveis.

Neste tópico:

- [Noções básicas de versão](#version-basics) incluindo sufixos de versão de pré-lançamento.
- [Curingas e intervalos de versão](#version-ranges-and-wildcards)
- [Números de versão normalizado](#normalized-version-numbers)

## <a name="version-basics"></a>Noções básicas de versão

Um número de versão específico está no formato *Major [-sufixo]*, onde os componentes têm os seguintes significados:

- *Principais*: alterações recentes
- *Secundária*: novos recursos, mas compatível com versões anteriores
- *Patch*: correções de bugs compatíveis com versões anteriores somente
- *-Sufixo* (opcional): um hífen seguido por uma cadeia de caracteres que indica uma versão de pré-lançamento (seguir o [convenção de controle de versão semântico ou 1.0 SemVer](http://semver.org/spec/v1.0.0.html)).

**Exemplos:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> NuGet.org rejeita qualquer upload do pacote que não tem um número de versão exata. A versão deve ser especificada no `.nuspec` ou arquivo de projeto usado para criar o pacote.

### <a name="pre-release-versions"></a>As versões de pré-lançamento

Tecnicamente, os criadores de pacote podem usar qualquer cadeia de caracteres como um sufixo a para denotar uma versão de pré-lançamento, como NuGet trata qualquer versão tal como pré-lançamento e não faz com que nenhum outra interpretação. Ou seja, o NuGet exibe a versão completa da cadeia de caracteres em qualquer interface de usuário estiver envolvido, deixando qualquer interpretação do significado do sufixo para o consumidor.

Dito isso, os desenvolvedores geralmente seguem as convenções de nomenclatura reconhecidas:

- `-alpha`: Versão alfa, normalmente usado para o trabalho em andamento e experimentação.
- `-beta`: versão beta, normalmente uma completa com recursos para a próxima versão planejada, mas pode conter erros conhecidos.
- `-rc`: versão Release candidate, normalmente uma versão que é potencialmente a final (estável), a menos que surjam bugs significativos.

> [!Note]
> Oferece suporte a 4.3.0+ NuGet [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), que oferece suporte a números de versão de pré-lançamento com a notação de ponto, como em *1.0.1-build.23*. Não há suporte para a notação de ponto com as versões anteriores ao 4.3.0 NuGet. Você pode usar um formulário como *1.0.1-build23*.

Ao resolver referências de pacote e várias versões de pacote são diferentes apenas pelo sufixo, NuGet escolhe uma versão sem um sufixo primeiro, em seguida, aplica-se a prioridade para as versões em ordem alfabética inversa de pré-lançamento. Por exemplo, as versões a seguir serão escolhidas na ordem exata mostrado:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Controle de versão semântico 2.0.0

Com o NuGet 4.3.0+ e Visual Studio 2017 versão 15,3 +, NuGet dá suporte a [o controle de versão semântico 2.0.0](http://semver.org/spec/v2.0.0.html).

Não há suporte para determinados semântica de v SemVer 2.0.0 em clientes mais antigos. NuGet considera uma versão do pacote a ser SemVer v 2.0.0 específico se qualquer uma das instruções a seguir for verdadeira:

- O rótulo de pré-lançamento é separado por pontos, por exemplo, *1.0.0-alpha.1*
- A versão tem metadados de compilação, por exemplo, *1.0.0+githash*

Para nuget.org, um pacote é definido como um pacote de v 2.0.0 SemVer se qualquer uma das instruções a seguir for verdadeira:

- A versão do pacote é SemVer v 2.0.0 compatível, mas não SemVer v1.0.0 compatíveis, conforme definido acima.
- Nenhum dos intervalos de versão de dependência do pacote tem uma versão mínima ou máxima é SemVer v 2.0.0 compatível, mas não SemVer v1.0.0 compatíveis, definidos acima. Por exemplo, *[1.0.0-alpha.1,)*.

Se você carregar um pacote de v 2.0.0 específico SemVer nuget.org, o pacote é invisível para clientes mais antigos e disponível para os seguintes clientes NuGet:

- NuGet 4.3.0+
- Visual Studio 2017 versão 15,3 +
- Visual Studio 2015 com [v3.6.0 VSIX NuGet](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet.exe (2.0.0+ .NET SDK)

Clientes de terceiros:

- Cláusula JetBrains adicional
- Paket versão 5.0 +

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>Curingas e intervalos de versão

Ao fazer referência a dependências do pacote, NuGet suporta usando a notação de intervalo para especificar os intervalos de versão, resumidos da seguinte maneira:

| Notation | Regra aplicada | Descrição |
|----------|--------------|-------------|
| 1.0 | 1.0 ≤ x | Versão mínima, inclusive |
| (1.0,) | 1.0 < x | Versão mínima, exclusivo |
| [1.0] | x = = 1.0 | Correspondência exata de versão |
| (,1.0] | x ≤ 1.0 | Versão máxima, inclusive |
| (,1.0) | x < 1.0 | Versão máxima, exclusivo |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Intervalo exato, inclusive |
| (1.0,2.0) | 1.0 < x < 2.0 | Intervalo exato, exclusivo |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | Mista inclusivo mínima e exclusiva máximo da versão |
| (1.0)    | inválidos | inválidos |

Ao usar o formato PackageReference, os NuGet também oferece suporte ao uso de uma notação de curinga, \*, para o principal, secundária, Patch e partes de sufixo de pré-lançamento do número. Não há suporte para caracteres curinga com o `packages.config` formato.

> [!Note]
> As versões de pré-lançamento não são incluídas durante a resolução de intervalos de versão. As versões de pré-lançamento *são* incluído ao usar um caractere curinga (\*). O intervalo de versão *[1.0,2.0]*, por exemplo, não inclua 2.0 beta, mas a notação de curinga _2.0-*_ does. Consulte [emitir 912](https://github.com/NuGet/Home/issues/912) para uma discussão mais detalhada em pré-lançamento curingas.

### <a name="examples"></a>Exemplos

Sempre especifique uma versão ou um intervalo de versão para as dependências do pacote em arquivos de projeto, `packages.config` arquivos, e `.nuspec` arquivos. Sem uma versão ou um intervalo de versão, o NuGet 2.8.x e escolhe anteriormente a versão mais recente do pacote disponíveis ao resolver uma dependência, enquanto o NuGet 3. x e posterior escolhe a versão mais antiga do pacote. Especificando uma versão ou intervalo evita este incerteza.

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

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

**Referências em `packages.config`:**

Em `packages.config`, cada dependência é listada com um exata `version` atributo que é usado durante a restauração de pacotes. O `allowedVersions` atributo é usado somente durante as operações de atualização para restringir as versões aos quais o pacote pode ser atualizado.

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

O `version` atributo em um `<dependency>` elemento descreve as versões de intervalo são aceitáveis em uma dependência.

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any 6.x.y version. -->
<dependency id="ExamplePackage" version="6.*" />

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
> Isso é uma alteração significativa para NuGet 3.4 e versões posteriores.

Ao obter pacotes de um repositório durante a instalação, reinstale ou restaurar as operações, o NuGet 3.4 + trata números de versão da seguinte maneira:

- Zeros à esquerda são removidos dos números de versão:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Um zero na quarta parte do número de versão será omitido

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

Essa normalização não afeta os números de versão dos pacotes em si; ele afeta somente como NuGet corresponde versões durante a resolução de dependências.

No entanto, os repositórios de pacote do NuGet devem tratar esses valores da mesma maneira como o NuGet para evitar duplicação de versão do pacote. Portanto, um repositório que contém a versão *1.0* de um pacote não devem também hospedar versão *1.0.0* como um pacote diferente e separado.
