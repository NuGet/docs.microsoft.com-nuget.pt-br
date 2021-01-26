---
title: Notas de versão do 3,5 RC
description: Notas de versão do NuGet 3,5 RC incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 04ec402df5ff993b405bb710abf26e1cdc850703
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780203"
---
# <a name="nuget-35-rc-release-notes"></a>Notas de versão do NuGet 3,5 RC

Notas de versão do [NuGet 3,5-beta2](../release-notes/nuget-3.5-Beta2.md)  |  [NuGet 3,5-notas de versão RTM](../release-notes/nuget-3.5-RTM.md)

a versão 3,5 concentra-se em melhorar a qualidade e o desempenho de clientes NuGet. Além disso, enviamos alguns recursos como suporte para pastas de [fallback](https://github.com/NuGet/Home/issues/2899), suporte a [PackageType](https://github.com/NuGet/Home/issues/2476) no `.nuspec` e mais.

[Lista de problemas](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>Correções de bugs

* Falha na instalação/restauração de um pacote com "o pacote contém vários `.nuspec` arquivos". - [#3231](https://github.com/NuGet/Home/issues/3231)

* o pacote NuGet adiciona `.tt` arquivos à pasta de conteúdo de modo forçado, independentemente do que [#3203](https://github.com/NuGet/Home/issues/3203)

* o NuGet Pack csproj (with `project.json` ) falhará se não houver packoptions e proprietário no arquivo JSON- [#3180](https://github.com/NuGet/Home/issues/3180)

* o pacote NuGet para `project.json` ignora marcas packoptions, como resumo, autores, proprietários etc- [#3161](https://github.com/NuGet/Home/issues/3161)

* o pacote NuGet ignora dependências na saída `.nuspec` para `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* A atualização de vários pacotes com a reversão deixa o projeto em um estado desfeito- [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles em qualquer um não é adicionado para projetos netstandard- [#3118](https://github.com/NuGet/Home/issues/3118)

* Não é possível empacotar a biblioteca com o padrão .net Standard corretamente- [#3108](https://github.com/NuGet/Home/issues/3108)

* Arquivo-> novo projeto-> biblioteca de classes (portátil) falha em VS2015 e Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)

* Erro do NuGet-1.0.0-* não é uma cadeia de caracteres de versão válida- [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package falha ao exibir, mas Install-Package Works- [#3068](https://github.com/NuGet/Home/issues/3068)

* Erro quando "Install-Package jQuery. Validation" em dev15- [#3061](https://github.com/NuGet/Home/issues/3061)

* Quando instalada VS 2015 atualização 3 em um VS que usa o erro do NuGet versão 3.5.0 ocorre- [#3053](https://github.com/NuGet/Home/issues/3053)

* Interface do usuário do Gerenciador de pacotes: não exibe a nova versão após atualizar um pacote- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey na linha de comando de exclusão não é lido/enviado em 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)

* Cadeia de caracteres incorreta: uma versão estável de um pacote não deve ter em uma dependência de pré-lançamento. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Criando exceção NullRef de Get do projeto PCL (net46 e Windows 10). - [#3014](https://github.com/NuGet/Home/issues/3014)

* A atualização do NuGet deve fornecer uma mensagem informativa quando uma versão superior é restrita pela restrição allowedVersions- [#3013](https://github.com/NuGet/Home/issues/3013)

* O plug-in de credencial saiu com o erro-1/erro ao baixar o pacote ao usar provedores de credenciais com várias fontes- [#2885](https://github.com/NuGet/Home/issues/2885)

* pacote NuGet-faltando Newtonsoft.Jsna dependência de pacote- [#2876](https://github.com/NuGet/Home/issues/2876)

* Bug em ExecuteSynchronizedCore no linux/MacOS + mono- [#2860](https://github.com/NuGet/Home/issues/2860)

* O VS não oferece suporte a variáveis de ambiente no repositoryPath (nuget.exe) – [#2763](https://github.com/NuGet/Home/issues/2763)

* Corrigir problemas de acessibilidade- [#2745](https://github.com/NuGet/Home/issues/2745)

* Estruturas portáteis com perfis hifenizados são rejeitadas. - [#2734](https://github.com/NuGet/Home/issues/2734)

* O Gerenciador de pacotes NuGet deve tornar claro que a lista de opções no detalhes dos pacotes não se aplica a `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* Falha na atualização do NuGet 3.3.0 com ' uma restrição adicional... definido em packages.config impede esta operação. ' - [#1816](https://github.com/NuGet/Home/issues/1816)

* A instalação do pacote de uma fonte local que não existe gera um [#1674](https://github.com/NuGet/Home/issues/1674) de mensagens falso

* O filtro "atualizar disponíveis" mostra atualizações que violam a restrição de versão- [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>Melhorias no desempenho

* Desempenho: melhorar a análise da estrutura de destino ContentModel- [#3162](https://github.com/NuGet/Home/issues/3162)

* Desempenho: Evite `runtime.json` a leitura de arquivos para restaurações que não têm RIDs [#3150](https://github.com/NuGet/Home/issues/3150). Em máquinas de CI, a restauração de um aplicativo Web ASP.NET de exemplo foi reduzida de mais de 15 segundos para 3 segundos.

* Desempenho: o console do Gerenciador de pacotes init.ps1 tempo de carregamento [#2956](https://github.com/NuGet/Home/issues/2956). Tempo para abrir o PackageManagerConsole melhorou em alguns casos de 132s para 10s.

* Solucionar problemas de desempenho de resnitidez no NuGet update- [#3044](https://github.com/NuGet/Home/issues/3044): em um projeto de exemplo, tempo necessário para instalar pacotes reduzidos de 140s para 68S.

## <a name="dcrs"></a>DCRs

* O NuGet precisa permitir que os usuários saibam que a atualização/instalação em uma PCL baseada em TFM de dotnet pode causar problemas- [#3138](https://github.com/NuGet/Home/issues/3138)

* Avisar instalação/atualização inadequada para o projeto c/TFM = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* Adicionar suporte a netcoreapp11 e netstandard17- [#2998](https://github.com/NuGet/Home/issues/2998)

* Imprimir NuGet-Warning conteúdo do cabeçalho no console do em nuget.exe- [#2934](https://github.com/NuGet/Home/issues/2934)

* Aproveitar o atributo AssemblyMetadata para `.nuspec` substituições de token- [#2851](https://github.com/NuGet/Home/issues/2851)

* Remover a propriedade locked do arquivo de bloqueio- [#2379](https://github.com/NuGet/Home/issues/2379)

* Os pacotes de símbolo não devem nunca ser usados na instalação ou atualização #2807

## <a name="features"></a>Recursos

* Suporte para pastas de pacotes de fallback- [#2899](https://github.com/NuGet/Home/issues/2899)

* Projete e implemente uma noção de tipo de pacote para oferecer suporte a pacotes de ferramentas- [#2476](https://github.com/NuGet/Home/issues/2476)

* API para obter o caminho para a pasta de pacotes globais- [#2403](https://github.com/NuGet/Home/issues/2403)

* Suporte à atualização de pacotes nativos- [#1291](https://github.com/NuGet/Home/issues/1291)
