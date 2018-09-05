---
title: Notas de versão 1.7 do NuGet
description: Notas de versão do NuGet de 1,7 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 07cd541ef215d2a1bacc45995a22dadb6dfeac6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551461"
---
# <a name="nuget-17-release-notes"></a>Notas de versão 1.7 do NuGet

[Notas de versão do NuGet 1.6](../release-notes/nuget-1.6.md) | [notas de versão do NuGet 1.8](../release-notes/nuget-1.8.md)

1.7 NuGet foi lançado em 4 de abril de 2012.

## <a name="known-installation-issue"></a>Problema de instalação conhecidos
Se você estiver executando o VS 2010 SP1, você pode executar em um erro de instalação quando tentar atualizar o NuGet se você tiver uma versão mais antiga instalada.

A solução alternativa é simplesmente desinstalar o NuGet e, em seguida, instalá-lo da Galeria de extensão do VS.  Veja [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) para obter mais informações.

Observação: Se o Visual Studio não permitirão que você desinstale a extensão (o botão Desinstalar está desabilitado), em seguida, é provável que você precisa reiniciar o Visual Studio usando "Executar como administrador".

## <a name="features"></a>Recursos

### <a name="support-opening-readmetxt-file-after-installation"></a>Abrindo o arquivo readme. txt após a instalação de suporte
Novo no 1.7, se o pacote inclui um `readme.txt` arquivo na raiz do pacote, o NuGet abrirá automaticamente esse arquivo depois de concluir a instalação de seu pacote.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>Mostrar pacotes de pré-lançamento na caixa de diálogo de pacotes NuGet de gerenciar
A caixa de diálogo Gerenciar pacotes NuGet agora inclui uma lista suspensa que fornece a opção para mostrar os pacotes de pré-lançamento.

![Mostrando os pacotes de pré-lançamento](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>Mostrar botão de restauração de pacote quando os arquivos de pacote estão ausentes
Quando você abrir o console do Gerenciador de pacotes ou pacotes do NuGet o Gerenciador de caixa de diálogo, o NuGet verificará se a solução atual tiver habilitado o modo de restauração de pacote e se os arquivos de pacote estão ausentes do `packages` pasta. Se estas duas condições forem atendidas, o NuGet irá notificá-lo e mostrará um botão Restaurar conveniente. Este botão irá disparar o NuGet para restaurar todos os pacotes ausentes.

![Botão de restauração de pacote na caixa de diálogo](./media/packagerestore-dialog.png)

![Botão de restauração de pacote no console](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>Adicionar arquivo Packages. config do nível da solução
Nas versões anteriores do NuGet, cada projeto tem um `packages.config` arquivo que mantém o controle de quais pacotes do NuGet são instalados no projeto. No entanto, não houve nenhum arquivo semelhante no nível da solução para manter o controle de pacotes de nível de solução. Como resultado, não houve nenhuma maneira de restaurar os pacotes de nível de solução.
Agora, esse recurso é implementado no NuGet 1.7. Nível da solução `packages.config` arquivo está sob o `.nuget` pasta na solução raiz e armazenará o nível da solução apenas pacotes.

### <a name="remove-new-package-command"></a>Remover o comando New-Package
Devido ao baixo uso, o comando New-Package foi removido. Os desenvolvedores são recomendados para usar nuget.exe ou o Explorador de pacotes do NuGet úteis para criar pacotes.

## <a name="bug-fixes"></a>Correções de Bug
1.7 NuGet corrigiu muitos bugs em torno de restauração de pacote do fluxo de trabalho e cenários de controle de fonte/rede.

Para obter uma lista completa de trabalho itens corrigidos no NuGet 1.7, por favor, modo de exibição de [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
