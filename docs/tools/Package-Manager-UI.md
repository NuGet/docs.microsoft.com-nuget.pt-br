---
title: Referência de interface do usuário do Gerenciador de pacotes do NuGet
description: Instruções sobre como usar a UI do Gerenciador de pacotes NuGet no Visual Studio para trabalhar com pacotes do NuGet.
author: karann-msft
ms.author: karann
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 1de6ddeca6295c621a90409807af198bc3c7a068
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981178"
---
# <a name="nuget-package-manager-ui"></a>Interface do usuário de Gerenciador de pacotes do NuGet

UI do Gerenciador de pacotes NuGet no Visual Studio no Windows permite que você instalar, desinstalar e atualizar pacotes do NuGet em projetos e soluções com facilidade. Para obter a experiência no Visual Studio para Mac, consulte [incluindo um pacote do NuGet em seu projeto](/visualstudio/mac/nuget-walkthrough). A UI do Gerenciador de pacotes não está incluída no Visual Studio Code.

Neste tópico:

- [Localizando e instalando um pacote (guia Browse)](#finding-and-installing-a-package)
- [Desinstalar um pacote (aba instalado)](#uninstalling-a-package)
- [Atualizar um pacote (guias instalado e atualizações)](#updating-a-package) (inclui o ["Mencionada implicitamente por um SDK" ou "AutoReferenced" mensagem](#implicit_reference))
- [Gerenciamento de pacotes para a solução](#managing-packages-for-the-solution) (trabalhando com vários projetos ao mesmo tempo).
- [Origens de pacote](#package-sources)
- [Controle de opções do Gerenciador de pacote](#package-manager-options-control)

> [!Note]
> Verifique se você está ignorando o Gerenciador de pacotes do NuGet no Visual Studio 2015, **Ferramentas > extensões e atualizações...**  e procure o *NuGet Package Manager* extensão. Se você não puder usar o instalador de extensões no Visual Studio, baixe a extensão diretamente [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).
>
> No Visual Studio 2017, NuGet e o Gerenciador de pacotes do NuGet são instalados automaticamente com qualquer um. Cargas de trabalho relacionados à rede. Instalá-lo individualmente selecionando o **componentes individuais > Ferramentas de código > Gerenciador de pacotes NuGet** opção no instalador do Visual Studio 2017.

## <a name="finding-and-installing-a-package"></a>Localizando e instalando um pacote

1. No **Gerenciador de soluções**, clique com botão direito seja **referências** ou um projeto e selecione **gerenciar pacotes NuGet...** .

    ![Gerenciar a opção de menu de pacotes do NuGet](media/ManagePackagesUICommand.png)

1. O **navegue** guia exibe os pacotes por popularidade da fonte selecionada no momento (consulte [origens de pacotes](#package-sources)). Pesquisar um pacote específico usando a caixa de pesquisa no canto superior esquerdo. Selecione um pacote na lista para exibir suas informações, que também permite que o **instalar** botão juntamente com uma lista suspensa de seleção de versão.

    ![Gerenciar guia Procurar de caixa de diálogo de pacotes do NuGet](media/Search.png)

1. Selecione a versão desejada na lista suspensa e selecione **instalar**. Visual Studio instala o pacote e suas dependências no projeto. Você pode ser solicitado a aceitar os termos de licença. Quando a instalação for concluída, os pacotes adicionados aparecem na **instalado** guia. Pacotes também são listados na **referências** nó do Gerenciador de soluções, indicando que você possa consultá-los no projeto com `using` instruções.

    ![Referências no Gerenciador de soluções](media/References.png)

> [!Tip]
> Para incluir versões de pré-lançamento na pesquisa e fazer versões de pré-lançamento disponível na versão de lista suspensa, selecione o **incluir pré-lançamento** opção.

## <a name="uninstalling-a-package"></a>Desinstalar um pacote

1. No **Gerenciador de soluções**, clique com botão direito seja **referências** ou o projeto desejado e selecione **gerenciar pacotes NuGet...** .
1. Selecione o **instalado** guia.
1. Selecione o pacote para desinstalar (usando a pesquisa para filtrar a lista se necessário) e selecione **desinstalação**.

    ![Desinstalar um pacote](media/UninstallPackage.png)

1. Observe que o **incluir pré-lançamento** e **origem do pacote** controles não têm nenhum efeito ao desinstalar pacotes.

## <a name="updating-a-package"></a>Atualizar um pacote

1. No **Gerenciador de soluções**, clique com botão direito seja **referências** ou o projeto desejado e selecione **gerenciar pacotes NuGet...** . (Em projetos de site da web, clique com botão direito do **Bin** pasta.)
1. Selecione o **atualizações** guia para ver os pacotes com atualizações disponíveis das fontes de pacote selecionado. Selecione **incluir pré-lançamento** inclui pacotes pré-lançados na lista de atualização.
1. Selecione o pacote para atualizar, selecione a versão desejada na lista suspensa à direita e selecione **atualizar**.

    ![Atualizar um pacote](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>Para alguns pacotes, o **atualização** botão será desabilitado e será exibida uma mensagem dizendo que ele é "implicitamente referenciado por um SDK" (ou "AutoReferenced"). Esta mensagem indica que o pacote faz parte de uma estrutura ou o SDK maior e não deve ser atualizado de forma independente. (Internamente, esses pacotes são marcados com `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Por exemplo, `Microsoft.NETCore.App` faz parte do SDK do .NET Core e a versão do pacote não é igual à versão do framework de tempo de execução usado pelo aplicativo. Você precisará [atualizar sua instalação do .NET Core](https://aka.ms/dotnet-download) para obter novas versões do tempo de execução do ASP.NET Core e .NET Core. [Consulte este documento para obter mais detalhes sobre metapacotes .NET Core e o controle de versão](/dotnet/core/packages). Isso se aplica aos seguintes pacotes comumente usados:
    * Microsoft.AspNetCore.All
    * Microsoft
    * Microsoft.NETCore.App
    * NETStandard.Library

    ![Pacote de exemplo são marcados como implicitamente referências ou AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. Para atualizar vários pacotes para suas versões mais recentes, selecione-os na lista e selecione o **atualizar** botão acima da lista.
1. Você também pode atualizar um pacote individual do **instalado** guia. Nesse caso, os detalhes do pacote incluem um seletor de versão (sujeito a **incluir pré-lançamento** opção) e um **atualização** botão.

## <a name="managing-packages-for-the-solution"></a>Gerenciamento de pacotes para a solução

Gerenciamento de pacotes para uma solução é uma maneira conveniente para trabalhar com vários projetos simultaneamente.

1. Selecione o **Ferramentas > Gerenciador de pacotes NuGet > Gerenciar pacotes NuGet para solução...**  menu de comando, ou a solução com o botão direito e selecione **gerenciar pacotes NuGet...** :

    ![Gerenciar pacotes NuGet para a solução](media/ManagePackagesSolutionUICommand.png)

1. Ao gerenciar pacotes para a solução, a interface do usuário permite que você selecione os projetos que são afetados pelas operações:

    ![Seletor de projeto durante o gerenciamento de pacotes para a solução](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>Guia de consolidação

Os desenvolvedores normalmente consideram a ele prática inadequada para usar versões diferentes do mesmo pacote do NuGet em projetos diferentes na mesma solução. Quando você escolhe gerenciar os pacotes para uma solução, a UI do Gerenciador de pacotes fornece um **consolidar** guia na qual você pode ver facilmente onde os pacotes com números de versão diferentes são usados por diferentes projetos na solução:

![Guia de consolidar de interface do usuário do Gerenciador de pacotes](media/ConsolidateTab.png)

Neste exemplo, o projeto ClassLibrary1 está usando o EntityFramework 6.2.0, enquanto ConsoleApp1 é usando o EntityFramework 6.1.0. Para consolidar as versões do pacote, faça o seguinte:

- Selecione os projetos para atualizar na lista de projetos.
- Selecione a versão a ser usada em todos os projetos na **versão** controle, como o EntityFramework 6.2.0.
- Selecione o **instalar** botão.

O Gerenciador de pacotes instala a versão do pacote selecionado em todos os projetos selecionados, após o qual o pacote não aparece mais na **consolidar** guia.

## <a name="package-sources"></a>Origens de pacote

Para alterar a origem do qual o Visual Studio obtém pacotes, selecione uma opção do seletor de origem:

![Seletor de origem do pacote no Gerenciador de pacotes da interface do usuário](media/PackageSourceDropDown.png)

Para gerenciar fontes de pacote:

1. Selecione o **as configurações** ícone da UI do Gerenciador de pacotes descritas abaixo ou usar o **Ferramentas > Opções** de comando e role até **Gerenciador de pacotes NuGet**:

    ![Ícone de configurações de interface do usuário de Gerenciador de pacote](media/PackageSourceSettings.png)

1. Selecione o **origens do pacote** nó:

    ![Opções de fontes de pacote](media/options.png)

1. Para adicionar uma fonte, selecione **+**, edite o nome, insira a URL ou caminho na **fonte** controle e selecione **atualização**. O código-fonte agora aparece no menu suspenso do seletor.
1. Para alterar uma origem de pacote, selecione-o, fazer edições na **nome** e **fonte** caixas e selecione **atualização**.
1. Para desabilitar uma origem de pacote, desmarque a caixa à esquerda do nome na lista.
1. Para remover uma origem de pacote, selecione-o e, em seguida, selecione a **X** botão.
1. Use a para cima e para baixo de botões de seta para alterar a ordem de prioridade das fontes de pacote. Visual Studio procura essas fontes na ordem de prioridade ao restaurar pacotes para um projeto. Para obter mais informações, consulte [restauração do pacote](../consume-packages/package-restore.md).

> [!Tip]
> Se uma origem de pacote for exibida novamente após a exclusão, ele pode estar listado em um nível de computador ou usuário `NuGet.Config` arquivos. Ver [o comportamento do NuGet configurando](../consume-packages/configuring-nuget-behavior.md) para o local desses arquivos, em seguida, remover a fonte editando os arquivos manualmente ou usando o [nuget fontes de comando](../tools/nuget-exe-CLI-reference.md).

## <a name="package-manager-options-control"></a>Controle de opções do Gerenciador de pacote

Quando um pacote é selecionado, a UI do Gerenciador de pacotes exibe um pequeno expansível **opções** controle abaixo o seletor de versão (mostrado aqui ambos recolhido ou expandido). Observe que, para alguns projetos, tipos, somente o **Mostrar janela de visualização** opção é fornecida.

![Opções do Gerenciador de pacote](media/PackageManagerUIOptions.png)

As seções a seguir explicam essas opções.

### <a name="show-preview-window"></a>Mostrar janela de visualização

Quando selecionada, uma janela modal exibe quais as dependências de um pacote escolhido antes de instalar o pacote:

![Caixa de diálogo de visualização de exemplo](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Opções de atualização e instalação

(Não disponível para todos os tipos de projeto.)

**Comportamento de dependência** configura como o NuGet decide quais versões dos pacotes dependentes para instalar:

- *Ignorar dependências* ignora a instalação de todas as dependências, que geralmente interrompe o pacote que está sendo instalado.
- *Mais baixo* [padrão] a dependência é instalado com o número de versão mínima que atende aos requisitos do pacote principal escolhido.
- *Patch do mais alto* instala a versão com os mesmos números de versão principal e secundária, mas o número mais alto de patch. Por exemplo, se a versão 1.2.2 for especificada, em seguida, a versão mais recente que começa com 1.2 será instalada
- *Mais alto Minor* instala a versão com o mesmo número de versão principal, mas o menor número mais alto e o número de patch. Se a versão 1.2.2 for especificada, a versão mais recente que começa com 1 será instalada
- *Mais alto* instala a versão disponível mais recente do pacote.

**Ação de conflitos de arquivo** Especifica como o NuGet deve manipular pacotes que já existem no projeto ou no computador local:

- *Prompt* instrui o NuGet para perguntar se deseja manter ou substituir os pacotes existentes.
- *Ignorar tudo* instrui o NuGet ignore a substituição de todos os pacotes existentes.
- *Substituir tudo* instrui o NuGet para substituir todos os pacotes existentes.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>Opções de desinstalação

(Não disponível para todos os tipos de projeto.)

**Remover dependências**: quando selecionado, remove todos os pacotes dependentes se elas não são referenciadas em outro lugar no projeto.

**Desinstalação forçada, mesmo se não houver dependências nele**: quando selecionado, desinstala um pacote, mesmo se ele ainda está sendo referenciado no projeto. Isso normalmente é usado em combinação com **remover dependências** para remover um pacote e tudo o que dependências ele instalado. O uso dessa opção pode, no entanto, levar a referências quebradas no projeto. Nesses casos, talvez você precise [reinstalar esses outros pacotes](../consume-packages/reinstalling-and-updating-packages.md).
