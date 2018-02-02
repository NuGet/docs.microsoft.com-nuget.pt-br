---
title: "Notas de versão do NuGet 3.5 Beta | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de versão 3.5 do NuGet incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão 3.5 do NuGet, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ee78ceb2ff032c05c0f8ef9a6623b94cc56ee0a9
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-35-release-notes"></a>Notas de versão 3.5 do NuGet

[Notas de versão de RC 3.5 do NuGet](../release-notes/nuget-3.5-RC.md) | [notas de versão de RC do NuGet 4.0](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>Correções de Bug

* Pacote de não usa o MSBuild 14,1 em mono - [#3550](https://github.com/NuGet/Home/issues/3550)

* Guia de atualização não selecione a versão mais recente disponível para atualizar em vez disso, selecione a versão instalada atual - [#3498](https://github.com/NuGet/Home/issues/3498)

* Corrija a falha depois de autenticar uma v2 privada MyGet feed e clicando em "Mostrar x mais resultados"- [#3469](https://github.com/NuGet/Home/issues/3469)

* Mensagens de log parecem estar na ordem inversa para a interface do usuário - [#3446](https://github.com/NuGet/Home/issues/3446)

* gera de restauração do Nuget V3.4.4 - "formato do caminho especificado não é suportado" - [#3442](https://github.com/NuGet/Home/issues/3442)

* NuGet cmdLine 3.6 beta não honra - Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)

* Instalar o NuGet IKVM lenta em grande projeto - [#3428](https://github.com/NuGet/Home/issues/3428)

* NuGet.exe Update - Self mantém na atualização em si - [#3395](https://github.com/NuGet/Home/issues/3395)

* instalação/restaurar 3.5 do compartilhamento UNC tem desempenho regressão de 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)

* Erro ao instalar Moq do gerenciamento de pacote da interface do usuário para um projeto de net451 - [#3349](https://github.com/NuGet/Home/issues/3349)

* Guia de instalação no nível da solução não mostra a versão do pacote - [#3339](https://github.com/NuGet/Home/issues/3339)

* xproj `project.json` atualização instalada guia perde estado - [#3303](https://github.com/NuGet/Home/issues/3303)

* Pacote do NuGet em `.csproj` ignora o elemento de arquivos vazios no `.nuspec` arquivo - [#3257](https://github.com/NuGet/Home/issues/3257)

* Projetos de site hospedados no IIS não devem causar restauração falhe - [#3235](https://github.com/NuGet/Home/issues/3235)

* As credenciais não foram recuperadas do NuGet. config quando o ponto de extremidade v3 redireciona v2 - [#3179](https://github.com/NuGet/Home/issues/3179)

* Pacote do NuGet não conseguir resolver o assembly ao recuperar metadados de assembly portátil - [#3128](https://github.com/NuGet/Home/issues/3128)

* O NuGet não é possível localizar `msbuild.exe` em Mono - [#3085](https://github.com/NuGet/Home/issues/3085)

* pacote de NuGet.exe não permite uma marca de pré-lançamento que começa com números de - [#1743](https://github.com/NuGet/Home/issues/1743)

* Falha de instalação do pacote NuGet em VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)

* Allowedverdions filtrar não funcionar no nível da solução - [#333](https://github.com/NuGet/Home/issues/333)

* A restauração falhará aleatoriamente um item com a mesma chave já foi adicionada. - [#2646](https://github.com/NuGet/Home/issues/2646)

* Não é possível instalar Nuget.Common em `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)

* Ao usar a interface do usuário para pesquisar uma fonte V2, FindPackagesById é chamado duas vezes para cada ID - [#2517](https://github.com/NuGet/Home/issues/2517)

* Pacotes não podem depender de projetos - [#2490](https://github.com/NuGet/Home/issues/2490)

* pacote de NuGet.exe - Exclude é documentado mas não tem suporte - [#2284](https://github.com/NuGet/Home/issues/2284)

* Problemas com o erro mensagens quando a seção 'contentFiles' de `.nuspec` é inválida - [#1686](https://github.com/NuGet/Home/issues/1686)

* Push sempre envia todo pacote duas vezes com origens do pacote - autenticado [#1501](https://github.com/NuGet/Home/issues/1501)

* Nenhuma informação foi fornecida durante a chamada de nuget.exe atualização csproj enquanto o projeto não tem um `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)

* `packages.config`Restore não tenta novamente em códigos de status 5xx do código-fonte V2 - [#1217](https://github.com/NuGet/Home/issues/1217)

* Ponto duplo no arquivo src em `.nuspec` não funciona - [#2947](https://github.com/NuGet/Home/issues/2947)

* Restauração do CoreCLR precisa ignorar feeds com criptografia - [#2942](https://github.com/NuGet/Home/issues/2942)

* NuGet.exe push tratamento 403 - solicitação incorreta de credenciais - [#2910](https://github.com/NuGet/Home/issues/2910)

* NuGet atualização por meio do Gerenciador de pacotes remove propriedades a partir de `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)

* Tente carregar "NuGet.TeamFoundationServer14", mas que o nome da DLL alterado para "NuGet.TeamFoundationServer" - NuGet.PackageManagement.VisualStudio [#2857](https://github.com/NuGet/Home/issues/2857)

* Gerenciador de pacote UI não mostra recentemente atualizado versão - [&#2828;](https://github.com/NuGet/Home/issues/2828)

* pacote de atualização tentando usar packageid, versão, em vez de package.version - [#2771](https://github.com/NuGet/Home/issues/2771)

* NuGet restauração csproj deve erro se o projeto não está usando o nuget (`packages.config` ou `project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)

* Erro do TFS "[arquivo] não ser encontrado no espaço de trabalho, ou você não tem permissão para acessá-lo" durante a atualização ou desinstalação ao projeto/solução está associado ao controle de origem do TFS - [#2739](https://github.com/NuGet/Home/issues/2739)

* pacote de atualização não obter dependências de pacotes de destino não - [#2724](https://github.com/NuGet/Home/issues/2724)

* Não é possível definir o nível de verbosidade de logs para ações de interface do usuário de Gerenciador de pacote Nuget - [#2705](https://github.com/NuGet/Home/issues/2705)

* configuração do NuGet é inválida - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* DefaultPushSource em `NuGetDefaults.Config` (`ProgramData\NuGet`) não funciona - [#2653](https://github.com/NuGet/Home/issues/2653)

* versão do NuGet 3.4.3 - Obtendo o valor não pode ser nulo na compilação do pacote - [#2648](https://github.com/NuGet/Home/issues/2648)

* a restauração não está usando credenciais armazenadas do NuGet. config para feeds do VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)

* [dotnet restauração] – configfile é relativo ao diretório de projeto em vez do dir cmd - [#2639](https://github.com/NuGet/Home/issues/2639)

* Alocações excessivas no código da versão comparsion - [#2632](https://github.com/NuGet/Home/issues/2632)

* Várias instâncias de nuget.exe tentando instalar o mesmo pacote em paralelo faz com que uma gravação dupla - [#2628](https://github.com/NuGet/Home/issues/2628)

* Informações de dependência não é armazenado em cache para operações de multiprojetos - [#2619](https://github.com/NuGet/Home/issues/2619)

* Instalar e atualizar os pacotes de download sem verificar a pasta pacotes primeiro - [#2618](https://github.com/NuGet/Home/issues/2618)

* Se a lista de origem do pacote está vazia, não é possível adicionar origem do pacote por meio da interface do usuário (NuGet 3.4. x)- [#2617](https://github.com/NuGet/Home/issues/2617)

* Enganar erro ao tentar instalar o pacote que depende de tempo de design fachadas - [#2594](https://github.com/NuGet/Home/issues/2594)

* Instalação de um pacote do console PackageManager com a configuração de "All" tenta somente primeira fonte - [#2557](https://github.com/NuGet/Home/issues/2557)

* Versão beta mais recente não descompactar ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)

* VS2015 Falha na inicialização com o NuGet automática interna 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)

* Comando de atualização pode ser um pouco mais detalhado se exigir que ele seja portanto... - i [#2418](https://github.com/NuGet/Home/issues/2418)

* VSIX criado localmente deve ter o mesmo DLLs e arquivos que a compilação de CI. - [#2401](https://github.com/NuGet/Home/issues/2401)

* Corrigir avisos de downgrade do NuGet em compilação - [#2396](https://github.com/NuGet/Home/issues/2396)

* Falha ao autenticar a origem do pacote (3 vezes) está bloqueada para sempre - [#2362](https://github.com/NuGet/Home/issues/2362)

* Conteúdo do pacote não será restaurado corretamente quando instalar um pacote do nuget v3.3 + feed com o argumento - NoCache quando o pacote contiver `.nupkg` arquivos - [#2354](https://github.com/NuGet/Home/issues/2354)

* Ocorre falha na instalação do NuGet com todas as fontes de pacote, mas o pacote ausente da fonte de 1 - [#2322](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+*lt; &gt;c__DisplayClass_0 +&lt;&lt;Adicionarreferencia&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)

* Instalar blocos se uma única fonte não será autorizada - [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec`versão do intervalo deve substituir a versão - IncludeReferencedProjects - [#1983](https://github.com/NuGet/Home/issues/1983)

* Pacote de atualização muito lenta - "tentando coletar informações de dependências" - [#1909](https://github.com/NuGet/Home/issues/1909)

* Downgrades furtivos NuGet do pacote ao lote Atualizando suas dependências - [#1903](https://github.com/NuGet/Home/issues/1903)

* atualização de NuGet.exe descarta o nome forte do assembly e o atributo privado. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Caminho de arquivo relativo para "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)

* Melhorar a mensagens de falha de resolução - [#1373](https://github.com/NuGet/Home/issues/1373)

* Falha do pacote de atualização no v3 com pacotes não na origem especificada - [#1013](https://github.com/NuGet/Home/issues/1013)

* Usar caminhos relativos para fontes de pacote é problemático para usar - [#865](https://github.com/NuGet/Home/issues/865)

* Não tem dependência no arquivo NUPKG gerado do projeto, se a dependência indireta já existe com um requisito de versão inferior - [#759](https://github.com/NuGet/Home/issues/759)

* Excluir um projeto fecha a janela de interface do usuário correspondente, mas, renomear um projeto não renomeia a janela de interface do usuário. Observe que PMC escuta renomeação de projeto e eventos do projeto remove - [#670](https://github.com/NuGet/Home/issues/670)

* [Willow carga de trabalho da Web] Criar Razor v3 WSP trava - [#3241](https://github.com/NuGet/Home/issues/3241)

* Instalação/restauração de um determinado pacote falha com "Pacote contêm vários arquivos nuspec." - [#3231](https://github.com/NuGet/Home/issues/3231)

* Letras minúsculas IDs & `packages.config` cenários - [#3209](https://github.com/NuGet/Home/issues/3209)

* [beta2 3.5] Restauração do pacote não conseguir restaurar os pacotes "herdados" - [#3208](https://github.com/NuGet/Home/issues/3208)

* pacote do NuGet Force adiciona arquivos. TT para pasta de conteúdo, não importando qual - [#3203](https://github.com/NuGet/Home/issues/3203)

* pacote de atualização do aplicativo web ASP.NET gera o aviso relacionado ao arquivo: origem - [#3194](https://github.com/NuGet/Home/issues/3194)

* csproj de pacote do NuGet (com `project.json`) falha se não houver nenhum packOptions e proprietário no arquivo JSON - [#3180](https://github.com/NuGet/Home/issues/3180)

* pacote do NuGet para `project.json` ignora packOptions marcas como resumo, autores e proprietários etc - [#3161](https://github.com/NuGet/Home/issues/3161)

* NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)

* Pacote do NuGet ignora dependências na saída `.nuspec` para `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Atualizar vários pacotes com a reversão deixa o projeto em um estado interrompido - [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles em qualquer não são adicionados para projetos de identificadores de netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)

* Não é possível empacotar biblioteca direcionado ao .net padrão corretamente - [#3108](https://github.com/NuGet/Home/issues/3108)

* Arquivo -> Novo projeto -> Falha de projeto de biblioteca de classes (portátil) em VS2015 e Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)

* Erro do NuGet - 1.0.0-* não é uma cadeia de caracteres de versão válida - [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package falha para exibição, mas funciona Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)

* Erro ao "Install-Package jquery.validation" em dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)

* pacote de NuGet xproj é Padronizando para caminho de destino inválido - [#3060](https://github.com/NuGet/Home/issues/3060)

* Quando instalado VS 2015 atualização 3 em uma relação que usa NuGet versão 3.5.0 erro - [#3053](https://github.com/NuGet/Home/issues/3053)

* "Bloqueado por Packages" `project.json` (UWP, também conhecidos como compilação integrada) projeto - [#3046](https://github.com/NuGet/Home/issues/3046)

* Atualize dotnet cli instalada pelo script de compilação para preview2-003121, que é a compilação preview2 oficial. - [#3045](https://github.com/NuGet/Home/issues/3045)

* Interface de usuário do Gerenciador de pacote: não exibir a nova versão depois de atualizar um pacote- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey na linha de comando de exclusão não é leitura/enviada em 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)

* Cadeia de caracteres incorreta: uma versão estável de um pacote não deve ter em uma dependência de pré-lançamento. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Cache de OptimizedZipPackage deixa as pastas vazias - [#3029](https://github.com/NuGet/Home/issues/3029)

* Criando get de projeto PCL (net46 e windows 10) NullRef exceção. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Atualização do NuGet deve fornecer a mensagem informativa quando uma versão mais recente é restrito por restrição Allowedverdions - [#3013](https://github.com/NuGet/Home/issues/3013)

* Problemas de restauração do NuGet v3 - [#2891](https://github.com/NuGet/Home/issues/2891)

* Plug-in de credencial foi encerrado com erro -1 / erro baixar pacote ao usar os provedores de credenciais com várias fontes - [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json`restauração do NuGet provoca a recompilação quando nada alterado - [#2817](https://github.com/NuGet/Home/issues/2817)

* Pacotes de símbolos nunca não devem ser usada na instalação ou atualização - [#2807](https://github.com/NuGet/Home/issues/2807)

* VS não oferece suporte a variáveis de ambiente no caminho do repositório (nuget.exe faz) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Rótulo de UIElements sem rótulo na UI do Gerenciador de pacotes para acessibilidade - [#2745](https://github.com/NuGet/Home/issues/2745)

* Estruturas portátil com perfis hifenizadas são rejeitadas. - [#2734](https://github.com/NuGet/Home/issues/2734)

* O Gerenciador de pacotes do NuGet deve esclarecer essa lista de opções em pacotes detalhes não se aplicam a `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* envio/excluir NuGet.exe não usam a chave de API - [#2627](https://github.com/NuGet/Home/issues/2627)

* Remova a propriedade locked do arquivo lock - [#2379](https://github.com/NuGet/Home/issues/2379)

* Falha de atualização do NuGet 3.3.0 '... uma restrição adicional definida no Packages impede esta operação.' - [#1816](https://github.com/NuGet/Home/issues/1816)

* Instalando o pacote de um local de origem que não existe gera uma mensagem falso - [#1674](https://github.com/NuGet/Home/issues/1674)

* Filtro de "Atualização disponível" mostra as atualizações que violam a restrição de versão - [#1094](https://github.com/NuGet/Home/issues/1094)

* Não é possível atualizar os pacotes nativos - [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>Recursos

* Suporte à configuração CopyLocal como falso nas referências adicionadas pelo NuGet - [#329](https://github.com/NuGet/Home/issues/329)

* suporte de NuGet.exe para 15 MSBuild - [#1937](https://github.com/NuGet/Home/issues/1937)

* Pacote de suporte.`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* Desabilitar ação do usuário quando há ações do usuário que está sendo executadas- [#1440](https://github.com/NuGet/Home/issues/1440)

* NuGet deve adicionar suporte para `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)

* Adicionar compatibilidades framework ausente no NuGet 2. x (que já estão em 3. x) - [#2720](https://github.com/NuGet/Home/issues/2720)

* Suporte para pastas de pacote de fallback - [#2899](https://github.com/NuGet/Home/issues/2899)

* Projetar e implementar uma noção do tipo de pacote para dar suporte a pacotes de ferramenta - [#2476](https://github.com/NuGet/Home/issues/2476)

* Adicionar uma API para obter o caminho para a pasta de pacotes global - [#2403](https://github.com/NuGet/Home/issues/2403)

* Habilitar SemVer 2.0.0 no pacote - [#3356](https://github.com/NuGet/Home/issues/3356)

## <a name="dcrs"></a>DCRs

* NuGet.exe push - o parâmetro de tempo limite não funciona - [#2785](https://github.com/NuGet/Home/issues/2785)

* Texto de descrição do pacote deve ser selecionável - [#1769](https://github.com/NuGet/Home/issues/1769)

* Habilitar nuget.exe produzir `.props` e `.targets` arquivos de `.nuproj` projetos [#2711](https://github.com/NuGet/Home/issues/2711)

* Adicionar extensibilidade API para comparar estruturas com importações - [#2633](https://github.com/NuGet/Home/issues/2633)

* Ocultar as opções da dependência ao usar `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Impressão do cabeçalho de versão de nuget.exe na saída detalhada - [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet precisa que os usuários saibam que atualizar/instalar em um tfm dotnet com base em PCL pode causar problemas - [#3138](https://github.com/NuGet/Home/issues/3138)

* Avisar incorreta instalar ou atualizar para o projeto com tfm = "dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)

* Corrigir problemas de desempenho com ReShaper e NuGet para Update - [#3044](https://github.com/NuGet/Home/issues/3044)

* Adicionar suporte netcoreapp11 e netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)

* Atributo AssemblyMetadata aproveite `.nuspec` token substituições - [#2851](https://github.com/NuGet/Home/issues/2851)
