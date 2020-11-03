---
title: Suporte a caminhos longos da CLI do NuGet
description: Referência para suporte de caminho longo nuget.exe
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 1143da911c80125a9d60e4b98798b11871e9988a
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238186"
---
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="5b8a5-103">Suporte a caminho longo (CLI do NuGet)</span><span class="sxs-lookup"><span data-stu-id="5b8a5-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="5b8a5-104">**Aplica-se a:** todas as &bullet; **versões com suporte:** 4.8 +</span><span class="sxs-lookup"><span data-stu-id="5b8a5-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="5b8a5-105">NuGet.exe 4,8 e posteriores dão suporte a caminhos longos para arquivos e diretórios para cenários como pacote, restauração, instalação e a maioria dos outros cenários que precisam de caminhos de arquivo.</span><span class="sxs-lookup"><span data-stu-id="5b8a5-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="5b8a5-106">Sistema operacional necessário</span><span class="sxs-lookup"><span data-stu-id="5b8a5-106">Required Operating System</span></span>

-   <span data-ttu-id="5b8a5-107">Windows 10 (versão 1607 ou posterior)</span><span class="sxs-lookup"><span data-stu-id="5b8a5-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="5b8a5-108">Windows 10 (versão de 2015 de julho ou 1511) se você atualizar .NET Framework para versões 4.6.2 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="5b8a5-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="5b8a5-109">Windows Server 2016 (todas as versões)</span><span class="sxs-lookup"><span data-stu-id="5b8a5-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="5b8a5-110">Habilitar Política de Grupo de "caminhos longos do Win32"</span><span class="sxs-lookup"><span data-stu-id="5b8a5-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="5b8a5-111">É necessário habilitar o suporte de caminho longo nesses sistemas definindo uma política de grupo.</span><span class="sxs-lookup"><span data-stu-id="5b8a5-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="5b8a5-112">Etapas:</span><span class="sxs-lookup"><span data-stu-id="5b8a5-112">Steps:</span></span>
1. <span data-ttu-id="5b8a5-113">Inicie o **Editor de política de grupo** – digite "Editar política de grupo" na barra Iniciar pesquisa ou execute "gpedit. msc" no comando executar (Windows-R).</span><span class="sxs-lookup"><span data-stu-id="5b8a5-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="5b8a5-114">No **Editor de política de grupo local** , habilite "política do computador local/configuração do computador/Modelos administrativos/todas as configurações/Habilitar caminhos longos do Win32".</span><span class="sxs-lookup"><span data-stu-id="5b8a5-114">In the **Local Group Policy Editor** , enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![Política de caminho longo](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="5b8a5-116">Habilitando outras ferramentas do NuGet para dar suporte a caminhos longos</span><span class="sxs-lookup"><span data-stu-id="5b8a5-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="5b8a5-117">A CLI do dotnet dá suporte a caminhos longos, independentemente do sistema operacional ou da versão.</span><span class="sxs-lookup"><span data-stu-id="5b8a5-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="5b8a5-118">O Visual Studio ou `msbuild -t:restore` ainda não dá suporte a caminhos longos.</span><span class="sxs-lookup"><span data-stu-id="5b8a5-118">Visual Studio or `msbuild -t:restore` does not yet support long paths.</span></span>
> -   <span data-ttu-id="5b8a5-119">O software que usa as bibliotecas do NuGet para executar a restauração e outros comandos oferecerá suporte a caminhos longos nos mesmos sistemas nos quais NuGet.exe funciona, se eles também definirem `longPathAware` em seu manifesto do Windows e configurarem `UseLegacyPathHandling` `false` por meio de App.Config [Ver mais informações](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)</span><span class="sxs-lookup"><span data-stu-id="5b8a5-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set `longPathAware` in their windows manifest and configure `UseLegacyPathHandling` to `false` via App.Config [See more information](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)</span></span>