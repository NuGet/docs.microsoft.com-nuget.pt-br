---
title: O que é o NuGet e o que ele faz?
description: Uma introdução abrangente sobre o que o NuGet é e o que ele faz
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/10/2018
ms.topic: overview
ms.openlocfilehash: 7237db8f3be3d9a1d46b9e6be41bff5c06593a20
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="an-introduction-to-nuget"></a>Uma introdução ao NuGet

Uma ferramenta essencial para qualquer plataforma de desenvolvimento moderna é um mecanismo por meio do qual os desenvolvedores podem criar, compartilhar e consumir código útil. Geralmente, esse código é fornecido em "pacotes" que contêm código compilado (como DLLs) juntamente com outro conteúdo necessário nos projetos que consomem esses pacotes.

Para .NET (incluindo .NET Core), o mecanismo com suporte da Microsoft para compartilhar código é **NuGet**, que define como os pacotes .NET são criados, hospedados e consumidos e fornece as ferramentas para cada uma dessas funções.

Em suma, um pacote do NuGet é um arquivo ZIP com a extensão `.nupkg` que contém o código compilado (DLLs), outros arquivos relacionados a esse código e um manifesto descritivo que inclui informações como o número de versão do pacote. Os desenvolvedores com código para compartilhar criam pacotes e os publicam em um host público ou privado. Os consumidores de pacote obtêm esses pacotes de hosts adequados, os adicionam aos seus projetos e chamam a funcionalidade de um pacote no código do projeto. Em seguida, o próprio NuGet manipula todos os detalhes de intermediários.

Como o NuGet oferece suporte a hosts privados junto com o host público nuget.org, é possível usar pacotes NuGet para compartilhar código exclusivo a uma organização ou a um grupo de trabalho. Você também pode usar os pacotes NuGet como uma forma conveniente de levar em consideração seu próprio código para uso em nada além de seus próprios projetos. Em resumo, um pacote NuGet é uma unidade compartilhável de código, mas não exige nem implica qualquer meio específico de compartilhamento.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>O fluxo de pacotes entre criadores, hosts e clientes

