---
title: Notas de versão Beta do NuGet 3.5
description: Notas de versão do NuGet 3.5, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d8df2cb51ddcc03fb3922d9e9def17b39fccc661
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550678"
---
# <a name="nuget-35-release-notes"></a>Notas de versão 3.5 do NuGet

[Notas de versão do RC 3.5 do NuGet](../release-notes/nuget-3.5-RC.md) | [notas de versão do NuGet 4.0 RC](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>Correções de Bug

* Pacote de não usa o MSBuild 14,1 no mono - [#3550](https://github.com/NuGet/Home/issues/3550)

* Guia de atualização não seleciona a versão mais recente disponível para atualizar em vez disso, selecione a versão instalada atual - [#3498](https://github.com/NuGet/Home/issues/3498)

* Corrigir falhas depois de autenticar uma privada v2 feed MyGet e clicando em "Mostrar x mais resultados"- [#3469](https://github.com/NuGet/Home/issues/3469)

* Mensagens de log parecem estar na ordem inversa para a interface do usuário – [3446 #](https://github.com/NuGet/Home/issues/3446)

* gera de restauração do Nuget V3.4.4 - "formato do caminho especificado não é suportado" - [#3442](https://github.com/NuGet/Home/issues/3442)

* NuGet cmdLine 3.6 beta não honra - Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)

* Instalar o NuGet IKVM lento em um projeto grande - [#3428](https://github.com/NuGet/Home/issues/3428)

* NuGet.exe Update - Self mantém em atualizar a próprio - [#3395](https://github.com/NuGet/Home/issues/3395)

* 3.5 instalação/restauração de compartilhamento de UNC tem a regressão de desempenho de 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)

* Erro ao instalar Moq do gerenciamento de pacote da interface do usuário para um projeto de net451 - [#3349](https://github.com/NuGet/Home/issues/3349)

* Guia de instalação no nível da solução não mostra a versão do pacote - [#3339](https://github.com/NuGet/Home/issues/3339)

* xproj `project.json` atualização de aba instalado perde o estado - [#3303](https://github.com/NuGet/Home/issues/3303)

* Pacote do NuGet na `.csproj` ignora o elemento de arquivos vazios no `.nuspec` arquivo - [#3257](https://github.com/NuGet/Home/issues/3257)

* Projetos de site hospedados no IIS não devem causar restauração falhe - [#3235](https://github.com/NuGet/Home/issues/3235)

* As credenciais não são recuperadas do NuGet. config quando o ponto de extremidade v3 redireciona para a v2 - [#3179](https://github.com/NuGet/Home/issues/3179)

* Pacote do NuGet não conseguir resolver o assembly ao recuperar metadados de assembly portátil - [#3128](https://github.com/NuGet/Home/issues/3128)

* O NuGet não é possível localizar `msbuild.exe` em Mono - [#3085](https://github.com/NuGet/Home/issues/3085)

* pacote de NuGet.exe não permite que uma marca de pré-lançamento que começa com números de - [#1743](https://github.com/NuGet/Home/issues/1743)

* Falha de instalação do pacote NuGet em VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)

* allowedVersions filtrar não trabalhar no nível da solução - [#333](https://github.com/NuGet/Home/issues/333)

* Restauração aleatoriamente falhará com um item com a mesma chave já foi adicionada. - [#2646](https://github.com/NuGet/Home/issues/2646)

* Não é possível instalar Nuget.Common em `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)

* Ao usar a interface do usuário para pesquisar uma fonte V2, FindPackagesById é chamado duas vezes para cada ID - [#2517](https://github.com/NuGet/Home/issues/2517)

* Pacotes não podem depender de projetos – [2490 #](https://github.com/NuGet/Home/issues/2490)

* pacote de NuGet.exe - Exclude é documentado mas não tem suporte - [#2284](https://github.com/NuGet/Home/issues/2284)

* Problemas com o erro mensagens quando 'contentFiles' seção de `.nuspec` inválido - [#1686](https://github.com/NuGet/Home/issues/1686)

* Envio por push sempre envia todo pacote duas vezes com origens do pacote - autenticada [#1501](https://github.com/NuGet/Home/issues/1501)

* Nenhuma informação foi fornecida durante a chamada de nuget.exe atualização *.csproj enquanto o projeto não tem um `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)

* `packages.config` Restore não tentará novamente em códigos de status 5xx do código-fonte V2 - [#1217](https://github.com/NuGet/Home/issues/1217)

* Um ponto duplo no arquivo src na `.nuspec` não funciona – [2947 #](https://github.com/NuGet/Home/issues/2947)

* Restauração de CoreCLR precisa ignorar feeds com criptografia - [#2942](https://github.com/NuGet/Home/issues/2942)

* NuGet.exe push tratamento 403 - incorretamente pedir credenciais – [2910 #](https://github.com/NuGet/Home/issues/2910)

* A atualização por meio do Gerenciador de pacotes do NuGet remove as propriedades do `project.json`  -  [2888 #](https://github.com/NuGet/Home/issues/2888)

* Tente carregar "NuGet.TeamFoundationServer14", mas que o nome da DLL alterado para "NuGet.TeamFoundationServer" - NuGet.PackageManagement.VisualStudio [#2857](https://github.com/NuGet/Home/issues/2857)

* Gerenciador de pacotes, interface do usuário não mostra recentemente atualizado versão - [2828 #](https://github.com/NuGet/Home/issues/2828)

* pacote de atualização tentando usar packageid, versão, em vez de package.version - [#2771](https://github.com/NuGet/Home/issues/2771)

* NuGet restauração csproj deve erro se o projeto não está usando o nuget (`packages.config` ou `project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)

* Erro do TFS "[file] não ser encontrado no seu espaço de trabalho, ou você não tem permissão para acessá-lo" durante a atualizar ou desinstalar quando o projeto/solução está associado ao controle do código-fonte do TFS - [#2739](https://github.com/NuGet/Home/issues/2739)

* pacote de atualização não obter dependências para pacotes de destino não - [#2724](https://github.com/NuGet/Home/issues/2724)

* Não é possível definir o nível de verbosidade de logs para ações de interface do usuário de Gerenciador de pacote Nuget - [#2705](https://github.com/NuGet/Home/issues/2705)

* configuração do NuGet é inválida - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* DefaultPushSource na `NuGetDefaults.Config` (`ProgramData\NuGet`) não funciona – [2653 #](https://github.com/NuGet/Home/issues/2653)

* versão do NuGet 3.4.3 - Obtendo o valor não pode ser nulo na compilação do pacote - [#2648](https://github.com/NuGet/Home/issues/2648)

* restauração não está usando credenciais armazenadas do NuGet. config para feeds do VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)

* [dotnet restore] - configfile é relativo ao projeto dir em vez de dir cmd - [#2639](https://github.com/NuGet/Home/issues/2639)

* Alocações excessivas no código da versão comparsion - [#2632](https://github.com/NuGet/Home/issues/2632)

* Várias instâncias do nuget.exe tentando instalar o mesmo pacote em paralelo faz com que uma gravação dupla - [#2628](https://github.com/NuGet/Home/issues/2628)

* Informações de dependência não é armazenado em cache para operações de vários projetos – [2619 #](https://github.com/NuGet/Home/issues/2619)

* Instalar e atualizar os pacotes de download sem verificar a pasta pacotes primeiro - [#2618](https://github.com/NuGet/Home/issues/2618)

* Se a lista de origem do pacote está vazia, não é possível adicionar origem do pacote por meio da interface do usuário (NuGet 3.4. x)- [#2617](https://github.com/NuGet/Home/issues/2617)

* Erro enganoso quando a tentativa de instalar o pacote que depende do tempo de design fachadas - [#2594](https://github.com/NuGet/Home/issues/2594)

* Instalação de um pacote no console do PackageManager com a configuração "All" tenta somente primeira fonte - [#2557](https://github.com/NuGet/Home/issues/2557)

* Versão beta mais recente não descompactar ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)

* VS2015 Falha na inicialização com o NuGet criado automaticamente 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)

* Comando de atualização pode ser um pouco mais detalhado se i pedir que ele seja portanto... - [#2418](https://github.com/NuGet/Home/issues/2418)

* VSIX criado localmente deve ter as mesmas DLLs e arquivos como o build de CI. - [#2401](https://github.com/NuGet/Home/issues/2401)

* Corrigir avisos de downgrade do NuGet em compilação - [#2396](https://github.com/NuGet/Home/issues/2396)

* Falha ao autenticar a origem do pacote (3 vezes) está bloqueada para sempre - [#2362](https://github.com/NuGet/Home/issues/2362)

* Conteúdo do pacote não será restaurado corretamente durante a instalação de um pacote do nuget v3.3 + feed com o argumento - NoCache quando o pacote contiver `.nupkg` arquivos - [#2354](https://github.com/NuGet/Home/issues/2354)

* Falha na instalação do NuGet com todas as fontes de pacote, mas o pacote ausente da 1 fonte, - [#2322](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+*lt; &gt;c__DisplayClass_0 +&lt;&lt;Adicionarreferencia&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)

* Instalar blocos se uma única fonte falhar autorização - [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` versão do intervalo deve substituir a versão - IncludeReferencedProjects - [#1983](https://github.com/NuGet/Home/issues/1983)

* Pacote de atualização muito lenta - "tentando coletar informações de dependências" - [#1909](https://github.com/NuGet/Home/issues/1909)

* Downgrades furtivos NuGet do pacote ao lote Atualizando suas dependências - [#1903](https://github.com/NuGet/Home/issues/1903)

* atualização de NuGet.exe descarta o nome forte do assembly e o atributo particular. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Caminho relativo do arquivo para "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)

* Melhorar a mensagens de falha de resolvedor - [#1373](https://github.com/NuGet/Home/issues/1373)

* pacote de atualização na v3 falha com os pacotes não na fonte especificada - [#1013](https://github.com/NuGet/Home/issues/1013)

* Usando caminhos relativos para origens de pacote é problemático para usar - [#865](https://github.com/NuGet/Home/issues/865)

* Dependência no arquivo NUPKG gerado do projeto, se a dependência indireta já existe com um requisito de versão inferior - ausente [#759](https://github.com/NuGet/Home/issues/759)

* Exclusão de um projeto fecha a janela de interface do usuário correspondente, mas, renomear um projeto não renomeia a janela de interface do usuário. Observe que o PMC escuta a renomeação de projeto e eventos de remover do projeto - [#670](https://github.com/NuGet/Home/issues/670)

* [Carga de trabalho de Web Willow] Criar o Razor v3 WSP trava - [#3241](https://github.com/NuGet/Home/issues/3241)

* Instalação/restauração de um determinado pacote falhar com "O pacote contém vários arquivos nuspec." - [#3231](https://github.com/NuGet/Home/issues/3231)

* Letras minúsculas de IDs de & `packages.config` cenários - [#3209](https://github.com/NuGet/Home/issues/3209)

* [3.5-beta2] Restauração de pacote não conseguir restaurar pacotes "herdados" - [#3208](https://github.com/NuGet/Home/issues/3208)

* pacote NuGet adiciona forçada arquivos. TT para pasta de conteúdo importa - [#3203](https://github.com/NuGet/Home/issues/3203)

* pacote de atualização de aplicativo web ASP.NET gera o aviso relacionado ao arquivo: source - [#3194](https://github.com/NuGet/Home/issues/3194)

* NuGet pack csproj (com `project.json`) falha se não houver nenhum packOptions e o proprietário do arquivo JSON - [#3180](https://github.com/NuGet/Home/issues/3180)

* pacote do NuGet para `project.json` ignora packOptions marcas como resumo, os autores, proprietários etc - [#3161](https://github.com/NuGet/Home/issues/3161)

* NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)

* Pacote do NuGet ignora as dependências na saída `.nuspec` para `project.json`  -  [3145 #](https://github.com/NuGet/Home/issues/3145)

* Atualizar vários pacotes com reversão deixa o projeto em um estado interrompido - [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles em qualquer não são adicionados para projetos de identificadores de netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)

* Não é possível empacotar a biblioteca destinados ao .net Standard corretamente - [#3108](https://github.com/NuGet/Home/issues/3108)

* Arquivo -> Novo projeto -> Falha de projeto de biblioteca de classes (portátil) em VS2015 e Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)

* Erro do NuGet - 1.0.0-* não é uma cadeia de caracteres de versão válida - [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package falha para exibição, mas funciona de Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)

* Erro ao "Install-Package jquery.validation" em dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)

* pacote de NuGet xproj é Padronizando para caminho de destino inválido - [#3060](https://github.com/NuGet/Home/issues/3060)

* Quando instalado VS 2015 atualização 3 em uma que usa o NuGet, ocorre o erro de versão 3.5.0 - VS [#3053](https://github.com/NuGet/Home/issues/3053)

* "Bloqueado pelo Packages. config" `project.json` (build também conhecidas como integrado UWP) projeto - [#3046](https://github.com/NuGet/Home/issues/3046)

* Atualize a cli do dotnet instalada pelo script de compilação para visualização 2-003121, que é a compilação de visualização 2 oficial. - [#3045](https://github.com/NuGet/Home/issues/3045)

* Interface do usuário do Gerenciador de pacotes: não exibe a nova versão depois de atualizar um pacote- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey na linha de comando de exclusão não é leitura/enviada em 3.5.0-Beta - [#3037](https://github.com/NuGet/Home/issues/3037)

* Cadeia de caracteres incorreta: uma versão estável de um pacote não deve ter em uma dependência de pré-lançamento. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Cache OptimizedZipPackage deixa pastas vazias - [#3029](https://github.com/NuGet/Home/issues/3029)

* Criando get de projeto PCL (net46 e windows 10) exceção NullRef. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Atualização do NuGet deve fornecer a mensagem informativa quando uma versão mais recente é restrito pela restrição allowedVersions - [#3013](https://github.com/NuGet/Home/issues/3013)

* Problemas de restauração do NuGet v3 - [#2891](https://github.com/NuGet/Home/issues/2891)

* Plug-in de credencial foi encerrado com erro -1 / Erro ao baixar pacote ao usar provedores de credenciais com várias fontes - [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json` restauração do NuGet provoca a recompilação quando nada alterado - [#2817](https://github.com/NuGet/Home/issues/2817)

* Pacotes de símbolos não devem nunca ser usado na instalação ou atualização - [#2807](https://github.com/NuGet/Home/issues/2807)

* VS não dá suporte a variáveis de ambiente no caminho do repositório (nuget.exe faz) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Rótulo de UIElements sem rótulo na UI do Gerenciador de pacotes para acessibilidade - [#2745](https://github.com/NuGet/Home/issues/2745)

* Estruturas portátil com perfis hifenizadas são rejeitadas. - [#2734](https://github.com/NuGet/Home/issues/2734)

* O Gerenciador de pacotes do NuGet deve esclarecer essa lista de opções em pacotes detalhes não se aplicam a `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* envio/excluir NuGet.exe não usam a chave de API - [#2627](https://github.com/NuGet/Home/issues/2627)

* Remova a propriedade locked do arquivo lock - [#2379](https://github.com/NuGet/Home/issues/2379)

* NuGet 3.3.0 atualização falha com '... uma restrição adicional definido em Packages. config impede que esta operação.' - [#1816](https://github.com/NuGet/Home/issues/1816)

* Ao instalar o pacote de um local de origem que não existe gera uma mensagem de falso - [#1674](https://github.com/NuGet/Home/issues/1674)

* Filtro de "Atualização disponível" mostra as atualizações que violam a restrição de versão - [#1094](https://github.com/NuGet/Home/issues/1094)

* Não é possível atualizar pacotes nativos - [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>Recursos

* Suporte à configuração CopyLocal como falso nas referências adicionadas pelo NuGet - [#329](https://github.com/NuGet/Home/issues/329)

* o suporte para o MSBuild 15 - NuGet.exe [1937 #](https://github.com/NuGet/Home/issues/1937)

* Pacote de suporte.`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* Desabilitar a ação do usuário quando há ações do usuário que está sendo executadas- [#1440](https://github.com/NuGet/Home/issues/1440)

* O NuGet deve adicionar suporte para `runtimes/{rid}/nativeassets/{txm}/`  -  [2782 #](https://github.com/NuGet/Home/issues/2782)

* Adicionar às compatibilidades de framework ausente no NuGet 2.x (que já estão em 3. x) - [#2720](https://github.com/NuGet/Home/issues/2720)

* Suporte para pastas de pacote fallback - [#2899](https://github.com/NuGet/Home/issues/2899)

* Projetar e implementar uma noção de tipo de pacote para dar suporte a pacotes de ferramenta - [#2476](https://github.com/NuGet/Home/issues/2476)

* Adicionar uma API para obter o caminho para a pasta de pacotes globais - [#2403](https://github.com/NuGet/Home/issues/2403)

* Habilitar SemVer 2.0.0 no pacote - [#3356](https://github.com/NuGet/Home/issues/3356)

## <a name="dcrs"></a>DCRs

* NuGet.exe push - o parâmetro de tempo limite não funciona - [#2785](https://github.com/NuGet/Home/issues/2785)

* Texto de descrição do pacote deve ser selecionável - [#1769](https://github.com/NuGet/Home/issues/1769)

* Habilitar nuget.exe produzir `.props` e `.targets` arquivos para `.nuproj` projetos [#2711](https://github.com/NuGet/Home/issues/2711)

* Adicionar a API para comparar as estruturas de importações - de extensibilidade [#2633](https://github.com/NuGet/Home/issues/2633)

* Ocultar as opções da dependência ao usar `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Imprimir o cabeçalho de versão nuget.exe na saída detalhada - [#1887](https://github.com/NuGet/Home/issues/1887)

* O NuGet precisa que os usuários saibam que atualizar/instalar em um tfm dotnet com base em PCL poderá causar problemas - [#3138](https://github.com/NuGet/Home/issues/3138)

* Avisar ruim instalar/atualizar para o projeto c / tfm = "dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)

* Corrigir problemas de desempenho com ReShaper e NuGet para Update - [#3044](https://github.com/NuGet/Home/issues/3044)

* Adicionar suporte netcoreapp11 e netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)

* Atributo AssemblyMetadata aproveite `.nuspec` token substituições - [#2851](https://github.com/NuGet/Home/issues/2851)
