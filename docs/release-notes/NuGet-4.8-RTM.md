---
title: Notas sobre a versão do NuGet 4.8 RTM
description: Notas sobre a versão do NuGet 4.8.1, incluindo problemas conhecidos, correções de bugs, funcionalidades adicionadas e DCRs.
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: e6f6d9f703dd4761236d166f3772618c100aca09
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813761"
---
# <a name="nuget-48-release-notes"></a>Notas sobre a versão do NuGet 4.8

O [Visual Studio 2017 15.8 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) vem com funcionalidade do NuGet 4.8.


Versões de linha de comando da mesma funcionalidade também estão disponíveis:
* NuGet.exe 4.8 – [nuget.org/downloads](https://nuget.org/downloads)
* DotNet.exe – [SDK do .NET Core 2.1.400](https://www.microsoft.com/net/download/visual-studio-sdks)


## <a name="summary-whats-new-in-480"></a>Resumo: o que há de novo no 4.8.0
* NuGet.exe agora dá suporte a longfilenames no Windows 10 – [#6937](https://github.com/NuGet/Home/issues/6937)
* Plug-ins de autenticação agora funcionam em MsBuild, DotNet.exe, NuGet.exe e Visual Studio, incluindo multiplataforma. A primeira geração de plug-ins de autenticação não tinha suporte no MsBuild, DotNet.exe. Observação: builds de Versão Prévia do VS 2017 15.9 têm um plug-in de autenticação do VSTS incluído. [#6486](https://github.com/NuGet/Home/issues/6486)
* O Resolvedor de SDK do MsBuild agora compila como parte do NuGet e é instalado com as ferramentas do NuGet para VS. Isso evitará que as versões saiam de sincronia. [#6799](https://github.com/NuGet/Home/issues/6799)
* PackageReference agora dá suporte a metadados DevelopmentDependency – [#4125](https://github.com/NuGet/Home/issues/4125)

## <a name="summary-whats-new-in-482"></a>Resumo: o que há de novo no 4.8.2

* Correção de segurança: as permissões em arquivos criados dentro de ~/.NuGet são muito abertas [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="known-issues"></a>Problemas conhecidos
### <a name="installing-signed-packages-on-a-ci-machine-or-in-an-offline-environment-takes-longer-than-usual"></a>Instalar pacotes assinados em um computador de CI ou em um ambiente offline leva mais tempo do que o normal

#### <a name="issue"></a>Problema
Se o computador tiver acesso restrito à Internet (por exemplo, um computador de build em um cenário de CI/CD), a instalação/restauração de um pacote do nuget com sinal resultará um aviso ([NU3028](../reference/errors-and-warnings/nu3028.md)), pois os servidores de revogação não estarão acessíveis. Isso é esperado. No entanto, em alguns casos, isso pode ter consequências não intencionais, como a instalação/restauração do pacote levar mais tempo que o normal.

#### <a name="workaround"></a>Solução alternativa
Atualizar para o Visual Studio 15.8.4 e NuGet.exe 4.8.1, nos quais introduzimos uma variável de ambiente para alternar o modo de verificação de revogação.
Definir a variável de ambiente `NUGET_CERT_REVOCATION_MODE` como `offline` forçará o NuGet a verificar o status de revogação do certificado apenas com relação à lista de certificados revogados armazenado em cache, e o NuGet não tentará acessar servidores de revogação. Quando o modo de verificação de revogação é definido como `offline`, será feito o downgrade do aviso para uma informação.

> [!Warning]
> Não é recomendável colocar o modo de verificação de revogação offline em circunstâncias normais. Isso fará o NuGet ignorar a verificação de revogação online e executar apenas uma verificação de revogação offline em relação à lista de certificados revogados armazenada em cache, que pode estar desatualizada. Isso significa que pacotes em que o certificado de assinatura possa ter sido revogado continuará a ser instalado/restaurado, o que, de outra forma, teria falhado na verificação de revogação e não teria sido instalado.

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>A opção `Migrate packages.config to PackageReference...` não está disponível no menu de contexto de clique com o botão direito do mouse

#### <a name="issue"></a>Problema

Quando um projeto é aberto pela primeira vez, o NuGet pode não ser inicializado até que uma operação do NuGet seja executada. Isso faz com que a opção de migração não apareça no menu de contexto com o botão direito do mouse em `packages.config` ou `References`.

#### <a name="workaround"></a>Solução alternativa

Execute qualquer uma das seguintes ações NuGet:
* Abra a interface do usuário do Gerenciador de Pacotes, clique com o botão direito do mouse em `References` e selecione `Manage NuGet Packages...`
* Abra o Console do Gerenciador de Pacotes em `Tools > NuGet Package Manager`, selecione `Package Manager Console`
* Execute a restauração do NuGet, clique com o botão direito do mouse no nó de solução no Gerenciador de Soluções e selecione `Restore NuGet Packages`
* Compile o projeto, o que também acionará a restauração do NuGet

Agora você deve conseguir ver a opção de migração. Observe que essa opção não tem suporte e não será exibida para os tipos de projeto do ASP.NET e C++.
Observação: isso foi corrigido no VS 2017 15.9 Versão Prévia 3

## <a name="issues-fixed-in-this-release"></a>Problemas corrigidos nesta versão

### <a name="bugs"></a>Bugs
#### <a name="signing"></a>Assinatura
* Assinatura: Como instalar um pacote assinado em um ambiente offline [#7008](https://github.com/NuGet/Home/issues/7008) – corrigido na 4.8.1
* Assinatura: verificação de URL incorreta – [#7174](https://github.com/NuGet/Home/issues/7174)
* Assinatura: verificar a integridade de pacote em RepositorySignatureVerifier quando o pacote for referendado pelo repositório – [#6926](https://github.com/NuGet/Home/issues/6926)
* "Falha na verificação de integridade do pacote." deve ter a ID do pacote na mensagem (e código de erro) – [#6944](https://github.com/NuGet/Home/issues/6944)
* A verificação de pacote assinado do repositório permite os pacotes assinados por outro certificado – [#6884](https://github.com/NuGet/Home/issues/6884)
* NuGet – assinatura – a URL de carimbo de data/hora não pode ser https://? - [#6871](https://github.com/NuGet/Home/issues/6871)
* Não usar NullRef em cenário de pacote NuSpec também melhora as opções – [#6866](https://github.com/NuGet/Home/issues/6866)
* A memória é inválida ao atualizar as informações de signatário ao adicionar o carimbo de data/hora à referenda – [#6840](https://github.com/NuGet/Home/issues/6840)
* Assinatura: remover exceções CTL – [#6794](https://github.com/NuGet/Home/issues/6794)
* Assinatura: contentUrl DEVE ser HTTPS – [#6777](https://github.com/NuGet/Home/issues/6777)
* Assinatura: SignedPackageVerifierSettings.VSClientDefaultPolicy não é usado – [#6601](https://github.com/NuGet/Home/issues/6601)


#### <a name="pack"></a>Pacote
* compilação e restauração não devem ser necessárias ao usar dotnet.exe para empacotar nuspec – [#6866](https://github.com/NuGet/Home/issues/6866)
* Permitir tokens de substituição vazios em NuspecProperties – [#6722](https://github.com/NuGet/Home/issues/6722)
* PackTask gera NullReferenceException quando NuspecProperties é especificado – [#4649](https://github.com/NuGet/Home/issues/4649)

#### <a name="accessibility"></a>Acessibilidade
* [Acessibilidade] Cadeia de caracteres 'Pré-lançamento' sob o botão de pacote é coberta pela sua descrição do pacote na interface do usuário do PM – [#4504](https://github.com/NuGet/Home/issues/4504)
* [Acessibilidade] Botão de configurações e lista suspensa de origem do pacote truncado ao selecionar 'Pacotes Offline do Microsoft Visual Studio' na interface do usuário do PM – [#4502](https://github.com/NuGet/Home/issues/4502)

#### <a name="powershell-management-console-pmc"></a>PMC (Console de Gerenciamento do PowerShell)
* `Update-Package` ignora o intervalo de versão de PackageReference – [#6775](https://github.com/NuGet/Home/issues/6775)
* `Update-Package -reinstall` problema em toda a solução – [#3127](https://github.com/NuGet/Home/issues/3127)
* `Update-Package [packagename] -reinstall` reinstala todos os pacotes, em vez de apenas aquele nomeado – [#737](https://github.com/NuGet/Home/issues/737)
* Pode atualizar para o pacote NuGet não listado no Console do Gerenciador de Pacotes – [#4553](https://github.com/NuGet/Home/issues/4553)

#### <a name="misc"></a>Misc
* Para corrigir `NuGet update self`, NuGet.CommandLine nupkg não deve ser semver2.0 – [#7116](https://github.com/NuGet/Home/issues/7116)
* Melhorar as experiências com falhas de instalação NU1107 – [#7107](https://github.com/NuGet/Home/issues/7107)
* A serialização de GetAuthenticationCredentialRequest está incorreta – [#6983](https://github.com/NuGet/Home/issues/6983)
* AsyncPackage do Visual Studio do NuGet falha ao carregar quando inicializado fora do thread de interface do usuário – [#6976](https://github.com/NuGet/Home/issues/6976)
* A restauração está relatando erros enganosos dizendo que project.json é necessário – [#6959](https://github.com/NuGet/Home/issues/6959)
* Interface do usuário do gerenciador de pacotes: visualizar alterações, botão OK não automaticamente utilizável pelo teclado – [#6893](https://github.com/NuGet/Home/issues/6893)
* RestoreSources são ignoradas para um projeto com referências de p2p – [#6776](https://github.com/NuGet/Home/issues/6776)
* Criar um projeto de teste de unidade usando o modelo .NET Framework abrirá um modelo de projeto mais antigo com packages.config – [#6736](https://github.com/NuGet/Home/issues/6736)
* permitir que a referência de projeto substitua a dependência de pacote – [#6536](https://github.com/NuGet/Home/issues/6536)
* Expor NoDefaultExcludes na tarefa MSBuild – [#6450](https://github.com/NuGet/Home/issues/6450)
* Mensagem de status para "Limpar Todo o Cache do NuGet" pode ser ocultada no redimensionamento da janela – [#5938](https://github.com/NuGet/Home/issues/5938)


[Lista de todos os problemas corrigidos nesta versão](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.8")
