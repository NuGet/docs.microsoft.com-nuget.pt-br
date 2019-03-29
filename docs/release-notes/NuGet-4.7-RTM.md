---
title: Notas de versão do NuGet 4.7 RTM
description: Notas de versão do NuGet 4.7.0, incluindo problemas conhecidos, correções de bugs, funcionalidades adicionadas e DCRs.
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: f1397e2f42fd65c3a883c864bd430ba5892c12b2
ms.sourcegitcommit: 74bf831e013470da8b0c1f43193df10bfb1f4fe6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/26/2019
ms.locfileid: "58432515"
---
# <a name="nuget-47-release-notes"></a>Notas sobre a versão do NuGet 4.7

O [Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) vem com o [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe).

## <a name="summary-whats-new-in-470"></a>Resumo: Novidades na versão 4.7.0

* Ampliamos a assinatura de pacote para habilitar [pacotes assinados do repositório](https://github.com/NuGet/Home/wiki/Repository-Signatures)

* Com o Visual Studio versão 15.7, apresentamos a capacidade de [migrar os projetos existentes que usam o formato packages.config para usar o PackageReference](https://docs.microsoft.com/en-us/nuget/reference/migrate-packages-config-to-package-reference).

## <a name="summary-whats-new-in-472"></a>Resumo: Novidades na versão 4.7.2

* Correção de segurança: Permissões em arquivos criados dentro de ~/.nuget são muito abertas [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-473"></a>Resumo: Novidades na versão 4.7.3

* Correção de segurança: Arquivos dentro de NUPKGs podem ter um caminho relativo acima do diretório NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Problemas conhecidos

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

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problemas com o .NET Standard 2.0 com o .NET Framework & NuGet

O .NET Standard e suas ferramentas foram projetados de modo que os projetos destinados ao .NET Framework 4.6.1 podem consumir pacotes do NuGet e projetos destinados ao .NET Standard 2.0 ou anterior. [Este documento](https://github.com/dotnet/standard/issues/481) resume os problemas desse cenário, o plano para lidar com eles e soluções alternativas que você pode implantar com o estado atual das ferramentas.

## <a name="top-issues-fixed-in-this-release"></a>Principais problemas corrigidos nesta versão

### <a name="bugs"></a>Bugs

* O NuGet executa um deadlock no sistema de projeto .Net Core (nova regressão). - [#6733](https://github.com/NuGet/Home/issues/6733)
* Pacote: O PackagePath será construído incorretamente se TfmSpecificPackageFile for usado com caminhos de recurso de curinga – [#6726](https://github.com/NuGet/Home/issues/6726)
* Pacote: o projeto API Web não pode criar o pacote, a menos que ispackable seja definido explicitamente. - [#6156](https://github.com/NuGet/Home/issues/6156)
* A interface de usuário do VS e do PMC leva 30 minutos para ver o novo pacote (o nuget.exe vê imediatamente) – [#6657](https://github.com/NuGet/Home/issues/6657)
* Assinatura:  SignatureUtility.GetCertificateChain(...) não verifica todos os status de cadeia – [#6565](https://github.com/NuGet/Home/issues/6565)
* Autenticação: melhorar a manipulação de GeneralizedTime DER – [#6564](https://github.com/NuGet/Home/issues/6564)
* Assinatura: VS não mostra um erro NU3002 ao instalar um pacote violado – [#6337](https://github.com/NuGet/Home/issues/6337)
* O lockFile.GetLibrary diferencia maiúsculas de minúsculas – [#6500](https://github.com/NuGet/Home/issues/6500)
* Instalar/atualizar o código de restauração e os caminhos de código de restauração não são consistentes – [#3471](https://github.com/NuGet/Home/issues/3471)
* A solução PackageManager versão ComboBox pode selecionar o separador via teclado – [#2606](https://github.com/NuGet/Home/issues/2606)
* Não é possível carregar o índice de serviço para a fonte `https://www.myget.org/F/<id>` ---> System.Net.Http.HttpRequestException: O código de status de resposta não indica êxito: 403 (Proibido) – [#2530](https://github.com/NuGet/Home/issues/2530)

### <a name="dcrs"></a>DCRs

* Emitir o cabeçalho X-NuGet-Session-Id para correlacionar as solicitações [proposta de recurso] – [#5330](https://github.com/NuGet/Home/issues/5330)
* Expor uma forma de espera para executar a operação de restauração em execução no Visual Studio por meio de APIs de IVs. - [#6029](https://github.com/NuGet/Home/issues/6029)
* NuGet.exe – NoServiceEndpoint evitará anexar o sufixo da URL do serviço – [#6586](https://github.com/NuGet/Home/issues/6586)
* adicionar hash de confirmação à versão informativa – [#6492](https://github.com/NuGet/Home/issues/6492)
* Autenticação: habilitar a remoção de assinatura/referenda do repositório – [#6646](https://github.com/NuGet/Home/issues/6646)
* Assinatura:  API para remoção de assinatura/referenda de repositório – [#6589](https://github.com/NuGet/Home/issues/6589)
* Registrar as informações de origem no VS – [#6527](https://github.com/NuGet/Home/issues/6527)
* Filtrar /tools somente no TFM e RID, para que as configurações de XML possam ser colocadas na pasta /tools – [6197 #](https://github.com/NuGet/Home/issues/6197)
* Avisar quando o comando Pack exclui um arquivo que começa com .  - [#3308](https://github.com/NuGet/Home/issues/3308)

[Lista de todos os problemas corrigidos nesta versão](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
