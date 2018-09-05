---
title: Notas de versão 2.6 do NuGet
description: Notas de versão do NuGet 2.6.1 para WebMatrix, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f011a8db7ac2067a2ed7db67849d63f7dd40d1ce
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551937"
---
# <a name="nuget-26-release-notes"></a>Notas de versão 2.6 do NuGet

[Notas de versão do NuGet 2.5](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 para notas de lançamento do WebMatrix](../release-notes/nuget-2.6.1-for-webmatrix.md)

O NuGet 2.6 foi lançada em 26 de junho de 2013.

## <a name="notable-features-in-the-release"></a>Recursos importantes da versão

### <a name="support-for-visual-studio-2013"></a>Suporte para Visual Studio 2013

O NuGet 2.6 é a primeira versão que dá suporte para Visual Studio 2013. E como o Visual Studio 2012, a extensão do Gerenciador de pacotes do NuGet é incluída em todas as edições do Visual Studio.

Para fornecer o melhor suporte possível para Visual Studio 2013 e ao mesmo tempo que dão suporte a Visual Studio 2010 e o Visual Studio 2012, mantendo os tamanhos de extensão tão pequenos quanto possível, estamos desenvolvendo uma extensão separada para Visual Studio 2013, enquanto o extensão original continua direcionar o Visual Studio 2010 e 2012.

Começando com o NuGet 2.6, publicaremos duas extensões conforme mostrado a seguir:

