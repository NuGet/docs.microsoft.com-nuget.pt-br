---
title: Notas de versão do NuGet 2.7.2
description: Notas de versão do NuGet 2.7.2 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7643bf930bca39684eb626fe737001bc3e3ea769
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776778"
---
# <a name="nuget-272-release-notes"></a>Notas de versão do NuGet 2.7.2

Notas de versão do [NuGet 2.7.1](../release-notes/nuget-2.7.1.md)  |  [Notas de versão do NuGet 2,8](../release-notes/nuget-2.8.md)

O NuGet 2.7.2 foi lançado em 11 de novembro de 2013.

## <a name="noteworthy-bug-fixes-and-features"></a>Recursos e correções de bugs notáveis

### <a name="license-text"></a>Texto da licença
Por algum tempo, a Microsoft incluiu os pacotes NuGet para várias bibliotecas de software livre populares como parte dos modelos padrão para projetos de aplicativos Web no Visual Studio. o jQuery é provavelmente o exemplo mais conhecido desse tipo de biblioteca. Devido ao contrato de suporte associado aos componentes que são entregues junto com um produto, o arquivo de script do pacote contém um texto de licença diferente do arquivo de script encontrado no mesmo pacote na Galeria nuget.org pública. Essa diferença no texto pode impedir que atualizações de pacote continuem como resultado dos diferentes blocos de texto de licença, fazendo com que os arquivos de script tenham valores de hash de conteúdo diferentes (e, portanto, sejam tratados como modificados no projeto).

Para atenuar esse problema, o NuGet 2.7.2 permite que o autor do script inclua o bloco de texto de licença em uma seção especialmente marcada, que tem a seguinte aparência.

```
/************** NUGET: BEGIN LICENSE TEXT **************
    * The following code is licensed under the MIT license
    * Additional license information below is informational
    * only.
    ************** NUGET: END LICENSE TEXT ***************/
```

Ao atualizar pacotes com arquivos de conteúdo que contenham esse bloco, o NuGet não calcula o conteúdo do bloco na comparação com a versão na galeria do NuGet e, portanto, pode excluir e atualizar o arquivo de conteúdo como se ele corresponda à cópia original.

Esse bloco é identificado pelo texto "NUGET: BEGIN LICENSE TEXT" e "NUGET: END LICENSE TEXT" ocorrendo em qualquer lugar nas linhas inicial e final.  Não existem outros requisitos de formatação, permitindo que esse recurso seja usado em qualquer tipo de arquivo de texto, independentemente do idioma.

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>Adicionar redirecionamentos de associação para assemblies que não são da estrutura
Para assemblies que fazem parte do .NET Framework, o NuGet ignora a adição de redirecionamentos de associação ao arquivo de configuração do aplicativo ao atualizar o pacote. Essa correção aborda uma regressão no NuGet 2,7, na qual redirecionamentos de associação não estavam sendo adicionados a alguns assemblies, mesmo que esses assemblies não sejam considerados uma parte do .NET Framework. O NuGet 2.7.2 restaura o comportamento anterior do NuGet 2,5 e 2,6 e adiciona os redirecionamentos de associação.

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>Instalando bibliotecas portáteis com as ferramentas do Xamarin instaladas
Quando as ferramentas de desenvolvimento do Xamarin são instaladas em um computador, elas modificam os dados de configuração de estruturas com suporte para especificar a compatibilidade entre as combinações de estrutura de destino existentes e as estruturas do Xamarin. Com a versão 2.7.2, o NuGet agora está ciente dessas regras implícitas de compatibilidade e, portanto, facilita para os desenvolvedores direcionarem as plataformas Xamarin para instalar bibliotecas portáteis que são compatíveis com o Xamarin, mas não explicitamente marcados como tais nos próprios metadados do pacote.

### <a name="machine-wide-configuration-settings-honored"></a>Definições de configuração de todo o computador respeitadas
Ao usar arquivos de Nuget.Config hierárquicos, a chave repositoryPath não estava sendo respeitada para Nuget.Config arquivos mais próximos da raiz da solução. No Visual Studio 2013, o NuGet instala um arquivo de Nuget.Config personalizado em% ProgramData% \NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config para adicionar a origem do pacote "Microsoft e .NET". Como resultado, o trabalho para usar um repositoryPath personalizado em uma solução era excluir o nível de máquina Nuget.Config-que também significava remover a origem do pacote "Microsoft e .NET". O NuGet 2.7.2 agora honra as regras de precedência para repositoryPath ao usar arquivos de Nuget.Config hierárquicos.

## <a name="all-changes"></a>Todas as alterações
Para obter uma lista completa de itens de trabalho corrigidos no NuGet 2.7.2, consulte o [rastreador de problemas do NuGet para esta versão](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).
