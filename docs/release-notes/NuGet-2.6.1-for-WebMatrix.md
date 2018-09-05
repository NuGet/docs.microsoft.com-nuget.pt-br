---
title: NuGet 2.6.1 para notas de lançamento do WebMatrix
description: Notas de versão do NuGet 2.6.1 para WebMatrix, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 10d80a921cbc34b537f91644da97efc44530fa75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550311"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>NuGet 2.6.1 para notas de lançamento do WebMatrix

[Notas de versão do NuGet 2.6](../release-notes/nuget-2.6.md) | [notas de versão do NuGet 2.7](../release-notes/nuget-2.7.md)

A equipe do NuGet lançou uma extensão do Gerenciador de pacotes NuGet atualizado para o WebMatrix em 26 de março de 2014.  Essa atualização pode ser instalada do [Galeria de extensão do WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) usando as seguintes etapas:

1. Abre o WebMatrix 3
1. Clique no ícone de extensões na faixa de opções página inicial
1. Selecione a guia atualizações
1. Clique para atualizar o Gerenciador de pacotes NuGet para 2.6.1
1. Feche e reinicie o WebMatrix 3

## <a name="notable-changes"></a>Alterações importantes

Essa extensão atualização resolve dois dos usuários problemas maiores têm enfrentado consumir pacotes do NuGet do WebMatrix.  O primeiro foi um erro de versão de esquema do NuGet e a segunda era um bug que leva a DLLs de zero byte no `bin` pasta.

### <a name="nuget-schema-version-error"></a>Erro de versão do esquema do NuGet

Desde o lançamento do WebMatrix 3, novos recursos foram introduzidos no NuGet que exigem uma nova versão de esquema para os pacotes do NuGet.  Ao tentar gerenciar os pacotes do NuGet em seu site da web, esses novos pacotes podem levar a erros que você vê no WebMatrix.

![Ocorreu um erro. A versão do esquema é incompatível. Atualize o NuGet para a versão mais recente.](./media/NuGet-2.8/webmatrix-schema-version.png)

Esta versão mais recente fornece compatibilidade com os pacotes NuGet mais recentes, impedindo que esse erro ocorra. Novas versões dos pacotes incluindo Microsoft.AspNet.WebPages agora podem ser instaladas no WebMatrix.  Alguns desses pacotes foram usando recursos do NuGet, como [transformações XDT config](../release-notes/nuget-2.6.md#xdt), que não era suportado no WebMatrix até agora.

### <a name="zero-byte-dlls-in-bin-folder"></a>DLLs de zero bytes na pasta de compartimentalização

Alguns usuários relataram que a depois de instalar o NuGet pacotes em WebMatrix que incluem as DLLs que podem ser copiadas para o compartimento que mostram as DLLs para cima no `bin` pasta arquivos de 0 byte.  Isso interrompe o aplicativo em tempo de execução.

[Esse problema](https://nuget.codeplex.com/workitem/4060) agora foi corrigido.

## <a name="other-recent-improvements"></a>Outros aperfeiçoamentos recentes

Quando o Gerenciador de pacote NuGet 2.8 foi lançado para o Visual Studio, também lançamos NuGet Package Manager 2.5.0 para o WebMatrix.  Enquanto isso foi mencionado o [notas de versão do NuGet 2.8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), não mencionamos específico novos recursos que introduziu a atualização.

### <a name="update-all"></a>Atualizar tudo

Agora você pode atualizar todos os pacotes do seu site em uma única etapa!  Quando você abre a extensão do NuGet no WebMatrix, você ver a lista de todos os pacotes na galeria, estiverem instalados e aqueles com atualizações disponíveis.  Anteriormente, todos os pacotes precisaria ser atualizado individualmente, mas agora há um botão "Atualizar tudo" útil que aparece na guia atualizações.

![Clique em Atualizar tudo para atualizar todos os pacotes com atualizações disponíveis](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>Substituir arquivos existentes

Ao instalar os pacotes que contêm arquivos que já existem no seu site da web, o NuGet ignorou silenciosamente sempre apenas desses arquivos (deixando apenas os arquivos existentes).  Isso pode levar a impressão de que um pacote foi instalado ou atualizado corretamente quando na verdade não era.  Agora, o NuGet solicitará para arquivos a serem substituídos.

![Resolução de conflitos de arquivo](./media/NuGet-2.8/webmatrix-overwrite-file.png)
