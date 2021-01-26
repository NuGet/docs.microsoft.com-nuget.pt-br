---
title: Notas de versão do 3,5 beta2
description: Notas de versão do NuGet 3,5 Beta 2, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2aa92d4ef97acb2b4b70388cd4d580e7094aea45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776389"
---
# <a name="nuget-35-beta2-release-notes"></a>Notas de versão do NuGet 3,5 beta2

Notas de versão do [NuGet 3,5-Beta](../release-notes/nuget-3.5-Beta.md)  |  [Notas de versão do NuGet 3,5-RC](../release-notes/nuget-3.5-RC.md)

O NuGet 3,5 Beta 2 RTM foi lançado em 27 de junho de 2016 para Visual Studio 2013 e nuget.exe

[Changelog completo](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[Lista de problemas](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Correções de bugs

* Mensagem de erro atualizada para falta de suporte para a senha decrpytion no .NET Core para feeds autenticados- [#2942](https://github.com/NuGet/Home/issues/2942)

* O console do Gerenciador de pacotes Get-Package falhará se o projeto do .NET Core estiver aberto- [#2932](https://github.com/NuGet/Home/issues/2932)

* Corrija o tratamento incorreto de 403 no comando de push do NuGet [#2910](https://github.com/NuGet/Home/issues/2910)

* Corrija problemas na desinstalação de pacotes em uma solução associada ao controle do código-fonte do TFS quando disableSourceControlIntegration está definido como true- [#2739](https://github.com/NuGet/Home/issues/2739)

* Corrija a atualização do pacote para levar em conta pacotes de não-destino- [#2724](https://github.com/NuGet/Home/issues/2724)

* Use o nível de detalhes do MSBuild para definir o nível de agente para ações de interface do usuário do Gerenciador de pacotes NuGet- [#2705](https://github.com/NuGet/Home/issues/2705)

* Corrigir a configuração do NuGet é um erro inválido nos projetos do site – VSIX do VS 2015 (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)

* Problemas de correção de pacote `.csproj` quando arquivos de conteúdo são incluídos- [#2658](https://github.com/NuGet/Home/issues/2658)

* Defaultpushname in `NuGetDefaults.Config` ( `ProgramData\NuGet` ) não funciona – [#2653](https://github.com/NuGet/Home/issues/2653)

* Correção do problema na versão do NuGet 3.4.3-o valor não pode ser nulo na criação do pacote- [#2648](https://github.com/NuGet/Home/issues/2648)

* Restore usa credenciais armazenadas do Nuget.Config para feeds do VSTS- [#2647](https://github.com/NuGet/Home/issues/2647)

* Desempenho-corrigir alocações excessivas no código de análise da versão- [#2632](https://github.com/NuGet/Home/issues/2632)

* Corrigir problemas quando várias instâncias do nuget.exe tentam instalar o mesmo pacote em paralelo- [#2628](https://github.com/NuGet/Home/issues/2628)

* Informações de dependência de cache de desempenho para operações de vários projetos- [#2619](https://github.com/NuGet/Home/issues/2619)

* Correção do problema em que as origens do pacote não foi possível ser adicionadas das configurações quando a lista de origem está vazia- [#2617](https://github.com/NuGet/Home/issues/2617)

* Corrigir erro enganoso ao tentar instalar o pacote que depende do tempo de design fachadas- [#2594](https://github.com/NuGet/Home/issues/2594)

* Instalar um pacote do console do PackageManager com a configuração "All" tenta somente a primeira fonte- [#2557](https://github.com/NuGet/Home/issues/2557)

* Corrigir problemas com pacotes que têm arquivos com tempos de gravação no futuro (mono)- [#2518](https://github.com/NuGet/Home/issues/2518)

* Exibir exceção quando houver uma falha ao localizar projetos no comando update- [#2418](https://github.com/NuGet/Home/issues/2418)

* O conteúdo do pacote não é restaurado corretamente ao instalar um pacote de um feed do NuGet v 3.3 + com o argumento-NoCache quando o pacote contém `.nupkg` arquivos- [#2354](https://github.com/NuGet/Home/issues/2354)

* Correção do problema com a instalação do pacote (todas as fontes) quando o pacote está faltando em 1 fonte- [#2322](https://github.com/NuGet/Home/issues/2322)

* Instalar blocos se uma única fonte falhar na autorização- [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` o intervalo de versão deve substituir-IncludeReferencedProjects versão- [#1983](https://github.com/NuGet/Home/issues/1983)

* Falha na atualização do NuGet 3.3.0 com ' uma restrição adicional... definido em packages.config impede esta operação. ' - [#1816](https://github.com/NuGet/Home/issues/1816)

* nuget.exe atualização descarta o nome forte do assembly e o atributo privado. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Corrigir problemas com o caminho de arquivo relativo para "defaultpushexception"- [#1746](https://github.com/NuGet/Home/issues/1746)

* Melhorar mensagens de falha do resolvedor de atualizações- [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>Recursos e alterações de comportamento

* nuget.exe parâmetro Push-timeout não funciona – [#2785](https://github.com/NuGet/Home/issues/2785)

* nuget.exe Restore não produz `.props` e `.targets` arquivos para `.nuproj` projetos (regressão em v 3.4.3.855) – [#2711](https://github.com/NuGet/Home/issues/2711)

* Necessidade de API de extensibilidade para comparar estruturas com importações- [#2633](https://github.com/NuGet/Home/issues/2633)

* Ocultar opções de dependência ao usar `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Imprimir nuget.exe cabeçalho da versão na saída detalhada- [#1887](https://github.com/NuGet/Home/issues/1887)

* O NuGet deve adicionar suporte para/runtimes/{RID}/nativeassets/{TXM}/- [#2782](https://github.com/NuGet/Home/issues/2782)