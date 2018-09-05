---
title: Notas de versão do NuGet 3.0 versão prévia
description: Notas de versão do NuGet 3.0 Preview incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9389639476172d05556b95d589e429ddfe0e3026
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546459"
---
# <a name="nuget-30-preview-release-notes"></a>Notas de versão do NuGet 3.0 versão prévia

[Notas de versão de RC NuGet 2.9](../release-notes/nuget-2.9-rc.md) | [notas de versão do NuGet 3.0 Beta](../release-notes/nuget-3.0-beta.md)

Versão prévia do NuGet 3.0 foi lançada em 12 de novembro de 2014, como parte da versão do Visual Studio 2015 Preview. Lançamos a versão prévia do NuGet 3.0. Isso é um grande lançamento para nós (embora uma versão prévia), e estamos ansiosos para começar a obter comentários sobre nossas alterações.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Essa visualização do NuGet 3.0 está incluída no Visual Studio 2015 Preview. Estamos trabalhando para obter os descartes de visualização-out para Visual Studio 2012 e Visual Studio 2013 muito em breve. Compartilhamos anteriormente nossa intenção [descontinuar atualizações para o Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), podemos tomar essa decisão difícil.

## <a name="brand-new-ui"></a>Nova interface do usuário

A primeira coisa a que observar sobre o NuGet 3.0 Preview é nossa nova interface do usuário. Não é mais uma caixa de diálogo modal; Agora é uma janela de documento do Visual Studio completa. Isso permite que você abra a interface do usuário para vários projetos (e/ou a solução) ao mesmo tempo, separar a janela para outro monitor, encaixá-la, no entanto, seria como, etc.

![O novo UI NuGet](./media/NuGet-3.0-Preview/new-ui.png)

Além das diferenças de usabilidade devido a abandonar a caixa de diálogo modal, também temos vários dos novos recursos na nova interface de usuário.

### <a name="version-selection"></a>Seleção de versão

Talvez o mais solicitados de recurso de interface do usuário é permitir a seleção de versão para a instalação do pacote e atualização – agora está disponível.

![Seleção de versão do pacote](./media/NuGet-3.0-Preview/version-selection.png)

Se você estiver instalando ou atualizando um pacote, a lista suspensa de versão permite que você veja todas as versões disponíveis para o pacote, com algumas versões notáveis promovidos à parte superior da lista para facilitar a seleção. Você não precisa usar o Console do PowerShell para obter versões específicas que não são a versão mais recente.

### <a name="combined-installedonlineupdates-workflows"></a>Fluxos de trabalho combinados/Online/atualizações instaladas

Nossa interface do usuário anterior tinha 3 guias para on-line, instalado e atualizações. Os pacotes listados foram específicos para esses fluxos de trabalho e as ações disponíveis eram específicas para os fluxos de trabalho. Embora essa parecia ser lógica, que nós ouvimos que muitos de vocês geralmente seriam obter atropelados por essa separação.

Agora temos uma experiência combinada, onde você pode instalar, atualizar ou desinstalar um pacote, independentemente de como você chegou o pacote selecionado. Para ajudar com os fluxos de trabalho específicos, agora temos uma lista suspensa de filtro que permite filtrar os pacotes visíveis, mas, em seguida, as ações disponíveis para o pacote são consistentes.

![Desinstalar um pacote](./media/NuGet-3.0-Preview/uninstall-package.png)

Usando o filtro de "Instalado", você pode, em seguida, ver facilmente seus pacotes instalados, quais delas têm as atualizações disponíveis, e, em seguida, você pode desinstalar ou atualizar o pacote alterando a seleção de versão para ver alterar a ação disponível.

