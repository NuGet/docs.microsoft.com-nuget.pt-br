---
title: Práticas recomendadas de produção de pacotes
description: Um guia geral das práticas recomendadas para criar pacotes de NuGet de alta qualidade.
author: chgill-MSFT
ms.author: chgill
ms.date: 09/17/2020
ms.topic: conceptual
ms.openlocfilehash: ec1532900bed7d13ea2400afe9f855105a5c2fde
ms.sourcegitcommit: adb261dd4b2a8cd75447f7b5ea6a9e5a1a54d61d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2021
ms.locfileid: "122209885"
---
# <a name="package-authoring-best-practices"></a>Práticas recomendadas de produção de pacotes

Essa orientação destina-se a dar NuGet autores de pacote uma referência leve para criar e publicar pacotes de alta qualidade. Ele se concentrará principalmente em práticas recomendadas específicas do pacote, como metadados e empacotamento. Para obter sugestões mais detalhadas para a criação de bibliotecas de alta qualidade, consulte as diretrizes da biblioteca de [código-fonte aberto do](/dotnet/standard/library-guidance/).NET.

## <a name="types-of-recommendations"></a>Tipos de recomendações

Cada artigo apresenta quatro tipos de recomendação: **Fazer**, **Considerar**, **Evitar** e **Não fazer**. O tipo de recomendação indica o quanto ela deve ser seguida.

Procure quase sempre seguir a recomendação **Fazer**. Por exemplo:

✔️ DO inclua uma breve descrição para seu pacote que descreve para que ele se trata.

Por outro lado, considere **recomendações** geralmente devem ser seguidas, mas há exceções legítimas para a regra:

✔️ CONSIDERE escolher um nome de pacote do NuGet com um prefixo que cumpra os [critérios](../nuget-org/id-prefix-reservation.md) de reserva de prefixo do NuGet.

As recomendações **Evitar** mencionam coisas que em geral não são ideais, mas há casos em que, às vezes, quebrar a regra faz sentido:

❌EVITE NuGet de pacote que exigem uma versão exata.

Por fim, as recomendações **Não fazer** indicam algo que você quase nunca deve fazer:

❌ NÃO use a propriedade `LicenseUrl` de metadados.

## <a name="create-a-nuget-package"></a>Criar um pacote NuGet

