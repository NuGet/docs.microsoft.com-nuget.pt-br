---
title: Referência de interface do usuário do Gerenciador de pacotes do NuGet
description: Instruções para usar o NuGet Package Manager UI no Visual Studio para trabalhar com pacotes do NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 307416908aff5db12fbf6f419e20acc6e0a9b241
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818835"
---
# <a name="nuget-package-manager-ui"></a>Interface do usuário de Gerenciador de pacotes do NuGet

O NuGet Package Manager UI no Visual Studio no Windows permite que você facilmente instalar, desinstalar e atualizar pacotes do NuGet em projetos e soluções. Para obter a experiência no Visual Studio para Mac, consulte [incluindo NuGet um pacote em seu projeto](/visualstudio/mac/nuget-walkthrough). A UI do Gerenciador de pacote não está incluída com o código do Visual Studio.

Neste tópico:

- [Localizar e instalar um pacote (guia de navegação)](#finding-and-installing-a-package)
- [Desinstalar um pacote (guia instalado)](#uninstalling-a-package)
- [Atualizando um pacote (guias instalado e atualizações)](#updating-a-package) (inclui o ["Mencionada implicitamente por um SDK" ou "AutoReferenced" mensagem](#implicit_reference))
- [Gerenciando pacotes para a solução](#managing-packages-for-the-solution) (trabalhando com vários projetos ao mesmo tempo).
- [Fontes de pacote](#package-sources)
- [Controle de opções do Gerenciador de pacote](#package-manager-options-control)

> [!Note]
> Verifique se está faltando o NuGet Package Manager no Visual Studio 2015, **Ferramentas > extensões e atualizações...**  e procure o *NuGet Package Manager* extensão. Se não for possível usar o instalador de extensões do Visual Studio, baixe a extensão diretamente do [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).
>
> No Visual Studio de 2017, o NuGet e o NuGet Package Manager são instalados automaticamente com qualquer. Cargas de trabalho relacionados à rede. Instalá-lo individualmente selecionando o **componentes individuais > código Ferramentas > Gerenciador de pacotes do NuGet** opção no instalador do Visual Studio de 2017.

## <a name="finding-and-installing-a-package"></a>Localizar e instalar um pacote

1. Em **Solution Explorer**, clique **referências** ou um projeto e selecione **gerenciar pacotes NuGet...** .

    ![Gerenciar a opção de menu de pacotes do NuGet](media/ManagePackagesUICommand.png)

1. O **procurar** guia exibe pacotes por popularidade da origem selecionada atualmente (consulte [pacote fontes](#package-sources)). Procurar por um pacote específico usando a caixa de pesquisa no canto superior esquerdo. Selecione um pacote na lista para exibir suas informações, que também permite que o **instalar** botão juntamente com um menu suspenso de seleção de versão.

    ![Gerenciar guia Procurar de caixa de diálogo de pacotes do NuGet](media/Search.png)

1. Selecione a versão desejada na lista suspensa e selecione **instalar**. O Visual Studio instala o pacote e suas dependências no projeto. Você poderá ser solicitado a aceitar os termos de licença. Quando a instalação for concluída, os pacotes adicionados são exibidos no **instalado** guia. Os pacotes também são listados no **referências** nó do Gerenciador de soluções, indicando que você possa consultá-los no projeto com `using` instruções.

    ![Referências no Gerenciador de soluções](media/References.png)

> [!Tip]
> Para incluir as versões de pré-lançamento na pesquisa e para disponibilizar as versões de pré-lançamento na versão de lista suspensa, selecione o **incluir pré-lançamento** opção.

## <a name="uninstalling-a-package"></a>Desinstalar um pacote

1. Em **Solution Explorer**, clique **referências** ou o projeto desejado e selecione **gerenciar pacotes NuGet...** .
1. Selecione o **instalado** guia.
1. Selecione o pacote para desinstalar (usando a pesquisa para filtrar a lista, se necessário) e selecione **desinstalação**.

    ![Desinstalar um pacote](media/UninstallPackage.png)

1. Observe que o **incluir pré-lançamento** e **origem do pacote** controles não têm nenhum efeito durante a desinstalação de pacotes.

## <a name="updating-a-package"></a>Um pacote de atualização

1. Em **Solution Explorer**, clique **referências** ou o projeto desejado e selecione **gerenciar pacotes NuGet...** . (Em projetos de site da web, clique com botão direito do **Bin** pasta.)
1. Selecione o **atualizações** guia para ver os pacotes que têm atualizações disponíveis de origens do pacote selecionado. Selecione **incluir pré-lançamento** inclui pacotes pré-lançados na lista de atualização.
1. Selecione o pacote para atualizar, selecione a versão desejada na lista suspensa à direita e selecione **atualizar**.

    ![Um pacote de atualização](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>Para alguns pacotes, o **atualização** botão será desabilitado e será exibida uma mensagem dizendo que é "implicitamente referenciado por um SDK" (ou "AutoReferenced"). A mensagem indica que o pacote, como Microsoft.NETCore.App ou Microsoft.NETStandard.Library, faz parte de uma estrutura ou o SDK maior e não deve ser atualizado independentemente. (Esses pacotes internamente são marcados com `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Para atualizar o pacote, atualize o SDK ao qual ele pertence, inferir o SDK do recipiente do nome do pacote. Por exemplo, um pacote como Microsoft.NETCore.App faz parte do SDK .NET Core, portanto você precisa atualizar sua instalação do SDK do .NET Core.

    ![Pacote de exemplo são marcados como implicitamente referências ou AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. Para atualizar vários pacotes para as versões mais recentes, selecione na lista e selecione o **atualizar** botão acima da lista.
1. Você também pode atualizar um pacote individual do **instalado** guia. Nesse caso, os detalhes do pacote incluem um seletor de versão (sujeito a **incluir pré-lançamento** opção) e um **atualização** botão.

## <a name="managing-packages-for-the-solution"></a>Gerenciando pacotes para a solução

Gerenciando pacotes para uma solução é uma maneira conveniente para trabalhar com vários projetos simultaneamente.

1. Selecione o **Ferramentas > Gerenciador de pacotes do NuGet > Gerenciar pacotes NuGet para solução...**  menu de comando, ou a solução e selecione **gerenciar pacotes NuGet...** :

    ![Gerenciar pacotes NuGet para a solução](media/ManagePackagesSolutionUICommand.png)

1. Ao gerenciar pacotes da solução, a interface do usuário permite que você selecione os projetos que são afetados pelas operações:

    ![Seletor de projeto ao gerenciar pacotes da solução](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>Consolidar guia

Os desenvolvedores geralmente ele considerar prática inadequada para usar versões diferentes do mesmo pacote do NuGet em diferentes projetos na mesma solução. Quando você optar por gerenciar os pacotes para uma solução, a UI Package Manager fornece um **consolidar** guia na qual você pode ver facilmente onde os pacotes com números de versão diferentes são usados por diferentes projetos na solução:

![Guia de consolidar de interface do usuário do Gerenciador de pacotes](media/ConsolidateTab.png)

Neste exemplo, o projeto ClassLibrary1 está usando EntityFramework 6.2.0, enquanto ConsoleApp1 é usando o EntityFramework 6.1.0. Para consolidar as versões do pacote, faça o seguinte:

- Selecione os projetos para atualizar a lista de projeto.
- Selecione a versão a ser usado em todos os projetos no **versão** controle, como EntityFramework 6.2.0.
- Selecione o **instalar** botão.

O Gerenciador de pacote instala a versão do pacote selecionado em todos os projetos selecionados, após o qual o pacote não aparecerá mais no **consolidar** guia.

## <a name="package-sources"></a>Fontes de pacote

Para alterar a origem do qual o Visual Studio obtém pacotes, selecione um do seletor de origem:

![Seletor de origem do pacote no Gerenciador de pacote da interface do usuário](media/PackageSourceDropDown.png)

Para gerenciar fontes de pacote:

1. Selecione o **configurações** ícone na UI do Gerenciador de pacotes descritas a seguir ou use o **Ferramentas > Opções** de comando e role até **NuGet Package Manager**:

    ![Ícone de configurações de interface do usuário do pacote manager](media/PackageSourceSettings.png)

1. Selecione o **origens do pacote** nó:

    ![Opções de fontes de pacote](media/options.png)

1. Para adicionar uma fonte, selecione **+**, edite o nome, digite a URL ou caminho de **fonte** controle e selecione **atualização**. A fonte agora aparece no seletor de lista suspensa.
1. Para alterar uma origem do pacote, selecioná-lo, faça edições no **nome** e **fonte** caixas e selecione **atualização**.
1. Para desabilitar uma origem do pacote, desmarque a caixa à esquerda do nome na lista.
1. Para remover uma origem do pacote, selecione-o e, em seguida, selecione o **X** botão.
1. Use a cima e para os botões de seta para alterar a ordem de prioridade das origens do pacote. O Visual Studio procura essas fontes na ordem de prioridade ao restaurar pacotes para um projeto. Para obter mais informações, consulte [restauração do pacote](../consume-packages/package-restore.md).

> [!Tip]
> Se uma origem de pacote reaparecer após a exclusão, podem ser listado em um nível de computador ou usuário `NuGet.Config` arquivos. Consulte [NuGet Configurando comportamento](../consume-packages/configuring-nuget-behavior.md) para o local desses arquivos, em seguida, remover a fonte editando os arquivos manualmente ou usando o [nuget fontes comando](../tools/nuget-exe-CLI-reference.md).

## <a name="package-manager-options-control"></a>Controle de opções do Gerenciador de pacote

Quando um pacote é selecionado, a UI Package Manager exibe um pequeno expansível **opções** controle abaixo do seletor de versão (mostrado aqui ambos recolhidos e expandidos). Observe que, para alguns projetos, tipos, somente o **Mostrar janela de visualização** opção é fornecida.

![Opções do Gerenciador de pacote](media/PackageManagerUIOptions.png)

As seções a seguir explicam essas opções.

### <a name="show-preview-window"></a>Mostrar janela de visualização

Quando selecionada, uma janela modal exibe quais as dependências de um pacote escolhido antes de instalar o pacote:

![Caixa de diálogo de visualização de exemplo](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Opções de atualização e instalação

(Não disponível para todos os tipos de projeto.)

**Comportamento da dependência** configura como o NuGet decide quais versões dos pacotes dependentes para instalar:

- *Ignorar dependências* ignora a instalação de todas as dependências, que normalmente interrompe o pacote que está sendo instalado.
- *Menor* [padrão] instala a dependência com o número de versão mínima que atenda aos requisitos do pacote principal escolhido.
- *Patch do mais alto* instala a versão com os mesmos números de versão primária e secundária, mas o número mais alto de patch. Por exemplo, se a versão 1.2.2 for especificada, em seguida, a versão mais recente que começa com 1.2 será instalada
- *Mais alta secundária* instala a versão com o mesmo número de versão principal, mas o número mais alto de pequena e o número de patch. Se a versão 1.2.2 for especificada, a versão mais recente que começa com 1 será instalada
- *Mais alto* instala a versão mais recente disponível do pacote.

**Ação de conflitos de arquivo** Especifica como o NuGet deve manipular pacotes que já existem no projeto ou no computador local:

- *Prompt* instrui o NuGet para perguntar se deseja manter ou substituir os pacotes existentes.
- *Ignorar tudo* instrui o NuGet para ignorar a substituição de todos os pacotes existentes.
- *Substituir todos os* instrui o NuGet para substituir todos os pacotes existentes.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>As opções de desinstalação

(Não disponível para todos os tipos de projeto.)

**Remover dependências**: quando selecionada, remove todos os pacotes dependentes que elas não são referenciadas em outro lugar no projeto.

**Forçar desinstalação mesmo se houver dependências nele**: quando selecionado, desinstala um pacote mesmo se ele ainda está sendo referenciado no projeto. Isso geralmente é usado em combinação com **remover dependências** para remover um pacote e tudo o que ele instalado de dependências. O uso dessa opção pode, no entanto, levar a referências quebradas no projeto. Nesses casos, talvez seja necessário para [reinstalar esses outros pacotes](../consume-packages/reinstalling-and-updating-packages.md).
