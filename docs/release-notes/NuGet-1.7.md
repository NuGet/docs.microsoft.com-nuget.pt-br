---
title: Notas de versão 1.7 do NuGet
description: Notas de versão do NuGet 1.7 incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 81db81642ac21b7dd41f5940dfba919d0871ec01
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820921"
---
# <a name="nuget-17-release-notes"></a>Notas de versão 1.7 do NuGet

[Notas de versão do NuGet 1.6](../release-notes/nuget-1.6.md) | [notas de versão 1.8 do NuGet](../release-notes/nuget-1.8.md)

1.7 NuGet foi lançado em 4 de abril de 2012.

## <a name="known-installation-issue"></a>Problema de instalação conhecidos
Se você estiver executando o VS 2010 SP1, você pode executar em um erro de instalação durante a tentativa de atualizar o NuGet se você tiver uma versão mais antiga.

A solução alternativa é simplesmente desinstalar NuGet e, em seguida, instalá-lo a partir da Galeria de extensão do VS.  Veja [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) para obter mais informações.

Observação: Se o Visual Studio não permitirão que você desinstalar a extensão (o botão de desinstalação estiver desabilitado), em seguida, provavelmente você precisa reiniciar o Visual Studio usando "Executar como administrador".

## <a name="features"></a>Recursos

### <a name="support-opening-readmetxt-file-after-installation"></a>Suporte para abertura de arquivo Leiame. txt após a instalação
Novo no 1.7, se o pacote inclui um `readme.txt` arquivo na raiz do pacote, o NuGet abrirá automaticamente esse arquivo depois que ele terminou de instalar o pacote.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>Mostrar pacotes de pré-lançamento na caixa de diálogo Gerenciar NuGet pacotes
A caixa de diálogo Gerenciar pacotes NuGet agora inclui uma lista suspensa que fornece a opção para mostrar os pacotes de pré-lançamento.

![Mostrando os pacotes de pré-lançamento](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>Mostrar botão de restauração de pacotes quando os arquivos de pacote estão ausentes
Quando você abrir o console do Gerenciador de pacotes ou pacotes do NuGet do Gerenciador de caixa de diálogo, o NuGet irá verificar se a solução atual tiver habilitado o modo de restauração de pacote e se os arquivos de pacote estão ausentes do `packages` pasta. Se estas duas condições forem atendidas, o NuGet será notificado e mostrará um botão Restaurar conveniente. Este botão irá disparar o NuGet para restaurar todos os pacotes ausentes.

![Botão de restauração do pacote na caixa de diálogo](./media/packagerestore-dialog.png)

![Botão de restauração do pacote no console](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>Adicionar arquivo Packages. config de nível de solução
Nas versões anteriores do NuGet, cada projeto tem um `packages.config` arquivo que mantém o controle de quais pacotes NuGet estão instalados no projeto. No entanto, não houve nenhum arquivo semelhante no nível da solução para controlar os pacotes de solução de nível. Como resultado, não havia uma maneira de restaurar os pacotes de solução de nível.
Agora, esse recurso é implementado no NuGet 1.7. Nível da solução `packages.config` arquivo está sob o `.nuget` pasta sob a solução raiz e armazena os pacotes somente de solução de nível.

### <a name="remove-new-package-command"></a>Remova o comando New-Package
Devido ao uso de baixo, o comando New-Package foi removido. Os desenvolvedores são recomendados para usar o nuget.exe ou o Explorador de pacotes do NuGet útil para criar pacotes.

## <a name="bug-fixes"></a>Correções de Bug
1.7 NuGet corrigiu vários bugs em torno de fluxo de trabalho de restauração de pacotes e cenários de controle de origem da rede /.

Para obter uma lista completa de trabalho itens corrigidos no NuGet 1.7. exibir o [NuGet Issue Tracker para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
