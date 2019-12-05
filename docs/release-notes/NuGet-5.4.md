---
title: Notas de versão do NuGet 5,4
description: Notas de versão do NuGet 5,4, incluindo novos recursos, correções de bugs e DCRs.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 69f78ba5483fcc92887624584663e8c496cfc497
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2019
ms.locfileid: "74828404"
---
# <a name="nuget-54-release-notes"></a>Notas de versão do NuGet 5,4

Veículos de distribuição do NuGet:

| Versão do NuGet | Disponível na versão do Visual Studio| Disponível em SDKs do .NET|
|:---|:---|:---|
| [**5.4.0**](https://nuget.org/downloads) | [Visual Studio 2019 versão 16,4](https://visualstudio.microsoft.com/downloads/) | [3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> Instalado com o Visual Studio 2019 com carga de trabalho do .NET Core

## <a name="summary-whats-new-in-54"></a>Resumo: o que há de novo no 5,4

* Tempo de carregamento de solução mais rápido – a sobrecarga de execução do código NuGet durante o primeiro carregamento da solução foi reduzida por meio de um NGen parcial para reduzir [#6007](https://github.com/NuGet/Home/issues/6007) de custo JIT

* Nova função auxiliar – dada uma lista de IDs e versões de pacote, obtenha os pacotes de nível superior prováveis. - [#8316](https://github.com/NuGet/Home/issues/8316)

### <a name="issues-fixed-in-this-release"></a>Problemas corrigidos nesta versão

**•s**

* Plugin: a precisão do tempo de log está desativada no Linux/Mac- [#8747](https://github.com/NuGet/Home/issues/8747)

* A descartação de um plug-in pode, às vezes, lançar e falhar toda a operação. - [#8732](https://github.com/NuGet/Home/issues/8732)

* Parar de exibir duplicatas de versão na lista de versões permitidas e bloqueadas em PMUI- [#8679](https://github.com/NuGet/Home/issues/8679)

* O arquivo de bloqueio não foi gerado corretamente-a ordenação de estrutura não deve afetar a restauração com o modo bloqueado- [#8645](https://github.com/NuGet/Home/issues/8645)

* A validação de lockfile falha para projetos com <RuntimeIdentifiers> definido no SDK 3.0.100- [#8639](https://github.com/NuGet/Home/issues/8639)

* A validação de assinatura agora rejeitará corretamente as assinaturas com carimbos de data/hora que têm 2 valores na mesma OID- [#8629](https://github.com/NuGet/Home/issues/8629)

* Atualizar a lista de licenças- [#8544](https://github.com/NuGet/Home/issues/8544)

**DCRs**

* Integração de arquivos de diagnóstico ao IFeedbackDiagnosticFileProvider- [#8535](https://github.com/NuGet/Home/issues/8535)

**[Lista de todos os problemas corrigidos nesta versão-5,4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**
