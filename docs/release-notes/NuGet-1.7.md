---
title: Notas de versão do NuGet 1,7
description: Notas de versão do NuGet 1,7 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 50eb326c5ada4f74685b07c0d1b0f84b14e547ac
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777070"
---
# <a name="nuget-17-release-notes"></a>Notas de versão do NuGet 1,7

Notas de versão do [NuGet 1,6](../release-notes/nuget-1.6.md)  |  [Notas de versão do NuGet 1,8](../release-notes/nuget-1.8.md)

O NuGet 1,7 foi lançado em 4 de abril de 2012.

## <a name="known-installation-issue"></a>Problema de instalação conhecido
Se você estiver executando o VS 2010 SP1, poderá encontrar um erro de instalação ao tentar atualizar o NuGet se tiver uma versão mais antiga instalada.

A solução alternativa é simplesmente desinstalar o NuGet e, em seguida, instalá-lo a partir da Galeria de extensões do VS.  Consulte <https://support.microsoft.com/kb/2581019> para obter mais informações.

Observação: se o Visual Studio não permitir que você desinstale a extensão (o botão desinstalar está desabilitado), provavelmente, você precisará reiniciar o Visual Studio usando "executar como administrador".

## <a name="features"></a>Recursos

### <a name="support-opening-readmetxt-file-after-installation"></a>Suporte ao abrir o arquivo de readme.txt após a instalação
Novo no 1,7, se o pacote incluir um `readme.txt` arquivo na raiz do pacote, o NuGet abrirá automaticamente esse arquivo depois de concluir a instalação do pacote.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>Mostrar pacotes de pré-lançamento na caixa de diálogo gerenciar pacotes NuGet
A caixa de diálogo gerenciar pacotes NuGet agora inclui uma lista suspensa que fornece a opção para mostrar pacotes de pré-lançamento.

![Mostrando pacotes de pré-lançamento](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>Mostrar botão de restauração de pacote quando arquivos de pacote estiverem ausentes
Quando você abre o console do Gerenciador de pacotes ou a caixa de diálogo pacotes NuGet do Gerenciador, o NuGet verificará se a solução atual habilitou o modo de restauração do pacote e se algum arquivo de pacote está ausente da `packages` pasta. Se essas duas condições forem atendidas, o NuGet irá notificá-lo e mostrará um botão de restauração conveniente. Clicar neste botão irá disparar o NuGet para restaurar todos os pacotes ausentes.

![Botão de restauração do pacote na caixa de diálogo](./media/packagerestore-dialog.png)

![Botão de restauração do pacote no console](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>Adicionar arquivo de packages.config no nível da solução
Nas versões anteriores do NuGet, cada projeto tem um `packages.config` arquivo que controla quais pacotes NuGet estão instalados nesse projeto. No entanto, não havia nenhum arquivo semelhante no nível da solução para controlar os pacotes no nível da solução. Como resultado, não havia como restaurar pacotes de nível de solução.
Esse recurso agora está implementado no NuGet 1,7. O arquivo de nível de solução `packages.config` é colocado sob a `.nuget` pasta na raiz da solução e armazenará apenas pacotes no nível da solução.

### <a name="remove-new-package-command"></a>Remover New-Package comando
Devido ao baixo uso, o comando New-Package foi removido. Os desenvolvedores são recomendados a usar nuget.exe ou o Gerenciador de pacotes do NuGet útil para criar pacotes.

## <a name="bug-fixes"></a>Correções de bugs
O NuGet 1,7 corrigiu muitos bugs em relação ao fluxo de trabalho de restauração de pacote e aos cenários de controle de rede/origem.

Para obter uma lista completa de itens de trabalho corrigidos no NuGet 1,7, consulte o [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