1. [Gerenciador de pacotes NuGet](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (aplica-se ao Visual Studio 2010 e 2012)
1. [Gerenciador de pacotes do NuGet para Visual Studio 2013](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

Com essa divisão, o [nuget.org](https://nuget.org) botão de "Instalar o NuGet" da home page leva você para o [instalando NuGet](../install-nuget-client-tools.md) página, onde você pode encontrar mais informações sobre como instalar os diferentes clientes do NuGet.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>Suporte à transformação de Web. config de XDT

Um dos recursos altamente solicitados para o cliente do NuGet foi oferecer suporte a transformações mais potentes do XML usando o mecanismo de transformação XDT que é usado em transformações de configuração de build do Visual Studio.

Em abril de 2013, fizemos duas anúncios big sobre o suporte do NuGet para XDT. A primeira foi a própria biblioteca XDT estava sendo em si [lançado como um pacote do NuGet](https://nuget.org/packages/Microsoft.Web.Xdt) e [software livre no CodePlex](http://xdt.codeplex.com/). Esta etapa habilitado o mecanismo XDT a ser usado gratuitamente por outros softwares de código-fonte aberto, incluindo o cliente do NuGet. O segundo lançamento foi o plano de suporte ao uso do mecanismo de XDT para transformações no cliente do NuGet. Essa integração inclui o NuGet 2.6.

#### <a name="how-it-works"></a>Como ele funciona

Para tirar proveito do suporte XDT do NuGet, a mecânica semelhante da [recurso de transformação de config atual](../create-packages/source-and-config-file-transformations.md).
Arquivos de transformação são adicionados à pasta de conteúdo do pacote. No entanto, embora as transformações de configuração usam um único arquivo para instalação e desinstalação, transformações XDT habilita um controle refinado sobre esses dois processos usando os seguintes arquivos:

- Web.config.install.xdt
- Web.config.uninstall.xdt

Além disso, o NuGet usa o sufixo de arquivo para determinar qual mecanismo a ser executado para transformações, portanto, os pacotes usando o web.config.transforms existentes continuarão a funcionar. Transformações XDT também podem ser aplicadas a qualquer arquivo XML (não apenas Web. config), portanto, você pode aproveitar isso para outros aplicativos em seu projeto.

#### <a name="what-you-can-do-with-xdt"></a>O que você pode fazer com o XDT

Uma das vantagens de maior do XDT é sua [sintaxe simple mas poderosa](http://msdn.microsoft.com/library/dd465326.aspx) para manipular a estrutura de um DOM. XML Em vez de simplesmente sobreposição de uma estrutura de documento fixo em outra estrutura, o XDT fornece controles para correspondência de elementos em uma variedade de formas de correspondência de nomes de atributo simple para suporte XPath completo. Depois que for encontrado um elemento correspondente ou o conjunto de elementos, XDT fornece um rico conjunto de funções para manipular os elementos, se o que significa que adicionar, atualizar, ou remover os atributos, colocando um novo elemento em um local específico, ou substituir ou remover todo o elemento e seus filhos.

### <a name="machine-wide-configuration"></a>Configuração do computador

Uma das vantagens do NuGet excelentes é que ele divide um executável grande caso contrário, ou uma biblioteca em um conjunto de componentes modulares que pode ser integrada e o mais importante é mantida e com controle de versão independentemente. Um efeito colateral isso, no entanto, é que a ideia convencional de um produto ou família de produtos potencialmente se torna mais fragmentada.
Recurso de origem do pacote personalizado do NuGet fornece uma maneira de organizar pacotes; No entanto, as fontes de pacote personalizado não são detectáveis por conta própria.

A lógica para a configuração do NuGet, pesquisando a hierarquia de pastas sob o caminho % ProgramData%/NuGet/Config estende o NuGet 2.6. Instaladores de produto podem adicionar arquivos de configuração personalizados do NuGet nessa pasta para registrar uma origem de pacote personalizado para seus produtos. Além disso, a estrutura de pastas dá suporte à semântica de produto, versão e até mesmo SKU do IDE. Configurações dos seguintes diretórios são aplicadas na seguinte ordem com uma estratégia de precedência "pela última vez no wins".

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*. config
3. %ProgramData%\NuGet\Config\{IDE}\{versão}\*. config
4. %ProgramData%\NuGet\Config\{IDE}\{versão}\{SKU}\*. config

Nessa lista, o espaço reservado {IDE} é específico para o IDE em que o NuGet está em execução, portanto, no caso do Visual Studio, ele será "VisualStudio". {Version} e espaços reservados de {SKU} são fornecidos pelo IDE (por exemplo, "11.0" e "WDExpress", "VWDExpress" e "Pro", respectivamente). A pasta, em seguida, pode conter muitos arquivos diferentes de config.
Portanto, a empresa de componente ACME pode, como parte do instalador do seu produto, adicionar uma origem de pacote personalizado que serão visível somente nas versões Professional e o Ultimate do Visual Studio 2012, criando o seguinte caminho de arquivo:

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

Embora a estrutura de pastas torna fácil para programas, como instaladores de software para adicionar fontes de pacote de todo o computador a configuração do NuGet, a caixa de diálogo de configuração do NuGet também foi atualizada para permitir o registro de fontes de pacote como qualquer um dos específicas do usuário (por exemplo, registrada no % AppData%/NuGet/NuGet.Config) ou todo o computador.

Esse recurso é utilizado pelo Visual Studio 2013, em que um arquivo é instalado em:

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

Nesse arquivo, uma nova fonte de pacote chamada "Pacotes do .NET Framework" é configurada.

![Configurações de máquina de arquivo de configuração do NuGet](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Contextualizando pesquisa

Como o número de pacotes atendidas pela Galeria do NuGet continua a crescer em um ritmo exponencial, melhorando a pesquisa nunca permanece na parte superior da lista de prioridades do NuGet. Um dos recursos planejados para o NuGet é uma pesquisa contextual, que significa que o NuGet usará informações sobre a versão e SKU do Visual Studio que você está usando e o tipo de projeto que você está compilando como critérios para determinar a relevância da pesquisa potencial de resultados.

Começando com o NuGet 2.6, sempre que um pacote é instalado, o contexto para a instalação é registrado como parte dos dados da operação de instalação.  Pesquisas também enviar as mesmas informações de contexto, o que permitirão que a Galeria do NuGet melhorar os resultados da pesquisa por tendências de instalação contextuais.  Uma atualização futura para a Galeria do NuGet habilitará esse aumento de relevância sensível ao contexto.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Acompanhamento vs instala direto. Instalações de dependência

Os autores de pacote estão contando com mais de [estatísticas de pacote](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) fornecida na Galeria do NuGet.  Um ponto de dados ausentes significativos que autores pediram para é uma diferenciação entre instalações de pacote direto e instalações de dependência.  Até agora, o cliente do NuGet não enviou nenhum contexto de delimitar a operação de instalação para o desenvolvedor se diretamente o pacote instalado ou se ele foi instalado para satisfazer uma dependência.
Começando com o NuGet 2.6, que os dados agora serão enviados para a operação de instalação.  Estatísticas de pacote na Galeria do NuGet irá expor esses dados como operações de instalação separada, com um "-dependência" sufixo.

* Instalar o
* Dependência de instalação
* Atualização
* Dependência de atualização
* Reinstalar
* Dependência reinstalar

Além do nome de operação diferente, a id do pacote dependente também é registrada para a instalação.  Uma atualização futura para a Galeria do NuGet irá expor esses dados em relatórios, permitindo que os autores de pacote entender completamente como os desenvolvedores estão instalando os pacotes.

## <a name="bug-fixes"></a>Correções de Bug

O NuGet 2.6 também inclui várias correções de bugs. Para obter uma lista completa de trabalho itens corrigidos no NuGet 2.6, por favor, modo de exibição de [rastreador de problemas do NuGet para esta versão](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).