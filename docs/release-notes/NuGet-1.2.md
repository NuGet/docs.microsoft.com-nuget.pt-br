---
title: Notas de versão do NuGet 1,2
description: Notas de versão do NuGet 1,2 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5d10d6bf27614980a144c30c3af6f9892a109061
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79429083"
---
# <a name="nuget-12-release-notes"></a>Notas de versão do NuGet 1,2

[Notas de versão do nuget 1,0 e 1,1](../release-notes/nuget-1.1.md) | [notas de versão do NuGet 1,3](../release-notes/nuget-1.3.md)

O NuGet 1,2 foi lançado em 30 de março de 2011.

## <a name="new-features"></a>Novos recursos

### <a name="framework-profile-support"></a>Suporte a perfil de estrutura

Desde o início, o NuGet tem suporte para as bibliotecas que têm como destino diferentes estruturas. Mas agora os pacotes podem conter assemblies destinados a perfis específicos, como o perfil de Windows Phone. Para direcionar um perfil específico de uma estrutura, acrescente um traço seguido pela abreviação do perfil. Por exemplo, para direcionar o SilverLight em execução em um Windows Phone (também conhecido como Windows Phone 7), você pode colocar um assembly na pasta SL3-WP conforme demonstrado na captura de tela a seguir.

![Layout da pasta de perfil do Framework](./media/framework-profile-support.png)

Você pode perguntar por que não simplesmente optamos por usar "WP7" como o moniker. Em parte, estamos antecipando que Windows Phone 7 pode executar uma versão mais recente do Silverlight no futuro; nesse caso, talvez seja necessário ser mais específico sobre o perfil de estrutura que você está voltadosndo.

### <a name="automatically-add-binding-redirects"></a>Adicionar redirecionamentos de associação automaticamente

Ao instalar um pacote com assemblies nomeados fortes, o NuGet agora pode detectar casos em que o projeto requer que os redirecionamentos de associação sejam adicionados ao arquivo de configuração para que o projeto seja compilado e adicionado automaticamente. A parte 3 da série de postagens de blog de David Ebbo sobre o controle de versão do NuGet intitulado "a[unificação por meio de redirecionamentos de associação](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)" aborda a finalidade desse recurso em mais detalhes.

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>Especificando referências de assembly de estrutura (GAC)

Em alguns casos, um pacote pode depender de um assembly que está no .NET Framework. Estritamente falando, nem sempre é necessário que o consumidor do seu pacote faça referência ao assembly da estrutura. Mas, em alguns casos, é importante, por exemplo, quando o desenvolvedor precisa codificar em relação a tipos nesse assembly para usar o pacote. O novo elemento `frameworkAssemblies`, um elemento filho do elemento Metadata, permite que você especifique um conjunto de elementos `frameworkAssembly` apontando para um assembly de estrutura no GAC. Observe a ênfase no assembly de estrutura.
Esses assemblies não são incluídos no seu pacote, pois eles são considerados em cada computador como parte do .NET Framework. A tabela a seguir lista os atributos do elemento `frameworkAssembly`.


|Atributo |DESCRIÇÃO|
|----------------|-----------|
|**assemblyName**|*Obrigatório*. Nome do assembly, como `System.Net`.|
|**targetFramework**|*Opcional*. Permite especificar um nome de estrutura e perfil (ou alias) que esse assembly de estrutura aplica a como "net40" ou "SL4". Usa o mesmo formato descrito em [suporte a várias estruturas de destino](../create-packages/supporting-multiple-target-frameworks.md).|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>o NuGet. exe agora é capaz de armazenar credenciais de chave de API

Ao usar a ferramenta de linha de comando NuGet. exe, agora você pode usar o comando SetApiKey para armazenar sua chave de API. Dessa forma, você não precisará especificá-la toda vez que enviar um pacote por push. Para obter mais detalhes sobre como salvar sua chave de API com NuGet. exe, [Leia a documentação sobre como publicar um pacote](../nuget-org/publish-a-package.md).

### <a name="package-explorer"></a>Explorador de pacotes
O explorador de pacotes foi atualizado para dar suporte ao NuGet 1,2. Para obter mais informações, Confira as [notas de versão do explorador de pacotes](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).

## <a name="other-featuresfixes"></a>Outros recursos/correções

A lista anterior era o mais perceptível dos muitos recursos que implementamos e os bugs que corrigimos. Em todos, implementamos/corrigimos [59 itens de trabalho](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) nesta versão.

## <a name="known-issues"></a>Problemas conhecidos

* **incompatibilidade de pacote 1,2**: os pacotes criados com a versão mais recente da ferramenta de linha de comando, NuGet. exe (> 1,2) não funcionarão com versões mais antigas do suplemento do NuGet vs (como 1,1). Se você encontrar uma mensagem de erro informando algo sobre o esquema incompatível, você está executando esse erro. Atualize o NuGet para a versão mais recente.
* **Incompatibilidade do NuGet. Server**: se você estiver hospedando um feed do NuGet interno usando o projeto NuGet. Server, você precisará atualizar esse projeto com a versão mais recente do NuGet. Server.
* **Erro de incompatibilidade de assinatura**: se você encontrar um erro durante uma atualização com uma mensagem sobre uma incompatibilidade de assinatura, será necessário desinstalar primeiro o NuGet e, em seguida, instalá-lo. Isso é listado em nossa [página de problemas conhecidos](../release-notes/known-issues.md) que fornece mais detalhes. O problema afeta apenas aqueles que executam o Visual Studio 2010 SP1 e tem uma versão do NuGet 1,0 instalada que foi assinada incorretamente. Essa versão só foi disponibilizada no site do CodePlex por um breve período, portanto, esse problema não deve afetar muitas pessoas.