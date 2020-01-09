---
title: Notas de versão do NuGet 2,0
description: Notas de versão do NuGet 2,0 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 01fdbfafcaea009cf119dfa880b2b16539c9b088
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383061"
---
# <a name="nuget-20-release-notes"></a>Notas de versão do NuGet 2,0

[Notas de versão do nuget 1,8](../release-notes/nuget-1.8.md) | [notas de versão do NuGet 2,1](../release-notes/nuget-2.1.md)

O NuGet 2,0 foi lançado em 19 de junho de 2012.

## <a name="known-installation-issue"></a>Problema de instalação conhecido
Se você estiver executando o VS 2010 SP1, poderá encontrar um erro de instalação ao tentar atualizar o NuGet se tiver uma versão mais antiga instalada.

A solução alternativa é simplesmente desinstalar o NuGet e, em seguida, instalá-lo a partir da Galeria de extensões do VS.  Consulte <https://support.microsoft.com/kb/2581019> para obter mais informações ou [vá diretamente para o hotfix do vs](http://bit.ly/vsixcertfix).

Observação: se o Visual Studio não permitir que você desinstale a extensão (o botão desinstalar está desabilitado), provavelmente, você precisará reiniciar o Visual Studio usando "executar como administrador".

## <a name="package-restore-consent-is-now-active"></a>O consentimento de restauração do pacote agora está ativo

Conforme descrito nesta [postagem no consentimento de restauração de pacote](http://blog.nuget.org/20120518/package-restore-and-consent.html), o NuGet 2,0 agora exigirá que o consentimento seja fornecido para habilitar a restauração do pacote para ficar online e baixar pacotes. Verifique se você forneceu o consentimento por meio da caixa de diálogo configuração do Gerenciador de pacotes ou da variável de ambiente EnableNuGetPackageRestore.

## <a name="group-dependencies-by-target-frameworks"></a>Agrupar dependências por estruturas de destino

A partir da versão 2,0, as dependências de pacote podem variar com base no perfil de estrutura do projeto de destino. Isso é feito usando um esquema de `.nuspec` atualizado. O elemento `<dependencies>` agora pode conter um conjunto de elementos `<group>`. Cada grupo contém zero ou mais elementos `<dependency>` e um atributo `targetFramework`. Todas as dependências dentro de um grupo serão instaladas juntas se a estrutura de destino for compatível com o perfil de estrutura do projeto de destino. Por exemplo:

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

Observe que um grupo pode conter **zero** dependências. No exemplo acima, se o pacote for instalado em um projeto direcionado ao Silverlight 3,0 ou posterior, nenhuma dependência será instalada. Se o pacote for instalado em um projeto direcionado ao .NET 4,0 ou posterior, duas dependências, jQuery e webactivator serão instaladas.  Se o pacote for instalado em um projeto direcionado a uma versão anterior dessas duas estruturas, ou qualquer outra estrutura, o RouteMagic 1.1.0 será instalado. Não há herança entre grupos. Se a estrutura de destino de um projeto corresponder ao atributo `targetFramework` de um grupo, somente as dependências dentro desse grupo serão instaladas.

Um pacote pode especificar dependências de pacote em um dos dois formatos: o formato antigo de uma lista simples de elementos de `<dependency>` ou grupos. Se o formato de `<group>` for usado, o pacote não poderá ser instalado em versões do NuGet anteriores a 2,0.

Observe que a combinação dos dois formatos não é permitida. Por exemplo, o trecho a seguir é **inválido** e será rejeitado pelo NuGet.

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>Agrupando arquivos de conteúdo e scripts do PowerShell por estrutura de destino

Além das referências de assembly, os arquivos de conteúdo e os scripts do PowerShell também podem ser agrupados por estrutura de destino. A mesma estrutura de pastas encontrada na pasta `lib` para especificar a estrutura de destino agora pode ser aplicada da mesma maneira com as pastas `content` e `tools`. Por exemplo:

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

**Observação**: como `init.ps1` é executado no nível da solução e não é dependente de nenhum projeto individual, ele deve ser colocado diretamente na pasta `tools`. Se colocado em uma pasta específica da estrutura, ele será ignorado.

Além disso, um novo recurso no NuGet 2,0 é que uma pasta de estrutura pode estar *vazia*, nesse caso, o NuGet não adicionará referências de assembly, adicionará arquivos de conteúdo ou executará scripts do PowerShell para a versão específica do Framework. No exemplo acima, a pasta `content\net40` está vazia.

## <a name="improved-tab-completion-performance"></a>Desempenho de preenchimento com Tab aprimorado
O recurso de preenchimento de guia no console do Gerenciador de pacotes NuGet foi atualizado para melhorar significativamente o desempenho. Haverá muito menos atraso desde o momento em que a tecla Tab é pressionada até que a lista suspensa de sugestões seja exibida.

## <a name="bug-fixes"></a>Correções de Bug
O NuGet 2,0 inclui muitas correções de bugs com ênfase no consentimento e no desempenho da restauração de pacotes.
Para obter uma lista completa de itens de trabalho corrigidos no NuGet 2,0, consulte o [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
