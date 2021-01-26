---
title: Notas de versão do NuGet 3.2.1
description: Notas de versão do NuGet 3.2.1, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cbbef3517122ceda91cb4b4463fe8be43d204db4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776525"
---
# <a name="nuget-321-release-notes"></a>Notas de versão do NuGet 3.2.1

Notas de versão do [NuGet 3,2](../release-notes/nuget-3.2.md)  |  [Notas de versão do NuGet 3,3](../release-notes/nuget-3.3.md)

O NuGet 3.2.1 para a linha de comando foi lançado em 12 de outubro de 2015 com algumas otimizações e correções para a versão 3,2 e está disponível em [dist.NuGet.org](http://dist.nuget.org/index.html).

## <a name="improvements"></a>Aprimoramentos

* O NuGet agora usa o arquivo de configuração com a capitalização original de `NuGet.Config` .  Isso é importante em sistemas operacionais com distinção de maiúsculas e minúsculas [1427](https://github.com/NuGet/Home/issues/1427)
* A restauração do NuGet agora irá ignorar projetos DNX ( `*.xproj` ) que devem ser processados com `dnu` [1227](https://github.com/NuGet/Home/issues/1227)
* Utilização de rede otimizada ao trabalhar com `index.json` e empacotar dados de registro [1426](https://github.com/NuGet/Home/issues/1426)
* Tratamento aprimorado de download de recursos para ser mais robusto com os serviços v2 [1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>Correções

* A atualização do NuGet atualiza corretamente as `.csproj` / `.vcxproj` referências [1483](https://github.com/NuGet/Home/issues/1483)
* Agora, impedir que uma pasta local. NuGet seja criada quando um SpecialFolders. UserProfile não puder ser localizado [1531](https://github.com/NuGet/Home/issues/1531)
* Tratamento aprimorado de pacotes no cache local que estão corrompidos durante o download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

Uma lista completa de problemas abordados para a extensão de linha de comando e do Visual Studio pode ser encontrada no [Marco](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed) do GitHub do NuGet 3.2.1

## <a name="known-issues"></a>Problemas conhecidos

Continuamos a acompanhar problemas em nossa lista de problemas do GitHub, que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)