Em sua função como host público, o próprio NuGet mantém o repositório central de mais de 100.000 pacotes exclusivos em [nuget.org](https://www.nuget.org). Esses pacotes são utilizados por milhões de desenvolvedores de .NET/.NET Core diariamente. O NuGet também permite hospedar pacotes em particular na nuvem (como no Visual Studio Team Services), em uma rede privada ou até mesmo apenas em seu sistema de arquivos local. Ao fazer isso, esses pacotes ficam disponíveis apenas aos desenvolvedores que têm acesso ao host, fornecendo a capacidade de tornar os pacotes disponíveis a um grupo específico de consumidores. As opções são explicadas em [Hospedando seus próprios feeds do NuGet](hosting-packages/overview.md). Por meio de opções de configuração, você também pode controlar exatamente quais hosts podem ser acessados por um determinado computador, garantindo assim que os pacotes sejam obtidos de fontes específicas, em vez de um repositório público como nuget.org.

Qualquer seja sua natureza, um host que serve como o ponto de conexão entre os *criadores* e os *consumidores* do pacote. Os criadores compilam pacotes do NuGet úteis e os publicam em um host. Os consumidores pesquisam então por pacotes úteis e compatíveis em hosts acessíveis, baixando e incluindo esses pacotes em seus projetos. Depois de instalado em um projeto, as APIs dos pacotes estão disponíveis para o restante do código do projeto.

![Relação entre os criadores de pacote, hosts de pacote e consumidores de pacote](media/nuget-roles.png)

## <a name="package-targeting-compatibility"></a>Compatibilidade de direcionamento do pacote

Um pacote “compatível” significa que ele contém os assemblies criados para pelo menos um .NET framework de destino que seja compatível com a estrutura de destino do projeto consumidor. Os desenvolvedores podem criar pacotes específicos a uma estrutura, assim como acontece com os controles UWP, ou podem dar suporte a uma grande variedade de destinos. Para maximizar a compatibilidade de um pacote, os desenvolvedores direcionam para [.NET Standard](/dotnet/standard/net-standard), que todos os projetos do .NET e .NET Core podem consumir. Esse é o meio mais eficiente para criadores e consumidores, pois um único pacote (geralmente contendo um único assembly) funciona para todos os projetos de consumo.

Por outro lado, os desenvolvedores de pacote que precisam de APIs fora do .NET Standard, criam assemblies separados para as estruturas de destino diferentes para as quais desejam dar suporte e incluem todos os assemblies no mesmo pacote (que é chamado de "multidirecionamento"). Quando um consumidor instalado um pacote como esse, o NuGet extrai apenas os assemblies que são necessárias para o projeto. Isso minimiza a superfície do pacote no aplicativo final e/ou assemblies produzidos pelo projeto. Um pacote multidirecionamento é, obviamente, mais difícil para o criador manter.

> [!Note]
> O direcionamento para .NET Standard substitui a abordagem anterior de usar vários destinos de bibliotecas de classes portáteis (PCL). Portanto, esta documentação se concentra na criação de pacotes para .NET Standard.

## <a name="nuget-tools"></a>Ferramentas do NuGet

Além da compatibilidade com a hospedagem, o NuGet também fornece uma variedade de ferramentas usadas por criadores e por consumidores. Veja [Instalar as ferramentas de cliente do NuGet](install-nuget-client-tools.md) para saber como obter ferramentas específicas.

| Ferramenta | Plataformas | Cenários Aplicáveis | Descrição |
| --- | --- | --- | --- |
| [CLI do nuget.exe](tools/nuget-exe-cli-reference.md) | Todos | Criação, Consumo | Fornece todos os recursos do NuGet, com alguns comandos de que aplicam especificamente aos criadores de pacote, alguns somente aos consumidores e outros a ambos. Por exemplo, os criadores de pacote usam o comando `nuget pack` para criar um pacote de vários assemblies e arquivos relacionados, os consumidores de pacote usam `nuget install` para incluir pacotes em uma pasta do projeto e todos usam `nuget config` para definir as variáveis de configuração do NuGet. Como uma ferramenta independente de plataforma, a CLI do NuGet não interage com projetos do Visual Studio. |
| [CLI do dotnet](tools/dotnet-Commands.md) | Todos | Criação, Consumo | Fornece certas funcionalidades da CLI do NuGet diretamente na cadeia de ferramentas do .NET Core. Assim como ocorre com a CLI do NuGet, a CLI do dotnet não interage com projetos do Visual Studio. |
| [Console do gerenciador de pacotes](tools/package-manager-console.md) | Visual Studio no Windows | Consumo | Fornece [comandos do PowerShell](tools/Powershell-Reference.md) para instalar e gerenciar pacotes em projetos do Visual Studio. |
| [Interface do usuário do Gerenciador de Pacotes](tools/package-manager-ui.md) | Visual Studio no Windows | Consumo | Fornece uma IU fácil de usar para instalar e gerenciar pacotes em projetos do Visual Studio. |
| [Gerenciar a interface do usuário do NuGet](/visualstudio/mac/nuget-walkthrough) | Visual Studio para Mac | Consumo | Fornece uma IU fácil de usar para instalar e gerenciar pacotes em projetos do Visual Studio para Mac. |
| [MSBuild](reference/msbuild-targets.md) | Windows | Criação, Consumo | Fornece a capacidade de criar e restaurar os pacotes usados em um projeto diretamente por meio da cadeia de ferramentas do MSBuild. |

Como você pode ver, as ferramentas do NuGet com as quais você trabalha dependem muito se você está criando ou consumindo pacotes, e a plataforma de trabalho na qual você está trabalhando. Os criadores de pacotes normalmente também são consumidores, pois eles aproveitam funcionalidades que existe em outros pacotes do NuGet. E, é claro, esses pacotes podem, por sua vez, depender de outros.

Para saber mais, comece com os artigos [Fluxo de trabalho de criação de pacote](create-packages/Overview-and-Workflow.md) e [Fluxo de trabalho de consumo de pacote](consume-packages/Overview-and-Workflow.md).

## <a name="managing-dependencies"></a>Gerenciamento de dependências

A capacidade de aproveitar facilmente o trabalho de outras pessoas é um dos recursos mais poderosos de um sistema de gerenciamento de pacotes. Da mesma forma, grande parte do que o NuGet faz é gerenciar essa árvore de dependência ou “grafo” em nome de um projeto. Em poucas palavras, você precisa apenas se preocupar com os pacotes que você está usando diretamente em um projeto. Se algum desses pacotes consumir outros pacotes (o que pode, por sua vez, consumir ainda mais), o NuGet cuidará de todas essas dependências de nível inferior.

A imagem a seguir mostra um projeto que depende de cinco pacotes, que por sua vez dependem de muitos outros.

![Um grafo de dependência NuGet de exemplo para um projeto do .NET](media/dependency-graph.png)

Observe que alguns pacotes aparecem várias vezes no grafo de dependência. Por exemplo, há três consumidores diferentes do pacote B e cada consumidor também pode especificar uma versão diferente do pacote (não mostrado). Isso é uma ocorrência comum, especialmente para pacotes amplamente usados. Felizmente, o NuGet faz o trabalho duro para determinar exatamente qual versão do Pacote B atende a todos os consumidores. Em seguida, o NuGet faz o mesmo para todos os outros pacotes, independente da profundidade do grafo de dependência.

Para obter mais detalhes sobre como o NuGet executa esse serviço, consulte [Resolução de dependência](consume-packages/dependency-resolution.md).

## <a name="tracking-references-and-restoring-packages"></a>Rastreando referências e restaurando pacotes

Como projetos podem ser movidos facilmente entre os computadores de desenvolvedor, repositórios de controle do código-fonte, servidores de build e assim por diante, é altamente impraticável manter assemblies binários dos pacotes do NuGet diretamente associados a um projeto. Isso tornaria cada cópia do projeto desnecessariamente sobrecarregada (e, assim, desperdiçaria espaço em repositórios de controle do código-fonte). Também dificultaria muito a atualização de binários de pacote para versões mais recentes, pois as atualizações precisariam ser aplicadas em todas as cópias do projeto.

Em vez disso, o NuGet mantém uma lista de referências simples dos pacotes dos quais um projeto depende, incluindo dependências de nível superior e inferior. Ou seja, sempre que você instala um pacote de algum host em um projeto, o NuGet registra o identificador de pacote e o número de versão nesta lista de referência. (Desinstalar um pacote, é claro, remove-o da lista.) O NuGet, em seguida, fornece um meio para restaurar todos os pacotes referenciados mediante solicitação, conforme descrito em [Restauração do pacote](consume-packages/package-restore.md).

![Uma lista de referências de NuGet é criada na instalação do pacote e pode ser usada para restaurar os pacotes em outro lugar](media/nuget-restore.png)

Com apenas a lista de referência, o NuGet pode, então, reinstalar&mdash;ou seja, *restaurar*&mdash;todos os pacotes de hosts públicos e/ou privados a qualquer momento posteriormente. Ao confirmar um projeto no controle do código-fonte ou compartilhá-lo de alguma outra forma, você inclui apenas a lista de referências e exclui os binários do pacote (veja [Pacotes e controle do código-fonte](consume-packages/packages-and-source-control.md).)

O computador que recebe um projeto, como um servidor de build obtendo uma cópia do projeto como parte de um sistema de implantação automatizada, simplesmente pede ao NuGet para restaurar as dependências sempre que necessário. Sistemas de build como o Visual Studio Team Services fornecem etapas de “restauração do NuGet” para essa finalidade exata. Da mesma forma, quando os desenvolvedores obtêm uma cópia de um projeto (por exemplo, ao clonar um repositório), eles podem invocar um comando como `nuget restore` (CLI do NuGet), `dotnet restore` (CLI do dotnet) ou `Install-Package` (Console do Gerenciador de Pacotes) para obter todos os pacotes necessários. O Visual Studio, por sua vez, restaura automaticamente os pacotes ao compilar um projeto (contanto que a restauração automática esteja ativada, conforme descrito em [Restauração de pacote](consume-packages/package-restore.md)).

Claramente, a função primária do NuGet, no que diz respeito aos desenvolvedores, é manter essa lista de referência em nome do seu projeto e fornecer os meios para restaurar (e atualizar) com eficiência os pacotes referenciados. Essa lista é mantida em um dos dois *formatos de gerenciamento de pacote*, como são chamados:

- [`packages.config`](reference/packages-config.md): *(NuGet 1.0 ou superior)* Como um arquivo XML que mantém uma lista simples de todas as dependências do projeto, incluindo as dependências de outros pacotes instalados. Os pacotes instalados ou restaurados são armazenados em uma pasta `packages`.

- [PackageReference](consume-packages/package-references-in-project-files.md) (ou "referências de pacote em arquivos de projeto") |*(NuGet 4.0 ou superior)* Mantém uma lista de dependências de nível superior do projeto diretamente no arquivo de projeto, portanto, nenhum arquivo separado é necessário. Um arquivo associado, `obj/project.assets.json`, é gerado dinamicamente para gerenciar o grafo de dependência geral dos pacotes que um projeto usa juntamente com todas as dependências de nível inferior. PackageReference é sempre usado por projetos do .NET Core.

Qual formato de gerenciamento de pacotes é aplicado a um projeto depende do tipo de projeto e a versão disponível do NuGet (e/ou Visual Studio). Para verificar qual formato está sendo usado, simplesmente procure por `packages.config` na raiz do projeto depois de instalar o primeiro pacote. Se você não tiver esse arquivo, procure no arquivo de projeto diretamente por um elemento \<PackageReference\>.

Quando você tiver escolha, será recomendável usar PackageReference. `packages.config` é mantido para fins de legado e não está mais em desenvolvimento ativo.

> [!Tip]
> Vários comandos da CLI do `nuget.exe`, como `nuget install`, não adicionam o pacote automaticamente à lista de referências. A lista é atualizada durante a instalação de um pacote com o Gerenciador de Pacotes do Visual Studio (interface do usuário ou Console) e com a CLI `dotnet.exe`.

## <a name="what-else-does-nuget-do"></a>O que mais o NuGet faz?

Até agora, você aprendeu as seguintes características do NuGet:

- O NuGet fornece o repositório central nuget.org com suporte para a hospedagem privada.
- O NuGet fornece as ferramentas que os desenvolvedores precisam para criar, publicar e consumir pacotes.
- Mais importante, o NuGet mantém uma lista de referência de pacotes usados em um projeto e a capacidade de restaurar e atualizar esses pacotes da lista.

Para fazer com que esses processos funcionem com eficiência, o NuGet realiza algumas otimizações nos bastidores. Particularmente, o NuGet gerencia um cache de pacote e uma pasta de pacotes globais para abreviar a instalação e a reinstalação. O cache evita o download de um pacote já instalado no computador. A pasta de pacotes globais permite que vários projetos compartilhem o mesmo pacote instalado, reduzindo, assim, a superfície geral do NuGet no computador. As pastas de cache e de pacotes globais também são muito úteis quando você restaura com frequência um grande número de pacotes, como em um servidor de build. Para obter mais detalhes sobre esses mecanismos, confira [Como gerenciar as pastas de pacotes globais e de cache](consume-packages/managing-the-global-packages-and-cache-folders.md).

Em um projeto individual, o NuGet gerencia o grafo de dependência geral, que inclui novamente a resolução de múltiplas referências para versões diferentes do mesmo pacote. É muito comum que um projeto adote uma dependência de um ou mais pacotes que tenham eles próprios as mesmas dependências. Alguns dos pacotes de utilitário mais úteis no nuget.org são utilizados por muitos outros pacotes. No grafo de dependência inteiro, dez, você poderia ter facilmente ter dez referências diferentes para diferentes versões do mesmo pacote. Para evitar trazer várias versões do pacote para o próprio aplicativo, o NuGet classifica qual versão única pode ser usada por qualquer consumidor. (Para saber mais, confira [Resolução de dependência](consume-packages/dependency-resolution.md).)

Além disso, o NuGet mantém todas as especificações relacionadas a como os pacotes são estruturados (incluindo [localização](create-packages/creating-localized-packages.md) e [símbolos de depuração](create-packages/symbol-packages.md)) e como eles são referenciados (incluindo [intervalos de versão](reference/package-versioning.md#version-ranges-and-wildcards) e [versões de pré-lançamento](create-packages/prerelease-packages.md)). O NuGet também oferece várias APIs para trabalhar com seus serviços por meio de programação, e fornece suporte para os desenvolvedores que escrevem modelos de projeto e extensões do Visual Studio.

Reserve um tempo para navegar pelo sumário desta documentação e você verá todos esses recursos representados nele, junto com as notas de versão desde o início do NuGet.

## <a name="comments-contributions-and-issues"></a>Comentários, contribuições e problemas

Por fim, apreciamos muito os comentários e contribuições para essa documentação&mdash;basta selecionar os comandos **Comentários** e **Editar** no tipo de qualquer página, ou visite o [repositório de documentos](https://github.com/NuGet/docs.microsoft.com-nuget/) e a [lista de problemas de documentos](https://github.com/NuGet/docs.microsoft.com-nuget/issues) no GitHub.

Também aceitamos contribuições para o NuGet em si por meio de seus [vários repositórios de GitHub](https://github.com/NuGet/Home); problemas do NuGet podem ser encontrados em [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues).

Aproveite sua experiência com o NuGet.
