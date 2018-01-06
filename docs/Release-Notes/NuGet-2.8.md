---
title: "Notas de versão do NuGet 2.8 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 77ba98d8-3d66-4126-b2b6-813ddd8ef192
description: "Notas de versão do NuGet 2.8 incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão 2.8 NuGet, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 182e7d1e2224c431631cddd14fdbea8dd9e14278
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-28-release-notes"></a>Notas de versão 2.8 do NuGet

[Notas de versão do NuGet 2.7.2](../release-notes/nuget-2.7.2.md) | [notas de versão do NuGet 2.8.1](../release-notes/nuget-2.8.1.md)

NuGet 2.8 foi lançado em 29 de janeiro de 2014.

## <a name="acknowledgements"></a>Confirmações

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466) - quando os pacotes, verificando a Id de pacote de dependência de remessa.
1. [Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [#2379](https://nuget.codeplex.com/workitem/2379) -remova o sufixo $metadata quando persistening feed credenciais.
1. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) - Especifica o arquivo de projeto para o comando de atualização de nuget.exe de suporte.
1. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) -tokens de substituição não passados com - IncludeReferencedProjects.
1. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) -corrigir nuget.push lançando OutOfMemoryException ao enviar um pacote grande.
1. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -caminho de destino incorreto de correção ao projeto faz referência a outro projeto CLI/C++.
1. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) -permita que os pacotes serão instalados como dependências de desenvolvimento por padrão
1. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) -remover implícita atualizações para a versão mais recente de patch
1. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - Vários erros corrigidos e aprimoramentos para NuGet.Server, o comando de espelho nuget.exe e outros.
    - Esse trabalho foi feito por vários meses, com Gregory trabalhar em intervalo direito para integrar o mestre para 2.8.

## <a name="patch-resolution-for-dependencies"></a>Resolução de patch para dependências

Ao resolver as dependências do pacote, o NuGet historicamente implementou uma estratégia de selecionar a versão do pacote de principais e secundárias menor que satisfaz as dependências do pacote. Ao contrário da versão principal e secundária, no entanto, a versão de patch sempre foi resolvida para a versão mais recente. Embora o comportamento foi bem intencionado, ele criado uma falta de determinismo para instalar os pacotes com dependências. Considere o exemplo a seguir:

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

Neste exemplo, embora Developer1 e Developer2 instalados PackageA@1.0.0, cada encerrado backup com uma versão diferente do PackageB. 2.8 NuGet altera esse comportamento padrão, de modo que o comportamento de resolução de dependência para versões de patch é consistente com o comportamento de versões principais e secundárias. No exemplo acima, em seguida, PackageB@1.0.0 deve ser instalado como resultado da instalação PackageA@1.0.0, independentemente da versão de patch mais recente.

## <a name="-dependencyversion-switch"></a>Opção - DependencyVersion

Embora NuGet 2.8 altera o _padrão_ comportamento para resolver as dependências, ele também adiciona um controle mais preciso sobre o processo de resolução de dependência via switch - DependencyVersion no console do Gerenciador do pacote. A opção permite que a resolução de dependências para a versão mais baixa possível (comportamento padrão), a versão mais alta possível, ou o menor mais alto ou versão de patch.  Essa opção só funciona para o pacote de instalação no comando do powershell.

