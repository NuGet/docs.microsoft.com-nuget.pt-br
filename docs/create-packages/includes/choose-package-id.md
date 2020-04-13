---
ms.openlocfilehash: c92f6e0c34347ee8555d416140d95ea2df5a3fbb
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610538"
---
O identificador de pacote e o número de versão são os dois valores mais importantes no projeto, pois identificam exclusivamente o código exato que está contido no pacote.

**Práticas recomendadas para o identificador de pacote:**

- **Exclusividade**: o identificador deve ser exclusivo no nuget.org ou na galeria que hospeda o pacote. Antes de decidir sobre um identificador, pesquise a galeria aplicável para verificar se o nome já está em uso. Para evitar conflitos, um bom padrão é usar o nome da sua empresa como a primeira parte do identificador, como `Contoso.`.
- **Nomes semelhantes a namespace**: siga um padrão semelhante aos namespaces no .NET, usando a notação de ponto em vez de hifens. Por exemplo, use `Contoso.Utility.UsefulStuff` em vez de `Contoso-Utility-UsefulStuff` ou `Contoso_Utility_UsefulStuff`. Também é útil para os consumidores quando o identificador de pacote corresponde os namespaces usados no código.
- **Pacotes de exemplo**: se você gerar um pacote de código de exemplo que demonstra como usar outro pacote, anexe `.Sample` como um sufixo ao identificador, como em `Contoso.Utility.UsefulStuff.Sample`. (O pacote de amostra teria, naturalmente, uma dependência do outro pacote.) Ao criar um pacote `contentFiles` de `<IncludeAssets>`exemplo, use o valor em . Na pasta `content`, organize o código de exemplo em uma pasta chamada `\Samples\<identifier>` como no `\Samples\Contoso.Utility.UsefulStuff.Sample`.

**Práticas recomendadas para a versão de pacote:**

- Em geral, defina a versão do pacote para corresponder ao projeto (ou assembly), embora isso não seja estritamente necessário. Isso é uma questão simples quando você limita um pacote a um único assembly. Em geral, lembre-se que o NuGet em si lida com versões do pacote ao resolver as dependências, não versões de assembly.
- Ao usar um esquema de versão não padrão, considere as regras de controle de versão do NuGet, conforme explicado em [Controle de versão do pacote](../../concepts/package-versioning.md). O NuGet é, na maioria das vezes, [compatível com semver 2](../../concepts/package-versioning.md#semantic-versioning-200).

> Para saber mais sobre a resolução de dependência, confira [Resolução de dependência com PackageReference](../../concepts/dependency-resolution.md#dependency-resolution-with-packagereference). Para obter informações mais antigas que também podem ser úteis para entender melhor o controle de versão, confira esta série de postagens no blog.
>
> - [Parte 1: assumindo o DLL Hell](https://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Parte 2: o algoritmo principal](https://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Parte 3: unificação por meio de redirecionamentos de associação](https://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)
