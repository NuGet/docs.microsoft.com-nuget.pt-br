---
title: Notas de versão 2.6 do NuGet
description: Notas de versão do NuGet 2.6.1 para o WebMatrix, incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39ce6ac3d36464d26966b0dabb0893f09ad4afdc
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821896"
---
# <a name="nuget-26-release-notes"></a>Notas de versão 2.6 do NuGet

[Notas de versão do NuGet 2.5](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 para notas de versão do WebMatrix](../release-notes/nuget-2.6.1-for-webmatrix.md)

2.6 NuGet foi lançado em 26 de junho de 2013.

## <a name="notable-features-in-the-release"></a>Recursos importantes da versão

### <a name="support-for-visual-studio-2013"></a>Suporte para Visual Studio 2013

2.6 do NuGet é a primeira versão que oferece suporte ao Visual Studio 2013. E como o Visual Studio 2012, a extensão do NuGet Package Manager está incluída em todas as edições do Visual Studio.

Para fornecer o melhor suporte possível para Visual Studio 2013 e ao mesmo tempo com suporte Visual Studio 2010 e o Visual Studio 2012, mantendo os tamanhos de extensão tão pequenos quanto possível, estamos desenvolvendo uma extensão separada para Visual Studio 2013 enquanto o extensão original continua direcionar o Visual Studio 2010 e 2012.

A partir do NuGet 2.6, publicaremos duas extensões como abaixo:

