---
title: Notas de versão do NuGet 5,3
description: Notas de versão do NuGet 5,3, incluindo novos recursos, correções de bugs e DCRs.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: f16bfe5481009f7924a61f03233d288d25ac618f
ms.sourcegitcommit: f4bfdbf62302c95f1f39e81ccf998f8bbc6d56b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70774097"
---
# <a name="nuget-53-release-notes"></a>Notas de versão do NuGet 5,3

Veículos de distribuição do NuGet:

| Versão do NuGet | Disponível na versão do Visual Studio| Disponível em SDKs do .NET|
|:---|:---|:---|
| [**5.3.0-preview3**](https://nuget.org/downloads) | [Visual Studio 2019 versão 16,3 Preview 3](https://visualstudio.microsoft.com/vs/preview/) | [3.0.100-preview9](https://dotnet.microsoft.com/download/dotnet-core/3.0) <sup>1</sup> |

<sup>1</sup> Instalado com o Visual Studio 2019 com carga de trabalho do .NET Core

## <a name="summary-whats-new-in-53-preview-3"></a>Resumo: O que há de novo na versão prévia 3 do 5,3

* [O ícone de pacote pode ser inserido no pacote](../reference/msbuild-targets.md#packing-an-icon-image-file), em vez de precisar de uma URL externa. - [#352](https://github.com/NuGet/Home/issues/352)

* Segurança aprimorada com rastreamento e imposição de SHA para Packages. config- [#7281](https://github.com/NuGet/Home/issues/7281)

### <a name="issues-fixed-in-this-release"></a>Problemas corrigidos nesta versão

**•s**

* VS: os assemblies são totalmente baseados em NGen-Ed não parcialmente-Ed- [#8513](https://github.com/NuGet/Home/issues/8513)

* Reduzir o uso de memória (cancelar assinatura de eventos)- [#8471](https://github.com/NuGet/Home/issues/8471)

* A mensagem "Error_UnableToFindProjectInfo" não está gramaticalmente correta- [#8441](https://github.com/NuGet/Home/issues/8441)

* Aprimoramentos do NU1403 – validar todos os pacotes, incluir os valores de Sha esperados/reais- [#8424](https://github.com/NuGet/Home/issues/8424)

* Enumeração múltipla em NuGetPackageManager. PreviewUpdatePackagesAsync- [#8401](https://github.com/NuGet/Home/issues/8401)

* Reverter alteração "pública > interna" em PluginProcess- [#8390](https://github.com/NuGet/Home/issues/8390)

* IVsPackageSourceProvider. getsources (...) tem comportamento de exceção mal definido- [#8383](https://github.com/NuGet/Home/issues/8383)

* Tornar o Construtor PlugInManager público novamente- [#8379](https://github.com/NuGet/Home/issues/8379)

* Métricas para acompanhar a taxa de atualização da interface do usuário do PM- [#8369](https://github.com/NuGet/Home/issues/8369)

* Diminuir o número de atualizações da interface do usuário ao instalar por meio da interface do usuário do Gerenciador de pacotes- [#8358](https://github.com/NuGet/Home/issues/8358)

* Telemetria: os valores de DateTime usam formatos específicos de cultura- [#8351](https://github.com/NuGet/Home/issues/8351)

* Reduzir as atualizações da interface do usuário na guia procurar da interface do usuário do Gerenciador de pacotes #6570- [#8339](https://github.com/NuGet/Home/issues/8339)

* [Falha de teste] "Não é possível analisar o arquivo de configuração" solicitará duas vezes [#8320](https://github.com/NuGet/Home/issues/8320)

* Gerar erro NU5037 com boa página de documento que explica as correções do cliente (o arquivo nuspec necessário está faltando no pacote)- [#8291](https://github.com/NuGet/Home/issues/8291)

* A restauração de modo bloqueado falha quando o RuntimeIdentifier de um projeto é alterado- [#8260](https://github.com/NuGet/Home/issues/8260)

* Fazer com que as configurações sejam lidas em VS Lazy- [#8156](https://github.com/NuGet/Home/issues/8156)

* A regressão em ' adicionar fontes do NuGet ' causa "o caractere ': ', valor hexadecimal 0x3A, não pode ser incluído em um nome" Errors- [#7948](https://github.com/NuGet/Home/issues/7948)

* Provedores de credenciais do plug-in NuGet-ocultar a janela processo- [#7511](https://github.com/NuGet/Home/issues/7511)

* Impor PackagePathResolver é um caminho absoluto- [#7349](https://github.com/NuGet/Home/issues/7349)

* Reduzir as atualizações da interface do usuário nas guias instalar e atualizar da interface do usuário do Gerenciador de pacotes- [#6570](https://github.com/NuGet/Home/issues/6570)

**DCR:**

* Atualizar as estruturas do Xamarin para mapear para o netstandard 2,1- [#8368](https://github.com/NuGet/Home/issues/8368)

* Habilitar a cópia do conteúdo da "janela de visualização" do Gerenciador de pacotes para instalar/atualizar- [#8324](https://github.com/NuGet/Home/issues/8324)

* Habilitar a restauração em arquivos. proj- [#8212](https://github.com/NuGet/Home/issues/8212)

* Introduza `NUGET_NETFX_PLUGIN_PATHS` e`NUGET_NETCORE_PLUGIN_PATHS` para dar suporte à configuração de ambos ao mesmo tempo- [#8151](https://github.com/NuGet/Home/issues/8151)

* Habilitar várias versões para um PackageDownload por meio do atributo de versão- [#8074](https://github.com/NuGet/Home/issues/8074)

* Adicionar opções-SolutionDirectory e-PackageDirectory ao NuGet. exe Pack- [#7163](https://github.com/NuGet/Home/issues/7163)

* Habilitar o NuGet Pack para ser determinístico- [#6229](https://github.com/NuGet/Home/issues/6229)

**[Lista de todos os problemas corrigidos nesta versão-5,3 Preview 3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**
