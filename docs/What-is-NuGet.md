---
title: "O que é o NuGet e o que ele faz? | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/26/2017
ms.topic: hero-article
ms.prod: nuget
ms.technology: 
ms.assetid: c3faf278-4cbf-4733-96f6-9ee9f7203af9
description: "Uma introdução abrangente sobre o que o NuGet é e o que ele faz"
keywords: "Gerenciador de pacotes do NuGet, consumo, criação de pacote, hospedagem de pacote"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 29dcedf33a54e249fe0b6acf588e4aafde28304f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="an-introduction-to-nuget"></a>Uma introdução ao NuGet

Uma ferramenta essencial para qualquer plataforma de desenvolvimento moderna é um mecanismo por meio do qual os desenvolvedores podem criar, compartilhar e consumir bibliotecas de código úteis. Essas bibliotecas são normalmente chamadas de “pacotes” porque podem conter código compilado (como DLLs) juntamente com outros tipos de conteúdo que podem ser necessárias nos projetos que as consomem.

Para .NET, o mecanismo para compartilhar código é **NuGet**, que define como os pacotes .NET são criados, hospedados e consumidos e fornece as ferramentas para cada uma dessas funções. 

Em suma, um pacote do NuGet é um arquivo ZIP com a extensão `.nupkg` que contém o código compilado (DLLs), outros arquivos relacionados a esse código e um manifesto descritivo que inclui informações como o número de versão do pacote. Os desenvolvedores de biblioteca criam arquivos de pacote e os publicam em um host. Os consumidores de pacote recebem esses pacotes, os adicionam aos seus projetos e chamam a funcionalidade da biblioteca no código de projeto. Em seguida, o próprio NuGet manipula todos os detalhes de intermediários.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>O fluxo de pacotes entre criadores, hosts e clientes

