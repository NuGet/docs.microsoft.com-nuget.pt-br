---
title: "Notas de versão do NuGet 1.2 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 48f23141-b2ad-4cdf-8d81-7bb6b9419aa6
description: "Notas de versão do NuGet 1.2, incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão NuGet 1.2, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d69a65352d42025b61df9068473ddedffc5f1663
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-12-release-notes"></a>Notas de versão 1.2 do NuGet

[Notas de versão 1.0 e 1.1 NuGet](../release-notes/nuget-1.1.md) | [notas de versão 1.3 do NuGet](../release-notes/nuget-1.3.md)

NuGet 1.2 foi lançado em 30 de março de 2011.

## <a name="new-features"></a>Novos recursos

### <a name="framework-profile-support"></a>Suporte ao perfil de estrutura

Desde o início, o NuGet tem suporte com bibliotecas diferentes estruturas de destino. Mas agora os pacotes podem conter assemblies que se destinam a perfis específicos, como o perfil do Windows Phone. Para um perfil específico de uma estrutura de destino, acrescente um traço seguido a abreviação do perfil. Por exemplo, para direcionar o SilverLight em execução em um Windows Phone (também conhecido como o Windows Phone 7), você pode colocar um assembly na pasta sl3 wp conforme mostrado na seguinte captura de tela.

![Layout de pasta de perfil de estrutura](./media/framework-profile-support.png)

Você pode perguntar por que estamos apenas não optar por usar "wp7" como o moniker. Em parte, podemos está prevendo que o Windows Phone 7 pode executar uma versão mais recente do Silverlight no futuro, caso em que você talvez precisem ser mais específico sobre estrutura de perfil estiver direcionando.

### <a name="automatically-add-binding-redirects"></a>Adicionar automaticamente os redirecionamentos de associação

Ao instalar um pacote com conjuntos de alta segurança, o NuGet agora pode detectar os casos em que o projeto requer a ligação redireciona para ser adicionado ao arquivo de configuração para que o projeto compilar e adicioná-los automaticamente. Parte 3 de série de postagens de blog de David Ebbo no controle de versão do NuGet intitulada "[Unificação por meio de associação redireciona](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)" aborda a finalidade desse recurso em mais detalhes.

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>Especificação de Framework referências de Assembly (GAC)

Em alguns casos, um pacote pode depender de um assembly do .NET Framework. Estritamente falando, nem sempre é necessário que o consumidor do seu pacote de referenciar o assembly do framework. Mas, em alguns casos, é importante, como quando o desenvolvedor precisa contra tipos neste assembly de código para usar o pacote. O novo `frameworkAssemblies` elemento, um elemento filho do elemento de metadados, permite que você especifique um conjunto de `frameworkAssembly` elementos apontando para um assembly do Framework no GAC. Observe a ênfase em assembly do Framework.
Esses assemblies não são incluídos em seu pacote, como eles são considerados em todos os computadores como parte do .NET Framework. A tabela a seguir lista os atributos do `frameworkAssembly` elemento.


|Atributo |Descrição|
|----------------|-----------|
|**assemblyName**|*Necessário*. Nome do assembly como `System.Net`.|
|**targetFramework**|*Opcional*. Permite especificar um nome de perfil e do framework (ou alias) que este assembly do framework aplica-se a como "net40" ou "sl4". Usa o mesmo formato descrito na [dando suporte a várias estruturas de destino](../create-packages/supporting-multiple-target-frameworks.md).|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>NuGet.exe agora é capaz de armazenar as credenciais de chave de API

Ao usar a ferramenta de linha de comando nuget.exe, agora você pode usar o comando SetApiKey para armazenar sua chave de API. Dessa forma, você não precisa especificá-lo toda vez que você enviar um pacote. Para obter mais detalhes sobre como salvar sua chave de API com nuget.exe, [leia a documentação sobre publicação de um pacote](../create-packages/publish-a-package.md).

### <a name="package-explorer"></a>Explorador de pacotes
Explorador de pacotes foi atualizado para dar suporte NuGet 1.2. Para obter mais informações, confira o [notas de versão do Explorador de pacotes](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).

## <a name="other-featuresfixes"></a>Outros recursos/correções

A lista anterior foi dos muitos recursos implementamos e bugs corrigimos mais perceptível. Implementado/corrigimos [itens de trabalho 59](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) nesta versão.

## <a name="known-issues"></a>Problemas conhecidos

* **1.2 incompatibilidade do pacote**: pacotes criados com a versão mais recente da ferramenta de linha de comando, nuget.exe (> 1.2) não funcionará com versões anteriores do NuGet VS suplemento (como 1.1). Se você tiver uma mensagem de erro informando que algo sobre esquema incompatível, você está executando para esse erro. Atualize o NuGet para a versão mais recente.
* **Incompatibilidade de NuGet.Server**: se você estiver hospedando um feed usando o projeto NuGet.Server o NuGet interno, você precisará atualizar o projeto com a versão mais recente do NuGet.Server.
* **Erro de incompatibilidade de assinatura**: se você encontrar um erro durante uma atualização com uma mensagem sobre uma incompatibilidade de assinatura, você precisará desinstalar NuGet primeiro e, em seguida, instalá-lo. Ele está listado na nossa [página problemas conhecidos](../release-notes/Known-Issues.md) que fornece mais detalhes. O problema só afeta os que estão executando o Visual Studio 2010 SP1 e tiver uma versão 1.0 do NuGet instalada que foi assinado incorretamente. Esta versão foi disponibilizada somente do site do CodePlex por um breve período para que esse problema não deve afetar muitas pessoas.