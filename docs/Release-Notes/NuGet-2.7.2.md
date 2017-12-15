---
title: "Notas de versão do NuGet 2.7.2 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: c775d1d7-de26-476c-bf9e-0cf95986a22f
description: "Notas de versão do NuGet 2.7.2 incluindo problemas conhecidos, correções de bug, recursos adicionados e DCRs."
keywords: "Notas de versão NuGet 2.7.2, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5bb1eb346666c5d5ee790fcdcd7d844bfd37b22e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-272-release-notes"></a>Notas de versão do NuGet 2.7.2

[Notas de versão do NuGet 2.7.1](../release-notes/nuget-2.7.1.md) | [notas de versão do NuGet 2.8](../release-notes/nuget-2.8.md)

NuGet 2.7.2 foi lançado em 11 de novembro de 2013.

## <a name="noteworthy-bug-fixes-and-features"></a>Recursos e correções de bugs notáveis

### <a name="license-text"></a>Texto de licença
Há algum tempo, a Microsoft incluiu os pacotes do NuGet para várias bibliotecas de código-fonte aberto populares como parte dos modelos padrão para projetos de aplicativo Web no Visual Studio. jQuery é provavelmente o exemplo mais conhecido desse tipo de biblioteca. Devido o contrato de suporte associado aos componentes que são entregues com um produto, o arquivo de script do pacote contém texto de licenças diferente que o arquivo de script encontrado no mesmo pacote na Galeria do nuget.org pública. Essa diferença no texto pode impedir que as atualizações de pacote continuar como resultado de blocos de texto de licenças diferente fazendo com que os arquivos de script com valores de hash de conteúdo diferentes (e, portanto, para serem tratados como modificados dentro do projeto).

Para atenuar esse problema, o NuGet 2.7.2 permite que o autor do script incluir o bloco de texto dentro de uma seção remarcação que será semelhante ao seguinte licença.

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

Ao atualizar os pacotes com conteúdo de arquivos que contêm esse bloco, NuGet não influenciar o conteúdo do bloco de comparação com a versão na Galeria do NuGet e podem, portanto, excluir e atualizar o arquivo de conteúdo como se ele corresponde a cópia original.

Esse bloco é identificado pelo texto "NUGET: começar a licença" e "NUGET: final licença texto" que ocorrem em qualquer lugar no início e final de linhas.  Não há outros requisitos de formatação existem, permitindo que esse recurso a ser usado em qualquer tipo de arquivo de texto, independentemente do idioma.

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>Adicionar ligação redireciona para Assemblies não Framework
Para assemblies que fazem parte do .NET Framework, o NuGet ignora adicionando redirecionamentos de associação no arquivo de configuração do aplicativo quando a atualização do pacote. Essa correção endereços uma regressão em 2.7 NuGet na qual redirecionamentos de associação não foram sendo adicionados para alguns assemblies, mesmo que esses assemblies não são considerados parte do .NET Framework. NuGet 2.7.2 restaura o NuGet 2.5 anterior e comportamento 2.6 e adiciona os redirecionamentos de associação.

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>Instalando bibliotecas portáteis com Xamarin Tools instalado
Quando as ferramentas de desenvolvimento do Xamarin estão instaladas em um computador, eles modificar os dados de configuração de estruturas com suporte para especificar a compatibilidade entre combinações de framework de destino existentes e estruturas de Xamarin. Com a versão 2.7.2, NuGet agora está ciente dessas regras de compatibilidade implícita e, portanto, facilita para os desenvolvedores direcionando plataformas Xamarin instalar bibliotecas portáteis que são compatíveis com o Xamarin, mas não foi explicitamente marcado como tal no pacote metadados em si.

### <a name="machine-wide-configuration-settings-honored"></a>Definições de configuração de máquina respeitadas
Ao usar arquivos hierárquicos do NuGet. config, o caminho do repositório chave não foi sendo cumprido para arquivos do NuGet. config mais próximos para a raiz da solução. No Visual Studio 2013, o NuGet instala um arquivo de config personalizado no %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config para adicionar a origem do pacote "Microsoft e .NET". Como resultado, a solução alternativa para usar um caminho do repositório personalizado em uma solução era excluir o NuGet. config no nível da máquina - que também deve remover a origem do pacote "Microsoft e .NET". NuGet 2.7.2 agora segue as regras de precedência para o caminho do repositório ao usar arquivos hierárquicos do NuGet. config.

## <a name="all-changes"></a>Todas as alterações
Para obter uma lista completa de trabalho itens corrigidos no NuGet 2.7.2, por favor, exibir o [NuGet Issue Tracker para esta versão](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).
