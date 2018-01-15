---
title: "Referências de estruturas de destino para NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/11/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 4343a48e-f6df-4a44-9d66-4616c3caacf5
description: "As referências de estrutura de destino do NuGet identificam e isolam componentes dependentes de estrutura de um pacote."
keywords: "Direcionamento de pacote do NuGet, destinos do .NET framework, versões do .NET framework"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 36e1f0cd6e4284a6bd272ce3c85749e9ed72cbcd
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="target-frameworks"></a>Frameworks de destino

O NuGet usa referências de estrutura de destino em uma variedade de locais para identificar e isolar especificamente os componentes dependentes de estrutura de um pacote:

- [Manifesto do .nuspec](../schema/nuspec.md): um pacote pode indicar pacotes distintos a serem incluídos em um projeto dependendo da estrutura de destino dele.
- [Nome da pasta .nupkg](../create-packages/creating-a-package.md#from-a-convention-based-working-directory): as pastas dentro de uma pasta `lib` do pacote pode ser nomeada de acordo com a estrutura de destino, cada uma delas contém as DLLs e outros tipos de conteúdo apropriado para essa estrutura.
- [packages.config](../Schema/packages-config.md): o atributo `targetframework` de uma dependência especifica a variante de um pacote a ser instalado.
- [project.json](../Schema/project-json.md): o nó `frameworks` especifica as versões da estrutura com as quais o projeto pode ser compilado.

> [!Note]
> O código-fonte do cliente do NuGet que calcula as tabelas abaixo é encontrado nos seguintes locais:
> -  Suporte para nomes de estrutura: [FrameworkConstants.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/FrameworkConstants.cs)
> -  Precedência e mapeamento do Framework: [DefaultFrameworkMappings.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/DefaultFrameworkMappings.cs)

## <a name="supported-frameworks"></a>Estruturas com suporte

Normalmente, uma estrutura é referenciada por um moniker curto de estrutura de destino ou TFM. No .NET Standard, isso também é generalizado para *TxM* a fim de permitir uma única referência para várias estruturas.

Os clientes do NuGet são compatíveis com as estruturas indicadas na tabela abaixo. Equivalentes são mostrados entre colchetes []. Observe que algumas ferramentas, como `dotnet`, podem usar as variações de TFMs canônicos em alguns arquivos. Por exemplo, `dotnet pack` usa `.NETCoreApp2.0` em um arquivo `.nuspec` em vez de `netcoreapp2.0`. As várias ferramentas de cliente do NuGet manipulam essas variações corretamente, mas você sempre deve usar TFMs canônicos ao editar arquivos diretamente.

| Nome           | Abreviação de | TFMs/TxMs |
| -------------  | ------------ | --------- |
|.NET Framework  | net          | net11     |
|                |              | net20     |
|                |              | net35     |
|                |              | net40     |
|                |              | net403    |
|                |              | net45      |
|                |              | net451     |
|                |              | net452     |
|                |              | net46      |
|                |              | net461     |
|                |              | net462     |
|Microsoft Store (Windows Store) | netcore      | netcore [netcore45] |
|                |              | netcore45 [win, win8] |
|                |              | netcore451 [win81] |
|                |              | netcore50 |
|.NET MicroFramework | netmf    | netmf |
|Windows         | win          | win [win8, netcore45] |
| | | win8 [netcore45, win] |
| | | win81 [netcore451] |
| | | win10 (incompatível com a plataforma Windows 10) |
Silverlight | sl | sl4 |
| | | sl5 |
Windows Phone (SL) | wp | wp [wp7] |
| | | wp7 |
| | | wp75 |
| | | wp8 |
| | | wp81 |
Windows Phone (UWP) | | wpa81 |
Plataforma Universal do Windows | uap | uap [uap10.0] |
| | | uap10.0 |
.NET Standard | netstandard | netstandard1.0 |
| | | netstandard1.1 |
| | | netstandard1.2 |
| | | netstandard1.3 |
| | | netstandard1.4 |
| | | netstandard1.5 |
| | | netstandard1.6 |
| | | netstandard2.0 |
Aplicativos .NET Core | netcoreapp | netcoreapp1.0 |
| | | netcoreapp1.1 |
| | | netcoreapp2.0 |
Tizen | tizen | tizen3 |
| | | tizen4 |

## <a name="deprecated-frameworks"></a>Estruturas preteridas
As seguintes estruturas são preteridas. Os pacotes direcionados a essas estruturas devem ser migrados para as substituições indicadas.

| Estrutura preterida | Substituição
| --- | ---
| aspnet50 | netcoreapp |
| aspnetcore50 |
| dnxcore50 |
| dnx |
| dnx45 |
| dnx451 |
| dnx452 |
| dotnet | netstandard |
| dotnet50 | |
| dotnet51 | |
| dotnet52 | |
| dotnet53 | |
| dotnet54 | |
| dotnet55 | |
| dotnet56 | |
| winrt | win |

## <a name="precedence"></a>Precedência

Várias estruturas relacionadas e compatíveis entre si, mas não necessariamente equivalentes:

| Framework | Pode usar |
| --- | --- |
| uap (Plataforma Universal do Windows) | win81 |
| | wpa81 |
| | netcore50 |
| win (Microsoft Store) | winrt |
| | | winrt45 |

## <a name="net-platform-standard"></a>NET Platform Standard

O [.NET Platform Standard](https://github.com/dotnet/corefx/blob/master/Documentation/architecture/net-platform-standard.md) simplifica referências entre estruturas compatíveis com o binário, permitindo que uma estrutura de destino única faça referência a uma combinação de outras. (Para obter informações, consulte o [.NET Primer](/dotnet/articles/standard/index).)

A [Ferramenta Obter a ferramenta de estrutura mais próxima do NuGet](https://aka.ms/s2m3th) simula o que o NuGet usa para a seleção de uma estrutura de muitos ativos de estrutura disponíveis em um pacote baseado na estrutura do projeto.

A série de monikers `dotnet` deve ser usada no NuGet 3.3 e versões anteriores; a sintaxe de moniker `netstandard` deve ser usada no v3.4 e posterior.

## <a name="portable-class-libraries"></a>Bibliotecas de Classes Portáteis

> [!Warning]
> **PCLs não são recomendados**. Embora haja suporte para PCLs, os autores de pacote devem dar suporte ao netstandard em vez disso. O .NET Platform Standard é uma evolução de PCLs e representa a portabilidade binária entre plataformas que usam um moniker único que não está vinculado a um estático como monikers *portable-a+b+c*.

Para definir uma estrutura de destino que se refere a várias estruturas de destino filho, a palavra-chave `portable` é usada para prefixar a lista de estruturas referenciadas. Evite incluir estruturas extras artificialmente que não são diretamente compiladas, pois o erro pode causar efeitos colaterais indesejados nessas estruturas.

Estruturas adicionais definidas por terceiros fornecem compatibilidade com outros ambientes acessíveis dessa maneira. Além disso, há diversos perfis abreviados que estão disponíveis para fazer referência a essas combinações de estruturas relacionadas como `Profile#`, mas essa não é uma prática recomendada para usar esses números, pois isso reduz a legibilidade das pastas e `.nuspec`.

| Nº do perfil | Estruturas | Nome completo | .NET Standard |
 --- | --- | --- | ---
 Profile2 | .NETFramework 4.0 | portable-net40+win8+sl4+wp7 |
 | | Windows 8.0 | |
 | | Silverlight 4.0 |
 | | WindowsPhone 7.0|
 Profile3 | .NETFramework 4.0 | portable-net40+sl4
 | | Silverlight 4.0 |
 Profile4 | .NETFramework 4.5 | portable-net45+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile5 | .NETFramework 4.0 | portable-net40+win8
 | | Windows 8.0 |
 Profile6 | .NETFramework 4.0.3 | portable-net403+win8
 | | Windows 8.0 |
 Profile7 | .NETFramework 4.5 | portable-net45+win8 | netstandard1.1
 | | Windows 8.0 |
 Profile14 | .NETFramework 4.0 | portable-net40+sl5
 | | Silverlight 5.0 |
 Profile18 | .NETFramework 4.0.3 | portable-net403+sl4
 | | Silverlight 4.0 |
 Profile19 | .NETFramework 4.0.3 | portable-net403+sl5
 | | Silverlight 5.0 |
 Profile23 | .NETFramework 4.5 | portable-net45+sl4
 | | Silverlight 4.0 |
 Profile24 | .NETFramework 4.5 | portable-net45+sl5
 | | Silverlight 5.0 |
 Profile31 | Windows 8.1 | portable-win81+wp81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 Profile32 | Windows 8.1 | portable-win81+wpa81 | netstandard1.2
 | | WindowsPhone 8.1 (UWP) |
 Profile36 | .NETFramework 4.0 | portable-net40+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile37 | .NETFramework 4.0 | portable-net40+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile41 | .NETFramework 4.0.3 | portable-net403+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile42 | .NETFramework 4.0.3 | portable-net403+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile44 | .NETFramework 4.5.1 | portable-net451+win81 | netstandard1.2
 | | Windows 8.1 |
 Profile46 | .NETFramework 4.5 | portable-net45+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile47 | .NETFramework 4.5 | portable-net45+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile49 | .NETFramework 4.5 | portable-net45+wp8 | netstandard1.0
 | | WindowsPhone 8.0 (SL) |
 Profile78 | .NETFramework 4.5 | portable-net45+win8+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile84 | WindowsPhone 8.1 | portable-wp81+wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (UWP) |
 Profile88 | .NETFramework 4.0 | portable-net40+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile92 | .NETFramework 4.0 | portable-net40+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile95 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile96 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile102 | .NETFramework 4.0.3 | portable-net403+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile104 | .NETFramework 4.5 | portable-net45+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile111 | .NETFramework 4.5 | portable-net45+win8+wpa81 | netstandard1.1
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile136 | .NETFramework 4.0 | portable-net40+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile143 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile147 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile151 | NETFramework 4.5.1 | portable-net451+win81+wpa81 | netstandard1.2
 | | Windows 8.1 |
 | | WindowsPhone 8.1 (UWP) |
 Profile154 | .NETFramework 4.5 | portable-net45+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile157 | Windows 8.1 | portable-win81+wp81+wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 | | WindowsPhone 8.1 (UWP) |
 Profile158 | .NETFramework 4.5 | portable-net45+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile225 | .NETFramework 4.0 | portable-net40+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile240 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wpa8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile255 | .NETFramework 4.5 | portable-net45+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile259 | .NETFramework 4.5 | portable-net45+win8+wpa81+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile328 | .NETFramework 4.0 | portable-net40+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile336 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile344 | .NETFramework 4.5 | portable-net45+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |

Além disso, os pacotes do NuGet direcionados ao Xamarin podem usar estruturas adicionais definidas pelo Xamarin. Consulte [Criando pacotes do NuGet para Xamarin](https://developer.xamarin.com/guides/cross-platform/advanced/nuget/).

| Nome | Descrição | .NET Standard |
| --- | --- | ---
| monoandroid | Suporte a Mono para o sistema operacional Android | netstandard1.4 |
| monotouch | Suporte Mono para iOS | netstandard1.4 |
| monomac | Suporte Mono para OSX | netstandard1.4 |
| xamarinios | Suporte para Xamarin para iOS | netstandard1.4 |
| xamarinmac | Suportes para Xamarin para Mac | netstandard1.4 |
| xamarinpsthree | Suporte para Xamarin no Playstation 3 | netstandard1.4 |
| xamarinpsfour | Suporte para Xamarin no Playstation 4 | netstandard1.4 |
| xamarinpsvita | Suporte para Xamarin no PS Vita | netstandard1.4 |
| xamarinwatchos | Xamarin para Watch OS | netstandard1.4 |
| xamarintvos | Xamarin para TV OS | netstandard1.4 |
| xamarinxboxthreesixty | Xamarin para XBox 360 | netstandard1.4 |
| xamarinxboxone | Xamarin para XBox One | netstandard1.4 |

> [!Note]
> Stephen Cleary criou uma ferramenta que lista os PCLs compatíveis, a qual pode ser encontrada na sua postagem, [Perfis de estrutura no .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html).
