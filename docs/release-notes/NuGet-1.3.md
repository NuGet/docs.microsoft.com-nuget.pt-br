---
title: Notas de versão do NuGet 1,3
description: Notas de versão do NuGet 1,3 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 54eda149352810eacc1d6340ad16cec1b03194e3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777113"
---
# <a name="nuget-13-release-notes"></a>Notas de versão do NuGet 1,3

Notas de versão do [NuGet 1,2](../release-notes/nuget-1.2.md)  |  [Notas de versão do NuGet 1,4](../release-notes/nuget-1.4.md)

O NuGet 1,3 foi lançado em 25 de abril de 2011.

## <a name="new-features"></a>Novos recursos

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>Criação de pacotes simplificada com integração de servidor de símbolos

A equipe do NuGet fez parceria com o pessoal em [SymbolSource.org](http://www.symbolsource.org/) para oferecer uma maneira realmente simples de publicar suas fontes e PDB junto com seu pacote. Isso permite que os consumidores do seu pacote concorram a fonte do seu pacote no depurador. Para obter mais detalhes, leia [criando e publicando um pacote de símbolos](../create-packages/symbol-packages.md) a maneira fácil de publicar pacotes NuGet com fontes. Você também pode assistir a uma demonstração ao vivo desse recurso como parte do NuGet em profundidade em Mix11. Esse recurso é totalmente demonstrado a partir da marca de 20 minutos do vídeo.

### <a name="open-packagepage-command"></a>`Open-PackagePage` Comando

Esse comando facilita a obtenção da página do projeto para um pacote de dentro do console do Gerenciador de pacotes. Ele também fornece opções para abrir a URL da licença e a página relatar abuso para o pacote.
A sintaxe para o comando é:

```
Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]
```

A `-PassThru` opção é usada para retornar o valor da URL especificada.

Exemplos:

```
PM> Open-PackagePage Ninject
```

Abre um navegador para a URL do projeto especificada no pacote Ninject.

```
PM> Open-PackagePage Ninject -License
```

Abre um navegador para a URL de licença especificada no pacote Ninject.

```
PM> Open-PackagePage Ninject -ReportAbuse
```

Abre um navegador para a URL na origem do pacote atual usada para relatar abuso para o pacote especificado.

```
PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru
```

Atribui a URL de licença à variável, $url, sem abrir a URL em um navegador.

### <a name="performance-improvements"></a>Melhorias no desempenho

O NuGet 1,3 apresenta muitas melhorias de desempenho. O NuGet 1,3 evita o download da mesma versão de um pacote várias vezes, incluindo um cache local por usuário. O cache pode ser acessado e limpo por meio da caixa de diálogo Configurações do Gerenciador de pacotes:

![Caixa de diálogo opções do NuGet com configurações de cache do pacote](./media/nuget-options.png)

Outros aprimoramentos de desempenho incluem adicionar suporte para compactação HTTP e melhorar a velocidade de instalação do pacote no Visual Studio.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>O Visual Studio e o nuget.exe usam a mesma lista de origens do pacote

Antes do NuGet 1,3, a lista de origens do pacote usada pelo nuget.exe e pelo Add-In do NuGet do Visual Studio não foi armazenada no mesmo local. O NuGet 1,3 agora usa a mesma lista em ambos os locais. A lista é armazenada em `NuGet.Config` e armazenada na pasta AppData.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>nuget.exe ignora arquivos e pastas que começam com '. ' por padrão

Para fazer com que o NuGet funcione bem com sistemas de controle do código-fonte, como subversão e Mercurial, nuget.exe ignora pastas e arquivos que começam com o caractere '. ' ao criar pacotes. Isso pode ser substituído usando dois novos sinalizadores:

* __-NoDefaultExcludes__ é usado para substituir essa configuração e incluir todos os arquivos.
* __-Exclude__ é usado para adicionar outros arquivos/pastas a serem excluídos usando um padrão. Por exemplo, para excluir todos os arquivos com a extensão de arquivo '. bak '

```cli
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_Observação: o padrão não é recursivo por padrão._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>Suporte para projetos do WiX e para o .NET micro Framework

Graças às contribuições da Comunidade, o NuGet inclui suporte para tipos de projeto do WiX, bem como para o .NET micro Framework.

## <a name="bug-fixes"></a>Correções de bugs

Para obter uma lista completa de correções de bugs, consulte o [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correções de bugs vale a pena observar

* Os pacotes com arquivos de origem funcionam em sites e em projetos de aplicativos Web.
Para sites, os arquivos de origem são copiados para a `App_Code` pasta
