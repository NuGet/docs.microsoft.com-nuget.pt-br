---
title: Como criar um pacote do NuGet localizado | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Detalhes sobre os dois modos de criar pacotes do NuGet localizados, incluindo todos os assemblies em um único pacote ou publicando assemblies separados."
keywords: "Localização de pacote do NuGet, assemblies satélite do NuGet, criação de pacotes localizados, convenções de localização do NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5946ba6b43d3c418a1624aeb27d12b385d66b2fb
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2018
---
# <a name="creating-localized-nuget-packages"></a>Criando pacotes do NuGet localizados

Há duas maneiras de criar versões localizadas de uma biblioteca:

1. Inclua todos os assemblies de recursos localizados em um único pacote.
1. Crie pacotes satélite em locais separados seguindo um conjunto restrito de convenções.

Ambos os métodos têm vantagens e desvantagens, conforme discutido nas seções a seguir.

## <a name="localized-resource-assemblies-in-a-single-package"></a>Assemblies de recursos localizados em um único pacote

Incluir assemblies de recurso localizado em um único pacote geralmente é a abordagem mais simples. Para fazer isso, crie pastas dentro de `lib` para os idiomas compatíveis além do padrão do pacote (presumido como en-us). Nessas pastas, você pode colocar assemblies de recursos e arquivos XML do IntelliSense localizados.

Por exemplo, a seguinte estrutura de pasta é compatível com alemão (de), italiano (it), japonês (ja), russo (ru), chinês (simplificado) (zh-Hans) e chinês (tradicional) (zh-Hant):

    lib
    └───net40
        │   Contoso.Utilities.dll
        │   Contoso.Utilities.xml
        │
        ├───de
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───it
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ja
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ru
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───zh-Hans
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        └───zh-Hant
                Contoso.Utilities.resources.dll
                Contoso.Utilities.xml

Você pode ver que os idiomas estão todos listados sob a pasta `net40` da estrutura de destino. Se você oferecer [compatibilidade a diversas estruturas](../create-packages/supporting-multiple-target-frameworks.md), terá uma pasta em `lib` para cada variedade.

Com essas pastas em vigor, você pode fazer referência a todos os arquivos em seu `.nuspec`:

```xml
<?xml version="1.0"?>
<package>
    <metadata>...
    </metadata>
    <files>
    <file src="lib\**" target="lib" />
    </files>
</package>
```

