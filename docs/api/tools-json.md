---
title: Tools. JSON para descobrir as versões do NuGet. exe
description: O ponto de extremidade para
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: a186db9727bdfd1b55bf73a1f29283352555dede
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611025"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>Tools. JSON para descobrir as versões do NuGet. exe

Hoje, há algumas maneiras de obter a versão mais recente do NuGet. exe em seu computador de maneira programável. Por exemplo, você pode baixar e extrair o pacote de [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) do NuGet.org. Isso tem alguma complexidade, pois ela requer que você já tenha NuGet. exe (para `nuget.exe install`) ou precise descompactar o. nupkg usando uma ferramenta de descompactação básica e localizar o binário interno.

Se você já tiver o NuGet. exe, também poderá usar `nuget.exe update -self`, mas isso também requer uma cópia existente do NuGet. exe. Essa abordagem também o atualiza para a versão mais recente. Ele não permite o uso de uma versão específica.

O ponto de extremidade `tools.json` está disponível para resolver o problema de inicialização e para dar o controle da versão do NuGet. exe que você baixa. Isso pode ser usado em ambientes de CI/CD ou em scripts personalizados para descobrir e baixar qualquer versão de lançamento do NuGet. exe.

O ponto de extremidade `tools.json` pode ser obtido usando uma solicitação HTTP não autenticada (por exemplo, `Invoke-WebRequest` no PowerShell ou `wget`). Ele pode ser analisado usando um desserializador JSON e as URLs de download do NuGet. exe subsequentes também podem ser buscadas usando solicitações HTTP não autenticadas.

O ponto de extremidade pode ser buscado usando o método `GET`:

    GET https://dist.nuget.org/tools.json

O [esquema JSON](https://json-schema.org/) para o ponto de extremidade está disponível aqui:

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a>Resposta

A resposta é um documento JSON que contém todas as versões disponíveis do NuGet. exe.

O objeto JSON raiz tem a seguinte propriedade:

Name      | Digite             | Necessária
--------- | ---------------- | --------
nuget.exe | matriz de objetos | sim

Cada objeto na matriz de `nuget.exe` tem as seguintes propriedades:

Name     | Digite   | Necessária | Anotações
-------- | ------ | -------- | -----
version  | cadeia de caracteres | sim      | Uma cadeia de caracteres SemVer 2.0.0
url      | cadeia de caracteres | sim      | Uma URL absoluta para baixar esta versão do NuGet. exe
Test    | cadeia de caracteres | sim      | Uma cadeia de caracteres de enumeração
atualizada | cadeia de caracteres | sim      | Um carimbo de data/hora ISO 8601 aproximado de quando a versão foi disponibilizada

Os itens na matriz serão classificados em ordem decrescente, SemVer 2.0.0 Order. Essa garantia destina-se a reduzir a carga de um cliente que está interessado no número de versão mais alto. No entanto, isso significa que a lista não está classificada em ordem cronológica. Por exemplo, se uma versão principal inferior for atendida em uma data posterior à versão principal mais alta, essa versão de serviço não aparecerá na parte superior da lista. Se você quiser que a versão mais recente seja liberada pelo *carimbo de data/hora*, basta classificar a matriz pela cadeia de caracteres de `uploaded`. Isso funciona porque o carimbo de data/hora `uploaded` está no formato [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) , que pode ser classificado cronologicamente usando uma classificação lexicográfica (ou seja, uma classificação de cadeia de caracteres simples).

A propriedade `stage` indica como verificados esta versão da ferramenta. 

Estágio              | Significado
------------------ | ------
EarlyAccessPreview | Ainda não está visível na [página de download da Web](https://www.nuget.org/downloads) e deve ser validada pelos parceiros
Liberado           | Disponível no site de download, mas ainda não é recomendado para consumo de larga propagação
ReleasedAndBlessed | Disponível no site de download e é recomendado para consumo

Uma abordagem simples para ter a versão mais recente e recomendada é usar a primeira versão na lista com o `stage` valor de `ReleasedAndBlessed`. Isso funciona porque as versões são classificadas em SemVer 2.0.0 Order.

O pacote de `NuGet.CommandLine` no nuget.org normalmente é atualizado apenas com `ReleasedAndBlessed` versões.

### <a name="sample-request"></a>Exemplo de solicitação

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a>Exemplo de resposta

[!code-JSON [tools-json.json](./_data/tools-json.json)]
