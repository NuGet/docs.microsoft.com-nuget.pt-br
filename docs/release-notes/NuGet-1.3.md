---
title: Notas de versão 1.3 do NuGet
description: Notas de versão para 1.3 de NuGet, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fa89af100096356c2ffb4d6c501c4a34296ad0ea
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551345"
---
# <a name="nuget-13-release-notes"></a>Notas de versão 1.3 do NuGet

[Notas de versão do NuGet 1.2](../release-notes/nuget-1.2.md) | [notas de versão do NuGet 1.4](../release-notes/nuget-1.4.md)

1.3 do NuGet foi lançado em 25 de abril de 2011.

## <a name="new-features"></a>Novos recursos

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>Criação simplificada de pacote com a integração do servidor de símbolo

A equipe do NuGet em parceria com o pessoal [SymbolSource.org](http://www.symbolsource.org/) para oferecer uma maneira muito simple de publicação de suas fontes e do PDB junto com seu pacote. Isso permite que os consumidores do seu pacote percorrer o código-fonte para o pacote no depurador. Para obter mais detalhes, leia [criando e publicando um pacote de símbolos](../create-packages/symbol-packages.md) a forma mais fácil para publicar pacotes do NuGet com códigos-fonte. Você também pode assistir uma demonstração ao vivo desse recurso como parte do NuGet em profundidade falar em Mix11. Esse recurso totalmente é demonstrado começando na marca de 20 minutos do vídeo.

### <a name="open-packagepage-command"></a>`Open-PackagePage` Comando

Este comando torna fácil chegar à página do projeto para um pacote de dentro do Console do Gerenciador de pacotes. Ele também fornece opções para abrir a URL de licença e a página de abuso de relatório para o pacote.
A sintaxe do comando é:

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

O `-PassThru` opção é usada para retornar o valor da URL especificada.

Exemplos:

    PM> Open-PackagePage Ninject

Abre um navegador para a URL de projeto especificada no pacote Ninject.

    PM> Open-PackagePage Ninject -License

Abre um navegador para a URL de licença especificada no pacote Ninject.

    PM> Open-PackagePage Ninject -ReportAbuse

Abre um navegador para a URL de origem do pacote atual usada para relatar abuso para o pacote especificado.

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

Atribui a URL de licença à variável, $url, sem abrir a URL em um navegador.

### <a name="performance-improvements"></a>Melhorias de desempenho

1.3 NuGet apresenta muitos dos aprimoramentos de desempenho. 1.3 NuGet evita o download a mesma versão de um pacote várias vezes com a inclusão de um cache local por usuário. O cache pode ser acessado e desmarcado por meio da caixa de diálogo Configurações do Gerenciador de pacotes:

![Caixa de diálogo de opções de NuGet com as configurações de Cache do pacote](./media/nuget-options.png)

Outros aprimoramentos de desempenho incluem adicionar suporte à compactação HTTP e melhorar a velocidade de instalação do pacote dentro do Visual Studio.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>O Visual Studio e nuget.exe usa a mesma lista de origens de pacote

Antes do NuGet 1.3, a lista de origens de pacote usado pelo nuget.exe e o NuGet Visual Studio Add-In não foram armazenados no mesmo local. 1.3 NuGet agora usa a mesma lista em ambos os locais. A lista é armazenada em `NuGet.Config` e armazenados na pasta AppData.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>NuGet.exe ignora arquivos e pastas que começam com '.' por padrão

Para fazer com que o NuGet funciona bem com sistemas de controle do código-fonte, como o Subversion e o Mercurial, nuget.exe ignora pastas e arquivos que começam com o '.' ao criar pacotes de caracteres. Isso pode ser substituído usando dois sinalizadores novo:

* __-NoDefaultExcludes__ é usado para substituir essa configuração e incluir todos os arquivos.
* __-Excluir__ é usado para adicionar outros arquivos ou pastas a serem excluídos usando um padrão. Por exemplo, para excluir todos os arquivos com a extensão de arquivo '. bak'

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_Observação: o padrão não é recursiva por padrão._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>Suporte para projetos WiX e o .NET Micro Framework

Graças a contribuições da comunidade, o NuGet inclui suporte para tipos de projeto do WiX, bem como o .NET Micro Framework.

## <a name="bug-fixes"></a>Correções de Bug

Para obter uma lista completa de correções de bugs, exibir o [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correções de bugs, vale a pena observar

* Pacotes com arquivos de origem funcionam em ambos os sites e em projetos de aplicativos Web.
Para sites, os arquivos de origem são copiados para o `App_Code` pasta
