---
title: Notas de versão do NuGet 2,6
description: Notas de versão do NuGet 2.6.1 para WebMatrix, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 812a0e806e29c5a2141db4f2fbab4bf91b0983f9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776833"
---
# <a name="nuget-26-release-notes"></a>Notas de versão do NuGet 2,6

Notas de versão do [NuGet 2,5](../release-notes/nuget-2.5.md)  |  [Notas de versão do NuGet 2.6.1 para WebMatrix](../release-notes/nuget-2.6.1-for-webmatrix.md)

O NuGet 2,6 foi lançado em 26 de junho de 2013.

## <a name="notable-features-in-the-release"></a>Recursos notáveis na versão

### <a name="support-for-visual-studio-2013"></a>Suporte para Visual Studio 2013

O NuGet 2,6 é a primeira versão que fornece suporte para Visual Studio 2013. E, assim como o Visual Studio 2012, a extensão do Gerenciador de pacotes NuGet está incluída em todas as edições do Visual Studio.

Para fornecer o melhor suporte possível para Visual Studio 2013 ao mesmo tempo em que ainda oferece suporte ao Visual Studio 2010 e ao Visual Studio 2012 e manter os tamanhos de extensão o menor possível, estamos produzindo uma extensão separada para Visual Studio 2013 enquanto a extensão original continua a direcionar o Visual Studio 2010 e o 2012.

A partir do NuGet 2,6, publicaremos duas extensões como a seguir:

