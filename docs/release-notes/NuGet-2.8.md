---
title: Notas de versão 2.8 do NuGet
description: Notas de versão do NuGet 2.8, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547453"
---
# <a name="nuget-28-release-notes"></a>Notas de versão 2.8 do NuGet

[Notas de versão do NuGet 2.7.2](../release-notes/nuget-2.7.2.md) | [notas de versão do NuGet 2.8.1](../release-notes/nuget-2.8.1.md)

NuGet 2.8 foi lançado em 29 de janeiro de 2014.

## <a name="acknowledgements"></a>Confirmações

1. [Fazer Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466) - ao empacotar pacotes, verificando a identificação de pacotes de dependência.
2. [Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [#2379](https://nuget.codeplex.com/workitem/2379) -remover o sufixo $metadata quando persistening feed credenciais.
3. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) – Especifica o arquivo de projeto para o comando de atualização nuget.exe de suporte.
4. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) -tokens de substituição não é passados com - IncludeReferencedProjects.
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) -corrigir nuget.push lançando OutOfMemoryException ao enviar um pacote grande.
6. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -correção de caminho de destino incorreto quando o projeto referencia outro projeto CLI/C++.
7. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) -permitir que os pacotes serão instalados como dependências de desenvolvimento por padrão
8. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) -remover implícitas atualizações para a versão de patch mais recente
9. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - Várias correções de bug e melhorias para NuGet. Server, o comando de espelho nuget.exe e outros.
    - Esse trabalho foi realizado durante vários meses, com Gregory trabalhar no tempo certo para integrar o mestre de 2.8.

## <a name="patch-resolution-for-dependencies"></a>Resolução de patch para dependências

Para resolver as dependências do pacote, o NuGet historicamente implementou uma estratégia de selecionar a versão mais antiga do pacote principal e secundária que satisfaça as dependências do pacote. Ao contrário da versão principal e secundária, no entanto, a versão de patch sempre foi resolvida para a versão mais recente. Embora o comportamento era bem-intencionado, ele criou uma falta de determinismo para instalar pacotes com dependências. Considere o exemplo a seguir:

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

Neste exemplo, embora Developer1 e Developer2 instalados PackageA@1.0.0, cada encerrado-se com uma versão diferente do PackageB. NuGet 2.8 altera esse comportamento padrão, de modo que o comportamento de resolução de dependência para versões de patch é consistente com o comportamento de versões principais e secundárias. No exemplo acima, em seguida, PackageB@1.0.0 seria instalado como resultado da instalação PackageA@1.0.0, independentemente da versão de patch mais recente.

## <a name="-dependencyversion-switch"></a>Opção DependencyVersion-

Embora o NuGet 2.8 altera a _padrão_ comportamento para resolver as dependências, ele também adiciona um controle mais preciso sobre o processo de resolução de dependência por meio da opção - DependencyVersion no console do Gerenciador de pacotes. O comutador permite resolver as dependências para a versão mais antiga possível (comportamento padrão), a versão mais alta possível, ou o mais alto minor ou versão de patch.  Essa opção só funciona para o pacote de instalação no comando do powershell.

