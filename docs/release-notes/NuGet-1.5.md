---
title: Notas de versão do NuGet 1,5
description: Notas de versão do NuGet 1,5 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940a19cdc485d611d03b52ee3102bc95a78a36bb
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383343"
---
# <a name="nuget-15-release-notes"></a>Notas de versão do NuGet 1,5

[Notas de versão do nuget 1,4](../release-notes/nuget-1.4.md) | [notas de versão do NuGet 1,6](../release-notes/nuget-1.6.md)

O NuGet 1,5 foi lançado em 30 de agosto de 2011.

## <a name="features"></a>Recursos

### <a name="project-templates-with-preinstalled-nuget-packages"></a>Modelos de projeto com pacotes NuGet pré-instalados
Ao criar um novo modelo de projeto do ASP.NET MVC 3, as bibliotecas de script do jQuery incluídas no projeto são realmente colocadas lá instalando os pacotes do NuGet.

O modelo de projeto ASP.NET MVC 3 inclui um conjunto de pacotes NuGet que são instalados quando o modelo de projeto é invocado. Essa capacidade de incluir pacotes NuGet com um modelo de projeto agora é um recurso do NuGet que _qualquer_ modelo de projeto agora pode aproveitar.

Para obter mais detalhes sobre esse recurso, leia esta [postagem de blog pelo desenvolvedor do recurso](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).

### <a name="explicit-assembly-references"></a>Referências explícitas de assembly

Adicionado um novo elemento `<references />` usado para especificar explicitamente quais assemblies no pacote devem ser referenciados.

Por exemplo, se você adicionar o seguinte:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

Em seguida, somente os `xunit.dll` e `xunit.extensions.dll` serão referenciados da [subpasta estrutura/perfil](../reference/nuspec.md#explicit-assembly-references) apropriada da pasta `lib`, mesmo se houver outros assemblies na pasta.

Se esse elemento for omitido, o comportamento usual se aplicará, que é fazer referência a cada assembly na pasta `lib`.

__Para que esse recurso é usado?__

Esse recurso dá suporte apenas a assemblies de tempo de design. Por exemplo, ao usar contratos de código, os assemblies de contrato precisam estar ao lado dos assemblies de tempo de execução que eles aumentam para que o Visual Studio possa encontrá-los, mas os assemblies de contrato não devem realmente ser referenciados pelo projeto e não devem ser copiados para a pasta `bin`.

Da mesma forma, o recurso pode ser usado para estruturas de teste de unidade, como XUnit, que precisam que seus assemblies de ferramentas estejam localizados ao lado dos assemblies de tempo de execução, mas excluídos de referências de projeto.

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>Capacidade adicional de excluir arquivos no. nuspec
O elemento `<file>` dentro de um arquivo de `.nuspec` pode ser usado para incluir um arquivo específico ou um conjunto de arquivos usando um caractere curinga. Ao usar um caractere curinga, não há como excluir um subconjunto específico dos arquivos incluídos. Por exemplo, suponha que você queira todos os arquivos de texto dentro de uma pasta, exceto um específico.

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

Use ponto e vírgula para especificar vários arquivos.

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

Ou use um curinga para excluir um conjunto de arquivos, como todos os arquivos de backup

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>Removendo pacotes usando os prompts da caixa de diálogo para remover dependências
Ao desinstalar um pacote com dependências, os prompts do NuGet, permitindo a remoção das dependências de um pacote junto com o pacote.

![Removendo pacotes dependentes](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>aperfeiçoamento do comando `Get-Package`
O comando `Get-Package` agora dá suporte a um parâmetro `-ProjectName`. Portanto, o comando

    Get-Package –ProjectName A

listará todos os pacotes instalados no projeto A.

### <a name="support-for-proxies-that-require-authentication"></a>Suporte para proxies que exigem autenticação
Ao usar o NuGet por trás de um proxy que requer autenticação, o NuGet agora solicitará credenciais de proxy. A inserção de credenciais permite que o NuGet se conecte ao repositório remoto.

### <a name="support-for-repositories-that-require-authentication"></a>Suporte para repositórios que exigem autenticação
O NuGet agora dá suporte à conexão com [repositórios privados](../hosting-packages/local-feeds.md) que exigem autenticação básica ou NTLM.

O suporte para autenticação Digest será adicionado em uma versão futura.

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Melhorias de desempenho no repositório nuget.org
Fizemos várias melhorias de desempenho na Galeria de nuget.org para tornar a listagem e a pesquisa de pacotes mais rápidas.

### <a name="solution-dialog-project-filtering"></a>Filtragem de projeto de caixa de diálogo de solução
Na caixa de diálogo nível da solução, ao solicitar quais projetos instalar, mostramos apenas os projetos que são compatíveis com o pacote selecionado.

### <a name="package-release-notes"></a>Notas de versão do pacote
Agora, os pacotes NuGet incluem suporte para notas de versão. As notas de versão aparecem apenas ao exibir _atualizações_ para um pacote, portanto, não faz sentido adicioná-las à sua primeira versão.

![Notas de versão na guia Atualizações](./media/manage-nuget-packages-release-notes.png)

Para adicionar notas de versão a um pacote, use o novo elemento de metadados `<releaseNotes />` em seu arquivo NuSpec.

### <a name="nuspec-ltfiles-gt-improvement"></a>. nuspec & melhoria de ltfiles/&gt;
O arquivo de `.nuspec` agora permite o elemento de `<files />` vazio, o que informa ao NuGet. exe para não incluir nenhum arquivo no pacote.

## <a name="bug-fixes"></a>Correções de Bug
O NuGet 1,5 tinha um total de 107 itens de trabalho corrigidos. 103 deles foram marcados como bugs.

Para obter uma lista completa de itens de trabalho corrigidos no NuGet 1,5, consulte o [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correções de bugs vale a pena observar:

* [Problema 1273](http://nuget.codeplex.com/workitem/1273): fez `packages.config` mais controle de versão amigável classificando os pacotes em ordem alfabética e removendo espaços em branco extras.
* [Problema 844](http://nuget.codeplex.com/workitem/844): os números de versão agora são normalizados para que `Install-Package 1.0` funcione em um pacote com a versão `1.0.0`.
* [Problema 1060](http://nuget.codeplex.com/workitem/1060): ao criar um pacote usando NuGet. exe, o sinalizador `-Version` substitui o elemento `<version />`.
