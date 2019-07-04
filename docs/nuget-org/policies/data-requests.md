---
title: Solicitações de dados de usuário
description: Políticas de solicitação de exportação e exclusão de dados de usuário
author: karann-msft
ms.author: karann
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: ef054f741755bccf56eedfd462915b8e9fd6931a
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426981"
---
# <a name="user-data-requests"></a><span data-ttu-id="d0480-103">Solicitações de dados de usuário</span><span class="sxs-lookup"><span data-stu-id="d0480-103">User Data Requests</span></span>

<span data-ttu-id="d0480-104">Os usuários do nuget.org podem enviar solicitações de exclusão de informações e solicitações de exportação de informações por meio do [nuget.org](https://www.nuget.org). Ambos os tipos são enviados em forma de solicitações de suporte e devem ser executados pelos administradores do nuget.org em até 30 dias.</span><span class="sxs-lookup"><span data-stu-id="d0480-104">nuget.org users can submit information delete requests and information export requests through [nuget.org](https://www.nuget.org). Both types are submitted in the form of support requests and are be executed by the nuget.org administrators within 30 days.</span></span>

<span data-ttu-id="d0480-105">Os seguintes dados do usuário podem ser acessados diretamente por meio do nuget.org:</span><span class="sxs-lookup"><span data-stu-id="d0480-105">The following user data is directly accessible through nuget.org:</span></span>

* <span data-ttu-id="d0480-106">Dados relacionados a contas, como endereço de email, conta de logon, imagem do perfil e configurações de notificação por email</span><span class="sxs-lookup"><span data-stu-id="d0480-106">Account related data such as email address, login account, profile picture, and email notification settings</span></span>
* <span data-ttu-id="d0480-107">Chaves de API de propriedade</span><span class="sxs-lookup"><span data-stu-id="d0480-107">Owned API Keys</span></span>
* <span data-ttu-id="d0480-108">Lista de pacotes de propriedade</span><span class="sxs-lookup"><span data-stu-id="d0480-108">List of owned packages</span></span>

<span data-ttu-id="d0480-109">Esses dados não são incluídos nos dados exportados pela solicitação de suporte.</span><span class="sxs-lookup"><span data-stu-id="d0480-109">This data is not included in data exported through the support request.</span></span>

## <a name="identifying-customer-data"></a><span data-ttu-id="d0480-110">Identificando dados do cliente</span><span class="sxs-lookup"><span data-stu-id="d0480-110">Identifying customer data</span></span>

<span data-ttu-id="d0480-111">Os dados do cliente podem ser identificados como nomes de conta de usuário do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d0480-111">Customer data can be identified as nuget.org user account names.</span></span>

## <a name="deleting-customer-data"></a><span data-ttu-id="d0480-112">Excluindo dados de cliente</span><span class="sxs-lookup"><span data-stu-id="d0480-112">Deleting customer data</span></span>

<span data-ttu-id="d0480-113">Para solicitar a exclusão de dados de usuário do nuget.org:</span><span class="sxs-lookup"><span data-stu-id="d0480-113">To request deleting user data from nuget.org:</span></span>

1. <span data-ttu-id="d0480-114">O usuário precisa entrar no [nuget.org](https://www.nuget.org)</span><span class="sxs-lookup"><span data-stu-id="d0480-114">The user must sign-in to [nuget.org](https://www.nuget.org)</span></span>
1. <span data-ttu-id="d0480-115">O usuário precisa enviar uma solicitação de exclusão da conta [nuget.org/account/delete](https://www.nuget.org/account/delete)</span><span class="sxs-lookup"><span data-stu-id="d0480-115">The user must submit a request for their account to be deleted [nuget.org/account/delete](https://www.nuget.org/account/delete)</span></span>

<span data-ttu-id="d0480-116">Recomenda-se que os usuários que são proprietários únicos de pacotes encontrem novos proprietários antes de solicitar a exclusão da conta.</span><span class="sxs-lookup"><span data-stu-id="d0480-116">Users that are sole owners of packages are encouraged to find new owners before asking to have their account deleted.</span></span> <span data-ttu-id="d0480-117">Se a propriedade do pacote não for transferida, o pacote do NuGet não será mais listado e, como resultado, não estará mais disponível nas consultas de pesquisa do Visual Studio nem no site nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d0480-117">If package ownership is not transferred, the NuGet package is unlisted and, as a result, it is no longer available in search queries in Visual Studio or on the nuget.org website.</span></span> <span data-ttu-id="d0480-118">Antes de excluir a conta, os administradores do nuget.org ajudam o usuário a encontrar novos proprietários para seus pacotes.</span><span class="sxs-lookup"><span data-stu-id="d0480-118">Before deleting the account, the nuget.org administrators work with the user to find new owners for the packages they own.</span></span>

<span data-ttu-id="d0480-119">A ação de exclusão de conta é concluída pelo administrador do nuget.org em até 30 dias a partir da data da solicitação.</span><span class="sxs-lookup"><span data-stu-id="d0480-119">The account delete action is completed by the nuget.org administrator within 30 days from the date of the request.</span></span>

<span data-ttu-id="d0480-120">Após a exclusão da conta, todos os dados do usuário são removidos do sistema nuget.org e as seguintes ações são executadas:</span><span class="sxs-lookup"><span data-stu-id="d0480-120">Upon account deletion, all of the user's data is be removed from the nuget.org system and the following actions are taken:</span></span>

* <span data-ttu-id="d0480-121">A conta excluída torna-se não registrada no nuget.org</span><span class="sxs-lookup"><span data-stu-id="d0480-121">The deleted account becomes unregistered with nuget.org</span></span>
* <span data-ttu-id="d0480-122">Todas as chaves de API de propriedade são excluídas</span><span class="sxs-lookup"><span data-stu-id="d0480-122">All owned API Keys are deleted</span></span>
* <span data-ttu-id="d0480-123">Todos os namespaces reservados são liberados</span><span class="sxs-lookup"><span data-stu-id="d0480-123">All reserved namespaces are released</span></span>
* <span data-ttu-id="d0480-124">Todas as propriedades de pacotes são removidas</span><span class="sxs-lookup"><span data-stu-id="d0480-124">Any package ownership are removed</span></span>

<span data-ttu-id="d0480-125">Os pacotes de propriedade *não* são excluídos.</span><span class="sxs-lookup"><span data-stu-id="d0480-125">The owned packages are *not* deleted.</span></span> <span data-ttu-id="d0480-126">Embora não conste na lista de resultados da pesquisa, eles permanecem disponíveis por meio da restauração de pacote para projetos que dependem deles.</span><span class="sxs-lookup"><span data-stu-id="d0480-126">Though unlisted from search results, they remain available through package restore to projects that depend on them.</span></span>

## <a name="exporting-customer-data"></a><span data-ttu-id="d0480-127">Exportando dados do cliente</span><span class="sxs-lookup"><span data-stu-id="d0480-127">Exporting customer data</span></span>

<span data-ttu-id="d0480-128">Depois de entrar no nuget.org, o usuário pode enviar uma solicitação de exportação por meio de [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span><span class="sxs-lookup"><span data-stu-id="d0480-128">After sign-in to nuget.org, a user can submit an export request through [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span></span>

<span data-ttu-id="d0480-129">Os dados exportados são disponibilizados por 48 horas ao usuário para download por meio de um Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="d0480-129">The data exported is made available for 48 hours to the user for download through an Azure Blob.</span></span> <span data-ttu-id="d0480-130">Depois de 48 horas, o acesso expira e o usuário precisa enviar uma nova solicitação de exportação, conforme o necessário.</span><span class="sxs-lookup"><span data-stu-id="d0480-130">After 48 hours, access expires and the user must submit a new export request as needed.</span></span>

<span data-ttu-id="d0480-131">Os dados exportados incluem:</span><span class="sxs-lookup"><span data-stu-id="d0480-131">The exported data includes:</span></span>

* <span data-ttu-id="d0480-132">As solicitações de suporte do usuário</span><span class="sxs-lookup"><span data-stu-id="d0480-132">The user's support requests</span></span>
* <span data-ttu-id="d0480-133">As ações do usuário (publicar o pacote, criar conta) persistentes nos logs de auditoria</span><span class="sxs-lookup"><span data-stu-id="d0480-133">The user's actions (publish package, create account) as persisted in the audit logs</span></span>
* <span data-ttu-id="d0480-134">Informações de usuário persistentes nos logs do IIS</span><span class="sxs-lookup"><span data-stu-id="d0480-134">Any user information as persisted in the IIS logs</span></span>
