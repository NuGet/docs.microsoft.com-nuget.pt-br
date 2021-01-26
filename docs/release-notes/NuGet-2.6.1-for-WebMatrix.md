---
title: Notas de versão do NuGet 2.6.1 para WebMatrix
description: Notas de versão do NuGet 2.6.1 para WebMatrix, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: de568829efd5060f3b02c3129ccfee2b27782821
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780419"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>Notas de versão do NuGet 2.6.1 para WebMatrix

Notas de versão do [NuGet 2,6](../release-notes/nuget-2.6.md)  |  [Notas de versão do NuGet 2,7](../release-notes/nuget-2.7.md)

A equipe do NuGet lançou uma extensão atualizada do Gerenciador de pacotes do NuGet para WebMatrix em 26 de março de 2014.  Essa atualização pode ser instalada a partir da [Galeria de extensões do WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) usando as seguintes etapas:

1. Abrir o WebMatrix 3
1. Clique no ícone extensões na faixa de faixas página inicial
1. Selecione a guia Atualizações
1. Clique para atualizar o Gerenciador de pacotes NuGet para 2.6.1
1. Fechar e reiniciar o WebMatrix 3

## <a name="notable-changes"></a>Alterações notáveis

Essa atualização de extensão aborda dois dos maiores problemas que os usuários enfrentam para consumir pacotes NuGet no WebMatrix.  O primeiro era um erro de versão do esquema do NuGet e o segundo era um bug que levava a DLLs de zero byte na `bin` pasta.

### <a name="nuget-schema-version-error"></a>Erro de versão do esquema do NuGet

Como o WebMatrix 3 foi lançado, novos recursos foram introduzidos no NuGet que exigem uma nova versão de esquema para os pacotes NuGet.  Ao tentar gerenciar seus pacotes NuGet no seu site, esses novos pacotes podem levar a erros que você vê no WebMatrix.

![Ocorreu um erro. A versão do esquema é incompatível. Atualize o NuGet para a versão mais recente.](./media/NuGet-2.8/webmatrix-schema-version.png)

Esta versão mais recente fornece compatibilidade com os pacotes NuGet mais recentes, impedindo que esse erro ocorra. Novas versões de pacotes, incluindo Microsoft. AspNet. webpages, agora podem ser instaladas no WebMatrix.  Alguns desses pacotes estavam usando recursos do NuGet, como [transformações de configuração xdt](../release-notes/nuget-2.6.md#xdt), que não tinha suporte no WebMatrix até agora.

### <a name="zero-byte-dlls-in-bin-folder"></a>Zero-Byte DLLs na pasta bin

Alguns usuários relataram que depois de instalar os pacotes NuGet no WebMatrix que incluem DLLs que são copiadas para o compartimento, que as DLLs aparecem na `bin` pasta como arquivos de 0 byte.  Isso interrompe o aplicativo em tempo de execução.

[Esse problema](https://nuget.codeplex.com/workitem/4060) agora foi corrigido.

## <a name="other-recent-improvements"></a>Outros aprimoramentos recentes

Quando o Gerenciador de pacotes NuGet 2,8 foi lançado para o Visual Studio, também lançamos o Gerenciador de pacotes NuGet 2.5.0 para WebMatrix.  Embora isso tenha sido mencionado nas [notas de versão do NuGet 2,8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), não mencionamos os novos recursos específicos que a atualização introduziu.

### <a name="update-all"></a>Atualizar Tudo

Agora você pode atualizar todos os pacotes de seu site em uma única etapa!  Quando você abre a extensão NuGet no WebMatrix, você vê a lista de todos os pacotes na Galeria, aqueles instalados e aqueles com atualizações disponíveis.  Anteriormente, todo pacote teria que ser atualizado individualmente, mas agora há um botão "atualizar tudo" útil que aparece na guia Atualizações.

![Clique em atualizar tudo para atualizar todos os pacotes com atualizações disponíveis](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>Substituir arquivos existentes

Ao instalar pacotes que contêm arquivos que já existem no seu site, o NuGet sempre ignorou silenciosamente esses arquivos (deixando apenas os arquivos existentes).  Isso pode levar à impressão de que um pacote foi instalado ou atualizado corretamente quando, na verdade, não era.  Agora, o NuGet solicitará que os arquivos sejam substituídos.

![Resolução de conflito de arquivo](./media/NuGet-2.8/webmatrix-overwrite-file.png)
