---
title: Notas de versão do NuGet 5,1 RTM
description: Notas de versão do NuGet 5,1, incluindo novos recursos, correções de bugs e DCRs.
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 2a94360dc375ba90b90c1045f4acbcfca81fea5b
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699863"
---
# <a name="nuget-51-release-notes"></a>Notas de versão do NuGet 5,1

Veículos de distribuição do NuGet:

| Versão do NuGet | Disponível na versão do Visual Studio| Disponível em SDKs do .NET|
|:---|:---|:---|
| [**5.1.0**](https://nuget.org/downloads) | [Visual Studio 2019 versão 16,1](https://visualstudio.microsoft.com/downloads/) | [2.1.70 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Instalado com o Visual Studio 2019 com carga de trabalho do .NET Core 

<sup>2</sup> Disponível como uma instalação opcional com o Visual Studio 2019 com carga de trabalho do .NET Core

## <a name="summary-whats-new-in-51"></a>Resumo: o que há de novo no 5,1

* Suporte para ignorar um push de pacote se ele já existir para permitir uma melhor integração com fluxos de trabalho de CI/CD- [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)

* Agora, o Visual Studio fornece um link conveniente para a página da Galeria nuget.org do pacote- [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)

* Suporte para novos ativos 3,0 do .NET Core, como [pacotes de direcionamento](https://github.com/dotnet/cli/issues/10006) e [pacotes de tempo de execução](https://github.com/dotnet/cli/issues/10007)
  * NuGet Pack e Restore support for FrameworkReferences to Enable Targeting and Runtime Package References- [#7342](https://github.com/NuGet/Home/issues/7342)
  * Suporte ao cenário de pacote "somente download" com PackageDownload- [#7339](https://github.com/NuGet/Home/issues/7339)
  * Excluir tempo de execução e pacotes de direcionamento dos resultados da pesquisa & restaurar grafo usando o Pacotetype- [#7337](https://github.com/NuGet/Home/issues/7337)

### <a name="issues-fixed-in-this-release"></a>Problemas corrigidos nesta versão

**Bugs**

* Plug-ins: detalhes da exceção perdidos durante a criação do plug-in- [#8057](https://github.com/NuGet/Home/issues/8057)

* O intervalo de PackageReference com limite inferior exclusivo não funcionará se o limite inferior estiver presente em uma das fontes. - [#8054](https://github.com/NuGet/Home/issues/8054)

* Melhorar a mensagem de IsPackableFalseError- [#8021](https://github.com/NuGet/Home/issues/8021)

* Pacotes de bloqueio de arquivo – gerar novamente o arquivo de bloqueio quando o Project Graph alterar- [#8019](https://github.com/NuGet/Home/issues/8019)

* Bug ProjectSystem: pacotes NuGet sendo removidos automaticamente- [#8017](https://github.com/NuGet/Home/issues/8017)

* Adicionar um destino para retornar o FrameworkReference semelhante a CollectPackageDownloads e CollectPackageReferences- [#8005](https://github.com/NuGet/Home/issues/8005)

* Cache HTTP: o recurso RepositoryResources não está armazenado em cache de maneira com versão [#7997](https://github.com/NuGet/Home/issues/7997)

* Registro em log: as pilhas de chamadas de exceção não são relatadas com detalhes detalhados- [#7955](https://github.com/NuGet/Home/issues/7955)

* Alterar todas as URLs de documentos do NuGet para usar HTTPS- [#7950](https://github.com/NuGet/Home/issues/7950)

* Melhorar a mensagem de aviso do NU3024- [#7933](https://github.com/NuGet/Home/issues/7933)

* bloquear arquivo não atualizando quando packagereference removido- [#7930](https://github.com/NuGet/Home/issues/7930)

* Melhorar o tratamento de casos de erro ao validar licenseurl e o elemento de licença no nuspec- [#7915](https://github.com/NuGet/Home/issues/7915)

* Interface do usuário do PM-clique com o botão direito do mouse no cabeçalho da guia e clique em "abrir local do arquivo" resulta em erro- [#7913](https://github.com/NuGet/Home/issues/7913)

* Plugins: log quando o processo do plug-in é encerrado- [#7907](https://github.com/NuGet/Home/issues/7907)

* Plug-ins: alta taxa de colisão no log de valores de data/hora- [#7899](https://github.com/NuGet/Home/issues/7899)

* Manifest. ReadFrom falha em qualquer nuspec com Licenseid- [#7894](https://github.com/NuGet/Home/issues/7894)

* RestoreLockedMode: NU1004 inesperado quando ProjectReference se refere a um projeto com AssemblyName- [#7889](https://github.com/NuGet/Home/issues/7889) personalizado

* Melhor mensagem de erro quando a inicialização do plug-in falha com uma exceção- [#7857](https://github.com/NuGet/Home/issues/7857)

* Ao fazer uma restauração de NoOp, evite * .dgspec.jsem gravar no diretório obj- [#7854](https://github.com/NuGet/Home/issues/7854)

* GeneratePathProperty = true falha ao gerar Propriedade em caso de incompatibilidade de caso- [#7843](https://github.com/NuGet/Home/issues/7843)

* Configurações: caractere inválido no caminho de origem do pacote pode falhar VS- [#7820](https://github.com/NuGet/Home/issues/7820)

* Se o arquivo de bloqueio for excluído, Restore não gerará o arquivo de bloqueio em NoOp- [#7807](https://github.com/NuGet/Home/issues/7807)

* A URL de licença e a licença causam erro de leitura com metadados- [#7547](https://github.com/NuGet/Home/issues/7547)

* Exceções sem tratamento em V2FeedParser- [#7523](https://github.com/NuGet/Home/issues/7523)

* nuget.exe retorna o código de saída zero para argumentos inválidos- [#7178](https://github.com/NuGet/Home/issues/7178)

* Atualizar os erros e documentos de aviso para refletir cenários relacionados à assinatura- [#6498](https://github.com/NuGet/Home/issues/6498)

* O arquivo de ativos deve usar caminhos relativos para habilitar a movimentação de projetos com mais facilidade [#4582](https://github.com/NuGet/Home/issues/4582)

**DCRs**

* Plug-ins: habilitar log de diagnóstico- [#7859](https://github.com/NuGet/Home/issues/7859)

* Fazer o tizen 6 mapear para o netstandard 2,1- [#7773](https://github.com/NuGet/Home/issues/7773)

**[Lista de todos os problemas corrigidos nesta versão-5,1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**
