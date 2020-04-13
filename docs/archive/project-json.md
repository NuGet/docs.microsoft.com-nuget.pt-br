---
title: Referência do arquivo project.json para NuGet
description: Em alguns tipos de projeto, o project.json mantém a lista de pacotes do NuGet usados no projeto.
author: karann-msft
ms.author: karann
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: 5ecbcd4855de8ea7b6301a5e307779216baf96fc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488290"
---
# <a name="projectjson-reference"></a>Referência do project.json

*NuGet 3.x+*

O arquivo `project.json` mantém uma lista de pacotes usados em um projeto, conhecidos como um formato de gerenciamento de pacote. Ele substitui `packages.config`, mas é, por sua vez substituído por [PackageReference](../consume-packages/package-references-in-project-files.md) com o NuGet 4.0 e superior.

O [`project.lock.json`](#projectlockjson) arquivo (descrito abaixo) também é `project.json`usado em projetos de empregabilidade .

`project.json` tem a seguinte estrutura básica, em que cada um dos quatro objetos de nível superior pode ter qualquer número de objetos filho:

```json
{
    "dependencies": {
        "PackageID" : "{version_constraint}"
    },
    "frameworks" : {
        "TxM" : {}
    },
    "runtimes" : {
        "RID": {}
    },
    "supports" : {
        "CompatibilityProfile" : {}
    }
}
```

## <a name="dependencies"></a>Dependências

Lista as dependências de pacote do NuGet do seu projeto no seguinte formato:

```json
"PackageID" : "version_constraint"
```

Por exemplo:

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

É na seção `dependencies` que a caixa de diálogo do Gerenciador de Pacotes do NuGet adiciona as dependências de pacote ao seu projeto.

A id do pacote corresponde à id do pacote no nuget.org, que é a mesma usada no console do gerenciador de pacotes: `Install-Package Microsoft.NETCore`.

Ao restaurar pacotes, a restrição de versão do `"5.0.0"` implica em `>= 5.0.0`. Ou seja, se 5.0.0 não estiver disponível no servidor, mas o 5.0.1 sim, o NuGet instala o 5.0.1 e avisa sobre o upgrade. Caso contrário, o NuGet escolhe a versão mais antiga possível no servidor correspondente à restrição.

Consulte [Resolução de dependência](../concepts/dependency-resolution.md) para obter mais detalhes sobre as regras de resolução.

### <a name="managing-dependency-assets"></a>Gerenciamento de ativos de dependência

Quais ativos do fluxo de dependências para o projeto de nível superior é controlado pela especificação de um conjunto de marcas delimitado por vírgulas nas propriedades `include` e `exclude` da referência de dependência. As marcas são listadas na tabela abaixo:

| Marca Incluir/Excluir | Pastas afetadas do destino |
| --- | --- |
| contentFiles | Conteúdo  |
| runtime | Runtime, Resources e FrameworkAssemblies  |
| compilar | lib |
| compilar | build (objetos e destinos do MSBuild) |
| nativa | nativa |
| none | Nenhuma pasta |
| all | Todas as pastas |

Marcas especificadas com `exclude` têm precedência sobre aquelas especificadas com `include`. Por exemplo, `include="runtime, compile" exclude="compile"` é o mesmo que `include="runtime"`.

Por exemplo, para incluir as pastas `build` e `native` de uma dependência, use o seguinte:

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "include": "build, native"
    }
  }
}
```

Para excluir as pastas `content` e `build` de uma dependência, use o seguinte:

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "exclude": "contentFiles, build"
    }
  }
}
```

## <a name="frameworks"></a>Estruturas

Lista as estruturas em que o projeto é executado, como `net45`, `netcoreapp`, `netstandard`.

```json
"frameworks": {
    "netcore50": {}
    }
 ```

Somente uma única entrada é permitida na seção `frameworks`. (Uma exceção são os arquivos `project.json` para projetos do ASP.NET compilados com a cadeia de ferramentas DNX preterida, o que permite considerar vários destinos).

## <a name="runtimes"></a>Runtimes

Lista os sistemas operacionais e arquiteturas nos quais seu aplicativo é executado, como `win10-arm`, `win8-x64`, `win8-x86`.

