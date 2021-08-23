---
title: NuGet notas sobre a versão 5.11
description: Notas sobre a versão NuGet 5.11, incluindo novos recursos, correções de bugs e DCRs.
author: erdembayar
ms.author: eryondon
ms.date: 8/10/2021
ms.topic: conceptual
ms.openlocfilehash: 97b59be0fa3da2bfb788e540fef795522d938ed4
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/23/2021
ms.locfileid: "122728430"
---
# <a name="nuget-511-release-notes"></a>NuGet notas sobre a versão 5.11

Veículos de distribuição do NuGet:

| Versão do NuGet | Disponível na versão do Visual Studio | Disponível em SDKs do .NET |
|:---|:---|:---|
| [**5.11.0**](https://nuget.org/downloads) | [Visual Studio 2019 versão 16.11](https://visualstudio.microsoft.com/downloads/) | [5.0.400](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> Instalado com o Visual Studio 2019 com carga de trabalho do .NET Core
  
> [!NOTE]
> Visual Studio 16.11, MSBuild 16.11 e .NET 5.0.400+ requer NuGet.exe 5.11 ou posterior.

## <a name="summary-whats-new-in-511"></a>Resumo: Novidades na versão 5.11

### <a name="issues-fixed-in-this-release"></a>Problemas corrigidos nesta versão

**Bugs:**

* Ferramentas -> Opções -> NuGet Gerenciador de Pacotes cadeia de caracteres é truncada - [#10779](https://github.com/NuGet/Home/issues/10779)

* Trava quando o evento PackagesMissingStatusChanged é [acionado](https://github.com/NuGet/Home/issues/10854) – #10854

* O NuGet cliente ignora a configuração de NO_PROXY - [#10902](https://github.com/NuGet/Home/issues/10902)

**[Lista de todos os problemas corrigidos nesta versão – 5.11](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTk5MDE)**

**[Lista de confirmações nesta versão – 5.11](https://github.com/NuGet/NuGet.Client/compare/5.10.0.7240...5.11.0.17)**

## <a name="feedback-welcome"></a>Boas-vindas aos comentários

Seus comentários são importantes para nós.  Se houver problemas com esta versão, verifique nossos problemas GitHub e Visual Studio [desenvolvedor Community](https://developercommunity.visualstudio.com/) problemas existentes. [](https://github.com/NuGet/Home/issues)  Para novos problemas no NuGet, informe um [GitHub problema](https://github.com/NuGet/Home/issues/new).
Para problemas NuGet experiência geral, informe-nos [](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) por meio da opção Relatar um problema encontrada em seu IDE favorito em Ajuda > **Relatar um Problema**.
