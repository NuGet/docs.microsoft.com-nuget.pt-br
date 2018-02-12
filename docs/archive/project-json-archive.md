---
title: "Conteúdo do arquivo project.json do NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/17/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Diversos bits de conteúdo do project.json removidos de outras áreas da documentação do NuGet."
keywords: Arquivo project.json do NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 42a40c6c637839c13effc9e476ac5702a92cfd2a
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2018
---
# <a name="projectjson-archive"></a>Arquivo project.json

O formato de referência `project.json` foi introduzido com o NuGet 3.x e é usado para determinados tipos de projeto. Ele foi substituído com a introdução do formato PackageReference, no qual as dependências são listadas diretamente em um arquivo de projeto.

Consulte também:

- [Esquema do project.json](project-json.md)
- [Impacto do project.json em autores de pacote](project-json-impact.md)
- [project.json e UWP](project-json-and-uwp.md)

## <a name="projectjson-reference-format"></a>Formato de referência do project.json

*Originalmente em [Restauração do pacote](../what-is-nuget.md).*

Na lista de formatos de referência:

- [`project.json`](project-json.md): *(preterido)* Um arquivo JSON que mantém uma lista de dependências do projeto com um grafo geral do pacote em um arquivo associado, `project.lock.json`. Esse formato foi preterido em favor de PackageReference.

## <a name="nuget-restore-on-mono"></a>Restauração do nuget no Mono

*Originalmente em [Instalar as ferramentas de cliente do NuGet](../install-nuget-client-tools.md).*

Ferramenta com `project.json`.

## <a name="constraining-package-versions-with-restore"></a>Restrições de versões de pacote com restauração

*Originalmente em [Restauração do pacote](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*

- `project.json`: especifique um intervalo de versão diretamente com o número de versão da dependência. Por exemplo:

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a>Comandos da CLI do NuGet

- `nuget install` não funciona com `project.json`.
- `nuget restore`: com projetos usando o `project.json`, gera um arquivo `project.lock.json` e um arquivo `<project>.nuget.props`, se for necessário. (Os dois arquivos podem ser omitidos do controle do código-fonte.) O argumento `<projectPath>` pode apontar um arquivo `project.json` e tem o mesmo comportamento que apontar para um `packages.config` ou arquivo de projeto. Na ordem de prioridade das pastas de pacote, `%userprofile%\.nuget\packages` é pesquisado pela primeira vez ao usar `project.json`.
- `nuget update`: Em Mono, esse comando não funciona com projetos que usam `project.json`.

## <a name="dependency-resolution-with-packagereference"></a>Resolução de dependência com PackageReference

*Originalmente em [Resolução de dependência](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*

O comportamento de PackageReference se aplica também a `project.json`. A restauração do NuGet grava o grafo de dependência em um arquivo denominado `project.lock.json` juntamente com `project.json`.

## <a name="managing-dependency-assets"></a>Gerenciamento de ativos de dependência

*Originalmente em [Resolução de dependência](../consume-packages/dependency-resolution.md#managing-dependency-assets).*

Ao usar o formato `project.json`, é possível controlar de quais ativos as dependências fluem no projeto de nível superior. Para obter detalhes, veja [project.json](project-json.md).

## <a name="excluding-references"></a>Excluindo referências

*Originalmente em [Resolução de dependência](../consume-packages/dependency-resolution.md#excluding-references).*

- `project.json`: adicionar `"exclude" : "all"` à dependência para PackageC:

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="resolving-incompatible-package-errors"></a>Resolvendo erros de pacote incompatível

*Originalmente em [Resolução de dependência](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*

Um outro jeito de resolver erros:

- **Não recomendável**: como uma solução temporária enquanto você trabalha junto com o autor do pacote, projetos voltados para `netcore`, `netstandard` e `netcoreapp` pode indicar outras estruturas como compatíveis, permitindo assim que os pacotes sejam direcionados para essas outras estruturas a serem usadas. Consulte [Importações do project.json](project-json.md#imports) e [PackageTargetFallback do restore target do MSBuild](../reference/msbuild-targets.md#packagetargetfallback). Isso pode causar comportamentos inesperados, por isso, novamente, é melhor resolver as incompatibilidades de pacote trabalhando com o autor do pacote em uma atualização.

## <a name="target-frameworks"></a>Frameworks de destino

*Originalmente em [Estruturas de destino](../reference/target-frameworks.md).*

- [project.json](project-json.md): o nó `frameworks` especifica as versões da estrutura com as quais o projeto pode ser compilado.

## <a name="creating-a-package"></a>Criar um pacote

*Originalmente em [Criar um pacote](../create-packages/creating-a-package.md)*

### <a name="setting-a-package-type"></a>Definindo um tipo de pacote

Com o .NET Core 1.x, quando um pacote DotnetCliTool é instalado, o Visual Studio coloca o pacote no nó `project.json` `tools` em vez do nó `dependencies`.

Os tipos de pacote são definidos em `project.json`.

- `project.json`: indica o tipo de pacote em um propriedade json `packOptions.packageType`:

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a>Adicionar destinos e objetos ao MSBuild

*Originalmente em [Criar pacotes NuGet do .NET Standard com o Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*

Ao usar `project.json`, os destinos não são adicionados ao projeto, mas são disponibilizados por meio do `project.lock.json`.

### <a name="package-versioning"></a>Controle de versão do pacote

*Originalmente em [Restauração do pacote](../reference/package-versioning.md).*

Ao usar o formato `project.json`, o NuGet também dá suporte ao uso de uma notação de curinga, \*, para as partes principal, secundária, patch e de sufixo de pré-lançamento do número.

### <a name="nugetconfig-reference"></a>Referência do NuGet.Config

*Original na [Referência do NuGet.Config](../reference/nuget-config-file.md).*

`globalPackagesFolder` aplica-se somente a `project.json`.

### <a name="nuspec-file-reference"></a>Referência ao arquivo nuspec

*Originalmente em [Referência a nuspec](../reference/nuspec.md).*

O elemento `<contentFiles>` é usado em vez de `<files>` com `project.json`.

### <a name="package-manager-options-control"></a>Controle de opções do Gerenciador de Pacotes

*Originalmente em [Referência da interface do usuário do Gerenciador de Pacotes](../tools/package-manager-ui.md).*

Os projetos que usam o formato de referência `project.json` mostram apenas a opção **Mostrar janela de visualização**.

### <a name="visual-studio-templates"></a>Modelos do Visual Studio

*Originalmente em [Pacotes NuGet em modelos do Visual Studio](../visual-studio-extensibility/visual-studio-templates.md).*

Práticas recomendadas: os modelos não incluem um arquivo `project.json`, nem incluem referências ou conteúdo que seria adicionado quando os pacotes NuGet são instalados.