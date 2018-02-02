---
title: Excluindo pacotes do NuGet do nuget.org | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Políticas para remover pacotes do nuget.org; a exclusão permanente não é compatível, exceto quando os pacotes violam outras políticas."
keywords: "Exclusão de pacote do NuGet, remoção de pacote do NuGet da lista, usos proibidos de pacotes"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6169e46e55176757bc1ad471a3d80885cb50e403
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="deleting-packages"></a>Excluindo pacotes

O nuget.org não é compatível com a exclusão permanente de pacotes. Isso interrompe todos os projetos dependendo da disponibilidade do pacote, especialmente com fluxos de trabalho de build que envolvem a restauração do pacote.

O nuget.org é compatível com a *remoção* de um pacote da lista, o que pode ser feito na página de gerenciamento de pacotes no site. Pacotes não listados não aparecem em nuget.org ou na interface do usuário do Visual Studio e não aparecem nos resultados da pesquisa. Pacotes não listados, no entanto, ainda podem ser baixados e instalados usando um número de versão exata, compatível com a restauração do pacote. Além disso, os pacotes não listados ainda podem ser descobertos nos seguintes cenários específicos:

- Restauração de pacote usando versões flutuante (por exemplo, `1.0.0-*`), se o pacote mais recente que corresponder às restrições de versão ou de dependência for um pacote não listado.
- Replicação de pacotes por meio do catálogo (visto que o catálogo também contém os pacotes não listados).

## <a name="exceptions"></a>Exceções

Em situações excepcionais como violação de direitos autorais e conteúdo potencialmente prejudicial, os pacotes podem ser excluídos manualmente pela equipe do NuGet. Envie uma solicitação de suporte por meio da [Galeria NuGet](http://www.nuget.org) para iniciar o processo.

## <a name="prohibited-use"></a>Uso proibido

Pacotes que atendem a qualquer um dos critérios a seguir não são permitidos na Galeria NuGet pública e serão removidos imediatamente sem discussão. Os proprietários dos pacotes serão, contudo, notificados sobre a remoção.

- Contém malware, adware ou qualquer tipo de spyware.
- Foi projetado para prejudicar a estação de trabalho do desenvolvedor ou sua organização.
- Viola direitos autorais ou licenças.
- Tem conteúdo ilegal.
- Está sendo usado para ocultar identificadores de pacote, incluindo pacotes que não tem nenhum conteúdo produtivo. Os pacotes precisam conter código ou os proprietários precisam conceder o identificador para alguém que realmente tem um produto para enviar.
- Tenta fazer a galeria fazer algo que ela não foi explicitamente projetada para fazer.

Se você encontrar um pacote que representa uma violação de qualquer um desses itens, clique no link **Relatar Abuso** na página de detalhes do pacote e envie um relatório.

Observe que a equipe do NuGet e a .NET Foundation reserva o direito de alterar esses critérios a qualquer momento.
