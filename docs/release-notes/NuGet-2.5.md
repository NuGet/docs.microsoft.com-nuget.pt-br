---
title: Notas de versão 2.5 do NuGet
description: Notas de versão do NuGet 2.5, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 29d0b33714a574281680e110b967269699afbaf1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550477"
---
# <a name="nuget-25-release-notes"></a>Notas de versão 2.5 do NuGet

[Notas de versão do NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [notas de versão do NuGet 2.6](../release-notes/nuget-2.6.md)

O NuGet 2.5 foi lançado em 25 de abril de 2013. Esta versão era tão grande, constatamos forçadas ignorar as versões 2.3 e 2.4! Até o momento, esta é a versão de maior que tivemos para o NuGet, com failover [itens de trabalho de 160](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) na versão.

## <a name="acknowledgements"></a>Confirmações

Gostaríamos de agradecer os seguintes colaboradores externos por suas contribuições significativas para o NuGet 2.5:

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) -adicionar MonoAndroid, MonoTouch e MonoMac à lista de identificadores de estrutura de destino conhecidos.
2. [Aragoneses de g. Andres](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) -corrigir a ortografia do `NuGet.targets` para um sistema de operacional diferencia maiusculas de minúsculas
3. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - Verifique a solução de build no Mono.
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - Corrija os testes de unidade com falha no Mono.
5. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [#2920](https://nuget.codeplex.com/workitem/2920) -comando de pacote nuget.exe não propaga as propriedades para o MSBuild
6. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#1511](https://nuget.codeplex.com/workitem/1511) - XML modificado código de tratamento para preservar a formatação.
7. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - Palavras reconhecidas adicionadas ao dicionário personalizado para permitir que o build. cmd seja bem-sucedida.
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - Corrija os testes de unidade durante a execução no VS localizadas.
9. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - Interface extraído do PackageService
10. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
     - [#936](https://nuget.codeplex.com/workitem/936) -lidar com as dependências do projeto quando o empacotamento
11. [Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
     - [#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -suporte senha com texto não criptografado ao armazenar credenciais de origem do pacote em arquivos de nuget.cofig
12. [James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
     - [#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -descrição de Ajuda do Get-Package corrigir

Também Agradecemos os indivíduos a seguir para localizar bugs com o NuGet 2.5 Beta/RC que foram aprovados e corrigido antes do lançamento final:

1. [Tony parede](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) - MSTest dividido com mais recente NuGet 2.4 e 2.5 compilações

## <a name="notable-features-in-the-release"></a>Recursos importantes da versão

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>Permitir que os usuários substituir os arquivos de conteúdo que já existe

Um dos recursos mais solicitados de todo o tempo foi a capacidade de substituir os arquivos de conteúdo que já existem no disco quando incluído em um pacote do NuGet. Começando com o NuGet 2.5, os conflitos são identificados e você será solicitado a substituir os arquivos, enquanto que anteriormente esses arquivos sempre foram ignorados.

![Substituir arquivos de conteúdo](./media/NuGet-2.5/overwrite-file.png)

'nuget.exe update' e 'Install-Package' agora têm uma nova opção '-FileConflictAction' para definir alguns padrão para cenários de linha de comando.

Defina uma ação padrão quando já existe um arquivo de um pacote no projeto de destino. Definido como 'Substituição' para substituir os arquivos sempre. Defina como 'Ignorar' para ignorar arquivos. Se não for especificado, ele solicitará para cada arquivo conflitante.

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>Importação automática de arquivos de destinos e objetos do MSBuild

Uma nova pasta convencional foi criada no nível superior do pacote do NuGet.  Como um par `\lib`, `\content`, e `\tools`, agora você pode incluir um `\build` pasta em seu pacote.  Nesta pasta, você pode colocar dois arquivos com nomes fixos, `{packageid}.targets` ou `{packageid}.props`. Esses dois arquivos podem ser diretamente em `build` ou em pastas específicas do framework assim como as outras pastas. A regra para a pasta de framework melhor correspondentes de separação é exatamente o mesmo aqueles.

Quando o NuGet instala um pacote com arquivos \build, ele adicionará um MSBuild `<Import>` elemento no arquivo de projeto que aponta para o `.targets` e `.props` arquivos. O `.props` arquivo for adicionado na parte superior, enquanto o `.targets` arquivo é adicionado à parte inferior.

### <a name="specify-different-references-per-platform-using-references-element"></a>Especifique as referências de diferentes por plataforma usando `<References/>` elemento

Antes de 2.5, em `.nuspec` arquivo, o usuário só pode especificar os arquivos de referência, a ser adicionada para todos os framework. Agora, com esse novo recurso no 2.5, o usuário pode criar o `<reference/>` elemento para cada plataforma suportada, por exemplo:

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

Aqui está o fluxo para como o NuGet adiciona referências a projetos com base no `.nuspec` arquivo:

1. Encontre o `lib` pasta que é apropriado para a estrutura de destino e obter a lista de assemblies da pasta
1. Separadamente, localize o grupo de referências que é apropriado para a estrutura de destino e obter a lista de assemblies do grupo. Grupo de referência sem a estrutura de destino especificado é o fallback.
1. Localize a interseção das duas listas e usá-lo como as referências para adicionar

Esse novo recurso permitirá que os autores de pacote usar o recurso de referências para aplicar a subconjuntos de assemblies para estruturas diferentes quando eles precisariam executar assemblies duplicados em vários `lib` pastas.

Observação: você deve, no momento usar nuget.exe pack para usar esse recurso; Explorador de pacotes NuGet ainda não dá suporte-lo.

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>Atualizar todos os botões para permitir a atualização de todos os pacotes ao mesmo tempo

Muitos de vocês sabem sobre o cmdlet do PowerShell "Update-Package" para atualizar todos os seus pacotes; Agora há uma maneira fácil de fazer isso por meio da interface do usuário também.

Para experimentar este recurso:

1. Criar um novo aplicativo ASP.NET MVC
1. Iniciar a caixa de diálogo 'Gerenciar pacotes do NuGet'
1. Selecione 'Atualizações'
1. Clique no botão 'Atualizar tudo'

![Botão tudo na caixa de diálogo de atualização](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Suporte de referência de projeto aprimorado para nuget.exe Pack

Agora nuget.exe processos de comando de pacote referenciado em projetos com as seguintes regras:

1. Se o projeto referenciado tem correspondente `.nuspec` do arquivo, por exemplo, há um arquivo chamado `proj1.nuspec` na mesma pasta que `proj1.csproj`, este projeto é adicionado como uma dependência ao pacote, usando a id e versão leia o `.nuspec` arquivo.
1. Caso contrário, os arquivos do projeto referenciado são empacotados em pacote. Em seguida, projetos referenciados por este projeto serão processados usando o mesmos regras recursivamente.
1. DLL de todos os `.pdb`, e `.exe` arquivos são adicionados.
1. Todos os outros arquivos de conteúdo são adicionados.
1. Todas as dependências são mescladas.

Isso permite que um projeto referenciado deve ser tratada como uma dependência, se houver um `.nuspec` de arquivos, caso contrário, ele se torna parte do pacote.

Mais detalhes aqui: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>Adicionar uma propriedade 'Mínimo a versão do NuGet' aos pacotes

Um novo atributo de metadados chamado 'minClientVersion' agora pode indicar a versão de cliente do NuGet mínima necessária para consumir um pacote.

Esse recurso ajuda o autor do pacote para especificar que um pacote funcionará apenas depois de uma versão específica do NuGet. Como novos `.nuspec` recursos são adicionados após o NuGet 2.5, pacotes serão possível reivindicar uma versão mínima do NuGet.

```xml
<metadata minClientVersion="2.6">
```

Se o usuário tem o NuGet 2.5 instalado e um pacote é identificado como exigindo 2.6, indicações visuais serão fornecidas para o usuário indicando que o pacote não será instalado. Em seguida, o usuário será orientado para atualizar sua versão do NuGet.

Isso melhora na experiência existente no qual começam a pacotes para instalar, mas falhar, em seguida, o que indica que uma versão de esquema não reconhecido foi identificada.

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>Dependências não desnecessariamente são atualizadas durante a instalação do pacote

Antes do NuGet 2.5, quando um pacote foi instalado que depende de um pacote já instalado no projeto, a dependência será atualizada como parte da nova instalação, mesmo se a versão existente satisfez a dependência.

Começando com o NuGet 2.5, se uma versão de dependência já for atendida, a dependência não será atualizada durante outras instalações de pacote.

**Cenário:**

1. O repositório de origem contém o pacote B com a versão 1.0.0 e 1.0.2. Ele também contém o pacote a, que tem uma dependência em B (> = 1.0.0).
1. Suponha que o projeto atual já tem a versão do pacote B 1.0.0 instalado. Agora que você deseja instalar a pacote.

**No NuGet 2.2 e anteriores:**

* Ao instalar um pacote, o NuGet será atualizado automaticamente B à 1.0.2, mesmo que a versão existente 1.0.0 já atende à restrição de versão de dependência, que é > = 1.0.0.

**No NuGet 2.5 e mais recente:**

* O NuGet não será mais atualizado B, pois detecta que a versão existente 1.0.0 satisfaz a restrição de versão de dependência.

Para obter mais informações sobre essa alteração, leia a página detalhada [item de trabalho](http://nuget.codeplex.com/workitem/1681) , bem como os relacionados [thread de discussão](http://nuget.codeplex.com/discussions/436712).

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>NuGet.exe gera solicitações http detalhado

Se você estiver solucionando problemas de nuget.exe ou apenas curioso quais solicitações HTTP são feitas durante as operações, o '-detalhamento detalhada ' switch agora produzirá todas as solicitações HTTP feitas.

![Saída HTTP do nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>push NuGet.exe agora dá suporte a fontes de UNC e pasta

Antes do NuGet 2.5, se você tentou executar 'nuget.exe push' para uma origem de pacote com base em um caminho UNC ou uma pasta local, o envio por push falharia. Com o recurso de configuração hierárquicos adicionados recentemente, tornou-se comum para nuget.exe precisar direcionar para uma fonte de pasta/UNC ou uma galeria do NuGet com base em HTTP.

Começando com o NuGet 2.5 se nuget.exe identifica uma fonte UNC/pasta, ele fará a cópia do arquivo para a fonte.

O comando a seguir funcionará:

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>NuGet.exe dá suporte a arquivos de configuração especificado explicitamente

comandos de NuGet.exe que acessar a configuração (todos, exceto 'especificação' e 'pack') agora dão suporte a um novo '-ConfigFile' opção, o que força a um arquivo de configuração específico a ser usado no lugar do arquivo de configuração padrão em % AppData%\nuget\Nuget.Config.

Exemplo:

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>Suporte para projetos nativos

Com o NuGet 2.5, as ferramentas do NuGet agora estão disponível para projetos nativos no Visual Studio. Esperamos que mais pacotes nativos utilizarão o recurso de importações do MSBuild acima, usando uma ferramenta criada pela [CoApp projeto](http://coapp.org). Para obter mais informações, leia [os detalhes sobre a ferramenta](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) no site da coapp.org.

O nome da estrutura de destino de "nativo" é introduzido para pacotes incluir arquivos \build, \content e \tools quando o pacote é instalado em um projeto nativo.  O \`lib' pasta não é usada para projetos nativos.
