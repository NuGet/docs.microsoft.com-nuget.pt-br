---
title: Notas de Versão do NuGet 4.0 RC
description: Notas de versão do NuGet 4.0 RC incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 44f15e2fc33cca8a3d88af17bf76f1dcc16ca860
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780191"
---
# <a name="nuget-40-rc-release-notes"></a>Notas de Versão do NuGet 4.0 RC

[Notas de Versão do NuGet 3.5 RTM](../release-notes/nuget-3.5-RTM.md)

O [NuGet 4.0 RC para Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) se concentra em adicionar suporte para cenários do .NET Core, abordando os principais comentários dos clientes e melhorando o desempenho de uma variedade de cenários. Esta versão proporciona várias melhorias, como suporte para PackageReference, comandos do NuGet como destinos do MSBuild, restauração do pacote em segundo plano e muito mais.

## <a name="bug-fixes"></a>Correções de bugs

- Alterações de comportamento em `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)

- Restauração do nuget.exe no computador do vs "15" somente falha – [#3834](https://github.com/NuGet/Home/issues/3834)

- O novo projeto do .NETCore deve bloquear o build durante a restauração – [#3780](https://github.com/NuGet/Home/issues/3780)

- Aplicativo Web do ASP.NET Core migrado do VS2015 para VS "15", não é possível restaurar. - [#3773](https://github.com/NuGet/Home/issues/3773)

- [Falha de Teste]O pacote ‘jQuery Validation’ não pode ser desinstalado pela interface do usuário do PM – [#3755](https://github.com/NuGet/Home/issues/3755)

- Quando um pacote é instalado para a UWP `project.json`, os projetos pai também devem ser restaurados – [#3731](https://github.com/NuGet/Home/issues/3731)

- Modificar os destinos do NuGet para registrar as origens de pacote como Alto detalhamento em vez de Normal – [#3719](https://github.com/NuGet/Home/issues/3719)

- dotnet
  - dotnetcore pack3 deve incluir a documentação de XML por padrão – [#3698](https://github.com/NuGet/Home/issues/3698)

- Falha da atualização em lote da interface do usuário quando a origem sem o pacote é a primeira e a origem Todos é selecionada – [#3696](https://github.com/NuGet/Home/issues/3696)

- O comando Nuget pack não inclui todos os arquivos – [#3678](https://github.com/NuGet/Home/issues/3678)

- Problema do OOM – [#3661](https://github.com/NuGet/Home/issues/3661)

- A seção de ProjectFileDependencyGroups do arquivo de ativos deve usar nomes de biblioteca para projetos – [#3611](https://github.com/NuGet/Home/issues/3611)

- “dotnet restore” e diretórios recursivos – [#3517](https://github.com/NuGet/Home/issues/3517)

- Falhas do Restore3 são registradas como avisos em vez de erros – [#3503](https://github.com/NuGet/Home/issues/3503)

- Problema do TFS: “O [file] não pode ser encontrado no seu workspace ou você não tem permissão para acessá-lo.” – [#2805](https://github.com/NuGet/Home/issues/2805)

- Digitar “nuget <packagename>“ na caixa de pesquisa de início rápido do vs mantém o prefixo “nuget” – [#2719](https://github.com/NuGet/Home/issues/2719)

- System.Xml.XmlException: elemento raiz não reconhecido na parte Core Properties. Linha 2, posição 2. - [#2718](https://github.com/NuGet/Home/issues/2718)

- `.nuspec` com &lt; ou &gt; de escape em campos de texto não é mais compilado – [#2651](https://github.com/NuGet/Home/issues/2651)

- A exclusão do nuget.exe não solicita credenciais (está no modo não interativo) – [#2626](https://github.com/NuGet/Home/issues/2626)

- A exclusão do nuget.exe avisa sobre a Chave de API para origens locais, mesmo que isso não faça sentido – [#2625](https://github.com/NuGet/Home/issues/2625)

- Erro de experiência ruim ao instalar o pacote EF -pre – [#2566](https://github.com/NuGet/Home/issues/2566)

- O Visual Studio travou ao tentar alterar a seleção no Gerenciador de Pacotes – [#2551](https://github.com/NuGet/Home/issues/2551)

- dotnet
  - dotnetcore restore realiza pesquisas de ID que diferenciam maiúsculas de minúsculas nos repositórios locais de lista plana quando versões flutuantes são usadas – [#2516](https://github.com/NuGet/Home/issues/2516)

- A exclusão nuget.exe está interrompida para feed V2 ‑ [#2509](https://github.com/NuGet/Home/issues/2509)

- O tempo limite de push do nuget.exe precisa de uma mensagem de erro melhor – [#2503](https://github.com/NuGet/Home/issues/2503)

- A restauração da ferramenta sem as devidas importações falha silenciosamente. - [#2462](https://github.com/NuGet/Home/issues/2462)

- O NuGet solicita as credenciais quando há um feed privado mesmo ao instalar do nuget.org – [#2346](https://github.com/NuGet/Home/issues/2346)

- O pacote do ApplicationInsights 2.0 é listado, mas ainda não existe – [#2317](https://github.com/NuGet/Home/issues/2317)

- UIDelay no VS "15" preview branch 5 – [#3500](https://github.com/NuGet/Home/issues/3500)

- O primeiro evento OnBuild é perdido para a Restauração durante o Build para UWP – [#3489](https://github.com/NuGet/Home/issues/3489)

- O PowerShell5 interrompe a instalação do EntityFramework? - [#3312](https://github.com/NuGet/Home/issues/3312)

- Adicionar origem ao log detalhado (considere para 3.5) – [#3294](https://github.com/NuGet/Home/issues/3294)

- O parâmetro NoCache não é observado na versão de cliente do nuget 3.4 ou superior – [#3074](https://github.com/NuGet/Home/issues/3074)

- Quando um provedor de credenciais falha ao carregar no VS, não interrompa o NuGet – [#2422](https://github.com/NuGet/Home/issues/2422)

## <a name="features"></a>Recursos

- Configurar o IC para executar x86 – [#3868](https://github.com/NuGet/Home/issues/3868)

- Restauração automática 3/3: interface do usuário sem bloqueio – [#3658](https://github.com/NuGet/Home/issues/3658)

- Restauração automática 2/3: restauração em segundo plano na indicação – [#3657](https://github.com/NuGet/Home/issues/3657)

- Restaurar referências de projeto para corresponder ao comportamento de build (repetir) – [#3615](https://github.com/NuGet/Home/issues/3615)

- Suporte a DPL no VS "15" – minbar – [#3614](https://github.com/NuGet/Home/issues/3614)

- Mover o arquivo de configurações para Arquivos de Programas – [#3613](https://github.com/NuGet/Home/issues/3613)

- Objetos e destinos de restauração gerados precisam de suporte para a participação de direcionamento cruzado – [#3496](https://github.com/NuGet/Home/issues/3496)

- Suporte à restauração do NuGet para PackageTargetFallback (importações f.k.a) – [#3494](https://github.com/NuGet/Home/issues/3494)

- Implementação ToolsRef – [#3472](https://github.com/NuGet/Home/issues/3472)

- Restore3 para um RID – [#3465](https://github.com/NuGet/Home/issues/3465)

- Interface do usuário do NuGet para dar suporte à Adição/Remoção/Atualização de PackageRefs – [#3457](https://github.com/NuGet/Home/issues/3457)

- Restauração automática 1/3: implementação da API de indicação por meio de cache das informações de restauração de projeto – [#3456](https://github.com/NuGet/Home/issues/3456)

- [0] Tarefa e destinos de restauração do NuGet – [#2994](https://github.com/NuGet/Home/issues/2994)

- [1] Habilitar a restauração no nível da solução no MSBuild – [#2993](https://github.com/NuGet/Home/issues/2993)

- Suporte à extensibilidade pública do provedor de credenciais no Visual Studio – [#2909](https://github.com/NuGet/Home/issues/2909)

- Restauração de nuget recursiva – [#2533](https://github.com/NuGet/Home/issues/2533)

- Não é possível carregar o Microsoft.TeamFoundation.Client dev15, é necessário atualizar a versão do Microsoft.TeamFoundation.Client para 15.0 para o VS "15" Preview – [#2392](https://github.com/NuGet/Home/issues/2392)

- Não é possível instalar o pacote C++ para um projeto UWP C++ no VS "15" Preview – [#2369](https://github.com/NuGet/Home/issues/2369)

- O Nupkg precisa dar suporte à pasta \buildCrossTargeting\ – e importar `.targets` / `.props` para escopo de “multiplataforma” do MSBuild. - [#3499](https://github.com/NuGet/Home/issues/3499)

- Design de ToolsReference – [#3462](https://github.com/NuGet/Home/issues/3462)

- Corrigir a interface do usuário do NuGet para dar suporte à restauração com PackageReferences em `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)

