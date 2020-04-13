---
title: Excluindo pacotes do NuGet de nuget.org
description: Políticas para remover pacotes do nuget.org; a exclusão permanente não é compatível, exceto quando os pacotes violam outras políticas.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 3abe809d76e75801c2f936aba129d27ba7b64913
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "80581272"
---
# <a name="deleting-packages"></a>Excluir pacotes

O nuget.org não é compatível com a exclusão permanente de pacotes. Isso interrompe todos os projetos dependendo da disponibilidade do pacote, especialmente com fluxos de trabalho de build que envolvem a restauração do pacote.

nuget.org suporta [a deslistagem de um pacote,](#unlisting-a-package)que pode ser feito na página de gerenciamento de pacotes no site. Pacotes não listados não aparecem em nuget.org ou na interface do usuário do Visual Studio e não aparecem nos resultados da pesquisa. Pacotes não listados, no entanto, ainda podem ser baixados e instalados usando um número de versão exata, compatível com a restauração do pacote. Além disso, os pacotes não listados ainda podem ser descobertos nos seguintes cenários específicos:

- Restauração de pacote usando versões flutuante (por exemplo, `1.0.0-*`), se o pacote mais recente que corresponder às restrições de versão ou de dependência for um pacote não listado.
- Replicação de pacotes por meio do catálogo (visto que o catálogo também contém os pacotes não listados).

## <a name="exceptions"></a>Exceções

Em situações excepcionais como violação de direitos autorais e conteúdo potencialmente prejudicial, os pacotes podem ser excluídos manualmente pela equipe do NuGet. Você pode relatar um pacote usando o botão "Relatar abuso" na página de detalhes do pacote NuGet.org. Se você for o proprietário do pacote, faça logon em sua conta do NuGet.org para acessar o suporte do NuGet usando o botão "Entrar em contato com o suporte" na página de detalhes do pacote do NuGet.org.

## <a name="prohibited-use"></a>Uso proibido

Pacotes que atendem a qualquer um dos critérios a seguir não são permitidos na Galeria NuGet pública e serão removidos imediatamente sem discussão. Os proprietários dos pacotes serão, contudo, notificados sobre a remoção.

- Contém malware, adware ou qualquer tipo de spyware.
- Foi projetado para prejudicar a estação de trabalho do desenvolvedor ou sua organização.
- Viola direitos autorais ou licenças.
- Tem conteúdo ilegal.
- Está sendo usado para ocultar identificadores de pacote, incluindo pacotes que não tem nenhum conteúdo produtivo. Os pacotes precisam conter código ou os proprietários precisam conceder o identificador para alguém que realmente tem um produto para enviar.
- Tenta fazer a galeria fazer algo que ela não foi explicitamente projetada para fazer.

Se você encontrar um pacote que viole qualquer um desses pacotes, clique no link **Relatar Abuso** na página de detalhes do pacote e envie um relatório.

Observe que a equipe do NuGet e a .NET Foundation reserva o direito de alterar esses critérios a qualquer momento.

## <a name="unlisting-a-package"></a>Deslistagem de um pacote
A deslistagem de uma versão do pacote esconde-a da pesquisa e da página de detalhes do pacote nuget.org. Isso permite que os usuários existentes do pacote continuem a usá-lo, mas reduz a nova adoção, já que o pacote não é visível na pesquisa.

Etapas para deslistar um pacote:

1. Selecione `Your account name` (no canto superior direito) >`Manage packages` > `Published packages`
1. Selecione o ícone "Gerenciar pacote"
1. Expanda a seção "Listagem" e selecione a versão do pacote
1. Desmarque "Listar resultados de pesquisa" e selecione "Salvar"

A versão específica do pacote não foi listada. Para verificar isso, faça logout da sua conta e navegue até a página https://www.nuget.org/packages/YOUR-PACKAGE-NAME/do pacote (sem a parte da versão), por exemplo: . Você verá todas as versões desse pacote que **não** foram listadas. No entanto, o proprietário do pacote, quando conectado, pode ver todas as versões e seu status de listagem.

Também é possível depreciar uma versão do pacote (caso você não possa excluir uma versão do pacote). Para obter mais informações sobre a depreciação das versões do pacote, consulte [Pacotes de depreciação](../deprecate-packages.md).
