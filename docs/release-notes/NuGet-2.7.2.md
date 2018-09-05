---
title: Notas de versão do NuGet 2.7.2
description: Notas de versão do NuGet 2.7.2 incluindo conhecidos problemas, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3e63944a05f66d5dadf17c5d4b91d3bc4478bb33
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550064"
---
# <a name="nuget-272-release-notes"></a>Notas de versão do NuGet 2.7.2

[Notas de versão do NuGet 2.7.1](../release-notes/nuget-2.7.1.md) | [notas de versão do NuGet 2.8](../release-notes/nuget-2.8.md)

O NuGet 2.7.2 foi lançado em 11 de novembro de 2013.

## <a name="noteworthy-bug-fixes-and-features"></a>Recursos e correções de bugs notáveis

### <a name="license-text"></a>Texto de licença
Há algum tempo, a Microsoft incluiu os pacotes NuGet para várias bibliotecas de código-fonte aberto populares como parte dos modelos padrão para projetos de aplicativos Web no Visual Studio. jQuery é provavelmente o exemplo mais conhecido desse tipo de biblioteca. Devido ao contrato de suporte associado aos componentes que são entregues, juntamente com um produto, o arquivo de script do pacote contém o texto de licenças diferente que o arquivo de script encontrado no mesmo pacote na Galeria nuget.org pública. Essa diferença no texto pode impedir que as atualizações de pacote de continuar devido os blocos de texto de licenças diferente fazendo com que os arquivos de script ter valores de hash de conteúdo diferentes (e, portanto, para serem tratados como modificados dentro do projeto).

Para atenuar esse problema, o NuGet 2.7.2 permite que o autor do script incluir o bloco de texto dentro de uma seção marcado especialmente que será semelhante ao seguinte licença.

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

Ao atualizar os pacotes com conteúdo de arquivos que contêm este bloco NuGet não fatorar o conteúdo do bloco em comparação com a versão na Galeria do NuGet e pode, portanto, excluir e atualizar o arquivo de conteúdo como se ele corresponde a cópia original.

Este bloco é identificado pelo texto "NUGET: começar a licença TEXT" e "NUGET: final licença TEXT" que ocorrem em qualquer lugar no início e final de linhas.  Não há outros requisitos de formatação existirem, permitindo que esse recurso a ser usado em qualquer tipo de arquivo de texto, independentemente do idioma.

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>Adicionar redirecionamentos de associação para Assemblies não Framework
Para assemblies que fazem parte do .NET Framework, o NuGet ignora adicionar redirecionamentos de associação no arquivo de configuração do aplicativo quando a atualização do pacote. Essa correção endereços uma regressão no NuGet 2.7 no qual os redirecionamentos de associação não foram sendo adicionados para alguns assemblies, mesmo que esses assemblies não são considerados parte do .NET Framework. O NuGet 2.7.2 restaura o NuGet 2.5 anterior e o comportamento de 2,6 e adiciona os redirecionamentos de associação.

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>Instalando bibliotecas portáteis com as ferramentas do Xamarin instaladas
Quando as ferramentas de desenvolvimento do Xamarin são instaladas em um computador, eles modificar os dados de configuração de estruturas com suporte para especificar a compatibilidade entre combinações de framework de destino existente e as estruturas do Xamarin. Com a versão 2.7.2, o NuGet agora está ciente dessas regras de compatibilidade implícita e, portanto, torna mais fácil para desenvolvedores visando plataformas Xamarin instalar bibliotecas portáteis que são compatíveis com o Xamarin, mas não explicitamente marcados como tal no pacote metadados em si.

### <a name="machine-wide-configuration-settings-honored"></a>Definições de configuração de todo o computador respeitadas
Ao usar arquivos hierárquicos de NuGet. config, o caminho do repositório chave não estava sendo respeitado para arquivos do NuGet. config mais próximos da raiz da solução. No Visual Studio 2013, o NuGet instala um arquivo personalizado do NuGet. config em %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config para adicionar a origem do pacote "Microsoft e .NET". Como resultado, a solução alternativa para usar um caminho do repositório personalizado em uma solução era excluir o nível de máquina NuGet. config - qual também deve remover a origem do pacote "Microsoft e .NET". Agora, o NuGet 2.7.2 respeita as regras de precedência de caminho do repositório ao usar arquivos hierárquicos de NuGet. config.

## <a name="all-changes"></a>Todas as alterações
Para obter uma lista completa de trabalho itens corrigidos no NuGet 2.7.2, por favor, modo de exibição de [rastreador de problemas do NuGet para esta versão](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).
