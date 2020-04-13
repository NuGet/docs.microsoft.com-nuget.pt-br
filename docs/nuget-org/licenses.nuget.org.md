---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 717cf8c47335c620410be71300b07de82799e1d3
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427111"
---
# <a name="licensesnugetorg"></a>licenses.nuget.org

## <a name="rationale"></a>Fundamento

Com a introdução das [expressões de licença](../reference/nuspec.md#license), surgiu um requisito de ter um serviço confiável que fornecerá um texto de referência para identificadores de licença individuais, identificadores de exceção ou expressões de licença.
Um requisito adicional desse serviço é ter um esquema de URL estável, que não seja suscetível a links desfeitos, de modo que possamos usá-lo com segurança para fornecer compatibilidade com versões anteriores a clientes mais antigos.

Licenses.nuget.org cumpre essa função. O nuget.org usa-o para fornecer a referência de texto de licença para pacotes que especificam sua licença usando uma expressão de licença. `nuget pack` ou o empacotamento com outras [ferramentas de cliente](../install-nuget-client-tools.md) define o elemento [`licenseUrl`](../reference/nuspec.md#licenseurl) para que ele aponte para licenses.nuget.org visando fornecer compatibilidade com clientes mais antigos que não dão suporte ao elemento `license`.

## <a name="protocol"></a>Protocolo

Licenses.nuget.org destina-se a ser exibido por pessoas em seus navegadores; nenhuma resposta legível por computador é fornecida.
O protocolo HTTPS precisa ser usado, e as solicitações devem ser construídas de uma maneira específica. Ele só dá suporte a solicitações `GET`.
Aceita expressões de licença ou identificadores de exceção de licença como entrada de uma forma especificada abaixo. Observe que todos os elementos de expressões de licença diferenciam maiúsculas de minúsculas e, portanto, toda entrada para licenses.nuget.org também diferencia maiúsculas de minúsculas.

### <a name="license-expressions"></a>Expressões de licença

#### <a name="request"></a>Solicitação

As expressões de licença (incluindo os casos triviais em que a expressão consiste em uma única licença) devem ser [codificadas em URL](https://tools.ietf.org/html/rfc3986#section-2.1) e usadas como um caminho na solicitação para licenses.nuget.org.

| Expressão de licença | URL a ser usada |
|:---|:---|
| MIT                                                | <https://licenses.nuget.org/MIT> |
| (MIT)                                              | <https://licenses.nuget.org/(MIT)> |
| (LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+) | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

O serviço suporta apenas identificadores de licença e identificadores de exceção de licença que são aceitos por nuget.org. Todas as expressões de licença que contenham identificadores de licença não suportados ou identificadores de exceção de licença ou que não estejam em conformidade com a sintaxe de expressão da licença são consideradas inválidas.

#### <a name="response"></a>Resposta

Licenses.nuget.org responde às solicitações que contêm expressões de licença válidas com um código de status HTTP 200 e uma página da Web que contém uma descrição da expressão de licença:

* se a expressão de licença fornecida contiver um único identificador de licença, será retornada uma página da Web que contém o texto de referência dessa licença;
* se a expressão de licença fornecida for uma expressão de licença composta, será retornada uma página da Web que contém a expressão de licença com links para referências de exceção de licença ou licença individual.

Qualquer solicitação que contenha uma expressão de licença inválida resulta em uma resposta HTTP 404.

### <a name="license-exceptions"></a>Exceções de licença

#### <a name="request"></a>Solicitação

Os identificadores de exceção de licença devem ser codificados por URL e usados como um caminho na solicitação para licenses.nuget.org. Apenas um único identificador de exceção de licença pode ser fornecido em uma única solicitação. Nenhum caractere adicional além do identificador de exceção de licença pode estar presente na parte do caminho da URL.

| Identificador de exceção de licença | URL a ser usada |
|:---|:---|
|FLTK-exception            | <https://licenses.nuget.org/FLTK-exception> |
|openvpn-openssl-exception | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a>Resposta

Licenses.nuget.org responde a uma solicitação com um identificador de exceção de licença conhecido contendo uma resposta HTTP 200 e uma página da Web que contém o texto de referência para a exceção de licença especificada.

Qualquer solicitação que contenha um identificador de exceção de licença sem suporte resulta em uma resposta HTTP 404.