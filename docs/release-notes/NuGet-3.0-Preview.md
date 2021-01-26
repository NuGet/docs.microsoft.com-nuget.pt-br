---
title: Notas de versão de visualização do NuGet 3,0
description: Notas de versão do NuGet 3,0 Preview, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ecaed21c5e689a488e033404f8042cd1f17eed0d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780330"
---
# <a name="nuget-30-preview-release-notes"></a>Notas de versão de visualização do NuGet 3,0

Notas de versão do [NuGet 2,9 RC](../release-notes/nuget-2.9-rc.md)  |  [Notas de versão do NuGet 3,0 beta](../release-notes/nuget-3.0-beta.md)

O NuGet 3,0 Preview foi lançado em 12 de novembro de 2014 como parte da versão de visualização do Visual Studio 2015. Lançamos o NuGet 3,0 Preview. Esse é um grande lançamento para nós (embora seja uma versão prévia) e estamos empolgados em começar a obter comentários sobre nossas alterações.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Essa versão prévia do NuGet 3,0 está incluída no Visual Studio 2015 Preview. Estamos trabalhando para obter uma visualização descartada para o Visual Studio 2012 e Visual Studio 2013 muito em breve. Anteriormente, compartilhamos nossa intenção de [descontinuar as atualizações para o Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), e fizemos essa decisão difícil.

## <a name="brand-new-ui"></a>Interface do usuário totalmente nova

A primeira coisa que você observa sobre o NuGet 3,0 Preview é nossa interface do usuário totalmente nova. Não é mais uma caixa de diálogo modal; Agora é uma janela de documento completa do Visual Studio. Isso permite que você abra a interface do usuário para vários projetos (e/ou a solução) ao mesmo tempo, recorte a janela para outro monitor, encaixe-a, mas você gostaria, etc.

![A nova interface do usuário do NuGet](./media/NuGet-3.0-Preview/new-ui.png)

Além das diferenças de usabilidade devido ao abandono da caixa de diálogo modal, também temos vários novos recursos na nova interface do usuário.

### <a name="version-selection"></a>Seleção de versão

Talvez o recurso mais solicitado da interface do usuário seja permitir a seleção de versão para instalação e atualização do pacote--já está disponível.

![Seleção de versão do pacote](./media/NuGet-3.0-Preview/version-selection.png)

Se você estiver instalando ou atualizando um pacote, a lista suspensa versão permitirá que você veja todas as versões disponíveis para o pacote, com algumas versões notáveis promovidas para a parte superior da lista para facilitar a seleção. Você não precisa mais usar o console do PowerShell para obter versões específicas que não são as mais recentes.

### <a name="combined-installedonlineupdates-workflows"></a>Fluxos de trabalho instalados/online/atualizações combinados

Nossa interface do usuário anterior tinha três guias para instalação, online e atualizações. Os pacotes listados eram específicos para esses fluxos de trabalho e as ações disponíveis também eram específicas para os fluxos de trabalho. Embora isso parecia lógico, soubemos que muitos de vocês costumavam ser arredondados por essa separação.

Agora temos uma experiência combinada, na qual você pode instalar, atualizar ou desinstalar um pacote, independentemente de como o pacote foi selecionado. Para ajudar com os fluxos de trabalho específicos, agora temos um menu suspenso de filtro que permite filtrar os pacotes visíveis, mas as ações disponíveis para o pacote são consistentes.

![Desinstalar um pacote](./media/NuGet-3.0-Preview/uninstall-package.png)

Usando o filtro "instalado", você pode ver facilmente seus pacotes instalados, quais têm atualizações disponíveis e, em seguida, pode desinstalar ou atualizar o pacote alterando a seleção de versão para ver a alteração da ação disponível.

