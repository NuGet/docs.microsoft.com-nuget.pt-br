---
title: "Resolução de dependência de pacote do NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 8/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 1d530a72-3486-4a0d-b6fb-017524616f91
description: "Detalhes sobre o processo por meio do qual as dependências de um pacote do NuGet são resolvidas e instaladas no NuGet 2.x e 3.x ou superior."
keywords: "Dependências de pacotes do NuGet, controle de versão do NuGet, versões de dependência, grafo de versão, resolução de versão, restauração transitiva"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 44c69c07990fed72b439698d22021ebcbb2eed89
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="how-nuget-resolves-package-dependencies"></a>Como o NuGet resolve as dependências do pacote

Sempre que um pacote for instalado ou reinstalado, o que inclui o que está sendo instalado como parte de um processo de [restauração](../consume-packages/package-restore.md), o NuGet também instala todos os pacotes adicionais dos quais o primeiro pacote depende.

Essas dependências imediatas também podem ter suas próprias dependências, que podem continuar em uma profundidade arbitrária. Isso produz o que é chamado de um *grafo de dependência* que descreve as relações entre os pacotes em todos os níveis.

Quando vários pacotes têm a mesma dependência, a mesma ID de pacote pode aparecer no grafo várias vezes, potencialmente com restrições de versão diferentes. No entanto, somente uma versão de determinado pacote pode ser usada em um projeto, por isso o NuGet precisa escolher qual versão é usada. O processo exato depende do formato de referência de pacote que está sendo usado.

