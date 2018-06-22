---
title: Notas de versão do NuGet 3.0 Preview
description: Notas de versão do NuGet 3.0 Preview incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 67c217e52d975ed8f6889cd69f9b7e0d52b3a119
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821308"
---
# <a name="nuget-30-preview-release-notes"></a>Notas de versão do NuGet 3.0 Preview

[Notas de versão de RC do NuGet 2.9](../release-notes/nuget-2.9-rc.md) | [notas de versão do NuGet 3.0 Beta](../release-notes/nuget-3.0-beta.md)

Visualização do NuGet 3.0 foi lançada em 12 de novembro de 2014 como parte da versão do Visual Studio 2015 Preview. Lançamos NuGet 3.0 Preview. Esta é uma versão grande para que possamos (embora uma visualização), e estamos empolgados em para iniciar a obtenção de comentários em nossas alterações.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Essa visualização do NuGet 3.0 está incluída no Visual Studio 2015 Preview. Estamos trabalhando para sair descartes de preview para Visual Studio 2012 e o Visual Studio 2013 muito em breve. Anteriormente, compartilhamos nossa intenção [interromper as atualizações para o Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), e fez essa decisão difícil.

## <a name="brand-new-ui"></a>Nova interface do usuário

A primeira coisa que você observar sobre a visualização do NuGet 3.0 é nossa nova interface do usuário. Não é mais uma caixa de diálogo modal; Agora é uma janela de documento do Visual Studio completa. Isso permite que você abrir a interface do usuário para vários projetos (e/ou a solução) uma vez, separar a janela para outro monitor, encaixá-la, no entanto, seria como, etc.

![O novo UI NuGet](./media/NuGet-3.0-Preview/new-ui.png)

Além das diferenças de usabilidade devido a caixa de diálogo modal abandoná-la, também temos muitos novos recursos na nova interface de usuário.

### <a name="version-selection"></a>Seleção de versão

Talvez a mais solicitados é o recurso de interface do usuário permitir a seleção de versão para a instalação e a atualização agora está disponível.

![Seleção de versão do pacote](./media/NuGet-3.0-Preview/version-selection.png)

Se você estiver instalando ou atualizando um pacote, a lista suspensa de versão permite que você veja todas as versões disponíveis para o pacote, com algumas versões importantes promovidos para a parte superior da lista para facilitar a seleção. Você não precisa usar o Console do PowerShell para obter versões específicas que não sejam o mais recente.

### <a name="combined-installedonlineupdates-workflows"></a>Fluxos de trabalho combinados/Online/atualizações instaladas

Nossa interface do usuário anterior tinha 3 guias para on-line, instalado e atualizações. Os pacotes listados foram específicos para esses fluxos de trabalho e as ações disponíveis foram específicas para os fluxos de trabalho. Enquanto que parecia lógico, que ouvimos que muitos de vocês geralmente seriam obter ultrapassadas por essa separação.

Agora temos uma experiência combinada, onde você pode instalar, atualizar ou desinstalar um pacote, independentemente de como você obteve o pacote selecionado. Para ajudar com os fluxos de trabalho específicos, agora temos uma lista suspensa de filtro que permite a você filtrar os pacotes visíveis, mas, em seguida, as ações disponíveis para o pacote são consistentes.

![Desinstalar um pacote](./media/NuGet-3.0-Preview/uninstall-package.png)

Usando o filtro "Instalar", você poderá facilmente ver seus pacotes instalados, que possuem atualizações disponíveis, e, em seguida, você pode desinstalar ou atualizar o pacote alterando a seleção de versão para ver alterar a ação disponível.

