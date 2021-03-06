---
title: Notas de versão do NuGet 5,3
description: Notas de versão do NuGet 5,3, incluindo novos recursos, correções de bugs e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 009a219139a767ee6453305be68ccce478b0ec75
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780119"
---
# <a name="nuget-53-release-notes"></a>Notas de versão do NuGet 5,3

Veículos de distribuição do NuGet:

| Versão do NuGet | Disponível na versão do Visual Studio| Disponível em SDKs do .NET|
|:---|:---|:---|
| [**5.3.0**](https://nuget.org/downloads) | [Visual Studio 2019 versão 16,3](https://visualstudio.microsoft.com/downloads/) | [3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup> |
| [**5.3.1**](https://nuget.org/downloads) | [Visual Studio 2019 versão 16.3.6](https://visualstudio.microsoft.com/downloads/) | [Versão futura: 3.0.101](https://dotnet.microsoft.com/download/dotnet-core/3.0) |

<sup>1</sup> Instalado com o Visual Studio 2019 com carga de trabalho do .NET Core

## <a name="summary-whats-new-in-53"></a>Resumo: o que há de novo no 5,3

* [O ícone de pacote pode ser inserido no pacote](../reference/msbuild-targets.md#packing-an-icon-image-file), em vez de precisar de uma URL externa. - [#352](https://github.com/NuGet/Home/issues/352)

* Segurança aprimorada com rastreamento e imposição de SHA para Packages.Config- [#7281](https://github.com/NuGet/Home/issues/7281)

* Habilitar a reprovação de pacotes NuGet obsoletos/herdados [#2867](https://github.com/NuGet/Home/issues/2867)  |  documentos de[postagem de blog](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/)  |  [](../nuget-org/deprecate-packages.md)

### <a name="issues-fixed-in-this-release"></a>Problemas corrigidos nesta versão

**Bugs**

* Os pacotes NuGet produzidos com o SDK 3.0.100-preview9 não podem ser usados por usuários do SDK 2,2... dependendo do seu fuso horário [#8603](https://github.com/NuGet/Home/issues/8603)

* Aspas "os caracteres no caminho causam uma falha de" caracteres ilegais no caminho "em `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)

* VS: os assemblies são totalmente baseados em NGen-Ed não parcialmente-Ed- [#8513](https://github.com/NuGet/Home/issues/8513)

* Reduzir o uso de memória (cancelar assinatura de eventos)- [#8471](https://github.com/NuGet/Home/issues/8471)

* A mensagem "Error_UnableToFindProjectInfo" não está gramaticalmente correta- [#8441](https://github.com/NuGet/Home/issues/8441)

* Aprimoramentos do NU1403 – validar todos os pacotes, incluir os valores de Sha esperados/reais- [#8424](https://github.com/NuGet/Home/issues/8424)

* Várias enumerações em `NuGetPackageManager.PreviewUpdatePackagesAsync`  -  [#8401](https://github.com/NuGet/Home/issues/8401)

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

* A regressão em `Nuget sources add` causa "o caractere": ", valor hexadecimal 0x3A, não pode ser incluído em um nome" erros- [#7948](https://github.com/NuGet/Home/issues/7948)

* Provedores de credenciais do plug-in NuGet-ocultar a janela processo- [#7511](https://github.com/NuGet/Home/issues/7511)

* Impor PackagePathResolver é um caminho absoluto- [#7349](https://github.com/NuGet/Home/issues/7349)

* Reduzir as atualizações da interface do usuário nas guias instalar e atualizar da interface do usuário do Gerenciador de pacotes- [#6570](https://github.com/NuGet/Home/issues/6570)

**DCR:**

* Atualizar as estruturas do Xamarin para mapear para o netstandard 2,1- [#8368](https://github.com/NuGet/Home/issues/8368)

* Habilitar a cópia do conteúdo da "janela de visualização" do Gerenciador de pacotes para instalar/atualizar- [#8324](https://github.com/NuGet/Home/issues/8324)

* Habilitar a restauração em arquivos. proj- [#8212](https://github.com/NuGet/Home/issues/8212)

* Introduza `NUGET_NETFX_PLUGIN_PATHS` e `NUGET_NETCORE_PLUGIN_PATHS` para dar suporte à configuração de ambos ao mesmo tempo- [#8151](https://github.com/NuGet/Home/issues/8151)

* Habilitar várias versões para um PackageDownload por meio do atributo de versão- [#8074](https://github.com/NuGet/Home/issues/8074)

* Opções Add-SolutionDirectory e-PackageDirectory para nuget.exe Pack [#7163](https://github.com/NuGet/Home/issues/7163)

**[Lista de todos os problemas corrigidos nesta versão-5,3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**

## <a name="summary-whats-new-in-531"></a>Resumo: o que há de novo no 5.3.1

* Plugin: uma tarefa foi cancelada-não permita que cancelamentos afetem a instanciação do plug-in- [#8648](https://github.com/NuGet/Home/issues/8648)

* A tarefa de restauração não pode ser executada com segurança duas vezes em um processo (quando provedores de credenciais são usados)- [#8688](https://github.com/NuGet/Home/issues/8688)
