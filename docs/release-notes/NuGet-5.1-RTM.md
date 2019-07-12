---
title: Notas de versão do NuGet RTM 5.1
description: Notas de versão do 5.1 de NuGet, incluindo novos recursos, correções de bugs e DCRs.
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 384145947b19af6577dc1255985df1a361c72bb5
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842575"
---
# <a name="nuget-51-release-notes"></a>Notas de versão 5.1 do NuGet

Veículos de distribuição do NuGet:

| Versão do NuGet | Disponível na versão do Visual Studio| Disponível em SDKs do .NET|
|:---|:---|:---|
| [**5.1.0**](https://nuget.org/downloads) | [Visual Studio 2019 versão 16.1](https://visualstudio.microsoft.com/downloads/) | [2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>instaladas com o Visual Studio de 2019 com carga de trabalho do .NET Core 

<sup>2</sup>disponível como uma instalação opcional com o Visual Studio de 2019 com carga de trabalho do .NET Core

## <a name="summary-whats-new-in-51"></a>Resumo: O que há de novo no 5.1

* Suporte para ignorar um envio por push do pacote se ele já existe para permitir uma melhor integração com fluxos de trabalho CI/CD - [1630 #](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)

* O Visual Studio agora fornece um link conveniente para a página da Galeria do pacote nuget.org - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)

* Suporte para novos ativos do .NET Core 3.0, como [pacotes de direcionamento](https://github.com/dotnet/cli/issues/10006) e [pacotes de tempo de execução](https://github.com/dotnet/cli/issues/10007)
  * Suportam de pacote do NuGet e restauração para FrameworkReferences habilitar as referências de pacote de direcionamento e tempo de execução - [#7342](https://github.com/NuGet/Home/issues/7342)
  * Cenário de pacote "baixar apenas" suporte com PackageDownload - [7339 #](https://github.com/NuGet/Home/issues/7339)
  * Tempo de execução Exlcude e pacotes de resultados da pesquisa e a restauração de direcionamento do graph usando o tipo de pacote - [7337 #](https://github.com/NuGet/Home/issues/7337)

### <a name="issues-fixed-in-this-release"></a>Problemas corrigidos nesta versão

**•s**

* Plug-ins: detalhes da exceção perdido durante a criação do plug-in - [#8057](https://github.com/NuGet/Home/issues/8057)

* Intervalo de PackageReference com o limite inferior exclusivo não funcionará se o limite inferior está presente em uma das fontes. - [#8054](https://github.com/NuGet/Home/issues/8054)

* Melhorar a mensagem IsPackableFalseError - [8021 #](https://github.com/NuGet/Home/issues/8021)

* Empacota o arquivo de bloqueio – arquivo de bloqueio regenerar ao projeto gráfico muda - [8019 #](https://github.com/NuGet/Home/issues/8019)

* ProjectSystem bug: Obtendo automática de pacotes do NuGet removida - [8017 #](https://github.com/NuGet/Home/issues/8017)

* Adicionar um destino para retornar o FrameworkReference semelhantes a CollectPackageDownloads e CollectPackageReferences - [8005 #](https://github.com/NuGet/Home/issues/8005)

* Cache HTTP:  Recurso RepositoryResources não é armazenado em cache de uma forma de controle de versão - [#7997](https://github.com/NuGet/Home/issues/7997)

* Registro em log: pilhas de chamadas de exceção não são relatadas detalhado - [#7955](https://github.com/NuGet/Home/issues/7955)

* Alterar todas as URLs de NuGet Docs para usar HTTPS - [7950 #](https://github.com/NuGet/Home/issues/7950)

* Melhorar a mensagem de aviso NU3024 - [7933 #](https://github.com/NuGet/Home/issues/7933)

* arquivo de bloqueio não atualizando quando packagereference removido - [#7930](https://github.com/NuGet/Home/issues/7930)

* Melhorar a manipulação de caso de erro ao validar o elemento licenseurl e licença no nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)

* UI PM - clique com botão direito no cabeçalho da guia e clicando em "Abrir local do arquivo" resulta em erro de - [#7913](https://github.com/NuGet/Home/issues/7913)

* Plug-ins: registrar em log quando sai do processo de plug-in - [#7907](https://github.com/NuGet/Home/issues/7907)

* Plug-ins: taxa de colisão alta em valores de data e hora de registro em log - [7899 #](https://github.com/NuGet/Home/issues/7899)

* Manifest.ReadFrom falhar em qualquer nuspec com LicenseExpression - [7894 #](https://github.com/NuGet/Home/issues/7894)

* RestoreLockedMode: NU1004 inesperado quando ProjectReference refere-se a um projeto com AssemblyName personalizado - [#7889](https://github.com/NuGet/Home/issues/7889)

* Mensagem de erro melhor quando a inicialização do plug-in falhar com uma exceção - [#7857](https://github.com/NuGet/Home/issues/7857)

* Ao fazer uma restauração NoOp, evite *. dgspec.json gravação no diretório obj - [#7854](https://github.com/NuGet/Home/issues/7854)

* GeneratePathProperty = true Falha ao gerar a propriedade em maiuscula incompatível - [#7843](https://github.com/NuGet/Home/issues/7843)

* Configurações: caractere inválido no caminho de origem pode causar falha no VS - [#7820](https://github.com/NuGet/Home/issues/7820)

* Se o arquivo de bloqueio é excluído, restauração não gerar arquivo de bloqueio no NoOp - [#7807](https://github.com/NuGet/Home/issues/7807)

* URL de licença e as causas de licença ler erro com metadados - [#7547](https://github.com/NuGet/Home/issues/7547)

* Exceções sem tratamento no V2FeedParser - [7523 #](https://github.com/NuGet/Home/issues/7523)

* NuGet.exe retorna o código de saída zero argumentos inválidos - [#7178](https://github.com/NuGet/Home/issues/7178)

* Atualizar erros e documentos de aviso para refletir os cenários relacionados de assinatura - [#6498](https://github.com/NuGet/Home/issues/6498)

* Arquivo de ativos deve usar caminhos relativos para habilitar a movimentação de projetos com mais facilidade - [#4582](https://github.com/NuGet/Home/issues/4582)

**DCRs**

* Plug-ins: habilitar o log de diagnóstico - [#7859](https://github.com/NuGet/Home/issues/7859)

* Verifique Tizen 6 são mapeados para o NetStandard 2.1 - [7773 #](https://github.com/NuGet/Home/issues/7773)

**[Lista de todos os problemas corrigidos nesta versão - RTM 5.1](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**
