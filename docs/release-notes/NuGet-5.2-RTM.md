---
title: Notas de versão do NuGet 5,2 RTM
description: Notas de versão do NuGet 5,2, incluindo novos recursos, correções de bugs e DCRs.
author: karann-msft
ms.author: karann
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: f94bd8ddb8fac8bf47c2826bf5b417595b0efa8b
ms.sourcegitcommit: f291ff91561a6b58c2aec41c624d798e00ce41fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68471179"
---
# <a name="nuget-52-release-notes"></a>Notas de versão do NuGet 5,2

Veículos de distribuição do NuGet:

| Versão do NuGet | Disponível na versão do Visual Studio| Disponível em SDKs do .NET|
|:---|:---|:---|
| [**5.2.0**](https://nuget.org/downloads) | [Visual Studio 2019 versão 16,2](https://visualstudio.microsoft.com/downloads/) | [2.1.80 X](https://dotnet.microsoft.com/download/dotnet-core/2.1) <sup>1</sup>, [2.2.40 X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Instalado com o Visual Studio 2019 com carga de trabalho do .NET Core 

<sup>2</sup> Disponível como uma instalação opcional com o Visual Studio 2019 com carga de trabalho do .NET Core

## <a name="summary-whats-new-in-52"></a>Resumo: O que há de novo no 5,2

* Correção de um bug crítico que causava falhas ocasionais de operação do NuGet devido a problemas de caminho no Linux & Mac- [#7341](https://github.com/NuGet/Home/issues/7341)

* Melhor capacidade de resposta da interface do usuário ao procurar pacotes usando a interface do usuário do Gerenciador de pacotes NuGet no Visual Studio, especialmente perceptível para fontes lentas- [#8039](https://github.com/NuGet/Home/issues/8039)

* Toneladas de correções de confiabilidade para arquivos de bloqueio ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) e plug-in de autenticação ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198),[#7845](https://github.com/NuGet/Home/issues/7845))

### <a name="issues-fixed-in-this-release"></a>Problemas corrigidos nesta versão

**•s**

* Perf Console do Gerenciador de pacotes:  Atraso da interface do usuário ao atualizar o valor selecionado da ComboBox "projeto padrão"- [#8235](https://github.com/NuGet/Home/issues/8235)

* Perf Melhorias de desempenho na interface do usuário do PM- [#8039](https://github.com/NuGet/Home/issues/8039)

* Perf Atraso da interface do usuário ao ler o projeto padrão no PMC- [#6824](https://github.com/NuGet/Home/issues/6824)

* Perf: [vsfeedback] guia de atualização do NuGet congela para um pacote local fonte- [#6470](https://github.com/NuGet/Home/issues/6470)

* Plug  O NuGet aguarda o tempo limite de handshake completo se o plug-in falhar ao ser iniciado ou encerrado no início [#8300](https://github.com/NuGet/Home/issues/8300)

* Plugins: melhorar o diagnóstico da falha de inicialização do plug-in- [#8271](https://github.com/NuGet/Home/issues/8271)

* Plug Problema com a descoberta NuGet. exe de plugins internos- [#8269](https://github.com/NuGet/Home/issues/8269)

* Plugins: o arquivo de cache nunca é de leitura- [#8210](https://github.com/NuGet/Home/issues/8210)

* Plug  "Uma tarefa foi cancelada." erros com o plug-in de autenticação durante a restauração- [#8198](https://github.com/NuGet/Home/issues/8198)

* Cache de plugins não detectável intermitentemente em plataformas Linux- [#7845](https://github.com/NuGet/Home/issues/7845)

* Lockfile: com o ATF, ele tem falso NU1004 devido a uma verificação de igualdade de estrutura de destino inadequada- [#8187](https://github.com/NuGet/Home/issues/8187)

* Lockfile: '--modo bloqueado ' ' sinalizador de restauração não respeitado se o arquivo de bloqueio estiver vazio ou malformado- [#8160](https://github.com/NuGet/Home/issues/8160)

* Lockfile: Não há projetos em minúsculas com nomes de assembly personalizados em pacotes bloquear arquivo- [#8114](https://github.com/NuGet/Home/issues/8114)

* Lockfile: Fazer referência do projeto em minúsculas no arquivo de bloqueio- [#7840](https://github.com/NuGet/Home/issues/7840)

* Restaurar: a instalação de um pacote assinado violado resulta em várias tentativas de instalação com falha (com saída repetida)- [#8175](https://github.com/NuGet/Home/issues/8175)

* VS: as opções de usuário da solução falham ao desserializar após a atualização do NuGet- [#8166](https://github.com/NuGet/Home/issues/8166)

* dotnet-List-Package em um projeto UnitTest retorna um erro- [#8154](https://github.com/NuGet/Home/issues/8154)

* Criar grupo de pacotes NuGet para o instalador do VS – corrigindo alguns problemas de configuração do VSIX- [#8033](https://github.com/NuGet/Home/issues/8033)

* GeneratePackageOnBuild não deve definir nobuild. - [#7801](https://github.com/NuGet/Home/issues/7801)

* A nova opção "-SymbolPackageFormat snupkg" gera um erro quando o arquivo. nuspec contém um elemento de referência de assembly explícito- [#7638](https://github.com/NuGet/Home/issues/7638)

* NuGet.targets(498,5): error : Não foi possível encontrar uma parte do caminho '/tmp/NuGetScratch- [#7341](https://github.com/NuGet/Home/issues/7341)

**DCR:**

* Adicione uma propriedade do MSBuild que indica que PackageDownload tem suporte- [#8106](https://github.com/NuGet/Home/issues/8106)

* FrameworkReference suprimir o fluxo de dependência por meio de FrameworkReference. PrivateAssets- [#7988](https://github.com/NuGet/Home/issues/7988)

* Mecanismo para fornecer tempo de execução. JSON fora de um pacote- [#7351](https://github.com/NuGet/Home/issues/7351)

**[Lista de todos os problemas corrigidos nesta versão-5,2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**


