---
title: "Notas de versão do NuGet 1.5 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de versão do NuGet 1.5 incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão 1.5 do NuGet, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9f93000cd5e86cb8f3798e32daf6a4ded0d4e9c3
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-15-release-notes"></a>Notas de versão 1.5 do NuGet

[Notas de versão do NuGet 1.4](../release-notes/nuget-1.4.md) | [notas de versão 1.6 do NuGet](../release-notes/nuget-1.6.md)

1.5 NuGet foi lançada em 30 de agosto de 2011.

## <a name="features"></a>Recursos

### <a name="project-templates-with-preinstalled-nuget-packages"></a>Modelos de projeto com pacotes do NuGet pré-instalado
Ao criar um novo modelo de projeto do ASP.NET MVC 3, as bibliotecas de scripts jQuery incluídas no projeto, na verdade, são colocadas nesse local instalando pacotes do NuGet.

O modelo de projeto do ASP.NET MVC 3 inclui um conjunto de pacotes do NuGet é instalado quando o modelo de projeto é invocado. Essa capacidade de incluir pacotes do NuGet com um modelo de projeto agora é um recurso do NuGet que _qualquer_ modelo de projeto agora pode tirar proveito do.

Para obter mais detalhes sobre esse recurso, leia este [postagem de blog pelo desenvolvedor do recurso](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).

### <a name="explicit-assembly-references"></a>Referências de Assembly explícita

Adicionado um novo `<references />` usado para especificar explicitamente os assemblies dentro do elemento de pacote deve ser referenciado.

Por exemplo, se você adicionar o seguinte:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

E somente a `xunit.dll` e `xunit.extensions.dll` será referenciado do apropriada [framework/perfil](../reference/nuspec.md#explicit-assembly-references) do `lib` pasta mesmo se houver outros assemblies na pasta.

Se esse elemento for omitido, o comportamento comum se aplica, que é fazer referência a cada assembly no `lib` pasta.

__O que esse recurso é usado?__

Esse recurso oferece suporte a apenas assemblies de tempo de design. Por exemplo, ao usar contratos de código, os assemblies de contrato precisam ser próximo os assemblies de tempo de execução que eles aumentar para que o Visual Studio pode encontrá-los, mas os assemblies de contrato, na verdade, não devem ser referenciados pelo projeto e não devem ser copiados para o `bin` pasta.

Da mesma forma, o recurso pode ser usado para estruturas de teste de unidade como XUnit que precisam de seus conjuntos de ferramentas localizada ao lado de assemblies de tempo de execução, mas excluídas de referências de projeto.

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>Foi incluída a capacidade de excluir os arquivos. o NuSpec
O `<file>` elemento dentro de um `.nuspec` arquivo pode ser usado para incluir um arquivo específico ou um conjunto de arquivos usando um curinga. Ao usar um caractere curinga, não é possível excluir um subconjunto específico de arquivos incluídos. Por exemplo, suponha que você deseja que todos os arquivos de texto dentro de uma pasta, exceto um específico.

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

Ou use um caractere curinga para excluir um conjunto de arquivos, como todos os arquivos de backup

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>Remover pacotes usando a caixa de diálogo solicita para remover dependências
Quando você desinstala um pacote com dependências, solicita que o NuGet, que permite a remoção de dependências do pacote junto com o pacote.

![Removendo pacotes dependentes](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package` Aperfeiçoamento de comando
O `Get-Package` comando agora dá suporte a um `-ProjectName` parâmetro. Portanto o comando

    Get-Package –ProjectName A

lista todos os pacotes instalados no projeto A.

### <a name="support-for-proxies-that-require-authentication"></a>Suporte para Proxies que requer autenticação
Ao usar o NuGet atrás de um proxy que requer autenticação, NuGet agora solicitará as credenciais de proxy. Inserir credenciais permite que o NuGet para se conectar ao repositório remoto.

### <a name="support-for-repositories-that-require-authentication"></a>Suporte para repositórios que requer autenticação
NuGet agora dá suporte ao conectar-se a [repositórios privados](../hosting-packages/local-feeds.md) que exigem autenticação básica ou NTLM.

Suporte para a autenticação Digest será adicionado em uma versão futura.

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Aprimoramentos de desempenho para o repositório nuget.org
Fizemos vários aprimoramentos de desempenho para a Galeria nuget.org para tornar o pacote de listagem e a pesquisa mais rápida.

### <a name="solution-dialog-project-filtering"></a>A filtragem do projeto da caixa de diálogo de solução
No diálogo nível de solução, ao pedir que projetos instalar, mostramos somente projetos que são compatíveis com o pacote selecionado.

### <a name="package-release-notes"></a>Notas de versão do pacote
Pacotes do NuGet agora incluem suporte para notas de versão. As notas de versão só mostra backup ao exibir _atualizações_ para um pacote, portanto não faz sentido para adicioná-los para sua primeira versão.

![Notas de versão na guia atualizações](./media/manage-nuget-packages-release-notes.png)

Para adicionar notas de versão para um pacote, use o novo `<releaseNotes />` elemento de metadados em seu arquivo NuSpec.

### <a name="nuspec-ltfiles-gt-improvement"></a>. NuSpec & ltfiles /&gt; aperfeiçoamento
O `.nuspec` arquivo agora permite vazio `<files />` elemento, que informa o nuget.exe para não incluir qualquer arquivo no pacote.

## <a name="bug-fixes"></a>Correções de Bug
1.5 NuGet tinha um total de 107 fixos de itens de trabalho. 103 deles foram marcadas como bugs.

Para obter uma lista completa de trabalho itens corrigidos no NuGet 1.5, por favor, exibição de [NuGet Issue Tracker para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correções de bug, vale a pena observar:

* [Problema 1273](http://nuget.codeplex.com/workitem/1273): feitas `packages.config` mais controle de versão amigável classificação pacotes em ordem alfabética e removendo o espaço em branco extra.
* [Problema 844](http://nuget.codeplex.com/workitem/844): números de versão agora são normalizados para que `Install-Package 1.0` funciona em um pacote com a versão `1.0.0`.
* [Problema 1060](http://nuget.codeplex.com/workitem/1060): ao criar um pacote usando o nuget.exe, o `-Version` sinalizador substituições de `<version />` elemento.
