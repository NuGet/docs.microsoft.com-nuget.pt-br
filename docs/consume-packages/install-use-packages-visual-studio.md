---
title: Instalar e gerenciar pacotes do NuGet no Visual Studio
description: Instruções para usar a interface do usuário do Gerenciador de Pacotes do NuGet no Visual Studio para trabalhar com pacotes do NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 3adceac8c725d9ea1610aea090753c9c1d8bc818
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428691"
---
# <a name="install-and-manage-packages-in-visual-studio-using-the-nuget-package-manager"></a>Instalar e gerenciar pacotes no Visual Studio usando o Gerenciador de Pacotes do NuGet

A interface do usuário do Gerenciador de Pacotes do NuGet no Visual Studio no Windows possibilita instalar, desinstalar e atualizar pacotes do NuGet com facilidade em projetos e soluções. Para obter a experiência no Visual Studio para Mac, confira [Incluir um pacote do NuGet em seu projeto](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json). A interface do usuário do Gerenciador de Pacotes não está incluída no Visual Studio Code.

> [!NOTE]
> Se você não tem o Gerenciador de Pacotes do NuGet no Visual Studio 2015, marque **Ferramentas > Extensões e Atualizações...** e pesquise pela extensão *Gerenciador de Pacotes do NuGet*. Se você não puder usar o instalador de extensões no [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)Visual Studio, baixe a extensão diretamente de .
>
> A partir do Visual Studio 2017, o NuGet e o Gerenciador de Pacotes do NuGet são instalados automaticamente com qualquer carga de trabalho relacionada ao .NET. Para instalá-los individualmente, selecione a opção **Componentes individuais > Ferramentas de código > Gerenciador de Pacotes do NuGet** no instalador do Visual Studio.

## <a name="find-and-install-a-package"></a>Encontrar e instalar um pacote

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Referências** ou em um projeto e selecione **Gerenciar Pacotes do NuGet...**.

    ![Opção de menu Gerenciar Pacotes do NuGet](media/ManagePackagesUICommand.png)

