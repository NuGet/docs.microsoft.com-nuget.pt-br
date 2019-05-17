---
title: Versões de pré-lançamento em pacotes do NuGet
description: Diretrizes para compilar pacotes de pré-lançamento
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 845f0ea84bcb92fedf9e5f4fb2b1deee1462a004
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610489"
---
# <a name="building-pre-release-packages"></a>Compilando pacotes de pré-lançamento

Sempre que você liberar um pacote atualizado com um novo número de versão, o NuGet considerará esse como a “última versão estável” conforme mostrado, por exemplo, na interface do usuário do Gerenciador de Pacotes no Visual Studio:

![A interface do usuário do Gerenciador de Pacotes mostrando a versão estável mais recente](media/Prerelease_01-LatestStable.png)

Uma versão estável é aquela que é considerado confiável suficiente para ser usada na produção. A versão estável mais recente também é aquela que será instalada como uma atualização de pacote ou durante a restauração do pacote (sujeito a restrições, conforme descrito em [Reinstalando e atualizando pacotes](../consume-packages/reinstalling-and-updating-packages.md)).

Para dar suporte ao ciclo de vida de versão de software, o NuGet 1.6 e posterior permite a distribuição de pacotes de pré-lançamento, em que o número de versão inclui um sufixo de controle de versão semântico como `-alpha`, `-beta` ou `-rc`. Para obter mais informações, consulte [Controle de versão de pacote](../reference/package-versioning.md#pre-release-versions).

Você pode especificar essas versões usando uma das seguintes maneiras:

- **Se seu projeto usa [`PackageReference`](../consume-packages/package-references-in-project-files.md)**: incluir o sufixo de versão semântica no elemento [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion) do arquivo `.csproj`:

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- **Se seu projeto usa um arquivo [`packages.config`](../reference/packages-config.md)**: incluir o sufixo de versão semântica no elemento [`version`](../reference/nuspec.md#version) do arquivo [`.nuspec`](../reference/nuspec.md):

    ```xml
    <version>1.0.1-alpha</version>
    ```

Quando você estiver pronto para lançar uma versão estável, basta remover o sufixo e o pacote terá precedência sobre as versões de pré-lançamento. Novamente, consulte [Controle de versão do pacote](../reference/package-versioning.md#pre-release-versions).

## <a name="installing-and-updating-pre-release-packages"></a>Instalando e atualizando pacotes de pré-lançamento

Por padrão, o NuGet não inclui as versões de pré-lançamento ao trabalhar com pacotes, mas você pode alterar esse comportamento da seguinte maneira:

- **Interface do Usuário do Gerenciador de Pacotes no Visual Studio**: na Interface do Usuário **Gerenciar pacotes NuGet**, marque a caixa de seleção **Incluir pré-lançamento**:

    ![A caixa de seleção Incluir pré-lançamento no Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    Definir ou desmarcar esta caixa atualizará a interface do usuário do Gerenciador de Pacotes e a lista de versões disponíveis que você pode instalar.

- **Console do Gerenciador de Pacotes**: Use a opção `-IncludePrerelease` com os comandos `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package` e `Update-Package`. Consulte a [Referência do PowerShell](../tools/powershell-reference.md).

- **CLI do NuGet**: Use a opção `-prerelease` com os comandos `install`, `update`, `delete` e `mirror`. Consulte a [referência da CLI do NuGet](../tools/nuget-exe-cli-reference.md)

## <a name="semantic-versioning"></a>Controle de versão semântico

O [Semantic Versioning or SemVer convention](http://semver.org/spec/v1.0.0.html) (Controle de versão semântico ou convenção de SemVer) descreve como utilizar as cadeias de caracteres em números de versão para expressar o significado do código subjacente.

Nesta convenção, cada versão tem três partes, `Major.Minor.Patch`, com o seguinte significado:

- `Major`: Alterações da falha
- `Minor`: Novos recursos, mas compatível com versões anteriores
- `Patch`: Somente correções de bug compatíveis com versões anteriores

As versões de pré-lançamento são indicadas acrescentando um hífen e uma cadeia de caracteres após o número de patch. Tecnicamente, é possível usar *qualquer* cadeia de caracteres após o hífen e o NuGet tratará o pacote como a versão de pré-lançamento. O NuGet exibe, então, o número de versão completa na interface do usuário aplicável, deixando os consumidores para interpretar o significado por si mesmos.

Considerando isso, geralmente é aconselhável seguir as convenções de nomenclatura reconhecidas como a seguinte:

- `-alpha`: Versão alfa, normalmente usada para o trabalho e experimentação em andamento
- `-beta`: Versão beta, normalmente uma completa com recursos para a próxima versão planejada, mas pode conter erros conhecidos.
- `-rc`: Versão Release Candidate, normalmente uma versão que é potencialmente a final (estável), a menos que surjam bugs significativos.

> [!Note]
> O NuGet 4.3.0+ é compatível com o [Semantic Versioning v2.0.0](http://semver.org/spec/v2.0.0.html), que oferece compatibilidade com números com notação de ponto pré-lançamento, como no `1.0.1-build.23`. A notação de ponto não e compatível com as versões do NuGet anteriores à 4.3.0. Em versões anteriores do NuGet, você poderia usar um formulário como `1.0.1-build23`, mas ela sempre foi considerada uma versão de pré-lançamento.

Qualquer sufixo que você usar, no entanto, receberá precedência do NuGet cem ordem alfabética inversa:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

Conforme mostrado, a versão sem nenhum sufixo sempre terá precedência sobre as versões de pré-lançamento. Observe também que, se você usar sufixos numéricos com marcas de pré-lançamento que podem usar números de dois dígitos (ou mais), use zeros à esquerda como beta01 e beta05 para garantir que eles sejam classificados corretamente quando os números aumentarem.
