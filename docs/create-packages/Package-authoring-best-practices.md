---
title: Práticas recomendadas de criação de pacote
description: Um guia Geral das práticas recomendadas para a criação de pacotes NuGet de alta qualidade.
author: chgill-MSFT
ms.author: chgill
ms.date: 09/17/2020
ms.topic: conceptual
ms.openlocfilehash: 35eb000bddaa58726857cd3c1fd2362917f83196
ms.sourcegitcommit: c19d398cecee3cad2d79a8b22650fc1988d41a3f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2021
ms.locfileid: "99420853"
---
# <a name="package-authoring-best-practices"></a>Práticas recomendadas de criação de pacote

Este guia destina-se a dar aos autores de pacote NuGet uma referência leve para criar e publicar pacotes de alta qualidade. Ele se concentrará principalmente nas práticas recomendadas específicas do pacote, como metadados e empacotamento. Para obter sugestões mais detalhadas para a criação de bibliotecas de alta qualidade, consulte a [orientação da biblioteca](https://docs.microsoft.com/dotnet/standard/library-guidance/)de software livre .net.

## <a name="types-of-recommendations"></a>Tipos de recomendações

Cada artigo apresenta quatro tipos de recomendação: **Fazer**, **Considerar**, **Evitar** e **Não fazer**. O tipo de recomendação indica com que precisão ele deve ser seguido.

Procure quase sempre seguir a recomendação **Fazer**. Por exemplo: 

✔️ incluem uma breve descrição do pacote que descreve o que ele é para o.

Por outro lado, **considere** as recomendações que, em geral, devem ser seguidas, mas há exceções legítimas para a regra:

✔️ CONSIDERE escolher um nome de pacote do NuGet com um prefixo que cumpra os [critérios](https://docs.microsoft.com/nuget/reference/id-prefix-reservation) de reserva de prefixo do NuGet.

As recomendações **Evitar** mencionam coisas que em geral não são ideais, mas há casos em que, às vezes, quebrar a regra faz sentido:

❌ Evite as referências de pacote NuGet que exigem uma versão exata.

Por fim, as recomendações **Não fazer** indicam algo que você quase nunca deve fazer:

❌ Não use a `LicenseUrl` Propriedade Metadata.

## <a name="create-a-nuget-package"></a>Criar um pacote NuGet

A maneira mais recente recomendada para criar um pacote NuGet é de um [projeto no estilo SDK](https://docs.microsoft.com/nuget/resources/check-project-format). As propriedades do projeto no estilo SDK, incluindo a [estrutura de destino](https://docs.microsoft.com/dotnet/standard/frameworks) e os [metadados do pacote](#package-metadata), são definidas no arquivo do [projeto](https://docs.microsoft.com/visualstudio/ide/solutions-and-projects-in-visual-studio#project-file).

Crie um pacote do seu projeto no estilo do SDK definindo as propriedades necessárias e as embalagens no [Visual Studio](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli) ou na [CLI do dotnet](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli).

✔️ criar um projeto no estilo SDK e criar (Pack) seu pacote usando o Visual Studio ou a CLI do dotnet.

Para obter diretrizes mais detalhadas sobre a criação de pacotes, incluindo ferramentas de cliente necessárias, exemplo de arquivo de projeto e comandos, consulte [criar um pacote NuGet usando a CLI dotnet](https://docs.microsoft.com/nuget/create-packages/creating-a-package-dotnet-cli).

Para ajudar a decidir quais .NET Frameworks direcionar, consulte nossas [diretrizes mais recentes para direcionamento de plataforma cruzada](https://docs.microsoft.com/dotnet/standard/library-guidance/cross-platform-targeting).

## <a name="package-metadata"></a>Metadados de pacote

Metadata é um componente fundamental de qualquer pacote NuGet. A qualidade de seus metadados pode influenciar imensamente a descoberta, a usabilidade e a confiabilidade do seu pacote.

No Visual Studio, a maneira recomendada para especificar os metadados do pacote é usar o Project > as propriedades [Project Name] > pacote.

Os elementos de metadados do pacote também podem ser [especificados diretamente no arquivo do projeto](https://docs.microsoft.com/nuget/create-packages/creating-a-package-msbuild#set-properties).

Abaixo está um mapeamento de tabela e descrevendo os elementos de metadados de pacote disponíveis:

| Nome da Propriedade do Visual Studio                   | [Nome da Propriedade do arquivo/MSBuild do projeto](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                          | [Nome da propriedade Nuspec](https://docs.microsoft.com/nuget/reference/nuspec#general-form-and-schema) | Descrição                                                                                                       |
|-----------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| [`Package id`](#package-id)                   | [`PackageId`](https://docs.microsoft.com/dotnet/core/tools/csproj#packageid)                                                            | [`id`](https://docs.microsoft.com/nuget/reference/nuspec#id)                                      | O nome ou identificador do pacote.                    |
| [`Package version`](#package-version)         | [`PackageVersion`](https://docs.microsoft.com/dotnet/core/tools/csproj#packageversion)                                                  | [`version`](https://docs.microsoft.com/nuget/reference/nuspec#version)                            | Versão do pacote NuGet.                                           |
| [`Authors`](#authors)                         | [`Authors`](https://docs.microsoft.com/dotnet/core/tools/csproj#authors)                                                                | [`authors`](https://docs.microsoft.com/nuget/reference/nuspec#authors)                            | Uma lista separada por vírgulas de autores de pacote, geralmente usando o "nome" de uma organização individual ou de uma empresa.                             |
| [`Description`](#description)                 | [`Description`](https://docs.microsoft.com/dotnet/core/tools/csproj#description)                                                        | [`description`](https://docs.microsoft.com/nuget/reference/nuspec#description)                    | Uma descrição do pacote.                                                                |
| [`Copyright`](#copyright)                     | [`Copyright`](https://docs.microsoft.com/dotnet/core/tools/csproj#copyright)                                                            | [`copyright`](https://docs.microsoft.com/nuget/reference/nuspec#copyright)                        | Detalhes sobre direitos autorais do pacote.                                                                      |
| [`Licensing - Expression`](#licensing)        | [`PackageLicenseExpression`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file) | [`license type="expression"`](https://docs.microsoft.com/nuget/reference/nuspec#license)          | Uma expressão de licença SPDX.       |
| [`Licensing - File`](#licensing)              | [`PackageLicenseFile`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)       | [`license type="file"`](https://docs.microsoft.com/nuget/reference/nuspec#license)                | Caminho para um arquivo de licença personalizado.                                               |
| [`Project URL`](#project-url)                 | `PackageProjectUrl`                                                                                                                     | [`projectUrl`](https://docs.microsoft.com/nuget/reference/nuspec#projecturl)                      | Uma URL para a página inicial do projeto.                                                                                   |
| [`Icon File`](#icon)                          | [`PackageIcon`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file)                                  | [`icon`](https://docs.microsoft.com/nuget/reference/nuspec#icon)                                  | Caminho para o arquivo de imagem do ícone de pacote.                                                                      |
| [`Repository URL`](#repository-type-and-url)  | [`RepositoryUrl`](https://docs.microsoft.com/dotnet/core/tools/csproj#repositoryurl)                                                    | [`repository url`](https://docs.microsoft.com/nuget/reference/nuspec#repository)               | URL para o repositório do qual o pacote foi criado.                                                           |
| [`Repository type`](#repository-type-and-url) | [`RespositoryType`](https://docs.microsoft.com/dotnet/core/tools/csproj#repositorytype)                                                 | [`repository type`](https://docs.microsoft.com/nuget/reference/nuspec#repository)              | Tipo de repositório ao qual a URL do repositório está apontando (ou seja, "git").                                                   |
| [`Tags`](#tags)                               | [`PackageTags`](https://docs.microsoft.com/dotnet/core/tools/csproj#packagetags)                                                        | [`tags`](https://docs.microsoft.com/nuget/reference/nuspec#tags)                                  | Uma lista delimitada por espaço de marcas e palavras-chave que descrevem o pacote. Marcas são usadas ao pesquisar pacotes. |
| [`Release notes`](#release-notes)             | [`PackageReleaseNotes`](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                                          | [`releaseNotes`](https://docs.microsoft.com/nuget/reference/nuspec#releasenotes)                  | Uma descrição das alterações feitas nesta versão do pacote.                                                 |  |

### <a name="package-id"></a>ID do Pacote

Se você estiver publicando um pacote completamente novo:

✔️ escolher uma ID de pacote que seja exclusiva e claramente diferenciada dos pacotes existentes no NuGet.org.
> Você pode verificar se uma ID de pacote é exclusiva e diferenciável pesquisando a ID em NuGet.org ou verificando se o seguinte link existe: https://www.nuget.org/packages/<package nome \> .

✔️ CONSIDERE escolher um nome de pacote NuGet com um prefixo que atenda aos [critérios de reserva de prefixo](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation#id-prefix-reservation-criteria)do NuGet.
> Reservar a ID de prefixo para seu pacote permitirá que você obtenha a marca de verificação verificada: ![ imagem](media/Verified-check-mark.png)
> 
> Confira os [documentos de reserva de prefixo da ID do pacote](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation) para saber mais.

### <a name="package-version"></a>Versão do pacote

✔️ Considere usar [SemVer](https://semver.org/) para versão do seu pacote NuGet.
> Essencialmente, isso significa usar o formato principal. Minor. patch [-pré-lançamento].

✔️ publicar um pacote como um [pacote de pré-lançamento](https://docs.microsoft.com/nuget/create-packages/prerelease-packages) se ele não for estável ou uma visualização.

Consulte o [Guia de controle de versão da biblioteca do .net](https://docs.microsoft.com/dotnet/standard/library-guidance/versioning) para obter diretrizes mais avançadas.

### <a name="authors"></a>Autores

✔️ Use o campo autor para o seu ou o "nome" de sua organização.
> Por exemplo, se meu nome de usuário do NuGet.org for "jdoe", usar "Jane Doe" para o campo autor pode ajudar os consumidores a reconhecê-lo como autor. Se o nome de usuário do NuGet.org da minha organização for "ContosoToolkit", usar "Contoso Corporation" pode ser mais reconhecível e inspirar mais confiança do consumidor.
### <a name="description"></a>Descrição

✔️ incluem uma breve descrição (até 4000 caracteres) para descrever seu pacote.
> As descrições de pacote são um dos campos mais proeminentes na pesquisa NuGet e provavelmente serão a primeira coisa que os consumidores potenciais examinam para determinar se um pacote é adequado para eles.

### <a name="copyright"></a>Direitos autorais

✔️ Considere o copyright do seu pacote com "Copyright (c) <nome/empresa \> <ano \> ".
>Um aviso de direitos autorais indica basicamente que seu trabalho não pode ser copiado sem a sua permissão. A inclusão de um aviso de direitos autorais em seu pacote é fácil e não fará nenhum dano!

Exemplo: Copyright (c) contoso 2020

### <a name="licensing"></a>Licenciamento

✔️ [incluir uma expressão de licença ou um arquivo de licença em seu pacote](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).
> [!IMPORTANT]
> Um projeto sem uma licença usa como padrão [direitos autorais exclusivos](https://choosealicense.com/no-permission/), o que significa que você não concedeu permissão a ninguém para usar seu projeto.

❌ Não use a propriedade de metadados preterida `LicenseUrl` .
> Isso apresenta uma ambiguidade legal, pois as alterações de licença na URL alterarão retroativamente a licença exibida para versões de pacotes anteriores.

#### <a name="if-your-package-is-open-source"></a>Se o seu pacote for de [código-fonte aberto](https://opensource.org/osd)

✔️ [escolher uma licença](https://choosealicense.com/) de software livre para tornar o software livre de seu pacote.
> *"Licenças de software livre são licenças que estão em conformidade com a definição de código-fonte aberto — em resumo, elas permitem que o software seja usado livremente, modificado e compartilhado".* -Iniciativa de código-fonte aberto. Para saber mais sobre software livre e a iniciativa de código-fonte aberto, confira https://opensource.org/ .

✔️ Considere [incluir uma expressão de licença em seu pacote](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).
> As expressões de licença são exibidas mais claramente e tornam-as mais óbvias para os consumidores se puderem usar seu pacote ou se a licença tiver sido alterada. 
> [!Note]
> O NuGet.org só aceita expressões de licença para licenças que são aprovadas pela iniciativa de software livre ou pela base de softwares gratuita.

#### <a name="if-your-package-is-not-open-source"></a>Se o pacote não estiver em código aberto

✔️ [inclui um arquivo de licença em seu pacote](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).
> Qualquer arquivo de licença (. txt ou. MD) pode ser adicionado ao seu pacote, incluindo licenças não padrão. 

### <a name="project-url"></a>URL de Projeto

✔️ Considere incluir um link para um projeto, repositório ou site da empresa associado.
> O site do seu projeto deve ter tudo o que os usuários precisam saber sobre seu pacote e provavelmente será onde os usuários buscam documentação.

### <a name="icon"></a>ícone

✔️ Considere a [inclusão de um ícone com seu pacote](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file) para ajudar a diferenciá-lo visualmente. É uma adição relativamente pequena que pode melhorar a percepção da qualidade do pacote.
> Os ícones podem ser específicos para pacotes individuais ou ser um logotipo de marca.

✔️ usar uma imagem que seja 128x128 e tenha um plano de fundo transparente (PNG) para obter melhor exibição dos resultados.
> O NuGet dimensionará automaticamente a imagem para o cliente em que está sendo exibida.

❌ Não use a propriedade de metadados preterida `IconUrl` .

### <a name="repository-type-and-url"></a>Tipo de repositório e URL

✔️ CONSIDERE configurar o [link de origem](https://docs.microsoft.com/dotnet/standard/library-guidance/sourcelink) para adicionar automaticamente metadados de controle do código-fonte ao seu pacote NuGet e tornar sua biblioteca mais fácil de depurar.
> O link de origem adiciona `Repository URL` e `Repository Type` para os metadados do pacote automaticamente. Ele também adiciona a confirmação específica associada à versão do pacote.

### <a name="tags"></a>Marcações

os ✔️ incluem várias marcas com os principais termos relacionados ao seu pacote para aprimorar a capacidade de descoberta.
> As marcas são levadas em conta no algoritmo de pesquisa do NuGet. org e são especialmente úteis para termos que não estão na ID do pacote, mas são relevantes.

Por exemplo, se eu publicar um pacote para registrar cadeias de caracteres no console, incluiria: "log, log, console, Cadeia de caracteres, saída"

### <a name="release-notes"></a>Notas de versão

✔️ Considere a inclusão de notas de versão com cada atualização que descreve quais alterações foram feitas.
> Embora não haja um formato específico necessário para as notas de versão, é recomendável incluir:
>
> 1. Alterações de quebra
> 2. Novos recursos
> 3. Correções de bug
> 
> Se você já acompanha as notas de versão ou um changelog em seu repositório, também pode incluir um link para o arquivo relevante.

## <a name="related-topics"></a>Tópicos relacionados

- [Criar e publicar um pacote (CLI do dotnet)](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli)
- [Criar e publicar um pacote (Visual Studio)](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli)
