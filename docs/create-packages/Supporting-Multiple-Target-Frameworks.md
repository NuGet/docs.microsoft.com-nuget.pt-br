---
title: Multiplataforma para pacotes do NuGet
description: Descrição dos diversos métodos para várias versões do .NET Framework de dentro de um único pacote do NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 34f7c6132ba6050e20114642932ccf29a5ec088d
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75385090"
---
# <a name="support-multiple-net-versions"></a>Suporte a várias versões do .NET

Muitas bibliotecas se destinam a uma versão específica do .NET Framework. Por exemplo, você pode ter uma versão da biblioteca específica para a UWP e outra versão para aproveitar os recursos no .NET Framework 4.6. Para acomodar isso, o NuGet é compatível com a colocação de várias versões da mesma biblioteca em um único pacote.

Este artigo descreve o layout de um pacote NuGet, independentemente de como o pacote ou os assemblies são compilados (ou seja, o layout é o mesmo se você estiver usando vários arquivos *. csproj* de estilo não SDK e um arquivo *. nuspec* personalizado, ou um único SDK multiplataforma-Style *. csproj*). Para um projeto no estilo SDK, os [destinos do pacote](../reference/msbuild-targets.md) do NuGet reconhecem como o pacote deve ser definido e automatiza a colocação dos assemblies nas pastas corretas da biblioteca e a criação de grupos de dependências para cada estrutura de destino (TFM). Para saber mais, confira [Suporte a várias versões de .NET Framework em seu arquivo de projeto](multiple-target-frameworks-project-file.md).

