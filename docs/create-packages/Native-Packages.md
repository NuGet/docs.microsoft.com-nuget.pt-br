---
title: Criar pacotes nativos do NuGet
description: Detalhes sobre a criação de pacotes do NuGet nativos que contém código C++ em vez do código gerenciado, para uso em projetos C++.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 086084bdfae5eace0b0a6aab17140a1fa48ae977
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817054"
---
# <a name="creating-native-packages"></a><span data-ttu-id="597c7-103">Criando pacotes nativos</span><span class="sxs-lookup"><span data-stu-id="597c7-103">Creating native packages</span></span>

<span data-ttu-id="597c7-104">Um pacote nativo contém o código C++ nativo em vez do código gerenciado, permitindo que ele seja usado dentro de projetos C++.</span><span class="sxs-lookup"><span data-stu-id="597c7-104">A native package contains native C++ code instead of managed code, allowing it to be used within C++ projects.</span></span> <span data-ttu-id="597c7-105">(Consulte [Pacotes C++ nativos](../consume-packages/finding-and-choosing-packages.md#native-c-packages) na seção Consumir.)</span><span class="sxs-lookup"><span data-stu-id="597c7-105">(See [Native C++ Packages](../consume-packages/finding-and-choosing-packages.md#native-c-packages) in the Consume section.)</span></span>

<span data-ttu-id="597c7-106">Para ser consumido em um projeto C++, um pacote precisa ter como destino a estrutura `native`.</span><span class="sxs-lookup"><span data-stu-id="597c7-106">To be consumable in a C++ project, a package must target the `native` framework.</span></span> <span data-ttu-id="597c7-107">No momento não há nenhum número de versão associado a essa estrutura, visto que o NuGet trata todos os projetos do C++ da mesma forma.</span><span class="sxs-lookup"><span data-stu-id="597c7-107">At present there are not any version numbers associated with this framework as NuGet treats all C++ projects the same.</span></span>

> [!Note]
> <span data-ttu-id="597c7-108">Lembre-se de incluir *nativo* na seção `<tags>` do seu `.nuspec` para ajudar outros desenvolvedores a encontrarem seu pacote pesquisando essa marca.</span><span class="sxs-lookup"><span data-stu-id="597c7-108">Be sure to include *native* in the `<tags>` section of your `.nuspec` to help other developers find your package by searching on that tag.</span></span>

<span data-ttu-id="597c7-109">Pacotes do NuGet nativos voltados para `native` fornecerão arquivos nas pastas `\build`, `\content` e `\tools`. `\lib` não é usado neste caso (o NuGet não pode adicionar referências a um projeto C++ diretamente).</span><span class="sxs-lookup"><span data-stu-id="597c7-109">Native NuGet packages targeting `native` then provide files in `\build`, `\content`, and `\tools` folders; `\lib` is not used in this case (NuGet cannot directly add references to a C++ project).</span></span> <span data-ttu-id="597c7-110">Um pacote também pode incluir arquivos de destino e objetos no `\build` que o NuGet importará automaticamente para os projetos que consomem o pacote.</span><span class="sxs-lookup"><span data-stu-id="597c7-110">A package may also include targets and props files in `\build` that NuGet will automatically import into projects that consume the package.</span></span> <span data-ttu-id="597c7-111">Esses arquivos precisam ter o mesmo nome que a ID do pacote com as extensões `.targets` e/ou `.props`.</span><span class="sxs-lookup"><span data-stu-id="597c7-111">Those files must be named the same as the package ID with the `.targets` and/or `.props` extensions.</span></span> <span data-ttu-id="597c7-112">Por exemplo, o pacote [cpprestsdk](https://nuget.org/packages/cpprestsdk/) inclui um arquivo `cpprestsdk.targets` em sua pasta `\build`.</span><span class="sxs-lookup"><span data-stu-id="597c7-112">For example, the [cpprestsdk](https://nuget.org/packages/cpprestsdk/) package includes a `cpprestsdk.targets` file in its `\build` folder.</span></span>

<span data-ttu-id="597c7-113">A pasta `\build` pode ser usada para todos os pacotes do NuGet e não apenas pacotes nativos.</span><span class="sxs-lookup"><span data-stu-id="597c7-113">The `\build` folder can be used for all NuGet packages and not just native packages.</span></span> <span data-ttu-id="597c7-114">A pasta `\build` respeita a estrutura de destino como as pastas `\content`, `\lib` e `\tools`.</span><span class="sxs-lookup"><span data-stu-id="597c7-114">The `\build` folder respects target frameworks just like the `\content`, `\lib`, and `\tools` folders.</span></span> <span data-ttu-id="597c7-115">Isso significa que você pode criar as pastas `\build\net40` e `\build\net45`, e o NuGet importará os objetos e arquivos de destino para o projeto.</span><span class="sxs-lookup"><span data-stu-id="597c7-115">This means you can create a `\build\net40` folder and a `\build\net45` folder and NuGet will import the appropriate props and targets files into the project.</span></span> <span data-ttu-id="597c7-116">(Não é necessário usar scripts do PowerShell para importar destinos do MSBuild.)</span><span class="sxs-lookup"><span data-stu-id="597c7-116">(Use of PowerShell scripts to import MSBuild targets is not needed.)</span></span>