1. [Gerenciador de pacotes NuGet](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (aplica-se ao Visual Studio 2010 e 2012)
1. [Gerenciador de pacotes NuGet para Visual Studio 2013](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

Com essa divisão, o botão "instalar NuGet" do [nuget.org](https://nuget.org) Home Page leva você para a página [instalando o NuGet](../install-nuget-client-tools.md) , em que você pode encontrar mais informações sobre como instalar os diferentes clientes NuGet.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>Suporte à transformação de Web.config XDT

Um dos recursos mais solicitados para o cliente NuGet foi oferecer suporte a transformações XML mais poderosas usando o mecanismo de transformação XDT, que é usado em transformações de configuração de compilação do Visual Studio.

Em abril de 2013, fizemos dois anúncios grandes sobre o suporte do NuGet para XDT. A primeira era que a própria biblioteca XDT estava sendo [lançada como um pacote NuGet](https://nuget.org/packages/Microsoft.Web.Xdt) e foi [aberta com origem no CodePlex](http://xdt.codeplex.com/). Esta etapa habilitou o mecanismo XDT a ser usado livremente por outros softwares de software livre, incluindo o cliente NuGet. O segundo comunicado foi o plano para dar suporte ao uso do mecanismo XDT para transformações no cliente NuGet. O NuGet 2,6 inclui essa integração.

#### <a name="how-it-works"></a>Como ele funciona

Para aproveitar o suporte do XDT do NuGet, a mecânica é semelhante àquela do [recurso atual de transformação de configuração](../create-packages/source-and-config-file-transformations.md).
Os arquivos de transformação são adicionados à pasta de conteúdo do pacote. No entanto, enquanto as transformações de configuração usam um único arquivo para instalação e desinstalação, as transformações de XDT habilitam o controle refinado em ambos os processos usando os seguintes arquivos:

- Web.config. Install. xdt
- Web.config. Uninstall. xdt

Além disso, o NuGet usa o sufixo de arquivo para determinar qual mecanismo deve ser executado para transformações, de modo que os pacotes que usam o web.config. transformações continuarão funcionando. Transformações de XDT também podem ser aplicadas a qualquer arquivo XML (não apenas web.config), para que você possa aproveitar isso para outros aplicativos em seu projeto.

#### <a name="what-you-can-do-with-xdt"></a>O que você pode fazer com o XDT

Uma das maiores forças do XDT é sua [sintaxe simples mas poderosa](/previous-versions/aspnet/dd465326(v=vs.110)) para manipular a estrutura de um XML dom. Em vez de simplesmente sobreposição de uma estrutura de documento fixa em outra estrutura, o XDT fornece controles para correspondência de elementos de várias maneiras, desde o nome de atributo simples corresponder ao suporte total a XPath. Depois que um elemento correspondente ou conjunto de elementos é encontrado, o XDT fornece um rico conjunto de funções para manipular os elementos, se isso significa adicionar, atualizar ou remover atributos, colocar um novo elemento em um local específico ou substituir ou remover todo o elemento e seus filhos.

### <a name="machine-wide-configuration"></a>Configuração de Machine-Wide

Um dos grandes pontos fortes do NuGet é que ele divide um executável grande ou uma biblioteca em um conjunto de componentes modulares que podem ser integrados e, mais importante, mantidos e com controle de versão de forma independente. No entanto, um efeito colateral disso é que a ideia convencional de um produto ou família de produtos se torna potencialmente mais fragmentada.
O recurso de origem do pacote personalizado do NuGet fornece uma maneira de organizar pacotes; no entanto, as fontes de pacote personalizadas não são detectáveis por conta própria.

O NuGet 2,6 estende a lógica para configurar o NuGet pesquisando a hierarquia de pastas no caminho% ProgramData%/NuGet/Config. Os instaladores de produto podem adicionar arquivos de configuração personalizados do NuGet nessa pasta para registrar uma fonte de pacote personalizada para seus produtos. Além disso, a estrutura de pastas dá suporte à semântica para produto, versão e até mesmo SKU do IDE. As configurações desses diretórios são aplicadas na seguinte ordem com uma estratégia de precedência "última no WINS".

1. %ProgramData%\NuGet\Config \* . config
2. %ProgramData%\NuGet\Config \{ IDE} \* . config
3. %ProgramData%\NuGet\Config \{ IDE} \{ versão} \* . config
4. %ProgramData%\NuGet\Config \{ IDE} \{ versão} \{ SKU} \* . config

Nessa lista, o espaço reservado {IDE} é específico do IDE no qual o NuGet está em execução, portanto, no caso do Visual Studio, será "VisualStudio". Os espaços reservados {Version} e {SKU} são fornecidos pelo IDE (por exemplo, "11,0" e "WDExpress", "VWDExpress" e "pro", respectivamente). A pasta pode conter vários arquivos *. config diferentes.
Portanto, a empresa do componente ACME pode, como parte do instalador do produto, adicionar uma fonte de pacote personalizada que será visível apenas nas versões Professional e Ultimate do Visual Studio 2012 criando o seguinte caminho de arquivo:

% ProgramData% \NuGet\Config\VisualStudio\11.0\Pro\acme.config

Embora a estrutura de pastas torne simples para programas como instaladores de software adicionar fontes de pacote em todo o computador à configuração do NuGet, a caixa de diálogo de configuração do NuGet também foi atualizada para permitir o registro de origens do pacote como um usuário específico (por exemplo, registrado em% AppData%/NuGet/NuGet.Config) ou em todo o computador.

Esse recurso é utilizado por Visual Studio 2013, onde um arquivo é instalado em:

% ProgramData% \NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

Dentro desse arquivo, uma nova origem de pacote chamada "pacotes de .NET Framework" está configurada.

![Configurações amplas do computador do arquivo de configuração do NuGet](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Contextualização de pesquisa

Como o número de pacotes atendidos pela galeria do NuGet continua crescendo em um ritmo exponencial, melhorar a pesquisa permanece na parte superior da lista de prioridade do NuGet. Um dos recursos planejados para o NuGet é a pesquisa contextual, o que significa que o NuGet usará informações sobre a versão e o SKU do Visual Studio que você está usando e o tipo de projeto que você está criando como critérios para determinar a relevância de possíveis resultados da pesquisa.

A partir do NuGet 2,6, cada vez que um pacote é instalado, o contexto para a instalação é registrado como parte dos dados da operação de instalação.  As pesquisas também enviam as mesmas informações de contexto, o que permitirá que a galeria do NuGet aumente os resultados da pesquisa por tendências de instalação contextuais.  Uma atualização futura da galeria do NuGet permitirá esse aumento de relevância sensível ao contexto.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Rastreamento de instalações diretas versus instalações de dependência

Os autores de pacote estão confiando mais e mais nas [Estatísticas de pacote](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) fornecidas na galeria do NuGet.  Um ponto de dados ausente significativo que os autores solicitaram é uma diferenciação entre instalações de pacotes diretas e instalações de dependências.  Até agora, o cliente NuGet não enviou nenhum contexto em relação à operação de instalação para se o desenvolvedor instalasse o pacote diretamente ou se foi instalado para atender a uma dependência.
A partir do NuGet 2,6, esses dados agora serão enviados para a operação de instalação.  As estatísticas de pacote na galeria do NuGet vão expor esses dados como operações de instalação separadas, com um sufixo "-Dependency".

* Instalar
* Install-Dependency
* Atualizar
* Update-Dependency
* Reinstalar
* Reinstall-Dependency

Além do nome da operação diferente, a ID do pacote dependente também é registrada para a instalação.  Uma atualização futura da galeria do NuGet irá expor esses dados em relatórios, permitindo que os autores de pacotes entendam totalmente como os desenvolvedores estão instalando seus pacotes.

## <a name="bug-fixes"></a>Correções de bugs

O NuGet 2,6 também inclui várias correções de bugs. Para obter uma lista completa de itens de trabalho corrigidos no NuGet 2,6, consulte o [rastreador de problemas do NuGet para esta versão](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).