![Opção DependencyVersion](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>Atributo DependencyVersion

Além do comutador - DependencyVersion detalhado acima, o NuGet também permitiu a capacidade de definir um novo atributo no arquivo NuGet. config definindo o que é o valor padrão, se o comutador - DependencyVersion não for especificado em uma invocação de pacote de instalação. Esse valor também será respeitado pela caixa de diálogo Gerenciador de pacotes NuGet para operações de pacote de instalação. Para definir esse valor, adicione o atributo abaixo ao seu arquivo NuGet. config:

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>Operações do NuGet de visualização com - whatif

Alguns pacotes do NuGet podem ter gráficos de dependência profunda, e como tal, ele pode ser útil durante a instalação, desinstalar ou operação de atualização para o primeiro ver o que acontecerá. NuGet 2.8 adiciona o comutador padrão de - whatif do PowerShell para o pacote de instalação, desinstalar-package e comandos do pacote de atualização para habilitar a visualizar o fechamento inteiro de pacotes para o qual o comando será aplicado. Por exemplo, executando `install-package Microsoft.AspNet.WebApi -whatif` em uma Web vazio do ASP.NET o aplicativo produz o seguinte.

    PM> install-package Microsoft.AspNet.WebApi -whatif
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.WebHost (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Core (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Client (≥ 5.0.0)'.
    Attempting to resolve dependency 'Newtonsoft.Json (≥ 4.5.11)'.
    Install Newtonsoft.Json 4.5.11
    Install Microsoft.AspNet.WebApi.Client 5.0.0
    Install Microsoft.AspNet.WebApi.Core 5.0.0
    Install Microsoft.AspNet.WebApi.WebHost 5.0.0
    Install Microsoft.AspNet.WebApi 5.0.0

## <a name="downgrade-package"></a>Pacote de downgrade

Não é incomum para instalar uma versão de pré-lançamento de um pacote para investigar os novos recursos e então decidir se deseja reverter para a última versão estável. Antes do NuGet 2.8, isso era um processo de várias etapa de desinstalar o pacote de pré-lançamento e suas dependências e, em seguida, instalar a versão anterior. Com o NuGet 2.8, no entanto, o pacote de atualização agora reverterá o fechamento do pacote inteiro (por exemplo, árvore de dependência do pacote) para a versão anterior.

## <a name="development-dependencies"></a>Dependências de desenvolvimento

Muitos tipos diferentes de recursos podem ser entregues como pacotes do NuGet – incluindo as ferramentas que são usadas para otimizar o processo de desenvolvimento. Esses componentes, embora eles podem ser muito útil no desenvolvimento de um novo pacote, não devem ser considerados uma dependência do novo pacote quando ele é publicado posteriormente. NuGet 2.8 habilita um pacote para identificar a mesmo no `.nuspec` arquivo como um developmentDependency. Quando instalado, esses metadados também serão adicionados para o `packages.config` arquivo do projeto no qual o pacote foi instalado. Quando que `packages.config` arquivo é analisado posteriormente para as dependências do NuGet durante `nuget.exe pack`, ela exclui essas dependências marcadas como dependências de desenvolvimento.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>Arquivos Packages. config individuais para diferentes plataformas

Ao desenvolver aplicativos para várias plataformas de destino, é comum ter diferentes arquivos de projeto para cada um dos ambientes de compilação respectivo. Também é comum para consumir diferentes pacotes do NuGet em arquivos de projeto diferentes, como pacotes têm diferentes níveis de suporte para plataformas diferentes. NuGet 2.8 oferece suporte aprimorado para esse cenário, criando diferentes `packages.config` arquivos para arquivos de projeto diferente de específico da plataforma.

![Vários arquivos Package](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>Fallback para o Cache Local

Embora os pacotes do NuGet normalmente são consumidos de uma galeria remota, como [Galeria do NuGet](http://www.nuget.org/) usando uma conexão de rede, há muitos cenários em que o cliente não está conectado. Sem uma conexão de rede, o cliente do NuGet não foi capaz de instalar com êxito pacotes – mesmo quando esses pacotes já estavam na máquina do cliente no cache local do NuGet. NuGet 2.8 adiciona o fallback de cache automático para o console do Gerenciador de pacotes. Por exemplo, quando se desconectar o adaptador de rede e instalar jQuery, o console mostra o seguinte:

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

O recurso de fallback de cache não requer nenhum argumento de comando específico. Além disso, o cache fallback atualmente funciona apenas no console de Gerenciador de pacotes – o comportamento não funciona no momento na caixa de diálogo de Gerenciador de pacote.

## <a name="webmatrix-nuget-client-updates"></a>As atualizações do cliente do NuGet WebMatrix

Juntamente com o NuGet 2.8, a extensão do NuGet para o WebMatrix também foi atualizada para incluir muitos dos principais recursos fornecidos com [NuGet 2.5](../release-notes/nuget-2.5.md). Novos recursos incluem aqueles, como 'Atualizar tudo', 'Mínimo a versão do NuGet' e permitindo a substituição de arquivos de conteúdo.

Para atualizar sua extensão de Gerenciador de pacotes NuGet no WebMatrix 3:

1. Abre o WebMatrix 3
1. Clique no ícone de extensões na faixa de opções
1. Selecione a guia atualizações
1. Clique para atualizar o Gerenciador de pacotes NuGet para 2.5.0
1. Feche e reinicie o WebMatrix 3

Esta é primeira versão a equipe NuGet da extensão do Gerenciador de pacotes NuGet para o WebMatrix.  O código foi recentemente contribuído pela Microsoft para o projeto de NuGet de código-fonte aberto. Anteriormente, a integração com o NuGet foi incorporada ao WebMatrix e não pôde ser atualizado fora de banda do WebMatrix.  Agora, temos a capacidade adicional atualizá-lo junto com as outras ferramentas de cliente do NuGet.

## <a name="bug-fixes"></a>Correções de Bug

Um das principais correções de bug feitas era melhoria de desempenho no pacote de atualização-reinstale o comando.

Além desses recursos e a correção de desempenho mencionado anteriormente, esta versão do NuGet também inclui muitas correções de bugs. Havia 181 total de problemas abordados na versão. Para obter uma lista completa de trabalho itens corrigidos no NuGet 2.8, por favor, modo de exibição de [rastreador de problemas do NuGet para esta versão](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).
