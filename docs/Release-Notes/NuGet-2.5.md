---
title: "Notas de versão do NuGet 2.5 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de versão do NuGet 2.5, incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão 2.5 do NuGet, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4fb696a1f4d76bdd3461df6af461f279f9f0a8b0
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-25-release-notes"></a>Notas de versão 2.5 do NuGet

[Notas de versão do NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [notas de versão 2.6 do NuGet](../release-notes/nuget-2.6.md)

O NuGet 2.5 foi lançado em 25 de abril de 2013. Esta versão foi tão grande, percebemos forçadas ignorar as versões 2.3 e 2.4! Até agora, isso é a versão maior que tivemos para NuGet, com failover [itens de trabalho de 160](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) na versão.

## <a name="acknowledgements"></a>Confirmações

Gostaríamos de agradecer os seguintes colaboradores externos por suas contribuições significativas para o NuGet 2.5:

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) -adicionar MonoAndroid, MonoTouch e MonoMac à lista de identificadores do framework de destino conhecidos.
1. [Aragoneses g. Andres](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) -corrija a grafia de `NuGet.targets` para um sistema operacional diferencia maiusculas de minúsculas
1. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - Verifique a solução Mono de compilação.
1. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - Corrija os testes de unidade com falha em Mono.
1. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [#2920](https://nuget.codeplex.com/workitem/2920) -comando de pacote nuget.exe não propaga propriedades para o MSBuild
1. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#1511](https://nuget.codeplex.com/workitem/1511) - XML modificado código de tratamento para preservar a formatação.
1. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - Palavras reconhecidas adicionadas ao dicionário personalizado para permitir que build.cmd seja bem-sucedida.
1. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - Corrija os testes de unidade durante a execução no VS localizadas.
1. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - Interface extraído da PackageService
1. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
    - [#936](https://nuget.codeplex.com/workitem/936) -lidar com dependências do projeto quando de remessa
1. [Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
    - [#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -suporte senha com texto não criptografado ao armazenar credenciais de origem do pacote em arquivos de nuget.cofig
1. [James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
    - [#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -descrição de Ajuda do Get-Package corrigir

Agradecemos também as pessoas a seguir para localizar os bugs com o NuGet 2.5 Beta/RC que foram aprovadas e corrigido antes da versão final:

1. [Parede Tony](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) - MSTest dividido com mais recente NuGet 2.4 e 2.5 compilações

## <a name="notable-features-in-the-release"></a>Recursos importantes da versão

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>Permitir que os usuários substituir os arquivos de conteúdo que já existe

Um dos recursos mais solicitados de todo o tempo foi a capacidade de substituir os arquivos de conteúdo que já existem no disco quando incluídos em um pacote do NuGet. Começando com o NuGet 2.5, esses conflitos são identificados e você será solicitado a substituir os arquivos, enquanto que anteriormente esses arquivos sempre foram ignorados.

![Substituir os arquivos de conteúdo](./media/NuGet-2.5/overwrite-file.png)

'nuget.exe update' e 'Install-Package' agora têm uma nova opção '-FileConflictAction' para definir alguns padrão para cenários de linha de comando.

Defina uma ação padrão quando já existe um arquivo de um pacote no projeto de destino. Definido como 'Sobrescrever' para substituir os arquivos sempre. Defina como 'Ignorar' para ignorar arquivos. Se não for especificado, ele solicitará para cada arquivo conflitante.

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>Importação automática de arquivos de destino e destinos do MSBuild

Foi criada uma nova pasta convencional no nível superior do pacote do NuGet.  Como um par de `\lib`, `\content`, e `\tools`, você pode incluir um `\build` pasta em seu pacote.  Nesta pasta, você pode colocar dois arquivos com nomes fixos, `{packageid}.targets` ou `{packageid}.props`. Esses dois arquivos podem ser diretamente em `build` ou em pastas específicas do framework assim como as outras pastas. A regra para a pasta de estrutura melhor correspondência de separação é exatamente o mesmo que os.

Quando o NuGet instala um pacote com arquivos \build, ele adicionará um MSBuild `<Import>` elemento no arquivo de projeto apontando para o `.targets` e `.props` arquivos. O `.props` arquivo é adicionado na parte superior, enquanto o `.targets` é adicionado à parte inferior.

### <a name="specify-different-references-per-platform-using-references-element"></a>Especifique referências diferentes por plataforma usando `<References/>` elemento

Antes de 2.5, no `.nuspec` arquivo, o usuário só pode especificar os arquivos de referência, a ser adicionada para todos os framework. Agora com esse novo recurso no 2.5, o usuário pode criar o `<reference/>` elemento para cada plataforma suportada, por exemplo:

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

Aqui está o fluxo como NuGet adiciona referências a projetos com base no `.nuspec` arquivo:

1. Localizar o `lib` pasta que é apropriado para a estrutura de destino e obter a lista de assemblies da pasta
1. Separadamente, localizar o grupo de referências que é apropriado para a estrutura de destino e obter a lista de assemblies do grupo. Referência sem framework de destino especificado é o grupo de fallback.
1. Localize a interseção das duas listas e usá-lo como as referências para adicionar

Esse novo recurso permitirá que os autores de pacote usar o recurso de referências para aplicar subconjuntos de assemblies para estruturas diferentes quando eles precisaria executar assemblies duplicados em vários `lib` pastas.

Observação: você deve atualmente usar pacote de nuget.exe para usar esse recurso; Explorador de pacotes do NuGet ainda não suporta-lo.

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>Atualizar todos os botões para permitir que todos os pacotes de atualização de uma vez

Muitos de vocês sabem sobre o cmdlet do PowerShell "Pacote de atualização" para atualizar todos os pacotes; Agora há uma maneira fácil de fazer isso por meio de interface de usuário.

Para experimentar esse recurso:

1. Criar um novo aplicativo ASP.NET MVC
1. Iniciar a caixa de diálogo 'Gerenciar pacotes do NuGet'
1. Selecione 'Atualizações'
1. Clique no botão 'Atualizar tudo'

![Atualizar todos os botões na caixa de diálogo](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Suporte de referência de projeto aprimorado para nuget.exe Pack

Agora a processos de comando do pacote de nuget.exe referenciada projetos com as seguintes regras:

1. Se o projeto referenciado tem correspondente `.nuspec` de arquivos, por exemplo, há um arquivo chamado `proj1.nuspec` na mesma pasta que `proj1.csproj`, este projeto é adicionado como uma dependência no pacote, usando a id e ler a versão do `.nuspec` arquivo.
1. Caso contrário, os arquivos do projeto referenciado são incluídos no pacote. Em seguida, projetos referenciados por este projeto serão processados usando o mesmos regras recursivamente.
1. DLL de todos os `.pdb`, e `.exe` arquivos são adicionados.
1. Todos os outros arquivos de conteúdo são adicionados.
1. Todas as dependências são mescladas.

Isso permite que um projeto referenciado deve ser tratada como uma dependência, se houver um `.nuspec` de arquivos, caso contrário, ele se torna parte do pacote.

Mais detalhes aqui: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>Adicionar uma propriedade de 'Mínimo a versão do NuGet' para pacotes

Um novo atributo de metadados chamado 'minClientVersion' agora pode indicar a versão de cliente NuGet mínima necessária para consumir um pacote.

Esse recurso ajuda o autor do pacote para especificar que um pacote funcionará somente depois de uma versão específica do NuGet. Como novo `.nuspec` recursos foram adicionados após o NuGet 2.5 pacotes será capazes de declaração de uma versão mínima do NuGet.

```xml
<metadata minClientVersion="2.6">
```

Se o usuário tem o NuGet 2.5 instalado e um pacote é identificado como exigir 2.6, indicações visuais terá para o usuário indicando que o pacote não será instalado. Em seguida, o usuário será orientado para atualizar sua versão do NuGet.

Isso será aprimoram a experiência existente onde os pacotes de começam a instalar, mas não que indica que uma versão de esquema não reconhecido foi identificada.

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>Dependências não desnecessariamente são atualizadas durante a instalação do pacote

Antes do NuGet 2.5, quando foi instalado um pacote que depende de um pacote já instalado no projeto, a dependência será atualizada como parte da instalação do novo, mesmo se a versão existente atendidas a dependência.

Começando com o NuGet 2.5, se uma versão de dependência já for atendida, a dependência não será atualizada durante as outras instalações de pacote.

**Cenário:**

1. O repositório de origem contém o pacote B com a versão 1.0.0 e 1.0.2. Ele também contém o pacote que tem uma dependência em B (> = 1.0.0).
1. Suponha que o projeto atual já tem a versão do pacote B 1.0.0 instalado. Agora você deseja instalar a pacote.

**No NuGet 2.2 e anterior:**

* Ao instalar um pacote, o NuGet será atualizado automaticamente B à 1.0.2, mesmo que a versão existente 1.0.0 já atende à restrição de versão de dependência, que é > = 1.0.0.

**No NuGet 2.5 e mais recente:**

* O NuGet não serão mais atualizados B, pois detecta que a versão existente 1.0.0 satisfaz a restrição de versão de dependência.

Para obter mais informações sobre essa alteração, leia o detalhado [item de trabalho](http://nuget.codeplex.com/workitem/1681) , bem como os relacionados [segmento de discussão](http://nuget.codeplex.com/discussions/436712).

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>NuGet.exe produz solicitações http com detalhamento detalhado

Se você estiver solucionando problemas de nuget.exe ou apenas curioso que são feitas solicitações HTTP durante operações, o '-detalhes detalhadas ' switch agora mostrará todas as solicitações HTTP feitas.

![Saída HTTP de nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>push NuGet.exe agora dá suporte a fontes de UNC e pasta

Antes do NuGet 2.5, se você tentou executar 'nuget.exe push' para uma origem de pacote com base em um caminho UNC ou uma pasta local, o envio falhará. Com o recurso de configuração hierárquica adicionado recentemente, tornou-se comum de nuget.exe para precisa direcionar uma fonte UNC/pasta ou uma galeria do NuGet com base em HTTP.

Começando com o NuGet 2.5 se nuget.exe identifica uma fonte de pasta/UNC, ela executará a cópia do arquivo de origem.

O comando a seguir agora funcionará:

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>NuGet.exe oferece suporte a arquivos de configuração especificado explicitamente

suportam a comandos de NuGet.exe que acessar configuração (todos exceto 'especificação' e 'pacote') agora um novo '-ConfigFile' opção, o que força um arquivo de configuração específico a ser usado no lugar do arquivo de configuração padrão em % AppData%\nuget\Nuget.Config.

Exemplo:

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>Suporte para projetos nativos

Com o NuGet 2.5, a NuGet ferramentas agora está disponível para projetos nativos no Visual Studio. Esperamos que mais pacotes nativos utilizará o recurso de importações do MSBuild acima, usando uma ferramenta criada pelo [CoApp projeto](http://coapp.org). Para obter mais informações, leia [os detalhes sobre a ferramenta](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) no site da coapp.org.

O nome da estrutura de destino de "nativo" é introduzido para pacotes incluir arquivos no \build \content e \tools quando o pacote for instalado em um projeto nativo.  O \`lib' pasta não é usada para projetos nativos.