```json
"runtimes": {
    "win10-arm": { },
    "win10-arm-aot": { },
    "win10-x86": { },
    "win10-x86-aot": { },
    "win10-x64": { },
    "win10-x64-aot": { }
}
```

Um pacote que contém um PCL que pode ser executado em qualquer runtime não precisa especificar um runtime. Isso também deve ser verdadeiro para todas as dependências, caso contrário, você precisará especificar runtimes.


## <a name="supports"></a>Suporta

Define um conjunto de verificações para as dependências de pacote. Você pode definir onde você espera que o PCL ou aplicativo seja executado. As definições não são restritivas, visto que seu código pode ser capaz de ser executado em outro lugar. Porém, especificar essas verificações faz o NuGet verificar se todas as dependências são atendidas nos TxMs listados. Exemplos de valores para isso problema são: `net46.app`, `uwp.10.0.app`, etc.

Esta seção deve ser populada automaticamente quando você seleciona uma entrada na caixa de diálogo de destinos da Biblioteca de Classes Portátil.

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a>Importações

Importações foram desenvolvidas para permitir que os pacotes que usam o `dotnet` TxM operem com pacotes que não declaram um dotnet TxM. Se seu projeto usa o `dotnet` TxM, todos os pacotes dos quais você depende também precisam ter um `project.json` TxM, a menos que você adicione o seguinte ao seu `dotnet` para permitir que plataformas não `dotnet` sejam compatíveis com o `dotnet`:

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

Se você estiver usando o `dotnet` TxM, o sistema do projeto PCL adiciona a instrução `imports` apropriada com base nos destinos compatíveis.

## <a name="differences-from-portable-apps-and-web-projects"></a>Diferenças entre aplicativos portáteis e projetos Web

O arquivo `project.json` usado pelo NuGet é um subconjunto do que é encontrado em projetos do ASP.NET Core. No ASP.NET Core, o `project.json` é usado para metadados do projeto, informações de compilação e dependências. Quando usado em outros sistemas de projeto, essas três coisas são divididas em arquivos separados e o `project.json` contém menos informações. As diferenças notáveis incluem:

- Pode haver somente uma estrutura na seção `frameworks`.

- O arquivo não pode conter dependências, opções de compilação, etc. que são vistos nos arquivos `project.json` de DNX. Considerando que pode haver apenas uma única estrutura, não faz sentido inserir dependências específicas de estrutura.

- A compilação é tratada pelo MSBuild, por isso as opções de compilação, definições do pré-processador, etc. fazem parte do arquivo de projeto do MSBuild e não de `project.json`.

No NuGet 3 ou superior, não é esperado que os desenvolvedores editem o `project.json` manualmente, visto que a interface do usuário do Gerenciador de Pacotes no Visual Studio manipula o conteúdo. Dito isso, você certamente pode editar o arquivo, mas será preciso compilar o projeto para iniciar uma restauração de pacote ou invocar a restauração de outra maneira. Consulte [Restauração de pacote](../consume-packages/package-restore.md).


## <a name="projectlockjson"></a>project.lock.json

O arquivo `project.lock.json` é gerado no processo de restauração de pacotes do NuGet em projetos que usam `project.json`. Ele contém um instantâneo de todas as informações geradas à medida que o NuGet percorre o grafo de pacotes e inclui a versão, conteúdo e as dependências de todos os pacotes em seu projeto. O sistema de build usa isso para escolher os pacotes de um local global que são relevantes ao compilar o projeto em vez de depender de uma pasta de pacotes local no projeto em si. Isso resulta em desempenho mais rápido de build porque é necessário ler somente `project.lock.json` em vez de muitos arquivos `.nuspec` separados.

`project.lock.json` é gerado automaticamente na restauração do pacote, por isso ele pode ser omitido do controle do código-fonte adicionando-o aos arquivos `.gitignore` e `.tfignore` (consulte [Pacotes e controle do código-fonte](../consume-packages/packages-and-source-control.md). No entanto, se você incluí-lo no controle do código-fonte, o histórico de alterações mostrará as alterações em dependências resolvidas ao longo do tempo.
