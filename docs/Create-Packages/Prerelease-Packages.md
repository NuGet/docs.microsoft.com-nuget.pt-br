---
title: Versões pré-lançamento em pacotes do NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Diretrizes para compilar pacotes de pré-lançamento
keywords: controle de versão, controle de versão de pacote do NuGet, versões de pré-lançamento do NuGet, pacotes de pré-lançamento do NuGet, versões de versão prévia do pacote, versões RC do pacote, versões Beta do pacote, controle de versão semântico do NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 57f59e3906e2d49b6b6e078f530885a601553b06
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="building-pre-release-packages"></a>Compilando pacotes de pré-lançamento

Sempre que você liberar um pacote atualizado com um novo número de versão, o NuGet considerará esse como a “última versão estável” conforme mostrado, por exemplo, na interface do usuário do Gerenciador de Pacotes no Visual Studio:

![A interface do usuário do Gerenciador de Pacotes mostrando a versão estável mais recente](media/Prerelease_01-LatestStable.png)

Uma versão estável é aquela que é considerado confiável suficiente para ser usada na produção. A versão estável mais recente também é aquela que será instalada como uma atualização de pacote ou durante a restauração do pacote (sujeito a restrições, conforme descrito em [Reinstalando e atualizando pacotes](../consume-packages/reinstalling-and-updating-packages.md)).

Para dar suporte ao ciclo de vida de versão de software, o NuGet 1.6 e posterior permite a distribuição de pacotes de pré-lançamento, em que o número de versão inclui um sufixo de controle de versão semântico como `-alpha`, `-beta` ou `-rc`. Para obter mais informações, consulte [Controle de versão de pacote](../reference/package-versioning.md#pre-release-versions).

Você pode especificar essas versões de duas maneiras:

- Arquivo `.nuspec`: inclua o sufixo de versão semântico no elemento `version`:

    ```xml
    <version>1.0.1-alpha</version>
    ```

- Atributos de assembly: ao compilar um pacote de um projeto do Visual Studio (`.csproj` ou `.vbproj`), use o `AssemblyInformationalVersionAttribute` para especificar a versão:

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    O NuGet adota esse valor em vez daquele especificado no atributo `AssemblyVersion`, que não é compatível com o controle de versão semântico.

Quando você estiver pronto para lançar uma versão estável, basta remover o sufixo e o pacote terá precedência sobre as versões de pré-lançamento. Novamente, consulte [Controle de versão do pacote](../reference/package-versioning.md#pre-release-versions).

## <a name="installing-and-updating-pre-release-packages"></a>Instalando e atualizando pacotes de pré-lançamento

Por padrão, o NuGet não inclui as versões de pré-lançamento ao trabalhar com pacotes, mas você pode alterar esse comportamento da seguinte maneira:

- **Interface do usuário do Gerenciador de Pacotes no Visual Studio**: na interface do usuário **Gerenciar pacotes do NuGet**, marque a caixa **Incluir pré-lançamento**:

    ![A caixa de seleção Incluir pré-lançamento no Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    Definir ou desmarcar esta caixa atualizará a interface do usuário do Gerenciador de Pacotes e a lista de versões disponíveis que você pode instalar.

- **Console do Gerenciador de Pacotes**: use a opção `-IncludePrerelease` com os comandos `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package` e `Update-Package`. Consulte a [Referência do PowerShell](../tools/powershell-reference.md).

- **CLI do NuGet**: use a opção `-prerelease` com os comandos `install`, `update`, `delete` e `mirror`. Consulte a [referência da CLI do NuGet](../tools/nuget-exe-cli-reference.md)

## <a name="semantic-versioning"></a>Controle de versão semântico

O [Controle de versão semântico ou convenção de SemVer](http://semver.org/spec/v1.0.0.html) descreve como utilizar as cadeias de caracteres em números de versão para expressar o significado do código subjacente.

Nesta convenção, cada versão tem três partes, `Major.Minor.Patch`, com o seguinte significado:

- `Major`: alterações significativas
- `Minor`: novos recursos, mas compatível com versões anteriores
- `Patch`: somente correções de bug compatíveis com versões anteriores

As versões de pré-lançamento são indicadas acrescentando um hífen e uma cadeia de caracteres após o número de patch. Tecnicamente, você pode usar *qualquer* cadeia de caracteres após o hífen e o NuGet tratará o pacote como a versão de pré-lançamento. O NuGet exibe, então, o número de versão completa na interface do usuário aplicável, deixando os consumidores para interpretar o significado por si mesmos.

Considerando isso, geralmente é aconselhável seguir as convenções de nomenclatura reconhecidas como a seguinte:

- `-alpha`: versão alfa, normalmente usado para o trabalho e experimentação em andamento
- `-beta`: versão beta, normalmente uma completa com recursos para a próxima versão planejada, mas pode conter erros conhecidos.
- `-rc`: versão Release candidate, normalmente uma versão que é potencialmente a final (estável), a menos que surjam bugs significativos.

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
