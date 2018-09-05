---
title: Notas de versão do NuGet 2.8.2
description: Notas de versão do NuGet 2.8.2 incluindo conhecidos problemas, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ed22aef6766bbe8e4b688e0587304a18eaeb8895
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551142"
---
# <a name="nuget-282-release-notes"></a>Notas de versão do NuGet 2.8.2

[Notas de versão do NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [notas de versão do NuGet 2.8.3](../release-notes/nuget-2.8.3.md)

O NuGet 2.8.2 foi lançado em 22 de maio de 2014.  Esta versão incluídas apenas as alterações a nuget.exe de linha de comando, o pacote do NuGet. Server e outros pacotes do NuGet.  A versão não incluía uma extensão atualizada do Visual Studio ou a extensão do WebMatrix.

## <a name="notable-updates"></a>Atualizações importantes

As atualizações mais importantes ocorreram no nuget.exe de linha de comando e o pacote do NuGet. Server (para feeds de NuGet auto-hospedados).

### <a name="important-nugetexe-bug-fixes"></a>Correções de bugs importantes nuget.exe

1. [NuGet.exe Push falha e mantém a tentar novamente](https://nuget.codeplex.com/workitem/4000)
1. [NuGet.exe por Push não envia as credenciais de autenticação básica corretamente](https://nuget.codeplex.com/workitem/4109)
1. [NuGet.exe por Push não siga redirecionamento temporário](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>Correção de Bug importantes NuGet. Server

1. [Valor incorreto de IsAbsoluteLatestVersion retornado pelo NuGet. Server](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>Pacotes atualizados

Os nuget.exe de linha de comando e as correções do NuGet. Server são fornecidas como atualizações de pacote do NuGet.  Não havia outros pacotes atualizados com 2.8.2 também.

Aqui está a lista de pacotes atualizadas:

1. [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet.Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (o pacote, não a extensão)

## <a name="all-changes"></a>Todas as alterações
Havia 10 problemas abordados na versão. Para obter uma lista completa de trabalho itens corrigidos no NuGet 2.8.2, por favor, modo de exibição de [rastreador de problemas do NuGet para esta versão](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).
