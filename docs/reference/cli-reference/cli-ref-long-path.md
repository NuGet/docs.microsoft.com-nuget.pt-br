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
# <a name="long-path-support-nuget-cli"></a>Suporte a caminho longo (CLI do NuGet)

**Aplica-se a:** todas as &bullet; **versões com suporte:** 4.8 +

NuGet.exe 4,8 e posteriores dão suporte a caminhos longos para arquivos e diretórios para cenários como pacote, restauração, instalação e a maioria dos outros cenários que precisam de caminhos de arquivo.

## <a name="required-operating-system"></a>Sistema operacional necessário

-   Windows 10 (versão 1607 ou posterior)
-   Windows 10 (versão de 2015 de julho ou 1511) se você atualizar .NET Framework para versões 4.6.2 ou posterior.
-   Windows Server 2016 (todas as versões)

## <a name="enable-win32-long-paths-group-policy"></a>Habilitar Política de Grupo de "caminhos longos do Win32"

É necessário habilitar o suporte de caminho longo nesses sistemas definindo uma política de grupo.

Etapas:
1. Inicie o **Editor de política de grupo** – digite "Editar política de grupo" na barra Iniciar pesquisa ou execute "gpedit. msc" no comando executar (Windows-R).
2. No **Editor de política de grupo local** , habilite "política do computador local/configuração do computador/Modelos administrativos/todas as configurações/Habilitar caminhos longos do Win32".

![Política de caminho longo](media/LongPathPolicy.png)


> [!Note]
> Habilitando outras ferramentas do NuGet para dar suporte a caminhos longos
>
> -   A CLI do dotnet dá suporte a caminhos longos, independentemente do sistema operacional ou da versão.
> -   O Visual Studio ou `msbuild -t:restore` ainda não dá suporte a caminhos longos.
> -   O software que usa as bibliotecas do NuGet para executar a restauração e outros comandos oferecerá suporte a caminhos longos nos mesmos sistemas nos quais NuGet.exe funciona, se eles também definirem `longPathAware` em seu manifesto do Windows e configurarem `UseLegacyPathHandling` `false` por meio de App.Config [Ver mais informações](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)