---
title: Suporte ao caminho longo de CLI do NuGet
description: Referência para suporte de caminho longos nuget.exe
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 42b5b7d863d22d7aad99a65700ca11bcc2861db1
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453488"
---
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="876d8-103">Suporte a caminhos longos (CLI do NuGet)</span><span class="sxs-lookup"><span data-stu-id="876d8-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="876d8-104">**Aplica-se a:** todos os &bullet; **versões com suporte:** 4.8 +</span><span class="sxs-lookup"><span data-stu-id="876d8-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="876d8-105">Suporte 4,8 e versões posteriores de NuGet.exe caminhos longos para arquivos e diretórios para cenários como o pacote, restauração, instalação e a maioria dos outros cenários que precisam de caminhos de arquivo.</span><span class="sxs-lookup"><span data-stu-id="876d8-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="876d8-106">Sistema operacional necessário</span><span class="sxs-lookup"><span data-stu-id="876d8-106">Required Operating System</span></span>

-   <span data-ttu-id="876d8-107">Windows 10 (versão 1607 ou posterior)</span><span class="sxs-lookup"><span data-stu-id="876d8-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="876d8-108">Windows 10 (versão de julho de 2015 ou versão 1511) se você atualizar o .NET Framework para as versões 4.6.2 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="876d8-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="876d8-109">Windows Server 2016 (todas as versões)</span><span class="sxs-lookup"><span data-stu-id="876d8-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="876d8-110">Habilitar política de grupo "Caminhos longos do Win32"</span><span class="sxs-lookup"><span data-stu-id="876d8-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="876d8-111">É necessário habilitar o suporte de caminho longos nesses sistemas, definindo uma política de grupo.</span><span class="sxs-lookup"><span data-stu-id="876d8-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="876d8-112">Etapas:</span><span class="sxs-lookup"><span data-stu-id="876d8-112">Steps:</span></span>
1. <span data-ttu-id="876d8-113">Inicie **Editor de diretiva de grupo** - digite "Editar política de grupo" na barra de pesquisa do início ou executado "gpedit. msc" no comando executar (Windows-R).</span><span class="sxs-lookup"><span data-stu-id="876d8-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="876d8-114">No **Editor de diretiva de Grupo Local**, habilite "modelos substitui qualquer configuração de diretiva de computador de computador locais/todos os caminhos longos de configurações/Habilitar Win32".</span><span class="sxs-lookup"><span data-stu-id="876d8-114">In the **Local Group Policy Editor**, enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![Diretiva de caminho longo](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="876d8-116">Habilitando a outras ferramentas do NuGet dar suporte a caminhos longos</span><span class="sxs-lookup"><span data-stu-id="876d8-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="876d8-117">Dotnet CLI dá suporte a caminhos longos, independentemente do sistema operacional ou versão.</span><span class="sxs-lookup"><span data-stu-id="876d8-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="876d8-118">Visual Studio ou o msbuild - t: restauração ainda não dá suporte a caminhos longos.</span><span class="sxs-lookup"><span data-stu-id="876d8-118">Visual Studio or msbuild -t:restore does not yet support long paths.</span></span>
> -   <span data-ttu-id="876d8-119">Software que usa bibliotecas NuGet para executar outros comandos, e a restauração será dão suporte a caminhos longos nos mesmos sistemas que NuGet.exe funciona no, se eles também definem longPathAware em suas janelas de manifesto e configurar o UseLegacyPathHandling como falso por meio do App. config [ Obter mais informações](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span><span class="sxs-lookup"><span data-stu-id="876d8-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set longPathAware in their windows manifest and configure UseLegacyPathHandling to false via App.Config [See more information](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span></span>

