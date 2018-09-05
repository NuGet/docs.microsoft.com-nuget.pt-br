---
title: 3.5 notas de versão de RC
description: Notas de versão do NuGet 3.5 RC incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 52c443ecd79c9108203f5a3c327078ce9e28b95b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548532"
---
# <a name="nuget-35-rc-release-notes"></a>Notas de versão do NuGet 3.5 RC

[Notas de versão do NuGet 3.5-Beta2](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-notas de versão RTM](../release-notes/nuget-3.5-RTM.md)

versão 3.5 tem como foco melhorar a qualidade e desempenho de clientes do NuGet. Além disso, podemos enviar alguns recursos, como suporte para [pastas de Fallback](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) suporte no `.nuspec` e muito mais.

[Lista de Problemas](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>Correções de Bug

* Instalação/restauração de um pacote falha com "pacote contém vários `.nuspec` arquivos." - [#3231](https://github.com/NuGet/Home/issues/3231)

* pacote NuGet adiciona forçada `.tt` arquivos para pasta de conteúdo importa - [#3203](https://github.com/NuGet/Home/issues/3203)

* NuGet pack csproj (com `project.json`) falha se não houver nenhum packOptions e o proprietário do arquivo JSON - [#3180](https://github.com/NuGet/Home/issues/3180)

* pacote do NuGet para `project.json` ignora packOptions marcas como resumo, os autores, proprietários etc - [#3161](https://github.com/NuGet/Home/issues/3161)

* pacote do NuGet ignora as dependências na saída `.nuspec` para `project.json`  -  [3145 #](https://github.com/NuGet/Home/issues/3145)

* Atualizar vários pacotes com reversão deixa o projeto em um estado interrompido - [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles em qualquer não são adicionados para projetos de identificadores de netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)

* Não é possível empacotar a biblioteca destinados ao .net Standard corretamente - [#3108](https://github.com/NuGet/Home/issues/3108)

* Arquivo -> Novo projeto -> Falha de projeto de biblioteca de classes (portátil) em VS2015 e Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)

* Erro do NuGet - 1.0.0-* não é uma cadeia de caracteres de versão válida - [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package falha para exibição, mas funciona de Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)

* Erro ao "Install-Package jquery.validation" em dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)

* Quando instalado VS 2015 atualização 3 em uma que usa o NuGet, ocorre o erro de versão 3.5.0 - VS [#3053](https://github.com/NuGet/Home/issues/3053)

* Interface do usuário do Gerenciador de pacotes: não exibe a nova versão depois de atualizar um pacote- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey na linha de comando de exclusão não é leitura/enviada em 3.5.0-Beta - [#3037](https://github.com/NuGet/Home/issues/3037)

* Cadeia de caracteres incorreta: uma versão estável de um pacote não deve ter em uma dependência de pré-lançamento. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Criando get de projeto PCL (net46 e windows 10) exceção NullRef. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Atualização do NuGet deve fornecer a mensagem informativa quando uma versão mais recente é restrito pela restrição allowedVersions - [#3013](https://github.com/NuGet/Home/issues/3013)

* Plug-in de credencial foi encerrado com erro -1 / Erro ao baixar pacote ao usar provedores de credenciais com várias fontes - [#2885](https://github.com/NuGet/Home/issues/2885)

* pacote do NuGet - dependência de pacote ausente newtonsoft. JSON - [#2876](https://github.com/NuGet/Home/issues/2876)

* Erro no ExecuteSynchronizedCore no Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)

* VS não dá suporte a variáveis de ambiente no caminho do repositório (nuget.exe faz) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Corrigir problemas de acessibilidade - [#2745](https://github.com/NuGet/Home/issues/2745)

* Estruturas portátil com perfis hifenizadas são rejeitadas. - [#2734](https://github.com/NuGet/Home/issues/2734)

* O Gerenciador de pacotes do NuGet deve esclarecer essa lista de opções em pacotes detalhes não se aplicam a `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* NuGet 3.3.0 atualização falha com '... uma restrição adicional definido em Packages. config impede que esta operação.' - [#1816](https://github.com/NuGet/Home/issues/1816)

* Ao instalar o pacote de um local de origem que não existe gera uma mensagem de falso - [#1674](https://github.com/NuGet/Home/issues/1674)

* Filtro de "Atualização veis" mostra as atualizações que violam a restrição de versão - [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>Melhorias de desempenho

* Desempenho: Melhorar o análise de framework de destino de ContentModel - [#3162](https://github.com/NuGet/Home/issues/3162)

* Desempenho: Evitar leitura `runtime.json` arquivos para restaurações que não têm RIDs [#3150](https://github.com/NuGet/Home/issues/3150). Em máquinas de CI, restaure de uma amostra de que aplicativo Web ASP.NET reduzido mais de 15 segundos para 3 segundos.

* Desempenho: Tempo de carregamento Package Manager Console init.ps1 [#2956](https://github.com/NuGet/Home/issues/2956). Tempo para abrir PackageManagerConsole aprimorada em alguns casos de 132s para 10 segundos.

* Solucionar problemas de desempenho do ReSharper na atualização do NuGet - [#3044](https://github.com/NuGet/Home/issues/3044): em um projeto de exemplo, o tempo necessário para instalar pacotes reduzido de 140s para 68s.

## <a name="dcrs"></a>DCRs

* O NuGet precisa que os usuários saibam que atualizar/instalar em um tfm dotnet com base em PCL poderá causar problemas - [#3138](https://github.com/NuGet/Home/issues/3138)

* Avisar ruim instalar/atualizar para o projeto c / tfm = "dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)

* Adicionar suporte netcoreapp11 e netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)

* Imprimir o conteúdo do cabeçalho de aviso do NuGet para o console no nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)

* Atributo AssemblyMetadata aproveite `.nuspec` token substituições - [#2851](https://github.com/NuGet/Home/issues/2851)

* Remova a propriedade locked do arquivo lock - [#2379](https://github.com/NuGet/Home/issues/2379)

* Pacotes de símbolo já não devem ser usados em instalar ou atualizar #2807

## <a name="features"></a>Recursos

* Suporte para pastas de pacote fallback - [#2899](https://github.com/NuGet/Home/issues/2899)

* Projetar e implementar uma noção de tipo de pacote para dar suporte a pacotes de ferramenta - [#2476](https://github.com/NuGet/Home/issues/2476)

* API para obter o caminho para a pasta de pacotes globais - [#2403](https://github.com/NuGet/Home/issues/2403)

* Suporte - atualização de pacotes nativos [#1291](https://github.com/NuGet/Home/issues/1291)
