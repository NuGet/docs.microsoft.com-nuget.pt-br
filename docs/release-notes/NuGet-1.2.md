---
title: Notas de versão 1.2 do NuGet
description: Notas de versão do NuGet 1.2, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5d10d6bf27614980a144c30c3af6f9892a109061
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426185"
---
# <a name="nuget-12-release-notes"></a>Notas de versão 1.2 do NuGet

[Notas de versão do NuGet 1.0 e 1.1](../release-notes/nuget-1.1.md) | [notas de versão do NuGet 1.3](../release-notes/nuget-1.3.md)

NuGet 1.2 foi lançado em 30 de março de 2011.

## <a name="new-features"></a>Novos recursos

### <a name="framework-profile-support"></a>Suporte ao perfil de Framework

Desde o início, o NuGet tem suporte com bibliotecas diferentes estruturas de destino. Mas agora os pacotes podem conter assemblies direcionados perfis específicos, tais como o perfil do Windows Phone. Para um perfil específico de uma estrutura de destino, acrescente um traço seguido pela abreviação de perfil. Por exemplo, para direcionar o SilverLight em execução em um Windows Phone (também conhecido como o Windows Phone 7), você pode colocar um assembly na pasta sl3 wp conforme demonstrado na seguinte captura de tela.

![Layout de pasta de perfil do Framework](./media/framework-profile-support.png)

Você pode perguntar por que estamos apenas não optar por usar "wp7" como o moniker. Em parte, podemos está prevendo que o Windows Phone 7 pode executar uma versão mais recente do Silverlight no futuro, caso em que você talvez precise ser mais específico sobre qual estrutura de perfil você está direcionando.

### <a name="automatically-add-binding-redirects"></a>Adicionar automaticamente os redirecionamentos de associação

Ao instalar um pacote com conjuntos de alta segurança, o NuGet agora pode detectar os casos em que o projeto requer a ser adicionado ao arquivo de configuração para que o projeto compilar e adicioná-los automaticamente os redirecionamentos de associação. Parte 3 da série de postagens de blog de David Ebbo no controle de versão do NuGet intitulada "[Unificação por meio de redirecionamentos de associação](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)" aborda a finalidade desse recurso em mais detalhes.

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>Especificando referências de Assembly do Framework (GAC)

Em alguns casos, um pacote pode depender de um assembly que está no .NET Framework. Estritamente falando, ele nem sempre é necessário que o consumidor do seu pacote de referência de assembly do framework. Mas, em alguns casos, é importante, como quando o desenvolvedor precisa em relação aos tipos neste assembly de código para usar seu pacote. O novo `frameworkAssemblies` elemento, um elemento filho do elemento de metadados, permite que você especifique um conjunto de `frameworkAssembly` elementos apontando para um assembly do Framework no GAC. Observe a ênfase no assembly do Framework.
Esses assemblies não são incluídos em seu pacote conforme eles são considerados em todos os computadores como parte do .NET Framework. A tabela a seguir lista os atributos do `frameworkAssembly` elemento.


|Atributo |Descrição|
|----------------|-----------|
|**assemblyName**|*Necessário*. Nome do assembly, como `System.Net`.|
|**targetFramework**|*Opcional*. Permite especificar um nome de perfil e estrutura (ou alias) que esse assembly de estrutura se aplica a como "net40" ou "sl4". Usa o mesmo formato descrito na [que dão suporte a várias estruturas de destino](../create-packages/supporting-multiple-target-frameworks.md).|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>NuGet.exe agora é capaz de armazenar as credenciais de chave de API

Ao usar a ferramenta de linha de comando nuget.exe, agora você pode usar o comando SetApiKey para armazenar sua chave de API. Dessa forma, você não precisa especificá-lo toda vez que você enviar por push a um pacote. Para obter mais detalhes sobre como salvar sua chave de API com nuget.exe, [leia a documentação sobre publicação de um pacote](../nuget-org/publish-a-package.md).

### <a name="package-explorer"></a>Explorador de pacotes
Explorador de pacotes foi atualizado para dar suporte ao NuGet 1.2. Para obter mais informações, confira a [notas de versão do Explorador de pacotes](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).

## <a name="other-featuresfixes"></a>Outras correções de recursos /

A lista anterior foram dos muitos recursos que implementamos e bugs, corrigimos mais perceptível. Enfim, implementado/corrigimos [itens de trabalho de 59](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) nesta versão.

## <a name="known-issues"></a>Problemas Conhecidos

* **1.2 incompatibilidade de pacote**: Pacotes criados com a versão mais recente da ferramenta de linha de comando, nuget.exe (1.2 >) não funcionará com versões mais antigas do que o suplemento VS do NuGet (como 1.1). Se você tiver uma mensagem de erro dizendo algo sobre o esquema incompatível, você está executando para esse erro. Atualize o NuGet para a versão mais recente.
* **Incompatibilidade de NuGet. Server**: Se você estiver hospedando um feed usando o projeto NuGet. Server interno do NuGet, você precisará atualizar o projeto com a versão mais recente do NuGet. Server.
* **Erro de incompatibilidade de assinatura**: Se você tiver um erro durante uma atualização com uma mensagem sobre uma incompatibilidade de assinatura, você precisa desinstalar o NuGet primeiro e, em seguida, instalá-lo. Isso está listado em nossa [página de problemas conhecidos](../release-notes/known-issues.md) que fornece mais detalhes. O problema só afeta os que estão executando o Visual Studio 2010 SP1 e tiver uma versão do NuGet 1.0 instalado o que foi assinado incorretamente. Esta versão foi disponibilizada no site CodePlex por um breve período para que esse problema não deve afetar muitas pessoas.