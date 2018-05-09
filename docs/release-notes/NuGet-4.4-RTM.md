---
title: Notas de Versão do NuGet 4.4 RTM
description: Notas de versão do NuGet 4.3 RTM incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 3e969274e69de03ca9851d31a627919dcc46bb7d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-44-rtm-release-notes"></a>Notas de Versão do NuGet 4.4 RTM

O [Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) vem com o NuGet 4.4 RTM.

## <a name="known-issues"></a>Problemas conhecidos

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problemas com o .NET Standard 2.0 com o .NET Framework & NuGet 

O .NET Standard e suas ferramentas foram projetados de modo que os projetos destinados ao .NET Framework 4.6.1 podem consumir pacotes do NuGet e projetos destinados ao .NET Standard 2.0 ou anterior. [Este documento](https://github.com/dotnet/standard/issues/481) resume os problemas desse cenário, o plano para lidar com eles e soluções alternativas que você pode implantar com o estado atual das ferramentas.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Ao usar o Console do Gerenciador de Pacotes, talvez a tecla 'Enter' não funcione

#### <a name="issue"></a>Problema

Às vezes, a tecla enter não funciona no Console do Gerenciador de Pacotes. Se isso ocorrer, confira o progresso na correção e forneça informações úteis adicionais sobre as etapas de reprodução. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Solução alternativa

Reinicie o Visual Studio e abra o PMC antes de abrir a solução. Como alternativa, experimente excluir o `project.lock.json` e restaurá-lo novamente.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Você não consegue exibir, adicionar ou atualizar o DotNetCLITools usando o Gerenciador de Pacotes NuGet

#### <a name="issue"></a>Problema

O Gerenciador de Pacotes do NuGet não exibe nem permite a adição/atualização de DotNetCLITools. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Solução alternativa

O DotNetCLIToolReferences deve ser editado manualmente no arquivo de projeto.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Redirecionar a versão da estrutura de destino pode levar a um IntelliSense incompleto

#### <a name="issue"></a>Problema

Redirecionar a versão da estrutura de destino pode levar a um IntelliSense incompleto no Visual Studio. Isso acontece quando você está usando PackageReferences como o formato do gerenciador de pacotes. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Solução alternativa

Faça uma restauração manual.

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>Um pacote em um projeto do .NET Core que contém um assembly com uma assinatura inválida pode disparar um loop de restauração infinito

#### <a name="issue"></a>Problema

Às vezes, quando você usa um pacote que contém um assembly com uma assinatura inválida ou quando a versão do pacote é definida com o ticker 'DateTime', isso faz com que a restauração automática de pacotes seja executada em loop infinito (dotnet/project-system#1457).

#### <a name="workaround"></a>Solução alternativa

Não há nenhuma solução alternativa no momento.

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a>Problemas corrigidos no período de tempo do NuGet 4.4 RTM

[Notas de Versão do NuGet 4.3 RTM](../release-notes/nuget-4.3-RTM.md) – Lista todos os problemas corrigidos no NuGet 4.3 RTM

### <a name="features"></a>Recursos

- Suporte para Lightweight Solution Load em cenários PMC e interface do usuário do PM do NuGet – [#5180](https://github.com/NuGet/Home/issues/5180)

- O destino do pacote msbuild deve ter um gancho público para destinos de usuário em execução antes de si mesmo – [#5143](https://github.com/NuGet/Home/issues/5143)

- Recurso: adicionar a opção dependencyVersion à instalação do nuget – [#1806](https://github.com/NuGet/Home/issues/1806)

- uap10.0.TODO.0 deve ser mapeado para o .NET Standard 2.0 para NuGet – [#5684](https://github.com/NuGet/Home/issues/5684)

- Suporte ao SKU das Ferramentas de Build do Visual Studio com o msbuild /t:restore – [#5562](https://github.com/NuGet/Home/issues/5562)

- Durante a restauração, gera um erro se o suporte do .NET 4.6.1 para o .NET Standard 2.0 for necessário, mas não está instalado – [#5325](https://github.com/NuGet/Home/issues/5325)

- Interface do usuário do cliente de reserva do prefixo da ID do pacote – [#5572](https://github.com/NuGet/Home/issues/5572)

- entregar componentes nuget localizados para dar suporte à localização dotnet.exe – [#4336](https://github.com/NuGet/Home/issues/4336)

### <a name="bugs"></a>Bugs

- Caminhos de projeto com maiúsculas e minúsculas diferentes podem fazer com que a restauração perca PackageReferences – [#5855](https://github.com/NuGet/Home/issues/5855)

- Mover os códigos de erro com números de aviso para o intervalo de erro – [#5824](https://github.com/NuGet/Home/issues/5824)

- Erro enganoso quando a versão do .NET Standard não é conhecida como compatível com a estrutura de destino – [#5818](https://github.com/NuGet/Home/issues/5818)

- Arquivos de teste com licenças confusas – [#5776](https://github.com/NuGet/Home/issues/5776)

- Cabeçalhos de licença ausentes em modelos de teste EndToEnd – [#5774](https://github.com/NuGet/Home/issues/5774)

- A restauração de packages.config mostra erros como NU1000 – [#5743](https://github.com/NuGet/Home/issues/5743)

- A instalação do nuget.exe deve ter DisableParallelProcessing no mono – [#5741](https://github.com/NuGet/Home/issues/5741)

- A instalação do nuget.exe desabilita incorretamente o cache – [#5737](https://github.com/NuGet/Home/issues/5737)

- O VS executa o comando restore para packages.config quando a Restore está desabilitado exibe a mensagem incorreta – [#5718](https://github.com/NuGet/Home/issues/5718)

- VS; Executar o comando restore quando Restore está desabilitado exibe uma mensagem confusa – [#5659](https://github.com/NuGet/Home/issues/5659)

- GetRestoreDotnetCliToolsTask falha quando metadados da versão estão ausentes – [#5716](https://github.com/NuGet/Home/issues/5716)

- dotnet
  - dotnetcore add package pode limpar linhas vazias de um csproj – [#5697](https://github.com/NuGet/Home/issues/5697)

- Nomes de origens das configurações de credencial no NuGet.Config diferenciam maiúsculas de minúsculas – [#5695](https://github.com/NuGet/Home/issues/5695)

- Habilitar GeneratePackageOnBuild excluiu todo o meu histórico de pacotes – [#5676](https://github.com/NuGet/Home/issues/5676)

- A restauração não restaurará pacotes mono.cecil ou semver, mas todos os outros pacotes são restaurados. - [#5649](https://github.com/NuGet/Home/issues/5649)

- Erros e avisos – erro inválido quando uma origem está indisponível.  - [#5644](https://github.com/NuGet/Home/issues/5644)

- [DesignConsistency] O texto de status de instalação do NuGet não aparece corretamente no tema escuro no momento. - [#5642](https://github.com/NuGet/Home/issues/5642)

- Pacotes de atualização nas atualizações/instalações da solução para todos os projetos – [#5508](https://github.com/NuGet/Home/issues/5508)

- dotnet
  - dotnetcore pack demonstra um comportamento diferente entre TargetFramework e TargetFrameworks – [#5281](https://github.com/NuGet/Home/issues/5281)

- DLLs incluídas na pasta Ferramentas geram avisos – [#5020](https://github.com/NuGet/Home/issues/5020)

- O NuGet.ContentModel consome muita memória para operações de cadeia de caracteres – [#4714](https://github.com/NuGet/Home/issues/4714)

- RuntimeEnvironmentHelper.IsLinux retorna true para OSX – [#4648](https://github.com/NuGet/Home/issues/4648)

- 'dotnet pack' coloca nuspec em obj em vez de obj\Debug – [#4644](https://github.com/NuGet/Home/issues/4644)

- Upgrade extremamente lento de pacote do Nuget – [#4534](https://github.com/NuGet/Home/issues/4534)

- CPS fora de sincronia com a Restauração de grandes soluções que ainda não ativou o LSL (lightweight solution restore) – [#4307](https://github.com/NuGet/Home/issues/4307)

- SemVer 2.0 – nuget pack com a versão fornecida ignora os metadados (3.5.0-rtm-1938) – [#3643](https://github.com/NuGet/Home/issues/3643)

- O NuGet.exe (3.+) instala o pacote com número de Versão e o sinalizador ExcludeVersion não atualiza o pacote para a versão mais recente – [#2405](https://github.com/NuGet/Home/issues/2405)

- A restauração do project.json deve avisar quando pacotes de nível superior violam as restrições – [#2358](https://github.com/NuGet/Home/issues/2358)

- -ConfigFile não está definindo a configuração personalizada no comando install – [#1646](https://github.com/NuGet/Home/issues/1646)

- A instalação do nuget.exe não honra a opção '-DisableParallelProcessing' – [#1556](https://github.com/NuGet/Home/issues/1556)

- Origens desabilitadas ainda são usadas pelo DotNet.exe ou msbuild.exe – [#5704](https://github.com/NuGet/Home/issues/5704)

- Corrigir travamentos no cenário LSL – [#5685](https://github.com/NuGet/Home/issues/5685)

### <a name="dcrs"></a>DCRs

- Suporte a TargetFramework na instalação do nuget.exe – [#5736](https://github.com/NuGet/Home/issues/5736)

- Adicionar diferentes cadeias de caracteres UserAgent de tarefa do msbuild (netcore vs msbuild da área de trabalho) – [#5709](https://github.com/NuGet/Home/issues/5709)

- PackagePathResolver.GetPackageDirectoryName deve ser virtual – [#5700](https://github.com/NuGet/Home/issues/5700)

- [DesignConsistency] Mensagem confusa durante a adição de um pacote do NuGet – [#5641](https://github.com/NuGet/Home/issues/5641)

- [Avisos e erros] NoWarn não flui transitivamente por referências P2P – [#5501](https://github.com/NuGet/Home/issues/5501)

- Carga de Solução Leve: núcleo comum para interface do usuário de PM, PMC e IVs* – [#5057](https://github.com/NuGet/Home/issues/5057)

- Lightweight Solution Load: suporte – PMC – [#5053](https://github.com/NuGet/Home/issues/5053)

- Adicionar suporte para o destino do MSBuild pré-restauração que o Visual Studio dispara – [#4781](https://github.com/NuGet/Home/issues/4781)

- Adicione um destino público NuGet.targets que pode ser referenciado usando BeforeTargets- [#4634](https://github.com/NuGet/Home/issues/4634)

- O destino do pacote não pode criar contentFiles com ações de build corretamente – [#4166](https://github.com/NuGet/Home/issues/4166)

- RestoreOperationLogger.Do bloqueia os threads do pool de threads – [#5663](https://github.com/NuGet/Home/issues/5663)

### <a name="docs"></a>Docs

- Documentos para o comando de instalação DependencyVersion e sinalizadores do Framework – [#5858](https://github.com/NuGet/Home/issues/5858)

- Atualização para documentos em avisos e erros do NuGet – [#5857](https://github.com/NuGet/Home/issues/5857)

## <a name="links-to-github-issues-fixed-in-44-rtm"></a>Links para problemas do GitHub corrigidos no RTM 4.4

[Lista de Problemas 1](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[Lista de Problemas 2](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[Lista de Problemas 3](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
