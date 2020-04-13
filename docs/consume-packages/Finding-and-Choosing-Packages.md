---
title: Localizando e escolhendo pacotes do NuGet
description: Uma visão geral de como localizar e escolher os melhores pacotes do NuGet para um projeto, incluindo detalhes sobre a sintaxe de pesquisa do NuGet.
author: karann-msft
ms.author: karann
ms.date: 06/04/2018
ms.topic: conceptual
ms.openlocfilehash: 9f427005251bc2bf7a8a79285e39b4bd49062dbf
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428852"
---
# <a name="finding-and-evaluating-nuget-packages-for-your-project"></a>Localizando e avaliando pacotes do NuGet para o seu projeto

Ao iniciar qualquer projeto .NET ou sempre que você identificar uma necessidade funcional para seu aplicativo ou serviço, você pode economizar muito tempo e problemas usando os pacotes NuGet existentes que atendem a essa necessidade. Esses pacotes podem vir da coleção pública em [nuget.org](https://www.nuget.org/packages/) ou uma origem privada que é fornecida pela sua empresa ou por terceiros.

## <a name="finding-packages"></a>Localizando os pacotes

Quando você visita nuget.org ou abre a interface do usuário do Gerenciador de Pacotes no Visual Studio, verá uma lista de pacotes classificados por total de downloads. Isso imediatamente mostra os pacotes mais usados em milhões de projetos do .NET. Há uma boa chance de que pelo menos alguns dos pacotes listados nas primeiras páginas sejam úteis para seus projetos.

![Exibição padrão de nuget.org/packages mostrando os pacotes mais populares](media/Finding-01-Popularity.png)

Observe a opção **Incluir pré-lançamento** no canto superior direito da página. Quando selecionado, o nuget.org mostra todas as versões de pacotes, inclusive beta e as outras versões iniciais. Para mostrar apenas versões estáveis, desmarque a opção.

Para necessidades específicas, pesquisar por marcas (dentro do Gerenciador de Pacotes do Visual Studio ou em um portal como o nuget.org) é o meio mais comum de descobrir um pacote adequado. Por exemplo, pesquisar por “json” lista todos os pacotes do NuGet que estão marcados com essa palavra-chave e, portanto, têm alguma relação com o formato de dados JSON.

![Resultados da pesquisa para ‘json’ no nuget.org](media/Finding-02-SearchResults.png)

Você também pode pesquisar usando a ID de pacote, se conhecê-la. Consulte [Sintaxe de pesquisa](#search-syntax) abaixo.

Neste momento, os resultados da pesquisa são classificados somente por relevância, por isso geralmente é recomendável olhar pelo menos as primeiras páginas de resultados em busca de pacotes que atendam às suas necessidades ou refinar os termos de pesquisa para serem mais específicos.

### <a name="does-the-package-support-my-projects-target-framework"></a>O pacote é compatível com a estrutura de destino do meu projeto?

O NuGet instala um pacote em um projeto somente se estruturas compatíveis do pacote incluem a estrutura de destino do projeto. Se o pacote não for compatível, o NuGet emitirá um erro.

Alguns pacotes listam suas estruturas compatíveis diretamente na galeria do nuget.org, mas como esses dados não são necessários, muitos pacotes não incluem essa lista. No momento, não há nenhuma maneira de pesquisar pacotes no nuget.org compatível com uma estrutura de destino específica (tal recurso está em avaliação, consulte [Problema do NuGet 2936](https://github.com/NuGet/NuGetGallery/issues/2936)).

Felizmente, é possível determinar estruturas compatíveis por meio de dois outros meios:

1. Tente instalar um pacote em [`Install-Package`](../reference/ps-reference/ps-ref-install-package.md) um projeto usando o comando no Console Do Gerenciador de Pacotes NuGet. Se o pacote for incompatível, este comando mostrará as estruturas compatíveis com o pacote.

1. Baixe o pacote da sua página no nuget.org usando o link de **Download manual** em **Informações**. Altere a extensão de `.nupkg` para `.zip` e abra o arquivo para examinar o conteúdo da sua pasta `lib`. Lá você verá as subpastas para cada estrutura compatível, em que cada subpasta é chamada com um moniker da estrutura de destino (TFM; veja [Estruturas de destino](../reference/target-frameworks.md)). Se você não encontrar nenhuma subpasta em `lib` e apenas uma única DLL, será preciso tentar instalar o pacote no seu projeto para descobrir a compatibilidade dele.

## <a name="pre-release-packages"></a>Pacotes de pré-lançamento

Muitos autores de pacote disponibilizam versões prévias e betas ao continuar a implementar melhorias e buscam comentários sobre as revisões mais recentes.

Por padrão, o nuget.org mostra pacotes de pré-lançamento nos resultados da pesquisa. Para pesquisar apenas as versões estáveis, desmarque a opção **Incluir pré-lançamento** no canto superior direito da página

![Incluir caixa de seleção do pré-lançamento no nuget.org](media/Finding-06-include-prerelease.png)

No Visual Studio e ao usar a CLI do NuGet e ferramentas da CLI dotnet, o NuGet não inclui as versões de pré-lançamento por padrão. Para alterar esse comportamento, execute as etapas a seguir:

- **Interface do usuário do Gerenciador de Pacotes no Visual Studio**: na interface do usuário **Gerenciar pacotes do NuGet**, defina a caixa **Incluir pré-lançamento**. Definir ou desmarcar esta caixa atualiza a interface do usuário do Gerenciador de Pacotes e a lista de versões disponíveis que você pode instalar.

    ![A caixa de seleção Incluir pré-lançamento no Visual Studio](media/Prerelease_02-CheckPrerelease.png)

- **Console do gerenciador de**pacotes `Install-Package` `Sync-Package`: `Update-Package` Use o `-IncludePrerelease` interruptor com os `Find-Package`comandos , `Get-Package`e os comandos. Consulte a [Referência do PowerShell](../reference/powershell-reference.md).

- **nuget.exe CLI**: `-prerelease` Use `install`o `update` `delete`interruptor `mirror` com os comandos , e comandos. Consulte a [referência da CLI do NuGet](../reference/nuget-exe-cli-reference.md)

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

- *Uso do GitHub*: na página do pacote, a seção Uso do **GitHub** lista repositórios públicos do GitHub que dependem deste pacote e que têm um alto número de estrelas no GitHub. O número de estrelas de um repositório do GitHub geralmente indica o quão popular esse repositório é com os usuários do GitHub (mais estrelas geralmente significam mais popular). Visite a [página Getting Started do GitHub](https://help.github.com/en/github/getting-started-with-github/saving-repositories-with-stars#about-stars) para obter mais informações sobre o sistema de classificação de estrelas e repositórios do GitHub.

    ![Uso do GitHub](media/GitHub-Usage.png)

    > [!Note]
    > A seção de uso do GitHub de um pacote é gerada automaticamente, periodicamente, sem revisão humana de repositórios individuais e exclusivamente para fins informativos, a fim de mostrar-lhe repositórios do GitHub que dependem do pacote e que são populares entre os usuários do GitHub.

- *Histórico de versão*: na página do pacote, procure em **Informações** pela data da atualização mais recente e examine o **Histórico de versão**. Um pacote com boa manutenção tem atualizações recentes e um histórico de versões detalhado. Pacotes inativos têm algumas atualizações e geralmente não foram atualizados há algum tempo.

    ![Histórico de versão na página de listagem do pacote](media/Finding-04-VersionHistory.png)

- *Instalações recentes*: na página do pacote em **Estatísticas,** selecione **Exibir estatísticas completas**. A página de estatísticas completa mostra as instalações do pacote nas últimas seis semanas por número da versão. Um pacote que outros desenvolvedores estão usando ativamente normalmente é uma escolha melhor do que aqueles que não estão sendo usados.

- *Suporte*: na página do pacote em **Informações**, selecione **Site do Projeto** (se disponível) para ver quais opções de suporte o autor oferece. Um projeto com um site dedicado geralmente tem melhor suporte.

- *Histórico de desenvolvedor*: na página do pacote em **Proprietários**, selecione um proprietário para ver quais outros pacotes ele publicou. Aquelas com vários pacotes têm maior probabilidade de serem compatíveis com o trabalho no futuro.

- *Contribuições de software livre*: muitos pacotes são mantidos em repositórios de software livre, tornando possível para os desenvolvedores que dependem deles contribuir diretamente com correções de bugs e melhorias de recursos. O histórico de contribuição de qualquer pacote especificado também é um bom indicador de como muitos desenvolvedores estão ativamente envolvidos.

- *Entrevistar os proprietários*: novos desenvolvedores certamente podem estar igualmente comprometidos em produzir pacotes ótimos para você usar, é recomendável dar a eles uma chance de trazer novidades para o ecossistema do NuGet. Considerando isso, entre em contato diretamente com os desenvolvedores do pacote por meio da opção **Contatar os Proprietários** em **Informações** na página da listagem. Provavelmente eles terão prazer em trabalhar junto com você para atender as suas necessidades.

- *Prefixos de ID de pacote reservados*: vários proprietários de pacote solicitaram e receberam um [prefixo de ID de pacote reservado](../nuget-org/id-prefix-reservation.md). Quando a marca de seleção visual aparecer ao lado de uma ID de pacote em [nuget.org](https://www.nuget.org/), ou no Visual Studio, isso significará que o proprietário do pacote atingiu nossos [critérios](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria) para a reserva de ID de prefixo. Isso significa que o proprietário do pacote está sendo claro ao realizar a sua identificação e a do pacote.

> [!Note]
> Esteja sempre atento aos termos de licença de um pacote, que você pode ver selecionando Informações de **Licença** na página de listagem de um pacote no nuget.org. Se um pacote não especificar os termos da licença, entre em contato diretamente com o proprietário do pacote usando o link **Contatos proprietários** na página do pacote. A Microsoft não licencia nenhuma propriedade intelectual para você de provedores de pacotes de terceiros, nem é responsável pelas informações fornecidas por terceiros.

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

- **Filtragem**: Você pode aplicar um termo de pesquisa `<property>:<term>` a `<property>` uma propriedade específica usando `id` `packageid`a `version` `title`sintaxe onde (caso-insensível) pode ser , , , , `tags` `author`, , `description`, , e `summary`. `owner` Você pode procurar por várias propriedades ao mesmo tempo. As pesquisas `id` na propriedade são correspondências de substring, enquanto `packageid` e `owner` usa uma correspondência exata e insensível ao caso. Exemplos:

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
