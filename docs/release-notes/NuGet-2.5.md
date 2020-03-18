---
title: Notas de versão do NuGet 2,5
description: Notas de versão do NuGet 2,5 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940582d5173f5a53dcd04cf1258fc02a2439af4e
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428712"
---
# <a name="nuget-25-release-notes"></a>Notas de versão do NuGet 2,5

[Notas de versão do NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [notas de versão do NuGet 2,6](../release-notes/nuget-2.6.md)

O NuGet 2,5 foi lançado em 25 de abril de 2013. Essa versão foi tão grande, nós achamos obrigado a ignorar as versões 2,3 e 2,4! Até o momento, esta é a maior versão que tínhamos para o NuGet, com mais de [160 itens de trabalho](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) na versão.

## <a name="acknowledgements"></a>Agradecimentos

Gostaríamos de agradecer aos seguintes colaboradores externos por suas contribuições significativas para o NuGet 2,5:

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) -adicione o monoandroid, o MonoTouch e o MonoMac à lista de identificadores de estrutura de destino conhecidos.
2. [Andres G. aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) -corrigir a ortografia de `NuGet.targets` para um sistema operacional que diferencia maiúsculas de minúsculas
3. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - Faça com que a solução seja criada no mono.
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - Corrigir testes de unidade com falha no mono.
5. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [#2920](https://nuget.codeplex.com/workitem/2920) -o comando do pacote NuGet. exe não propaga as propriedades para o MSBuild
6. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - código de manipulação XML modificado [#1511](https://nuget.codeplex.com/workitem/1511) para preservar a formatação.
7. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - Palavras reconhecidas adicionadas ao dicionário personalizado para permitir que o Build. cmd tenha sucesso.
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - Corrigir testes de unidade durante a execução no localizado VS.
9. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - Interface extraída de PackageService
10. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
     - [#936](https://nuget.codeplex.com/workitem/936) -tratar dependências do projeto ao empacotar
11. [Xavier de descusto](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
     - [#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -dar suporte à senha de texto não criptografado ao armazenar as credenciais de origem do pacote em arquivos NuGet. cofig
12. [James Manning Publications](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
     - [#3190](http://nuget.codeplex.com/workitem/3190), descrição de ajuda do Get-Package do [#3191](http://nuget.codeplex.com/workitem/3191) -Fix

Também apreciamos os seguintes indivíduos para encontrar bugs com o NuGet 2,5 Beta/RC que foram aprovados e corrigidos antes da versão final:

1. [Tony parede](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) -MSTest rompido com as compilações mais recentes do NuGet 2,4 e 2,5

## <a name="notable-features-in-the-release"></a>Recursos notáveis na versão

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>Permitir que os usuários substituam os arquivos de conteúdo que já existem

Um dos recursos mais solicitados de todo o tempo foi a capacidade de substituir os arquivos de conteúdo que já existem no disco quando incluídos em um pacote NuGet. A partir do NuGet 2,5, esses conflitos são identificados e você é solicitado a substituir os arquivos, enquanto anteriormente esses arquivos eram sempre ignorados.

![Substituir arquivos de conteúdo](./media/NuGet-2.5/overwrite-file.png)

"NuGet. exe update" e "Install-Package" agora têm uma nova opção "-fileconflitoaction" para definir um padrão para cenários de linha de comando.

Defina uma ação padrão quando um arquivo de um pacote já existir no projeto de destino. Defina como ' overwrite ' para sempre substituir arquivos. Defina como ' ignorar ' para ignorar arquivos. Se não for especificado, ele solicitará cada arquivo conflitante.

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>Importação automática de destinos do MSBuild e arquivos de props

Uma nova pasta convencional foi criada no nível superior do pacote NuGet.  Como um par para `\lib`, `\content`e `\tools`, agora você pode incluir uma pasta `\build` em seu pacote.  Nessa pasta, você pode posicionar dois arquivos com nomes fixos, `{packageid}.targets` ou `{packageid}.props`. Esses dois arquivos podem ser diretamente sob `build` ou em pastas específicas da estrutura, assim como as outras pastas. A regra para escolher a pasta de estrutura de melhor correspondência é exatamente a mesma daquela.

Quando o NuGet instala um pacote com arquivos \Build, ele adicionará um elemento de `<Import>` do MSBuild no arquivo de projeto apontando para os arquivos `.targets` e `.props`. O arquivo de `.props` é adicionado na parte superior, enquanto o arquivo de `.targets` é adicionado à parte inferior.

### <a name="specify-different-references-per-platform-using-references-element"></a>Especificar referências diferentes por plataforma usando o elemento `<References/>`

Antes de 2,5, no arquivo `.nuspec`, o usuário só pode especificar os arquivos de referência para serem adicionados a todas as estruturas. Agora, com esse novo recurso do 2,5, o usuário pode criar o elemento `<reference/>` para cada uma das plataformas com suporte, por exemplo:

```xml
<references>
    <group targetFramework="net45">
        <reference file="a.dll" />
    </group>
    <group targetFramework="netcore45">
        <reference file="b.dll" />
    </group>
    <group>
        <reference file="c.dll" />
    </group>
</references>
```

Este é o fluxo de como o NuGet adiciona referências a projetos com base no arquivo de `.nuspec`:

1. Localize a pasta `lib` apropriada para a estrutura de destino e obtenha a lista de assemblies dessa pasta
1. Localize separadamente o grupo de referências que é apropriado para a estrutura de destino e obtenha a lista de assemblies desse grupo. O grupo de referência sem a estrutura de destino especificada é o grupo de fallback.
1. Localize a interseção das duas listas e use-a como as referências a serem adicionadas

Esse novo recurso permitirá que os autores de pacotes usem o recurso de referências para aplicar subconjuntos de assemblies a diferentes estruturas quando, de outra forma, precisariam executar assemblies duplicados em várias pastas de `lib`.

Observação: você deve usar atualmente o pacote NuGet. exe para usar esse recurso; O Gerenciador de pacotes NuGet ainda não dá suporte a ele.

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>Botão atualizar tudo para permitir a atualização de todos os pacotes ao mesmo tempo

Muitos de vocês sabem sobre o cmdlet "Update-Package" do PowerShell para atualizar todos os seus pacotes; Agora há uma maneira fácil de fazer isso por meio da interface do usuário também.

Para experimentar esse recurso:

1. Criar um novo aplicativo ASP.NET MVC
1. Iniciar a caixa de diálogo ' gerenciar pacotes NuGet '
1. Selecione ' atualizações '
1. Clique no botão ' atualizar tudo '

![Botão atualizar tudo na caixa de diálogo](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Suporte de referência de projeto aprimorado para o pacote NuGet. exe

Agora, o comando NuGet. exe Pack processa projetos referenciados com as seguintes regras:

1. Se o projeto referenciado tiver um arquivo `.nuspec` correspondente, por exemplo, há um arquivo chamado `proj1.nuspec` na mesma pasta que `proj1.csproj`, então esse projeto é adicionado como uma dependência ao pacote, usando a ID e a versão lidas do arquivo de `.nuspec`.
1. Caso contrário, os arquivos do projeto referenciado serão agrupados no pacote. Em seguida, os projetos referenciados por este projeto serão processados usando as mesmas regras recursivamente.
1. Todos os arquivos DLL, `.pdb`e `.exe` são adicionados.
1. Todos os outros arquivos de conteúdo são adicionados.
1. Todas as dependências são mescladas.

Isso permite que um projeto referenciado seja tratado como uma dependência se houver um arquivo `.nuspec`, caso contrário, ele se tornará parte do pacote.

Mais detalhes aqui: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>Adicionar uma propriedade ' versão mínima do NuGet ' aos pacotes

Um novo atributo de metadados chamado ' minClientVersion ' agora pode indicar a versão mínima do cliente NuGet necessária para consumir um pacote.

Esse recurso ajuda o autor do pacote a especificar que um pacote só funcionará depois de uma versão específica do NuGet. À medida que novos recursos de `.nuspec` são adicionados após o NuGet 2,5, os pacotes poderão declarar uma versão mínima do NuGet.

```xml
<metadata minClientVersion="2.6">
```

Se o usuário tiver o NuGet 2,5 instalado e um pacote for identificado como exigindo 2,6, as indicações visuais serão dadas ao usuário indicando que o pacote não poderá ser instalado. O usuário será então guiado para atualizar sua versão do NuGet.

Isso melhorará a experiência existente em que os pacotes começam a ser instalados, mas falham indicando que uma versão de esquema não reconhecida foi identificada.

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>As dependências não são mais desnecessariamente atualizadas durante a instalação do pacote

Antes do NuGet 2,5, quando um pacote foi instalado que dependia de um pacote já instalado no projeto, a dependência seria atualizada como parte da nova instalação, mesmo que a versão existente esteja satisfeita na dependência.

A partir do NuGet 2,5, se uma versão de dependência já estiver satisfeita, a dependência não será atualizada durante outras instalações de pacote.

**O cenário:**

1. O repositório de origem contém o pacote B com a versão 1.0.0 e 1.0.2. Ele também contém o pacote A que tem uma dependência em B (> = 1.0.0).
1. Suponha que o projeto atual já tenha a versão 1.0.0 do pacote B instalada. Agora você deseja instalar o pacote A.

**No NuGet 2,2 e mais antigo:**

* Ao instalar o pacote A, o NuGet atualizará automaticamente B para 1.0.2, mesmo que a versão existente 1.0.0 já satisfaça a restrição de versão de dependência, que é > = 1.0.0.

**No NuGet 2,5 e mais recente:**

* O NuGet não atualizará mais B, pois detecta que a versão atual do 1.0.0 atende à restrição de versão de dependência.

Para obter mais informações sobre essa alteração, leia o [item de trabalho](http://nuget.codeplex.com/workitem/1681) detalhado, bem como o [thread de discussão](http://nuget.codeplex.com/discussions/436712)relacionado.

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>o NuGet. exe gera solicitações HTTP com detalhes detalhados

Se você estiver solucionando problemas do NuGet. exe ou apenas curioso quais solicitações HTTP são feitas durante as operações, a opção '-detalhamento detalhado ' gerará agora todas as solicitações HTTP feitas.

![Saída HTTP do NuGet. exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>o push NuGet. exe agora dá suporte a fontes UNC e de pasta

Antes do NuGet 2,5, se você tentou executar ' NuGet. exe push ' em uma origem de pacote com base em um caminho UNC ou em uma pasta local, o push falharia. Com o recurso de configuração hierárquica adicionado recentemente, havia se tornado comum para o NuGet. exe precisar direcionar uma origem de UNC/pasta ou uma galeria de NuGet baseada em HTTP.

A partir do NuGet 2,5, se o NuGet. exe identificar uma origem UNC/pasta, ele executará a cópia do arquivo para a origem.

Agora, o seguinte comando funcionará:

```cli
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>o NuGet. exe dá suporte a arquivos de configuração especificados explicitamente

os comandos NuGet. exe que acessam a configuração (tudo exceto ' spec ' e ' Pack ') agora oferecem suporte a uma nova opção '-ConfigFile ', que força um arquivo de configuração específico a ser usado no lugar do arquivo de configuração padrão em%AppData%\nuget\Nuget.Config.

Exemplo:

```cli
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>Suporte para projetos nativos

Com o NuGet 2,5, as ferramentas do NuGet agora estão disponíveis para projetos nativos no Visual Studio. Esperamos que a maioria dos pacotes nativos utilize o recurso de importações do MSBuild acima, usando uma ferramenta criada pelo [projeto CoApp](http://coapp.org). Para obter mais informações, leia [os detalhes sobre a ferramenta](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) no site do coapp.org.

O nome da estrutura de destino "Native" é introduzido para pacotes para incluir arquivos em \Build, \Content e \Tools quando o pacote é instalado em um projeto nativo.  A pasta \`lib ' não é usada para projetos nativos.
