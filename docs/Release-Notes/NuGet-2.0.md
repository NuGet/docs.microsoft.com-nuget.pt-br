---
title: "Notas de versão do NuGet 2.0 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 51c7e94f-0084-4c62-bfba-7dfd81675361
description: "Notas de versão do NuGet 2.0, incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão 2.0 do NuGet, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 41eed1a7c6ad91d63813fb74986aa498765f3dea
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-20-release-notes"></a>Notas de versão 2.0 do NuGet

[Notas de versão do NuGet 1.8](../release-notes/nuget-1.8.md) | [notas de versão 2.1 do NuGet](../release-notes/nuget-2.1.md)

NuGet 2.0 foi lançada em 19 de junho de 2012.

## <a name="known-installation-issue"></a>Problema de instalação conhecidos
Se você estiver executando o VS 2010 SP1, você pode executar em um erro de instalação durante a tentativa de atualizar o NuGet se você tiver uma versão mais antiga.

A solução alternativa é simplesmente desinstalar NuGet e, em seguida, instalá-lo a partir da Galeria de extensão do VS.  Consulte [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) para obter mais informações, ou [vá diretamente para o hotfix VS](http://bit.ly/vsixcertfix).

Observação: Se o Visual Studio não permitirão que você desinstalar a extensão (o botão de desinstalação estiver desabilitado), em seguida, provavelmente você precisa reiniciar o Visual Studio usando "Executar como administrador".

## <a name="package-restore-consent-is-now-active"></a>Consentimento de restauração do pacote agora está ativo

Conforme descrito neste [postar no pacote restauração consentimento](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 agora exigirá que receber consentimento para permitir a restauração do pacote ficar online e baixar os pacotes. Certifique-se de que você forneceu consentimento via o diálogo de configuração do Gerenciador de pacote ou a variável de ambiente EnableNuGetPackageRestore.

## <a name="group-dependencies-by-target-frameworks"></a>Dependências de grupo pela estrutura de destino

Dependências podem variar de pacote a partir da versão 2.0, baseada no perfil de estrutura de projeto de destino. Isso é feito usando atualizada `.nuspec` esquema. O `<dependencies>` elemento agora pode conter um conjunto de `<group>` elementos. Cada grupo contém zero ou mais `<dependency>` elementos e um `targetFramework` atributo. Todas as dependências dentro de um grupo são instaladas juntos, se a estrutura de destino é compatível com o perfil de estrutura de projeto de destino. Por exemplo:

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

Observe que um grupo pode conter **zero** dependências. No exemplo acima, se o pacote for instalado em um projeto que tem como alvo o Silverlight 3.0 ou posterior, nenhuma dependência será instalada. Se o pacote for instalado em um projeto que tem como alvo o .NET 4.0 ou posterior, duas dependências, jQuery e WebActivator, serão instaladas.  Se o pacote for instalado em um projeto que tem como alvo uma versão anterior dessas estruturas de 2 ou qualquer outra estrutura, RouteMagic 1.1.0 será instalado. Não há nenhuma herança entre grupos. Se a estrutura de destino do projeto corresponde a `targetFramework` atributo de um grupo, somente as dependências dentro desse grupo será instalado.

Um pacote pode especificar as dependências do pacote em um dos dois formatos: o formato antigo de uma lista simples de `<dependency>` elementos ou grupos. Se o `<group>` formato é usado, o pacote não pode ser instalado em versões anteriores à 2.0 do NuGet.

Observe que não é permitido misturar os dois formatos. Por exemplo, o trecho a seguir é **inválido** e serão rejeitadas pelo NuGet.

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>Agrupando arquivos de conteúdo e scripts do PowerShell do framework de destino

Além de referências de assembly, arquivos de conteúdo e scripts do PowerShell também podem ser agrupados pela estrutura de destino. A mesma estrutura de pasta encontrado no `lib` agora pode ser aplicada a pasta para especificar a estrutura de destino da mesma forma para o `content` e `tools` pastas. Por exemplo:

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

**Observação**: porque `init.ps1` é executada no nível da solução e é independente de qualquer projeto individual, ele deve ser colocado diretamente sob o `tools` pasta. Se colocado dentro de uma pasta específica da estrutura, ele será ignorado.

Além disso, um novo recurso do NuGet 2.0 é que uma pasta da estrutura pode ser *vazio*, nesse caso, o NuGet não adicionará referências de assembly, adicionar arquivos de conteúdo ou executar scripts do PowerShell para a versão do framework específico. No exemplo acima, a pasta `content\net40` está vazio.

## <a name="improved-tab-completion-performance"></a>Desempenho de conclusão de guia aprimorado
O recurso de preenchimento no Console do Gerenciador de pacotes do NuGet foi atualizado para melhorar significativamente o desempenho. Haverá menos atraso entre o momento em que a tecla tab é pressionada até que seja exibida a lista suspensa de sugestões.

## <a name="bug-fixes"></a>Correções de Bug
NuGet 2.0 inclui muitas correções de bugs com ênfase em consentimento de restauração do pacote e o desempenho.
Para obter uma lista completa de trabalho itens corrigidos no NuGet 2.0, por favor, exibição de [NuGet Issue Tracker para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