Você deve definir manualmente o pacote conforme descrito neste artigo ao usar o método de diretório de trabalho baseado em convenções descrito em [Criar um pacote](../create-packages/creating-a-package.md#from-a-convention-based-working-directory). Para um projeto em estilo SDK, é recomendado o método automatizado, mas você também pode optar por definir manualmente o pacote como descrito neste artigo.

## <a name="framework-version-folder-structure"></a>Estrutura da pasta de versão do Framework

Ao compilar um pacote que contém somente uma versão de uma biblioteca ou destinado a várias estruturas, sempre crie as subpastas em `lib` usando nomes de estrutura que diferenciam maiúsculas de minúsculas com a seguinte convenção:

    lib\{framework name}[{version}]

Para ver uma lista completa de nomes compatíveis, consulte a [Referência a Estruturas de Destino](../reference/target-frameworks.md#supported-frameworks).

Você nunca deve ter uma versão da biblioteca que não seja específico para uma estrutura e colocada diretamente na pasta `lib` raiz. (Essa capacidade era compatível somente com `packages.config`). Isso tornaria a biblioteca compatível com qualquer estrutura de destino e permitiria que ela fosse instalada em qualquer lugar, provavelmente resultando em erros de runtime inesperados. A adição de assemblies à pasta raiz (como `lib\abc.dll`) ou subpastas (como `lib\abc\abc.dll`) foi preterida e será ignorada ao usar o formato de PackagesReference.

Por exemplo, a seguinte estrutura de pastas a seguir é compatível com quatro versões de um assembly que são específicas da estrutura:

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

Para incluir facilmente todos esses arquivos ao criar o pacote, use um curinga `**` recursivo na seção `<files>` do seu `.nuspec`:

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a>Pastas específicas de arquitetura

Se você tiver assemblies específicos de arquitetura, ou seja, assemblies separados destinados ao ARM, x86 e x64, será preciso colocá-los em uma pasta chamada `runtimes` dentro de subpastas denominadas `{platform}-{architecture}\lib\{framework}` ou `{platform}-{architecture}\native`. Por exemplo, a seguinte estrutura de pasta acomodaria DLLs nativos e gerenciados direcionados para o Windows 10 e a estrutura `uap10.0`:

    \runtimes
        \win10-arm
            \native
            \lib\uap10.0
        \win10-x86
            \native
            \lib\uap10.0
        \win10-x64
            \native
            \lib\uap10.0

Esses assemblies só estarão disponíveis no runtime, portanto, se você quiser fornecer o assembly de tempo de compilação correspondente, também terá um assembly `AnyCPU` na pasta `/ref/{tfm}`. 

O NuGet sempre escolhe esses recursos de compilação ou de runtime de uma pasta, portanto, se houver alguns ativos compatíveis de `/ref`, `/lib` será ignorado para adicionar conjuntos de tempo de compilação. Da mesma forma, se houver alguns ativos compatíveis de `/runtimes`, então `/lib` serão ignorados para tempo de execução.

Consulte [Criar pacotes de UWP](../guides/create-uwp-packages.md) para obter um exemplo de referência a esses arquivos no manifesto `.nuspec`.

Confira também [Como empacotar um componente de aplicativo da Windows Store com o NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a>Correspondendo versões de assembly e a estrutura de destino em um projeto

Quando o NuGet instala um pacote que tem várias versões de assembly, ele tenta corresponder o nome da estrutura do assembly com a estrutura de destino do projeto.

Se nenhuma correspondência for encontrada, o NuGet copia o assembly para a versão mais recente que seja menor ou igual à estrutura de destino do projeto, se disponível. Se nenhum assembly compatível for localizado, o NuGet retornará uma mensagem de erro apropriado.

Considere, por exemplo, a estrutura de pastas a seguir em um pacote:

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

Ao instalar esse pacote em um projeto voltado para o .NET Framework 4.6, o NuGet instala o assembly na pasta `net45`, pois é a versão mais recente disponível que é menor ou igual a 4.6.

Se o projeto se destina ao .NET Framework 4.6.1, por outro lado, o NuGet instala o assembly na pasta `net461`.

Se o projeto se destina ao .NET framework 4.0 e versões anterior, o NuGet gera uma mensagem de erro apropriada por não encontrar o assembly compatível.

## <a name="grouping-assemblies-by-framework-version"></a>Agrupando assemblies por versão de estrutura

O NuGet copia assemblies apenas de uma única pasta de biblioteca no pacote. Suponha, por exemplo, que um pacote tem a seguinte estrutura de pastas:

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

Quando o pacote é instalado em um projeto voltado para o .NET Framework 4.5, `MyAssembly.dll` (v2.0) é o único assembly instalado. `MyAssembly.Core.dll` (v1.0) não está instalado, porque ele não está listado na pasta `net45`. O NuGet se comporta dessa maneira porque `MyAssembly.Core.dll` pode ter sido mesclado na versão 2.0 do `MyAssembly.dll`.

Se você quiser que `MyAssembly.Core.dll` seja instalado para o .NET Framework 4.5, coloque uma cópia na pasta `net45`.

## <a name="grouping-assemblies-by-framework-profile"></a>Agrupando assemblies por perfil de estrutura

O NuGet também dá suporte ao direcionamento a um perfil de estrutura específico acrescentando um traço e o nome do perfil ao fim da pasta.

    lib\{framework name}-{profile}

Os perfis compatíveis são os seguintes:

- `client`: Perfil do cliente
- `full`: Perfil completo
- `wp`: Windows Phone
- `cf`: Compact Framework

## <a name="declaring-dependencies-advanced"></a>Declarar dependências (Avançado)

Ao empacotar um arquivo de projeto, o NuGet tenta gerar automaticamente as dependências do projeto. As informações nesta seção sobre como usar um arquivo *.nuspec* para declarar as dependências normalmente são necessárias apenas em cenários avançados.

*(Versão 2.0+)* Você pode declarar as dependências de pacote no *.nuspec* correspondente à estrutura do projeto de destino usando elementos `<group>` no elemento `<dependencies>`. Para saber mais, confira [elemento dependencies](../reference/nuspec.md#dependencies-element).

Cada grupo tem um atributo chamado `targetFramework` e contém zero ou mais elementos `<dependency>`. Essas referências são instaladas juntas quando a estrutura de destino é compatível com o perfil da estrutura do projeto. Consulte [Estruturas de destino](../reference/target-frameworks.md) para ver os identificadores de estrutura exatos.

Recomendamos usar um grupo por TFM (Moniker da Estrutura de Destino) para arquivos nas pastas *lib/* e *ref/* .

O exemplo a seguir mostra diferentes variações do elemento `<group>`:

```xml
<dependencies>

    <group targetFramework="net472">
        <dependency id="jQuery" version="1.10.2" />
        <dependency id="WebActivatorEx" version="2.2.0" />
    </group>

    <group targetFramework="net20">
    </group>

</dependencies>
```

## <a name="determining-which-nuget-target-to-use"></a>Determinar qual destino do NuGet deve ser usado

Quando pacotes de bibliotecas são direcionados à Biblioteca de Classes Portátil, pode ser difícil determinar qual destino NuGet deve ser usado nos nomes de pastas e no arquivo `.nuspec`, especialmente se o direcionamento for apenas de um subconjunto do PCL. Os seguintes recursos externos ajudarão você com isso:

- [Perfis de Framework no .NET](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)
- [Perfis de Biblioteca de Classes Portátil](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): tabela que enumera os perfis de PCL e suas metas equivalentes do NuGet
- [Ferramenta de perfis da Biblioteca de Classes Portátil](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): ferramenta de linha de comando para determinar perfis de PCL disponíveis no sistema

## <a name="content-files-and-powershell-scripts"></a>Arquivos de conteúdo e scripts do PowerShell

> [!Warning]
> Arquivos de conteúdo mutáveis e a execução de script estão disponíveis somente no formato `packages.config`; eles são preteridos com todos os outros formatos e não deve ser usado para nenhum pacote novo.

Com `packages.config`, arquivos de conteúdo e scripts do PowerShell podem ser agrupados pela estrutura de destino usando a mesma convenção de pasta dentro das pastas `content` e `tools`. Por exemplo:

    \content
        \net46
            \MyContent.txt
        \net461
            \MyContent461.txt
        \uap
            \MyUWPContent.html
        \netcore
    \tools
        init.ps1
        \net46
            install.ps1
            uninstall.ps1
        \uap
            install.ps1
            uninstall.ps1

Se uma pasta da estrutura for deixada vazia, o NuGet não adiciona referência de assembly ou arquivos de conteúdo, nem executam os scripts do PowerShell para essa estrutura.

> [!Note]
> Como `init.ps1` é executado no nível da solução e não depende do projeto, ele precisa ser colocado diretamente na pasta `tools`. Será ignorado se colocado em uma pasta da estrutura.