1. A guia **Procurar** exibe pacotes por popularidade a partir da origem selecionada no momento (confira [origens de pacotes](#package-sources)). Procure um pacote específico usando a caixa de pesquisa no canto superior esquerdo. Selecione um pacote na lista para exibir as informações sobre ele, o que também habilita o botão **Instalar** com uma lista suspensa de seleção de versão.

    ![Guia Procurar da caixa de diálogo Gerenciar Pacotes do NuGet](media/Search.png)

1. Selecione a versão desejada na lista suspensa e selecione **Instalar**. O Visual Studio instala o pacote e suas dependências no projeto. Você pode ser solicitado a aceitar os termos de licença. Quando a instalação é concluída, os pacotes adicionados aparecem na guia **Instalado.** Os pacotes também estão listados no nó `using` **Referências** do Solution Explorer, indicando que você pode se referir a eles no projeto com instruções.

    ![Referências no Gerenciador de Soluções](media/References.png)

> [!Tip]
> Para incluir versões de pré-lançamento na pesquisa e disponibilizar essas versões na lista suspensa de versões, selecione a opção **Incluir pré-lançamento**.

> [!Note]
> NuGet tem dois formatos nos quais um [`PackageReference`](package-references-in-project-files.md) [`packages.config`](../reference/packages-config.md)projeto pode usar pacotes: e . [O padrão pode ser definido na janela de opções do Visual Studio.](Package-Restore.md#choose-default-package-management-format)

## <a name="uninstall-a-package"></a>Desinstalar um pacote

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Referências** ou no projeto desejado e selecione **Gerenciar Pacotes do NuGet...**.
1. Selecione a guia **Instalado**.
1. Selecione o pacote a desinstalar (usando a pesquisa para filtrar a lista, se necessário) e selecione **Desinstalar**.

    ![Desinstalar um pacote](media/UninstallPackage.png)

1. Os controles **Incluir pré-lançamento** e **Origem do pacote** não têm efeito ao desinstalar pacotes.

## <a name="update-a-package"></a>Atualizar um pacote

1. No **Solution Explorer,** clique com o botão direito do mouse **nas referências** ou no projeto desejado e selecione **Gerenciar pacotes NuGet...**. (Em projetos de sites, clique com o botão direito do mouse na pasta **Bin.)**
1. Selecione a guia **Atualizações** para ver os pacotes que têm atualizações disponíveis das origens de pacotes selecionadas. Selecione **Incluir pré-lançamento** para incorporar pacotes de pré-lançamento à lista de atualizações.
1. Selecione o pacote a atualizar, escolha a versão desejada na lista suspensa à direita e selecione **Atualizar**.

    ![Atualizar um pacote](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>Em alguns pacotes, o botão **Atualizar** fica desabilitado e uma mensagem é exibida informando que é "Referenciado implicitamente por um SDK" (ou "Autorreferenciado"). Essa mensagem indica que o pacote faz parte de uma estrutura ou SDK mais amplo e não deve ser atualizado de forma independente. (Tais pacotes são marcados internamente com `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Por exemplo, `Microsoft.NETCore.App` faz parte do .NET Core SDK, e a versão do pacote não é a mesma da versão do framework de tempo de execução usado pelo aplicativo. É preciso [atualizar a instalação do .NET Core](https://aka.ms/dotnet-download) para obter novas versões do ASP.NET Core e do runtime do .NET Core. [Confira este documento para saber mais sobre o controle de versão e os metapacotes do .NET Core](/dotnet/core/packages). Isso se aplica aos seguintes pacotes usados com frequência:
    * Microsoft.AspNetCore.All
    * Microsoft.AspNetCore.App
    * Microsoft.NETCore.App
    * NETStandard.Library

    ![Exemplo de pacote marcado como Referenciado implicitamente ou Autorreferenciado](media/PackageManagerUIAutoReferenced.png)

1. Para atualizar vários pacotes para suas versões mais recentes, selecione-os na lista e selecione o botão **Atualizar** acima da lista.
1. Você também pode atualizar um pacote individual da guia **Instalado.** Neste caso, os detalhes do pacote incluem um seletor de versão (sujeito à opção **Incluir pré-lançamento)** e um botão **Atualizar.**

## <a name="manage-packages-for-the-solution"></a>Gerenciar pacotes para a solução

O gerenciamento de pacotes para uma solução é um meio conveniente de trabalhar com vários projetos ao mesmo tempo.

1. Selecione o comando no menu **Ferramentas > Gerenciador de Pacotes do NuGet > Gerenciar Pacotes do NuGet para Solução...** ou clique com o botão direito do mouse na solução e selecione **Gerenciar Pacotes do NuGet...**:

    ![Gerenciar Pacotes do NuGet para a solução](media/ManagePackagesSolutionUICommand.png)

1. Ao gerenciar pacotes para a solução, a interface do usuário possibilita selecionar os projetos afetados pelas operações:

    ![Seletor de projeto ao gerenciar pacotes para a solução](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>Guia Consolidar

Os desenvolvedores costumam considerar uma prática inadequada usar versões diferentes do mesmo pacote do NuGet em diferentes projetos na mesma solução. Ao optar por gerenciar pacotes para uma solução, a interface do usuário do Gerenciador de Pacotes fornece uma guia **Consolidar**, em que é possível ver facilmente onde os pacotes com números de versão distintos são usados por diferentes projetos na solução:

![Guia Consolidar da interface do usuário do Gerenciador de Pacotes](media/ConsolidateTab.png)

Neste exemplo, o projeto ClassLibrary1 está usando EntityFramework 6.2.0, enquanto o ConsoleApp1 está usando EntityFramework 6.1.0. Para consolidar as versões de pacote, faça o seguinte:

- Selecione os projetos a atualizar na lista de projetos.
- Selecione a versão a usar em todos esses projetos no controle **Versão**, como o EntityFramework 6.2.0.
- Selecione o botão **Instalar**.

O Gerenciador de Pacotes instala a versão de pacote selecionada em todos os projetos selecionados e, após isso, o pacote não aparece mais na guia **Consolidar**.

## <a name="package-sources"></a>Origens de pacotes

Para alterar a origem da qual o Visual Studio obtém pacotes, selecione uma no seletor de origem:

![Seletor de origem de pacotes na interface do usuário do Gerenciador de Pacotes](media/PackageSourceDropDown.png)

Para gerenciar origens de pacotes:

1. Selecione o ícone **Configurações** na interface do usuário do Gerenciador de Pacotes descrita abaixo ou use o comando **Ferramentas> Opções** e role até **Gerenciador de Pacotes do NuGet**:

    ![Ícone de configurações da interface do usuário do Gerenciador de Pacotes](media/PackageSourceSettings.png)

1. Selecione o nó **Origens do Pacote**:

    ![Opções de Origens do Pacote](media/options.png)

1. Para adicionar uma **+** fonte, selecione, edite o nome, insira a URL ou o caminho no controle **De origem** e selecione **Atualizar**. A origem agora aparece na lista suspensa do seletor.
1. Para alterar uma origem de pacotes, selecione-a, faça as edições nas caixas **Nome** e **Origem** e selecione **Atualizar**.
1. Para desabilitar uma origem de pacotes, desmarque a caixa à esquerda do nome na lista.
1. Para remover uma origem de pacotes, selecione-a e, em seguida, selecione o botão **X**.
1. O uso dos botões de seta para cima e para baixo não altera a ordem de prioridade das origens de pacotes. O Visual Studio ignora a ordem das origens de pacotes, usando o pacote de qualquer origem que responder às solicitações primeiro. Para saber mais, confira [Restauração de pacote](../consume-packages/package-restore.md).

> [!Tip]
> Caso uma origem de pacotes reapareça depois de ser excluída, pode ser listada em arquivos `NuGet.Config` no nível do computador ou do usuário. Confira [Configurações comuns do NuGet](../consume-packages/configuring-nuget-behavior.md) para conhecer o local desses arquivos, depois remova a origem editando os arquivos manualmente ou usando o [comando nuget sources](../reference/nuget-exe-CLI-reference.md).

## <a name="package-manager-options-control"></a>Controle de opções do Gerenciador de Pacotes

Ao selecionar um pacote, a interface do usuário do Gerenciador de Pacotes exibe um controle **Opções** pequeno e expansível abaixo do seletor de versão (mostrado aqui recolhido e expandido). Em alguns tipos de projeto, apenas a opção **Mostrar janela de visualização** é fornecida.

![Opções do Gerenciador de Pacotes](media/PackageManagerUIOptions.png)

As seções a seguir explicam essas opções.

### <a name="show-preview-window"></a>Mostrar janela de visualização

Quando selecionada, uma janela modal exibe as dependências de um pacote escolhido antes da instalação do pacote:

![Exemplo da caixa de diálogo Visualizar](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Opções de instalação e atualização

Não disponíveis para todos os tipos de projeto.

**Comportamento da dependência** define como o NuGet decide quais versões de pacotes dependentes serão instaladas:

- *Ignorar Dependências* ignora a instalação de dependências, o que normalmente interrompe a instalação do pacote.
- *Mais Baixa* [Padrão] instala a dependência com o número de versão mínimo que atende aos requisitos do pacote principal escolhido.
- *Patch Mais Alto* instala a versão com os mesmos números de versão principal e secundária, mas com o número de patch mais alto. Por exemplo, se a versão 1.2.2 for especificada, a versão mais alta que começa com 1.2 será instalada
- *Secundário Mais Alto* instala a versão com o mesmo número de versão principal, mas com o número secundário e o número de patch mais altos. Se a versão 1.2.2 for especificada, a versão mais alta que começa com 1 será instalada
- *Mais Alta* instala a versão mais alta disponível do pacote.

**Ação de conflito de arquivo** especifica como o NuGet deve lidar com pacotes que já existem no projeto ou no computador local:

- *Avisar* instrui o NuGet a perguntar se os pacotes existentes serão mantidos ou substituídos.
- *Ignorar tudo* instrui o NuGet a ignorar a substituição de pacotes existentes.
- *Substituir Tudo* instrui o NuGet a substituir pacotes existentes.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>Opções de desinstalação

Não disponíveis para todos os tipos de projeto.

**Remover dependências**: quando selecionada, remove todos os pacotes dependentes caso não estejam referenciados em outro lugar no projeto.

**Forçar desinstalação, mesmo se houver dependências**: quando selecionada, desinstala um pacote mesmo se ele ainda está sendo referenciado no projeto. Normalmente, isso é usado em combinação com **Remover dependências** para remover um pacote e quaisquer dependências que ele instalou. No entanto, o uso dessa opção pode causar referências inválidas no projeto. Nesses casos, talvez seja necessário [reinstalar os outros pacotes](../consume-packages/reinstalling-and-updating-packages.md).
