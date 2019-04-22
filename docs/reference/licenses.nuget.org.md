---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 4a40cc1f7d333e8d35a721f3eed2e6b9365faf7b
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2019
ms.locfileid: "58921553"
---
# <a name="licensesnugetorg"></a>licenses.nuget.org

## <a name="rationale"></a>Racional

Com a introdução do [expressões de licença](nuspec.md#license), um requisito surgiu para ter um serviço confiável que deveria fornecer um texto de referência para os identificadores de licença individual, os identificadores de exceção ou expressões de licença.
Um requisito adicional para esse serviço é ter um esquema de URL estável, que não é suscetível a vincular corrompidos, para que podemos pode usá-lo com segurança para fornecer compatibilidade com versões anteriores de clientes mais antigos.

Licenses.NuGet.org atende a essa função. NuGet.org usa para fornecer a referência de texto de licença para pacotes que especificam a licença usando uma expressão de licença. `nuget pack` ou embalagem com os outros [ferramentas de cliente](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) defina o [ `licenseUrl` ](nuspec.md#licenseurl) elemento para apontar para licenses.nuget.org para proporcionar compatibilidade com clientes mais antigos que não dão suporte a `license` elemento.

## <a name="protocol"></a>Protocolo

Nenhuma resposta legível por máquina licenses.NuGet.org se destina a ser exibido pelas pessoas em seus navegadores, é fornecida.
Protocolo HTTPS deve ser usado e as solicitações devem ser construídos em uma determinada maneira. Ele dá suporte apenas a `GET` solicitações.
Ele aceita expressões de licença ou identificadores de exceção de licença como uma entrada de uma forma especificada abaixo. Observe que todos os elementos de expressões de licença diferenciam maiusculas de minúsculas e, portanto, todas as entradas para licenses.nuget.org diferencia maiusculas de minúsculas, bem.

### <a name="license-expressions"></a>Expressões de licença

#### <a name="request"></a>Solicitação

Expressões de licença (incluindo os casos triviais quando a expressão consiste em uma única licença) precisam ser [codificado por URL](https://tools.ietf.org/html/rfc3986#section-2.1) e usado como um caminho na solicitação para licenses.nuget.org.

| Expressão de licença | URL a ser usada |
|:---|:---|
| MIT                                                | <https://licenses.nuget.org/MIT> |
| (MIT)                                              | <https://licenses.nuget.org/(MIT)> |
| (LGPL 2.0-somente com o Apache FLTK exceção OR-2.0 +) | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

O serviço oferece suporte somente a identificadores de licença e identificadores de exceção de licença são aceitos pelo nuget.org. Todas as expressões de licença que contêm os identificadores de licença sem suporte ou identificadores de exceção de licença ou que não estão em conformidade com a sintaxe de expressão de licença são consideradas inválidas.

#### <a name="response"></a>Resposta

Licenses.NuGet.org responde às solicitações que contêm expressões de licença válida com um código de status HTTP 200 e uma página da web que contém uma descrição da expressão de licença:

* Se for fornecido a expressão de licença contém um identificador de licença única que uma página da web é retornado que contém o texto de referência dessa licença;
* Se for fornecido expressão de licença é uma expressão de licença de composição, uma página da web é retornado que contém a expressão de licença com links para referências de exceção de licença ou licença individual.

Qualquer solicitação que contenha uma expressão de licença inválida resulta em uma resposta HTTP 404.

### <a name="license-exceptions"></a>Exceções de licença

#### <a name="request"></a>Solicitação

Identificadores de exceção de licença devem ser codificados de URL e é usada como um caminho na solicitação para licenses.nuget.org. Somente um identificador de exceção única licença pode ser fornecido em uma única solicitação. Não há caracteres adicionais além do identificador de exceção de licença podem estar presentes na parte do caminho da URL.

| Identificador de exceção de licença | URL a ser usada |
|:---|:---|
|FLTK-exception            | <https://licenses.nuget.org/FLTK-exception> |
|openvpn-openssl-exception | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a>Resposta

Licenses.NuGet.org responde a uma solicitação com um identificador de exceção de licenças conhecidos com uma resposta HTTP 200 e uma página da web que contém o texto de referência para a exceção de licença especificado.

Qualquer solicitação que contém um identificador de exceção sem suporte de licença resulta em uma resposta HTTP 404.