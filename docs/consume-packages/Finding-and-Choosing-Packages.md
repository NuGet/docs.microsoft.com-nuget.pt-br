---
title: Localizando e escolhendo pacotes do NuGet
description: Uma visão geral de como localizar e escolher os melhores pacotes do NuGet para um projeto, incluindo detalhes sobre a sintaxe de pesquisa do NuGet.
author: karann-msft
ms.author: karann
ms.date: 06/04/2018
ms.topic: conceptual
ms.openlocfilehash: 45928e60033959bc8b4f43d1ef3e4c943e7ec057
ms.sourcegitcommit: e02482e15c0cef63153086ed50d14f5b2a38f598
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2020
ms.locfileid: "87473851"
---
# <a name="finding-and-evaluating-nuget-packages-for-your-project"></a>Localizando e avaliando pacotes do NuGet para o seu projeto

Ao iniciar qualquer projeto .NET ou sempre que você identificar uma necessidade funcional para seu aplicativo ou serviço, você pode economizar muito tempo e problemas usando os pacotes NuGet existentes que atendem a essa necessidade. Esses pacotes podem vir da coleção pública em [nuget.org](https://www.nuget.org/packages/) ou uma origem privada que é fornecida pela sua empresa ou por terceiros.

## <a name="finding-packages"></a>Localizando os pacotes

Ao visitar o nuget.org ou abrir a interface do usuário do Gerenciador de pacotes no Visual Studio, você verá uma lista de pacotes classificados por relevância. Isso mostra os pacotes mais amplamente usados em todos os projetos .NET. Há uma boa chance de que alguns desses pacotes possam ser úteis para seus próprios projetos!

![Exibição padrão de nuget.org/packages mostrando os pacotes mais populares](media/Finding-01-Popularity.png)

Em nuget.org, observe o botão de **filtro** no canto superior direito da página. Quando clicado, o painel pesquisa avançada se expande para apresentar as opções de classificação e filtragem.

![Resultados da pesquisa para ‘json’ no nuget.org](media/Finding-02-SearchResults.png)

Você pode usar o filtro de **tipo de pacote** para mostrar pacotes de um tipo específico:
- **`All types`**: Esse é o comportamento padrão. Ele mostra todos os pacotes, independentemente de seu tipo.
- **`Dependency`**: Pacotes NuGet regulares que podem ser instalados em seu projeto.
- **`.NET tool`**: Isso filtra as [ferramentas .net](/dotnet/core/tools/global-tools), um pacote NuGet que contém um aplicativo de console.
- **`Template`**: Isso filtra os [modelos .net](/dotnet/core/install/templates), que podem ser usados para criar novos projetos usando o [`dotnet new`](/dotnet/core/tools/dotnet-new) comando.

Você pode usar a opção **classificar por** para classificar os resultados da pesquisa:
- **`Relevance`**: Esse é o comportamento padrão. Ele classifica os resultados de acordo com um algoritmo de Pontuação interno.
- **`Downloads`**: Classifica os resultados da pesquisa pelo número total de downloads, em ordem decrescente.
- **`Recently updated`**: Classifica os resultados da pesquisa pela data de criação da versão mais recente, em ordem cronológica decrescente.

Na seção **Opções** , podemos encontrar a caixa de **`Include prerelease`** seleção.
Quando marcada, nuget.org mostra todas as versões de pacotes, incluindo versões prévias. Para mostrar apenas as versões estáveis, desmarque a opção.

Para aplicar os filtros de pesquisa, clique no **`Apply`** botão. Você sempre pode retornar ao comportamento padrão clicando no **`Reset`** botão.

Você também pode usar a [sintaxe de pesquisa](#search-syntax) para filtrar marcas, proprietários e IDs de pacote.

### <a name="does-the-package-support-my-projects-target-framework"></a>O pacote é compatível com a estrutura de destino do meu projeto?

O NuGet instala um pacote em um projeto somente se estruturas compatíveis do pacote incluem a estrutura de destino do projeto. Se o pacote não for compatível, o NuGet emitirá um erro.

Alguns pacotes listam suas estruturas compatíveis diretamente na galeria do nuget.org, mas como esses dados não são necessários, muitos pacotes não incluem essa lista. No momento, não há nenhuma maneira de pesquisar pacotes no nuget.org compatível com uma estrutura de destino específica (tal recurso está em avaliação, consulte [Problema do NuGet 2936](https://github.com/NuGet/NuGetGallery/issues/2936)).

Felizmente, é possível determinar estruturas compatíveis por meio de dois outros meios:

1. Tente instalar um pacote em um projeto usando o [`Install-Package`](../reference/ps-reference/ps-ref-install-package.md) comando no console do Gerenciador de pacotes NuGet. Se o pacote for incompatível, este comando mostrará as estruturas compatíveis com o pacote.

1. Baixe o pacote da sua página no nuget.org usando o link de **Download manual** em **Informações**. Altere a extensão de `.nupkg` para `.zip` e abra o arquivo para examinar o conteúdo da sua pasta `lib`. Lá você verá as subpastas para cada estrutura compatível, em que cada subpasta é chamada com um moniker da estrutura de destino (TFM; veja [Estruturas de destino](../reference/target-frameworks.md)). Se você não encontrar nenhuma subpasta em `lib` e apenas uma única DLL, será preciso tentar instalar o pacote no seu projeto para descobrir a compatibilidade dele.

## <a name="pre-release-packages"></a>Pacotes de pré-lançamento

Muitos autores de pacote disponibilizam versões prévias e betas ao continuar a implementar melhorias e buscam comentários sobre as revisões mais recentes.

Por padrão, o nuget.org mostra pacotes de pré-lançamento nos resultados da pesquisa. Para pesquisar apenas as versões estáveis, desmarque a opção **incluir pré-lançamento** no painel pesquisa avançada que é acessível no botão de **filtro** no canto superior direito da página

![Incluir caixa de seleção do pré-lançamento no nuget.org](media/Finding-06-include-prerelease.png)

No Visual Studio e ao usar a CLI do NuGet e ferramentas da CLI dotnet, o NuGet não inclui as versões de pré-lançamento por padrão. Para alterar esse comportamento, execute as etapas a seguir:

- **Interface do usuário do Gerenciador de Pacotes no Visual Studio**: na interface do usuário **Gerenciar pacotes do NuGet**, defina a caixa **Incluir pré-lançamento**. Definir ou desmarcar esta caixa atualiza a interface do usuário do Gerenciador de Pacotes e a lista de versões disponíveis que você pode instalar.

    ![A caixa de seleção Incluir pré-lançamento no Visual Studio](media/Prerelease_02-CheckPrerelease.png)

- **Console do Gerenciador de pacotes**: Use a `-IncludePrerelease` opção com os `Find-Package` comandos,, `Get-Package` `Install-Package` , `Sync-Package` e `Update-Package` . Consulte a [Referência do PowerShell](../reference/powershell-reference.md).

- **CLI donuget.exe**: Use a `-prerelease` opção com `install` os `update` comandos,, `delete` e `mirror` . Consulte a [referência da CLI do NuGet](../reference/nuget-exe-cli-reference.md)

- **CLI dotnet.exe**: especifique a versão de pré-lançamento exata usando o argumento `-v`. Veja a [referência de dotnet add package](/dotnet/core/tools/dotnet-add-package).

<a name="native-cpp-packages"></a>

### <a name="native-c-packages"></a>Pacotes C++ nativos

O NuGet é compatível com pacotes C++ nativos que podem ser usados em projetos C++ no Visual Studio. Isso habilite o comando de menu de contexto **Gerenciar pacotes do NuGet** para projetos, apresenta uma estrutura de destino `native` e fornece integração com o MSBuild.

Para localizar pacotes nativos no [nuget.org](https://www.nuget.org/packages), pesquise usando `tag:native`. Esses pacotes normalmente fornecem arquivos `.targets` e `.props`, que o NuGet importa automaticamente quando o pacote é adicionado a um projeto.

## <a name="evaluating-packages"></a>Avaliando pacotes

A melhor maneira de avaliar a utilidade de um pacote é baixá-lo e testá-lo no seu código (a propósito, todos os pacotes do nuget.org são verificados rotineiramente em busca de vírus). Afinal, cada pacote popular começou sendo usado por apenas alguns desenvolvedores e você pode ser um dos usuários pioneiros.

Por outro lado, usar um pacote do NuGet significa assumir uma dependência, por isso é útil garantir que ele seja robusto e confiável. Visto que instalar e testar diretamente de um pacote é algo demorado, também é possível aprender muito sobre a qualidade do pacote usando as informações na página de listagem do pacote:

- *Estatísticas de downloads*: na página do pacote em nuget.org, a seção **Estatísticas** mostra o total de downloads, downloads da versão mais recente e média de downloads por dia. Números maiores indicam que muitos outros desenvolvedores adotaram uma dependência no pacote, o que significa que ele já se provou.

    ![Baixar estatísticas em uma página de listagem do pacote](media/Finding-03-Downloads.png)

- *Uso do GitHub*: na página pacote, a seção **uso do GitHub** lista os repositórios GitHub públicos que dependem deste pacote e que têm um número alto de estrelas no github. O número de estrelas de um repositório GitHub geralmente indica o quão popular esse repositório está com os usuários do GitHub (mais estrelas geralmente significa mais popular). Visite a [página de introdução do GitHub](https://help.github.com/en/github/getting-started-with-github/saving-repositories-with-stars#about-stars) para obter mais informações sobre o sistema de classificação de estrela e de repositório do github.

    ![Uso do GitHub](media/GitHub-Usage.png)

    > [!Note]
    > A seção de uso do GitHub de um pacote é gerada automaticamente, periodicamente, sem revisão humana de repositórios individuais e unicamente para fins informativos a fim de mostrar os repositórios do GitHub que dependem do pacote e que são populares com os usuários do GitHub.

- *Histórico de versão*: na página do pacote, procure em **Informações** pela data da atualização mais recente e examine o **Histórico de versão**. Um pacote com boa manutenção tem atualizações recentes e um histórico de versões detalhado. Pacotes inativos têm algumas atualizações e geralmente não foram atualizados há algum tempo.

    ![Histórico de versão na página de listagem do pacote](media/Finding-04-VersionHistory.png)

- *Instalações recentes*: na página pacote em **estatísticas**, selecione **exibir estatísticas completas**. A página de estatísticas completas mostra que o pacote é instalado nas últimas seis semanas por número de versão. Um pacote que outros desenvolvedores estão usando ativamente normalmente é uma escolha melhor do que aqueles que não estão sendo usados.

- *Suporte*: na página do pacote em **Informações**, selecione **Site do Projeto** (se disponível) para ver quais opções de suporte o autor oferece. Um projeto com um site dedicado geralmente tem melhor suporte.

- *Histórico de desenvolvedor*: na página do pacote em **Proprietários**, selecione um proprietário para ver quais outros pacotes ele publicou. Aquelas com vários pacotes têm maior probabilidade de serem compatíveis com o trabalho no futuro.

- *Contribuições de software livre*: muitos pacotes são mantidos em repositórios de software livre, tornando possível para os desenvolvedores que dependem deles contribuir diretamente com correções de bugs e melhorias de recursos. O histórico de contribuição de qualquer pacote especificado também é um bom indicador de como muitos desenvolvedores estão ativamente envolvidos.

- *Entrevistar os proprietários*: novos desenvolvedores certamente podem estar igualmente comprometidos em produzir pacotes ótimos para você usar, é recomendável dar a eles uma chance de trazer novidades para o ecossistema do NuGet. Considerando isso, entre em contato diretamente com os desenvolvedores do pacote por meio da opção **Contatar os Proprietários** em **Informações** na página da listagem. Provavelmente eles terão prazer em trabalhar junto com você para atender as suas necessidades.

- *Prefixos de ID de pacote reservados*: vários proprietários de pacote solicitaram e receberam um [prefixo de ID de pacote reservado](../nuget-org/id-prefix-reservation.md). Quando a marca de seleção visual aparecer ao lado de uma ID de pacote em [nuget.org](https://www.nuget.org/), ou no Visual Studio, isso significará que o proprietário do pacote atingiu nossos [critérios](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria) para a reserva de ID de prefixo. Isso significa que o proprietário do pacote está sendo claro ao realizar a sua identificação e a do pacote.

> [!Note]
> Sempre fique atento aos termos de licença de um pacote, que você pode ver selecionando **informações de licença** na página de listagem de um pacote em NuGet.org. Se um pacote não especificar os termos de licença, contate o proprietário do pacote diretamente usando o link **proprietários de contato** na página pacote. A Microsoft não licencia nenhuma propriedade intelectual para você de provedores de pacotes de terceiros, nem é responsável pelas informações fornecidas por terceiros.

## <a name="license-url-deprecation"></a>Substituição da URL da licença
Com a transição de [licenseUrl](../reference/nuspec.md#licenseurl) para [license](../reference/nuspec.md#license), alguns clientes do NuGet e feeds do NuGet podem não ter a capacidade de exibir as informações de licenciamento em alguns casos. Para manter a compatibilidade com versões anteriores, a URL da licença aponta para este documento que fala sobre como recuperar as informações da licença nesses casos.

Se você foi direcionado para esta página depois de clicar na URL, significa que o pacote contém um arquivo de licença e
* Você está conectado a um feed que ainda não sabe como interpretar e revelar novas informações de licença para o cliente **OU**
* Você está usando um cliente que ainda não sabe como interpretar e ler as novas informações de licença que são potencialmente fornecidas pelo feed **OU**
* Uma combinação de ambos os casos

Veja como você pode ler as informações contidas no arquivo de licença dentro do pacote:
1. Baixe o pacote NuGet e descompacte o conteúdo para uma pasta.
1. Abra o arquivo `.nuspec` que estaria na raiz da pasta.
1. Ele deve ter uma marca como `<license type="file">license\license.txt</license>`. Isso significa que o arquivo de licença se chama `license.txt` e está dentro de uma pasta denominada `license` que também estaria na raiz dessa pasta.
1. Navegue até a pasta `license` e abra o aquivo `license.txt`.

Para o MSBuild equivalente a definir a licença no `.nuspec`, confira [Empacotamento de uma expressão de licença ou um arquivo de licença](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file).

## <a name="search-syntax"></a>Sintaxe de pesquisa

A pesquisa de pacote do NuGet funciona da mesma forma no nuget.org, na CLI do NuGet e dentro da extensão do Gerenciador de Pacotes do NuGet no Visual Studio. Em geral, a pesquisa é aplicada a palavras-chave, bem como descrições de pacote.

- **Filtragem**: você pode aplicar um termo de pesquisa a uma propriedade específica usando a sintaxe `<property>:<term>` onde `<property>` (não diferencia maiúsculas de minúsculas) pode ser `id` ,,,,,, `packageid` `version` `title` `tags` `author` `description` , `summary` e `owner` . Você pode pesquisar várias propriedades ao mesmo tempo. As pesquisas na `id` propriedade são correspondências de subcadeias de caracteres, enquanto `packageid` e `owner` usa uma correspondência exata, que não diferencia maiúsculas de minúsculas. Exemplos:

```
PackageId:jquery             # Match the package ID in an exact, case-insensitive manner

owner:microsoft              # Match the owner in an exact, case-insensitive manner

id:NuGet.Core                # Match any part of the ID property
Id:"Nuget.Core"
ID:jQuery
id:jquery id:ui              # Search for multiple terms in the ID
id:jquery tags:validation    # Search multiple properties

invalid:jquery ui            # Unsupported properties are ignored, so this
                             # is the same as searching on ui
```