- Adicionar o botão Limpar cache às configurações do gerenciador de pacotes do VS – [#3289](https://github.com/NuGet/Home/issues/3289)

## <a name="dcrs"></a>DCRs

- A Restauração de solução deve ser bloqueada enquanto restauração automática está em andamento. - [#3797](https://github.com/NuGet/Home/issues/3797)

- A instalação NetCore da interface do usuário do Gerenciador de Pacotes do NuGet é instalada em todos os TFM, em vez daqueles compatíveis com o pacote – [#3721](https://github.com/NuGet/Home/issues/3721)

- A API do indicador de restauração também precisa ser compatível com o DotNetCliToolsReferences. - [#3702](https://github.com/NuGet/Home/issues/3702)

- Marcar nosso VS "15" vsix como um systemcomponent – [#3700](https://github.com/NuGet/Home/issues/3700)

- Migrar do MS.VS.Services.Client de referência para MS.VS.Services.Client.Interactive – [#3670](https://github.com/NuGet/Home/issues/3670)

- $(RestoreLegacyPackagesDirectory) deve ser respeitado no nível de projeto por restauração – [#3618](https://github.com/NuGet/Home/issues/3618)

- A restauração para o projeto com TargetFramework único não deve condicionar os objetos – [#3588](https://github.com/NuGet/Home/issues/3588)

- dotnet
  - dotnetcore restore3 foo.csproj deve seguir as dependências de projectref e restaurá-las também. Como o build. - [#3577](https://github.com/NuGet/Home/issues/3577)

- "type": dependências "platform" são representadas como "type":"package" no arquivo de bloqueio – [#2695](https://github.com/NuGet/Home/issues/2695)

- O Modo detalhado do nuget.exe deve mostrar a URL de download – [#2629](https://github.com/NuGet/Home/issues/2629)

- Mover o xplat do NuGet para o Microsoft.NetCore.App e netcoreapp1.0 – [#2483](https://github.com/NuGet/Home/issues/2483)

- Push – Deve ser possível substituir o servidor de símbolos ao efetuar push da linha de comando – [#2348](https://github.com/NuGet/Home/issues/2348)

- Consolidar o código para localizar caminho de pacotes globais – [#2296](https://github.com/NuGet/Home/issues/2296)

- É necessário um nome melhor que suppressParent – [#2196](https://github.com/NuGet/Home/issues/2196)

- Determinar o nome da dependência `project.json` a ser usado para projetos do MSBuild – [#1914](https://github.com/NuGet/Home/issues/1914)

- Adicionar suporte para SemVer 2.0.0 ao NuGet.Core – [#3383](https://github.com/NuGet/Home/issues/3383)

- Permitir NuPkgs de dependência transitiva com `.targets` disponíveis no MSBuild – [#3342](https://github.com/NuGet/Home/issues/3342)

- Restauração do NuGet da linha de comando é significativamente mais lenta do que o VS – [#3330](https://github.com/NuGet/Home/issues/3330)

- Não diferenciação de maiúsculas e minúsculas na comparação de ID e a versão do pacote – [#2522](https://github.com/NuGet/Home/issues/2522)

- A opção NoCache não funciona para restauração/instalação baseada em `packages.config` (GlobalPackagesFolder) – [#1406](https://github.com/NuGet/Home/issues/1406)

- O recurso FindPackageByIdResource precisa de um contexto de cache padrão e agente – [#1357](https://github.com/NuGet/Home/issues/1357)
