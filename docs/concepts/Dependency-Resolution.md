---
title: Resolução de dependências de pacote do NuGet
description: Detalhes sobre o processo por meio do qual as dependências de um pacote do NuGet são resolvidas e instaladas no NuGet 2.x e 3.x ou superior.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 4b95251e4b055523a9533b4125589b2650be932d
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237738"
---
# <a name="how-nuget-resolves-package-dependencies"></a>Como o NuGet resolve as dependências do pacote

Sempre que um pacote for instalado ou reinstalado, o que inclui o que está sendo instalado como parte de um processo de [restauração](../consume-packages/package-restore.md), o NuGet também instala todos os pacotes adicionais dos quais o primeiro pacote depende.

Essas dependências imediatas também podem ter suas próprias dependências, que podem continuar em uma profundidade arbitrária. Isso produz o que é chamado de um *grafo de dependência* que descreve as relações entre os pacotes em todos os níveis.

Quando vários pacotes têm a mesma dependência, a mesma ID de pacote pode aparecer no grafo várias vezes, potencialmente com restrições de versão diferentes. No entanto, somente uma versão de determinado pacote pode ser usada em um projeto, por isso o NuGet precisa escolher qual versão é usada. O processo exato depende do formato de gerenciamento de pacote em uso.

## <a name="dependency-resolution-with-packagereference"></a>Resolução de dependência com PackageReference

Ao instalar os pacotes em projetos usando o formato PackageReference, o NuGet adiciona referências a um grafo de pacote simples no arquivo apropriado e resolve conflitos antecipadamente. Esse processo é chamado de *restauração transitiva* . Reinstalar ou restaurar pacotes é um processo de baixar os pacotes listados no grafo, resultando em builds mais rápidos e mais previsíveis. Você também pode aproveitar as versões flutuantes, como 2,8. \* , para evitar modificar o projeto para usar a versão mais recente de um pacote.

Quando o processo de restauração do NuGet for executado antes de um build, ele resolverá as dependências primeiro na memória e, em seguida, gravará o grafo resultante em um arquivo chamado `project.assets.json`. Ele também grava as dependências resolvidas em um arquivo de bloqueio chamado `packages.lock.json`, se a [funcionalidade do arquivo de bloqueio estiver habilitada](../consume-packages/package-references-in-project-files.md#locking-dependencies).
O arquivo de ativos está localizado em `MSBuildProjectExtensionsPath`, cujo padrão é a pasta 'obj' do projeto. O MSBuild lê este arquivo e converte-o em um conjunto de pastas em que as referências em potencial podem ser encontradas e as adiciona à árvore de projeto na memória.

O arquivo `project.assets.json` é temporário e não deve ser adicionado ao controle do código-fonte. É listado por padrão em ambos `.gitignore` e `.tfignore`. Consulte [Pacotes e controle do código-fonte](../consume-packages/packages-and-source-control.md).

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

#### <a name="floating-versions"></a>Versões flutuantes

Uma versão de dependência flutuante é especificada com o \* caractere. Por exemplo, `6.0.*`. Esta especificação de versão diz "usar a versão mais recente 6.0. x"; `4.*` significa "usar a versão mais recente do 4. x". O uso de uma versão flutuante reduz as alterações no arquivo de projeto, mantendo-se atualizado com a versão mais recente de uma dependência.

Ao usar uma versão flutuante, o NuGet resolve a versão mais recente de um pacote que corresponde ao padrão de versão, por exemplo, `6.0.*` Obtém a versão mais recente de um pacote que começa com 6,0:

![Escolher a versão 6.0.1 quando uma versão flutuante 6.0.* é solicitada](media/projectJson-dependency-4.png)

> [!Note]
> Para obter informações sobre o comportamento de versões flutuantes e versões de pré-lançamento, consulte [controle de versão do pacote](package-versioning.md#version-ranges).


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

Por padrão, o NuGet 2.8 procura a versão de patch mais baixa (veja [Notas de versão do NuGet 2.8](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies)). Você pode controlar essa configuração por meio do atributo `DependencyVersion` em `Nuget.Config` e a opção `-DependencyVersion` na linha de comando.  

O processo `packages.config` para resolver as dependências fica complicado para grandes grafos de dependência. Cada nova instalação do pacote exige uma transversal de todo o grafo e aumenta as chances de conflitos de versão. Quando ocorre um conflito, a instalação é interrompida, deixando o projeto em um estado indeterminado, especialmente com possíveis modificações para o arquivo de projeto. Isso não é um problema ao usar outros formatos de gerenciamento de pacote.

## <a name="managing-dependency-assets"></a>Gerenciamento de ativos de dependência

Ao usar o formato PackageReference, é possível controlar de quais ativos as dependências fluem no projeto de nível superior. Para obter detalhes, veja [PackageReference](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

Quando o projeto de nível superior for um pacote, você também tem controle sobre esse fluxo usando os atributos `include` e `exclude` com dependências listadas no arquivo `.nuspec`. Consulte [Referência de .nuspec – Dependências](../reference/nuspec.md#dependencies).

## <a name="excluding-references"></a>Excluindo referências

Há cenários em que assemblies com o mesmo nome podem ser referenciados mais de uma vez em um projeto, produzindo erros de tempo de design e de tempo de build. Considere um projeto que contém uma versão personalizada do `C.dll` e faz referência ao Pacote C que também contém `C.dll`. Por outro lado, o projeto também depende do Pacote B, que também depende do Pacote C e `C.dll`. Como resultado, o NuGet não pode determinar qual `C.dll` usar, mas não é possível você apenas remover a dependência do projeto no pacote C porque o pacote B também depende dele.

Para resolver isso, você precisa referenciar diretamente o `C.dll` que você deseja (ou usar outro pacote que faz referência ao pacote correto) e, em seguida, adiciona uma dependência ao Pacote C que exclui todos os seus ativos. Isso é feito da seguinte maneira dependendo do formato de gerenciamento de pacote em uso:

- [PackageReference](../consume-packages/package-references-in-project-files.md): adicionar `ExcludeAssets="All"` à dependência:

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" ExcludeAssets="All" />
    ```

- `packages.config`: remova a referência a PackageC do arquivo `.csproj` de forma que ele faça referência somente à versão de `C.dll` que você deseja.
    
## <a name="dependency-updates-during-package-install"></a>Atualizações de dependência durante a instalação do pacote 

Se uma versão de dependência já for atendida, a dependência não será atualizada durante outras instalações de pacote. Por exemplo, considere o pacote A que depende do pacote B e especifica 1.0 para o número de versão. O repositório de origem contém as versões 1.0, 1.1 e 1.2 do pacote B. Se A estiver instalado em um projeto que já contém a versão 1.0 do B, B 1.0 permanecerá em uso, pois atende à restrição de versão. No entanto, se o pacote A solicitava a versão 1.1 ou superior de B, B 1.2 seria instalado. 

## <a name="resolving-incompatible-package-errors"></a>Resolvendo erros de pacote incompatível

Durante uma operação de restauração de pacote, você pode vir a encontrar o erro “Um ou mais pacotes não são compatíveis...” ou uma indicação de que um pacote “não é compatível” com a estrutura de destino do projeto.

Esse erro ocorre quando um ou mais dos pacotes referenciados em seu projeto não indica que eles dão suporte à estrutura de destino do projeto, ou seja, o pacote não contém uma DLL adequada em sua pasta `lib` para uma estrutura de destino que é compatível com o projeto. (Consulte [Estruturas de destino](../reference/target-frameworks.md) para ver uma lista.) 

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