![Um pacote de atualização](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>Consolidação de versão

É comum ter o mesmo pacote instalado em vários projetos em sua solução. Às vezes, as versões instaladas em cada projeto podem oscilar distância e é necessário consolidar as versões em uso. Versão prévia do NuGet 3.0 introduz um novo recurso para esse cenário.

A janela de gerenciamento de pacotes de nível de solução pode ser acessada clicando duas vezes na solução e escolha gerenciar pacotes NuGet para solução. A partir daí, se você selecionar um pacote que é instalado em vários projetos, mas com diferentes versões em uso, uma nova ação de "Consolidar" torna-se disponível. Na captura de tela abaixo, `Newtonsoft.Json` foi instalado para o `SamplesClassLibrary` com a versão `6.0.4` e instalada em `SamplesConsoleApp` com a versão `5.0.4`.

![Consolidar as versões](./media/NuGet-3.0-Preview/consolidate.png)

Aqui está o fluxo de trabalho para a consolidação em uma única versão.

1. Selecione o `Newtonsoft.Json` pacote na lista
1. Escolher `Consolidate` do `Action` lista suspensa
1. Use o `Version` na lista suspensa para selecionar a versão a ser consolidados em
1. Marque as caixas para os projetos que devem ser consolidados em que a versão (Observe que os projetos já estão na versão selecionada ficará esmaecidos)
1. Clique o `Consolidate` botão para executar a consolidação

### <a name="operation-previews"></a>Visualizações de operação

Independentemente de qual operação que você está executando – instalação/atualização/desinstalação – a nova interface do usuário agora oferece uma maneira de visualizar as alterações que serão feitas ao seu projeto. Essa visualização mostrará quaisquer novos pacotes que serão instalados pacotes que serão atualizados e pacotes que serão desinstalados, junto com pacotes que serão alterados durante a operação.

No exemplo a seguir, podemos ver que instalar ASPNET resultará em algumas poucas alterações ao projeto.

![Instalando o SignalR de visualização](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>Opções de instalação

Usando o Console do PowerShell, você teve controle sobre algumas das opções de instalação importantes. Agora, trouxemos esses recursos também a interface do usuário. Agora você pode controlar o comportamento de resolução de dependência para como as versões das dependências são selecionadas.

![Comportamento de dependência](./media/NuGet-3.0-Preview/dependency-behavior.png)

Você também pode especificar a ação a ser tomada quando os arquivos de conteúdo dos pacotes entram em conflito com os arquivos já está em seu projeto.

![Ação de conflitos de arquivo](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>A rolagem infinita

É usado para obter um pouco de comentários sobre nossa interface do usuário ter ambas as a rolagem e paradigmas de paginação ao listar os pacotes. Era muito comum ter role até a parte inferior da lista curta, clique o próximo número de página e, em seguida, role novamente. Com a nova interface do usuário, implementamos a rolagem infinita na lista de pacotes para que você precise rolar – não há mais de paginação.

![A rolagem infinita](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>Torná-lo o trabalho, torná-lo rápidos e torná-lo Pretty

Estamos felizes em obter essa nova interface do usuário-out para você experimentar. Durante essa etapa de visualização, estamos seguindo o bom princípio de "torná-lo funcionar, torná-lo mais rápido, embelezar." Nesta visualização, você conseguiu fazer mais do que primeiro objetivo – ele funciona. Nós sabemos muito rápido ainda não está, e sabemos que ele ainda não está muito bem. Relação de confiança que estaremos trabalhando essas metas entre agora e a versão RC. Nesse ínterim, adoraríamos ouvir seus comentários sobre o *usabilidade* a nova interface do usuário – a fluxos de trabalho, operações e como ele *parece* para usar a nova interface do usuário.

Há algumas funções que removemos em comparação com a interface do usuário antiga. Um deles foi intencional, e o outro é simplesmente não foi feito no tempo.

#### <a name="searching-all-package-sources"></a>Pesquisar fontes de pacote "Tudo"

A interface do usuário antigo permitia que você deve executar uma pesquisa de pacote em relação a todas as suas fontes de pacote. Removemos esse recurso na interface do usuário e nós não ser colocá-lo. Esse recurso usado para executar operações de pesquisa em relação a todas as suas fontes de pacote, reunir os resultados e tentar ordenar os resultados com base em sua seleção de classificação.

Descobrimos que a relevância de pesquisa é realmente difícil reunir. Você poderia imaginar executando uma pesquisa em relação ao Google e Bing e combinando os resultados em conjunto? Além disso, esse recurso estava lento e de fácil *acidentalmente* uso e estamos acredita que raramente era realmente úteis. Devido aos problemas o recurso introduzido, recebemos um número de relatórios de bugs nele poderia nunca foram corrigidos.

#### <a name="update-all"></a>Atualizar tudo

Costumávamos ter um botão "Atualizar tudo" na interface do usuário antigo que ainda não está lá na nova interface de usuário. Podemos será ressuscitar esse recurso para nossa versão RC.

## <a name="new-clientserver-api"></a>Novo cliente/servidor de API

Além de todos os novos recursos do nosso novo gerenciamento de pacotes da interface do usuário, também temos alguns detalhes de implementação para o protocolo de cliente/servidor do NuGet. O trabalho que fizemos é criar "V3 da API" para o NuGet, que é desenvolvido em torno de alta disponibilidade para cenários críticos como restauração de pacote e instalar pacotes. A nova API é baseada em REST e selecionou hipermídia e podemos [JSON-LD](http://json-ld.org) como nosso formato de recurso.

Os bits de visualização do NuGet 3.0, você verá uma nova origem de pacote chamada "preview.nuget.org" no menu suspenso de origem do pacote. Se você selecionar essa origem do pacote, vamos usar nossa nova API em vez disso, para se conectar ao nuget.org. Fizemos a fonte de visualização disponível na interface do usuário enquanto continuamos a testar, revisar e aprimorar a nova API. No NuGet 3.0 RC, essa nova fonte de pacote com base em v3 da API substituirá a origem do pacote com base em v2 "nuget.org".

Apesar do investimento que estamos colocando em v3 da API, fizemos todos esses novos recursos também funcionam com o protocolo de v2 nossa API existente, que significa que eles funcionarão com origens do pacote existente que não seja bem nuget.org.

## <a name="new-features-coming"></a>Novos recursos que virão

Entre agora e 3.0 RTM, também estamos trabalhando em alguns novos NuGet recursos fundamentais, além do que você vê na interface do usuário. Aqui está uma lista curta de áreas de investimento em destaque:

1. Estamos em parceria com o Visual Studio e equipes de MSBuild para obter [NuGet mais profundo na plataforma](http://blog.nuget.org/20141014/in-the-platform.html).
1. Estamos trabalhando para abandonar as convenções de pacote de instalação do tempo e em vez disso, aplique essas convenções no tempo de empacotamento com a introdução de um novo "autoritativo" [manifesto do pacote](http://blog.nuget.org/20141023/package-manifests.html).
1. Estamos trabalhando para refatorar o NuGet base de código para fazer com que os componentes cliente e servidor reutilizáveis em domínios diferentes, além do gerenciamento de pacotes no Visual Studio.
1. Estamos investigando a noção de "privadas dependências" em que um pacote pode indicar que ele tem dependências em outros pacotes para apenas os detalhes de implementação, e essas dependências não devem ser apresentadas como dependências de nível superior.

## <a name="stay-tuned"></a>Fique ligado

Por favor, fique atento [nosso blog](http://blog.nuget.org) para obter mais progresso e anúncios para NuGet 3.0!