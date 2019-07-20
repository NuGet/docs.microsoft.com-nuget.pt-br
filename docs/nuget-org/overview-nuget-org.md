---
title: Visão geral do NuGet.org
description: Visão geral do NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9a75ecbc589afa664e5684005e077b02913e8039
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427011"
---
# <a name="overview-of-nugetorg"></a>Visão geral do NuGet.org

O NuGet.org é um host público de pacotes NuGet que são utilizados por milhões de desenvolvedores do .NET e do .NET Core diariamente.

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a>Função do NuGet.org no ecossistema do NuGet

Em sua função como host público, o próprio NuGet.org mantém o repositório central de mais de 100.000 pacotes exclusivos em [nuget.org](https://www.nuget.org). O NuGet.org não é o único host possível para pacotes. A tecnologia do NuGet também permite hospedar pacotes em modo privado na nuvem (como o Azure DevOps), em uma rede privada ou, até mesmo, apenas no sistema de arquivos local. Caso esteja interessado em outro host ou outra opção de hospedagem, confira [Como hospedar seus próprios feeds do NuGet](../hosting-packages/overview.md).

O NuGet.org, como qualquer host para pacotes NuGet, serve como o ponto de conexão entre os *criadores* e os *consumidores* do pacote. Os criadores criam pacotes NuGet úteis e os publicam. Os consumidores pesquisam então por pacotes úteis e compatíveis em hosts acessíveis, baixando e incluindo esses pacotes em seus projetos. Depois de instalado em um projeto, as APIs dos pacotes estão disponíveis para o restante do código do projeto.

![Relação entre os criadores de pacote, hosts de pacote e consumidores de pacote](media/nuget-roles.png)

## <a name="accounts"></a>Contas

Para publicar pacotes no NuGet.org, primeiro crie uma [conta (de usuário) individual](individual-accounts.md). Isso se tornará sua identidade no NuGet.org.

O NuGet.org também permite que você crie uma [conta da organização](organizations-on-nuget-org.md). Uma conta da organização tem uma ou mais contas individuais como seus membros. Os membros podem gerenciar um conjunto de pacotes, mantendo uma única identidade para a propriedade. Por meio de sua conta individual, você pode ser membro de qualquer número de organizações.

Um pacote pode pertencer a uma conta da organização da mesma forma que pode pertencer a uma conta individual. Os consumidores do pacote não veem nenhuma diferença entre uma conta individual ou a conta da organização: ambas são exibidas como o pacote `owners`.

## <a name="api-keys"></a>Chaves de API

Depois que você tiver um pacote NuGet (arquivo *.nupkg*) para publicar, publique-o no NuGet.org usando a CLI do nuget.exe ou a CLI do dotnet.exe, juntamente com uma [chave de API](scoped-api-keys.md) adquirida no NuGet.org.

Quando você [publicar um pacote](../create-packages/creating-a-package.md), inclua o valor da chave de API no comando da CLI.

## <a name="id-prefixes"></a>Prefixos da ID

Ao publicar pacotes, você pode reservar e proteger sua identidade [reservando prefixos da ID](id-prefix-reservation.md). Ao instalar um pacote, os consumidores de pacotes recebem informações adicionais, indicando que o pacote que estão consumindo não é enganoso em suas propriedades de identificação.

## <a name="api-endpoint-for-nugetorg"></a>Ponto de extremidade de API para o NuGet.org

Para usar o NuGet.org como um repositório de pacotes com clientes do NuGet, você deverá usar o seguinte ponto de extremidade de API V3: 

`https://api.nuget.org/v3/index.json`

Os clientes mais antigos ainda podem usar o protocolo V2 para acessar o NuGet.org. No entanto, observe que os clientes do NuGet 3.0 ou posterior terão um serviço mais lento e menos confiável por meio do protocolo V2:

`https://www.nuget.org/api/v2` (**O protocolo V2 foi preterido.** )