A maneira recomendada mais recente de criar um NuGet é de um [projeto no estilo SDK](../resources/check-project-format.md). As propriedades do projeto no estilo SDK, incluindo a estrutura [de destino e](/dotnet/standard/frameworks) os [metadados do](#package-metadata)pacote, são definidas no arquivo de [projeto](/visualstudio/ide/solutions-and-projects-in-visual-studio#project-file).

Crie um pacote do seu projeto no estilo SDK definindo as propriedades necessárias e empacotando no Visual Studio [ou](../quickstart/create-and-publish-a-package-using-visual-studio.md?tabs=netcore-cli) na [CLI do dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

✔️ CRIE um projeto no estilo SDK e crie (empacote) seu pacote usando Visual Studio ou a CLI do dotnet.

Para obter diretrizes mais detalhadas sobre a criação de pacotes, incluindo ferramentas de cliente necessárias, exemplo de arquivo de projeto e comandos, consulte Criar um pacote [NuGet usando a CLI do dotnet](./creating-a-package-dotnet-cli.md).

Para ajudar a decidir quais estruturas do .NET direcionar, confira nossas diretrizes mais recentes para direcionamento [de plataforma cruzada.](/dotnet/standard/library-guidance/cross-platform-targeting)

## <a name="package-metadata"></a>Metadados de pacote

Os metadados são um componente fundamental de qualquer NuGet pacote. A qualidade dos metadados pode influenciar muito a capacidade de descoberta, a usabilidade e a confiabilidade do seu pacote.

No Visual Studio, a maneira recomendada de especificar metadados de pacote é usar Project > propriedades [Project Nome] > Pacote.

Os elementos de metadados do pacote também [podem ser especificados diretamente no arquivo de projeto](./creating-a-package-msbuild.md#set-properties).

Veja abaixo um mapeamento de tabela e a descrição dos elementos de metadados de pacote disponíveis:

| Visual Studio nome da propriedade                       | [Project arquivo/MSBuild nome da propriedade](/dotnet/core/tools/csproj#packagereleasenotes)                              | [Nome da propriedade Nuspec](/nuget/reference/nuspec#general-form-and-schema)   | Descrição                                                                                                           |
|-----------------------------------------------    |-----------------------------------------------------------------------------------------------------------------------------------------  |---------------------------------------------------------------------------------------------------    |-------------------------------------------------------------------------------------------------------------------    |
| [`Package id`](#package-id)                       | [`PackageId`](/nuget/reference/msbuild-targets#pack-target)                                                               | [`id`](/nuget/reference/nuspec#id)                                        | O nome ou identificador do pacote.                                                                                       |
| [`Package version`](#package-version)             | [`PackageVersion`](/nuget/reference/msbuild-targets#pack-target)                                                      | [`version`](/nuget/reference/nuspec#version)                              | Versão do pacote NuGet.                                                                                                |
| [`Authors`](#authors)                             | [`Authors`](/nuget/reference/msbuild-targets#pack-target)                                                                 | [`authors`](/nuget/reference/nuspec#authors)                              | Uma lista separada por vírgulas de autores de pacote, geralmente usando o "nome muito" do indivíduo ou de uma organização.           |
| [`Description`](#description)                     | [`Description`](/nuget/reference/msbuild-targets#pack-target)                                                         | [`description`](/nuget/reference/nuspec#description)                      | Uma descrição do pacote.                                                                                         |
| [`Copyright`](#copyright)                         | [`Copyright`](/nuget/reference/msbuild-targets#pack-target)                                                               | [`copyright`](/nuget/reference/nuspec#copyright)                          | Detalhes sobre direitos autorais do pacote.                                                                                    |
| [`Licensing - Expression`](#licensing)            | [`PackageLicenseExpression`](/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)     | [`license type="expression"`](/nuget/reference/nuspec#license)            | Uma expressão de licença SPDX.                                                                                           |
| [`Licensing - File`](#licensing)                  | [`PackageLicenseFile`](/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)           | [`license type="file"`](/nuget/reference/nuspec#license)                  | Caminho para um arquivo de licença personalizado.                                                                                        |
| [`Project URL`](#project-url)                     | `PackageProjectUrl`                                                                                                                       | [`projectUrl`](/nuget/reference/nuspec#projecturl)                        | Uma URL para a home page do projeto.                                                                                       |
| [`Icon File`](#icon)                              | [`PackageIcon`](/nuget/reference/msbuild-targets#packing-an-icon-image-file)                                      | [`icon`](/nuget/reference/nuspec#icon)                                    | Caminho para o arquivo de imagem do ícone de pacote.                                                                                  |
| [`Repository URL`](#repository-type-and-url)      | [`RepositoryUrl`](/nuget/reference/msbuild-targets#pack-target)                                                       | [`repository url`](/nuget/reference/nuspec#repository)                    | URL para o repositório do qual o pacote foi criado.                                                               |
| [`Repository type`](#repository-type-and-url)     | [`RespositoryType`](/nuget/reference/msbuild-targets#pack-target)                                                     | [`repository type`](/nuget/reference/nuspec#repository)                   | Tipo de repositório para o qual a URL do repositório está apontando (ou seja, "git").                                                    |
| [`Tags`](#tags)                                   | [`PackageTags`](/nuget/reference/msbuild-targets#pack-target)                                                         | [`tags`](/nuget/reference/nuspec#tags)                                    | Uma lista delimitada por espaço de marcas e palavras-chave que descrevem o pacote. Marcas são usadas ao pesquisar pacotes.     |
| [`Release notes`](#release-notes)                 | [`PackageReleaseNotes`](/nuget/reference/msbuild-targets#pack-target)                                         | [`releaseNotes`](/nuget/reference/nuspec#releasenotes)                    | Uma descrição das alterações feitas nesta versão do pacote.                                                     |
### <a name="package-id"></a>ID do Pacote

Se você estiver publicando um pacote completamente novo:

✔️ escolha uma ID de pacote que seja exclusiva e claramente diferenciada dos pacotes existentes no NuGet.org.
> Você pode verificar se uma ID de pacote é exclusiva e diferencial pesquisando a ID em NuGet.org ou verificando se o link a seguir existe: https://www.nuget.org/packages/<package nome \> .

✔️ CONSIDERE escolher um nome NuGet pacote com um prefixo que atenda NuGet critérios de reserva [de prefixo do .](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria)
> Reservar a ID de prefixo para seu pacote permitirá que você receba a marca de seleção verificada: ![ imagem](media/Verified-check-mark.png)
> 
> Confira os documentos [de reserva de prefixo](../nuget-org/id-prefix-reservation.md) da ID do pacote para saber mais.

### <a name="package-version"></a>Versão do pacote

✔️ CONSIDERE o uso [de SemVer para](https://semver.org/) fazer a versão do NuGet pacote.
> Essencialmente, isso significa usar o formato Major.Minor.Patch[-prerelease].

✔️ FAÇA a publicação de um pacote como um [pacote de pré-lançamento](./prerelease-packages.md) se ele não for estável ou uma versão prévia.

Consulte o guia de versão da biblioteca [do .NET](/dotnet/standard/library-guidance/versioning) para obter diretrizes mais avançadas.

### <a name="authors"></a>Autores

✔️ USE o campo autor para o "nome de sua organização".
> Por exemplo, se meu nome de usuário NuGet.org for "jdoe", o uso de "Jane Doe" para o campo autor poderá ajudar os consumidores a reconhecerem-me como autor. Se o nome de usuário NuGet.org da minha organização for "ContosoToolkit", o uso da "Contoso Corporation" poderá ser mais reconhecível e inspirar mais confiança do consumidor.
### <a name="description"></a>Descrição

✔️ DO incluem uma breve descrição (até 4.000 caracteres) para descrever seu pacote.
> As descrições do pacote são um dos campos mais proeminentes NuGet pesquisa e provavelmente serão a primeira coisa que os consumidores potenciais analisam para determinar se um pacote é certo para eles.

### <a name="copyright"></a>Direitos autorais

✔️ CONSIDERE a possibilidade de direitos autorais de seu pacote com "Copyright (c) <nome/empresa \> <\> ano".
>Uma notificação de direitos autorais indica essencialmente que seu trabalho não pode ser copiado sem sua permissão. Incluir uma notificação de direitos autorais em seu pacote é fácil e não causará nenhum dano!

Exemplo: Copyright (c) Contoso 2020

### <a name="licensing"></a>Licenciamento

✔️ DO [incluem uma expressão de licença ou um arquivo de licença em seu pacote](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file).
> [!IMPORTANT]
> Um projeto sem uma [](https://choosealicense.com/no-permission/)licença assume como padrão direitos autorais exclusivos, o que significa que você não concedeu permissão a ninguém para usar seu projeto.

❌ NÃO use a propriedade de metadados `LicenseUrl` preterida.
> Isso apresenta ambiguidade legal, pois as alterações de licença na URL alterarão retroativamente a licença exibida para versões anteriores do pacote.

#### <a name="if-your-package-is-open-source"></a>Se o pacote for [de código aberto](https://opensource.org/osd)

✔️ ESCOLHA [uma licença de código aberto para](https://choosealicense.com/) tornar seu pacote de código-fonte aberto.
> *"Licenças de software livre são licenças que estão em conformidade com a Definição de Software Livre – em resumo, elas permitem que o software seja usado livremente, modificado e compartilhado."* – Iniciativa open-source. Para saber mais sobre software livre e a Iniciativa de Software Livre, confira https://opensource.org/ .

✔️ CONSIDERE [incluir uma expressão de licença em seu pacote](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file).
> As expressões de licença são mais claras e torna mais óbvio para os consumidores se eles podem usar seu pacote ou se a licença foi alterada. 
> [!Note]
> NuGet.org aceita apenas expressões de licença para licenças aprovadas pela Open Source Initiative ou pela Free Software Foundation.

#### <a name="if-your-package-is-not-open-source"></a>Se o pacote não for de código aberto

✔️ DO [inclua um arquivo de licença em seu pacote](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file).
> Qualquer arquivo de licença (.txt ou .md) pode ser adicionado ao seu pacote, incluindo licenças não padrão. 

### <a name="project-url"></a>URL de Projeto

✔️ CONSIDERE incluir um link para um projeto, repositório ou site da empresa associado.
> Seu site de projeto deve ter tudo o que os usuários precisam saber sobre seu pacote e provavelmente será onde os usuários procurarão a documentação.

### <a name="icon"></a>ícone

✔️ CONSIDERE [incluir um ícone com seu pacote](../reference/msbuild-targets.md#packing-an-icon-image-file) para ajudar a diferenciá-lo visualmente. É uma adição relativamente pequena que pode melhorar a percepção da qualidade do pacote.
> Os ícones podem ser específicos para pacotes individuais ou ser um logotipo da marca.

✔️ DO use uma imagem que seja 128x128 e tenha uma PNG (plano de fundo transparente) para melhor exibição de resultados.
> NuGet dimensionar automaticamente sua imagem para o cliente em que ela está sendo exibida.

❌ NÃO use a propriedade de metadados `IconUrl` preterida.

### <a name="repository-type-and-url"></a>Tipo de repositório e URL

✔️ CONSIDERE configurar o [Link](/dotnet/standard/library-guidance/sourcelink) de Origem para adicionar automaticamente metadados de controle do código-fonte ao seu pacote NuGet e tornar sua biblioteca mais fácil de depurar.
> O Link de Origem adiciona `Repository URL` `Repository Type` automaticamente e aos metadados do pacote. Ele também adiciona a confirmação específica associada à versão do pacote.

### <a name="tags"></a>Marcas

✔️ DO incluem várias marcas com os principais termos relacionados ao seu pacote para aprimorar a capacidade de descoberta.
> As marcas são levadas em conta no algoritmo de pesquisa NuGet.org e são especialmente úteis para termos que não estão na ID do pacote, mas são relevantes.

Por exemplo, se eu publicasse um pacote para registrar cadeias de caracteres no console, incluiria: "log, log, console, cadeia de caracteres, saída"

### <a name="release-notes"></a>Notas de versão

✔️ CONSIDERE incluir notas de versão com cada atualização que descreve quais alterações foram feitas.
> Embora não haja nenhum formato específico necessário para notas de versão, recomendamos incluir:
>
> 1. Alterações de quebra
> 2. Novos recursos
> 3. Correções de bug
> 
> Se você já acompanhar as notas de versão ou um changelog no seu repo, também poderá incluir um link para o arquivo relevante.

## <a name="related-topics"></a>Tópicos relacionados

- [Criar e publicar um pacote (CLI do dotnet)](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [Criar e publicar um pacote (Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio.md?tabs=netcore-cli)
