---
title: Visão geral e fluxo de trabalho do uso de pacotes do NuGet
description: Uma visão geral do processo de consumir pacotes do NuGet em um projeto, com links para outras partes específicas do processo.
author: karann-msft
ms.author: karann
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: 4cfc2fde08b240288851b87a391dc42c1ac8ecaf
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842313"
---
# <a name="package-consumption-workflow"></a>Fluxo de trabalho de consumo do pacote

Entre o nuget.org e galerias de pacotes privadas que sua organização pode estabelecer, você pode encontrar dezenas de milhares de pacotes extremamente úteis para usar em seus aplicativos e serviços. Porém, independentemente da origem, consumir um pacote segue o mesmo fluxo de trabalho geral.

![Fluxo de ir para uma origem de pacote, localizar um pacote, instalá-lo em um projeto, adicioná-lo usando uma instrução e chamá-lo para a API de pacote](media/Overview-01-GeneralFlow.png)

\* _Somente Visual Studio e `dotnet.exe`. O comando `nuget install` não modifica arquivos de projeto ou o arquivo `packages.config`; as entradas precisam ser gerenciadas manualmente._

Para obter mais detalhes, confira [Como localizar e escolher pacotes](../consume-packages/finding-and-choosing-packages.md) e [O que acontece quando um pacote é instalado?](../concepts/package-installation-process.md).

O NuGet lembra da identidade e do número de versão de cada pacote instalado, gravando-os no arquivo de projeto (usando [PackageReference](../consume-packages/package-references-in-project-files.md)) ou [`packages.config`](../reference/packages-config.md), dependendo do tipo de projeto e da sua versão do NuGet. Com o NuGet 4.0 e posterior, é preferível usar PackageReference, embora isso seja configurável no Visual Studio por meio da [interface do usuário do Gerenciador de Pacotes](../tools/package-manager-ui.md). Em qualquer caso, você pode examinar o arquivo apropriado a qualquer momento para ver a lista completa das dependências para o seu projeto.

> [!Tip]
> É prudente sempre verificar a licença para cada pacote que você pretende usar no software. Em nuget.org, você encontra um link **Informações de licença** do lado direito da página de descrição de cada pacote. Se um pacote não especificar os termos de licença, entre em contato com o proprietário do pacote diretamente usando o link **Contatar os proprietários** na página do pacote. A Microsoft não licencia nenhuma propriedade intelectual para você de provedores de pacotes de terceiros, nem é responsável pelas informações fornecidas por terceiros.

Ao instalar pacotes, o NuGet normalmente verifica se o pacote já está disponível em seu cache. É possível limpar manualmente esse cache da linha de comando, conforme descrito em [Como gerenciar as pastas de pacotes globais e de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).

O NuGet também garante que as estruturas de destino com suporte no pacote sejam compatíveis com o seu projeto. Se o pacote não contiver assemblies compatíveis, o NuGet exibirá um erro. Consulte [Resolvendo erros de pacote incompatível](dependency-resolution.md#resolving-incompatible-package-errors).

Ao adicionar o código do projeto a um repositório de origem, pacotes do NuGet geralmente não são incluídos. Mais tarde, aqueles que clonarem o repositório ou adquirirem o projeto de outra forma, incluindo os agentes de build em sistemas como o Visual Studio Team Services, precisarão restaurar os pacotes necessários antes de executar um build:

![Fluxo de restauração de pacotes do NuGet clonando um repositório e usando um comando de restauração](media/Overview-02-RestoreFlow.png)

[Restauração de pacote](../consume-packages/package-restore.md) usa as informações no arquivo de projeto ou `packages.config` para reinstalar todas as dependências. Observe que há diferenças no processo envolvido, conforme descrito em [Resolução de dependências](../consume-packages/dependency-resolution.md). Além disso, o diagrama acima não mostra um comando de restauração para o Console do Gerenciador de Pacotes porque estar no Console significa também já estar no contexto do Visual Studio, o que normalmente restaura pacotes de modo automático e fornece o comando no nível da solução, conforme mostrado.

Ocasionalmente, é necessário reinstalar pacotes que já estão incluídos em um projeto, o que também pode reinstalar as dependências. É fácil fazer isso usando o comando `nuget reinstall` ou o Console do Gerenciador de Pacotes do NuGet. Para obter detalhes, consulte [Reinstalando e atualizando pacotes](../consume-packages/reinstalling-and-updating-packages.md).

Por fim, o comportamento do NuGet é orientado por arquivos `Nuget.Config`. Vários arquivos podem ser usados para centralizar determinadas configurações em níveis diferentes, conforme explicado em [Configurando o comportamento do NuGet](../consume-packages/configuring-nuget-behavior.md).

## <a name="ways-to-install-a-nuget-package"></a>Maneiras de instalar um pacote NuGet

Os pacotes NuGet são baixados e instalados por meio de um dos métodos descritos na tabela a seguir.

| Ferramenta | DESCRIÇÃO |
| --- | --- |
| [CLI do dotnet.exe](install-use-packages-dotnet-cli.md) | (Todas as plataformas) Ferramenta CLI para bibliotecas .NET Core e .NET Standard e projetos no estilo SDK direcionados ao .NET Framework (confira o [Atributo SDK](/dotnet/core/tools/csproj#additions)). Recupera o pacote identificado por \<package_name\> e adiciona uma referência ao arquivo de projeto. Além disso, recupera e instala as dependências. |
| Visual Studio | (Windows e Mac) Fornece uma interface do usuário por meio da qual você pode procurar, selecionar e instalar pacotes e suas dependências em um projeto a partir de uma fonte do pacote especificado. Adicione referências a pacotes instalados ao arquivo de projeto.<ul><li>[Instalar e gerenciar pacotes usando o Visual Studio](../tools/package-manager-ui.md)</li><li>[Incluir um pacote NuGet ao seu projeto (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| [Console do Gerenciador de Pacotes no Visual Studio](../tools/package-manager-console.md) | (Somente Windows) Recupera e instala o pacote identificado por \<package_name\> de uma fonte selecionada em um projeto especificado na solução, depois adiciona uma referência ao arquivo de projeto. Além disso, recupera e instala as dependências. |
| [CLI do nuget.exe](install-use-packages-dotnet-cli.md) | (Todas as plataformas) Ferramenta CLI para bibliotecas .NET Framework e projetos no estilo não SDK direcionados a bibliotecas .NET Standard. Recupera o pacote identificado por \<package_name\> e expande seu conteúdo em uma pasta no diretório atual; também pode recuperar todos os pacotes listados em um arquivo `packages.config`. Também recupera e instala dependências, mas não altera arquivos de projeto ou `packages.config`. |
