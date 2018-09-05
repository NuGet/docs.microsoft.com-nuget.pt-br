---
title: Suporte ao caminho longo de CLI do NuGet
description: Referência para suporte de caminho longos nuget.exe
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 7cd387e3eb05d149da9a88cc1c76dc08588d04b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547820"
---
# <a name="long-path-support-nuget-cli"></a>Suporte a caminhos longos (CLI do NuGet)

**Aplica-se a:** todos os &bullet; **versões com suporte:** 4.8 +

Suporte 4,8 e versões posteriores de NuGet.exe caminhos longos para arquivos e diretórios para cenários como o pacote, restauração, instalação e a maioria dos outros cenários que precisam de caminhos de arquivo.

## <a name="required-operating-system"></a>Sistema operacional necessário

-   Windows 10 (versão 1607 ou posterior)
-   Windows 10 (versão de julho de 2015 ou versão 1511) se você atualizar o .NET Framework para as versões 4.6.2 ou posterior.
-   Windows Server 2016 (todas as versões)

## <a name="enable-win32-long-paths-group-policy"></a>Habilitar política de grupo "Caminhos longos do Win32"

É necessário habilitar o suporte de caminho longos nesses sistemas, definindo uma política de grupo.

Etapas:
1. Inicie **Editor de diretiva de grupo** - digite "Editar política de grupo" na barra de pesquisa do início ou executado "gpedit. msc" no comando executar (Windows-R).
2. No **Editor de diretiva de Grupo Local**, habilite "modelos substitui qualquer configuração de diretiva de computador de computador locais/todos os caminhos longos de configurações/Habilitar Win32".

![Diretiva de caminho longo](media/LongPathPolicy.png)


> [!Note]
> Habilitando a outras ferramentas do NuGet dar suporte a caminhos longos
>
> -   Dotnet CLI dá suporte a caminhos longos, independentemente do sistema operacional ou versão.
> -   Ainda não há suporte para caminhos longos no Visual Studio ou o msbuild /t: Restore.
> -   Software que usa bibliotecas NuGet para executar outros comandos, e a restauração será dão suporte a caminhos longos nos mesmos sistemas que NuGet.exe funciona no, se eles também definem longPathAware em suas janelas de manifesto e configurar o UseLegacyPathHandling como falso por meio do App. config [ Obter mais informações](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)

