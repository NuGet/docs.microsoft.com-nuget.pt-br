---
title: Notas de versão 2.1 do NuGet
description: Notas da versão 2.1 do NuGet incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fd6dadc7968991c77c1b06a6a261415355b2fd73
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548591"
---
# <a name="nuget-21-release-notes"></a>Notas de versão 2.1 do NuGet

[Notas de versão do NuGet 2.0](../release-notes/nuget-2.0.md) | [notas de versão do NuGet 2.2](../release-notes/nuget-2.2.md)

2.1 do NuGet foi lançado em 4 de outubro de 2012.

## <a name="hierarchical-nugetconfig"></a>NuGet. config hierárquica

2.1 do NuGet fornece maior flexibilidade no controle de configurações do NuGet por meio de recursivamente, percorra a estrutura de pastas procurando `NuGet.Config` arquivos e, em seguida, compilar a configuração do conjunto de todos os arquivos encontrados.  Por exemplo, considere o cenário em que uma equipe tem um repositório do pacote interno para compilações de CI de outras dependências internas. A estrutura de pastas para um projeto individual pode parecer com o seguinte:

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

Além disso, se a restauração do pacote está habilitada para a solução, a pasta a seguir também existirá:

    C:\myteam\solution1\.nuget

Para ter um repositório de pacote interno da equipe disponível para todos os projetos que a equipe trabalha em, ao mesmo tempo, tornando-o não disponível para todos os projetos na máquina, podemos criar um novo arquivo NuGet. config e colocá-lo na pasta c:\myteam. Não há nenhuma maneira para especificar uma pasta de pacotes por projeto.

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

Agora podemos ver que a fonte foi adicionada executando o comando 'nuget.exe fontes' de qualquer pasta abaixo c:\myteam conforme mostrado abaixo:

![Fontes de pacote de configuração do nuget pai](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` arquivos são pesquisados na seguinte ordem:

1. `.nuget\Nuget.Config`
2. Recursiva ir da pasta do projeto raiz
3. Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)

As configurações são aplicadas na *ordem inversa*, que significa que, com base na classificação acima, o NuGet. config global seria ser aplicada primeiro, seguido por descobertos arquivos NuGet. config de raiz a pasta do projeto, seguidos por `.nuget\Nuget.Config`.  Isso é particularmente importante se você estiver usando o `<clear/>` elemento para remover um conjunto de itens de configuração.

## <a name="specify-packages-folder-location"></a>Especifique 'pacotes' local da pasta

No passado, o NuGet tem gerenciado pacotes da solução de uma pasta de pacotes' conhecidos' encontrada sob a pasta raiz da solução.  Para equipes de desenvolvimento que têm muitas soluções diferentes que têm pacotes NuGet instalados, isso pode resultar no mesmo pacote que está sendo instalado em diversos lugares no sistema de arquivos.

2.1 do NuGet fornece controle mais granular sobre o local da pasta de pacotes por meio de `repositoryPath` elemento no `NuGet.Config` arquivo.  Compilando o exemplo anterior de suporte hierárquico do NuGet. config, suponha que desejamos ter todos os projetos em C:\myteam\ compartilhar a mesma pasta de pacotes.  Para fazer isso, basta adicionar a seguinte entrada à `c:\myteam\Nuget.Config`.

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

Neste exemplo, o compartilhado `Nuget.Config` arquivo Especifica uma pasta de pacotes compartilhados para cada projeto que é criada abaixo C:\myteam, independentemente de profundidade. Observe que, se você tiver uma pasta de pacotes existente sob a raiz da solução, você precisa excluí-lo antes do NuGet colocará pacotes no novo local.

## <a name="support-for-portable-libraries"></a>Suporte para bibliotecas portáteis

[Bibliotecas portáteis](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) é um recurso introduzido pela primeira vez com o .NET 4 que permite que você crie assemblies que podem funcionar sem modificação em diferentes plataformas da Microsoft, de versões do.NET Framework para Silverlight para Windows Phone e Xbox até mesmo 360 (embora neste momento, o NuGet não suporta o destino de biblioteca portátil do Xbox).  Estendendo o [convenções de pacote](../create-packages/supporting-multiple-target-frameworks.md) para versões do framework e perfis, 2.1 do NuGet agora dá suporte a bibliotecas portáteis, permitindo que você criar pacotes que têm composto framework e o perfil de destino `lib` pastas.

Por exemplo, considere a possibilidade de plataformas de destino disponíveis da biblioteca de classes portátil seguintes.

![Caixa de diálogo de criação de biblioteca portátil](./media/releasenotes-21-plib.png)

Depois que a biblioteca é compilada e o comando `nuget.exe pack MyPortableProject.csproj` é executado, portátil nova estrutura de pastas de pacote de biblioteca pode ser vista examinando o conteúdo do pacote do NuGet gerado.

![Layout do pacote de biblioteca portátil](./media/releasenotes-21-plib-layout.png)

Como você pode ver, a convenção de nomes de pasta de biblioteca portátil segue o padrão 'portable-{framework 1} + {framework n}' em que os identificadores de framework siga existente [convenções de nome e a versão do framework](../reference/target-frameworks.md). Uma exceção com as convenções de nome e a versão for encontrada no identificador de estrutura usado para o Windows Phone.  Esse moniker deve usar o nome da estrutura 'wp' (wp7, wp71 ou wp8). Usar 'silverlight wp7', por exemplo, resultará em erro.

Ao instalar o pacote que é criado a partir dessa estrutura de pasta, o NuGet agora pode aplicar suas regras de estrutura e o perfil para vários destinos, conforme especificado no nome da pasta.  Por trás de regras de correspondência do NuGet é o princípio de que os destinos "mais específicos" terá precedência sobre "menos específicas".  Isso significa que monikers visando uma plataforma específica sempre será preferenciais sobre aqueles portátil se eles são compatíveis com um projeto.  Além disso, se vários destinos portáteis são compatíveis com um projeto, o NuGet vai preferir aquele em que o conjunto de plataformas com suporte é "mais próximo" para o projeto referenciando o pacote.

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>Direcionamento do Windows 8 e Windows Phone 8 projetos

Além de adicionar suporte para projetos de biblioteca portátil de direcionamento, 2.1 do NuGet fornece novos monikers de estrutura para projetos do Windows 8 Store e Windows Phone 8, bem como alguns novos monikers gerais para a Windows Store e projetos do Windows Phone que será mais fácil de gerenciar em versões futuras das respectivas plataformas.

Para aplicativos do Windows 8 Store, os identificadores semelhante ao seguinte:

| NuGet 2.0 e versões anterior | 2.1 do NuGet |
| ---------------- | ----------- |
| winRT45, .NETCore45 | Win do Windows, Windows8, win8 |

<br/>
Para projetos do Windows Phone, os identificadores semelhante ao seguinte:

| Sistema operacional do telefone | NuGet 2.0 e versões anterior | 2.1 do NuGet |
| --- | --- | --- |
| Windows Phone 7 | silverlight3 wp | WP, wp7, WindowsPhone, WindowsPhone7 |
| Windows Phone 7.5 (Mango) | silverlight4 wp71 | wp71, WindowsPhone71 |
| Windows Phone 8 | (sem suporte) | wp8, WindowsPhone8 |

<br/>
Em todas as alterações acima, os nomes antigos do framework continuarão tendo suporte completo pelo NuGet 2.1.  Mais adiante, os novos nomes devem ser usados como eles serão mais estáveis entre versões futuras das respectivas plataformas. Os novos nomes serão *não* ser, portanto, no entanto, com suporte nas versões do NuGet anteriores à 2.1, planeje adequadamente para quando a transição.

## <a name="improved-search-in-package-manager-dialog"></a>Pesquisa aperfeiçoada na caixa de diálogo Gerenciador de pacotes

Ao longo de várias iterações anteriores, as alterações foram introduzidas na Galeria do NuGet que melhorou muito a velocidade e a relevância das pesquisas de pacote.  No entanto, esses aprimoramentos eram limitados para o site nuget.org.  NuGet 2.1 torna a pesquisa aperfeiçoada experiência disponível por meio da caixa de diálogo do Gerenciador de pacote do NuGet.  Por exemplo, imagine que você queira localizar o pacote de versão prévia do Windows Azure de cache.  Uma consulta de pesquisa razoável para esse pacote pode ser "Cache do Azure".  Nas versões anteriores da caixa de diálogo de Gerenciador de pacote, o pacote desejado ainda não é listado na primeira página de resultados.  No entanto, o NuGet 2.1, o pacote desejado agora aparece na parte superior dos resultados da pesquisa.

![Pesquisa de caixa de diálogo de Gerenciador de pacote](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>Forçar a atualização de pacote

Antes de 2.1 do NuGet, NuGet seria ignorar a atualização de um pacote quando havia uma não um número de versão de alta.  Essa introduzida atrito para determinados cenários – especialmente no caso de compilação ou CI cenários em que a equipe não queria incrementar o número com cada compilação de versão do pacote.  Era o comportamento desejado forçar uma atualização independentemente.  2.1 do NuGet aborda isso com o sinalizador 'reinstalar'.  Por exemplo, as versões anteriores do NuGet resultaria no seguinte ao tentar atualizar um pacote que não tem uma versão mais recente do pacote:

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

Com o sinalizador de reinstalação, o pacote será atualizado independentemente se há uma versão mais recente.

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

Outro cenário em que o sinalizador de reinstalação é vantajoso é de estrutura redirecionar. Ao alterar a estrutura de destino de um projeto (por exemplo, do .NET 4 para o .NET 4.5), Update-Package-reinstalar pode atualizar as referências aos assemblies corretos para todos os pacotes NuGet instalados no projeto.

## <a name="edit-package-sources-within-visual-studio"></a>Editar fontes de pacote dentro do Visual Studio

Nas versões anteriores do NuGet, atualizando uma origem de pacote a partir a caixa de diálogo de opções do Visual Studio necessária excluir e adicionar novamente a origem do pacote.  2.1 do NuGet melhora este fluxo de trabalho com o suporte à atualização como uma função de primeira classe da interface do usuário de configuração.

![Diálogo de configuração do Gerenciador de pacote](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Correções de Bug

2.1 do NuGet inclui muitas correções de bugs. Para obter uma lista completa de trabalho itens corrigidos no NuGet 2.0, por favor, modo de exibição de [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
