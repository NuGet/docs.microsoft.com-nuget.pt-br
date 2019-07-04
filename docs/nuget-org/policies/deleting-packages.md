---
title: Excluindo pacotes do NuGet de nuget.org
description: Políticas para remover pacotes do nuget.org; a exclusão permanente não é compatível, exceto quando os pacotes violam outras políticas.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 833f4a67bc75c5d650e85180b52ecd8f69218f15
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426971"
---
# <a name="deleting-packages"></a><span data-ttu-id="ddc78-103">Excluindo pacotes</span><span class="sxs-lookup"><span data-stu-id="ddc78-103">Deleting packages</span></span>

<span data-ttu-id="ddc78-104">O nuget.org não é compatível com a exclusão permanente de pacotes.</span><span class="sxs-lookup"><span data-stu-id="ddc78-104">nuget.org does not support permanent deletion of packages.</span></span> <span data-ttu-id="ddc78-105">Isso interrompe todos os projetos dependendo da disponibilidade do pacote, especialmente com fluxos de trabalho de build que envolvem a restauração do pacote.</span><span class="sxs-lookup"><span data-stu-id="ddc78-105">Doing so would break every project depending on the availability of the package, especially with build workflows that involve package restore.</span></span>

<span data-ttu-id="ddc78-106">O nuget.org é compatível com a *remoção* de um pacote da lista, o que pode ser feito na página de gerenciamento de pacotes no site.</span><span class="sxs-lookup"><span data-stu-id="ddc78-106">nuget.org does supports *unlisting* a package, which can be done in the package management page on the web site.</span></span> <span data-ttu-id="ddc78-107">Pacotes não listados não aparecem em nuget.org ou na interface do usuário do Visual Studio e não aparecem nos resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="ddc78-107">Unlisted packages don't appear on nuget.org or in the Visual Studio UI, and do not appear in search results.</span></span> <span data-ttu-id="ddc78-108">Pacotes não listados, no entanto, ainda podem ser baixados e instalados usando um número de versão exata, compatível com a restauração do pacote.</span><span class="sxs-lookup"><span data-stu-id="ddc78-108">Unlisted packages, however, can still be downloaded and installed by using an exact version number, which supports package restore.</span></span> <span data-ttu-id="ddc78-109">Além disso, os pacotes não listados ainda podem ser descobertos nos seguintes cenários específicos:</span><span class="sxs-lookup"><span data-stu-id="ddc78-109">In addition, unlisted packages may still be discovered in the following specific scenarios:</span></span>

- <span data-ttu-id="ddc78-110">Restauração de pacote usando versões flutuante (por exemplo, `1.0.0-*`), se o pacote mais recente que corresponder às restrições de versão ou de dependência for um pacote não listado.</span><span class="sxs-lookup"><span data-stu-id="ddc78-110">Package restore using floating versions (for example, `1.0.0-*`), if the latest available package matching the version or dependency constraints is an unlisted package.</span></span>
- <span data-ttu-id="ddc78-111">Replicação de pacotes por meio do catálogo (visto que o catálogo também contém os pacotes não listados).</span><span class="sxs-lookup"><span data-stu-id="ddc78-111">Replication of packages through the catalog (as the catalog also contains unlisted packages).</span></span>

## <a name="exceptions"></a><span data-ttu-id="ddc78-112">Exceções</span><span class="sxs-lookup"><span data-stu-id="ddc78-112">Exceptions</span></span>

