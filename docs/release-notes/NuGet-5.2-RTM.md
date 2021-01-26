---
title: Notas de versão do NuGet 5,2 RTM
description: Notas de versão do NuGet 5,2, incluindo novos recursos, correções de bugs e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: 25fa1d09046a583fb987b9f3dd51a0099f4331a7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776211"
---
# <a name="nuget-52-release-notes"></a>Notas de versão do NuGet 5,2

Veículos de distribuição do NuGet:

| Versão do NuGet | Disponível na versão do Visual Studio| Disponível em SDKs do .NET|
|:---|:---|:---|
| [**5.2.0**](https://nuget.org/downloads) | [Visual Studio 2019 versão 16,2](https://visualstudio.microsoft.com/downloads/) | [2.1.80 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.40 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Instalado com o Visual Studio 2019 com carga de trabalho do .NET Core 

<sup>2</sup> Disponível como uma instalação opcional com o Visual Studio 2019 com carga de trabalho do .NET Core

## <a name="summary-whats-new-in-52"></a>Resumo: o que há de novo no 5,2

* Correção de um bug crítico que causava falhas ocasionais de operação do NuGet devido a problemas de caminho no Linux & Mac- [#7341](https://github.com/NuGet/Home/issues/7341)

* Melhor capacidade de resposta da interface do usuário ao procurar pacotes usando a interface do usuário do Gerenciador de pacotes NuGet no Visual Studio, especialmente perceptível para fontes lentas- [#8039](https://github.com/NuGet/Home/issues/8039)

* Toneladas de correções de confiabilidade para arquivos de bloqueio ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) e plug-in de autenticação ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198),[#7845](https://github.com/NuGet/Home/issues/7845))

### <a name="issues-fixed-in-this-release"></a>Problemas corrigidos nesta versão

**Bugs**

* Perf: console do Gerenciador de pacotes: atraso da interface do usuário atualizando o valor selecionado da ComboBox "projeto padrão"- [#8235](https://github.com/NuGet/Home/issues/8235)

* Desempenho: melhorias de desempenho na interface do usuário do PM- [#8039](https://github.com/NuGet/Home/issues/8039)

* Perf: atraso da interface do usuário ao ler o projeto padrão no PMC- [#6824](https://github.com/NuGet/Home/issues/6824)

* Perf: [vsfeedback] guia de atualização do NuGet congela para um pacote local fonte- [#6470](https://github.com/NuGet/Home/issues/6470)

* Plug-ins: o NuGet aguarda o tempo limite completo de handshake se o plug-in falhar ao iniciar ou encerrar o [#8300](https://github.com/NuGet/Home/issues/8300) inicial

* Plugins: melhorar o diagnóstico da falha de inicialização do plug-in- [#8271](https://github.com/NuGet/Home/issues/8271)

* Plug-ins: problema com a descoberta de nuget.exe de plugins internos- [#8269](https://github.com/NuGet/Home/issues/8269)

* Plugins: o arquivo de cache nunca é de leitura- [#8210](https://github.com/NuGet/Home/issues/8210)

* Plugins: "uma tarefa foi cancelada". erros com o plug-in de autenticação durante a restauração- [#8198](https://github.com/NuGet/Home/issues/8198)

* Cache de plugins não detectável intermitentemente em plataformas Linux- [#7845](https://github.com/NuGet/Home/issues/7845)

* Lockfile: com o ATF, ele tem falso NU1004 devido a uma verificação de igualdade de estrutura de destino inadequada- [#8187](https://github.com/NuGet/Home/issues/8187)

* Lockfile: '--modo bloqueado ' ' sinalizador de restauração não respeitado se o arquivo de bloqueio estiver vazio ou malformado- [#8160](https://github.com/NuGet/Home/issues/8160)

* Lockfile: não há projetos em minúsculas com nomes de assembly personalizados em pacotes bloquear arquivo- [#8114](https://github.com/NuGet/Home/issues/8114)

* Lockfile: tornar a referência do projeto em minúsculas no arquivo de bloqueio- [#7840](https://github.com/NuGet/Home/issues/7840)

* Restaurar: a instalação de um pacote assinado violado resulta em várias tentativas de instalação com falha (com saída repetida)- [#8175](https://github.com/NuGet/Home/issues/8175)

* VS: as opções de usuário da solução falham ao desserializar após a atualização do NuGet- [#8166](https://github.com/NuGet/Home/issues/8166)

* dotnet-List-Package em um projeto UnitTest retorna um erro- [#8154](https://github.com/NuGet/Home/issues/8154)

* Criar grupo de pacotes NuGet para o instalador do VS – corrigindo alguns problemas de configuração do VSIX- [#8033](https://github.com/NuGet/Home/issues/8033)

* GeneratePackageOnBuild não deve definir nobuild. - [#7801](https://github.com/NuGet/Home/issues/7801)

* A nova opção "-SymbolPackageFormat snupkg" gera um erro quando o arquivo. nuspec contém um elemento de referência de assembly explícito- [#7638](https://github.com/NuGet/Home/issues/7638)

* NuGet. targets (498, 5): erro: não foi possível encontrar uma parte do caminho '/tmp/NuGetScratch- [#7341](https://github.com/NuGet/Home/issues/7341)

**DCR:**

* Adicione uma propriedade do MSBuild que indica que PackageDownload tem suporte- [#8106](https://github.com/NuGet/Home/issues/8106)

* FrameworkReference suprimir o fluxo de dependência por meio de FrameworkReference. PrivateAssets- [#7988](https://github.com/NuGet/Home/issues/7988)

* Mecanismo para fornecer runtime.jsde fora de um pacote- [#7351](https://github.com/NuGet/Home/issues/7351)

**[Lista de todos os problemas corrigidos nesta versão-5,2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**