Um pacote de exemplo que usa essa abordagem é [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a>Vantagens e desvantagens (assemblies de recursos localizados)

Agrupar todos os idiomas em um único pacote traz algumas desvantagens:

1. **Metadados compartilhados**: como um pacote do NuGet só pode conter um único arquivo `.nuspec`, é possível fornecer metadados para um único idioma. Ou seja, o NuGet não apresenta suporte a metadados localizados.
1. **Tamanho do pacote**: dependendo do número de idiomas compatíveis, a biblioteca pode ficar consideravelmente grande, o que atrasa a instalação e restauração do pacote.
1. **Versões simultâneas**: agrupar arquivos localizados em um único pacote requer que você libere todos os ativos no pacote ao mesmo tempo, em vez de liberar cada localização separadamente. Além disso, qualquer atualização feita em uma localização requer uma nova versão do pacote inteiro.

No entanto, isso também traz alguns benefícios:

1. **Simplicidade**: os consumidores do pacote obtém todos os idiomas compatíveis em uma única instalação, em vez de ter que instalar cada idioma separadamente. Também é mais fácil de localizar um único pacote no nuget.org.
1. **Versões acopladas**: como todos os assemblies de recursos estão no mesmo pacote que o assembly principal, todos eles compartilham o mesmo número de versão e não correm o risco de serem desacopladas inadvertidamente.

## <a name="localized-satellite-packages"></a>Pacotes satélite localizados

Semelhante a como o .NET Framework dá suporte a assemblies satélite, esse método separa os recursos localizados e arquivos XML do IntelliSense em pacotes satélite.

Para fazer isso, o pacote principal usa a convenção de nomenclatura `{identifier}.{version}.nupkg` e contém o assembly para o idioma padrão (por exemplo, en-US). Por exemplo, `ContosoUtilities.1.0.0.nupkg` conteria a seguinte estrutura:

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

Dessa forma, um assembly satélite usa a convenção de nomenclatura `{identifier}.{language}.{version}.nupkg`, como `ContosoUtilities.de.1.0.0.nupkg`. O identificador **precisa** corresponder exatamente ao pacote principal.

Como esse é um pacote separado, ele tem seu próprio arquivo `.nuspec` que contém metadados localizado. Lembre-se que o idioma no `.nuspec` **precisa** corresponder àquele usado no nome do arquivo.

O assembly satélite também **precisa** declarar uma versão exata do pacote principal como uma dependência, usando a notação de versão [] \(consulte [Controle de versão do pacote](../reference/package-versioning.md)). Por exemplo, `ContosoUtilities.de.1.0.0.nupkg` precisa declarar uma dependência em `ContosoUtilities.1.0.0.nupkg` usando a notação `[1.0.0]`. O pacote satélite pode, obviamente, ter um número de versão diferente do pacote principal.

A estrutura do pacote satélite deverá incluir o assembly do recurso e o arquivo XML do IntelliSense em uma subpasta que corresponde a `{language}` no nome de arquivo do pacote:

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

**Observação**: a menos que subculturas específicos como `ja-JP` sejam necessárias, sempre use o identificador de idioma de nível superior, como `ja`.

Em um assembly satélite, o NuGet reconhecerá **somente** esses arquivos na pasta que corresponde ao `{language}` no nome de arquivo. Todos os outros são ignorados.

Quando todas essas convenções são atendidas, o NuGet reconhecerá o pacote como um pacote de satélite e instalará os arquivos localizados na pasta `lib` do pacote principal, como se tivesse sido fornecidos empacotados. Desinstalar o pacote satélite removerá seus arquivos da mesma pasta.

Assemblies satélite adicionais são criados da mesma forma para cada idioma compatível. Por exemplo, examine o conjunto de pacotes do ASP.NET MVC:

- [Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (principal em inglês)
- [Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (alemão)
- [Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (japonês)
- [Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (chinês (simplificado))
- [Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (chinês (tradicional))

### <a name="summary-of-required-conventions"></a>Resumo das convenções necessárias

- O pacote principal deve ser nomeado `{identifier}.{version}.nupkg`
- Um pacote satélite deve ser nomeado `{identifier}.{language}.{version}.nupkg`
- Um `.nuspec` do pacote satélite precisa especificar o idioma para corresponder ao nome do arquivo.
- Um pacote satélite precisa declarar uma dependência em uma versão exata do primário usando a notação [] no seu arquivo `.nuspec`. Não há suporte para intervalos.
- Um pacote satélite precisa colocar os arquivos na pasta `lib\[{framework}\]{language}` que corresponde exatamente ao `{language}` no nome de arquivo.

### <a name="advantages-and-disadvantages-satellite-packages"></a>Vantagens e desvantagens (pacotes satélites)

Usar pacotes satélite traz alguns benefícios:

1. **Tamanho do pacote**: a superfície geral do pacote principal é minimizada e os consumidores incorrem somente nos custos de cada idioma que desejam usar.
1. **Metadados separados**: cada pacote satélite tem seu próprio arquivo `.nuspec` e, portanto, seus próprios metadados localizado porque. Isso pode permitir que alguns consumidores localizem os pacotes mais facilmente pesquisando nuget.org com termos localizados.
1. **Versões desacopladas**: assemblies satélite podem ser liberados ao longo do tempo, em vez de uma só vez, permitindo que você distribua seus esforços de localização.

No entanto, pacotes satélite trazem seu próprio conjunto de desvantagens:

1. **Desordem**: em vez de um único pacote, você tem muitos pacotes que podem levar a resultados da pesquisa desorganizados no nuget.org e uma longa lista de referências em um projeto do Visual Studio.
1. **Convenções estritas**. Pacotes satélite devem seguir as convenções com exatidão ou as versões localizadas não serão selecionadas corretamente.
1. **Controle de versão**: cada pacote satélite precisa ter uma dependência de versão exata do pacote principal. Isso significa que a atualização do pacote principal pode requerer a atualização de todos os pacotes satélite, mesmo se os recursos não foram alterados.
