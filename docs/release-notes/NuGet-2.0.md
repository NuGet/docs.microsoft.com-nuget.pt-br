---
title: Notas de versão 2.0 do NuGet
description: Notas de versão do NuGet 2.0, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f32eea9260ce7e307ff56b7f3e6b48c6d98e6c90
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547569"
---
# <a name="nuget-20-release-notes"></a>Notas de versão 2.0 do NuGet

[Notas de versão do NuGet 1.8](../release-notes/nuget-1.8.md) | [notas de versão 2.1 do NuGet](../release-notes/nuget-2.1.md)

NuGet 2.0 foi lançada em 19 de junho de 2012.

## <a name="known-installation-issue"></a>Problema de instalação conhecidos
Se você estiver executando o VS 2010 SP1, você pode executar em um erro de instalação quando tentar atualizar o NuGet se você tiver uma versão mais antiga instalada.

A solução alternativa é simplesmente desinstalar o NuGet e, em seguida, instalá-lo da Galeria de extensão do VS.  Ver [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) para obter mais informações, ou [vá diretamente para o hotfix VS](http://bit.ly/vsixcertfix).

Observação: Se o Visual Studio não permitirão que você desinstale a extensão (o botão Desinstalar está desabilitado), em seguida, é provável que você precisa reiniciar o Visual Studio usando "Executar como administrador".

## <a name="package-restore-consent-is-now-active"></a>Consentimento de restauração de pacote agora está ativo

Conforme descrito neste [postar no consentimento de restauração de pacote](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 agora exigirá que receber consentimento para permitir a restauração de pacote ficar online e baixar os pacotes. Certifique-se de que você forneceu consentimento por meio da caixa de diálogo de configuração de Gerenciador de pacote ou a variável de ambiente EnableNuGetPackageRestore.

## <a name="group-dependencies-by-target-frameworks"></a>Dependências de grupo por estruturas de destino

Começando com a versão 2.0, o pacote de dependências podem variar com base no perfil da estrutura de projeto de destino. Isso é feito usando atualizada `.nuspec` esquema. O `<dependencies>` elemento agora pode conter um conjunto de `<group>` elementos. Cada grupo contém zero ou mais `<dependency>` elementos e um `targetFramework` atributo. Todas as dependências dentro de um grupo são instaladas juntos, se a estrutura de destino é compatível com o perfil de estrutura de projeto de destino. Por exemplo:

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

Observe que um grupo pode conter **zero** dependências. No exemplo acima, se o pacote for instalado em um projeto que tem como alvo o Silverlight 3.0 ou posterior, sem dependências serão instaladas. Se o pacote for instalado em um projeto que tem como alvo o .NET 4.0 ou posterior, duas dependências, o jQuery e WebActivator, serão instaladas.  Se o pacote é instalado em um projeto que tem como alvo uma versão anterior dessas 2 estruturas ou qualquer outra estrutura, RouteMagic 1.1.0 será instalado. Não há nenhuma herança entre grupos. Se a estrutura de destino do projeto corresponde a `targetFramework` atributo de um grupo, apenas as dependências dentro desse grupo será instalado.

Um pacote pode especificar as dependências do pacote em qualquer um dos dois formatos: o formato antigo de uma lista simples de `<dependency>` elementos ou grupos. Se o `<group>` formato for usado, o pacote não pode ser instalado em versões do NuGet anteriores à 2.0.

Observe que não é permitido misturar os dois formatos. Por exemplo, é o trecho a seguir **inválido** e serão rejeitadas pelo NuGet.

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>Agrupar arquivos de conteúdo e scripts do PowerShell por estrutura de destino

Além das referências de assembly, arquivos de conteúdo e scripts do PowerShell também podem ser agrupados pela estrutura de destino. A mesma estrutura de pasta encontrada na `lib` agora pode ser aplicada a pasta para especificar a estrutura de destino da mesma forma para o `content` e `tools` pastas. Por exemplo:

    \content
        \net11
            \MyContent.txt
        \net20
            \MyContent20.txt
        \net40
        \sl40
            \MySilverlightContent.html

    \tools
        \init.ps1
        \net40
            \install.ps1
            \uninstall.ps1
        \sl40
            \install.ps1
            \uninstall.ps1

**Observação**: porque `init.ps1` é executada no nível da solução e é independente de qualquer projeto individual, ele deve ser colocado diretamente sob o `tools` pasta. Se colocado dentro de uma pasta específica do framework, ele será ignorado.

Além disso, um novo recurso do NuGet 2.0 é que uma pasta de framework pode ser *vazio*, caso em que o NuGet adicionará não adicionar referências de assembly, arquivos de conteúdo ou executar scripts do PowerShell para a versão de estrutura específico. No exemplo acima, a pasta `content\net40` está vazio.

## <a name="improved-tab-completion-performance"></a>Desempenho de conclusão de guia aprimorado
O recurso de preenchimento no Console do Gerenciador de pacotes NuGet atualizou para melhorar significativamente o desempenho. Haverá muito menos atraso entre o momento em que a tecla tab é pressionada até que seja exibida a lista suspensa de sugestões.

## <a name="bug-fixes"></a>Correções de Bug
NuGet 2.0 inclui muitas correções de bugs com ênfase em consentimento de restauração de pacote e o desempenho.
Para obter uma lista completa de trabalho itens corrigidos no NuGet 2.0, por favor, modo de exibição de [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
