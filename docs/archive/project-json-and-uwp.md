---
title: Arquivo project.json do NuGet com projetos UWP
description: Descrição de como o arquivo project.json é usado para rastrear dependências do NuGet em projetos UWP (Plataforma Universal do Windows).
author: JonDouglas
ms.author: jodou
ms.date: 07/17/2017
ms.topic: conceptual
ms.openlocfilehash: 30e2272aafb5d2ea8d932e3cb0209d97c30b3209
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773805"
---
# <a name="projectjson-and-uwp"></a>project.json e UWP

> [!Important]
> Este conteúdo foi preterido. Os projetos devem usar os formatos `packages.config` ou PackageReference.

Este documento descreve a estrutura do pacote que utiliza os recursos do NuGet 3 ou superior (Visual Studio 2015 e posterior). A propriedade `minClientVersion` do seu `.nuspec` pode ser usada para indicar que você requer os recursos descritos aqui definindo-a para 3.1.

## <a name="adding-uwp-support-to-an-existing-package"></a>Adicionar suporte para UWP a um pacote existente

Se você tiver um pacote existente e desejar adicionar suporte para aplicativos UWP, não será necessário adotar o formato de empacotamento descrito aqui. Você só precisa adotar esse formato se precisar dos recursos que ele descreve e estiver disposto a trabalhar somente com clientes que foram atualizados para a versão 3 ou superior do cliente do NuGet.

## <a name="i-already-target-netcore45"></a>Já direcionado para netcore45

Se seu projeto já se destina ao `netcore45` e você não precisa aproveitar os recursos descritos aqui, nenhuma ação é necessária. Pacotes `netcore45` podem ser consumidos por aplicativos UWP.

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a>Desejo aproveitar as APIs específicas do Windows 10

Nesse caso, será necessário adicionar o moniker da estrutura de destino `uap10.0` (TFM ou TxM) ao seu pacote. Crie uma nova pasta no seu pacote e adicione o assembly que foi compilado para funcionar com o Windows 10 para essa pasta.

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a>Não preciso de APIs específicas do Windows 10, mas desejo novos recursos do .NET ou ainda não tenho o netcore45

Nesse caso, você adicionaria o `dotnet` TxM ao seu pacote. Ao contrário de outros TxMs, o `dotnet` não implica em uma plataforma ou área da superfície. É informado que seu pacote funciona em qualquer plataforma com as quais suas dependências funcionam. Ao criar um pacote com o `dotnet` TxM, é provável que você tenha muito mais dependências específicas de TxM em seu `.nuspec` , pois você precisa definir os pacotes de BCL dos quais depende, como, `System.Text` `System.Xml` etc. Os locais em que essas dependências funcionam definem onde o pacote funciona.

### <a name="how-do-i-find-out-my-dependencies"></a>Como fazer para localizar minhas dependências

Há duas maneiras de descobrir quais dependências listar:

