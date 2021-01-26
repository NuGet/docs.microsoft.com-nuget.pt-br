---
title: Notas de versão do NuGet 2,1
description: Notas de versão do NuGet 2,1 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c44ad32c8c4018ccb517b41bffda674eef1f11f3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777026"
---
# <a name="nuget-21-release-notes"></a>Notas de versão do NuGet 2,1

Notas de versão do [NuGet 2,0](../release-notes/nuget-2.0.md)  |  [Notas de versão do NuGet 2,2](../release-notes/nuget-2.2.md)

O NuGet 2,1 foi lançado em 4 de outubro de 2012.

## <a name="hierarchical-nugetconfig"></a>Nuget.Config hierárquica

O NuGet 2,1 proporciona maior flexibilidade no controle das configurações do NuGet por meio da movimentação recursiva da estrutura de pastas procurando `NuGet.Config` arquivos e, em seguida, compilando a configuração do conjunto de todos os arquivos encontrados.  Como exemplo, considere o cenário em que uma equipe tem um repositório de pacotes interno para compilações de CI de outras dependências internas. A estrutura de pastas de um projeto individual pode ser semelhante ao seguinte:

```
C:\
C:\myteam\
C:\myteam\solution1
C:\myteam\solution1\project1
```

Além disso, se a restauração do pacote estiver habilitada para a solução, a seguinte pasta também existirá:

```
C:\myteam\solution1\.nuget
```

Para que o repositório de pacotes interno da equipe esteja disponível para todos os projetos nos quais a equipe trabalha, embora não o esteja disponibilizando para cada projeto no computador, podemos criar um novo arquivo Nuget.Config e colocá-lo na pasta c:\myteam Não há nenhuma maneira de especificar uma pasta de pacotes por projeto.

```xml
<configuration>
    <packageSources>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </packageSources>
    <disabledPackageSources />
    <activePackageSource>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </activePackageSource>
</configuration>
```

Agora podemos ver que a fonte foi adicionada executando o comando ' nuget.exe Sources ' de qualquer pasta abaixo de c:\myteam, conforme mostrado abaixo:

![Origens do pacote da configuração pai do NuGet](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` os arquivos são pesquisados na seguinte ordem:

1. `.nuget\Nuget.Config`
2. Movimentação recursiva da pasta do projeto para a raiz
3. Global `Nuget.Config` ( `%appdata%\NuGet\Nuget.Config` )

As configurações são as aplicadas na *ordem inversa*, o que significa que com base na ordenação acima, a Nuget.Config global seria aplicada primeiro, seguida pelos arquivos de Nuget.Config descobertos da raiz para a pasta do projeto, seguido por `.nuget\Nuget.Config` .  Isso é particularmente importante se você estiver usando o `<clear/>` elemento para remover um conjunto de itens da configuração.

## <a name="specify-packages-folder-location"></a>Especificar o local da pasta ' Packages '

No passado, o NuGet gerenciava os pacotes de uma solução de uma pasta ' Packages ' conhecida encontrada abaixo da pasta raiz da solução.  Para equipes de desenvolvimento que têm muitas soluções diferentes que têm pacotes NuGet instalados, isso pode resultar na instalação do mesmo pacote em vários locais diferentes no sistema de arquivos.

O NuGet 2,1 fornece um controle mais granular sobre o local da pasta de pacotes por meio do `repositoryPath` elemento no `NuGet.Config` arquivo.  Criando o exemplo anterior de suporte hierárquico de Nuget.Config, suponha que desejamos que todos os projetos em C:\myteam\ compartilhem a mesma pasta de pacotes.  Para fazer isso, basta adicionar a entrada a seguir ao `c:\myteam\Nuget.Config` .

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

Neste exemplo, o arquivo compartilhado `Nuget.Config` especifica uma pasta de pacotes compartilhados para cada projeto criado sob C:\myteam, independentemente da profundidade. Observe que, se você tiver uma pasta pacotes existente sob a raiz da solução, será necessário excluí-la antes que o NuGet Coloque os pacotes no novo local.

## <a name="support-for-portable-libraries"></a>Suporte para bibliotecas portáteis

As [bibliotecas portáteis](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) são um recurso introduzido pela primeira vez com o .NET 4, que permite que você crie assemblies que podem funcionar sem modificação em diferentes plataformas da Microsoft, desde versões do The.NET Framework até o Silverlight até Windows Phone e até mesmo o Xbox 360 (embora, no momento, o NuGet não ofereça suporte ao destino da biblioteca portátil do Xbox).  Ao estender as [convenções de pacote](../create-packages/supporting-multiple-target-frameworks.md) para versões e perfis do Framework, o NuGet 2,1 agora dá suporte a bibliotecas portáteis, permitindo que você crie pacotes que tenham pastas compostas de estrutura e perfil de destino `lib` .

Como exemplo, considere as seguintes plataformas de destino disponíveis da biblioteca de classes portátil.

![Diálogo de criação de biblioteca portátil](./media/releasenotes-21-plib.png)

Depois que a biblioteca é criada e o comando `nuget.exe pack MyPortableProject.csproj` é executado, a nova estrutura de pasta de pacote de biblioteca portátil pode ser vista examinando o conteúdo do pacote NuGet gerado.

![Layout do pacote de biblioteca portátil](./media/releasenotes-21-plib-layout.png)

Como você pode ver, a Convenção de nome da pasta de biblioteca portátil segue o padrão ' Portable-{Framework 1} + {Framework n} ', em que os identificadores de estrutura seguem o [nome da estrutura e as convenções de versão](../reference/target-frameworks.md)existentes. Uma exceção às convenções de nome e versão é encontrada no identificador de estrutura usado para Windows Phone.  Esse moniker deve usar o nome de estrutura ' wp ' (WP7, wp71 ou WP8). O uso de ' Silverlight-WP7 ', por exemplo, resultará em um erro.

Ao instalar o pacote criado a partir dessa estrutura de pastas, o NuGet agora pode aplicar sua estrutura e regras de perfil a vários destinos, conforme especificado no nome da pasta.  Por trás das regras de correspondência do NuGet, é o princípio de que destinos "mais específicos" terão precedência sobre os "menos específicos".  Isso significa que os monikers que se destinam a uma plataforma específica sempre serão preferidos sobre os portáteis se forem ambos compatíveis com um projeto.  Além disso, se vários destinos portáteis forem compatíveis com um projeto, o NuGet preferirá aquele em que o conjunto de plataformas com suporte é "mais próximo" ao projeto que faz referência ao pacote.

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>Direcionando projetos do Windows 8 e do Windows Phone 8

Além de adicionar suporte para o direcionamento de projetos de biblioteca portátil, o NuGet 2,1 fornece novos monikers de estrutura para projetos do Windows 8 Store e do Windows Phone 8, bem como alguns novos monikers gerais para a Windows Store e Windows Phone projetos que serão mais fáceis de gerenciar em versões futuras das respectivas plataformas.

Para aplicativos da loja do Windows 8, os identificadores têm a seguinte aparência:

| NuGet 2,0 e anterior | NuGet 2.1 |
| ---------------- | ----------- |
| winRT45, . NETCore45 | Windows, windows8, Win, win8 |

<br/>
Para projetos Windows Phone, os identificadores têm a seguinte aparência:

| SO do telefone | NuGet 2,0 e anterior | NuGet 2.1 |
| --- | --- | --- |
| Windows Phone 7 | silverlight3-wp | WP, WP7, WindowsPhone, WindowsPhone7 |
| Windows Phone 7,5 (Mango) | silverlight4-wp71 | wp71, WindowsPhone71 |
| Windows Phone 8 | (sem suporte) | WP8, WindowsPhone8 |

<br/>
Em todas as alterações acima, os nomes de estrutura antigos continuarão a ser totalmente suportados pelo NuGet 2,1.  Avançando, os novos nomes devem ser usados, pois eles serão mais estáveis em versões futuras das respectivas plataformas. Os novos nomes *não* terão suporte em versões do NuGet anteriores a 2,1. no entanto, planeje adequadamente para quando fazer a alternância.

## <a name="improved-search-in-package-manager-dialog"></a>Pesquisa aprimorada na caixa de diálogo Gerenciador de pacotes

Nas últimas várias iterações, foram introduzidas alterações na galeria do NuGet que melhoraram muito a velocidade e a relevância das pesquisas de pacote.  No entanto, essas melhorias eram limitadas ao site da nuget.org.  O NuGet 2,1 torna a experiência de pesquisa aprimorada disponível por meio da caixa de diálogo Gerenciador de pacotes NuGet.  Como exemplo, imagine que você queria encontrar o pacote de visualização do Windows Azure Caching.  Uma consulta de pesquisa razoável para esse pacote pode ser "cache do Azure".  Nas versões anteriores da caixa de diálogo Gerenciador de pacotes, o pacote desejado nem mesmo seria listado na primeira página de resultados.  No entanto, no NuGet 2,1, o pacote desejado agora aparece na parte superior dos resultados da pesquisa.

![Pesquisa de diálogo do Gerenciador de pacotes](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>Forçar atualização do pacote

Antes do NuGet 2,1, o NuGet ignoraria a atualização de um pacote quando não havia um número de versão alto.  Isso introduziu o problema para determinados cenários – particularmente no caso de cenários de compilação ou CI, em que a equipe não queria incrementar o número de versão do pacote com cada compilação.  O comportamento desejado foi forçar uma atualização, independentemente.  O NuGet 2,1 resolve isso com o sinalizador ' Reinstall '.  Por exemplo, as versões anteriores do NuGet resultarão no seguinte ao tentar atualizar um pacote que não tinha uma versão mais recente do pacote:

```
PM> Update-Package Moq
No updates available for 'Moq' in project 'MySolution.MyConsole'.
```

Com o sinalizador REINSTALL, o pacote será atualizado independentemente de haver uma versão mais recente.

```
PM> Update-Package Moq -Reinstall
Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
Successfully uninstalled 'Moq 4.0.10827'.
Successfully installed 'Moq 4.0.10827'.
Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.
```

Outro cenário em que o sinalizador reinstalar comprova benéfico é o de redirecionamento de estrutura. Ao alterar a estrutura de destino de um projeto (por exemplo, do .NET 4 para o .NET 4,5), a reinstalação do Update-Package pode atualizar as referências aos assemblies corretos para todos os pacotes do NuGet instalados no projeto.

## <a name="edit-package-sources-within-visual-studio"></a>Editar fontes de pacote no Visual Studio

Nas versões anteriores do NuGet, a atualização de uma origem de pacote de dentro da caixa de diálogo opções do Visual Studio exigia a exclusão e a adição da origem do pacote.  O NuGet 2,1 melhora esse fluxo de trabalho ao dar suporte à atualização como uma função de primeira classe da interface do usuário de configuração.

![Caixa de diálogo de configuração do Gerenciador de pacotes](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Correções de bugs

O NuGet 2,1 inclui muitas correções de bugs. Para obter uma lista completa de itens de trabalho corrigidos no NuGet 2,0, consulte o [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