1. [O NuGet Package Manager](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (aplica-se ao Visual Studio 2010 e 2012)
1. [Gerenciador de pacotes do NuGet para Visual Studio 2013](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

Com essa divisão, o [nuget.org](https://nuget.org) botão de "Instalar o NuGet" da home page leva você para a [instalando NuGet](../install-nuget-client-tools.md) página, onde você pode encontrar mais informações sobre como instalar os clientes do NuGet diferentes.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>Suporte a transformações XDT Web. config

Um dos recursos altamente solicitado para o cliente do NuGet foi oferecer suporte a mais potentes transformações XML usando o mecanismo de transformação XDT que é usado em transformações de configuração de compilação do Visual Studio.

Em abril de 2013, fizemos duas anúncios grandes sobre o suporte do NuGet para XDT. A primeira foi da própria biblioteca XDT estava sendo próprio [lançada como um pacote do NuGet](https://nuget.org/packages/Microsoft.Web.Xdt) e [abrir originado no CodePlex](http://xdt.codeplex.com/). Esta etapa habilitado o mecanismo XDT a ser usado livremente por outro software de código-fonte aberto, incluindo o cliente do NuGet. O segundo lançamento foi o plano de suporte ao uso do mecanismo XDT para transformações no cliente do NuGet. 2.6 NuGet inclui essa integração.

#### <a name="how-it-works"></a>Como ele funciona

Para aproveitar o suporte do NuGet XDT, a mecânica semelhante do [recurso de transformação de configuração atual](../create-packages/source-and-config-file-transformations.md).
Arquivos de transformação são adicionados à pasta de conteúdo do pacote. No entanto, enquanto as transformações de configuração usarem um único arquivo de instalação e desinstalação, transformações XDT habilitam controle refinado de ambos os processos usando os seguintes arquivos:

- Web.config.install.xdt
- Web.config.uninstall.xdt

Além disso, o NuGet usa o sufixo de arquivo para determinar qual mecanismo de execução para transformações, para que pacotes usando o web.config.transforms existentes continuarão a funcionar. Transformações XDT também podem ser aplicadas a qualquer arquivo XML (não apenas Web. config), portanto você pode aproveitar isso para outros aplicativos em seu projeto.

#### <a name="what-you-can-do-with-xdt"></a>O que você pode fazer com XDT

Um dos pontos mais fortes do XDT é seu [sintaxe simple mas poderosa](http://msdn.microsoft.com/library/dd465326.aspx) para manipular a estrutura de um DOM. XML Em vez de simplesmente sobrepondo uma estrutura de documento fixo para outra estrutura, XDT fornece controles para correspondência de elementos em uma variedade de formas de correspondência de nomes de atributo simples para XPath suporte completo. Depois que for encontrado um elemento correspondente ou o conjunto de elementos, XDT fornece um conjunto avançado de funções para manipular os elementos, seja para adicionar, atualizar, ou removendo atributos, colocando um novo elemento em um local específico, ou substituir ou remover todo o elemento e seus filhos.

### <a name="machine-wide-configuration"></a>Configuração de máquina

Um dos excelentes pontos fortes do NuGet é que ele divide um executável caso contrário, grande ou a biblioteca em um conjunto de componentes modulares que pode ser integrado e o mais importante é mantida e com controle de versão independente. Um efeito colateral disto, no entanto, é que a ideia convencional de um produto ou a família de produtos potencialmente se torna mais fragmentada.
Recurso de origem de pacote personalizado do NuGet fornece uma maneira de organizar os pacotes. No entanto, as fontes de pacote personalizado não são detectáveis por conta própria.

2.6 NuGet estende a lógica de configuração NuGet pesquisando a hierarquia de pastas sob o caminho % ProgramData%/NuGet/Config. Instaladores de produto podem adicionar arquivos de configuração personalizados do NuGet nesta pasta para registrar uma origem de pacote personalizado para seus produtos. Além disso, a estrutura de pasta dá suporte à semântica de produto, versão e até mesmo SKU do IDE. Configurações dos seguintes diretórios são aplicadas na seguinte ordem com uma estratégia de precedência "última no wins".

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*. config
3. %ProgramData%\NuGet\Config\{IDE}\{versão}\*. config
4. %ProgramData%\NuGet\Config\{IDE}\{versão}\{SKU}\*. config

Nessa lista, o espaço reservado {IDE} é específico para o IDE no qual está executando o NuGet, portanto no caso do Visual Studio, ele será "VisualStudio". {Version} e espaços reservados de {SKU} (por exemplo, são fornecidos pelo IDE "11.0" e "WDExpress", "VWDExpress" e "Pro", respectivamente). A pasta, em seguida, pode conter muitos arquivos diferentes de config.
Portanto, a empresa de componente ACME pode, como parte do instalador de seu produto, adicionar uma origem de pacote personalizado que serão visível somente nas versões Professional e Ultimate do Visual Studio 2012, criando o seguinte caminho de arquivo:

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

Enquanto a estrutura de pasta facilita para os programas como instaladores de software para adicionar fontes de pacote de máquina a configuração do NuGet, a caixa de diálogo de configuração NuGet também foi atualizada para permitir o registro de fontes de pacote como qualquer específicas do usuário (por exemplo, registrada em % AppData%/NuGet/NuGet.Config) ou todo o computador.

Esse recurso é utilizado pelo Visual Studio 2013, onde um arquivo é instalado em:

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

Nesse arquivo, uma nova origem do pacote chamada ".NET Framework pacotes" está configurada.

![Configurações de arquivo de configuração NuGet máquina](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Pesquisa de contexto

Como o número de pacotes servidas por Galeria NuGet continua a crescer em um ritmo exponencial, melhorando a pesquisa permanece constante na parte superior da lista de prioridades NuGet. Um dos recursos planejados do NuGet é uma pesquisa contextual, que significa que o NuGet usará informações sobre a versão e SKU do Visual Studio que você está usando e o tipo de projeto que você está criando como critérios para determinar a relevância da pesquisa potencial resultados.

A partir do NuGet 2.6, sempre que um pacote é instalado, o contexto para a instalação é registrado como parte dos dados da operação de instalação.  Pesquisas também enviar as mesmas informações de contexto, o que permitirá que a Galeria do NuGet melhorar os resultados da pesquisa por tendências de instalação contextuais.  Uma atualização futura para a Galeria NuGet permite que esse aumento de relevância sensível ao contexto.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Controle direto instala vs. Instalações de dependência

Os autores de pacote depender mais o [estatísticas de pacote](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) fornecida na Galeria do NuGet.  Uma quantidade significativa de dados ausente do ponto que os autores pediram para é uma diferenciação entre instalações de pacote direto e instalações de dependência.  Até agora, o cliente do NuGet não enviou qualquer contexto pela operação de instalação para o desenvolvedor se diretamente o pacote instalado ou se ele foi instalado para satisfazer uma dependência.
Iniciando com o NuGet 2.6, que dados agora serão enviados para a operação de instalação.  Estatísticas de pacote na Galeria do NuGet irá expor esses dados como operações de instalação separado, com um "-dependência" sufixo.

* Instalar o
* Dependência de instalação
* Atualização
* Dependência de atualização
* Reinstalar
* Dependência reinstalar

Além do nome de operação diferente, a id de pacote dependente também é registrada para a instalação.  Uma atualização futura para a Galeria NuGet irá expor esses dados em relatórios, permitindo que os autores de pacote entender como os desenvolvedores estão instalando seus pacotes.

## <a name="bug-fixes"></a>Correções de Bug

2.6 NuGet também inclui várias correções de bug. Para obter uma lista completa de trabalho itens corrigidos na versão 2.6 do NuGet,. exibição o [NuGet Issue Tracker para esta versão](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).