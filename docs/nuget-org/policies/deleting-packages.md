---
title: Excluindo pacotes do NuGet de nuget.org
description: Políticas para remover pacotes do nuget.org; a exclusão permanente não é compatível, exceto quando os pacotes violam outras políticas.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 574ee874e2d6555a2e3e0a0643962e33b7ec1b09
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859441"
---
# <a name="deleting-packages"></a>Excluir pacotes

O nuget.org não é compatível com a exclusão permanente de pacotes. Isso interrompe todos os projetos dependendo da disponibilidade do pacote, especialmente com fluxos de trabalho de build que envolvem a restauração do pacote.

o nuget.org oferece suporte à [deslistação de um pacote](#unlisting-a-package), que pode ser feito na página de gerenciamento de pacotes no site da Web. Pacotes não listados não aparecem em nuget.org ou na interface do usuário do Visual Studio e não aparecem nos resultados da pesquisa. Pacotes não listados, no entanto, ainda podem ser baixados e instalados usando um número de versão exata, compatível com a restauração do pacote. Além disso, os pacotes não listados ainda podem ser descobertos nos seguintes cenários específicos:

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

## <a name="unlisting-a-package"></a>Deslistando um pacote
A deslistação de uma versão de pacote a oculta da pesquisa e da página de detalhes do pacote nuget.org. Isso permite que os usuários existentes do pacote continuem a usá-lo, mas reduz a nova adoção, já que o pacote não é visível na pesquisa.

Etapas para deslistar um pacote:

1. Selecione `Your account name` (no canto superior direito) >`Manage packages` > `Published packages`
1. Selecione o ícone "gerenciar pacote"
1. Expanda a seção "listagem" e selecione a versão do pacote
1. Desmarque "listar nos resultados da pesquisa" e selecione "salvar"

A versão específica do pacote agora foi deslistada. Para verificar isso, faça logoff da sua conta e navegue até a página do pacote (sem a parte da versão), por exemplo: https://www.nuget.org/packages/YOUR-PACKAGE-NAME/ . Você verá todas as versões desse pacote que **não** foram listadas. No entanto, o proprietário do pacote, quando conectado, pode ver todas as versões e seu status de listagem.

Também é possível substituir uma versão do pacote (caso não seja possível excluir uma versão do pacote). Para obter mais informações sobre como substituir versões de pacote, consulte [preterindo pacotes](../deprecate-packages.md).
