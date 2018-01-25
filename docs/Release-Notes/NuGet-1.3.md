---
title: "Notas de versão do NuGet 1.3 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de versão do NuGet 1.3 incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão 1.3 do NuGet, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 59169be5b39ba4436e13e0935a0ad6efa724e08e
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-13-release-notes"></a>Notas de versão 1.3 do NuGet

[Notas de versão do NuGet 1.2](../release-notes/nuget-1.2.md) | [notas de versão do NuGet 1.4](../release-notes/nuget-1.4.md)

1.3 NuGet foi lançado em 25 de abril de 2011.

## <a name="new-features"></a>Novos recursos

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>Criação de pacote simplificada com integração do servidor de símbolo

A equipe do NuGet fez uma parceria com o pessoal [SymbolSource.org](http://www.symbolsource.org/) para oferecer uma maneira muito simple de publicar seu do PDB e de fontes junto com o pacote. Isso permite que os consumidores de seu pacote passar para a fonte do seu pacote do depurador. Para obter mais detalhes, leia [criar e publicar um pacote de símbolos](../create-packages/symbol-packages.md) a maneira fácil de publicar pacotes do NuGet com fontes. Você também pode assistir uma demonstração ao vivo desse recurso como parte do NuGet em profundidade falar no Mix11. Esse recurso é demonstrado totalmente iniciando na marca de 20 minutos do vídeo.

### <a name="open-packagepage-command"></a>`Open-PackagePage`Comando

Este comando torna fácil de obter a página do projeto para um pacote a partir do Console do Gerenciador de pacotes. Ele também fornece opções para abrir a URL de licença e a página do relatório abuso para o pacote.
A sintaxe do comando é:

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

O `-PassThru` opção é usada para retornar o valor da URL especificada.

Exemplos:

    PM> Open-PackagePage Ninject

Abre um navegador para a URL do projeto especificada no pacote Ninject.

    PM> Open-PackagePage Ninject -License

Abre um navegador para a URL de licença especificada no pacote Ninject.

    PM> Open-PackagePage Ninject -ReportAbuse

Abre um navegador para a URL de origem do pacote atual usada para relatar abuso para o pacote especificado.

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

Atribui a URL de licença à variável, $url, sem abrir a URL em um navegador.

### <a name="performance-improvements"></a>Melhorias de desempenho

1.3 NuGet apresenta muitos dos aprimoramentos de desempenho. 1.3 NuGet evita baixar a mesma versão de um pacote várias vezes, incluindo um cache local por usuário. O cache pode ser acessado e desmarcado por meio da caixa de diálogo Configurações do Gerenciador de pacotes:

![Caixa de diálogo de opções de NuGet com configurações de Cache do pacote](./media/nuget-options.png)

Outras melhorias de desempenho incluem a adição de suporte para compactação HTTP e melhorar a velocidade de instalação do pacote dentro do Visual Studio.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>O Visual Studio e nuget.exe usa a mesma lista de fontes de pacote

Antes do NuGet 1.3, a lista de fontes de pacote usado pelo nuget.exe e o NuGet Visual Studio Add-In não foram armazenados no mesmo local. 1.3 NuGet agora usa a mesma lista em ambos os locais. A lista é armazenada em `NuGet.Config` e armazenados na pasta dados de aplicativos.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>NuGet.exe ignora arquivos e pastas que começam com '.' por padrão

Para fazer com que o NuGet funcionam bem com sistemas de controle de origem, como subversão e Mercurial, nuget.exe ignora pastas e arquivos que começam com o '.' ao criar pacotes de caracteres. Isso pode ser substituído usando dois sinalizadores novo:

* __-NoDefaultExcludes__ é usado para substituir essa configuração e incluir todos os arquivos.
* __-Excluir__ é usado para adicionar outros arquivos/pastas a serem excluídos usando um padrão. Por exemplo, para excluir todos os arquivos com a extensão de arquivo '. bak'

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_Observação: o padrão não é recursivos por padrão._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>Suporte para projetos WiX e Micro .NET Framework

Agradecimentos contribuições da comunidade, NuGet inclui suporte para tipos de projeto do WiX, bem como o Micro do .NET Framework.

## <a name="bug-fixes"></a>Correções de Bug

Para obter uma lista completa das correções de bug, exibir o [NuGet Issue Tracker para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correções de bug, vale a pena observar

* Pacotes com arquivos de origem funcionam em ambos os sites e em projetos de aplicativo Web.
Para sites, os arquivos de origem são copiados para o `App_Code` pasta
