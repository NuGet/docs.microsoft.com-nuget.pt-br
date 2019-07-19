---
title: Plug-in de autenticação multiplataforma do NuGet
description: Plugins de autenticação entre plataformas NuGet para NuGet. exe, dotnet. exe, MSBuild. exe e Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: a716737343ea826d28da6de46c32ca73aef590bd
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317272"
---
# <a name="nuget-cross-platform-authentication-plugin"></a>Plug-in de autenticação multiplataforma do NuGet

Na versão 4.8 +, todos os clientes NuGet (NuGet. exe, Visual Studio, dotnet. exe e MSBuild. exe) podem usar um plug-in de autenticação criado sobre o modelo de [plug-ins entre plataformas do NuGet](NuGet-Cross-Platform-Plugins.md) .

## <a name="authentication-in-dotnetexe"></a>Autenticação no dotnet. exe

O Visual Studio e o NuGet. exe são, por padrão, interativos. O NuGet. exe contém uma opção para torná-lo [não interativo](../nuget-exe-CLI-Reference.md).
Além disso, os plug-ins NuGet. exe e do Visual Studio solicitam a entrada do usuário.
No dotnet. exe, não há solicitação e o padrão não é interativo.

O mecanismo de autenticação no dotnet. exe é o fluxo do dispositivo. Quando a operação de restauração ou adição de pacote é executada interativamente, a operação bloqueia e instruções para o usuário como concluir as autenticações serão fornecidas na linha de comando.
Quando o usuário concluir a autenticação, a operação continuará.

Para tornar a operação interativa, uma delas deve `--interactive`ser aprovada.
Atualmente, somente os `dotnet restore` comandos `dotnet add package` explícitos e são compatíveis com um comutador interativo.
Não há nenhum comutador interativo `dotnet build` em `dotnet publish`e.

## <a name="authentication-in-msbuild"></a>Autenticação no MSBuild

Semelhante ao dotnet. exe, o MSBuild. exe é, por padrão, não interativo, o mecanismo de autenticação do MSBuild. exe é o fluxo do dispositivo.
Para permitir que a restauração Pause e aguarde a autenticação, chame Restore `msbuild -t:restore -p:NuGetInteractive="true"`with.

## <a name="creating-a-cross-platform-authentication-plugin"></a>Criando um plug-in de autenticação de plataforma cruzada

Uma implementação de exemplo pode ser encontrada no [plugin do provedor de credenciais da Microsoft](https://github.com/Microsoft/artifacts-credprovider).

É muito importante que os plug-ins estejam em conformidade com os requisitos de segurança definidos pelas ferramentas de cliente do NuGet.
A versão mínima necessária para um plug-in ser um plug-in de autenticação é *2.0.0*.
O NuGet executará o handshake com o plug-in e consultará as declarações de operação com suporte.
Consulte as [mensagens do protocolo](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) plugin entre plataformas do NuGet para obter mais detalhes sobre as mensagens específicas.

O NuGet definirá o nível de log e fornecerá informações de proxy para o plug-in, quando aplicável.
O log no console do NuGet só é aceitável depois que o NuGet tiver definido o nível de log para o plug-in.

- Comportamento de autenticação do plug-in .NET Framework

No .NET Framework, os plug-ins podem solicitar a entrada de um usuário, na forma de uma caixa de diálogo.

- Comportamento de autenticação do plug-in do .NET Core

No .NET Core, uma caixa de diálogo não pode ser mostrada. Os plug-ins devem usar o fluxo do dispositivo para autenticar.
O plug-in pode enviar mensagens de log para o NuGet com instruções para o usuário.
Observe que o registro em log está disponível depois que o nível de log foi definido para o plug-in.
O NuGet não usará nenhuma entrada interativa da linha de comando.

Quando o cliente chama o plug-in com uma obtenção de credenciais de autenticação, os plug-ins precisam estar em conformidade com o comutador de interatividade e respeitam a opção de caixa de diálogo. 

A tabela a seguir resume como o plug-in deve se comportar para todas as combinações.

| IsNonInteractive | Canshowdialog | Comportamento do plug-in |
| ---------------- | ------------- | --------------- |
| true | true | A opção IsNonInteractive tem precedência sobre a opção da caixa de diálogo. O plug-in não tem permissão para exibir uma caixa de diálogo. Essa combinação só é válida para plug-ins .NET Framework |
| true | false | A opção IsNonInteractive tem precedência sobre a opção da caixa de diálogo. O plug-in não tem permissão para bloquear. Essa combinação só é válida para plug-ins do .NET Core |
| false | true | O plug-in deve mostrar uma caixa de diálogo. Essa combinação só é válida para plug-ins .NET Framework |
| false | false | O plug-in deve/não pode mostrar uma caixa de diálogo. O plug-in deve usar o fluxo do dispositivo para autenticar ao registrar uma mensagem de instrução por meio do agente. Essa combinação só é válida para plug-ins do .NET Core |

Veja as especificações a seguir antes de gravar um plug-in.

- [Plug-in de download do pacote NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [Plug-in de autenticação entre Plat do NuGet](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
