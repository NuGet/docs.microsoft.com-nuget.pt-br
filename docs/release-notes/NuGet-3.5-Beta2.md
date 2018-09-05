---
title: 3.5 notas de versão Beta2
description: Notas de versão do NuGet 3.5 Beta 2, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b47939e2fafc11823c41a849b3c58bbf0800ada
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551985"
---
# <a name="nuget-35-beta2-release-notes"></a>Notas de versão do NuGet 3.5 Beta2

[Notas de versão 3.5 Beta do NuGet](../release-notes/nuget-3.5-Beta.md) | [notas de versão do RC 3.5 do NuGet](../release-notes/nuget-3.5-RC.md)

RTM do NuGet 3.5 Beta 2 foi lançado em 27 de junho de 2016 para o Visual Studio 2013 e nuget.exe

[Log de alterações completo](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[Lista de Problemas](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Correções de Bug

* Mensagem de erro atualizado será falta de suporte para decrpytion de senha no .NET Core para feeds autenticados - [#2942](https://github.com/NuGet/Home/issues/2942)

* Console do Gerenciador de pacotes do Get-Package falhará se o projeto .NET Core está aberto - [#2932](https://github.com/NuGet/Home/issues/2932)

* Corrija a manipulação incorreta de 403 no comando NuGet push [#2910](https://github.com/NuGet/Home/issues/2910)

* Corrigir problemas da desinstalação de pacotes em uma solução associada ao controle de origem do TFS quando disableSourceControlIntegration é definido como true - [#2739](https://github.com/NuGet/Home/issues/2739)

* Correção de atualização de pacote entrem em pacotes de destino não conta - [#2724](https://github.com/NuGet/Home/issues/2724)

* Usar o nível de detalhamento do MSBuild para definir o nível de agente de log para o Gerenciador de pacote do Nuget ações de interface do usuário - [#2705](https://github.com/NuGet/Home/issues/2705)

* Correção de configuração do NuGet é erro inválido em projetos de site - VSIX de VS 2015 (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* Corrigir problemas do pacote do `.csproj` quando os arquivos de conteúdo são incluídos - [#2658](https://github.com/NuGet/Home/issues/2658)

* DefaultPushSource na `NuGetDefaults.Config` (`ProgramData\NuGet`) não funciona – [2653 #](https://github.com/NuGet/Home/issues/2653)

* Corrigir o problema na versão do Nuget 3.4.3 - valor não pode ser nulo na criação do pacote - [#2648](https://github.com/NuGet/Home/issues/2648)

* A restauração usa credenciais armazenadas do NuGet. config para feeds do VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)

* Desempenho - alocações excessivas de correção no código da versão comparsion - [#2632](https://github.com/NuGet/Home/issues/2632)

* Corrigir problemas quando várias instâncias do nuget.exe tenta instalar o mesmo pacote em paralelo, [#2628](https://github.com/NuGet/Home/issues/2628)

* Desempenho - informações de dependência de Cache para operações de multiprojetos - [#2619](https://github.com/NuGet/Home/issues/2619)

* Corrija o problema onde adicionado das configurações de fontes de pacote não foi possível quando a lista de origem está vazia - [#2617](https://github.com/NuGet/Home/issues/2617)

* Corrigir o erro falsas ao tentar instalar o pacote que depende do tempo de design fachadas - [#2594](https://github.com/NuGet/Home/issues/2594)

* Instalação de um pacote no console do PackageManager com a configuração "All" tenta somente primeira fonte - [#2557](https://github.com/NuGet/Home/issues/2557)

* Corrigir problemas com os pacotes que têm arquivos com tempos de gravação no futuro (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)

* Exibir a exceção quando há uma falha de projetos de localização no comando update - [#2418](https://github.com/NuGet/Home/issues/2418)

* Conteúdo do pacote não será restaurado corretamente durante a instalação de um pacote do nuget v3.3 + feed com o argumento - NoCache quando o pacote contiver `.nupkg` arquivos - [#2354](https://github.com/NuGet/Home/issues/2354)

* Corrigir problema com o pacote para instalar (todas as fontes) quando o pacote está ausente da 1 origem - [#2322](https://github.com/NuGet/Home/issues/2322)

* Instalar blocos se uma única fonte falhar autorização - [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` versão do intervalo deve substituir a versão - IncludeReferencedProjects - [#1983](https://github.com/NuGet/Home/issues/1983)

* NuGet 3.3.0 atualização falha com '... uma restrição adicional definido em Packages. config impede que esta operação.' - [#1816](https://github.com/NuGet/Home/issues/1816)

* atualização de NuGet.exe descarta o nome forte do assembly e o atributo particular. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Corrigir problemas com o caminho relativo do arquivo para "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)

* Melhorar a mensagens de falha de resolvedor de Update - [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>Recursos e alterações de comportamento

* NuGet.exe push - o parâmetro de tempo limite não funciona - [#2785](https://github.com/NuGet/Home/issues/2785)

* restauração de NuGet.exe não produza `.props` e `.targets` arquivos para `.nuproj` projetos (regressão v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)

* Precisa de extensibilidade de API para comparar as estruturas de importações - [#2633](https://github.com/NuGet/Home/issues/2633)

* Ocultar as opções da dependência ao usar `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Imprimir o cabeçalho de versão nuget.exe na saída detalhada - [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet deve adicionar suporte para /nativeassets/ /runtimes/ {rid} {txm}- [#2782](https://github.com/NuGet/Home/issues/2782)