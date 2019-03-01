---
title: Notas de versão prévia 5.0 do NuGet
description: Notas de versão para as visualizações do NuGet 5.0 incluindo problemas conhecidos, correções de bug, novos recursos e DCRs.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 57b66b347ac47a3d05907a4bb237002de8981ecc
ms.sourcegitcommit: 85bf94e0efcfcee1f914650bdc142309ef3e06d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57196194"
---
# <a name="nuget-50-preview-release-notes"></a>Notas de versão do NuGet versão prévia 5.0

## <a name="nuget-50-preview-releases"></a>Versões de visualização 5.0 do NuGet

* 27 de fevereiro de 2010 - [NuGet 5.0 visualização 4](#summary-whats-new-in-50-preview-4)
* 13 de fevereiro de 2019 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)
* 23 de janeiro de 2019 - [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)

## <a name="summary-whats-new-in-nuget-50-preview-4"></a>Resumo: O que há de novo no NuGet 5.0 visualização 4

### <a name="issues-fixed-in-this-release"></a>Problemas corrigidos nesta versão

**Bugs:**

* NuGet.VisualStudio.IVsPackageInstaller - chamada em um projeto com nenhum pacote referencia sempre Packages. config usa, mesmo se o padrão é definido na PackageReference – [7005 #](https://github.com/NuGet/Home/issues/7005)

* PMC: Pacote de atualização reinstalar falhar ("não é possível localizar o pacote") removido da lista de pacotes. - [#7268](https://github.com/NuGet/Home/issues/7268)

* Adicionar um aviso de terceiros em nosso repositório e VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)

* NuGet.VisualStudio.IVsPackageInstaller.InstallPackage deve instalar a versão mais recente quando nenhuma versão considerando - [#7493](https://github.com/NuGet/Home/issues/7493)

* – suporte interativo para dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)

* Quando a restauração do arquivo de bloqueio, o aviso de NU1603 não deve ser gerado. - [#7529](https://github.com/NuGet/Home/issues/7529)

* O NuGet não deve imprimir o caminho do projeto durante a restauração com log mínimo - [#7647](https://github.com/NuGet/Home/issues/7647)

* – suporte interativo para dotnet remover pacote - [#7727](https://github.com/NuGet/Home/issues/7727)

* Adicionar de volta NuGet.Packaging.Core com TypeForwardedTo attrs - [7768 #](https://github.com/NuGet/Home/issues/7768)

* plugins_cache precisa de um caminho mais curto para funcionar bem - [#7770](https://github.com/NuGet/Home/issues/7770)

* Prefira o caminho para a descoberta do msbuild se o usuário não foi solicitado para a versão do msbuild específicas - [#7786](https://github.com/NuGet/Home/issues/7786)

**DCRs:**

* limitar o número de solicitação http por origem por meio do NuGet. config - [#4538](https://github.com/NuGet/Home/issues/4538)

* O NuGet deve ter como destino Net472 (para ajudar a limpar a compilação 16.0 do VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC: Remover comando OpenPackagePage - [7384 #](https://github.com/NuGet/Home/issues/7384)

* Verifique NetCoreApp 3.0 são mapeados para o NetStandard 2.1 - [7762 #](https://github.com/NuGet/Home/issues/7762)

* Adicionar suporte a netstandard2.0 para pacotes NuGet.* - [6516 #](https://github.com/NuGet/Home/issues/6516)


## <a name="summary-whats-new-in-nuget-50-preview-3"></a>Resumo: O que há de novo no NuGet 5.0 Preview 3

### <a name="issues-fixed-in-this-release"></a>Problemas corrigidos nesta versão 

**Bugs:**

* nuget.exe /? deve listar as versões corretas do msbuild – [7794 #](https://github.com/NuGet/Home/issues/7794)

* NuGet.targets(498,5): error : Não foi possível localizar uma parte do caminho ' / tmp/NuGetScratch - no mono - [7793 #](https://github.com/NuGet/Home/issues/7793)

* restauração desnecessariamente enumera o conteúdo de todas as versões do pacote referenciado no cache do computador - [#7639](https://github.com/NuGet/Home/issues/7639)

* Detecção automática de MSBuild sempre seleciona 16.0 após a instalação VS 2019 visualizar - [#7621](https://github.com/NuGet/Home/issues/7621)

* pacote do dotnet lista em uma solução gera entradas duplicadas para o framework - [#7607](https://github.com/NuGet/Home/issues/7607)

* Exceção "o nome de caminho vazio não é legal" quando chamada IVsPackageInstaller.InstallPackage antigo projetos e pacotes de pasta não existe. - [#5936](https://github.com/NuGet/Home/issues/5936)

* detalhamento do MSBuild /t: Restore mínimo deve ser mais mínimo - [#4695](https://github.com/NuGet/Home/issues/4695)

**DCRs:**

* Permitir que os autores de pacote definir o comportamento de transitiva de ativos de build - [#6091](https://github.com/NuGet/Home/issues/6091)

* Habilitar a restauração no VS para ter êxito se um projeto não é parte da solução ou não está carregado, mas anteriormente foi restaurado - [#5820](https://github.com/NuGet/Home/issues/5820)


## <a name="summary-whats-new-in-50-preview-2"></a>Resumo: O que há de novo no 5.0 Preview 2

### <a name="issues-fixed-in-this-release"></a>Problemas corrigidos nesta versão

**Bugs:**

* O VS do 16.0 UI NuGet tem guias ilegíveis devido a problemas de cor - [#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet. Core & esclarecimento Clients License - [#7629](https://github.com/NuGet/Home/issues/7629)

* Restauração desnecessariamente enumera a pasta de pacote global na tentativa de determinar o tipo - [#7596](https://github.com/NuGet/Home/issues/7596)

* Erros de imposição de arquivo de bloqueio deverá aparecer na janela de lista de erros - [#7429](https://github.com/NuGet/Home/issues/7429)

* Corrigir problemas de NuGet.Configuration - [7326 #](https://github.com/NuGet/Home/issues/7326)

* Adaptar-se a atualização do MSBuild é um local de instalação.  - [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet.Build.Tasks.Pack deve ser uma dependência de desenvolvimento - [#7249](https://github.com/NuGet/Home/issues/7249)

* Adicionar ponto de extensão do pacote para a inclusão de depurar símbolos - [#7234](https://github.com/NuGet/Home/issues/7234)

* dotnet pack deve preservar o intervalo de versão de dependência no nupkg criado. (mesmo se for usada a versão flutuante) - [#7232](https://github.com/NuGet/Home/issues/7232)

* restauração do dotnet falhará em fonte autenticada quando config de nível de usuário também tem origem - [#7209](https://github.com/NuGet/Home/issues/7209)

* Pacote não deve restringir o conjunto de BuildActions para arquivos de conteúdo - [#7155](https://github.com/NuGet/Home/issues/7155)

* Usando um projectreference que exige AssetTargetFallback tenha êxito, deverá avisar. - [#7137](https://github.com/NuGet/Home/issues/7137)

* Deadlock devido a problemas de threading durante uma chamada a CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)

* dotnet Adicionar pacote não usa as credenciais de configuração global para uma fonte especificada na configuração local – [6935 #](https://github.com/NuGet/Home/issues/6935)

* Problemas de Threading com MEF que está sendo chamado em caminhos do código assíncrono - [#6771](https://github.com/NuGet/Home/issues/6771)

* De autenticação: erro relatado duas vezes e sem a pilha de chamadas - [#6455](https://github.com/NuGet/Home/issues/6455)

* Instalar um pacote assinado com um certificado de assinatura não confiável deve mostrar o erro - [#6318](https://github.com/NuGet/Home/issues/6318)

* Restauração do NuGet incorretamente NoOps quando 2 projetos estão compartilhando a pasta obj - [#6114](https://github.com/NuGet/Home/issues/6114)

* Não é possível usar PAT com o comando dotnet restore no Linux com pacotes de feed autenticado - [#5651](https://github.com/NuGet/Home/issues/5651)

* dotnet restore falha devido a ampla de máquina desabilitada feed - [#5410](https://github.com/NuGet/Home/issues/5410)

**DCRs:**

* Assemblies de NuGet 5.0 para exigir o .NET 4.7.2 (por meio da alteração TFM) - [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData de Struktury deve ser um tipo público. Atualize metadados de licença ingeridos de spdx. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Remover APIs obsoletas de configurações - [#7294](https://github.com/NuGet/Home/issues/7294)

* Solução alternativa tempos limite de restauração em sistemas com 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet prefere autenticação NTLM, mesmo se houver credenciais no NuGet. config - adicionar a opção de configuração para os tipos de autenticação de filtro para credenciais - [#5286](https://github.com/NuGet/Home/issues/5286)

* Habilitar EmbedInteropTypes para PackageReference (recurso de Packages. config correspondente) - [2365 #](https://github.com/NuGet/Home/issues/2365)

[Lista de todos os problemas corrigidos 5.0.0-preview2 esta versão](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a>Problemas conhecidos

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>Os pacotes em FallbackFolders instalados pelo SDK .NET Core são instalados de forma personalizada e falham ao validar a assinatura. - [#7414](https://github.com/NuGet/Home/issues/7414)
**Problema** ao usar dotnet.exe 2.x para restaurar um projeto que netcoreapp vários destinos 1.x e netcoreapp 2. x, a pasta de fallback é tratado como um arquivo de feed. Isso significa que, ao restaurar, o NuGet escolherá o pacote da pasta de fallback e tentará instalá-lo na pasta de pacotes globais e fazer a validação de assinatura usual que falha.
**Solução alternativa** desabilitar o uso da pasta de fallback, definindo o `RestoreAdditionalProjectSources` como nothing. `<RestoreAdditionalProjectSources/>` Use essa opção com cuidado porque ela pode fazer com que muitos dos pacotes sejam baixados do NuGet.org, os quais, normalmente, seriam restaurados da pasta de fallback.
