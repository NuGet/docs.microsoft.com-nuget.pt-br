---
title: Notas de versão do NuGet 1,7
description: Notas de versão do NuGet 1,7 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a98da76038582202396c8da96f8eae166e6096f6
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383313"
---
# <a name="nuget-17-release-notes"></a>Notas de versão do NuGet 1,7

[Notas de versão do nuget 1,6](../release-notes/nuget-1.6.md) | [notas de versão do NuGet 1,8](../release-notes/nuget-1.8.md)

O NuGet 1,7 foi lançado em 4 de abril de 2012.

## <a name="known-installation-issue"></a>Problema de instalação conhecido
Se você estiver executando o VS 2010 SP1, poderá encontrar um erro de instalação ao tentar atualizar o NuGet se tiver uma versão mais antiga instalada.

A solução alternativa é simplesmente desinstalar o NuGet e, em seguida, instalá-lo a partir da Galeria de extensões do VS.  Consulte <https://support.microsoft.com/kb/2581019> para obter mais informações.

Observação: se o Visual Studio não permitir que você desinstale a extensão (o botão desinstalar está desabilitado), provavelmente, você precisará reiniciar o Visual Studio usando "executar como administrador".

## <a name="features"></a>Recursos

### <a name="support-opening-readmetxt-file-after-installation"></a>Suporte à abertura do arquivo readme. txt após a instalação
Novo no 1,7, se o pacote incluir um arquivo de `readme.txt` na raiz do pacote, o NuGet abrirá automaticamente esse arquivo depois de concluir a instalação do pacote.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>Mostrar pacotes de pré-lançamento na caixa de diálogo gerenciar pacotes NuGet
A caixa de diálogo gerenciar pacotes NuGet agora inclui uma lista suspensa que fornece a opção para mostrar pacotes de pré-lançamento.

![Mostrando pacotes de pré-lançamento](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>Mostrar botão de restauração de pacote quando arquivos de pacote estiverem ausentes
Quando você abre o console do Gerenciador de pacotes ou a caixa de diálogo pacotes NuGet do Gerenciador, o NuGet verificará se a solução atual habilitou o modo de restauração do pacote e se algum arquivo de pacote está ausente na pasta `packages`. Se essas duas condições forem atendidas, o NuGet irá notificá-lo e mostrará um botão de restauração conveniente. Clicar neste botão irá disparar o NuGet para restaurar todos os pacotes ausentes.

![Botão de restauração do pacote na caixa de diálogo](./media/packagerestore-dialog.png)

![Botão de restauração do pacote no console](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>Adicionar arquivo Packages. config de nível de solução
Nas versões anteriores do NuGet, cada projeto tem um arquivo de `packages.config` que controla quais pacotes NuGet são instalados nesse projeto. No entanto, não havia nenhum arquivo semelhante no nível da solução para controlar os pacotes no nível da solução. Como resultado, não havia como restaurar pacotes de nível de solução.
Esse recurso agora está implementado no NuGet 1,7. O arquivo de `packages.config` no nível da solução é colocado na pasta `.nuget` na raiz da solução e armazenará apenas pacotes no nível da solução.

### <a name="remove-new-package-command"></a>Remover comando de novo pacote
Devido ao baixo uso, o comando New-Package foi removido. Os desenvolvedores são recomendados a usar o NuGet. exe ou o Gerenciador de pacotes do NuGet útil para criar pacotes.

## <a name="bug-fixes"></a>Correções de Bug
O NuGet 1,7 corrigiu muitos bugs em relação ao fluxo de trabalho de restauração de pacote e aos cenários de controle de rede/origem.

Para obter uma lista completa de itens de trabalho corrigidos no NuGet 1,7, consulte o [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
