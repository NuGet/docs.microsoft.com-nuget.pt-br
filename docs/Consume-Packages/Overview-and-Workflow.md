---
title: "Visão geral e o fluxo de trabalho do uso de pacotes do NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3c60f920-457d-4f43-9efe-210c514e5242
description: "Uma visão geral do processo de consumir pacotes do NuGet em um projeto, com links para outras partes específicas do processo."
keywords: "Consumo de pacote do NuGet, visão geral de consumo do NuGet, fluxo de trabalho de consumo do NuGet, fluxo de trabalho de consumo do pacote, visão geral de consumo do pacote"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c48351cb6fed0ac94bd437d9443811f46c032bd0
ms.sourcegitcommit: 122bf7ce308365ea45da018b0768f0536de76a1f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="package-consumption-workflow"></a>Fluxo de trabalho de consumo do pacote

Entre o nuget.org e galerias de pacotes privadas que sua organização pode estabelecer, você pode encontrar dezenas de milhares de pacotes extremamente úteis para usar em seus aplicativos e serviços. Porém, independentemente da origem, consumir um pacote segue o mesmo fluxo de trabalho geral mostrado abaixo. Para obter detalhes, consulte [Localizando e escolhendo pacotes](../consume-packages/finding-and-choosing-packages.md) e [Usar um início rápido de pacote](../quickstart/use-a-package.md).

![Fluxo de ir para uma origem de pacote, localizar um pacote, instalá-lo em um projeto, adicioná-lo usando uma instrução e chamá-lo para a API de pacote](media/Overview-01-GeneralFlow.png)

\* _Exceto com `nuget install` na linha de comando, quando então é necessário editar os arquivos de configuração manualmente. Consulte a [referência do comando install](../tools/cli-ref-install.md)._

O NuGet lembra da identidade e do número de versão de cada pacote instalado, gravando-o em `packages.config`, no arquivo de projeto ou em um `project.json` arquivo na raiz de seu projeto, dependendo do tipo de projeto e da sua versão do NuGet. Com o NuGet 4.0 ou superior, [armazenar dependências no arquivo de projeto](../consume-packages/package-references-in-project-files.md) é o padrão (exceto para projetos UWP voltados para o Windows 10 RS1). Em qualquer caso, você pode examinar o arquivo apropriado a qualquer momento para ver a lista completa das dependências para o seu projeto.

> [!Tip]
> É prudente sempre verificar a licença para cada pacote que você pretende usar no software. Em nuget.org, você encontrará um link **Informações de licença** do lado direito da página de descrição de cada pacote. Se um pacote não especificar os termos de licença, entre em contato com o proprietário do pacote diretamente usando o link **Contatar os proprietários** na página do pacote. A Microsoft não licencia nenhuma propriedade intelectual para você de provedores de pacotes de terceiros, nem é responsável pelas informações fornecidas por terceiros.

Ao instalar pacotes, o NuGet normalmente verifica se o pacote já está disponível em seu cache. Você pode limpar manualmente esse cache da linha de comando, conforme descrito em [Gerenciamento do cache do NuGet](../consume-packages/managing-the-nuget-cache.md).

O NuGet também garante que as estruturas de destino com suporte no pacote sejam compatíveis com o seu projeto. Se o pacote não contém assemblies compatíveis, o NuGet mostrará uma mensagem de erro. Consulte [Resolvendo erros de pacote incompatível](dependency-resolution.md#resolving-incompatible-package-errors).

Ao adicionar o código do projeto a um repositório de origem, pacotes do NuGet geralmente não são incluídos. Mais tarde, aqueles que clonarem o repositório, incluindo os agentes de build em sistemas como o Visual Studio Team Services, precisarão restaurar os pacotes necessários antes de executar um build:

![Fluxo de restauração de pacotes do NuGet clonando um repositório e usando um comando de restauração](media/Overview-02-RestoreFlow.png)

[Restauração de pacote](../consume-packages/package-restore.md) usa as informações no arquivo de projeto, `packages.config`, `project.json` reinstalar todas as dependências. Observe que há diferenças no processo envolvido, conforme descrito em [Resolução de dependências](../consume-packages/dependency-resolution.md).

Ocasionalmente, é necessário reinstalar pacotes que já estão incluídos em um projeto, o que também pode reinstalar as dependências. É fácil fazer isso usando o comando `reinstall` com a linha de comando do NuGet ou o Console do Gerenciador de Pacotes do NuGet. Para obter detalhes, consulte [Reinstalando e atualizando pacotes](../consume-packages/reinstalling-and-updating-packages.md).

Por fim, o comportamento do NuGet é orientado por arquivos de configuração `Nuget.Config`. Vários arquivos podem ser usados para centralizar determinadas configurações em níveis diferentes, conforme explicado em [Configurando o comportamento do NuGet](../consume-packages/configuring-nuget-behavior.md).

Aproveite sua programação produtiva com pacotes do NuGet.