1. Use a ferramenta [Gerador de dependência de NuSpec](https://github.com/onovotny/ReferenceGenerator) **de terceiros**. A ferramenta automatiza o processo e atualiza seu arquivo `.nuspec` com os pacotes dependentes no build. Está disponível por meio de um pacote do NuGet, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).

1. (A maneira mais difícil) Use `ILDasm` para examinar seu `.dll` para ver quais assemblies são realmente necessários no runtime. Em seguida, determine de qual pacote do NuGet cada um deles veio.

Consulte o [`project.json`](project-json.md) tópico para obter detalhes sobre os recursos que ajudam na criação de um pacote que dá suporte ao `dotnet` TxM.

> [!Important]
> Se seu pacote se destina a trabalhar com projetos PCL, é altamente recomendável criar uma pasta `dotnet` para evitar avisos e possíveis problemas de compatibilidade.

## <a name="directory-structure"></a>Estrutura do diretório

Pacotes do NuGet usando esse formato tem a seguinte pasta e comportamento bem conhecidos:

| Pasta | Comportamentos |
| --- | --- |
| Build | Contém os arquivos de objeto e destinos do MSBuild nesta pasta, que estão integrados de forma diferente no projeto, porém, exceto isso, não há nenhuma alteração. |
| Ferramentas | `install.ps1` e `uninstall.ps1` não são executados. O continua `init.ps1` funcionando como sempre. |
| Conteúdo | O conteúdo não é copiado automaticamente para o projeto de um usuário. Suporte para inclusão de conteúdo do projeto está planejado para uma versão posterior. |
| Lib | Para muitos pacotes de `lib` que funcionam da mesma forma que no NuGet 2.x, mas com opções expandidas para que nomes possam ser usados dentro delas e lógica aprimorada para escolher a subpasta correta ao consumir pacotes. No entanto, quando usado junto com `ref`, a pasta `lib` contém os assemblies que implementam a área da superfície definida pelos assemblies na pasta `ref`. |
| Ref | `ref` é uma pasta opcional que contém os assemblies .NET definindo a superfície pública (tipos e métodos públicos) para compilar um aplicativo. Os assemblies nesta pasta não podem ter nenhuma implementação e são puramente usados para definir a área de superfície para o compilador. Se o pacote não tiver nenhuma pasta `ref`, o `lib` será o assembly de referência e o assembly de implementação. |
| Runtimes | `runtimes` é uma pasta opcional que contém o código específico do sistema operacional, como a arquitetura de CPU e binários do sistema operacional específicos ou dependentes da plataforma. |

## <a name="msbuild-targets-and-props-files-in-packages"></a>Arquivos de destino e objetos do MSBuild em pacotes

Pacotes do NuGet podem conter arquivos `.targets` e `.props` que são importados para qualquer projeto do MSBuild em que o pacote é instalado. No NuGet 2.x, isso foi feito injetando instruções `<Import>` no arquivo `.csproj`, enquanto no NuGet 3.0 não há nenhuma ação de “instalação específica no projeto”. Em vez disso, o processo de restauração do pacote grava dois arquivos `[projectname].nuget.props` e `[projectname].NuGet.targets`.

O MSBuild sabe procurar esses dois arquivos e os importa automaticamente próximo ao início e no final do processo de build do projeto. Isso fornece um comportamento muito semelhante ao NuGet 2.x, mas com uma grande diferença: *não há nenhuma garantia da ordem dos arquivos de destinos/objetos neste caso*. No entanto, o MSBuild fornece maneiras de ordenar destinos por meio dos atributos `BeforeTargets` e `AfterTargets` da definição `<Target>` (consulte [Elemento de Destino (MSBuild)](/visualstudio/msbuild/target-element-msbuild).

## <a name="lib-and-ref"></a>Lib e Ref

O comportamento da pasta `lib` ainda não foi alterado significativamente no NuGet v3. No entanto, todos os assemblies devem estar dentro de subpastas nomeadas com um TxM e não pode ser colocados diretamente na pasta `lib`. Um TxM é o nome de uma plataforma para a qual determinado ativo em um pacote trabalha. Logicamente, isso é uma extensão do TFM (Moniker do Framework de Destino), por exemplo, `net45`, `net46`, `netcore50` e `dnxcore50` são exemplos de TxMs (consulte [Estrutura de destino](../reference/target-frameworks.md). O TxM pode se referir a uma estrutura (TFM), bem como outras áreas da superfície específicas da plataforma. Por exemplo, o TxM de UWP (`uap10.0`) representa a área de superfície do .NET, bem como a área de superfície do Windows para aplicativos UWP.

Um exemplo de estrutura de lib:

```
lib
├───net40
│       MyLibrary.dll
└───wp81
        MyLibrary.dll
```

A pasta `lib` contém os assemblies que são usados no runtime. Para a maioria dos pacotes, tudo o que é necessário é uma pasta em `lib` para cada destino TxMs.

## <a name="ref"></a>Ref

Às vezes, há casos em que um assembly diferente deve ser usado durante a compilação (Assemblies de referência do .NET fazem isso atualmente). Para esses casos, use uma pasta de nível superior chamada `ref` (abreviação de “Assemblies de Referência”).

A maioria dos autores de pacote não exigem a pasta `ref`. É útil para os pacotes que precisam fornecer uma área de superfície consistente para compilação e IntelliSense, mas têm uma implementação diferente para TxMs diferentes. O maior caso de uso são os pacotes `System.*` que estão sendo produzidos como parte do envio de .NET Core no NuGet. Estes pacotes têm várias implementações que estão sendo unificadas por um conjunto consistente de assemblies de referência.

Mecanicamente, os assemblies incluídos na pasta `ref` são os assemblies de referência que estão sendo passados para o compilador. Para aqueles dentre vocês que usaram csc.exe, esses são os assemblies que estamos passando para a opção [C# /reference option](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option).

A estrutura da pasta `ref` é o mesmo que `lib`, por exemplo:

```
└───MyImageProcessingLib
        ├───lib
        │   ├───net40
        │   │       MyImageProcessingLibrary.dll
        │   │
        │   ├───net451
        │   │       MyImageProcessingLibrary.dll
        │   │
        │   └───win81
        │           MyImageProcessingLibrary.dll
        │
        └───ref
            ├───net40
            │       MyImageProcessingLibrary.dll
            │
            └───portable-net451-win81
                    MyImageProcessingLibrary.dll
```

Neste exemplo, os assemblies nos diretórios `ref` serão idênticos.

## <a name="runtimes"></a>Runtimes

A pasta de runtimes contém os assemblies e bibliotecas nativos necessários para executar em “runtimes” específicos, que geralmente são definidos pelo sistema operacional e arquitetura de CPU. Esses tempos de execução são identificados usando [RIDs (identificadores de tempo de execução)](/dotnet/core/rid-catalog) , como `win` ,, `win-x86` `win7-x86` , `win8-64` etc.

## <a name="native-helpers-to-use-platform-specific-apis"></a>Auxiliares nativo para usar APIs específicas de plataforma

O exemplo a seguir mostra um pacote que tem uma implementação totalmente gerenciada para várias plataformas, mas usa auxiliares nativos no Windows 8, em que ele pode chamar APIs nativas específicas do Windows 8.

```
└───MyLibrary
        ├───lib
        │   └───net40
        │           MyLibrary.dll
        │
        └───runtimes
            ├───win8-x64
            │   ├───lib
            │   │   └───net40
            │   │           MyLibrary.dll
            │   │
            │   └───native
            │           MyNativeLibrary.dll
            │
            └───win8-x86
                ├───lib
                │   └───net40
                │           MyLibrary.dll
                │
                └───native
                        MyNativeLibrary.dll
```

Considerando o pacote acima, acontece o seguinte:

- Quando não está no Windows 8, o assembly `lib/net40/MyLibrary.dll` é usado.

- No Windows 8, o `runtimes/win8-<architecture>/lib/MyLibrary.dll` é usado e o `native/MyNativeHelper.dll` é copiado para a saída do build.

No exemplo acima, o assembly `lib/net40` é composto puramente por código gerenciado, embora os assemblies na pasta de runtimes serão p/invoke para o assembly auxiliar nativo para chamar as APIs específicas para o Windows 8.

Somente uma pasta `lib` única será escolhida, por isso se houver uma pasta específica do runtime, ela será escolhida em vez do `lib` específico fora do runtime. A pasta nativa é aditiva, se existir, ela é copiada para a saída do build.

## <a name="managed-wrapper"></a>Wrapper gerenciado

Outra maneira de usar os runtimes é fornecer um pacote que é essencialmente um wrapper gerenciado em um assembly nativo. Neste cenário, você cria um pacote como o seguinte:

```
└───MyLibrary
        └───runtimes
            ├───win8-x64
            │   ├───lib
            │   │   └───net451
            │   │           MyLibrary.dll
            │   │
            │   └───native
            │           MyImplementation.dll
            │
            └───win8-x86
                ├───lib
                │   └───net451
                │           MyLibrary.dll
                │
                └───native
                        MyImplementation.dll
```

Nesse caso não há pasta `lib` de nível superior, pois não há nenhuma implementação desse pacote que não conte com o assembly nativo correspondente. Se o assembly gerenciado, `MyLibrary.dll`, era exatamente o mesmo em ambos os casos, poderíamos colocá-lo em uma pasta `lib` de nível superior, mas como a falta de um assembly nativo não causa falha de instalação do pacote, se ele foi instalado em uma plataforma que não era win-x86 ou win-x64, a biblioteca de nível superior será usada, mas nenhum assembly nativo será copiado.

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a>Criação de pacotes do NuGet 2 e 3

Se você deseja criar um pacote que pode ser consumido por projetos usando o `packages.config`, bem como pacotes que usam o `project.json`, o seguinte se aplica:

- REF e runtimes só funcionam no NuGet 3. Eles são ambos ignorados pelo NuGet 2.

- Você não pode contar que `install.ps1` ou `uninstall.ps1` funcionem. Esses arquivos são executados ao usar `packages.config`, mas são ignorados com `project.json`. Assim, seu pacote precisa ser usado quando eles não estiverem em execução. `init.ps1` ainda é executado no NuGet 3.

- A instalação de Destinos e Objetos é diferente, por isso verifique se seu pacote funciona conforme o esperado em ambos os clientes.

- Os subdiretórios de lib devem ser um TxM do NuGet 3. Não é possível colocar as bibliotecas na raiz da pasta `lib`.

- O conteúdo não é copiado automaticamente com o NuGet 3. Os consumidores do seu pacote poderia copiar os próprios arquivos ou usar uma ferramenta como um executor de tarefas para automatizar a cópia dos arquivos.

- Transformações de arquivo de configuração e de origem não são executadas pelo NuGet 3.

Se você estiver dando suporte ao NuGet 2 e 3, seu `minClientVersion` deverá ter a versão mais antiga do cliente do NuGet 2 na qual seu pacote funciona. No caso de um pacote existente, ele não deve precisar ser alterado.