![Opção DependencyVersion](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>Atributo DependencyVersion

Além de switch - DependencyVersion detalhado acima, NuGet também permitiu a capacidade de definir um novo atributo no arquivo de config definindo o que é o valor padrão, se a opção - DependencyVersion não for especificada em uma chamada de pacote de instalação. Esse valor também será respeitado pela caixa de diálogo Gerenciador de pacotes do NuGet para qualquer operação de pacote de instalação. Para definir esse valor, adicione o atributo abaixo ao seu arquivo de config:

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>Operações de NuGet de visualização com - whatif

Alguns pacotes do NuGet podem ter gráficos de dependência profunda, e como tal, pode ser útil durante a instalação, desinstalar ou operação de atualização para o primeiro consulte o que acontecerá. 2.8 NuGet adiciona o comutador padrão de - whatif do PowerShell para o pacote de instalação, desinstalar o pacote e comandos de pacote de atualização para habilitar visualizando o encerramento inteiro de pacotes para o qual o comando será aplicado. Por exemplo, executando `install-package Microsoft.AspNet.WebApi -whatif` em uma Web ASP.NET vazia aplicativo produz o seguinte.

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

Não é incomum para instalar uma versão de pré-lançamento de um pacote para investigar os novos recursos e então decidir se deseja reverter para a última versão estável. Antes do NuGet 2.8, isso era um processo de várias etapa de desinstalar o pacote de pré-lançamento e suas dependências e, em seguida, instalar a versão anterior. Com o NuGet 2.8, no entanto, o pacote de atualização agora reverterá o encerramento de pacote inteiro (por exemplo, árvore de dependência do pacote) para a versão anterior.

## <a name="development-dependencies"></a>Dependências de desenvolvimento

Muitos tipos diferentes de recursos podem ser entregues como pacotes do NuGet - incluindo ferramentas que são usadas para otimizar o processo de desenvolvimento. Esses componentes, enquanto que podem ser fundamental para o desenvolvimento de um novo pacote, não devem ser consideradas uma dependência do novo pacote quando ele é publicado posteriormente. 2.8 NuGet permite que um pacote identificar-se no `.nuspec` arquivo como um developmentDependency. Quando instalado, esses metadados também serão adicionado para o `packages.config` arquivo do projeto no qual o pacote foi instalado. Quando que `packages.config` arquivo é analisado mais tarde para dependências do NuGet durante `nuget.exe pack`, ele excluirá essas dependências marcadas como dependências de desenvolvimento.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>Arquivos individuais Packages para diferentes plataformas

Ao desenvolver aplicativos para várias plataformas de destino, é comum ter diferentes arquivos de projeto para cada um dos ambientes de compilação do respectivos. Também é comum para consumir os diferentes pacotes do NuGet em arquivos de projeto diferente, como pacotes têm vários níveis de suporte para diferentes plataformas. 2.8 NuGet oferece suporte aprimorado para este cenário, criando diferentes `packages.config` arquivos para arquivos de projeto específico da plataforma diferente.

![Vários arquivos de package.config](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>Fallback para o Cache Local

Embora os pacotes do NuGet normalmente são consumidos de uma galeria remota como [Galeria NuGet](http://www.nuget.org/) usando uma conexão de rede, há muitos cenários em que o cliente não está conectado. Sem uma conexão de rede, o cliente do NuGet não pôde instalar com êxito os pacotes - mesmo quando esses pacotes já estavam na máquina do cliente no cache local NuGet. 2.8 NuGet adiciona automática de cache fallback para o console do Gerenciador de pacote. Por exemplo, ao desconectar o adaptador de rede e instalar jQuery, o console mostra o seguinte:

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

O recurso de fallback de cache não requer quaisquer argumentos de comando específico. Além disso, o cache fallback atualmente funciona apenas no console do Gerenciador de pacote - o comportamento não funciona na caixa de diálogo de Gerenciador de pacote.

## <a name="webmatrix-nuget-client-updates"></a>As atualizações do cliente do NuGet WebMatrix

Junto com o NuGet 2.8, a extensão do NuGet para o WebMatrix também foi atualizada para incluir a muitos dos principais recursos fornecidos com [NuGet 2.5](../release-notes/nuget-2.5.md). Novos recursos incluem aqueles como 'Atualizar tudo', 'Versão do NuGet mínimo' e permitindo a substituição de arquivos de conteúdo.

Para atualizar a extensão do Gerenciador de pacotes do NuGet no WebMatrix 3:

1. Abrir o WebMatrix 3
1. Clique no ícone de extensões na faixa de opções
1. Selecione a guia atualizações
1. Clique para atualizar o NuGet Package Manager para 2.5.0
1. Feche e reinicie o WebMatrix 3

Isso é que primeira versão a equipe do NuGet da extensão do Gerenciador de pacotes do NuGet para o WebMatrix.  O código foi recentemente a contribuição pela Microsoft para o projeto do código-fonte aberto NuGet. Anteriormente, a integração do NuGet foi criada para o WebMatrix, e não pôde ser atualizado fora da banda do WebMatrix.  Agora, temos a capacidade adicional atualizá-lo junto com o restante das ferramentas de cliente do NuGet.

## <a name="bug-fixes"></a>Correções de Bug

As principais correções feitas foram melhoria de desempenho no pacote de atualização-reinstale o comando.

Além desses recursos e a correção de desempenho mencionados acima, esta versão do NuGet também inclui muitas correções de bugs. Não havia 181 questões total na versão. Para obter uma lista completa do trabalho de itens corrigidos no NuGet 2.8,. exibir o [NuGet Issue Tracker para esta versão](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).
