---
title: Tools.JSON para descobrir as versões nuget.exe
description: O ponto de extremidade
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: 003139abac7808dbdaef4aa66119e09772db2b4f
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852527"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>Tools.JSON para descobrir as versões nuget.exe

Atualmente, há algumas maneiras de obter a versão mais recente do nuget.exe em seu computador de forma programável por script. Por exemplo, você pode baixar e extrair os [ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/) pacote em nuget.org. Isso tem alguma complexidade, pois ele exige que você já tenha nuget.exe (para `nuget.exe install`) ou você tem que descompactar o. nupkg usando uma ferramenta de descompactação básica e localizar os binário dentro.

Se você já tiver nuget.exe, você também pode usar `nuget.exe update -self`, no entanto, isso também requer que uma cópia existente do nuget.exe. Essa abordagem também atualiza a versão mais recente. Ele não permite o uso de uma versão específica.

O `tools.json` ponto de extremidade está disponível para ambos resolve o problema de inicialização e oferecer controle da versão do nuget.exe que você baixar. Isso pode ser usado em ambientes de CI/CD ou em scripts personalizados para descobrir e baixar qualquer versão de lançamento do nuget.exe.

O `tools.json` ponto de extremidade pode ser obtido usando uma solicitação HTTP não autenticada (por exemplo, `Invoke-WebRequest` no PowerShell ou `wget`). Pode ser analisada usando um desserializador JSON e download nuget.exe subsequentes que URLs também podem ser buscadas usando não autenticado a solicitações HTTP.

O ponto de extremidade pode ser buscado usando o `GET` método:

    GET https://dist.nuget.org/tools.json

O [esquema JSON](http://json-schema.org/) para o ponto de extremidade está disponível aqui:

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a>Resposta

A resposta é um documento JSON que contém todas as versões disponíveis do nuget.exe.

O objeto JSON de raiz tem a seguinte propriedade:

Nome      | Tipo             | Necessária
--------- | ---------------- | --------
nuget.exe | matriz de objetos | sim

Cada objeto no `nuget.exe` matriz tem as seguintes propriedades:

Nome     | Tipo   | Necessária | Observações
-------- | ------ | -------- | -----
version  | cadeia de caracteres | sim      | Uma cadeia de caracteres SemVer 2.0.0
url      | cadeia de caracteres | sim      | Uma URL absoluta para baixar essa versão do nuget.exe
estágio    | cadeia de caracteres | sim      | Uma cadeia de caracteres de enum
carregado | cadeia de caracteres | sim      | Um carimbo de hora ISO 8601 aproximado de quando a versão foi disponibilizada

Os itens na matriz serão classificados em ordem decrescente de, SemVer 2.0.0. Essa garantia destina-se para reduzir a carga de um cliente que está interessado no maior número de versão. No entanto, isso significa que a lista não é classificada em ordem cronológica. Por exemplo, se uma versão principal inferior é atendida em uma data posterior uma versão principal superior, essa versão de serviço não aparecerá na parte superior da lista. Se você quiser que a versão mais recente lançada pela *timestamp*, simplesmente classifique matriz pelo `uploaded` cadeia de caracteres. Isso funciona porque o `uploaded` carimbo de hora está no [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) formato que pode ser classificado em ordem cronológica, usando uma classificação lexicográfica (ou seja, uma classificação de cadeia de caracteres simples).

O `stage` propriedade indica que esta versão da ferramenta de lojas como está. 

Estágio              | Significado
------------------ | ------
EarlyAccessPreview | Ainda não estiver visível na [baixar a página da web](https://www.nuget.org/downloads) e devem ser validados por parceiros
Liberado           | Disponível no site de download, mas ainda não tiver sido recomendado para consumo ampla
ReleasedAndBlessed | Disponível no site de download e é recomendado para consumo

Uma abordagem simples para ter a versão mais recente, versão recomendada é tirar a primeira versão na lista que tem o `stage` valor de `ReleasedAndBlessed`. Isso funciona porque as versões são classificadas em ordem de SemVer 2.0.0.

O `NuGet.CommandLine` pacote em nuget.org normalmente é atualizada apenas com `ReleasedAndBlessed` versões.

### <a name="sample-request"></a>Exemplo de solicitação

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [tools-json.json](./_data/tools-json.json)]
