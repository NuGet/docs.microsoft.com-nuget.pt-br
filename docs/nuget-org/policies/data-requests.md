---
title: Solicitações de dados de usuário
description: Políticas de solicitação de exportação e exclusão de dados de usuário
author: karann-msft
ms.author: karann
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: ef054f741755bccf56eedfd462915b8e9fd6931a
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "67426981"
---
# <a name="user-data-requests"></a>Solicitações de dados de usuário

nuget.org os usuários podem enviar informações para excluir solicitações e solicitações de exportação de informações através [de nuget.org](https://www.nuget.org). Ambos os tipos são submetidos sob a forma de solicitações de suporte e são executados pelos administradores nuget.org dentro de 30 dias.

Os seguintes dados do usuário podem ser acessados diretamente por meio do nuget.org:

* Dados relacionados a contas, como endereço de email, conta de logon, imagem do perfil e configurações de notificação por email
* Chaves de API de propriedade
* Lista de pacotes de propriedade

Esses dados não são incluídos nos dados exportados pela solicitação de suporte.

## <a name="identifying-customer-data"></a>Identificando os dados do cliente

Os dados do cliente podem ser identificados como nomes de conta de usuário do nuget.org.

## <a name="deleting-customer-data"></a>Excluindo os dados do cliente

Para solicitar a exclusão de dados de usuário do nuget.org:

1. O usuário precisa entrar no [nuget.org](https://www.nuget.org)
1. O usuário precisa enviar uma solicitação de exclusão da conta [nuget.org/account/delete](https://www.nuget.org/account/delete)

Recomenda-se que os usuários que são proprietários únicos de pacotes encontrem novos proprietários antes de solicitar a exclusão da conta. Se a propriedade do pacote não for transferida, o pacote do NuGet não será mais listado e, como resultado, não estará mais disponível nas consultas de pesquisa do Visual Studio nem no site nuget.org. Antes de excluir a conta, os administradores do nuget.org ajudam o usuário a encontrar novos proprietários para seus pacotes.

A ação de exclusão de conta é concluída pelo administrador do nuget.org em até 30 dias a partir da data da solicitação.

Após a exclusão da conta, todos os dados do usuário são removidos do sistema nuget.org e as seguintes ações são executadas:

* A conta excluída torna-se não registrada no nuget.org
* Todas as chaves de API de propriedade são excluídas
* Todos os namespaces reservados são liberados
* Todas as propriedades de pacotes são removidas

Os pacotes de propriedade *não* são excluídos. Embora não conste na lista de resultados da pesquisa, eles permanecem disponíveis por meio da restauração de pacote para projetos que dependem deles.

## <a name="exporting-customer-data"></a>Exportando os dados do cliente

Depois de entrar no nuget.org, o usuário pode enviar uma solicitação de exportação por meio de [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)

Os dados exportados são disponibilizados por 48 horas ao usuário para download por meio de um Blob do Azure. Depois de 48 horas, o acesso expira e o usuário precisa enviar uma nova solicitação de exportação, conforme o necessário.

Os dados exportados incluem:

* As solicitações de suporte do usuário
* As ações do usuário (publicar o pacote, criar conta) persistentes nos logs de auditoria
* Informações de usuário persistentes nos logs do IIS
