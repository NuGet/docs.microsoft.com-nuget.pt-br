---
title: Notas de versão do NuGet 5,0 RTM
description: Notas de versão do NuGet 5,0 incluindo problemas conhecidos, correções de bugs, novos recursos e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 637db1ae128ce020c33e54e56148c848a5f905a5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776220"
---
# <a name="nuget-50-release-notes"></a>Notas de versão do NuGet 5,0

Veículos de distribuição do NuGet:

| Versão do NuGet | Disponível na versão do Visual Studio| Disponível em SDKs do .NET|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Visual Studio 2019 versão 16,0](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |
| [**5.0.2**](https://nuget.org/downloads) | [Visual Studio 2019 versão 16.0.4](https://visualstudio.microsoft.com/downloads/) | [2.1.60 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Instalado com o Visual Studio 2019 com carga de trabalho do .NET Core 

<sup>2</sup> Disponível como uma instalação opcional com o Visual Studio 2019 com carga de trabalho do .NET Core

## <a name="summary-whats-new-in-50"></a>Resumo: o que há de novo no 5,0

* Suporte para restaurar [soluções filtradas](/visualstudio/ide/filtered-solutions?view=vs-2019) no Visual Studio 2019- [#5820](https://github.com/NuGet/Home/issues/5820)
* `BuildTransitive` a pasta permite que os pacotes contribuam de forma transitiva destinos/props para o projeto de host- [#6091](https://github.com/NuGet/Home/issues/6091)
* Melhor suporte para cenários de PackageReference no NuGet IVs APIs- [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` foi preterido- [#7928](https://github.com/NuGet/Home/issues/7928)
* O plugin do provedor de credenciais Gen 1 foi substituído pela [Gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) e em breve será preterido- [#7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>Problemas corrigidos nesta versão

**Bugs**

* Ao fazer uma restauração de NoOp, evite * .dgspec.jsem gravar no diretório obj- [#7854](https://github.com/NuGet/Home/issues/7854)

* As permissões em arquivos criados dentro de ~/.NuGet são muito abertas- [#7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated`Não funciona com fontes que precisam de [#7605](https://github.com/NuGet/Home/issues/7605) de autenticação

* NuGet. VisualStudio. IVsPackageInstaller-a chamada em um projeto sem referências de pacote sempre usa packages.config, mesmo que o padrão esteja definido como PackageReference- [#7005](https://github.com/NuGet/Home/issues/7005)

* PMC: a reinstalação do Update-Package falha ("não é possível localizar o pacote") em pacotes deslistados. - [#7268](https://github.com/NuGet/Home/issues/7268)

* Adicionar aviso de terceiros em nosso repositório e VSIX- [#7409](https://github.com/NuGet/Home/issues/7409)

* NuGet. VisualStudio. IVsPackageInstaller. InstallPackage deve instalar a versão mais recente quando nenhuma versão é fornecida- [#7493](https://github.com/NuGet/Home/issues/7493)

* --suporte interativo para o [#7519](https://github.com/NuGet/Home/issues/7519) dotnet do NuGet

* Ao restaurar com o arquivo de bloqueio, o aviso de NU1603 não deve ser gerado. - [#7529](https://github.com/NuGet/Home/issues/7529)

* O NuGet não deve imprimir o caminho do projeto durante a restauração com o mínimo de log- [#7647](https://github.com/NuGet/Home/issues/7647)

* --suporte interativo para o dotnet remover pacote- [#7727](https://github.com/NuGet/Home/issues/7727)

* Adicionar NuGet. Packaging. Core com TypeForwardedTo attrs- [#7768](https://github.com/NuGet/Home/issues/7768)

* plugins_cache precisa de um caminho mais curto para funcionar bem [#7770](https://github.com/NuGet/Home/issues/7770)

* Prefira o caminho para a descoberta do MSBuild se o usuário não solicitar uma versão do MSBuild específica- [#7786](https://github.com/NuGet/Home/issues/7786)

* `nuget.exe /?` deve listar as versões corretas do MSBuild- [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet. targets (498, 5): erro: não foi possível encontrar uma parte do caminho '/tmp/NuGetScratch-on mono- [#7793](https://github.com/NuGet/Home/issues/7793)

* restaurar desnecessariamente enumera o conteúdo de todas as versões do pacote referenciado no cache da máquina- [#7639](https://github.com/NuGet/Home/issues/7639)

* A detecção automática do MSBuild sempre seleciona 16,0 após a instalação do VS 2019 Preview- [#7621](https://github.com/NuGet/Home/issues/7621)

* o pacote de lista dotnet em uma solução gera entradas duplicadas para o Framework- [#7607](https://github.com/NuGet/Home/issues/7607)

* Exceção "o nome do caminho vazio não é válido" ao chamar IVsPackageInstaller. InstallPackage na pasta projetos e pacotes antigos não existe. - [#5936](https://github.com/NuGet/Home/issues/5936)

* MSBuild/t: Restore o mínimo de detalhes deve ser mais mínimo [#4695](https://github.com/NuGet/Home/issues/4695)

* A interface do usuário do NuGet do VS 16.0 tem guias ilegíveis devido a problemas de cor- [#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet. Core & NuGet. clients License.txt esclarecimento- [#7629](https://github.com/NuGet/Home/issues/7629)

* Restauração desnecessariamente enumera a pasta de pacote global em tentativa de determinar o tipo [#7596](https://github.com/NuGet/Home/issues/7596)

* Os erros da imposição de arquivos bloqueados devem aparecer na janela Lista de Erros- [#7429](https://github.com/NuGet/Home/issues/7429)

* Corrigir NuGet.Configproblemas de uração- [#7326](https://github.com/NuGet/Home/issues/7326)

* Adaptar ao MSBuild atualizando seu local de instalação- [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet. Build. Tasks. Pack deve ser uma dependência de desenvolvimento- [#7249](https://github.com/NuGet/Home/issues/7249)

* Adicionar ponto de extensão de pacote para incluir símbolos de depuração- [#7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` deve preservar o intervalo de versão de dependência no nupkg criado (mesmo se a versão flutuante for usada)- [#7232](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore`falha na origem autenticada quando a configuração no nível do usuário também tem [#7209](https://github.com/NuGet/Home/issues/7209) de origem

* O pacote não deve restringir o conjunto de BuildActions para arquivos de conteúdo- [#7155](https://github.com/NuGet/Home/issues/7155)

* Usando um ProjectReference que exige que o AssetTargetFallback tenha sucesso, deve avisar. - [#7137](https://github.com/NuGet/Home/issues/7137)

* Deadlock devido a problemas de Threading ao chamar o CPS (CommonProjectSystem)- [#7103](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` Não usa credenciais da configuração global para uma origem especificada na configuração local- [#6935](https://github.com/NuGet/Home/issues/6935)

* Problemas de Threading com o MEF sendo chamado em caminhos de código assíncrono- [#6771](https://github.com/NuGet/Home/issues/6771)

* Assinatura: erro relatado duas vezes e sem pilha de chamadas- [#6455](https://github.com/NuGet/Home/issues/6455)

* A instalação de um pacote assinado com um certificado de autenticação não confiável deve mostrar o erro- [#6318](https://github.com/NuGet/Home/issues/6318)

* Restauração do NuGet incorretamente NoOps quando 2 projetos estão compartilhando Diretório obj- [#6114](https://github.com/NuGet/Home/issues/6114)

* Não é possível usar PAT com `dotnet restore` no Linux com pacotes do feed autenticado- [#5651](https://github.com/NuGet/Home/issues/5651)

* dotnet restore falha devido a um feed em todo o computador desabilitado- [#5410](https://github.com/NuGet/Home/issues/5410)

**DCRs**

* Aviso de futura remoção do "dotnet do project.jsdo pacote"- [#7928](https://github.com/NuGet/Home/issues/7928)
 
* Adicionar um aviso de reprovação para o plug-in de credencial Gen1- [#7819](https://github.com/NuGet/Home/issues/7819)
 
* Assinatura: repositório habilitado para exigir a verificação do cliente de cada pacote como assinado pelo repositório – por meio do recurso RepositorySignatures/5.0.0- [#7759](https://github.com/NuGet/Home/issues/7759)

* limitar o número de solicitação HTTP por origem por meio de NuGet.Config- [#4538](https://github.com/NuGet/Home/issues/4538)

* O NuGet deve direcionar Net472 (para ajudar a limpar a compilação 16,0 do VSIX) – [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC: remover comando OpenPackagePage- [#7384](https://github.com/NuGet/Home/issues/7384)

* Fazer o mapa do NetCoreApp 3,0 para o netstandard 2,1- [#7762](https://github.com/NuGet/Home/issues/7762)

* Adicionar suporte do netstandard 2.0 a pacotes NuGet. *- [#6516](https://github.com/NuGet/Home/issues/6516)

* Permitir que os autores de pacotes definam comportamento transitivo de compilação de ativos- [#6091](https://github.com/NuGet/Home/issues/6091)

* Suporte ao recurso de filtro de solução VS 2019. Também dá suporte a projeto que não está na solução ou projetos descarregados. Precisa restaurar a solução completa (via CLI ou VS) primeiro [#5820](https://github.com/NuGet/Home/issues/5820)

* Assemblies do NuGet 5,0 para exigir o .NET 4.7.2 (via alteração de TFM)- [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData do NuGet. o empacotamento deve ser um tipo público. Atualizar metadados de licença ingeridos de spdx. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Remover configurações obsoletas APIs- [#7294](https://github.com/NuGet/Home/issues/7294)

* Tempos limite de restauração de solução alternativa em sistemas com 1 [#6742](https://github.com/NuGet/Home/issues/6742) de CPU

* O NuGet prefere a autenticação NTLM mesmo se houver credenciais na opção NuGet.config-adicionar configuração para filtrar tipos de autenticação para credenciais- [#5286](https://github.com/NuGet/Home/issues/5286)

* Habilitar EmbedInteropTypes para PackageReference (Packages.Config capacidade de correspondência) – [#2365](https://github.com/NuGet/Home/issues/2365)

**[Lista de todos os problemas corrigidos nesta versão-5,0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="summary-whats-new-in-502"></a>Resumo: o que há de novo no 5.0.2

* Segurança (quando executado via dotnet.exe ou mono.exe)-a pasta obj deve ser criada com as permissões corretas [#7908](https://github.com/NuGet/Home/issues/7908)

* A restauração de nuget.exe em mono/MacOS falha com nuget.config personalizado e `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)


## <a name="known-issues"></a>Problemas conhecidos

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a>Os pacotes em FallbackFolders instalados pelo SDK .NET Core são instalados de forma personalizada e falham ao validar a assinatura. - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>Problema
Ao usar o dotnet.exe 2.x para restaurar um projeto que fará o direcionamento múltiplo para netcoreapp 1.x e netcoreapp 2.x, a pasta de fallback será tratada como um feed de arquivos. Isso significa que, ao restaurar, o NuGet escolherá o pacote da pasta de fallback e tentará instalá-lo na pasta de pacotes globais e fazer a validação de assinatura usual que falha.<br>
#### <a name="workaround"></a>Solução alternativa
Desabilite o uso da pasta de fallback definindo o `RestoreAdditionalProjectSources` como nada:

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

Use isso com cuidado, pois os pacotes que seriam restaurados da pasta de fallback agora serão baixados de NuGet.org.