---
title: "Notas de versão do NuGet 2.1 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 6f972803-9e17-43f5-b77b-973c3accf695
description: "Notas de versão do NuGet 2.1 incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão 2.1 do NuGet, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: dafe575eedbfed215c0b1c86795bea281de97252
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-21-release-notes"></a>Notas de versão 2.1 do NuGet

[Notas de versão do NuGet 2.0](../release-notes/nuget-2.0.md) | [notas de versão 2.2 do NuGet](../release-notes/nuget-2.2.md)

2.1 NuGet foi lançado em 4 de outubro de 2012.

## <a name="hierarchical-nugetconfig"></a>NuGet. config hierárquica
NuGet 2.1 oferece maior flexibilidade no controle NuGet configurações por meio de recursivamente para percorrer a estrutura de pasta procurando `NuGet.Config` arquivos e, depois, compilando a configuração do conjunto de todos os arquivos encontrados.  Por exemplo, considere o cenário em que uma equipe tem um repositório interno do pacote para compilações de CI de outras dependências internas. A estrutura de pastas para um projeto individual pode parecer com o seguinte:

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

Além disso, se a restauração do pacote está habilitada para a solução, a pasta a seguir também vai existir:

    C:\myteam\solution1\.nuget

Para ter o repositório de pacote interno da equipe disponível para todos os projetos de equipe funciona em, ao mesmo tempo, tornando-o não disponível para todos os projetos na máquina, podemos criar um novo arquivo NuGet. config e colocá-lo na pasta c:\myteam. Não é possível especificar para uma pasta de pacotes por projeto.

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

Agora podemos ver que a origem foi adicionada, executando o comando 'nuget.exe fontes' de qualquer pasta abaixo c:\myteam conforme mostrado abaixo:

![Fontes de pacote de configuração do nuget pai](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config`arquivos são procurados na seguinte ordem:

1. `.nuget\Nuget.Config`
2. Recursiva ir da pasta do projeto raiz
3. Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)

As configurações são aplicadas a *ordem inversa*, que significa que, com base na classificação acima, o NuGet. config global deve ser aplicada primeiro, seguido pelos arquivos detectados NuGet. config de raiz a pasta do projeto, seguidos por `.nuget\Nuget.Config`.  Isso é particularmente importante se você estiver usando o `<clear/>` elemento para remover um conjunto de itens de configuração.

## <a name="specify-packages-folder-location"></a>Especifique 'packages' local da pasta
No passado, o NuGet gerencia pacotes da solução de uma pasta conhecida 'packages' encontrada sob a pasta raiz de solução.  Para as equipes de desenvolvimento que têm diferentes soluções que têm os pacotes do NuGet instalados, isso pode resultar no mesmo pacote que está sendo instalado em vários locais diferentes no sistema de arquivos.

2.1 NuGet fornece controle mais granular sobre o local da pasta de pacotes por meio de `repositoryPath` elemento o `NuGet.Config` arquivo.  Compilando o exemplo anterior de suporte do NuGet. config hierárquico, suponha que queremos ter todos os projetos em C:\myteam\ compartilhar a mesma pasta de pacotes.  Para fazer isso, basta adicionar a seguinte entrada ao `c:\myteam\Nuget.Config`.

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

Neste exemplo, compartilhado `Nuget.Config` arquivo Especifica uma pasta compartilhada de pacotes para cada projeto que é criado sob C:\myteam, independentemente de profundidade. Observe que, se você tiver uma pasta de pacotes existente sob a raiz da solução, será necessário excluí-lo antes que o NuGet colocará pacotes no novo local.

## <a name="support-for-portable-libraries"></a>Suporte para bibliotecas portáteis
[Bibliotecas portáteis](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) é um recurso introduzido pela primeira vez com o .NET 4 que permite criar assemblies que podem funcionar sem modificação em diferentes plataformas da Microsoft, de versões do.NET Framework para Silverlight para Windows Phone e até mesmo Xbox 360 (embora, neste momento, o NuGet não suporta o destino de biblioteca portátil do Xbox).  Estendendo o [pacote convenções](../create-packages/supporting-multiple-target-frameworks.md) para versões do framework e perfis, NuGet 2.1 agora dá suporte a bibliotecas portáteis, permitindo que você crie pacotes que têm composto framework e o perfil de destino `lib` pastas.

Por exemplo, considere a possibilidade de plataformas de destino disponíveis da biblioteca de classes portátil seguinte.

![Caixa de diálogo de criação de biblioteca portátil](./media/releasenotes-21-plib.png)

Depois que a biblioteca é criada e o comando `nuget.exe pack MyPortableProject.csproj` é executado, o portátil nova estrutura de pasta do pacote de biblioteca pode ser vista examinando o conteúdo do pacote do NuGet gerado.

![Layout do pacote de biblioteca portátil](./media/releasenotes-21-plib-layout.png)

Como você pode ver, a convenção de nomes de pasta de biblioteca portátil segue o padrão 'portátil-{framework 1} + {framework n}' em que os identificadores de framework siga existente [convenções de nome e versão do framework](../schema/target-frameworks.md). Uma exceção com as convenções de nome e versão foi encontrada no identificador de estrutura usado para Windows Phone.  Esse identificador de origem deve usar o nome da estrutura 'wp' (wp7, wp71 ou wp8). Usar 'silverlight-wp7', por exemplo, resultará em erro.

Ao instalar o pacote que é criado a partir dessa estrutura de pasta, o NuGet agora pode aplicar suas regras de estrutura e o perfil para vários destinos, conforme especificado no nome da pasta.  Atrás de regras de correspondência do NuGet é o princípio de que os destinos "mais específicos" terá precedência sobre "menos específicos".  Isso significa que monikers direcionar uma plataforma específica sempre será preferenciais sobre portátil se eles são compatíveis com um projeto.  Além disso, se vários destinos portáteis são compatíveis com um projeto, o NuGet preferirá aquele em que o conjunto de plataformas com suporte é "mais próximo" para o projeto de referência do pacote.

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>Direcionamento do Windows 8 e Windows Phone 8 projetos
Além de adicionar suporte para projetos de biblioteca portátil de destino, o NuGet 2.1 fornece novos identificadores de framework para projetos de armazenamento do Windows 8 e Windows Phone 8, bem como alguns novos identificadores gerais da Windows Store e projetos do Windows Phone que será mais fácil de gerenciar em versões futuras das respectivas plataformas.

Para aplicativos de armazenamento do Windows 8, os identificadores semelhante ao seguinte:

|NuGet 2.0 e versões anterior|2.1 NuGet|
|----------------|-----------|
|winRT45. NETCore45|Ganho de Windows, Windows 8, win8|

<br/>
Para projetos do Windows Phone, os identificadores semelhante ao seguinte:

|Sistema operacional do telefone|NuGet 2.0 e versões anterior|2.1 NuGet
|----------------|-----------|-----------|
|Windows Phone 7|silverlight3 wp|WP, wp7, WindowsPhone, WindowsPhone7|
|Windows Phone 7.5 (Mango)|silverilght4 wp71|wp71, WindowsPhone71|
|Windows Phone 8|(sem suporte)|wp8, WindowsPhone8|
<br/>
Em todas as alterações acima, os nomes de framework antigos continuarão ser totalmente suportados pelo NuGet 2.1.  Mais adiante, os novos nomes devem ser usados porque elas serão mais estáveis em versões futuras das respectivas plataformas. Os novos nomes serão *não* ser suportados em versões do NuGet antes 2.1, no entanto, por isso, planeje adequadamente quando fazer a transição.

## <a name="improved-search-in-package-manager-dialog"></a>Pesquisa aprimorada na caixa de diálogo Gerenciador de pacote
Sobre várias iterações anteriores, as alterações foram introduzidas para a Galeria do NuGet que aprimorados significativamente a velocidade e a relevância das pesquisas de pacote.  No entanto, esses melhorias foram limitadas para o site nuget.org.  2.1 NuGet faz com que a pesquisa aprimorada experiência disponíveis por meio de caixa de diálogo de Gerenciador de pacote do NuGet.  Por exemplo, imagine que você deseja encontrar o pacote de visualização de cache do Windows Azure.  Uma consulta de pesquisa razoável para esse pacote pode ser "Cache do Azure".  Nas versões anteriores da caixa de diálogo de Gerenciador de pacote, o pacote desejado ainda não é listado na primeira página de resultados.  No entanto, no NuGet 2.1, o pacote desejado agora aparece na parte superior dos resultados da pesquisa.

![Pesquisa de caixa de diálogo de Gerenciador de pacote](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>Forçar a atualização de pacote
Antes do NuGet 2.1, NuGet deve ignorar a atualização de um pacote quando não houve um número de versão de alta.  Isso introduzido fricção para determinados cenários – especialmente no caso de compilação ou CI cenários em que a equipe não queria incrementar a versão do pacote número em cada compilação.  O comportamento desejado foi forçar uma atualização independentemente.  NuGet 2.1 lida com isso com o sinalizador 'reinstalar'.  Por exemplo, versões anteriores do NuGet resultaria no seguinte ao tentar atualizar um pacote que não tem uma versão mais recente do pacote:

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

Com o sinalizador de reinstalação, o pacote será atualizado independentemente se há uma versão mais recente.

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

Outro cenário em que o sinalizador de reinstalação é vantajoso é de estrutura redirecionando. Ao alterar a estrutura de destino de um projeto (por exemplo, do .NET 4 para o .NET 4.5), pacote de atualização-reinstalar pode atualizar referências aos assemblies corretos para todos os pacotes do NuGet instalados no projeto.

## <a name="edit-package-sources-within-visual-studio"></a>Editar origens do pacote dentro do Visual Studio
Nas versões anteriores do NuGet, atualizando uma origem do pacote de dentro da caixa de diálogo de opções da Visual Studio necessária excluir e adicionar novamente a origem do pacote.  2.1 NuGet melhora esse fluxo de trabalho com o suporte à atualização como uma função de primeira classe da interface do usuário de configuração.

![Diálogo de configuração do Gerenciador de pacote](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Correções de Bug
NuGet 2.1 inclui muitas correções de bugs. Para obter uma lista completa de trabalho itens corrigidos no NuGet 2.0, por favor, exibição de [NuGet Issue Tracker para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
