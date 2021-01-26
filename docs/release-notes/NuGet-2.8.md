---
title: Notas de versão do NuGet 2,8
description: Notas de versão do NuGet 2,8 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cb77cf0f049b5b3cfe1039d83ab58e33457674bf
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776714"
---
# <a name="nuget-28-release-notes"></a>Notas de versão do NuGet 2,8

Notas de versão do [NuGet 2.7.2](../release-notes/nuget-2.7.2.md)  |  [Notas de versão do NuGet 2.8.1](../release-notes/nuget-2.8.1.md)

O NuGet 2,8 foi lançado em 29 de janeiro de 2014.

## <a name="acknowledgements"></a>Confirmações

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ( [@leppie](https://twitter.com/leppie) )
    - [#3466](https://nuget.codeplex.com/workitem/3466) -ao empacotar pacotes, verificando a ID dos pacotes de dependência.
2. [Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ( [@maartenballiauw](https://twitter.com/maartenballiauw) )
    - [#2379](https://nuget.codeplex.com/workitem/2379) -remova o sufixo $Metadata quando as credenciais do feed persistening.
3. [Filip de vos](https://www.codeplex.com/site/users/view/FilipDeVos) ( [@foxtricks](https://twitter.com/foxtricks) )
    - [#3538](http://nuget.codeplex.com/workitem/3538) -suporte ao especificar o arquivo de projeto para o comando nuget.exe Update.
4. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - tokens de substituição de [#3536](http://nuget.codeplex.com/workitem/3536) não passados com-IncludeReferencedProjects.
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ( [@Sarkie_Dave](https://twitter.com/Sarkie_Dave) )
    - [#3677](http://nuget.codeplex.com/workitem/3677) -corrigir o NuGet. push que lança OutOfMemoryException ao enviar um pacote grande.
6. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -corrigir caminho de destino incorreto quando o projeto faz referência a outro projeto de CLI/C++.
7. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ( [@adamralph](https://twitter.com/adamralph) )
    - [#3639](https://nuget.codeplex.com/workitem/3639) -permitir que os pacotes sejam instalados como dependências de desenvolvimento por padrão
8. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ( [@davidfowl](https://twitter.com/davidfowl) )
    - [#3717](https://nuget.codeplex.com/workitem/3717) -remover atualizações implícitas para a versão mais recente do patch
9. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - Várias correções de bugs e aprimoramentos para NuGet. Server, o comando nuget.exe Mirror e outros.
    - Esse trabalho foi feito em vários meses, com Gregory trabalhando conosco no prazo certo para integrar-se ao mestre para 2,8.

## <a name="patch-resolution-for-dependencies"></a>Resolução de patch para dependências

Ao resolver dependências de pacote, o NuGet implementou historicamente uma estratégia de seleção da versão mais baixa e secundária do pacote que satisfaz as dependências no pacote. No entanto, ao contrário da versão principal e secundária, a versão do patch foi sempre resolvida para a versão mais recente. Embora o comportamento tenha sido bem intencional, ele criou uma falta de determinantes para a instalação de pacotes com dependências. Considere o seguinte exemplo:

```
PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

PackageB@1.0.1 is published

Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1
```

Neste exemplo, embora o Developer1 e o Developer2 estejam instalados PackageA@1.0.0 , cada um acaba com uma versão diferente do PackageB. O NuGet 2,8 altera esse comportamento padrão de modo que o comportamento de resolução de dependência para versões de patch seja consistente com o comportamento das versões principal e secundária. No exemplo acima, o PackageB@1.0.0 seria instalado como resultado da instalação PackageA@1.0.0 , independentemente da versão mais recente do patch.

## <a name="-dependencyversion-switch"></a>Opção-DependencyVersion

Embora o NuGet 2,8 altere o comportamento _padrão_ para resolver dependências, ele também adiciona controle mais preciso sobre o processo de resolução de dependência por meio da opção-DependencyVersion no console do Gerenciador de pacotes. A opção habilita a resolução de dependências para a versão mais baixa possível (comportamento padrão), a versão mais alta possível ou a versão secundária ou de patch mais alta.  Essa opção funciona apenas para Install-Package no comando do PowerShell.

![Comutador DependencyVersion](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>Atributo DependencyVersion

Além da opção-DependencyVersion detalhadamente acima, o NuGet também permitiu a capacidade de definir um novo atributo no arquivo de Nuget.Config que define o valor padrão, se a opção-DependencyVersion não for especificada em uma invocação de install-Package. Esse valor também será respeitado pela caixa de diálogo Gerenciador de pacotes NuGet para qualquer operação de pacote de instalação. Para definir esse valor, adicione o atributo abaixo ao arquivo Nuget.Config:

```xml
<config>
    <add key="dependencyversion" value="Highest" />
</config>
```

## <a name="preview-nuget-operations-with--whatif"></a>Visualizar operações do NuGet com-WhatIf

Alguns pacotes NuGet podem ter grafos de dependência profunda e, como tal, podem ser úteis durante uma operação de instalação, desinstalação ou atualização para ver primeiro o que acontecerá. O NuGet 2,8 adiciona a opção PowerShell-WhatIf padrão aos comandos install-Package, Uninstall-Package e Update-Package para habilitar a visualização do fechamento completo de pacotes aos quais o comando será aplicado. Por exemplo, `install-package Microsoft.AspNet.WebApi -whatif` a execução em um aplicativo Web ASP.net vazio produz o seguinte.

```
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
```

## <a name="downgrade-package"></a>Fazer downgrade do pacote

Não é incomum instalar uma versão de pré-lançamento de um pacote para investigar novos recursos e, em seguida, decidir reverter para a última versão estável. Antes do NuGet 2,8, esse era um processo de várias etapas para desinstalar o pacote de pré-lançamento e suas dependências e, em seguida, instalar a versão anterior. Com o NuGet 2,8, no entanto, o Update-Package agora reverterá todo o fechamento do pacote (por exemplo, a árvore de dependência do pacote) para a versão anterior.

## <a name="development-dependencies"></a>Dependências de desenvolvimento

Muitos tipos diferentes de recursos podem ser fornecidos como pacotes NuGet, incluindo ferramentas que são usadas para otimizar o processo de desenvolvimento. Esses componentes, embora possam ser fundamentais no desenvolvimento de um novo pacote, não devem ser considerados uma dependência do novo pacote quando ele é publicado posteriormente. O NuGet 2,8 permite que um pacote se identifique no `.nuspec` arquivo como um developmentDependency. Quando instalado, esses metadados também serão adicionados ao `packages.config` arquivo do projeto no qual o pacote foi instalado. Quando esse `packages.config` arquivo for posteriormente analisado para dependências do NuGet durante `nuget.exe pack` , ele excluirá as dependências marcadas como dependências de desenvolvimento.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>Arquivos de packages.config individuais para diferentes plataformas

Ao desenvolver aplicativos para várias plataformas de destino, é comum ter arquivos de projeto diferentes para cada um dos respectivos ambientes de compilação. Também é comum consumir diferentes pacotes NuGet em arquivos de projeto diferentes, pois os pacotes têm níveis variados de suporte para diferentes plataformas. O NuGet 2,8 fornece suporte aprimorado para esse cenário criando `packages.config` arquivos diferentes para diferentes arquivos de projeto específicos da plataforma.

![Vários arquivos package.config](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>Fallback para o cache local

Embora os pacotes NuGet normalmente sejam consumidos de uma galeria remota, como [a galeria do NuGet](http://www.nuget.org/) usando uma conexão de rede, há muitos cenários em que o cliente não está conectado. Sem uma conexão de rede, o cliente NuGet não conseguiu instalar pacotes com êxito, mesmo quando esses pacotes já estavam no computador do cliente no cache do NuGet local. O NuGet 2,8 adiciona o fallback de cache automático para o console do Gerenciador de pacotes. Por exemplo, ao desconectar o adaptador de rede e instalar o jQuery, o console do mostra o seguinte:

```
PM> Install-Package jquery
The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
Installing 'jQuery 2.0.3'.
Successfully installed 'jQuery 2.0.3'.
Adding 'jQuery 2.0.3' to WebApplication18.
Successfully added 'jQuery 2.0.3' to WebApplication18.
```

O recurso fallback de cache não requer nenhum argumento de comando específico. Além disso, o fallback de cache atualmente funciona apenas no console do Gerenciador de pacotes-o comportamento não funciona atualmente na caixa de diálogo Gerenciador de pacotes.

## <a name="webmatrix-nuget-client-updates"></a>Atualizações de cliente do WebMatrix NuGet

Junto com o NuGet 2,8, a extensão do NuGet para WebMatrix também foi atualizada para incluir muitos dos principais recursos fornecidos com o [NuGet 2,5](../release-notes/nuget-2.5.md). Os novos recursos incluem aqueles como "atualizar tudo", "versão mínima do NuGet" e permitir a substituição de arquivos de conteúdo.

Para atualizar sua extensão do Gerenciador de pacotes NuGet no WebMatrix 3:

1. Abrir o WebMatrix 3
1. Clique no ícone extensões na faixa de faixas
1. Selecione a guia Atualizações
1. Clique para atualizar o Gerenciador de pacotes NuGet para 2.5.0
1. Fechar e reiniciar o WebMatrix 3

Esta é a primeira versão da equipe do NuGet da extensão do Gerenciador de pacotes NuGet para o WebMatrix.  O código foi contribuído recentemente pela Microsoft para o projeto NuGet de código-fonte aberto. Anteriormente, a integração do NuGet foi criada no WebMatrix e não podia ser atualizada fora da banda do WebMatrix.  Agora temos a capacidade de atualizá-lo ainda mais junto com o restante das ferramentas de cliente do NuGet.

## <a name="bug-fixes"></a>Correções de bugs

Uma das principais correções de bugs feitas foi a melhoria no desempenho do comando Update-Package-REINSTALL.

Além desses recursos e da correção de desempenho mencionada anteriormente, esta versão do NuGet também inclui muitas outras correções de bugs. Havia 181 problemas totais abordados na versão. Para obter uma lista completa dos itens de trabalho corrigidos no NuGet 2,8, consulte o [rastreador de problemas do NuGet para esta versão](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).