<span data-ttu-id="ddc78-113">Em situações excepcionais como violação de direitos autorais e conteúdo potencialmente prejudicial, os pacotes podem ser excluídos manualmente pela equipe do NuGet.</span><span class="sxs-lookup"><span data-stu-id="ddc78-113">In exceptional situations such as copyright infringement and potentially harmful content, packages can be deleted manually by the NuGet team.</span></span> <span data-ttu-id="ddc78-114">Você pode relatar um pacote usando o botão "Relatar abuso" na página de detalhes do pacote NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="ddc78-114">You can report a package using the "Report abuse" button on the NuGet.org package details page.</span></span> <span data-ttu-id="ddc78-115">Se você for o proprietário do pacote, faça logon em sua conta do NuGet.org para acessar o suporte do NuGet usando o botão "Entrar em contato com o suporte" na página de detalhes do pacote do NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="ddc78-115">If you are the package owner, login to your NuGet.org account to reach NuGet support using the "Contact support" button on the NuGet.org package details page.</span></span>

## <a name="prohibited-use"></a><span data-ttu-id="ddc78-116">Uso proibido</span><span class="sxs-lookup"><span data-stu-id="ddc78-116">Prohibited use</span></span>

<span data-ttu-id="ddc78-117">Pacotes que atendem a qualquer um dos critérios a seguir não são permitidos na Galeria NuGet pública e serão removidos imediatamente sem discussão.</span><span class="sxs-lookup"><span data-stu-id="ddc78-117">Packages that meet any of the following criteria are not allowed on the public NuGet gallery and will be immediately removed without discussion.</span></span> <span data-ttu-id="ddc78-118">Os proprietários dos pacotes serão, contudo, notificados sobre a remoção.</span><span class="sxs-lookup"><span data-stu-id="ddc78-118">Package owners will, however, be notified of the removal.</span></span>

- <span data-ttu-id="ddc78-119">Contém malware, adware ou qualquer tipo de spyware.</span><span class="sxs-lookup"><span data-stu-id="ddc78-119">Contains malware, adware, or any kind of spyware.</span></span>
- <span data-ttu-id="ddc78-120">Foi projetado para prejudicar a estação de trabalho do desenvolvedor ou sua organização.</span><span class="sxs-lookup"><span data-stu-id="ddc78-120">Are designed to harm a developer's workstation or their organization.</span></span>
- <span data-ttu-id="ddc78-121">Viola direitos autorais ou licenças.</span><span class="sxs-lookup"><span data-stu-id="ddc78-121">Infringes copyrights or violates licenses.</span></span>
- <span data-ttu-id="ddc78-122">Tem conteúdo ilegal.</span><span class="sxs-lookup"><span data-stu-id="ddc78-122">Contains illegal content.</span></span>
- <span data-ttu-id="ddc78-123">Está sendo usado para ocultar identificadores de pacote, incluindo pacotes que não tem nenhum conteúdo produtivo.</span><span class="sxs-lookup"><span data-stu-id="ddc78-123">Are being used to squat on package identifiers, including packages that have zero productive content.</span></span> <span data-ttu-id="ddc78-124">Os pacotes precisam conter código ou os proprietários precisam conceder o identificador para alguém que realmente tem um produto para enviar.</span><span class="sxs-lookup"><span data-stu-id="ddc78-124">Packages must contain code or the owners must concede the identifier to someone who actually has a product to ship.</span></span>
- <span data-ttu-id="ddc78-125">Tenta fazer a galeria fazer algo que ela não foi explicitamente projetada para fazer.</span><span class="sxs-lookup"><span data-stu-id="ddc78-125">Attempt to make the gallery do something that it's not explicitly designed to do.</span></span>

<span data-ttu-id="ddc78-126">Se você encontrar um pacote que representa uma violação de qualquer um desses itens, clique no link **Relatar Abuso** na página de detalhes do pacote e envie um relatório.</span><span class="sxs-lookup"><span data-stu-id="ddc78-126">If you find a package that is in violation of any of these items, click the **Report Abuse** link on the package details page and submit a report.</span></span>

<span data-ttu-id="ddc78-127">Observe que a equipe do NuGet e a .NET Foundation reserva o direito de alterar esses critérios a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="ddc78-127">Note that the NuGet team and the .NET Foundation reserves the right to change these criteria at any time.</span></span>
