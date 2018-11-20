---
title: Visão geral e fluxo de trabalho do uso de pacotes do NuGet
description: Uma visão geral do processo de consumir pacotes do NuGet em um projeto, com links para outras partes específicas do processo.
author: karann-msft
ms.author: karann
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: 5f52b00e0c45882fb7a4bd1c1a80022192f3be6b
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580240"
---
# <a name="package-consumption-workflow"></a>Fluxo de trabalho de consumo do pacote

Entre o nuget.org e galerias de pacotes privadas que sua organização pode estabelecer, você pode encontrar dezenas de milhares de pacotes extremamente úteis para usar em seus aplicativos e serviços. Porém, independentemente da origem, consumir um pacote segue o mesmo fluxo de trabalho geral.

![Fluxo de ir para uma origem de pacote, localizar um pacote, instalá-lo em um projeto, adicioná-lo usando uma instrução e chamá-lo para a API de pacote](media/Overview-01-GeneralFlow.png)

\* _Somente Visual Studio e `dotnet.exe`. O comando `nuget install` não modifica arquivos de projeto ou o arquivo `packages.config`; as entradas precisam ser gerenciadas manualmente._

Para obter mais detalhes, veja [Localizar e escolher pacotes](../consume-packages/finding-and-choosing-packages.md) e [Maneiras diferentes de instalar um pacote do NuGet](ways-to-install-a-package.md).

O NuGet lembra da identidade e do número de versão de cada pacote instalado, gravando-os em [`packages.config`](../reference/packages-config.md) ou no arquivo de projeto (usando [PackageReference](../consume-packages/package-references-in-project-files.md)), dependendo do tipo de projeto e da sua versão do NuGet. Com o NuGet 4.0 +, é preferível usar PackageReference, embora ele seja configurável no Visual Studio por meio das [opções de interface do usuário do Gerenciador de Pacotes](../tools/package-manager-ui.md). Em qualquer caso, você pode examinar o arquivo apropriado a qualquer momento para ver a lista completa das dependências para o seu projeto.

> [!Tip]
> É prudente sempre verificar a licença para cada pacote que você pretende usar no software. Em nuget.org, você encontra um link **Informações de licença** do lado direito da página de descrição de cada pacote. Se um pacote não especificar os termos de licença, entre em contato com o proprietário do pacote diretamente usando o link **Contatar os proprietários** na página do pacote. A Microsoft não licencia nenhuma propriedade intelectual para você de provedores de pacotes de terceiros, nem é responsável pelas informações fornecidas por terceiros.

Ao instalar pacotes, o NuGet normalmente verifica se o pacote já está disponível em seu cache. É possível limpar manualmente esse cache da linha de comando, conforme descrito em [Como gerenciar as pastas de pacotes globais e de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).

O NuGet também garante que as estruturas de destino com suporte no pacote sejam compatíveis com o seu projeto. Se o pacote não contiver assemblies compatíveis, o NuGet exibirá um erro. Consulte [Resolvendo erros de pacote incompatível](dependency-resolution.md#resolving-incompatible-package-errors).

Ao adicionar o código do projeto a um repositório de origem, pacotes do NuGet geralmente não são incluídos. Mais tarde, aqueles que clonarem o repositório ou adquirirem o projeto de outra forma, incluindo os agentes de build em sistemas como o Visual Studio Team Services, precisarão restaurar os pacotes necessários antes de executar um build:

![Fluxo de restauração de pacotes do NuGet clonando um repositório e usando um comando de restauração](media/Overview-02-RestoreFlow.png)

[Restauração de pacote](../consume-packages/package-restore.md) usa as informações no arquivo de projeto ou `packages.config` para reinstalar todas as dependências. Observe que há diferenças no processo envolvido, conforme descrito em [Resolução de dependências](../consume-packages/dependency-resolution.md). Além disso, o diagrama acima não mostra um comando de restauração para o Console do Gerenciador de Pacotes porque você está no Console e já está no contexto do Visual Studio, o que normalmente restaura pacotes de modo automático e fornece o comando solution-level, conforme mostrado.

Ocasionalmente, é necessário reinstalar pacotes que já estão incluídos em um projeto, o que também pode reinstalar as dependências. É fácil fazer isso usando o comando `nuget reinstall` ou o Console do Gerenciador de Pacotes do NuGet. Para obter detalhes, consulte [Reinstalando e atualizando pacotes](../consume-packages/reinstalling-and-updating-packages.md).

Por fim, o comportamento do NuGet é orientado por arquivos `Nuget.Config`. Vários arquivos podem ser usados para centralizar determinadas configurações em níveis diferentes, conforme explicado em [Configurando o comportamento do NuGet](../consume-packages/configuring-nuget-behavior.md).

Aproveite sua programação produtiva com pacotes do NuGet.