![Atualizar um pacote](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>Consolidação de versão

É comum ter o mesmo pacote instalado em vários projetos dentro de sua solução. Às vezes, as versões instaladas em cada projeto podem se separar e é necessário consolidar as versões em uso. A visualização do NuGet 3,0 apresenta um novo recurso apenas para esse cenário.

A janela Gerenciamento de pacotes de nível de solução pode ser acessada clicando com o botão direito do mouse na solução e escolhendo gerenciar pacotes NuGet para solução. A partir daí, se você selecionar um pacote que é instalado em vários projetos, mas com versões diferentes em uso, uma nova ação "consolidar" ficará disponível. Na captura de tela abaixo, o `Newtonsoft.Json` foi instalado na `SamplesClassLibrary` versão com `6.0.4` e foi instalado no `SamplesConsoleApp` com a versão `5.0.4` .

![Consolidar versões](./media/NuGet-3.0-Preview/consolidate.png)

Este é o fluxo de trabalho para consolidação em uma única versão.

1. Selecione o `Newtonsoft.Json` pacote na lista
1. Escolha `Consolidate` na `Action` lista suspensa
1. Use a `Version` lista suspensa para selecionar a versão na qual será consolidada
1. Marque as caixas dos projetos que devem ser consolidados nessa versão (Observe que os projetos que já estão na versão selecionada ficarão esmaecidos)
1. Clique no `Consolidate` botão para executar a consolidação

### <a name="operation-previews"></a>Visualizações de operação

Independentemente da operação que você está executando, Instale/atualize/desinstale--a nova interface do usuário agora oferece uma maneira de visualizar as alterações que serão feitas em seu projeto. Essa visualização mostrará os novos pacotes que serão instalados, os pacotes que serão atualizados e os pacotes que serão desinstalados, juntamente com os pacotes que serão inalterados durante a operação.

No exemplo a seguir, podemos ver que a instalação do Microsoft. AspNet. Signalr resultará em algumas alterações no projeto.

![Visualizar instalando o Signalr](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>Opções de instalação

Usando o console do PowerShell, você tinha controle sobre algumas opções de instalação notáveis. Agora, colocamos esses recursos na interface do usuário. Agora você pode controlar o comportamento da resolução de dependências de como as versões das dependências são selecionadas.

![Comportamento de dependência](./media/NuGet-3.0-Preview/dependency-behavior.png)

Você também pode especificar a ação a ser tomada quando os arquivos de conteúdo de pacotes entram em conflito com os arquivos que já estão em seu projeto.

![Ação de conflito de arquivo](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>Rolagem infinita

Nós usamos um pouco de comentários sobre nossa interface do usuário tendo os paradigmas de rolagem e de paginação ao listar pacotes. Era muito comum ter de rolar para a parte inferior da lista curta, clicar no número da próxima página e, em seguida, rolar novamente. Com a nova interface do usuário, implementamos a rolagem infinita na lista de pacotes para que você só precise rolar, sem mais paginação.

![Rolagem infinita](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>Fazê-lo funcionar, torná-lo rápido, torná-lo muito bom

Estamos empolgados para obter essa nova interface do usuário para você experimentar. Durante essa etapa de visualização, estamos seguindo os bons adágio de "fazer tudo funcionar, torná-lo mais rápido, deixá-lo bem". Nesta versão prévia, atingimos a maior parte desse primeiro objetivo... ele funciona. Sabemos que isso ainda não é muito rápido, e sabemos que ainda não é muito bem. Confie que vamos trabalhar nessas metas entre agora e a versão RC. Enquanto isso, adoraríamos ouvir seus comentários sobre a *usabilidade* da nova interface do usuário – os fluxos de trabalho, operações e como se *sente* usar a nova interface do usuário.

Há algumas funções que removemos quando comparadas à interface do usuário antiga. Uma delas era intencional e a outra simplesmente não foi feita no tempo.

#### <a name="searching-all-package-sources"></a>Pesquisando "todos" fontes de pacote

A interface do usuário antiga permitia que você executasse uma pesquisa de pacote em todas as suas origens de pacote. Removemos esse recurso na interface do usuário e não vamos colocá-lo de volta. Esse recurso costumava executar operações de pesquisa em todas as suas origens de pacote, religar os resultados e tentar ordenar os resultados com base na seleção de classificação.

Descobrimos que a relevância da pesquisa é realmente difícil de ser reunida. Você poderia imaginar a execução de uma pesquisa no Google e no Bing e combinando os resultados juntos? Além disso, esse recurso era lento, fácil de usar *acidentalmente* e acreditamos que raramente era útil. Devido aos problemas que o recurso apresentou, recebemos vários relatórios de bugs que nunca podiam ser corrigidos.

#### <a name="update-all"></a>Atualizar Tudo

Usamos um botão "atualizar tudo" na interface do usuário antiga que ainda não existe na nova interface do usuário. Vamos ressuscitar esse recurso para a versão RC.

## <a name="new-clientserver-api"></a>Nova API de cliente/servidor

Além de todos os novos recursos em nossa nova interface do usuário de gerenciamento de pacotes, também estamos trabalhando em alguns detalhes de implementação para o protocolo cliente/servidor do NuGet. O trabalho que fizemos é criar a "API v3" para o NuGet, que foi projetado em relação à alta disponibilidade para cenários críticos, como a restauração de pacotes e a instalação de pacotes. A nova API é baseada em REST e hipermídia e selecionamos [JSON-LD](http://json-ld.org) como nosso formato de recurso.

Nos bits de visualização do NuGet 3,0, você verá uma nova origem do pacote chamada "preview.nuget.org" na lista suspensa de origem do pacote. Se você selecionar essa origem do pacote, usaremos nossa nova API em vez de conectar-se ao nuget.org. Disponibilizamos a fonte de visualização na interface do usuário enquanto continuamos testando, revisamos e aperfeiçoamos a nova API. No NuGet 3,0 RC, essa nova fonte de pacote baseada na API v3 substituirá a origem do pacote "nuget.org" baseado em v2.

Apesar do investimento que estamos colocando na API v3, fizemos todos esses novos recursos também funcionam com nosso protocolo de API v2 existente, o que significa que eles funcionarão com fontes de pacote existentes além de nuget.org.

## <a name="new-features-coming"></a>Novos recursos chegando

Entre agora e 3,0 RTM, também estamos trabalhando em alguns dos novos recursos fundamentais do NuGet, além do que você vê na interface do usuário. Aqui está uma pequena lista de áreas de investimento evidentes:

1. Estamos fazendo uma parceria com as equipes do Visual Studio e do MSBuild para obter [o NuGet mais profundo na plataforma](http://blog.nuget.org/20141014/in-the-platform.html).
1. Estamos trabalhando para abandonar as convenções de pacote de tempo de instalação e, em vez disso, aplicar essas convenções no momento do empacotamento, introduzindo um novo [manifesto de pacote](http://blog.nuget.org/20141023/package-manifests.html)"autoritativo".
1. Estamos trabalhando para refatorar a base de código NuGet para tornar os componentes do cliente e do servidor reutilizáveis em diferentes domínios além do gerenciamento de pacotes no Visual Studio.
1. Estamos investigando a noção de "dependências privadas", em que um pacote pode indicar que tem dependências em outros pacotes apenas para detalhes de implementação, e essas dependências não devem ser apresentadas como dependências de nível superior.

## <a name="stay-tuned"></a>Fique atento

Fique atento ao [nosso blog](http://blog.nuget.org) para obter mais progresso e anúncios para o NuGet 3,0!