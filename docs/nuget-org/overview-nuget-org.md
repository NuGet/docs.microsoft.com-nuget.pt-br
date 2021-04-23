---
title: Visão geral do NuGet.org
description: Visão geral do NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 2dac6ebd6367f3ed1a5ef9e81d843867a4a22f62
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901870"
---
# <a name="overview-of-nugetorg"></a><span data-ttu-id="24b0a-103">Visão geral do NuGet.org</span><span class="sxs-lookup"><span data-stu-id="24b0a-103">Overview of NuGet.org</span></span>

<span data-ttu-id="24b0a-104">O NuGet.org é um host público de pacotes NuGet que são utilizados por milhões de desenvolvedores do .NET e do .NET Core diariamente.</span><span class="sxs-lookup"><span data-stu-id="24b0a-104">NuGet.org is a public host of NuGet packages that are employed by millions of .NET and .NET Core developers every day.</span></span>

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a><span data-ttu-id="24b0a-105">Função do NuGet.org no ecossistema do NuGet</span><span class="sxs-lookup"><span data-stu-id="24b0a-105">Role of NuGet.org in the NuGet ecosystem</span></span>

<span data-ttu-id="24b0a-106">Em sua função como um host público, o próprio NuGet.org mantém o repositório central de mais de 100.000 pacotes exclusivos em [NuGet.org](https://www.nuget.org). NuGet.org não é o único host possível para pacotes.</span><span class="sxs-lookup"><span data-stu-id="24b0a-106">In its role as a public host, NuGet.org itself maintains the central repository of over 100,000 unique packages at [nuget.org](https://www.nuget.org). NuGet.org is not the only possible host for packages.</span></span> <span data-ttu-id="24b0a-107">A tecnologia do NuGet também permite hospedar pacotes em modo privado na nuvem (como o Azure DevOps), em uma rede privada ou, até mesmo, apenas no sistema de arquivos local.</span><span class="sxs-lookup"><span data-stu-id="24b0a-107">The NuGet technology also enables you to host packages privately in the cloud (such as on Azure DevOps), on a private network, or even on just your local file system.</span></span> <span data-ttu-id="24b0a-108">Caso esteja interessado em outro host ou outra opção de hospedagem, confira [Como hospedar seus próprios feeds do NuGet](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="24b0a-108">If you are interested in a different host or hosting option, see [Hosting your own NuGet feeds](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="24b0a-109">O NuGet.org, como qualquer host para pacotes NuGet, serve como o ponto de conexão entre os *criadores* e os *consumidores* do pacote.</span><span class="sxs-lookup"><span data-stu-id="24b0a-109">NuGet.org, like any host for NuGet packages, serves as the point of connection between package *creators* and package *consumers*.</span></span> <span data-ttu-id="24b0a-110">Os criadores criam pacotes NuGet úteis e os publicam.</span><span class="sxs-lookup"><span data-stu-id="24b0a-110">Creators build useful NuGet packages and publish them.</span></span> <span data-ttu-id="24b0a-111">Os consumidores pesquisam então por pacotes úteis e compatíveis em hosts acessíveis, baixando e incluindo esses pacotes em seus projetos.</span><span class="sxs-lookup"><span data-stu-id="24b0a-111">Consumers then search for useful and compatible packages on accessible hosts, downloading and including those packages in their projects.</span></span> <span data-ttu-id="24b0a-112">Depois de instalado em um projeto, as APIs dos pacotes estão disponíveis para o restante do código do projeto.</span><span class="sxs-lookup"><span data-stu-id="24b0a-112">Once installed in a project, the packages' APIs are available to the rest of the project code.</span></span>

![Relação entre os criadores de pacote, hosts de pacote e consumidores de pacote](media/nuget-roles.png)

## <a name="accounts"></a><span data-ttu-id="24b0a-114">Contas</span><span class="sxs-lookup"><span data-stu-id="24b0a-114">Accounts</span></span>

<span data-ttu-id="24b0a-115">Para publicar pacotes no NuGet.org, primeiro crie uma [conta (de usuário) individual](individual-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="24b0a-115">To publish packages on NuGet.org, you first create an [individual (user) account](individual-accounts.md).</span></span> <span data-ttu-id="24b0a-116">Isso se tornará sua identidade no NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="24b0a-116">This becomes your identity on NuGet.org.</span></span>

<span data-ttu-id="24b0a-117">O NuGet.org também permite que você crie uma [conta da organização](organizations-on-nuget-org.md).</span><span class="sxs-lookup"><span data-stu-id="24b0a-117">NuGet.org also allows you to create an [organization account](organizations-on-nuget-org.md).</span></span> <span data-ttu-id="24b0a-118">Uma conta da organização tem uma ou mais contas individuais como seus membros.</span><span class="sxs-lookup"><span data-stu-id="24b0a-118">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="24b0a-119">Os membros podem gerenciar um conjunto de pacotes, mantendo uma única identidade para a propriedade.</span><span class="sxs-lookup"><span data-stu-id="24b0a-119">Members can manage a set of packages while maintaining a single identity for ownership.</span></span> <span data-ttu-id="24b0a-120">Por meio de sua conta individual, você pode ser membro de qualquer número de organizações.</span><span class="sxs-lookup"><span data-stu-id="24b0a-120">Through your individual account, you can be a member of any number of organizations.</span></span>

<span data-ttu-id="24b0a-121">Um pacote pode pertencer a uma conta da organização da mesma forma que pode pertencer a uma conta individual.</span><span class="sxs-lookup"><span data-stu-id="24b0a-121">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="24b0a-122">Os consumidores do pacote não veem nenhuma diferença entre uma conta individual ou a conta da organização: ambas são exibidas como o pacote `owners`.</span><span class="sxs-lookup"><span data-stu-id="24b0a-122">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="api-keys"></a><span data-ttu-id="24b0a-123">Chaves de API</span><span class="sxs-lookup"><span data-stu-id="24b0a-123">API keys</span></span>

<span data-ttu-id="24b0a-124">Depois que você tiver um pacote NuGet (arquivo *.nupkg*) para publicar, publique-o no NuGet.org usando a CLI do nuget.exe ou a CLI do dotnet.exe, juntamente com uma [chave de API](scoped-api-keys.md) adquirida no NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="24b0a-124">Once you have a NuGet package (*.nupkg* file) to publish, you publish it to NuGet.org using either the nuget.exe CLI or the dotnet.exe CLI, along with an [API key](scoped-api-keys.md) acquired from NuGet.org.</span></span>

<span data-ttu-id="24b0a-125">Quando você [publicar um pacote](../create-packages/creating-a-package.md), inclua o valor da chave de API no comando da CLI.</span><span class="sxs-lookup"><span data-stu-id="24b0a-125">When you [publish a package](../create-packages/creating-a-package.md), you include the API key value in the CLI command.</span></span>

## <a name="id-prefixes"></a><span data-ttu-id="24b0a-126">Prefixos da ID</span><span class="sxs-lookup"><span data-stu-id="24b0a-126">ID prefixes</span></span>

<span data-ttu-id="24b0a-127">Ao publicar pacotes, você pode reservar e proteger sua identidade [reservando prefixos da ID](id-prefix-reservation.md).</span><span class="sxs-lookup"><span data-stu-id="24b0a-127">When you publish packages, you can reserve and protect your identity by [reserving ID prefixes](id-prefix-reservation.md).</span></span> <span data-ttu-id="24b0a-128">Ao instalar um pacote, os consumidores de pacotes recebem informações adicionais, indicando que o pacote que estão consumindo não é enganoso em suas propriedades de identificação.</span><span class="sxs-lookup"><span data-stu-id="24b0a-128">When installing a package, package consumers are provided with additional information indicating that the package they are consuming is not deceptive in its identifying properties.</span></span>

## <a name="api-endpoint-for-nugetorg"></a><span data-ttu-id="24b0a-129">Ponto de extremidade de API para o NuGet.org</span><span class="sxs-lookup"><span data-stu-id="24b0a-129">API endpoint for NuGet.org</span></span>

<span data-ttu-id="24b0a-130">Para usar o NuGet.org como um repositório de pacotes com clientes do NuGet, você deverá usar o seguinte ponto de extremidade de API V3:</span><span class="sxs-lookup"><span data-stu-id="24b0a-130">To use NuGet.org as a package repository with NuGet clients, you should use the following V3 API endpoint:</span></span> 

`https://api.nuget.org/v3/index.json`

<span data-ttu-id="24b0a-131">Clientes mais antigos ainda podem usar o protocolo v2 para alcançar o NuGet.org. No entanto, observe que os clientes NuGet 3,0 ou posteriores terão um serviço mais lento e menos confiável usando o protocolo v2:</span><span class="sxs-lookup"><span data-stu-id="24b0a-131">Older clients can still use the V2 protocol to reach NuGet.org. However, please note, NuGet clients 3.0 or later will have slower and less reliable service using the V2 protocol:</span></span>

<span data-ttu-id="24b0a-132">`https://www.nuget.org/api/v2` (**O protocolo v2 foi preterido!**)</span><span class="sxs-lookup"><span data-stu-id="24b0a-132">`https://www.nuget.org/api/v2` (**The V2 protocol is deprecated!**)</span></span>
