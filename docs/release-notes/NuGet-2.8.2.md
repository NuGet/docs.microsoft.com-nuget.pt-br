---
title: Notas de versão do NuGet 2.8.2
description: Notas de versão do NuGet 2.8.2 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d39f2dc9a429ed264461174325c2080468fa8aae
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780374"
---
# <a name="nuget-282-release-notes"></a>Notas de versão do NuGet 2.8.2

Notas de versão do [NuGet 2.8.1](../release-notes/nuget-2.8.1.md)  |  [Notas de versão do NuGet 2.8.3](../release-notes/nuget-2.8.3.md)

O NuGet 2.8.2 foi lançado em 22 de maio de 2014.  Essa versão inclui apenas alterações na linha de comando nuget.exe, no pacote NuGet. Server e em outros pacotes NuGet.  A versão não incluiu uma extensão do Visual Studio atualizada ou a extensão do WebMatrix.

## <a name="notable-updates"></a>Atualizações notáveis

As atualizações mais notáveis estavam na linha de comando nuget.exe e no pacote NuGet. Server (para feeds do NuGet auto-hospedados).

### <a name="important-nugetexe-bug-fixes"></a>Importantes nuget.exe correções de bugs

1. [nuget.exe Push falha e continua tentando novamente](https://nuget.codeplex.com/workitem/4000)
1. [nuget.exe Push não envia credenciais de autenticação básicas corretamente](https://nuget.codeplex.com/workitem/4109)
1. [nuget.exe Push não seguirá o redirecionamento temporário](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>Correção importante do bug do NuGet. Server

1. [Valor errado de IsAbsoluteLatestVersion retornado pelo NuGet. Server](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>Pacotes atualizados

As correções de linha de comando nuget.exe e NuGet. Server são fornecidas como atualizações de pacote NuGet.  Havia outros pacotes atualizados com 2.8.2 também.

Aqui está a lista de pacotes atualizados:

1. [NuGet. Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet. CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet. Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (o pacote, não a extensão)

## <a name="all-changes"></a>Todas as alterações
Foram abordados 10 problemas na versão. Para obter uma lista completa dos itens de trabalho corrigidos no NuGet 2.8.2, consulte o [rastreador de problemas do NuGet para esta versão](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).
