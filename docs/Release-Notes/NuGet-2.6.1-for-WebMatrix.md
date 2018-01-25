---
title: "NuGet 2.6.1 para notas de versão do WebMatrix | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 119ea65b-b38b-4a8c-a4ed-6ea06f1aad09
description: "Notas de versão do NuGet 2.6.1 para o WebMatrix, incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "NuGet 2.6.1 para notas de versão do WebMatrix, correções de bugs, problemas conhecidos, adicionar recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9c37ddc998378b8aaa477dd5df814bab6f0b3c58
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>NuGet 2.6.1 para notas de versão do WebMatrix

[Notas de versão do NuGet 2.6](../release-notes/nuget-2.6.md) | [notas de versão do NuGet 2.7](../release-notes/nuget-2.7.md)

A equipe do NuGet lançou uma extensão NuGet Package Manager atualizado para o WebMatrix em 26 de março de 2014.  Essa atualização pode ser instalada do [Galeria de extensões do WebMatrix](http://extensions.webmatrix.com/packages/NuGetPackageManager/) usando as seguintes etapas:

1. Abrir o WebMatrix 3
2. Clique no ícone de extensões na faixa de opções página inicial
3. Selecione a guia atualizações
4. Clique para atualizar o NuGet Package Manager 2.6.1
6. Feche e reinicie o WebMatrix 3

## <a name="notable-changes"></a>Alterações importantes

Esta extensão atualização resolve dois dos maiores usuários problemas ter enfrentado consumo pacotes do NuGet do WebMatrix.  O primeiro um erro de versão de esquema do NuGet e o segundo era um bug que levam a DLLs de zero bytes no `bin` pasta.

### <a name="nuget-schema-version-error"></a>Erro de versão do esquema do NuGet

Desde o lançamento do WebMatrix 3, novos recursos foram introduzidos NuGet que exigem uma nova versão de esquema para os pacotes do NuGet.  Ao tentar gerenciar seus pacotes do NuGet em seu site da web, esses novos pacotes podem levar a erros que você verá no WebMatrix.

![Ocorreu um erro. A versão do esquema é incompatível. Atualize o NuGet para a versão mais recente.](./media/NuGet-2.8/webmatrix-schema-version.png)

Esta última versão fornece compatibilidade com os pacotes do NuGet mais recentes, impedindo que esse erro ocorra. Novas versões de pacotes, inclusive Microsoft.AspNet.WebPages agora podem ser instaladas no WebMatrix.  Alguns desses pacotes foram usando recursos do NuGet como [XDT config transforma](../release-notes/nuget-2.6.md#xdt), que não era suportado no WebMatrix até agora.

### <a name="zero-byte-dlls-in-bin-folder"></a>DLLs de zero bytes na pasta de compartimento

Alguns usuários relatou que depois de instalar o NuGet empacota no WebMatrix que incluem DLLs que podem ser copiadas para guardar, que mostram as DLLs no `bin` pasta arquivos de 0 byte.  Isso interrompe o aplicativo em tempo de execução.

[Esse problema](https://nuget.codeplex.com/workitem/4060) agora foram corrigidos.

## <a name="other-recent-improvements"></a>Outros aperfeiçoamentos recentes

Quando foi lançado 2.8 de Gerenciador de pacote do NuGet para Visual Studio, também lançamos NuGet Package Manager 2.5.0 para o WebMatrix.  Enquanto isso foi mencionado o [notas de versão do NuGet 2.8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), não mencionamos específico novos recursos que introduziu a atualização.

### <a name="update-all"></a>Atualizar tudo

Agora você pode atualizar todos os pacotes do seu site em uma única etapa!  Quando você abre a extensão do NuGet no WebMatrix, você ver a lista de todos os pacotes em Galeria, estiverem instalados e as atualizações disponíveis.  Anteriormente, cada pacote precisa ser atualizado individualmente, mas agora há um botão "Atualizar tudo" útil que aparece na guia atualizações.

![Clique em Atualizar tudo para atualizar todos os pacotes com atualizações disponíveis](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>Substituir arquivos existentes

Ao instalar os pacotes que contêm arquivos que já existem no seu site da web, NuGet sempre apenas silenciosamente ignorado esses arquivos (abandonando os arquivos existentes).  Isso poderia gerar a impressão de que um pacote foi instalado ou atualizado corretamente quando na verdade não era.  NuGet agora solicita arquivos a serem substituídos.

![Resolução de conflitos de arquivo](./media/NuGet-2.8/webmatrix-overwrite-file.png)
