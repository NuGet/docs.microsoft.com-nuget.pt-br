---
title: NuGet cross plug-in de autenticação de plataforma
description: NuGet cross plug-ins de autenticação de plataforma para NuGet.exe, dotnet.exe, msbuild.exe e Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: d80339eb81ade1cf2c323a604cc4fac06dcb1012
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981048"
---
# <a name="nuget-cross-platform-authentication-plugin"></a>NuGet cross plug-in de autenticação de plataforma

Na versão 4.8 + NuGet todos os clientes (NuGet.exe, Visual Studio, dotnet.exe e MSBuild.exe) podem usar um plug-in de autenticação criado na parte superior dos [NuGet cruzada plugins de plataforma](NuGet-Cross-Platform-Plugins.md) modelo.

## <a name="authentication-in-dotnetexe"></a>Autenticação no dotnet.exe

O Visual Studio e NuGet.exe são por padrão interativo. NuGet.exe conterá um comutador para torná-lo [não interativo](../../tools/nuget-exe-CLI-Reference.md).
Além disso, os plug-ins NuGet.exe e o Visual Studio solicitará a entrada do usuário.
Dotnet.exe não há nenhum aviso e o padrão é não interativo.

O mecanismo de autenticação no dotnet.exe é o fluxo do dispositivo. Quando a restauração ou adicionar a operação de pacote é executada interativamente, os blocos de operação e se as instruções para o usuário como concluída as autenticações serão ser fornecidas na linha de comando.
Quando o usuário conclui a autenticação continuará a operação.

Para que a operação interativa, um deve passar `--interactive`.
Atualmente, apenas explícito `dotnet restore` e `dotnet add package` comandos dão suporte a um comutador interativo.
Não há nenhuma opção interativa na `dotnet build` e `dotnet publish`.

## <a name="authentication-in-msbuild"></a>Autenticação no MSBuild

Semelhante ao dotnet.exe, MSBuild.exe é por padrão, não que é o mecanismo de autenticação MSBuild.exe interativo fluxo do dispositivo.
Para permitir que a restauração pause e aguarde para autenticação, chame a restauração com `msbuild /t:restore /p:NuGetInteractive="true"`.

## <a name="creating-a-cross-platform-authentication-plugin"></a>Criando um plug-in de autenticação de plataforma cruzada

Uma implementação de exemplo pode ser encontrada no [plug-in do provedor de credenciais do Microsoft](https://github.com/Microsoft/artifacts-credprovider).

É muito importante que os plug-ins está em conformidade com os requisitos de segurança estabelecidos pelas ferramentas de cliente do NuGet.
O mínimo necessário é de versão para um plug-in ser um plug-in de autenticação *2.0.0*.
NuGet executará o handshake com o plug-in e a consulta para as declarações de operação com suporte.
Consulte o NuGet cruzada plug-in de plataforma [mensagens de protocolo](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) para obter mais detalhes sobre as mensagens específicas.

O NuGet será definir o nível de log e fornecer informações de proxy para o plug-in quando aplicável.
Registro em log para o NuGet console só é aceitável após NuGet tiver definido o nível de log para o plug-in.

- Comportamento de autenticação de plug-in do .NET framework

No .NET Framework, os plug-ins são permitidos para solicitar que um usuário para entrada, na forma de uma caixa de diálogo.

- Comportamento de autenticação de plug-in do .NET core

No .NET Core, não é possível mostrar uma caixa de diálogo. Os plug-ins devem usar o fluxo do dispositivo para autenticar.
O plug-in pode enviar mensagens de log para o NuGet com instruções para o usuário.
Observe que o registro em log está disponível depois que o nível de log tiver sido definido para o plug-in.
O NuGet não terão qualquer entrada interativa da linha de comando.

Quando o cliente chama o plug-in com uma obter credenciais de autenticação, os plug-ins precisam estar de acordo com a opção de interatividade e respeita a opção de caixa de diálogo. 

A tabela a seguir resume como o plug-in deve se comportar para todas as combinações.

| IsNonInteractive | CanShowDialog | Comportamento de plug-in |
| ---------------- | ------------- | --------------- |
| true | true | O comutador IsNonInteractive tem precedência sobre a opção de caixa de diálogo. O plug-in não é permitido para mostrar uma caixa de diálogo. Essa combinação só é válida para o plug-ins do .NET Framework |
| true | false | O comutador IsNonInteractive tem precedência sobre a opção de caixa de diálogo. O plug-in não tem permissão para bloquear. Essa combinação só é válida para o plug-ins do .NET Core |
| false | true | O plug-in deve mostrar uma caixa de diálogo. Essa combinação só é válida para o plug-ins do .NET Framework |
| false | false | O plug-in deve/pode não mostrar uma caixa de diálogo. O plug-in deve usar o fluxo do dispositivo para autenticar pelo registro em log uma mensagem de instrução por meio do agente de log. Essa combinação só é válida para o plug-ins do .NET Core |

Consulte as especificações a seguir antes de escrever um plug-in.

- [Plug-in de Download de pacote do NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [NuGet cruzada plug-in de autenticação de várias plataformas](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