![Um pacote de atualização](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>Consolidação de versão

É comum ter o mesmo pacote instalado em vários projetos em sua solução. Às vezes, as versões instaladas em cada projeto podem desviar e é necessário consolidar as versões em uso. Visualização do NuGet 3.0 apresenta um novo recurso para apenas nesse cenário.

A janela de gerenciamento de nível de solução de pacote pode ser acessada clicando duas vezes na solução e escolha gerenciar pacotes NuGet para solução. A partir daí, se você selecionar um pacote que está instalado em vários projetos, mas com diferentes versões em uso, uma nova ação de "Consolidar" se torna disponível. Na captura de tela abaixo, `Newtonsoft.Json` foi instalado para o `SamplesClassLibrary` com versão `6.0.4` e instalado em `SamplesConsoleApp` com a versão `5.0.4`.

![Consolidar versões](./media/NuGet-3.0-Preview/consolidate.png)

Aqui está o fluxo de trabalho para consolidação em uma única versão.

1. Selecione o `Newtonsoft.Json` pacote da lista
1. Escolha `Consolidate` do `Action` suspenso
1. Use o `Version` lista suspensa para selecionar a versão a ser consolidados em
1. Marque as caixas de projetos que devem ser consolidados em que a versão (Observe que projetos que já está na versão selecionada ficará esmaecidos)
1. Clique o `Consolidate` botão para executar a consolidação

### <a name="operation-previews"></a>Visualizações de operação

Independentemente de qual operação estiver executando – instalação/atualização/desinstalação – a nova interface do usuário agora oferece uma maneira de visualizar as alterações que serão feitas ao seu projeto. Essa visualização mostra qualquer novos pacotes que serão instalados pacotes que serão atualizados e pacotes que serão desinstalados, junto com pacotes que serão alterados durante a operação.

No exemplo a seguir, podemos ver que instalar o SignalR resultará em algumas poucas alterações ao projeto.

![Visualização instalando SignalR](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>Opções de instalação

Usando o Console do PowerShell, você teve controle sobre algumas das opções de instalação importantes. Agora, trouxemos esses recursos para a interface de usuário. Agora você pode controlar o comportamento de resolução de dependência para como as versões das dependências são selecionadas.

![Comportamento da dependência](./media/NuGet-3.0-Preview/dependency-behavior.png)

Você também pode especificar a ação a ser tomada quando os arquivos de conteúdo de pacotes em conflito com arquivos já está em seu projeto.

![Ação de conflitos de arquivo](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>Rolagem infinita

É usado para obter um pouco de comentários sobre nossa interface do usuário ter ambos a rolagem e paginação paradigmas ao listar os pacotes. Era muito comum para rolar para a parte inferior da lista curta, clique o próximo número de página e, em seguida, role novamente. Com a nova interface do usuário, implementamos infinito de rolagem na lista de pacote para que você só precisará rolar – não há mais de paginação.

![Rolagem infinita](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>Torná-lo o trabalho, torná-lo rápidos e torná-lo a formatação

Estamos felizes em obter essa nova interface do usuário-out para você experimentar. Durante essa etapa de visualização, estamos seguindo o bom princípio de "realizar funcionam, torná-lo mais rápido, embelezar." Nesta visualização, podemos tenha realizado grande parte dessa primeira meta - ele funciona. Sabemos que ele ainda não é muito rápido e sabemos muito bem ainda não está. Relação de confiança que podemos trabalhar com esses objetivos entre agora e a versão RC. Enquanto isso, adoraríamos receber seus comentários sobre o *usabilidade* da nova interface do usuário – a fluxos de trabalho, operações e como ele *parece* para usar a nova interface do usuário.

Há algumas funções removemos quando comparado com a antiga interface do usuário. Um deles tenha sido intencional e outros aquele apenas não é realizada no tempo.

#### <a name="searching-all-package-sources"></a>Pesquisar fontes de pacote "Tudo"

A interface do usuário antigo permitido a você realizar uma pesquisa de pacote em relação a todas as suas fontes de pacote. Removemos esse recurso na interface de usuário e não seja colocá-lo. Esse recurso é usado para executar operações de pesquisa em todas as suas fontes de pacote, reunir os resultados e tentar ordenar os resultados com base em sua seleção de classificação.

Descobrimos que a relevância da pesquisa é realmente difícil reunir. Você pode imaginar realizar uma pesquisa no Google e Bing e combinando os resultados em conjunto? Além disso, esse recurso foi lenta, fácil de *acidentalmente* uso e acredita que raramente é realmente útil. Devido os problemas de recurso introduzido, recebemos um número de relatórios de bugs nele pode nunca foram corrigidos.

#### <a name="update-all"></a>Atualizar tudo

Usamos têm um botão "Atualizar tudo" na interface de usuário antiga que ainda não está lá na nova interface de usuário. Podemos será ressuscitar esse recurso para nossa versão RC.

## <a name="new-clientserver-api"></a>Novo cliente/servidor de API

Além de todos os novos recursos do nosso novo gerenciamento de pacote da interface do usuário, podemos também tenha trabalhado em alguns detalhes de implementação para o protocolo de cliente/servidor do NuGet. O trabalho que já fizemos é criar "API v3" NuGet, que foi projetado para alta disponibilidade de cenários críticos como a restauração do pacote e instalação de pacotes. A nova API é baseada em REST e hipermídia e selecionou [JSON LD](http://json-ld.org) como nosso formato de recurso.

Os bits de visualização do NuGet 3.0, você verá uma nova origem do pacote chamada "preview.nuget.org" no menu suspenso de origem do pacote. Se você selecionar essa fonte de pacote, vamos usar nossa nova API em vez disso, para se conectar ao nuget.org. Fizemos visualizar fonte disponível na interface de usuário enquanto continuamos a testar, revisar e melhorar a nova API. No NuGet 3.0 RC, essa nova fonte de pacote com base em v3 API substituirá a origem do pacote com base em v2 "nuget.org".

Apesar do investimento em que nós colocamos em API v3, fizemos todos esses novos recursos também funcionam com o protocolo de v2 nossa API existente, que significa que eles funcionarão com fontes de pacote existentes que não seja bem nuget.org.

## <a name="new-features-coming"></a>Novos recursos em

Entre agora e 3.0 RTM, estamos também trabalhando em alguns novos NuGet recursos fundamentais, além do que você vê na interface do usuário. Aqui está uma lista curta de áreas de investimento principais:

1. Podemos estiver está em parceria com o Visual Studio e as equipes de MSBuild para obter [NuGet mais profundo na plataforma](http://blog.nuget.org/20141014/in-the-platform.html).
1. Estamos trabalhando para abandonar as convenções do pacote de tempo de instalação e aplicar em vez disso, essas convenções em tempo de empacotamento introduzindo um novo "autoritativo" [manifesto de pacote](http://blog.nuget.org/20141023/package-manifests.html).
1. Estamos trabalhando para refatorar o NuGet codebase para fazer com que os componentes de cliente e servidor reutilizáveis em domínios diferentes, além do gerenciamento de pacotes no Visual Studio.
1. Estamos investigando a noção de "dependências privadas" em que um pacote pode indicar que ele tem dependências em outros pacotes para apenas os detalhes de implementação, e essas dependências não devem ser apresentadas como dependências de nível superior.

## <a name="stay-tuned"></a>Fique atento

Fique atento [nosso blog](http://blog.nuget.org) para mais de progresso e avisos do NuGet 3.0!