Neste tópico:
- [Resolução de dependência com PackageReference e project.json](#dependency-resolution-with-packagereference-and-projectjson)
- [Resolução de dependência com packages.config](#dependency-resolution-with-packagesconfig)
- [Excluindo referências](#excluding-references), que é necessário quando houver um conflito entre uma dependência especificada em um projeto e um assembly que é produzido por outro.
- [Atualizações de dependência durante a instalação do pacote](#dependency-updates-during-package-install)
- [Resolvendo erros de pacote incompatível](#resolving-incompatible-package-errors)

## <a name="dependency-resolution-with-packagereference-and-projectjson"></a>Resolução de dependência com PackageReference e project.json

Ao instalar os pacotes em projetos usando o PackageReference ou formatos `project.json`, o NuGet adiciona referências a um grafo de pacote simples no arquivo apropriado e resolve conflitos antecipadamente. Esse processo é chamado de *restauração transitiva*. Reinstalar ou restaurar pacotes é um processo de baixar os pacotes listados no grafo, resultando em builds mais rápidos e mais previsíveis. Você também pode aproveitar as versões curinga (flutuantes), como 2.8. \*, evitando chamadas caras e propensas a erro para `nuget update` em computadores clientes e servidores de build.

Quando o processo de restauração do NuGet é executado antes de um build, ele resolve as dependências primeiro na memória, em seguida, grava o grafo resultante em um arquivo chamado `project.assets.json` na pasta `obj` de um projeto usando PackageReference ou em um arquivo chamado `project.lock.json` ao lado de `project.json`. O MSBuild lê este arquivo e converte-o em um conjunto de pastas em que as referências em potencial podem ser encontradas e as adiciona à árvore de projeto na memória.

O arquivo de bloqueio é temporário e não deve ser adicionado ao controle do código-fonte. É listado por padrão em ambos `.gitignore` e `.tfignore`. Consulte [Pacotes e controle do código-fonte](Packages-and-Source-Control.md).

### <a name="dependency-resolution-rules"></a>Regras de resolução de dependência

A restauração transitiva aplica quatro regras principais para resolver as dependências: versão mais antiga aplicável, versões flutuantes, wins mais próximos e dependências primo.

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a>Versão mais antiga aplicável

A regra de versão aplicáveis mais antiga restaura a versão mais antiga possível de um pacote, conforme definido por suas dependências. Ela também se aplica às dependências do aplicativo ou à biblioteca de classes, a menos que seja declarado como [flutuante](#floating-versions).

Na figura a seguir, por exemplo, 1.0-beta é considerado inferior a 1.0, por isso o NuGet escolhe a versão 1.0:

![Escolher a versão mais antiga aplicável](media/projectJson-dependency-1.png)

Na figura a seguir, a versão 2.1 não está disponível no feed, mas como a restrição de versão é >=2.1, o NuGet escolhe a próxima versão mais antiga encontrada, neste caso 2.2:

![Escolher a próxima versão mais antiga disponível no feed](media/projectJson-dependency-2.png)

Quando um aplicativo especifica um número de versão exata, como 1.2, que não está disponível no feed, o NuGet falhará com um erro ao tentar instalar ou restaurar o pacote:

![O NuGet gera um erro quando uma versão exata do pacote não está disponível](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-wildcard-versions"></a>Versões flutuante (curinga)

Uma versão de dependência flutuante ou curinga é especificada com o curinga \*, assim como acontece com o 6.0.\*. Essa especificação de versão diz “use a versão mais recente do 6.0”; 4.\* significa “use a versão mais recente de 4.x”. Usar um caractere curinga permite que um pacote de dependência continue a se desenvolver sem a necessidade de uma alteração no aplicativo (ou pacote) consumidor.

Ao usar um caractere curinga, o NuGet resolverá a versão mais recente de um pacote que corresponde ao padrão de versão, por exemplo 6.0. \* obtém a versão mais recente de um pacote que começa com 6.0:

![Escolher a versão 6.0.1 quando uma versão flutuante 6.0.* é solicitada](media/projectJson-dependency-4.png)

> [!Note]
> Para obter informações sobre o comportamento de curingas e as versões de pré-lançamento, consulte [Controle de versão do pacote](../reference/package-versioning.md#version-ranges-and-wildcards).


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a>Wins mais próximos

Quando o grafo de pacote para um aplicativo contém versões diferentes do mesmo pacote, o NuGet escolhe aquele que é mais próximo do aplicativo no grafo e ignora todos os demais. Esse comportamento permite que um aplicativo substitua qualquer versão do pacote específico no grafo de dependência.

No exemplo abaixo, o aplicativo depende diretamente no Pacote B com uma restrição de versão de >=2.0. O aplicativo também depende do Pacote A, que por sua vez também depende do Pacote B, mas com uma restrição >=1.0. Como a dependência do Pacote B 2.0 é mais próxima do aplicativo no grafo, essa versão é usada:

![Aplicativo que usa a regra O mais próximo vence](media/projectJson-dependency-5.png)

>[!Warning]
> A regra O mais próximo vence pode resultar em um downgrade da versão do pacote, potencialmente interrompendo, dessa forma, outras dependências no grafo. Portanto, essa regra é aplicada com um aviso para alertar o usuário.

Esta regra também resulta em maior eficiência com um grande grafo de dependência (como aqueles com os pacotes BCL) porque depois que uma determinada dependência é ignorada, o NuGet também ignora todas as dependências restantes no branch do grafo. No diagrama abaixo, por exemplo, como o Pacote C 2.0 é usado, o NuGet ignora os branches no grafo que fazem referência a uma versão anterior do Pacote C:

![Quando o NuGet ignora um pacote no grafo, ele ignora todo o branch](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a>Dependências primo

Quando versões diferentes do pacote são referidas na mesma distância no grafo do aplicativo, o NuGet usa a versão mais antiga que cumpre todos os requisitos de versão (assim como acontece com as regras [versão mais antiga aplicável](#lowest-applicable-version) e [versões flutuantes](#floating-versions)). Na imagem abaixo, por exemplo, a versão 2.0 do Pacote B satisfaz a outra restrição >=1.0 e, portanto, é usada:

![Resolvendo as dependências primo usando a versão inferior que atende todas as restrições](media/projectJson-dependency-7.png)

Em alguns casos, não é possível atender a todos os requisitos de versão. Conforme mostrado abaixo, se o Pacote A requer exatamente o Pacote B 1.0 e o Pacote C requer Pacote B >= 2.0, o NuGet não poderá resolver as dependências e apresentará um erro.

![Dependências não podem ser resolvidas devido a um requisito de versão exata](media/projectJson-dependency-8.png)

Nessas situações, o consumidor de nível superior (o aplicativo ou pacote) deve adicionar sua própria dependência direta no Pacote B para que a regra [O mais próximo vence](#nearest-wins) se aplique.

## <a name="dependency-resolution-with-packagesconfig"></a>Resolução de dependência com packages.config

Com o `packages.config`, as dependências do projeto são gravadas em `packages.config` como uma lista simples. Todas as dependências desses pacotes também são gravadas na mesma lista. Quando os pacotes são instalados, o NuGet também pode modificar o arquivo `.csproj`, `app.config`, `web.config` e outros arquivos individuais.

Com `packages.config`, o NuGet tenta resolver conflitos de dependência durante a instalação de cada pacote individual. Ou seja, se o Pacote A está sendo instalado e depende do Pacote B, e este já está listado em `packages.config` como uma dependência de outra coisa, o NuGet compara as versões do Pacote B que está sendo solicitado e tenta localizar uma versão que atenda a todas as restrições de versão. Especificamente, o NuGet seleciona a versão *principal.secundária* mais antiga que satisfaça as dependências.

Por padrão, o NuGet 2.7 e anterior resolve a versão de *patch* mais recente (usando a convenção *principal.secundária.patch.build*). [NuGet 2.8 e superior](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies) altera esse comportamento para procurar para a versão de patch mais antiga por padrão. Você pode controlar essa configuração por meio do atributo `DependencyVersion` em `Nuget.Config` e a opção `-DependencyVersion` na linha de comando.  

O processo `packages.config` para resolver as dependências fica complicado para grandes grafos de dependência. Cada nova instalação do pacote exige uma transversal de todo o grafo e aumenta as chances de conflitos de versão. Quando ocorre um conflito, a instalação é interrompida, deixando o projeto em um estado indeterminado, especialmente com possíveis modificações para o arquivo de projeto. Isso não é um problema ao usar outros formatos de referência de pacote.


## <a name="managing-dependency-assets"></a>Gerenciamento de ativos de dependência

Ao usar os formatos `project.json` ou PackageReference, é possível controlar de quais ativos as dependências fluem no projeto de nível superior. Para obter detalhes, consulte [project.json](../Schema/project-json.md) e [Referências de pacote em arquivos de projeto](Package-References-in-Project-Files.md#controlling-dependency-assets).

Quando o projeto de nível superior for um pacote, você também tem controle sobre esse fluxo usando os atributos `include` e `exclude` com dependências listadas no arquivo `.nuspec`. Consulte [Referência de .nuspec – Dependências](../Schema/nuspec.md#dependencies).

## <a name="excluding-references"></a>Excluindo referências

Há cenários em que assemblies com o mesmo nome podem ser referenciados mais de uma vez em um projeto, produzindo erros de tempo de design e de tempo de build. Considere um projeto que contém uma versão personalizada do `C.dll` e faz referência ao Pacote C que também contém `C.dll`. Por outro lado, o projeto também depende do Pacote B, que também depende do Pacote C e `C.dll`. Como resultado, o NuGet não pode determinar qual `C.dll` usar, mas não é possível você apenas remover a dependência do projeto no pacote C porque o pacote B também depende dele.

Para resolver isso, você precisa referenciar diretamente o `C.dll` que você deseja (ou usar outro pacote que faz referência ao pacote correto) e, em seguida, adiciona uma dependência ao Pacote C que exclui todos os seus ativos. Isso é feito da seguinte maneira dependendo do formato de referência de pacote em uso:

- [PackageReference](../consume-packages/package-references-in-project-files.md): adicionar `Exclude="All"` à dependência:

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" Exclude="All" />
    ```

- `packages.config`: remova a referência a PackageC do arquivo `.csproj` de forma que ele faça referência somente à versão de `C.dll` que você deseja.
    
- `project.json`: adicionar `"exclude" : "all"` à dependência para PackageC:

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="dependency-updates-during-package-install"></a>Atualizações de dependência durante a instalação do pacote 

Com o NuGet 2.4.x e anterior, quando um pacote é instalado cuja dependência já existe no projeto, a dependência é atualizada para a versão mais recente que atenda as restrições de versão, mesmo se a versão existente também atender a essas restrições. 

Por exemplo, considere o pacote A que depende do pacote B e especifica 1.0 para o número de versão. O repositório de origem contém as versões 1.0, 1.1 e 1.2 do pacote B. Se A estiver instalado em um projeto que já contém a versão 1.0 do B, B será atualizado para a versão 1.2. 

Com o NuGet 2.5 e versões posteriores, se uma versão de dependência já for atendida, a dependência não será atualizada durante outras instalações de pacote. 

No mesmo exemplo acima, instalar o pacote A com o NuGet 2.5 e posteriormente deixa o pacote B 1.0 no projeto, pois ele já atende à restrição de versão. No entanto, se o pacote A solicitava a versão 1.1 ou superior de B, B 1.2 seria instalado. 

## <a name="resolving-incompatible-package-errors"></a>Resolvendo erros de pacote incompatível

Durante uma operação de restauração de pacote, você pode vir a encontrar o erro “Um ou mais pacotes não são compatíveis...” ou uma indicação de que um pacote “não é compatível” com a estrutura de destino do projeto.

Esse erro ocorre quando um ou mais dos pacotes referenciados em seu projeto não indica que eles dão suporte à estrutura de destino do projeto, ou seja, o pacote não contém uma DLL adequada em sua pasta `lib` para uma estrutura de destino que é compatível com o projeto. (Consulte [Estruturas de destino](../Schema/Target-Frameworks.md) para ver uma lista.) 

Por exemplo, se um projeto utiliza `netstandard1.6` e você tentar instalar um pacote que contém as DLLs somente nas pastas `lib\net20` e `\lib\net45`, você verá mensagens com a seguinte para o pacote e, possivelmente, seus dependentes:

```output
Restoring packages for myproject.csproj...
Package ContosoUtilities 2.1.2.3 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoUtilities 2.1.2.3 supports:
  - net20 (.NETFramework,Version=v2.0)
  - net45 (.NETFramework,Version=v4.5)
Package ContosoCore 0.86.0 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoCore 0.86.0 supports:
  - 11 (11,Version=v0.0)
  - net20 (.NETFramework,Version=v2.0)
  - sl3 (Silverlight,Version=v3.0)
  - sl4 (Silverlight,Version=v4.0)
One or more packages are incompatible with .NETStandard,Version=v1.6.
Package restore failed. Rolling back package changes for 'MyProject'.
```

Para resolver as incompatibilidades, siga um destes procedimentos:

- Redirecione seu projeto para uma estrutura que é compatível com os pacotes que você deseja usar.
- Entre em contato com o autor dos pacotes e trabalhe junto a eles para adicionar suporte à estrutura escolhida. Cada página de listagem de pacote no [nuget.org](https://www.nuget.org/) tem um link **Contatar os Proprietários** para essa finalidade.
- **Não recomendável**: como uma solução temporária enquanto você trabalha junto com o autor do pacote, projetos voltados para `netcore`, `netstandard` e `netcoreapp` pode indicar outras estruturas como compatíveis, permitindo assim que os pacotes sejam direcionados para essas outras estruturas a serem usadas. Consulte [Importações do project.json](../Schema/project-json.md#imports) e [PackageTargetFallback do restore target do MSBuild](../Schema/msbuild-targets.md#packagetargetfallback). Isso pode causar comportamentos inesperados, por isso, novamente, é melhor resolver as incompatibilidades de pacote trabalhando com o autor do pacote em uma atualização.
