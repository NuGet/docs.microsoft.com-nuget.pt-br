---
title: Localizando e escolhendo pacotes do NuGet
description: Uma visão geral de como localizar e escolher os melhores pacotes do NuGet para um projeto, incluindo detalhes sobre a sintaxe de pesquisa do NuGet.
author: karann-msft
ms.author: karann
ms.date: 06/04/2018
ms.topic: conceptual
ms.openlocfilehash: 8cd7529c4a1ecf659abde03fb1632e26431aebf3
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426747"
---
# <a name="finding-and-evaluating-nuget-packages-for-your-project"></a>Localizando e avaliando pacotes do NuGet para o seu projeto

Ao iniciar qualquer projeto .NET ou sempre que você identificar uma necessidade funcional para seu aplicativo ou serviço, você pode economizar muito tempo e problemas usando os pacotes NuGet existentes que atendem a essa necessidade. Esses pacotes podem vir da coleção pública em [nuget.org](http://www.nuget.org/packages/) ou uma origem privada que é fornecida pela sua empresa ou por terceiros.

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

1. Tentativa de instalar um pacote em um projeto usando o comando [`Install-Package`](../tools/ps-ref-install-package.md) no Console do Gerenciador de Pacotes do NuGet. Se o pacote for incompatível, este comando mostrará as estruturas compatíveis com o pacote.

1. Baixe o pacote da sua página no nuget.org usando o link de **Download manual** em **Informações**. Altere a extensão de `.nupkg` para `.zip` e abra o arquivo para examinar o conteúdo da sua pasta `lib`. Lá você verá as subpastas para cada estrutura compatível, em que cada subpasta é chamada com um moniker da estrutura de destino (TFM; veja [Estruturas de destino](../reference/target-frameworks.md)). Se você não encontrar nenhuma subpasta em `lib` e apenas uma única DLL, será preciso tentar instalar o pacote no seu projeto para descobrir a compatibilidade dele.

## <a name="pre-release-packages"></a>Pacotes de pré-lançamento

Muitos autores de pacote disponibilizam versões prévias e betas ao continuar a implementar melhorias e buscam comentários sobre as revisões mais recentes.

Por padrão, o nuget.org mostra pacotes de pré-lançamento nos resultados da pesquisa. Para pesquisar apenas as versões estáveis, desmarque a opção **Incluir pré-lançamento** no canto superior direito da página

![Incluir caixa de seleção do pré-lançamento no nuget.org](media/Finding-06-include-prerelease.png)

No Visual Studio e ao usar a CLI do NuGet e ferramentas da CLI dotnet, o NuGet não inclui as versões de pré-lançamento por padrão. Para alterar esse comportamento, execute as etapas a seguir:

- **Interface do Usuário do Gerenciador de Pacotes no Visual Studio**: Na interface do usuário **Gerenciar Pacotes NuGet**, defina a caixa **Incluir pré-lançamento**. Definir ou desmarcar esta caixa atualiza a interface do usuário do Gerenciador de Pacotes e a lista de versões disponíveis que você pode instalar.

    ![A caixa de seleção Incluir pré-lançamento no Visual Studio](media/Prerelease_02-CheckPrerelease.png)

- **Console do Gerenciador de Pacotes**: Use a opção `-IncludePrerelease` com os comandos `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package` e `Update-Package`. Consulte a [Referência do PowerShell](../tools/powershell-reference.md).

- **CLI do nuget.exe**: Use a opção `-prerelease` com os comandos `install`, `update`, `delete` e `mirror`. Consulte a [referência da CLI do NuGet](../tools/nuget-exe-cli-reference.md)

- **CLI do dotnet.exe**: Especifique a versão de pré-lançamento exata usando o argumento `-v`. Veja a [referência de dotnet add package](/dotnet/core/tools/dotnet-add-package).

<a name="native-cpp-packages"></a>

### <a name="native-c-packages"></a>Pacotes C++ nativos

O NuGet é compatível com pacotes C++ nativos que podem ser usados em projetos C++ no Visual Studio. Isso habilite o comando de menu de contexto **Gerenciar pacotes do NuGet** para projetos, apresenta uma estrutura de destino `native` e fornece integração com o MSBuild.

Para localizar pacotes nativos no [nuget.org](https://www.nuget.org/packages), pesquise usando `tag:native`. Esses pacotes normalmente fornecem arquivos `.targets` e `.props`, que o NuGet importa automaticamente quando o pacote é adicionado a um projeto.

## <a name="evaluating-packages"></a>Avaliando pacotes

A melhor maneira de avaliar a utilidade de um pacote é baixá-lo e testá-lo no seu código (a propósito, todos os pacotes do nuget.org são verificados rotineiramente em busca de vírus). Afinal, cada pacote popular começou sendo usado por apenas alguns desenvolvedores e você pode ser um dos usuários pioneiros.

Por outro lado, usar um pacote do NuGet significa assumir uma dependência, por isso é útil garantir que ele seja robusto e confiável. Visto que instalar e testar diretamente de um pacote é algo demorado, também é possível aprender muito sobre a qualidade do pacote usando as informações na página de listagem do pacote:

- *Estatísticas de downloads*: na página do pacote em nuget.org, a seção **Estatísticas** mostra o total de downloads, downloads da versão mais recente e média de downloads por dia. Números maiores indicam que muitos outros desenvolvedores adotaram uma dependência no pacote, o que significa que ele já se provou.

    ![Baixar estatísticas em uma página de listagem do pacote](media/Finding-03-Downloads.png)

- *Histórico de versão*: na página do pacote, procure em **Informações** pela data da atualização mais recente e examine o **Histórico de versão**. Um pacote com boa manutenção tem atualizações recentes e um histórico de versões detalhado. Pacotes inativos têm algumas atualizações e geralmente não foram atualizados há algum tempo.

    ![Histórico de versão na página de listagem do pacote](media/Finding-04-VersionHistory.png)

- *Instalações recentes*: na página do pacote em **Estatísticas**, selecione **Exibir as estatísticas completas**. A página de estatísticas total mostra as instalações do pacote nas últimas seis semanas pelo número de versão. Um pacote que outros desenvolvedores estão usando ativamente normalmente é uma escolha melhor do que aqueles que não estão sendo usados.

- *Suporte*: na página do pacote em **Informações**, selecione **Site do Projeto** (se disponível) para ver quais opções de suporte o autor oferece. Um projeto com um site dedicado geralmente tem melhor suporte.

- *Histórico de desenvolvedor*: na página do pacote em **Proprietários**, selecione um proprietário para ver quais outros pacotes ele publicou. Aquelas com vários pacotes têm maior probabilidade de serem compatíveis com o trabalho no futuro.

- *Contribuições de software livre*: muitos pacotes são mantidos em repositórios de software livre, tornando possível para os desenvolvedores que dependem deles contribuir diretamente com correções de bugs e melhorias de recursos. O histórico de contribuição de qualquer pacote especificado também é um bom indicador de como muitos desenvolvedores estão ativamente envolvidos.

- *Entrevistar os proprietários*: novos desenvolvedores certamente podem estar igualmente comprometidos em produzir pacotes ótimos para você usar, é recomendável dar a eles uma chance de trazer novidades para o ecossistema do NuGet. Considerando isso, entre em contato diretamente com os desenvolvedores do pacote por meio da opção **Contatar os Proprietários** em **Informações** na página da listagem. Provavelmente eles terão prazer em trabalhar junto com você para atender as suas necessidades.

- *Prefixos de ID de pacote reservados*: vários proprietários de pacote solicitaram e receberam um [prefixo de ID de pacote reservado](../nuget-org/id-prefix-reservation.md). Quando a marca de seleção visual aparecer ao lado de uma ID de pacote em [nuget.org](https://www.nuget.org/), ou no Visual Studio, isso significará que o proprietário do pacote atingiu nossos [critérios](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria) para a reserva de ID de prefixo. Isso significa que o proprietário do pacote está sendo claro ao realizar a sua identificação e a do pacote.

> [!Note]
> Sempre preste atenção aos termos de licença de um pacote, que você pode ver selecionando **Informações de Licença** na página de listagem do pacote no nuget.org. Se um pacote não especificar os termos de licença, entre em contato com o proprietário do pacote diretamente usando o link **Contatar os proprietários** na página do pacote. A Microsoft não licencia nenhuma propriedade intelectual para você de provedores de pacotes de terceiros, nem é responsável pelas informações fornecidas por terceiros.

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


## <a name="search-syntax"></a>Sintaxe de pesquisa

A pesquisa de pacote do NuGet funciona da mesma forma no nuget.org, na CLI do NuGet e dentro da extensão do Gerenciador de Pacotes do NuGet no Visual Studio. Em geral, a pesquisa é aplicada a palavras-chave, bem como descrições de pacote.

- **Palavras-chave**: A pesquisa procura pacotes relevantes que contêm uma das palavras-chaves fornecidas. Exemplo: `modern UI`. Para pesquisar pacotes que contêm todas as palavras-chave fornecidas, use "+" entre os termos, como `modern+UI`.
- **Frases**: A inserção de termos entre aspas procura a correspondência exata desses termos, sem diferenciar maiúsculas de minúsculas. Exemplo: `"modern UI" package`
- **Filtragem**: Você pode aplicar um termo de pesquisa a uma propriedade específica usando a sintaxe `<property>:<term>`, em que `<property>` (não diferencia maiúsculas de minúsculas) pode ser `id`, `packageid`, `version`, `title`, `tags`, `author`, `description`, `summary` e `owner`. Os termos podem estar contidos em aspas, se necessário e você pode pesquisar por várias propriedades ao mesmo tempo. Além disso, a pesquisa na propriedade `id` são correspondências de subcadeia de caracteres, enquanto `packageid` usa uma correspondência exata. Exemplos:

    ```
    id:NuGet.Core                # Match any part of the id property
    Id:"Nuget.Core"
    ID:jQuery
    title:jquery                 # Searches title as shown on the package listing
    PackageId:jquery             # Match the package id exactly
    id:jquery id:ui              # Search for multiple terms in the id
    id:jquery tags:validation    # Search multiple properties
    id:"jquery.ui"               # Phrase search
    invalid:jquery ui            # Unsupported properties are ignored, so this
                                 # is the same as searching on jquery ui
    ```
