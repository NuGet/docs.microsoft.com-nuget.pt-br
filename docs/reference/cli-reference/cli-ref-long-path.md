---
title: Suporte a caminhos longos da CLI do NuGet
description: Referência para o suporte de caminho longo do NuGet. exe
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 42b5b7d863d22d7aad99a65700ca11bcc2861db1
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327673"
---
# <a name="long-path-support-nuget-cli"></a>Suporte a caminho longo (CLI do NuGet)

**Aplica-se a:** todas as &bullet; **versões com suporte:** 4.8 +

O NuGet. exe 4,8 e versões posteriores dão suporte a caminhos longos para arquivos e diretórios para cenários como pacote, restauração, instalação e a maioria dos outros cenários que precisam de caminhos de arquivo.

## <a name="required-operating-system"></a>Sistema operacional necessário

-   Windows 10 (versão 1607 ou posterior)
-   Windows 10 (versão de 2015 de julho ou 1511) se você atualizar .NET Framework para versões 4.6.2 ou posterior.
-   Windows Server 2016 (todas as versões)

## <a name="enable-win32-long-paths-group-policy"></a>Habilitar Política de Grupo de "caminhos longos do Win32"

É necessário habilitar o suporte de caminho longo nesses sistemas definindo uma política de grupo.

Tarefas
1. Inicie o **Editor de política de grupo** – digite "Editar política de grupo" na barra Iniciar pesquisa ou execute "gpedit. msc" no comando executar (Windows-R).
2. No **Editor de política de grupo local**, habilite "política do computador local/configuração do computador/Modelos administrativos/todas as configurações/Habilitar caminhos longos do Win32".

![Política de caminho longo](media/LongPathPolicy.png)


> [!Note]
> Habilitando outras ferramentas do NuGet para dar suporte a caminhos longos
>
> -   A CLI do dotnet dá suporte a caminhos longos, independentemente do sistema operacional ou da versão.
> -   O Visual Studio ou o MSBuild-t:Restore ainda não dá suporte a caminhos longos.
> -   O software que usa as bibliotecas do NuGet para executar a restauração e outros comandos oferecerá suporte a caminhos longos nos mesmos sistemas em que o NuGet. exe funciona, se também definir longPathAware em seu manifesto do Windows e configurar UseLegacyPathHandling como false por meio de App. config [ Veja mais informações](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)

