---
title: Notas de Versão do NuGet 3.5 RTM
description: Notas de versão do NuGet 3,5 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 158373fb62f57fe6947fb863a1eef8122399959a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776356"
---
# <a name="nuget-35-release-notes"></a>Notas de versão do NuGet 3,5

Notas de versão do [NuGet 3,5-RC](../release-notes/nuget-3.5-RC.md)  |  [Notas de versão do NuGet 4,0 RC](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>Correções de bugs

* O pacote não usa o MSBuild 14,1 em mono- [#3550](https://github.com/NuGet/Home/issues/3550)

* A guia atualizar não seleciona a versão mais recente disponível para atualizar em vez disso, selecione versão instalada atual- [#3498](https://github.com/NuGet/Home/issues/3498)

* Corrija a falha após autenticar um feed MyGet particular V2 e clicando em "mostrar mais resultados"- [#3469](https://github.com/NuGet/Home/issues/3469)

* As mensagens de log parecem estar em ordem inversa para [#3446](https://github.com/NuGet/Home/issues/3446) da interface do usuário

* v 3.4.4-NuGet Restore lança "não há suporte para o formato do caminho fornecido"- [#3442](https://github.com/NuGet/Home/issues/3442)

* NuGet cmdLine 3,6 Beta não respeita-prop Configuration = Release- [#3432](https://github.com/NuGet/Home/issues/3432)

* IKVM do NuGet-instalação lenta em projeto grande- [#3428](https://github.com/NuGet/Home/issues/3428)

* Atualização nuget.exe-automantém a atualização propriamente dita – [#3395](https://github.com/NuGet/Home/issues/3395)

* 3,5 instalar/restaurar do compartilhamento UNC tem regressão de desempenho do 3.4.4- [#3355](https://github.com/NuGet/Home/issues/3355)

* Erro ao instalar o MOQ da interface do usuário de gerenciamento de pacotes para um projeto net451- [#3349](https://github.com/NuGet/Home/issues/3349)

* A guia instalar no nível da solução não mostra a versão do pacote- [#3339](https://github.com/NuGet/Home/issues/3339)

* xproj `project.json` atualização da guia instalada perde o estado [#3303](https://github.com/NuGet/Home/issues/3303)

* O NuGet Pack on `.csproj` ignora o elemento arquivos vazios no `.nuspec` arquivo- [#3257](https://github.com/NuGet/Home/issues/3257)

* Os projetos do site hospedados no IIS não devem causar falha na restauração [#3235](https://github.com/NuGet/Home/issues/3235)

* As credenciais não são recuperadas de Nuget.Config quando o ponto de extremidade v3 redireciona para v2- [#3179](https://github.com/NuGet/Home/issues/3179)

* O pacote NuGet não resolve o assembly ao recuperar metadados do assembly portátil- [#3128](https://github.com/NuGet/Home/issues/3128)

* O NuGet não pode ser encontrado `msbuild.exe` em mono- [#3085](https://github.com/NuGet/Home/issues/3085)

* O pacote de nuget.exe não permite uma marca de pré-lançamento que começa com números- [#1743](https://github.com/NuGet/Home/issues/1743)

* a instalação do pacote NuGet falha em VS2015E- [#1298](https://github.com/NuGet/Home/issues/1298)

* o filtro allowedVersions não está funcionando no nível da solução- [#333](https://github.com/NuGet/Home/issues/333)

* A restauração falha aleatoriamente com um item com a mesma chave já foi adicionado. - [#2646](https://github.com/NuGet/Home/issues/2646)

* Não é possível instalar NuGet. Common no `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)

* Ao usar a interface do usuário para pesquisar uma fonte v2, FindPackagesById é chamado duas vezes para cada ID- [#2517](https://github.com/NuGet/Home/issues/2517)

* Os pacotes não podem depender de projetos- [#2490](https://github.com/NuGet/Home/issues/2490)

* nuget.exe Pack – excluir está documentado, mas sem suporte- [#2284](https://github.com/NuGet/Home/issues/2284)

* Problemas com mensagens de erro quando a seção ' contentFiles ' de `.nuspec` é inválida- [#1686](https://github.com/NuGet/Home/issues/1686)

* O push sempre envia o pacote inteiro duas vezes com fontes de pacote autenticadas- [#1501](https://github.com/NuGet/Home/issues/1501)

* Nenhuma informação foi fornecida ao chamar nuget.exe Update *. csproj enquanto o projeto não tem um `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)

* `packages.config` Restore não tenta novamente em códigos de status 5xx de fontes v2- [#1217](https://github.com/NuGet/Home/issues/1217)

* O ponto duplo na src do arquivo `.nuspec` não funciona – [#2947](https://github.com/NuGet/Home/issues/2947)

* A restauração do CoreCLR precisa ignorar feeds com criptografia- [#2942](https://github.com/NuGet/Home/issues/2942)

* Manipulação de nuget.exe Push 403-solicitando incorretamente credenciais- [#2910](https://github.com/NuGet/Home/issues/2910)

* A atualização do NuGet por meio do Gerenciador de pacotes remove as propriedades do `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)

* NuGet. PackageManagement. VisualStudio tenta carregar "NuGet. TeamFoundationServer14", mas esse nome de DLL foi alterado para "NuGet. TeamFoundationServer"- [#2857](https://github.com/NuGet/Home/issues/2857)

* A interface do usuário do Gerenciador de pacotes não mostra a versão atualizada recentemente [#2828](https://github.com/NuGet/Home/issues/2828)

* Update-Package tentando usar PackageID, versão em vez de Package. Version- [#2771](https://github.com/NuGet/Home/issues/2771)

* o csproj de restauração do NuGet deve ser um erro se o projeto não estiver usando NuGet ( `packages.config` ou `project.json` )- [#2766](https://github.com/NuGet/Home/issues/2766)

* O erro do TFS "[File] não foi encontrado no seu espaço de trabalho ou você não tem permissão para acessá-lo" durante a atualização ou desinstalação quando a solução/projeto está associada ao controle do código-fonte do TFS- [#2739](https://github.com/NuGet/Home/issues/2739)

* o pacote de atualização não obtém dependências para pacotes que não são de destino- [#2724](https://github.com/NuGet/Home/issues/2724)

* Não há como definir o nível de detalhamento de logs para ações de interface do usuário do Gerenciador de pacotes NuGet- [#2705](https://github.com/NuGet/Home/issues/2705)

* a configuração do NuGet é inválida-VS 2015 VSIX (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)

* Defaultpushname in `NuGetDefaults.Config` ( `ProgramData\NuGet` ) não funciona – [#2653](https://github.com/NuGet/Home/issues/2653)

* versão 3.4.3 do NuGet-obter o valor não pode ser nulo no Build do pacote- [#2648](https://github.com/NuGet/Home/issues/2648)

* a restauração não está usando credenciais armazenadas do Nuget.Config para feeds do VSTS- [#2647](https://github.com/NuGet/Home/issues/2647)

* [dotnet restore]--ConfigFile é relativo ao diretório do projeto em vez da pasta cmd- [#2639](https://github.com/NuGet/Home/issues/2639)

* Alocações excessivas no código de análise da versão- [#2632](https://github.com/NuGet/Home/issues/2632)

* Várias instâncias do nuget.exe tentando instalar o mesmo pacote em paralelo causam uma [#2628](https://github.com/NuGet/Home/issues/2628) de gravação dupla

* As informações de dependência não são armazenadas em cache para operações de vários projetos- [#2619](https://github.com/NuGet/Home/issues/2619)

* Instalar e atualizar pacotes de download sem verificar a pasta de pacotes primeiro- [#2618](https://github.com/NuGet/Home/issues/2618)

* Se a lista de origem do pacote estiver vazia, não será possível adicionar a origem do pacote via interface do usuário (NuGet 3.4. x)- [#2617](https://github.com/NuGet/Home/issues/2617)

* Erro enganoso ao tentar instalar o pacote que depende do tempo de design fachadas- [#2594](https://github.com/NuGet/Home/issues/2594)

* Instalar um pacote do console do PackageManager com a configuração "All" tenta somente a primeira fonte- [#2557](https://github.com/NuGet/Home/issues/2557)

* Beta mais recente não descompactar ModernHttpClient- [#2518](https://github.com/NuGet/Home/issues/2518)

* VS2015 falha na inicialização com 3.4.1 de NuGet autocompilado- [#2419](https://github.com/NuGet/Home/issues/2419)

* O comando Update pode ser um pouco mais detalhado se eu fizer isso...- [#2418](https://github.com/NuGet/Home/issues/2418)

* O VSIX criado localmente deve ter os mesmos arquivos e DLLs que o CI Build. - [#2401](https://github.com/NuGet/Home/issues/2401)

* Corrigir avisos de downgrade do NuGet no [#2396](https://github.com/NuGet/Home/issues/2396) de compilação

* Falha ao autenticar a origem do pacote (3 vezes) é bloqueada para sempre [#2362](https://github.com/NuGet/Home/issues/2362)

* O conteúdo do pacote não é restaurado corretamente ao instalar um pacote de um feed do NuGet v 3.3 + com o argumento-NoCache quando o pacote contém `.nupkg` arquivos- [#2354](https://github.com/NuGet/Home/issues/2354)

* Instalação do NuGet com todas as origens do pacote, mas o pacote ausente da fonte 1, falha- [#2322](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet. PackageManagement. VisualStudio. VSMSBuildNuGetProjectSystem + * lt; &gt; c__DisplayClass_0 + &lt; &lt; addreference &gt; B__ &gt; d. MoveNext- [#2285](https://github.com/NuGet/Home/issues/2285)

* Instalar blocos se uma única fonte falhar na autorização- [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` o intervalo de versão deve substituir-IncludeReferencedProjects versão- [#1983](https://github.com/NuGet/Home/issues/1983)

* Update-Package super lento-"tentando coletar informações sobre dependências"- [#1909](https://github.com/NuGet/Home/issues/1909)

* Pacote de downgrades do NuGet stealth ao atualizar o lote de suas dependências- [#1903](https://github.com/NuGet/Home/issues/1903)

* nuget.exe atualização descarta o nome forte do assembly e o atributo privado. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Caminho de arquivo relativo para "defaultpushexception"- [#1746](https://github.com/NuGet/Home/issues/1746)

* Melhorar mensagens de falha do resolvedor- [#1373](https://github.com/NuGet/Home/issues/1373)

* Update-Package in v3 falha com pacotes que não estão na fonte especificada- [#1013](https://github.com/NuGet/Home/issues/1013)

* O uso de caminhos relativos para origens de pacote é problemático para uso- [#865](https://github.com/NuGet/Home/issues/865)

* Dependência ausente no NUPKG-File gerado do projeto se a dependência indireta já existe com um requisito de versão inferior- [#759](https://github.com/NuGet/Home/issues/759)

* Excluir um projeto fecha a janela da interface do usuário correspondente, mas a renomeação de um projeto não renomeia a janela da interface do usuário. Observe que o PMC escuta os eventos renomear projeto e remover projeto- [#670](https://github.com/NuGet/Home/issues/670)

* [Carga de trabalho da Web do Willow] Criação de travas de WSP do Razor v3- [#3241](https://github.com/NuGet/Home/issues/3241)

* A instalação/restauração de um pacote específico falha com "o pacote contém vários arquivos nuspec". - [#3231](https://github.com/NuGet/Home/issues/3231)

* IDs em minúsculas & `packages.config` cenários- [#3209](https://github.com/NuGet/Home/issues/3209)

* [3,5-beta2] Falha na restauração do pacote ao restaurar os pacotes "herdados"- [#3208](https://github.com/NuGet/Home/issues/3208)

* o pacote NuGet adiciona arquivos. TT de maneira forçada à pasta de conteúdo, independentemente do que [#3203](https://github.com/NuGet/Home/issues/3203)

* o pacote de atualização do aplicativo Web ASP.NET gera um aviso relacionado ao arquivo: Source- [#3194](https://github.com/NuGet/Home/issues/3194)

* o NuGet Pack csproj (with `project.json` ) falhará se não houver packoptions e proprietário no arquivo JSON- [#3180](https://github.com/NuGet/Home/issues/3180)

* o pacote NuGet para `project.json` ignora marcas packoptions, como resumo, autores, proprietários etc- [#3161](https://github.com/NuGet/Home/issues/3161)

* NullReferenceException via NuGet. Packaging. PhysicalPackageFile. GetStream- [#3160](https://github.com/NuGet/Home/issues/3160)

* O pacote NuGet ignora dependências na saída `.nuspec` para `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* A atualização de vários pacotes com a reversão deixa o projeto em um estado desfeito- [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles em qualquer um não é adicionado para projetos netstandard- [#3118](https://github.com/NuGet/Home/issues/3118)

* Não é possível empacotar a biblioteca com o padrão .net Standard corretamente- [#3108](https://github.com/NuGet/Home/issues/3108)

* Arquivo-> novo projeto-> biblioteca de classes (portátil) falha em VS2015 e Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)

* erro do nuGet-1.0.0-* não é uma cadeia de caracteres de versão válida- [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package falha ao exibir, mas Install-Package Works- [#3068](https://github.com/NuGet/Home/issues/3068)

* Erro quando "Install-Package jQuery. Validation" em dev15- [#3061](https://github.com/NuGet/Home/issues/3061)

* o pacote NuGet de xproj está padronizando para o caminho de destino inválido- [#3060](https://github.com/NuGet/Home/issues/3060)

* Quando instalada VS 2015 atualização 3 em um VS que usa o erro do NuGet versão 3.5.0 ocorre- [#3053](https://github.com/NuGet/Home/issues/3053)

* "Bloqueado por packages.config" no `project.json` projeto (UWP, a. k. a Build Integrated)- [#3046](https://github.com/NuGet/Home/issues/3046)

* Atualize a CLI do dotnet instalada pelo script de compilação para Preview2-003121, que é a compilação oficial do Preview2. - [#3045](https://github.com/NuGet/Home/issues/3045)

* Interface do usuário do Gerenciador de pacotes: não exibe a nova versão após atualizar um pacote- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey na linha de comando de exclusão não é lido/enviado em 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)

* Cadeia de caracteres incorreta: uma versão estável de um pacote não deve ter em uma dependência de pré-lançamento. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Cache OptimizedZipPackage deixa pastas vazias – [#3029](https://github.com/NuGet/Home/issues/3029)

* Criando exceção NullRef de Get do projeto PCL (net46 e Windows 10). - [#3014](https://github.com/NuGet/Home/issues/3014)

* A atualização do NuGet deve fornecer uma mensagem informativa quando uma versão superior é restrita pela restrição allowedVersions- [#3013](https://github.com/NuGet/Home/issues/3013)

* Problemas de restauração do NuGet v3- [#2891](https://github.com/NuGet/Home/issues/2891)

* O plug-in de credencial saiu com o erro-1/erro ao baixar o pacote ao usar provedores de credenciais com várias fontes- [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json` a restauração do NuGet causa recompilação quando nada é alterado- [#2817](https://github.com/NuGet/Home/issues/2817)

* Os pacotes de símbolos não devem nunca ser usados na instalação ou atualização- [#2807](https://github.com/NuGet/Home/issues/2807)

* O VS não oferece suporte a variáveis de ambiente no repositoryPath (nuget.exe) – [#2763](https://github.com/NuGet/Home/issues/2763)

* Rotule os UIElements não rotulados na interface do usuário do Gerenciador de pacotes para acessibilidade- [#2745](https://github.com/NuGet/Home/issues/2745)

* Estruturas portáteis com perfis hifenizados são rejeitadas. - [#2734](https://github.com/NuGet/Home/issues/2734)

* O Gerenciador de pacotes NuGet deve tornar claro que a lista de opções no detalhes dos pacotes não se aplica a `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* nuget.exe Push/excluir não usará a chave de API- [#2627](https://github.com/NuGet/Home/issues/2627)

* Remover a propriedade locked do arquivo de bloqueio- [#2379](https://github.com/NuGet/Home/issues/2379)

* Falha na atualização do NuGet 3.3.0 com ' uma restrição adicional... definido em packages.config impede esta operação. ' - [#1816](https://github.com/NuGet/Home/issues/1816)

* A instalação do pacote de uma fonte local que não existe gera um [#1674](https://github.com/NuGet/Home/issues/1674) de mensagens falso

* O filtro "atualização disponível" mostra atualizações que violam a restrição de versão- [#1094](https://github.com/NuGet/Home/issues/1094)

* Não é possível atualizar os pacotes nativos- [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>Recursos

* Suporte à configuração CopyLocal como false nas referências adicionadas pelo NuGet- [#329](https://github.com/NuGet/Home/issues/329)

* Suporte de nuget.exe para MSBuild 15- [#1937](https://github.com/NuGet/Home/issues/1937)

* Suporte do pacote para.`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* Desabilitar a ação do usuário quando houver ações do usuário sendo executadas- [#1440](https://github.com/NuGet/Home/issues/1440)

* O NuGet deve adicionar suporte para `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)

* Adicionar compatibilidades de estrutura ausentes no NuGet 2. x (que já estão em 3. x)- [#2720](https://github.com/NuGet/Home/issues/2720)

* Suporte para pastas de pacotes de fallback- [#2899](https://github.com/NuGet/Home/issues/2899)

* Projete e implemente uma noção de tipo de pacote para oferecer suporte a pacotes de ferramentas- [#2476](https://github.com/NuGet/Home/issues/2476)

* Adicione uma API para obter o caminho para a pasta de pacotes globais- [#2403](https://github.com/NuGet/Home/issues/2403)

* Habilitar SemVer 2.0.0 no [#3356](https://github.com/NuGet/Home/issues/3356) Pack

## <a name="dcrs"></a>DCRs

* nuget.exe parâmetro Push-timeout não funciona – [#2785](https://github.com/NuGet/Home/issues/2785)

* O texto de descrição do pacote deve ser selecionável- [#1769](https://github.com/NuGet/Home/issues/1769)

* Habilitar nuget.exe para produzir `.props` e `.targets` arquivos para `.nuproj` projetos [#2711](https://github.com/NuGet/Home/issues/2711)

* Adicionar API de extensibilidade para comparar estruturas com importações- [#2633](https://github.com/NuGet/Home/issues/2633)

* Ocultar opções de dependência ao usar `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Imprimir nuget.exe cabeçalho da versão na saída detalhada- [#1887](https://github.com/NuGet/Home/issues/1887)

* O NuGet precisa permitir que os usuários saibam que a atualização/instalação em uma PCL baseada em TFM de dotnet pode causar problemas- [#3138](https://github.com/NuGet/Home/issues/3138)

* Avisar instalação/atualização inadequada para o projeto c/TFM = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* Corrigir problemas de desempenho com remodelador e NuGet para update- [#3044](https://github.com/NuGet/Home/issues/3044)

* Adicionar suporte a netcoreapp11 e netstandard17- [#2998](https://github.com/NuGet/Home/issues/2998)

* Aproveitar o atributo AssemblyMetadata para `.nuspec` substituições de token- [#2851](https://github.com/NuGet/Home/issues/2851)