Em sua função como host, o próprio NuGet mantém o repositório central de mais de 60.000 pacotes exclusivos disponíveis publicamente no [nuget.org](https://www.nuget.org). Esses pacotes são utilizados por milhões de desenvolvedores de .NET diariamente. O NuGet também permite hospedar pacotes em particular na nuvem, em uma rede privada ou até mesmo apenas nos seu sistema de arquivos local. Ao fazer isso, esses pacotes estão disponíveis apenas para os desenvolvedores dentro de um grupo específico de empresas ou clientes. As opções são explicadas em [Hospedando seus próprios feeds do NuGet](Hosting-Packages/Overview.md).

Qualquer seja sua natureza, um host que serve como um ponto de conexão entre os *criadores* e os *consumidores* do pacote. Os criadores compilam pacotes do NuGet úteis e os publicam em um host. Os consumidores pesquisam então por pacotes úteis e compatíveis em hosts acessíveis, baixando e incluindo esses pacotes em seus projetos. Depois de instalado em um projeto, as APIs dos pacotes estão disponíveis para o restante do código do projeto.

![Relação entre os criadores de pacote, hosts de pacote e consumidores de pacote](media/nuget-roles.png)

Nesse caso, um pacote “compatível” significa que ele contém os assemblies criados para pelo menos um .NET framework de destino que seja compatível com a estrutura de destino do projeto consumidor. Para tornar um pacote amplamente compatível, o criador compila assemblies separados para várias estruturas de destino e inclui todas elas no mesmo pacote. Quando um consumidor instalado o pacote, o NuGet extrai apenas os assemblies que são necessárias para o projeto. Isso minimiza a superfície do pacote no aplicativo final e/ou assemblies produzidos pelo projeto.

## <a name="nuget-tools"></a>Ferramentas do NuGet

Além do suporte à hospedagem, o NuGet também fornece uma variedade de ferramentas usadas por criadores e consumidores:

| Ferramenta | Plataformas | Cenários Aplicáveis | Descrição |
| --- | --- | --- | --- |
| [CLI do nuget.exe](Tools/nuget-exe-CLI-Reference.md) | Todos | Criação, Consumo | Fornece todos os recursos do NuGet, com alguns comandos de que aplicam especificamente aos criadores de pacote, alguns somente aos consumidores e outros a ambos. Por exemplo, os criadores de pacote usam o comando `nuget pack` para criar um pacote de vários assemblies e arquivos relacionados, os consumidores de pacote usam `nuget install` para incluir pacotes em um projeto e todos usam `nuget config` para definir as variáveis de configuração do NuGet.  |
| [Interface do usuário do Gerenciador de Pacotes](Tools/Package-Manager-UI.md) | Visual Studio no Windows | Consumo | Fornece uma interface do usuário fácil de usar para instalar e gerenciar pacotes em projetos do .NET. | 
| [Gerenciar a interface do usuário do NuGet](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough) | Visual Studio para Mac | Consumo | Fornece uma interface do usuário fácil de usar para instalar e gerenciar pacotes em projetos do .NET. |
| [Console do gerenciador de pacotes](Tools/Package-Manager-Console.md) | Visual Studio no Windows | Consumo | Fornece [comandos do PowerShell](Tools/Powershell-Reference.md) para instalar e gerenciar pacotes em projetos do .NET. | 
| [CLI do dotnet](Tools/dotnet-Commands.md) | Todos | Criação, Consumo | Fornece certas funcionalidades da CLI do NuGet diretamente na cadeia de ferramentas do .NET Core. |
| [MSBuild](Schema/msbuild-targets.md) | Windows | Criação, Consumo | Fornece a capacidade de criar e restaurar os pacotes usados em um projeto diretamente por meio da cadeia de ferramentas do MSBuild. |

Como você pode ver, as ferramentas com as quais você trabalha com o NuGet dependem muito se você está criando (e publicando) ou consumindo pacotes e a plataforma de trabalho. Detalhes mais específicos podem ser encontrados nos tópicos [Fluxo de trabalho de criação de pacote](Create-Packages/Overview-and-Workflow.md) e [Fluxo de trabalho de consumo do pacote](Consume-Packages/Overview-and-Workflow.md), juntamente com outros tópicos nessas seções. 

Os criadores de pacotes normalmente também são consumidores, pois eles aproveitam funcionalidades que existe em outros pacotes do NuGet. E, é claro, esses pacotes podem, por sua vez, depender de outros.

## <a name="managing-dependencies"></a>Gerenciamento de dependências

A capacidade de aproveitar facilmente o trabalho de outras pessoas é uma das coisas que torna um sistema de gerenciamento de pacotes tão eficaz. Da mesma forma, grande parte do que o NuGet faz é gerenciar essa árvore de dependência ou “grafo” em nome do seu projeto. Em poucas palavras, você precisa apenas se preocupar com os pacotes que você está usando diretamente em um projeto. Se algum desses pacotes consumir outros pacotes ele mesmo (que pode consumir pacotes), o NuGet cuidará de todas essas dependências de nível inferior.

A imagem a seguir mostra um projeto que depende de cinco pacotes, que por sua vez dependem de muitos outros.  

![Um grafo de dependência NuGet de exemplo para um projeto do .NET](media/dependency-graph.png)

Observe que alguns pacotes aparecem várias vezes no grafo de dependência. Por exemplo, há três consumidores diferentes do pacote B e cada consumidor também pode especificar uma versão diferente do pacote (não mostrado). Como esta é uma ocorrência comum, o NuGet felizmente faz o trabalho duro para determinar exatamente qual versão do Pacote B atende a todos os seus consumidores. Em seguida, o NuGet faz o mesmo para todos os outros pacotes, independente da profundidade que o grafo de dependência alcance.

Para obter mais detalhes sobre como o NuGet executa esse serviço, consulte [Resolução de dependência](Consume-Packages/Dependency-Resolution.md).

## <a name="tracking-references-and-restoring-packages"></a>Rastreando referências e restaurando pacotes

Como projetos podem ser movidos facilmente entre os computadores de desenvolvedor, repositórios de controle do código-fonte, servidores de build e assim por diante, é altamente impraticável manter assemblies binários dos pacotes do NuGet diretamente associados a um projeto. Isso não apenas tornaria cada cópia do projeto desnecessariamente sobrecarregada (desperdiçando, portanto, espaço em repositórios de controle do código-fonte), isso também dificultaria muito a atualização de binários do pacote para versões mais recentes, pois isso precisaria ser feito em todas as cópias do projeto. 

Em vez disso, o NuGet simplesmente mantém uma lista de referência de pacotes dos quais um projeto depende (incluindo as dependências de nível superior e inferior) e fornece os meios para restaurar todos os pacotes referenciados mediante solicitação, conforme descrito em [Restauração de pacote](Consume-Packages/Package-Restore.md). Ou seja, sempre que você instala um pacote de algum host em um projeto, o NuGet registra o identificador de pacote e o número de versão nesta lista de referência. (Desinstalar um pacote, é claro, remove-o da lista.) 

![Uma lista de referências de NuGet é criada na instalação do pacote e pode ser usada para restaurar os pacotes em outro lugar](media/nuget-restore.png)

Com apenas a lista de referência, o NuGet pode, então, reinstalar&mdash;ou seja, restaurar&mdash;todos os pacotes de hosts públicos e/ou privados a qualquer momento posteriormente. (Por esse motivo, nuget.org não permite a exclusão permanente de pacotes publicados, embora eles possam ser ocultados; consulte [Excluir pacotes](Policies/deleting-packages.md).) Ao confirmar um projeto no controle do código-fonte ou compartilhá-lo de alguma outra forma, você só precisará incluir a lista de referências e não os binários do pacote (consulte [Pacotes e controle do código-fonte](Consume-Packages/Packages-and-Source-Control.md).)

O computador que recebe um projeto, como um servidor de build obtendo uma cópia do projeto como parte de um sistema de implantação automatizada, simplesmente pede ao NuGet para restaurar as dependências sempre que necessário. Sistemas de build como o Visual Studio Team Services fornecem etapas de “restauração do NuGet” para essa finalidade exata. Da mesma forma, quando os desenvolvedores obtêm uma cópia de um projeto (como ao clonar um repositório), abrir o projeto no Visual Studio e executar um build, o Visual Studio automaticamente restaura os pacotes do NuGet necessários. Os desenvolvedores também podem instruir o NuGet a restaurar pacotes a qualquer momento usando o comando `nuget restore` da CLI ou o cmdlet `Install-Package` no Console do Gerenciador de Pacotes.

Claramente, a função primária do NuGet, no que diz respeito aos desenvolvedores, é manter essa lista de referência em nome do seu projeto e fornecer os meios para restaurar (e atualizar) com eficiência os pacotes referenciados.

A maneira como isso acontece exatamente evoluiu entre as versões diferentes do NuGet, resultando em vários *formatos de gerenciamento de pacotes*, como são chamados:

- [`packages.config`](Schema/packages-config.md): *(NuGet 1.0 ou superior)* Como um arquivo XML que mantém uma lista simples de todas as dependências do projeto, incluindo as dependências de outros pacotes instalados. 
- [`project.json`](Schema/project-json.md): *(NuGet 3.0 ou superior)* Um arquivo JSON de que mantém uma lista de dependências do projeto com um grafo geral do pacote em um arquivo associado, `project.lock.json`. Essa estrutura oferece melhor desempenho em `packages.config` conforme descrito em [Resolução de dependência](Consume-Packages/Dependency-Resolution.md), incluindo restauração transitiva, mas ela própria geralmente é substituída pelo PackageReference abaixo.
- [Referências de pacote em arquivos de projeto](Consume-Packages/Package-References-in-Project-Files.md) (também conhecido como “PackageReference”) | *(NuGet 4.0 ou superior)* Mantém uma lista de dependências de nível superior do projeto diretamente no arquivo de projeto, portanto, nenhum arquivo separado é necessário. Um arquivo associado, `project.assets.json`, é gerado dinamicamente como `project.lock.json` para gerenciar o grafo de dependência geral.

Qual formato de gerenciamento de pacotes é aplicado a um projeto depende do tipo de projeto e a versão disponível do NuGet e Visual Studio. Para verificar qual formato está sendo usado, simplesmente procure por `packages.config` ou `project.json` na raiz do projeto depois de instalar o primeiro pacote. Se você não encontrar nenhum desses arquivos, procure no arquivo de projeto diretamente por um elemento &lt;PackageReference&gt;.

No Visual Studio 2017, por exemplo, a maioria dos tipos de projetos usa `packages.config`, exceto os projetos UWP C# e .NET Core que usam PackageReference. 

## <a name="what-else-does-nuget-do"></a>O que mais o NuGet faz?

Para resumir o que abordamos até agora, o NuGet fornece (em sua função de hospedagem) repositório central nuget.org e é compatível com hospedagem privada. O NuGet fornece as ferramentas que os desenvolvedores precisam para criar, publicar e consumir pacotes. Ainda mais importante, o NuGet mantém uma lista de referência de pacotes usados em um projeto e a capacidade de restaurar e atualizar esses pacotes da lista.

Para fazer com que esses processos funcionem com eficiência, o NuGet realiza algumas otimizações nos bastidores. Particularmente, o NuGet gerencia os caches do pacote de todo o computador e de todo o projeto para abreviar a instalação e a reinstalação. Com relação ao cache de todo o computador, qualquer pacote baixado e instalado em um projeto é armazenado no cache, de forma que instalar o mesmo pacote em outro projeto não requer baixá-lo novamente. Claramente, isso é muito útil quando você estiver restaurando um grande número de pacotes com frequência, como em um servidor de build. Para obter mais detalhes sobre o mecanismo e como trabalhar com ele, consulte [Gerenciamento do cache do NuGet](Consume-Packages/Managing-the-Nuget-Cache.md).

Dentro de um projeto individual, o NuGet faz trabalha muito para gerenciar o grafo de dependência geral. (Ao usar `project.json` ou &lt;PackageReference&gt;, o NuGet mantém as informações em um arquivo secundário chamado `project.lock.json` e `project.assets.json`, respectivamente.) Novamente, isso inclui resolver diversas referências a versões diferentes do mesmo pacote.

Ou seja, é muito comum que um projeto adote uma dependência de um ou mais pacotes que tenham ele próprios as mesmas dependências. Por exemplo, alguns dos pacotes de utilitário mais úteis no nuget.org são utilizados por muitos outros pacotes. No grafo de dependência inteiro, dez, você poderia ter facilmente ter dez referências diferentes para diferentes versões do mesmo pacote. No entanto, não é recomendável trazer várias versões do pacote para o aplicativo em si, por isso o NuGet classifica qual versão única qualquer pessoa pode usar. (Consulte [Resolução de dependência](Consume-Packages/Dependency-Resolution.md) para obter mais informações sobre este tópico.)

Além disso, o NuGet mantém todas as especificações relacionadas a como os pacotes são estruturados (incluindo [localização](Create-Packages/Creating-Localized-Packages.md) e [símbolos de depuração](Create-Packages/Symbol-Packages.md)) e como eles são referenciados (incluindo [intervalos de versão](reference/package-versioning.md#version-ranges-and-wildcards) e [versões de pré-lançamento](create-packages/Prerelease-Packages.md)). O NuGet também fornece APIs para provedores de credenciais (para acessar os hosts privados) e para os desenvolvedores que escrever modelos de projeto e extensões do Visual Studio.

Reserve um tempo para navegar pelo sumário desta documentação e você verá todos esses recursos representados nele, junto com as notas de versão desde o início do NuGet.

## <a name="comments-contributions-and-issues"></a>Comentários, contribuições e problemas

Por fim, apreciamos muito os comentários e contribuições para essa documentação&mdash;basta selecionar os **Comentários** e **Edite** os comandos em qualquer página ou visite o [repositório de documentos](https://github.com/NuGet/docs.microsoft.com-nuget/) e a [lista de problemas de documentos](https://github.com/NuGet/docs.microsoft.com-nuget/issues) no GitHub.

Também aceitamos contribuições para o NuGet em si por meio de seu [vários repositórios de GitHub](https://github.com/NuGet/Home); problemas do NuGet podem ser encontrados no [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues).

Aproveite sua experiência com o NuGet.
